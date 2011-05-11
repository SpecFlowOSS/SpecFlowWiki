Step bindings are global for the entire SpecFlow project. This means that a step binding that is bound to a very generic step text, like ``When I save the changes`` becomes challenging to implement. The general solution for this problem is to phrase the scenarios in a way that the steps are phrased in a way that the usage context can be extracted from them (e.g. ``When I save the book details``).

In some cases however, it is necessary to restrict the appliance of a step binding based on certain conditions. The "scoped steps" feature of SpecFlow can be used for this purpose.

The scoped steps can restrict the execution for 

* feature (by feature title)
* scenario (by scenario title)
* tag

The scope can be defined with the `[StepScope]` attribute:

```c#
[StepScope(Tag = "mytag", Feature = "feature title", Scenario = "scenario title")] 
```

##Scoped Step Rules:

* The scope can be defined on binding method or on binding class level.
* If multiple criteria (e.g. tag and feature) is specified in the same attribute, these are combined with AND.
* If `[StepScope]` attribute is placed on the same method or class, these are combined with OR.
* If a step matches for a step binding without scope and a scoped step binding, the scoped step will be used (no ambiguity).
* If a step matches for two scoped step bindings, the one with the most restriction is used. 
* Multiple scoped step binding with the maximal restriction causes an ambiguous step binding error.

##Examples

The following example shows the different binding for the same step depending on whether UI automation or controller automation has to be done.

```c#
[When(@"I perform a simple search on '(.*)'", StepScope(Tag = "controller"))]
public void WhenIPerformASimpleSearchOn(string searchTerm)
{
    var controller = new CatalogController();
    actionResult = controller.Search(searchTerm);
}

[When(@"I perform a simple search on '(.*)'"), StepScope(Tag = "web")]
public void PerformSimpleSearch(string title)
{
    selenium.GoToThePage("Home");
    selenium.Type("searchTerm", title);
    selenium.Click("searchButton");
}
```

The following example shows a way to "ignore" executing the scenarios marked with `@manual` (the SpecFlow tracing will still display the steps, so the manual scenarios can be checked based on the report).

```c#
[Binding, StepScope(Tag = "manual")]
public class ManualSteps
{
    [Given(".*"), When(".*"), Then(".*")]
    public void EmptyStep()
    {
    }

    [Given(".*"), When(".*"), Then(".*")]
    public void EmptyStep(string multiLineStringParam)
    {
    }

    [Given(".*"), When(".*"), Then(".*")]
    public void EmptyStep(Table tableParam)
    {
    }
}
```