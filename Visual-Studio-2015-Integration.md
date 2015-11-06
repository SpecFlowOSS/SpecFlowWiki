_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Visual-Studio-2015-Integration]]. We use the GitHub wiki for authoring the documentation pages._

SpecFlow provides integration for Visual Studio 2015 (Community, Professional, Enterprise editions).

The Visual Studio 2015 support can be installed from [[Visual Studio Gallery|http://go.specflow.org/vsgallery2015]] or from the online search in Visual Studio / Tools / Extensions and Updates. (You have to search for "SpecFlow" :).

The Visual Studio 2015 support is provided as a different Visual Studio Gallery package than the one for VS2013. This means that this integration tracks the reviews and ratings separately from the previous one.

**Please help us and the other users by rating the package on the [[Visual Studio Gallery|http://go.specflow.org/vsgallery2015]] page!**

## Supported Features

Currently the Visual Studio 2015 integration provides the same feature set as [[Visual Studio 2013 Integration]]. See details there.

## Troubleshooting

_See also: [[Troubleshooting Visual Studio Integration]]_

1. **Tests are not displayed in the Test Explorer window when using SpecFlow+ Runner**

   VS2015 appears to handles solution-level NuGet packages differently from previous versions (these packages were registered in the solution's `.nuget\packages.config` file). Solution-level NuGet packages now have to be listed at the project level, otherwise the Test Explorer will not recognise the test runner.

   To fix this issue, either re-install the SpecFlow+ Runner NuGet packages, or simply add the dependency on the `SpecRun.Runner` package (`<package id="SpecRun.Runner" version="1.2.0" />`) to the packages.config file of yourSpecFlow projects. You may need to restart Visual Studio to see your tests.

2. **Tests turn to grayish green in the Test Explorer window when using SpecFlow+ Runner after test execution has been completed**

   This is a known cosmetic issue, we will address it later.