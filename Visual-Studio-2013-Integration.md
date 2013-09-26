_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Visual-Studio-2013-Integration]]. We use the GitHub wiki for authoring the documentation pages._

SpecFlow v1.9.2 provides integration for Visual Studio 2013 (Professional, Premium and Ultimate editions).

The Visual Studio 2013 support can be installed from [[Visual Studio Gallery|http://go.specflow.org/vsgallery2013]] or from the online search in Visual Studio / Tools / Extensions and Updates. (You have to search for "SpecFlow" :).

The Visual Studio 2013 support is provided as a different Visual Studio Gallery package than the one for VS2010 and VS2012. This means that this integration tracks the reviews and ratings separately from the previous one.

**Please help us and the other users by rating the package on the [[Visual Studio Gallery|http://go.specflow.org/vsgallery2013]] page!**

## Supported Features

The Visual Studio 2013 integration provides all functionality provided by the [[earlier integrations|Visual Studio 2012 integration]], including feature file editor, step and keyword intellisense, navigation between feature files and step definitions. 

### Visual Studio Test Window Support

The Visual Studio integration supports executing the SpecFlow scenarios from the Visual Studio Test Window too. Although some basic integration features work with all unit test providers (*), with [[SpecRun|http://www.specrun.com]], you can run and debug your scenarios as first class citizens:

* You can run or debug individual scenarios or scenario outline examples from the feature file editor (choose "Run/Debug SpecFlow Scenarios" from the context menu)
* The scenarios are displayed int the test window with the scenario title
* Fro the test window, you can 
  * group the scenarios by tags (choose "Traits" grouping) and features (choose "Class")
  * filter scenarios by different criteria
  * run or debug selected or all scenarios
  * jump to the scenario in the feature file
  * view test execution results
* You can specify processor architecture (x86/x64), .NET platform and many other details for the test execution, including special config file transformation used for the test execution only.

See the short [[introduction video|http://go.specflow.org/specrun-vs2013]] or grab more details on the [[SpecRun website|http://www.specrun.com]].

_(*) You might need to install additional Visual Studio connectors, depending on the unit test framework._
