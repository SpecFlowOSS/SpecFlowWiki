The bindings ([[step definitions]], [[hooks]], etc.) provide the connection between the free-text specification and the application interfaces (see [[Bindings]]). For better reusability, the step definitions can be parametrized. This means that it is not necessary to define a new step definition for each step that just differs in a small portion.  E.g. the steps `When I perform a simple search on 'Domain'` and `When I perform a simple search on 'Communication'` can be automated with a single step definition. 

The following example shows a simple step definition that matches to the step `When I perform a simple search on 'Domain'` mentioned earlier. 

```c#
[When(@"I perform a simple search on '(.*)'")]
public void WhenIPerformASimpleSearchOn(string searchTerm)
{
    var controller = new CatalogController();
    actionResult = controller.Search(searchTerm);
}
```

Here the method is annotated with the `[When]` attribute, providing the regular expression to be used to match the step text. The match groups (`(…)`) of the regular expression define the parameters for the method. From SpecFlow v1.9 the step definitions can be also specified without regular expressions. Check the [[step definition styles]] page for details.

##Supported Step Definition Attributes

* `[Given(regex)]` or `[Given]` - `TechTalk.SpecFlow.GivenAttribute`
* `[When(regex)]` or `[When]` - `TechTalk.SpecFlow.WhenAttribute`
* `[Then(regex)]` or `[Then]` - `TechTalk.SpecFlow.ThenAttribute`
* `[StepDefinition(regex)]` or `[StepDefinition]` - `TechTalk.SpecFlow.StepDefinitionAttribute`, matches for given, when or then attributes (from v1.8)

You can annotate a single method with multiple attributes in order to support different phrasings in the feature file for the same automation logic.

```c#
[When(@"I perform a simple search on '(.*)'")]
[When(@"I search for '(.*)'")]
public void WhenIPerformASimpleSearchOn(string searchTerm)
{
  ...
}
```

##Rules for the Step Definition Method

* Must be in a public class, marked with the `[Binding]` attribute.
* Must be a public method.
* Can be either a static or an instance method. If it is an instance method, the containing class will be instantiated once for every scenario.
* Cannot have `out` or `ref` parameters.
* Cannot have a return type. 

##Step Matching Rules
* The rules depend on the step definition style you use. Check the [[step definition styles]] page for the exact rules.

##Parameter Matching Rules

* Step definitions can specify parameters. These will match to the parameters of the step definition method.
* The method parameter type can be `string` or other .NET type. In the later case [[configurable conversion|Step Argument Conversions]] is applied.
* With regular expressions
  * The match groups (`(…)`) of the regular expression define the arguments for the method based on the order (the match result of the first group becomes the first argument, etc.).
  * You can use non-capturing groups `(?:regex)` in order to use groups without a method argument.
* With method name matching
  * You can refer to the method parameters with either the parameter name (ALL-CAPS) or the parameter index (zero-based) with the `P` prefix, e.g. `P0`.

##Table or Multi-line Text Arguments

If the step definition method should match for steps having [[table or multi-line text arguments|Using Gherkin Language in SpecFlow]], additional `Table` and/or `string` parameters have to be defined in the method signature to be able to receive these arguments. If both table and multi-line text argument is used for the step, the multi-line text argument is provided first.

```
Given the following books
  |Author        |Title                          |
  |Martin Fowler |Analysis Patterns              |
  |Gojko Adzic   |Bridging the Communication Gap |
```

```c#
[Given(@"the following books")]
public void GivenTheFollowingBooks(Table table)
{
  ...
}
```

##See also

* [[Step Definition Styles]]
* [[Step Argument Conversions]]
* [[Scoped Bindings]]

