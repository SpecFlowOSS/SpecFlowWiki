# Scoped Bindings

## Page History
Bindings (step definitions, hooks) are global for the entire SpecFlow project. This means that a step definition that is bound to a very generic step text, like When I save the changes becomes challenging to implement. The general solution for this problem is to phrase the scenarios in a way that the steps are phrased in a way that the usage context can be extracted from them (e.g. When I save the book details).

In some cases however, it is necessary to restrict the appliance of a step definition or hook based on certain conditions. This feature of SpecFlow can be used for this purpose.

*Be careful!* Coupling your step definitions to the features is an anti-pattern. [Read more about it on the Cucumber Wiki](https://github.com/cucumber/cucumber/wiki/Feature-Coupled-Step-Definitions-%28Antipattern%29)

The scoped bindings can restrict the execution for

* feature (by feature title)
* scenario (by scenario title)
* tag

The scope can be defined with the `[Scope]` attribute. (Prior to v1.8, scopes has to be specified with the `[StepScope]` attribute.)

    [Scope(Tag = "mytag", Feature = "feature title", Scenario = "scenario title")] 

## Scoping Rules:

The scope can be defined on method or on class level.

If multiple criteria (e.g. tag and feature) is specified in the same attribute, these are combined with AND.

If `[Scope]` attribute is placed on the same method or class, these are combined with OR.

If a step matches for a step definition without scope and also to a scoped step definition, the scoped step definition will be used (no ambiguity).

If a step matches for two different scoped step definitions, the one with the most restriction is used.
Multiple scoped step definition with the maximal restriction causes an ambiguous step binding error.
Examples

The following example shows the different step definition for the same step depending on whether UI automation or controller automation has to be done.

    [When(@"I perform a simple search on '(.*)'", Scope(Tag = "controller"))]
    public void WhenIPerformASimpleSearchOn(string searchTerm)
    {
        var controller = new CatalogController();
        actionResult = controller.Search(searchTerm);
    }

    [When(@"I perform a simple search on '(.*)'"), Scope(Tag = "web")]
    public void PerformSimpleSearch(string title)
    {
        selenium.GoToThePage("Home");
        selenium.Type("searchTerm", title);
        selenium.Click("searchButton");
    }
The following example shows a way to "ignore" executing the scenarios marked with `@manual` (the SpecFlow tracing will still display the steps, so the manual scenarios can be checked based on the report).

    [Binding, Scope(Tag = "manual")]
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