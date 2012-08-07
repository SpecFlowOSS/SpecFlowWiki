SpecFlow v1.9 adds support for Visual Studio 2012 integration.

The Visual Studio 2012 support can be installed from [[Visual Studio Gallery|http://go.specflow.org/vsgallery]] or from the online search in Visual Studio / Tools / Extensions and Updates. (You have to search for "SpecFlow" :).

The Visual Studio 2012 integration provides all functionality provided by the [[Visual Studio 2010 integration]], including feature file editor, step and keyword intellisense, navigation between feature files and step definitions. In addition to these, it also supports executing the scenarios with the VS2012 generic test runner. 

##Visual Studio 2012 generic test runner support

The SpecFlow IDE integration supports triggering SpecFlow feature file execution for the newly introduced VS2012 test runner infrastructure. So altogether, the following test runner infrastructures are supported by SpecFlow in VS2012: VS2012, ReSharper, SpecRun.

SpecFlow can automatically detect and use the new test runner in VS2012. With the new VS2012 test runner, you can execute SpecFlow scenarios based on all supported unit testing platforms (e.g. NUnit, xUnit, MS-Test), and jump from the test explorer directly to the related feature files.