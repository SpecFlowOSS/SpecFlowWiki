_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Hooks]]. We use the GitHub wiki for authoring the documentation pages._

Hooks (event bindings) can be used to perform additional automation logic at specific times, such as before executing a scenario. In order to use hooks, you need to add the `Binding` attribute to your class:

```
[Binding]
public class MyClass
{
    ...
}

```

Hooks are global, but can be restricted to run only for features or scenarios with a specific tag by defining a [[scoped binding|scoped-bindings]]. The execution order of hooks for the same event is undefined.

## Supported Hook Attributes

<table>
    <tr>
        <th>Attribute</th>
        <th>Tag filtering</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>[BeforeTestRun]<br/>[AfterTestRun]</td>
        <td>-</td>
        <td>Automation logic that has to run before/after the entire test run<br/>
<i>Note: As most of the unit test runners do not provide a hook for executing logic once the tests have been executed, the [AfterTestRun] event is triggered by the test assembly unload event. The exact timing and thread of this execution may therefore differ for each test runner.</i><br/>
The method it is applied to must be static.
</td>
    </tr>
    <tr>
        <td>[BeforeFeature]<br/>[AfterFeature]</td>
        <td>+</td>
        <td>Automation logic that has to run before/after executing each feature<br/>
The method it is applied to must be static.</td>
    </tr>
    <tr>
        <td>[BeforeScenario] or [Before]<br/>[AfterScenario] or [After]</td>
        <td>+</td>
        <td>Automation logic that has to run before/after executing each scenario or scenario outline example<br/>
            Short attribute names are available from v1.8.</td>
    </tr>
    <tr>
        <td>[BeforeScenarioBlock]<br/>[AfterScenarioBlock]</td>
        <td>+</td>
        <td>Automation logic that has to run before/after executing each scenario block (e.g. between the "givens" and the "whens")</td>
    </tr>
    <tr>
        <td>[BeforeStep]<br/>[AfterStep]</td>
        <td>+</td>
        <td>Automation logic that has to run before/after executing each scenario step</td>
    </tr>
</table>

You can annotate a single method with multiple attributes.

## Hook Execution Order

By default the hooks of the same type (e.g. two `[BeforeScenario]` hook) are executed in an unpredictable order. If you need to ensure a specific execution order, you can specify the `Order` property for the hook attributes.

```c#
[BeforeScenario(Order = 0)]
public void CleanDatabase()
{
    // we need to run this first
}

[BeforeScenario(Order = 100)]
public void LoginUser()
{
    // we can perform login based on a clean database
}
```

The value provided for the order attribute specifies the order, not the priority, ie. the hook with the lower number always executed earlier both for before and after hooks.

If no order is specified, the default order of 1000 is used. It is not recommended to depend on this default value though.

## Tag Scoping

Most hooks support tag scoping, which means they are executed only if the feature or the scenario has *at least one* of the tags specified in the tag filter (tags are combined with OR). You can specify the tag in the attribute or using [[scoped bindings]].
