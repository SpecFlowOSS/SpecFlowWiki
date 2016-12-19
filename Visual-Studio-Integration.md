**THIS PAGE IS A WORK IN PROGRESS**

The SpecFlow Visual Studio integration provides a number of features to make using SpecFlow easier with Visual Studio.

You can install the integration from [[Visual Studio Gallery|http://go.specflow.org/vsgallery]] or from the online search in Visual Studio under **Tools | Extensions and Updates** (search for "SpecFlow").

The integration provides the following features:

* Editor
  * Gherkin (feature file) editor with syntax coloring
  * Intellisense (auto-completion) for keywords and steps
  * Outlining (folding) sections of the feature file
  * Highlight unbound steps and step parameters in the editor
  * Comment/uncomment feature file lines
  * Automatic Gherkin table formatting
* Navigation
  * Navigate from steps in scenarios to binding methods and vice versa
  * Detect bindings from the SpecFlow project, from project references and from assembly references
  * Cached step analysis for faster solution startup
* Execution
  * Execute scenarios from the context menu: _Run SpecFlow Scenarios_, _Debug SpecFlow Scenarios_
  * Debugging
* Generic Test Runner Support (VS 2013 and Higher)
  * You can execute tests using the following test runners: Visual Studio, ReSharper and SpecRun. You can execute SpecFlow scenarios on all supported unit testing platforms (e.g. NUnit, xUnit, MS-Test).
* Other
  * Generate step definition skeletons from feature files
  * Re-generate feature files (from project node context menu and automatically on configuration change)
  * Configurable options
  * Support for ReSharper command shortcuts (when ReSharper is installed): commenting, navigation, test execution

##



### Visual Studio Test Explorer Support

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

Refer to [[Visual Studio Integration Features]] for more details on the features supported by the Visual Studio integration.