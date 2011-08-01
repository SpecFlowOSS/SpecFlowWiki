The SpecFlow tests are usually placed into one or more separate project in the solution: the "SpecFlow Projects". 

## Setup SpecFlow projects step-by-step

### 1. Create a project
Since SpecFlow can use different unit testing frameworks to execute the SpecFlow tests, the SpecFlow projects have to be either _Test Projects_ (in case of MsTest) or a simple _Class Libraries_. Just like for unit tests, it makes sense to keep a consistent naming convention for these projects (usual project name postfixes are _Specs_ or _AcceptanceTests_).

### 2. Add reference for the SpecFlow runtime
SpecFlow projects need the `TechTalk.SpecFlow.dll` in order to compile. You need to add a reference to this assembly in one of the following ways:

* Add the reference with NuGet: `Install-Package SpecFlow`. This is the easiest and the recommended way. See [[NuGet Integration]] for details.
* Copy the content of the SpecFlow install folder to a folder inside your project structure and add a reference to the copied `TechTalk.SpecFlow.dll`. (Although the other assemblies are not directly used by the project, but they provide better tool and upgrade options, therefore it is a good practice to copy them too.) See detailed list of assemblies to be copied at the and of this page.

### 3. Configure SpecFlow project
In the most simple case (using NUnit provider) you don't need to configure anything. If you are using another unit test provider or want to fine tune SpecFlow, see [[Configuration]].

If you have configured the project with NuGet, you should already have an App.config file with the configuration skeleton and a link for the further options. 

### 4. Add your first feature file

Your project is ready to use SpecFlow. You can add the first feature files (with _Add / New Item_ in Visual Studio for example) and implement your applications in a [[Behavior Driven Development|http://behaviour-driven.org/]] style. 

## Advanced setup options

As mentioned in Step 2, you should copy all SpecFlow assemblies to the project's folder structure to have better upgrade and tool support. The SpecFlow IDE integration (currently only VS2010) tries to find the generator component of in your project structure to be able to use the generator version that matches to the SpecFlow runtime used in this project.

If you are using one of the methods described in Step 2, it will find it without any extra configuration. In any other cases, you should consider the following discovery rules (the are presented in order of priority, highest first).

The IDE  integration checks the generator in the following paths:
 
1. generator path configured in app.config (`<generator path="..\lib\SpecFlow"/>`, see [[Configuration]])
2. generator assembly (`TechTalk.SpecFlow.Generator.dll`) referenced from the SpecFlow project
3. generator in the same folder as the runtime (`TechTalk.SpecFlow.dll`)
4. generator is "near" to the runtime (`tools` or `..\tools`, relative to the runtime)
5. generator obtained through NuGet (`..\..\tools`, relative to the runtime)

If SpecFlow cannot find the generator or it is older than v1.6.0, the installed SpecFlow generator is used. If you use any custom plugins (e.g. unit test generator), this has to be in the same folder as the generator currently.

## Detailed list of assemblies that are required for the project

SpecFlow is also distributed as a binary package at [[GitHub|https://github.com/techtalk/SpecFlow/downloads]]. This package contains the assemblies that should be placed to the project folder. Here is a detailed list though:

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
