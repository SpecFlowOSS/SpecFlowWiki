_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Setup-SpecFlow-Projects]]. We use the GitHub wiki for authoring the documentation pages._

The SpecFlow tests are usually placed into one or more separate project in your solution: these are referred to as "SpecFlow projects". 

The [[Getting Started guide|http://go.specflow.org/getting-started]] provides a basic introduction to SpecFlow, including installing SpecFlow and setting up your first project. This page covers the available options in greater depth.

## Step-by-Step Guide to Setting Up SpecFlow Projects Using NuGet

This following outlines the recommended setup options. For alternatives, see the [[Advanced Project Setup]] page.

### 1. Create a project
Since SpecFlow supports various unit testing frameworks that can be used to execute the SpecFlow tests, SpecFlow projects must be either *Test Projects* (in case of MsTest) or simple *Class Libraries*. As with unit tests, it makes sense to adopt a consistent naming convention for these projects (usual project name postfixes are *Specs* or *AcceptanceTests*).

### 2. Add a reference for the SpecFlow runtime
SpecFlow projects require the `TechTalk.SpecFlow.dll` in order to compile. This DLL is deployed when installing the `[[SpecFlow|http://www.nuget.org/packages/SpecFlow]]` [[NuGet package|NuGet Integration]] or one of the specific [[helper packages|NuGet Integration]], such as `[[SpecFlow.NUnit|http://www.nuget.org/packages/SpecFlow.NUnit]]` or `[[SpecRun.SpecFlow|http://www.nuget.org/packages/SpecRun.SpecFlow]]`. The helper packages group all necessary dependencies and apply the necessary [[configuration]].

Install the NuGet packages by either right-clicking on your solution and selecting **Manage NuGet Packages for Solution** or from the Packet Manager console:

```
PM> Install-Package SpecFlow -ProjectName MyApp.Specs
```

### 3. Configure your SpecFlow project

If you used one of the [[helper NuGet packages|NuGet Integration]] to install SpecFlow, you don't need to configure anything. If you used the `SpecFlow` package or want to finetune SpecFlow, you need to change the settings in the App.config file. For details, refer to [[Configuration]].

### 4. Add your first feature file

Your project is now ready to use SpecFlow. You can add your first [[feature files|Using Gherkin Language In SpecFlow]] in Visual Studio be selecting *Add | New Item* and develop your applications according to the [[Specification by Example|http://www.specificationbyexample.com]] ([[Behavior Driven Development (BDD)|http://behaviour-driven.org/]] or [[Acceptance Test Driven Development (ATDD)|https://en.wikipedia.org/wiki/Acceptance_test-driven_development]]) paradigms. 