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

##Examples

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
public class OtherStepDefs{ // another binding class needing the person
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

##Advanced options

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
