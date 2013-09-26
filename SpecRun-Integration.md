[[SpecRun|http://www.specrun.com]] is a test execution framework specialized for SpecFlow and provides easy integration to the Visual Studio testing infrastructure and to the Team Foundation Server (TFS) Build. Grab more details on the [[SpecRun website|http://www.specrun.com]].

##Installation

The SpecRun integration is very easy: just add the `[[SpecRun.SpecFlow|http://www.nuget.org/packages/SpecRun.SpecFlow]]` NuGet package to your SpecFlow project and you are ready to run. 

##Visual Studio Test Window Support

With [[SpecRun|http://www.specrun.com]], you can run and debug your scenarios as first class citizens:

* You can run or debug individual scenarios or scenario outline examples from the feature file editor (choose "Run/Debug SpecFlow Scenarios" from the context menu)
* The scenarios are displayed int the test window with the scenario title
* Fro the test window, you can 
  * group the scenarios by tags (choose "Traits" grouping) and features (choose "Class")
  * filter scenarios by different criteria
  * run or debug selected or all scenarios
  * jump to the scenario in the feature file
  * view test execution results
* You can specify processor architecture (x86/x64), .NET platform and many other details for the test execution, including special config file transformation used for the test execution only. (See the short [[introduction video|http://go.specflow.org/specrun-testenv]].)

See the short [[introduction video|http://go.specflow.org/specrun-vs2013]] about Visual Studio integration.

##Team Foundation Server Support

The SpecRun NuGet package contains all necessary integration components for Team Foundation Server Build, and you don't need to do any additional configuration or build process template modification to let TFS build execute your scenarios, and even more:

* Display scenario titles in the execution result
* Generate detailed and customizable HTML report
* Allows filtering scenarios in the TFS build definition
* The integration also works with the hosted Team Foundation Service ([[http://tfs.visualstudio.com/]])

See the short [[introduction video|http://go.specflow.org/specrun-tfs]] on this topic.

##Test Execution Features

[[SpecRun|http://www.specrun.com]] is a smarter integration test runner for SpecFlow: 

* Faster feedback: parallel test execution and smart execution order
* More information: advanced metrics, detecting random failures, historical execution statistics
* Not limited to SpecFlow: execute integration tests written with other unit testing frameworks

See the short introduction video about the [[configurable test execution environments|http://go.specflow.org/specrun-testenv]] and about [[parallel test execution|http://go.specflow.org/specrun-parallel]].