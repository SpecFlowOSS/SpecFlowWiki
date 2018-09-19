_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Context-Injection]]. We use the GitHub wiki for authoring the documentation pages._

SpecFlow supports a very simple dependency framework that is able to instantiate and inject class instances for the scenarios. With this feature you can group the shared state to context-classes, and inject them into every binding class that is interested in that shared state.

To use context injection, you have to

1. Create your POCOs (simple .NET classes) representing the shared data
2. Define them as constructor parameters in every binding class you need them
3. Save the constructor argument to instance fields, so you can use them in the step definitions

Rules:

* The life-time of these objects are limited to a scenario execution. 
* If the injected objects implement `IDisposable`, they will be disposed after the scenario execution.
* The injection is resolved recursively, i.e. the injected class can also have dependencies. 
* The resolution is done using the public constructors only. 
* If there are multiple public constructors, SpecFlow takes the first one.

The container used by SpecFlow can be customized, e.g. you can include object instances created already or modify the resolution rules. See the _Advanced options_ section below for details.

## Examples

In the first example we define a POCO for holding the data of a person and use it in a _given_ and a _then_ step that are placed in different binding classes.

```c#
public class PersonData // the POCO for sharing person data
{ 
  public string FirstName;
  public string LastName;
}

[Binding]
public class MyStepDefs
{
  private readonly PersonData personData;
  public MyStepDefs(PersonData personData) // use it as ctor parameter
  { 
    this.personData = personData;
  }
  
  [Given] 
  public void The_person_FIRSTNAME_LASTNAME(string firstName, string lastName) 
  {
    personData.FirstName = firstName; // write into the shared data
    personData.LastName = lastName;
    //... do other things you need
  }
}

[Binding]
public class OtherStepDefs // another binding class needing the person
{ 
  private readonly PersonData personData;
  public OtherStepDefs(PersonData personData) // ctor parameter here too
  { 
    this.personData = personData;
  }
  
  [Then] 
  public void The_person_data_is_properly_displayed() 
  {
    var displayedData = ... // get the displayed data from the app
      // read from shared data, to perform assertions
    Assert.AreEqual(personData.FirstName + " " + personData.LastName, 
      displayedData, "Person name was not displayed properly");
  }
}
```

The following example defines a context class to store referred books. The context class is injected to a binding class.

```c#
public class CatalogContext
{
    public CatalogContext()
    {
        ReferenceBooks = new ReferenceBookList();
    }

    public ReferenceBookList ReferenceBooks { get; set; }
}

[Binding]
public class BookSteps
{
    private readonly CatalogContext _catalogContext;

    public BookSteps(CatalogContext catalogContext)
    {
        _catalogContext = catalogContext;
    }

    [Given(@"the following books")]
    public void GivenTheFollowingBooks(Table table)
    {
        foreach (var book in table.CreateSet<Book>())
        {
            SaveBook(book);
            _catalogContext.ReferenceBooks.Add(book.Id, book);
        }
    }
}
```

## Advanced options

The container used by SpecFlow can be customized, e.g. you can include object instances created already or modify the resolution rules. 

The customization of the container can be done from a [[plugin|Plugins]] or a before scenario [[hook|hooks]]. The class, that wants to customize the injection rules has to obtain an instance of the scenario execution container (an instance of `BoDi.IObjectContainer`). This can be done through constructor injection (see example below) or by calling `ScenarioContext.Current.GetBindingInstance(typeof(BoDi.IObjectContainer))`.

The following example adds the Selenium web driver to the container, so that binding classes can specify `IWebDriver` dependencies (a constructor argument of type `IWebDriver`).

```c#
[Binding]
public class WebDriverSupport
{
  private readonly IObjectContainer objectContainer;

  public WebDriverSupport(IObjectContainer objectContainer)
  {
    this.objectContainer = objectContainer;
  }

  [BeforeScenario]
  public void InitializeWebDriver()
  {
    var webDriver = new FirefoxDriver();
    objectContainer.RegisterInstanceAs<IWebDriver>(webDriver);
  }
}
```

## Custom Dependency Injection Frameworks

As mentioned the default SpecFlow container is `IObjectContainer` which is recommended for most scenarios, however you may have situations where you need slightly more control over the DI config, or make use of existing DI configuration within the project you are testing, i.e pulling in service layers for assisting with assertions in `Then` stages.

### Consuming existing plugins
- [SpecFlow.Autofac](https://github.com/gasparnagy/SpecFlow.Autofac)
- [SpecFlow.Unity](https://github.com/phatcher/SpecFlow.Unity)
- [SpecFlow.Ninject](https://github.com/MattMcKinney/SpecFlow.Ninject) (currently not on nuget)

To make use of these plugins you need to add a reference and add in your specflow configuration section:

```xml
<specFlow>
  <plugins>
    <add name="SpecFlow.Autofac" type="Runtime" />
  </plugins>
  <!-- Anything else -->
</specFlow>
```
This will tell SpecFlow to load the runtime plugin and will allow you to create an entry point to make use of this functionality like [shown in the autofac example](https://github.com/gasparnagy/SpecFlow.Autofac/blob/master/sample/MyCalculator/MyCalculator.Specs/Support/TestDependencies.cs). Once setup your dependencies will be injected into steps and bindings like they were with the `IObjectContainer`, but behind the scenes it will be pulling those dependencies from the DI container you have added.

> One thing to note here is that each plugin has its own conventions for loading the entry point, this is often a static class with a static method containing an attribute that is marked by the specific plugin, check with each plugins example to see what their example usage looks like

You can load all your dependencies within this handler section or if you wish you are able to inject the relevant IoC container into your binding sections like so:

```csharp
[Binding]
public class WebDriverPageHooks
{
    private readonly IKernel _kernel;

    // Inject in our container (using Ninject here)
    public WebDriverPageHooks(IKernel kernel)
    { _kernel = kernel; }
    
    private IWebDriver SetupWebDriver()
    {
        var options = new ChromeOptions();
        options.AddArgument("--start-maximized");
        options.AddArgument("--disable-notifications");
        return new ChromeDriver(options);
    }

    [BeforeScenario]
    public void BeforeScenario()
    {
        var webdriver = SetupWebDriver();        
        _kernel.Bind<IWebDriver>().ToConstant(webdriver);
    }

    [AfterScenario]
    public void AfterScenario()
    {
        var webDriver = _kernel.Get<IWebDriver>();
        
        // Output any screenshots or log dumps etc
        
        webDriver.Close();
        webDriver.Dispose();
    }
}
```

This allows you the option to either load types up front or create types within your binding sections so you are able to dispose of them in a defined way.

### Creating your own

It is best to look at the autofac example and the [plugins documentation](https://specflow.org/documentation/Plugins/) and follow its conventions.

> Just remember to adhere to the plugin documentation and have your assembly end in `.SpecFlowPlugin` i.e `SpecFlow.AutoFac.SpecFlowPlugin`, your internal namespaces can be anything you want but the assembly name is important or SpecFlow will be unable to find it.