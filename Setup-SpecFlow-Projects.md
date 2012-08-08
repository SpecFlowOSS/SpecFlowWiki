The SpecFlow tests are usually placed into one or more separate project in the solution: the "SpecFlow Projects". 

The [[Project Setup Guide|http://go.specflow.org/getting-started]] on our website provides a basic introduction to SpecFlow. This page contains a detailed description of the possibilities.

## Setup SpecFlow projects step-by-step

This list describes the recommended setup options. For alternatives check the _Advanced setup options_ section below.

### 1. Create a project
Since SpecFlow can use different unit testing frameworks to execute the SpecFlow tests, the SpecFlow projects have to be either _Test Projects_ (in case of MsTest) or a simple _Class Libraries_. Just like for unit tests, it makes sense to keep a consistent naming convention for these projects (usual project name postfixes are _Specs_ or _AcceptanceTests_).

### 2. Add reference for the SpecFlow runtime
SpecFlow projects need the `TechTalk.SpecFlow.dll` in order to compile. You can setup this by installing our [[NuGet package|NuGet Integration]]: `[[SpecFlow|http://www.nuget.org/packages/SpecFlow]]` or one of the specific [[helper packages|NuGet Integration]].

```
PM> Install-Package SpecFlow
```

### 3. Configure SpecFlow project

If you have used one of the [[helper NuGet packages|NuGet Integration]] you don't need to configure anything. If you have used the `SpecFlow` package or want to fine tune SpecFlow, you need to change the settings in the App.config file. See [[Configuration]] page for details.

### 4. Add your first feature file

Your project is ready to use SpecFlow. You can add the first feature files (with _Add / New Item_ in Visual Studio for example) and implement your applications in a [[Behavior Driven Development|http://behaviour-driven.org/]] style. 

## Advanced setup options

For a manual project setup (without [[NuGet packages|NuGet Integration]]), you should copy all SpecFlow assemblies to the project's folder structure to have better upgrade and tool support. You can [[download the binary package|http://go.speclow.org/download-bin]] that contains all the necessary files.

### Setting up the runtime

SpecFlow projects need the `TechTalk.SpecFlow.dll` (or one of the platform-specific variants) in order to compile. You have to add a reference to the SpecFlow project for the copied TechTalk.SpecFlow.dll (in the `bin\{platform}` folder of the binary package). 

### Setting up the generator

The SpecFlow IDE integration tries to find the generator component of in your project structure to be able to use the generator version that matches to the SpecFlow runtime used in this project.

If you have used the NuGet package or kept the original structure of the binary package folders, it will find it without any extra configuration (based on the reference for the `TechTalk.SpecFlow.dll` assembly). In any other cases, you should consider the following discovery rules (the are presented in order of priority, highest first).

The IDE  integration checks the generator in the following paths:
 
1. generator path configured in app.config (`<generator path="..\lib\SpecFlow"/>`, see [[Configuration]])
2. generator assembly (`TechTalk.SpecFlow.Generator.dll`) referenced from the SpecFlow project
3. generator in the same folder as the runtime (`TechTalk.SpecFlow.dll`)
4. generator is "near" to the runtime (`tools` or `..\tools`, relative to the runtime)
5. generator obtained through NuGet (`..\..\tools`, relative to the runtime)

If SpecFlow cannot find the generator or it is older than v1.6.0, the installed SpecFlow generator is used. If you use any custom plugins (e.g. unit test generator), this has to be in the same folder as the generator currently.

### Detailed list of assemblies that are required for the project

SpecFlow is also distributed as a [[binary package|http://go.speclow.org/download-bin]]. This package contains the assemblies that should be placed to the project folder. Here is a detailed list though:

* `TechTalk.SpecFlow.dll`
* `TechTalk.SpecFlow.Generator.dll`
* `TechTalk.SpecFlow.Parser.dll`
* `TechTalk.SpecFlow.Utils.dll`
* `Gherkin.dll`
* `IKVM.*.dll` (5 assemblies)
* `specflow.exe` (optional)
* `TechTalk.SpecFlow.Reporting.dll` (optional)
* `TechTalk.SpecFlow.targets` (optional)
* `TechTalk.SpecFlow.tasks` (optional)
