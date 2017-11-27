_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Unit-test-providers]]. We use the GitHub wiki for authoring the documentation pages._

SpecFlow supports several unit test framework to execute the acceptance tests. You can use one of the built-in unit test providers or create a custom provider. Use the [[&lt;unitTestProvider&gt;|Configuration]] configuration element in your `app.config` file to specify which unit test provide you want to use.

The following table contains the built-in unit test providers.

<table>
    <tr>
        <th rowspan="2">Name</th>
        <th colspan="3">Supports</th>
        <th rowspan="2">Description</th>
    </tr>
    <tr>
        <th>row tests</th>
        <th>categories</th>
        <th>inconclusive</th>
    </tr>
    <tr>
        <td>SpecFlow+ Runner (fka SpecRun)</td>
        <td>+</td>
        <td>+</td>
        <td>+</td>
        <td>[[SpecFlow+ Runner|http://www.specflow.org/plus/runner/]] is a dedicated test execution framework for SpecFlow. Install it with the SpecRun.SpecFlow NuGet package. See [[SpecRun Integration]] for details.</td>
    </tr>
    <tr>
        <td>NUnit</td>
        <td>+</td>
        <td>+</td>
        <td>+</td>
        <td>See [[http://www.nunit.org]]. Specialized [[NuGet packages|NuGet Integration]] available for easy setup: SpecFlow.NUnit, SpecFlow.NUnit.Runners. Supports parallel execution with NUnit v3. </td>
    </tr>
    <tr>
        <td>MsTest.2008</td>
        <td>-</td>
        <td>-</td>
        <td>+</td>
        <td>MsTest provider for .NET 3.5</td>
    </tr>
    <tr>
        <td>MsTest <br/> MsTest.2010</td>
        <td>-</td>
        <td>+</td>
        <td>+</td>
        <td>MsTest provider for .NET 4.0. Supports test categories. Specialized [[NuGet package|NuGet Integration]] available for easy setup: SpecFlow.MsTest.</td>
    </tr>
    <tr>
        <td>xUnit</td>
        <td>+</td>
        <td>-</td>
        <td>-</td>
        <td>See [[http://www.xunit.net]]. Specialized [[NuGet package|NuGet Integration]] available for easy setup: SpecFlow.xUnit. Supports parallel execution with xUnit v2.</td>    
    </tr>
    <tr>
        <td>mbUnit</td>
        <td>+</td>
        <td>+</td>
        <td>+</td>
        <td>MbUnit provider. See [[http://www.mbunit.com]].</td>    
    </tr>    
    <tr>
        <td>mbUnit.3</td>
        <td>+</td>
        <td>+</td>
        <td>+</td>
        <td>MbUnit Version 3 provider. See [[http://www.mbunit.com]].</td>    
    </tr>
</table>
