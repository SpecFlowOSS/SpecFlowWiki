SpecFlow supports several unit test framework to execute the acceptance tests. Use can use one of the built-in unit test providers or create a custom provider. The unit test provider to be used can be configured through the [[&lt;unitTestProvider&gt;|Configuration]] configuration element.

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
        <td>See [[http://www.nunit.org]].</td>
    </tr>
    <tr>
        <td>MsTest</td>
        <td>-</td>
        <td>-</td>
        <td>+</td>
        <td>MsTest provider for .Net 3.5</td>
    </tr>
    <tr>
        <td>MsTest.2010</td>
        <td>-</td>
        <td>+</td>
        <td>+</td>
        <td>MsTest provider for .Net 4.0. Supporting test-categories.</td>
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
        <td>See [[http://www.xunit.net]].</td>    
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
