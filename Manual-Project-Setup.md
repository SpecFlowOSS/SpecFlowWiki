The SpecFlow tests are usually placed into one or more separate project in the solution: the "SpecFlow Projects". 

The [[Project Setup Guide|http://go.specflow.org/getting-started]] on our website provides a basic introduction to SpecFlow (based on the NuGet packages). This page contains a description of the manual setup options for advanced usage scenarios.

To set up a project manually (without [[NuGet packages|NuGet Integration]]), you should copy all SpecFlow assemblies to the project's folder structure for improved upgrade and tool support. Download the binary package containing the necessary files [[here|http://go.specflow.org/download-bin]] .

## Setting up the runtime

SpecFlow projects need the `TechTalk.SpecFlow.dll` (or one of the platform-specific variants) in order to compile. You have to add a reference to the SpecFlow project to the copied TechTalk.SpecFlow.dll (in the `bin\{platform}` folder of the binary package). 

## Setting up the generator

The SpecFlow IDE integration tries to find the generator component in your project structure in order to use the generator version matching the SpecFlow runtime in your project.

If you have used the NuGet package or kept the original structure of the binary package folders, the IDE integration should locate it without requiring any extra configuration (based on the reference to the `TechTalk.SpecFlow.dll` assembly). Otherwise take the following discovery rules into account (these are listed in order of priority, highest first).

The IDE  integration checks for the generator in the following paths:
 
1. The generator path configured in app.config (`<generator path="..\lib\SpecFlow"/>`, see [[Configuration]])
2. The generator assembly (`TechTalk.SpecFlow.Generator.dll`) referenced from the SpecFlow project
3. The generator in the same folder as the runtime (`TechTalk.SpecFlow.dll`)
4. The generator located "near" to the runtime (`tools` or `..\tools`, relative to the runtime)
5. The generator obtained through NuGet (`..\..\tools`, relative to the runtime)

If SpecFlow cannot find the generator or it is older than v1.6.0, the installed SpecFlow generator is used. If you use any custom plugins (e.g. unit test generator), this must be in the same folder as the generator.

## Detailed list of assemblies that are required for the project

SpecFlow is also distributed as a [[binary package|http://go.specflow.org/download-bin]]. This package contains the assemblies that should be placed in your project folder:

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
