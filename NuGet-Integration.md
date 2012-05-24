SpecFlow is also available as a [[NuGet|http://www.nuget.org/]] package. This is the easiest way to setup your project for SpecFlow.

The NuGet package contains only the generator and the runtime components of SpecFlow, so you still need to install the SpecFlow installer to your machine. 

You can add SpecFlow to your project with the NuGet Package Management Console with
```
Install-Package SpecFlow -ProjectName myproject
```

For setting up SpecFlow with NUnit in one step, there are two additional packages

* `SpecFlow.NUnit` - installs SpecFlow and NUnit for running with arbitrary test runners (e.g. ReSharper)
* `SpecFlow.NUnit.Runners` - this is a specialized package, if you want to run SpecFlow tests with the nunit test runners together with `[AfterTestRun]` hooks. (see https://github.com/techtalk/SpecFlow/issues/26)