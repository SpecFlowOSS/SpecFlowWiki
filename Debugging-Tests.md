_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Debugging-Tests]]. We use the GitHub wiki for authoring the documentation pages._

SpecFlow Visual Studio integration also supports debugging the execution of the tests. Just like in the source code files of your project, you can also place breakpoints in the SpecFlow feature files. Whenever you execute the generated tests in debug mode, the execution will stop at the specified breakpoints and you can execute the steps one-by-one using the standard “Step Over” (F10) command or you can go to the detailed execution of the bindings using the “Step Into” (F11) command. 

Also when the execution of a SpecFlow test is stopped at a certain point of the binding (because of an exception for instance), you can navigate to the currently executed step of the feature file from the “Call Stack” tool window of Visual Studio.

By default, you cannot debug inside of the generated .feature.cs files. You can enable debugging of those files by setting [[&lt;generator allowDebugGeneratedFiles="true"&gt;|Configuration]] setting.