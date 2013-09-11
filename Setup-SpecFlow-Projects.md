The SpecFlow tests are usually placed into one or more separate project in the solution: the "SpecFlow Projects". 

The [[quick introduction guide|http://go.specflow.org/getting-started]] on our website provides a basic introduction to SpecFlow. This page contains a detailed description of the possibilities.

## Setup SpecFlow projects step-by-step using NuGet

This list describes the recommended setup options. For alternatives check the [[Advanced Project Setup]] page.

### 1. Create a project
Since SpecFlow can use different unit testing frameworks to execute the SpecFlow tests, the SpecFlow projects have to be either _Test Projects_ (in case of MsTest) or a simple _Class Libraries_. Just like for unit tests, it makes sense to keep a consistent naming convention for these projects (usual project name postfixes are _Specs_ or _AcceptanceTests_).

### 2. Add reference for the SpecFlow runtime
SpecFlow projects need the `TechTalk.SpecFlow.dll` in order to compile. You can setup this by installing our [[NuGet package|NuGet Integration]]: `[[SpecFlow|http://www.nuget.org/packages/SpecFlow]]` or one of the specific [[helper packages|NuGet Integration]], like `[[SpecFlow.NUnit|http://www.nuget.org/packages/SpecFlow.NUnit]]` or `[[SpecRun.SpecFlow|http://www.nuget.org/packages/SpecRun.SpecFlow]]`. The helper packages group all necessary dependencies and apply the necessary [[configuration]].

```
PM> Install-Package SpecFlow -ProjectName MyApp.Specs
```

### 3. Configure SpecFlow project

If you have used one of the [[helper NuGet packages|NuGet Integration]] you don't need to configure anything. If you have used the `SpecFlow` package or want to fine tune SpecFlow, you need to change the settings in the App.config file. See [[Configuration]] page for details.

### 4. Add your first feature file

Your project is ready to use SpecFlow. You can add the first [[feature files|Using Gherkin Language In SpecFlow]] (with _Add / New Item_ in Visual Studio for example) and implement your applications in [[Specification by Example|http://www.specificationbyexample.com]] ([[Behavior Driven Development (BDD)|http://behaviour-driven.org/]], [[Acceptance Test Driven Development (ATDD)|http://en.wikipedia.org/wiki/Test-driven_development]]) style. 

