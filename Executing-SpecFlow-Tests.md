_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Executing-SpecFlow-Tests]]. We use the GitHub wiki for authoring the documentation pages._

With SpecFlow you can define the acceptance criteria in feature files that can be executed. These tests are usually placed in a separate project in the solution (e.g. "BookShop.AcceptanceTests" in the [[BookShop sample|Examples]]).

SpecFlow generates executable unit tests from the defined acceptance criteria (called [[scenarios|Using Gherkin Language in SpecFlow]]). The generated unit tests are in a code-behind file of the feature files (e.g. `US01_BookSearch.feature.cs`).

The execution of the tests depends on the [[unit test provider|Unit Test Providers]] used by SpecFlow. The unit test provider can be [[configured|Configuration]] in the app.config file of the test project:
```xml
<specFlow>
  <unitTestProvider name="MsTest" />
</specFlow>
```

For example for MsTest unit test provider the tests can be executed from the Visual Studio test explorer window.

SpecFlow Visual Studio integration provides a simplified way to execute tests regardless of the provider. Use the "Run SpecFlow Scenarios" or "Debug SpecFlow Scenarios" commands from the context menu of the feature file editor or on the solution explorer nodes (project, folder, feature file).

See also [[Test Result]] and [[Debugging Tests]].