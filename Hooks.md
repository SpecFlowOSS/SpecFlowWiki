_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Hooks]]. We use the GitHub wiki for authoring the documentation pages._

The hooks (event bindings) can be used to perform additional automation logic on specific events, like before the execution of a scenario.

The hooks are global but can be restricted to run only for features or scenarios with a specific [[tag]] (see below). The execution order of hooks for the same event is undefined.

##Supported Hook Attributes

<table>
    <tr>
        <th>Attribute</th>
        <th>Tag filtering</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>[BeforeTestRun]<br/>[AfterTestRun]</td>
        <td>-</td>
        <td>automation logic that has to run before/after the entire test run<br/>
<i>Note: As the most of the unit test runners do not provide a hook for executing logic after the test execution has been finished, the [AfterTestRun] event is triggered by the test assembly unload event. The exact timing and thread of this execution might be different for each test runner.</i><br/>
The method it is applied to must be static.
</td>
    </tr>
    <tr>
        <td>[BeforeFeature]<br/>[AfterFeature]</td>
        <td>+</td>
        <td>automation logic that has to run before/after executing each feature<br/>
The method it is applied to must be static.</td>
    </tr>
    <tr>
        <td>[BeforeScenario] or [Before]<br/>[AfterScenario] or [After]</td>
        <td>+</td>
        <td>automation logic that has to run before/after executing each scenario or scenario outline example<br/>
            The short attribute names are available from v1.8.</td>
    </tr>
    <tr>
        <td>[BeforeScenarioBlock]<br/>[AfterScenarioBlock]</td>
        <td>+</td>
        <td>automation logic that has to run before/after executing each scenario block (e.g. between the "givens" and the "whens")</td>
    </tr>
    <tr>
        <td>[BeforeStep]<br/>[AfterStep]</td>
        <td>+</td>
        <td>automation logic that has to run before/after executing each scenario step</td>
    </tr>
</table>

You can annotate a single method with multiple attributes.

##Tag Filtering

Most of the hooks support tag filtering. This means that they are executed only if the feature or the scenario has at least one of the tags specified in the tag filter (so the tags are combined with OR). The tag can be made by specifying the tag in the attribute or with [[Scoped Bindings]] (from v1.8).

The following example starts Selenium for scenarios marked with `@web` tag.

```c#
[BeforeScenario("web")]
public static void BeforeWebScenario()
{
    StartSelenium();
}
```

For the scenario, scenarioblock or step events, the following tags are considered:

* tag on the feature
* tag on the scenario
* tag on the scenario outline
* tag on the scenario outline example set (`Examples:`)

For more complex filtering the [[ScenarioContext]] class can be used. The following example starts selenium if the scenario is tagged with `@web` _and_ `@automated`.


```c#
[BeforeScenario("web")]
public static void BeforeWebScenario()
{
    if(ScenarioContext.Current.ScenarioInfo.Tags.Contains("automated"))
        StartSelenium();
}
```

