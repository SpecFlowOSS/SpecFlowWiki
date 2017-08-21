## Enable Tracing

You can enable traces for SpecFlow. Once the tracing is enabled, a new `SpecFlow` pane is added to the output window showing diagnostic messages. 

To enable tracing, select **Tools | Options | SpecFlow** from the menu in Visual Studio and set **Enable Tracing** to 'True'. 

## Troubleshooting

### Steps are not recognised even though there are matching step definitions
  
The SpecFlow Visual Studio integration caches the binding status of step definitions. If the cache is corrupted, steps may be unrecognised. To delete the cache:

1. Close all Visual Studio instances.
2. Navigate to your `%TEMP%` folder and delete any files that are prefixed with `specflow-stepmap-`, e.g. `specflow-stepmap-SpecFlowProject-607539109-73a67da9-ef3b-45fd-9a24-6ee0135b5f5c.cache`.
3. Reopen your solution.

You may receive a more specific error message if you enable tracing (see above).

### Tests are not displayed in the Test Explorer window when using SpecFlow+ Runner###

The Visual Studio Test Adapter cache may also get corrupted, causing tests to not be displayed. If this happens, try clearing your cache as follows:

1. Close all Visual Studio instances
2. Navigate to your `%TEMP%\VisualStudioTestExplorerExtensions\` folder and delete any sub-folders related to SpecFlow/SpecRun.
3. Reopen your solution and ensure that it builds.

### Unable to find plugin in the plugin search path: SpecRun` when saving / generating feature files##

SpecFlow searches for plugins in the NuGet packages folder. This is detected relative to the reference to `TechTalk.SpecFlow.dll`. If this DLL is not loaded from the NuGet folder, the plugins will not be found. 

A common problem is that the NuGet folder is not yet ready (e.g. not restored) when opening the solution, but `TechTalk.SpecFlow.dll` in located in the `bin\Debug` folder of the project. In this case, Visual Studio may load the assembly from the `bin\Debug` folder instead of waiting for the NuGet folder to be properly restored. Once this has happened, Visual Studio remembers that it loaded the assembly from `bin\Debug`, so reopening the solution may not solve this issue. The best way to fix this issue is as follows:

1. Make sure the NuGet folders are properly restored.
2. Close Visual Studio.
3. Delete the `bin\Debug` folder from your project(s).
4. Reopen your solution in Visual Studio.

### Tests are not displayed in the Test Explorer window when using SpecFlow+ Runner, even after after restoring the NuGet package###

The `SpecRun.Runner` NuGet package that contains the Visual Studio Test Explorer adapter is a solution-level package (registered in the `.nuget\packages.config` file of the solution). In some situations, NuGet package restore on build does not restore solution-level packages. 
   
To fix this, open the NuGet console or the NuGet references dialog and click on the restore packages button. You may need to restart Visual Studio after restoring the packages.

### VS2015: Tests are not displayed in the Test Explorer window when using SpecFlow+ Runner###

It seems that VS2015 handles solution-level NuGet packages differently (those registered in the `.nuget\packages.config` file of the solution). As a result, solution-level NuGet packages must be listed in the projects that use them, otherwise Test Explorer cannot recognise the test runner.

To fix this issue, either re-install the SpecFlow+ Runner NuGet packages, or add the dependency on the `SpecRun.Runner` package (`<package id="SpecRun.Runner" version="1.2.0" />`) to the packages.config file of your SpecFlow projects. You might need to restart Visual Studio to see your tests.

### VS2015: Tests turn grayish-green in the Test Explorer window after completing the execution of tests with SpecFlow+ Runner###

This is a known cosmetic issue and will be addressed later.