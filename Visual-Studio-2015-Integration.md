_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Visual-Studio-2015-Integration]]. We use the GitHub wiki for authoring the documentation pages._

SpecFlow provides integration for Visual Studio 2015 (Community, Professional, Enterprise editions).

The Visual Studio 2015 support can be installed from [[Visual Studio Gallery|http://go.specflow.org/vsgallery2015]] or from the online search in Visual Studio / Tools / Extensions and Updates. (You have to search for "SpecFlow" :).

The Visual Studio 2015 support is provided as a different Visual Studio Gallery package than the one for VS2013. This means that this integration tracks the reviews and ratings separately from the previous one.

**Please help us and the other users by rating the package on the [[Visual Studio Gallery|http://go.specflow.org/vsgallery2015]] page!**

## Supported Features

Currently the Visual Studio 2015 integration provides the same feature set as [[Visual Studio 2013 Integration]]. See details there.

## Troubleshooting

1. **Tests are not displayed in the Test Explorer window when using SpecFlow+ Runner**

   It seems that VS2015 handles solution-level NuGet packages differently (these packages were registered in the `.nuget\packages.config` file of the solution). Now the solution-level NuGet packages have to be listed at the projects that use them, otherwise the Test Explorer will not recognize the test runner.

   To fix this issue, you have to either re-install the SpecFlow+ Runner NuGet packages, or simply add the dependency to the `SpecRun.Runner` package (`<package id="SpecRun.Runner" version="1.2.0" />`) to the packages.config file of the SpecFlow projects. You might need to restart Visual Studio to see the tests.

2. **Tests turn to grayish green in the Test Explorer window when using SpecFlow+ Runner after test execution has been completed**

   This is a known cosmetic issue, we will address it later.