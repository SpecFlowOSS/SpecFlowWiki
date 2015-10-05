_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Advanced-Project-Setup]]. We use the GitHub wiki for authoring the documentation pages._

The SpecFlow tests are usually placed into one or more separate project in the solution: the "SpecFlow projects". 

The [[Setup SpecFlow Projects]] page describes the recommended setup process. This page covers the advanced project setup options if you are unable to use the NuGet packages.

To set up a project manually (i.e. without [[NuGet packages|NuGet Integration]]), [[download the binary package|http://go.specflow.org/download-bin]] that contains all the necessary files and copy all SpecFlow assemblies to your project's folder structure for better upgrade and tool support. 

## Setting Up the Runtime

SpecFlow projects require `TechTalk.SpecFlow.dll` (or one of the platform-specific variants) in order to compile. Add a reference to the TechTalk.SpecFlow.dll (located in the `bin\{platform}` folder of the binary package) to your SpecFlow project. 

## Setting up the Generator

The SpecFlow IDE integration tries to locate the generator component in your project structure in order to use the generator version matching the SpecFlow runtime in your project.

If you installed SpecFlow with the NuGet package or have retained the original structure of the binary package, the generator will be located (based on the reference for the `TechTalk.SpecFlow.dll` assembly) without requiring any configuration. Otherwise, you need to take into account the following rules used to locate the generator (in order of priority, highest priority first):
 
1. The generator path configured in app.config (`<generator path="..\lib\SpecFlow"/>`, see [[Configuration]])
2. The same path as the generator assembly (`TechTalk.SpecFlow.Generator.dll`) referenced from the SpecFlow project
3. The same path as the runtime (`TechTalk.SpecFlow.dll`)
4. In the `tools` or `..\tools` directories relative to the runtime
5. The generator obtained through NuGet (`..\..\tools`, relative to the runtime)

If SpecFlow cannot find the generator or it is older than v1.6.0, the installed SpecFlow generator is used. If you use any custom plugins (e.g. unit test generator), they must be located in the same folder as the generator.

## Required Assemblies

SpecFlow is also distributed as a [[binary package|http://go.specflow.org/download-bin]]. This package contains the assemblies that should be placed to the project folder. The package contains the following:

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
