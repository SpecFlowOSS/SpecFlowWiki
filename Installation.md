_Note:_ If you are new to SpecFlow, we recommend checking the [[quick introduction guide|http://go.specflow.org/getting-started]] first. 

SpecFlow consists of three components:

* The **IDE Integration** that provides customized editor and test generation functions in your development environment, like Visual Studio 2012.

* The **generator** that can turn the Gherkin specifications into executable test classes.

* The **runtime** that is required for executing the generated tests. There are different runtime assemblies compiled for the different target platforms (.NET, Silverlight, Windows Phone).

In order to install everything you need, you have to install the IDE integration and setup your project to work with SpecFlow. 

## Installing the IDE Integration

The installation of the IDE Intergation packages depends on the IDE you use. For Visual Studio 2010 and above, the easiest way is to search for “SpecFlow” in the extension manager (Tools / Extensions and Updates) online search. For other IDE integrations and for the direct download links, check the [[Install IDE Integration]] page.

## Project Setup

The generator and the runtime is usually installed together per project. The easiest and most convenient way to install these is to use our NuGet package: `[[SpecFlow|http://www.nuget.org/packages/SpecFlow]]` or one of the specific helper packages, like `[[SpecFlow.NUnit|http://www.nuget.org/packages/SpecFlow.NUnit]]` or `[[SpecRun.SpecFlow|http://www.nuget.org/packages/SpecRun.SpecFlow]]`. 

```
Install-Package SpecFlow -ProjectName MyApp.Specs
```

For the full list of supported NuGet packages, check the [[NuGet Integration]] page. You can find more details about the project setup on the [[Setup SpecFlow Projects]] page.
