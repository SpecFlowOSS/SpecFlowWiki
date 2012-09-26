SpecFlow supports several unit test framework to execute the acceptance tests. You can use one of the built-in unit test providers or create a custom provider. The unit test provider to be used can be configured through the [[&lt;unitTestProvider&gt;|Configuration]] configuration element.

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
        <td>NUnit</td>
        <td>+</td>
        <td>+</td>
        <td>+</td>
        <td>See [[http://www.nunit.org]]. Specialized [[NuGet packages|NuGet Integration]] available for easy setup: SpecFlow.NUnit, SpecFlow.NUnit.Runners.</td>
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
        <td>MsTest provider for .NET 4.0. Supporting test-categories. (Note:  before SpecFlow v1.9, MsTest was referring to the .NET 3.5 provider.)</td>
    </tr>
    <tr>
        <td>MsTest.Silverlight <br/> MsTest.Silverlight3 <br/> MsTest.Silverlight4</td>
        <td>-</td>
        <td>+</td>
        <td>+</td>
        <td>Silverlight Unit Test Framework [[http://code.msdn.microsoft.com/silverlightut]]. See [[Silverlight Support]].</td>
    </tr>
    <tr>
        <td>MsTest.WindowsPhone7</td>
        <td>-</td>
        <td>+</td>
        <td>+</td>
        <td>See [[Windows Phone 7 Support]].</td>
    </tr>
    <tr>
        <td>xUnit</td>
        <td>+</td>
        <td>-</td>
        <td>-</td>
        <td>See [[http://www.xunit.net]]. Specialized [[NuGet package|NuGet Integration]] available for easy setup: SpecFlow.xUnit.</td>    
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
    <tr>
        <td>SpecRun <br/> SpecRun+NUnit <br/> SpecRun+MsTest</td>
        <td>+</td>
        <td>+</td>
        <td>+</td>
        <td>SpecRun provider. See [[http://www.specrun.com]]. Requires SpecRun plugin NuGet package: SpecRun.SpecFlow</td>    
    </tr>
</table>
