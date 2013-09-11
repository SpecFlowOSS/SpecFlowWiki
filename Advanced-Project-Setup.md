The SpecFlow tests are usually placed into one or more separate project in the solution: the "SpecFlow Projects". 

The [[Setup SpecFlow Projects]] page describes the recommended setup options. This page contains the advanced project setup options for cases you cannot use NuGet packages.

For a manual project setup (without [[NuGet packages|NuGet Integration]]), you should copy all SpecFlow assemblies to the project's folder structure to have better upgrade and tool support. You can [[download the binary package|http://go.specflow.org/download-bin]] that contains all the necessary files.

## Setting up the runtime

SpecFlow projects need the `TechTalk.SpecFlow.dll` (or one of the platform-specific variants) in order to compile. You have to add a reference to the SpecFlow project for the copied TechTalk.SpecFlow.dll (in the `bin\{platform}` folder of the binary package). 

## Setting up the generator

The SpecFlow IDE integration tries to find the generator component of in your project structure to be able to use the generator version that matches to the SpecFlow runtime used in this project.

If you have used the NuGet package or kept the original structure of the binary package folders, it will find it without any extra configuration (based on the reference for the `TechTalk.SpecFlow.dll` assembly). In any other cases, you should consider the following discovery rules (the are presented in order of priority, highest first).

The IDE  integration checks the generator in the following paths:
 
1. generator path configured in app.config (`<generator path="..\lib\SpecFlow"/>`, see [[Configuration]])
2. generator assembly (`TechTalk.SpecFlow.Generator.dll`) referenced from the SpecFlow project
3. generator in the same folder as the runtime (`TechTalk.SpecFlow.dll`)
4. generator is "near" to the runtime (`tools` or `..\tools`, relative to the runtime)
5. generator obtained through NuGet (`..\..\tools`, relative to the runtime)

If SpecFlow cannot find the generator or it is older than v1.6.0, the installed SpecFlow generator is used. If you use any custom plugins (e.g. unit test generator), this has to be in the same folder as the generator currently.

## Detailed list of assemblies that are required for the project

SpecFlow is also distributed as a [[binary package|http://go.specflow.org/download-bin]]. This package contains the assemblies that should be placed to the project folder. Here is a detailed list though:

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
