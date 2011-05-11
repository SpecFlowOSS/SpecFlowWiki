The event bindings can be used to perform additional automation logic on specific events, like before the execution of a scenario.

The event bindings are global but can be restricted to run only for features or scenarios with a specific [[tag]]. The execution order of event bindings for the same event is undefined.

##Supported Event Binding Attributes

<table>
    <tr>
        <th>Attribute</th>
        <th>Tag filtering</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>[BeforeTestRun]<br/>[AfterTestRun]</td>
        <td>-</td>
        <td>automation logic that has to run before/after the entire test run</td>
    </tr>
    <tr>
        <td>[BeforeFeature]<br/>[AfterFeature]</td>
        <td>+</td>
        <td>automation logic that has to run before/after executing each feature</td>
    </tr>
    <tr>
        <td>[BeforeScenario]<br/>[AfterScenario]</td>
        <td>+</td>
        <td>automation logic that has to run before/after executing each scenario or scenario outline example</td>
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

Most of the event bindings support tag filtering. This means that they are executed only if the feature or the scenario has at least one of the tags specified in the tag filter (so the tags are combined with OR).

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

