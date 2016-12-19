The Visual Studio integration supports executing SpecFlow scenarios from the Visual Studio Test Explorer. The basic features work with all unit test providers, although you may need to install additional Visual Studio connectors, depending on the unit test framework. Full integration is provided for [[SpecRun|http://www.specrun.com]], meaning you can run and debug your scenarios as first class citizens:

* Run or debug individual scenarios or scenario outline examples from the feature file editor (choose "Run/Debug SpecFlow Scenarios" from the context menu)
* Scenarios are displayed in the Test Explorer with the scenario title
* Functions in the Test Explorer: 
  * Group scenarios by tags (choose "Traits" grouping) and features (choose "Class")
  * Filter scenarios by various criteria
  * Run/debug selected or all scenarios
  * Jump to the scenario in the feature file
  * View test execution results
* Specify the processor architecture (x86/x64), .NET platform and many other details for the test execution, including special config file transformations used by your tests.