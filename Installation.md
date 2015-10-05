_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Installation]]. We use the GitHub wiki for authoring the documentation pages._

_Note:_ If you are new to SpecFlow, we recommend checking out the [[quick introduction guide|http://go.specflow.org/getting-started]] first. The quick introduction takes you through the process of installing SpecFlow and setting up your first project and tests in Visual Studio. 

SpecFlow consists of three components:

* The **IDE Integration** that provides a customized editor and test generation functions within your development environment.

* The **generator** that can turn Gherkin specifications into executable test classes.

* The **runtime** required for executing the generated tests. There are different runtime assemblies compiled for the different target platforms (.NET, Silverlight, Windows Phone).

In order to install everything you need, you first have to install the IDE integration and setup your project to work with SpecFlow. 

## Installing the IDE Integration

The process of installing the IDE Integration packages depends on your IDE. For Visual Studio 2010 and above, the easiest way is to search for “SpecFlow” in the online search in the extension manager (**Tools | Extensions and Updates**). For other IDE integrations and for the direct download links, see the [[Install IDE Integration]] page.

## Project Setup

The generator and runtime are usually installed together for each project. The easiest and most convenient way to install them is to use our NuGet package: `[[SpecFlow|http://www.nuget.org/packages/SpecFlow]]` or one of the specific helper packages, like `[[SpecFlow.NUnit|http://www.nuget.org/packages/SpecFlow.NUnit]]` or `[[SpecRun.SpecFlow|http://www.nuget.org/packages/SpecRun.SpecFlow]]`. 

```
Install-Package SpecFlow -ProjectName MyApp.Specs
```

Refer to the [[NuGet Integration]] page a full list of supported NuGet packages. You can find more details on setting up your project on the [[Setup SpecFlow Projects]] page.