## Enable Tracing

You can enable SpecFlow tracing in Visual Studio from _Tools / Options / SpecFlow_. Once the tracing is enabled, there is a new `SpecFlow` pane added to the output window showing diagnostic messages.

## Troubleshooting

1. **Steps are not recognized even though there are matching step definitions**
  
   SpecFlow Visual Studio integration caches the step definition binding status. This cache might get corrupted causing unrecognized steps. To delete the cache, you have to do the following steps.

   1. Close all Visual Studio instances.
   2. Go to `%TEMP%` folder and delete any files that are prefixed with `specflow-stepmap-`, e.g. `specflow-stepmap-SpecFlowProject-607539109-73a67da9-ef3b-45fd-9a24-6ee0135b5f5c.cache`.
   3. Reopen your solution.

   By enabling tracing (see above), you might see some more specific error.

1. **Tests are not displayed in the Test Explorer window when using SpecFlow+ Runner**

   Sometimes the Visual Studio Test Adapter cache gets corrupted, and the tests are not displayed. As a solution you can clean the cache with the following steps:

   1. Close all Visual Studio instances
   2. Go to `%TEMP%\VisualStudioTestExplorerExtensions\` folder and delete any sub folders related to SpecFlow/SpecRun.
   3. Reopen your solution and make sure it builds.

1. **`Unable to find plugin in the plugin search path: SpecRun` when saving / generating feature files**

   SpecFlow searches for plugins in the NuGet packages folder. This is detected relative to the reference for the `TechTalk.SpecFlow.dll`. If this dll is not loaded from the NuGet folder, the plugins are also not found. 

   A typical problem is if the NuGet folder is not ready yet (e.g. not restored) when the solution is opened, but there is a `TechTalk.SpecFlow.dll` in the `bin\Debug` folder of the project. In this case, Visual Studio might load the assembly from the `bin\Debug` folder instead of waiting for the NuGet folder properly restored. Once this has happened, Visual Studio even "remembers" that it loaded the assembly from `bin\Debug`, so reopening the solution might not help. The best way to fix this is:

    1. Make sure the NuGet folders are properly restored.
    2. Close Visual Studio.
    3. Delete `bin\Debug` folder from the project(s).
    4. Reopen solution in Visual Studio.

1. **Tests are not displayed in the Test Explorer window when using SpecFlow+ Runner, after NuGet restore**

   The `SpecRun.Runner` NuGet package, that contains the Visual Studio Test Explorer adapter is a solution-level package (these packages were registered in the `.nuget\packages.config` file of the solution). In some situations, NuGet package restore on build does not restore solution-level packages. 
   
   To fix this, you can open the NuGet console or the NuGet references dialog and click on the restore packages button. After restoring the packages properly, you might need to restart Visual Studio.

1. **VS2015: Tests are not displayed in the Test Explorer window when using SpecFlow+ Runner**

   It seems that VS2015 handles solution-level NuGet packages differently (these packages were registered in the `.nuget\packages.config` file of the solution). Now the solution-level NuGet packages have to be listed at the projects that use them, otherwise the Test Explorer will not recognize the test runner.

   To fix this issue, you have to either re-install the SpecFlow+ Runner NuGet packages, or simply add the dependency to the `SpecRun.Runner` package (`<package id="SpecRun.Runner" version="1.2.0" />`) to the packages.config file of the SpecFlow projects. You might need to restart Visual Studio to see the tests.

1. **VS2015: Tests turn to grayish green in the Test Explorer window when using SpecFlow+ Runner after test execution has been completed**

   This is a known cosmetic issue, we will address it later.