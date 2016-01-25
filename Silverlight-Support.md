_Note: The Silverlight Support has not been migrated yet to SpecFlow v2. Silverlight projects needs to be tested with SpecFlow 1.9 currently._

* Install [Silverlight Toolkit](http://silverlight.codeplex.com/).
It comes with the  SL Unit Test Framework (http://code.msdn.microsoft.com/silverlightut)
* In your solution add a "Silverlight Unit Test Application" project. This adds a Silverlight Application project with the tests and a web project to the solution. The former is the test project, where the feature files and step definitions should be added. The latter hosts the test project to execute it in the browser.
* Add an app.config to the project (even if it's not supported by SL), with the following content:

```xml
<?xml version="1.0" encoding="utf-8" ?>
 <configuration>
  <configSections>
    <section name="specFlow" type="TechTalk.SpecFlow.Configuration.ConfigurationSectionHandler, TechTalk.SpecFlow"/>
  </configSections>
  <specFlow>
    <unitTestProvider name="MsTest.Silverlight" />
  </specFlow>
</configuration>
```

This'll get the generator to create MsTest + silverlight-compatible c# files for every feature file you add.

* Add a reference to TechTalk.Specflow.Silverlight3.dll to the test project.
* Add the following command to the Pre-build event commands of the project found in "Project Properties -> Build Events".

```
{SpecFlow-tools-path}\SpecFlow.exe generateAll $(ProjectName) /force /verbose
```

* Add feature files and step definitions to the test project. You can use the templates in "Add -> New Item..." for that.
* Set the web project as your startup project. Execute it. You should see the result of the test execution displayed in the browser.