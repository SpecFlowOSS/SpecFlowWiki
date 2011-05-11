With SpecFlow you can define the acceptance criteria in feature files that can be executed. These tests are usually placed in a separate project in the solution (e.g. "BookShop.AcceptanceTests" in the [[BookShop sample|Examples]]).

SpecFlow generates executable unit tests from the defined acceptance criteria (called [[scenarios|Using Gherkin Language in SpecFlow]]). The generated unit tests are in a code-behind file of the feature files (e.g. `US01_BookSearch.feature.cs`).

The execution of the tests depends on the [[unit test provider|Unit Test Providers]] used by SpecFlow. The unit test provider can be [[configured|Configuration]] in the app.config file of the test project:
```xml
<specFlow>
  <unitTestProvider name="MsTest" />
</specFlow>
```

For example for MsTest unit test provider, all acceptance tests in the project can be executed with the following steps:
1.	Select the acceptance test project (e.g. `BookShop.AcceptanceTests`) in solution explorer.
2.	Select command from the main menu: Test / Run / Tests in Current Context (Ctrl R,T)

For executing a single scenario, the test explorer can be used. Alternatively the generated test method can be executed from the generated code-behind file.

See also [[Test Result]] and [[Debugging Tests]].