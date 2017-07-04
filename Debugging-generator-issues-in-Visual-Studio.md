These steps might be useful if you experience SpecFlow generator issues in Visual Studio and would like to help diagnosing the causes. The SpecFlow feature file generator is triggered when you save a feature file in Visual Studio. A generator issue might appear as:

* The generated code behind file contains an error pragma (`#error ...`)
* The generated code behind file does not reflect the SpecFlow config settings (wrong unit test provider, not applied plugin, etc.)
* The generated code behind file does not refer to the SpecFlow version you use in your project (e.g. you use SpecFlow v2.2, but the code behind file header says v1.9)

To diagnose such issues, you need to debug the Visual Studio instance. But this is not as hard as it sounds. Just follow the steps below.

## Generation concept

The SpecFlow Visual Studio integration is hooked to the save event of the feature files using the `SingleFileGenerator` infrastructure. 

The SpecFlow Visual Studio integration (normally) uses the SpecFlow package added to your project to generate the feature files (although it contains a version of SpecFlow, currently v1.9). In order to do that, whenever the generation is triggered, 

* it creates a new `AppDomain`, 
* loads the SpecFlow version from your project into that (from `packages\SpecFlow.X.Y.0\tools`) and
* invokes the generator API through remoting

For this to work, it is necessary that the generator API remains binary-remoting compatible with the version used in VS (v1.9). The API is located in the https://github.com/techtalk/SpecFlow/tree/master/TechTalk.SpecFlow.Generator/Interfaces folder. Think twice before changing these classes!

## Tracing

Make sure you have [enabled tracing](http://specflow.org/documentation/Troubleshooting-Visual-Studio-Integration/) before starting with the diagnosis. From the trace you should see which generator assembly has been loaded to preform the generation.

## Preparation for the debugging

* Have a version of the [SpecFlow codebase](https://github.com/techtalk/SpecFlow) on the machine where you do the debugging. Preferably the version that is related to the SpecFlow version of your project. You don't need to compile it.
* Optionally you can also download the [SpecFlow Visual Studio Integration codebase](https://github.com/techtalk/SpecFlow.VisualStudio). You don't need to compile it.
* Download the symbol files for the SpecFlow version of your project. The easiest(?) is to find it in the release build on [appveyor](https://ci.appveyor.com/project/SpecFlow/specflow/history), and take the `SpecFlowSymbolPackage.zip` from the build artifacts. The symbol files for the v2.2 are [here](https://ci.appveyor.com/api/buildjobs/5tm8f9ky3cbfa25g/artifacts/Installer%2FSpecFlowBinPackage%2Fbin%2FSpecFlowSymbolPackage.zip).
* Save the symbol (`*.pdb`) files to the `packages\SpecFlow.X.Y.0\tools` folder of your project.
* TODO: where to find the symbols for the VS integration?

## Reproduce the error

Open a your project in Visual Studio like normal and make sure the error is reproducible. (You save the file and you see the anomaly.) To make sure you are really reproducing the issue, you can make a manual change in the code-behind file and re-save the feature file. The manual change should be overridden. 

## Attach a debugger to Visual Studio

* Start another instance of Visual Studio as administrator.
* Go to _Tools / Options / Debugging_ and uncheck _Enable Just My Code_
* Go to _Debug / Attach to Process..._, find the VS process (`devenv.exe`) loaded your project and click _Attach_

Now you are debugging. You can try to save the feature file again in the other Visual Studio and see if there is an exception popping up in the debugger. Usually it won't because all exceptions are handled. So to find out more we need to enable stopping at all exceptions. This will stop at many (~20) exceptions, and many of them not relevant, but maybe you will find the one that leads you to the solution.

To enable stopping on all exceptions:

* Go to _Debug / Windows / Exception Settings_ 
* Make sure there is a check at _Common Language Runtime Exeptions_

## Start diagnosing the exceptions

If you save the feature file again, the exceptions will be triggered. You can safely skip the com exceptions, the type load exceptions of non-SpecFlow types and many other. On the exception window you can indicate whether you want to stop at the exceptions of the same time. In VS2017 you can even instruct the debugger not to stop at the exceptions if they are raised from a specific assembly.

Sooner or later you will hit a SpecFlow exception (typically like trying to load the feature file language). If you stop at this exception, if you have copied the right pdb-s to the right place, you can jump to the related SpecFlow source code. The debugger will not find the SpecFlow `.cs` files by default, because the build server used a different root directory for compilation, but you can browse the files manually from the downloaded SpecFlow source code. Once you browse one file, it will also find the others automatically, so you need to do this only once. 

Once the connection between the binaries and the source code has been made, you can even set breakpoints to the SpecFlow source files (open them with file open). E.g. putting a breakpoint to the test generator factory is a good starting point: https://github.com/techtalk/SpecFlow/blob/master/TechTalk.SpecFlow.Generator/TestGeneratorFactory.cs#L19

## Use your intuition

The rest is quite much depends on the situation. The call stack window might be also useful.
