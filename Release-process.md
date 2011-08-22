### Release Build

* make sure that all test pass (also on the build server)
* review changelog.txt, update header with the new version number & date
* if there are changes in the code generation: upgrade generator version number in `Generator\TestGeneratorFactory.cs`
* upgrade version number
  * VersionInfo.cs
  * Installer/SpecFlowInstaller/VS2008.wxs
  * Installer/SpecFlowInstaller/Product.wxs (2 instances)
  * IdeIntegration/Vs2010Integration/SpecFlowPackage.cs
  * IdeIntegration/Vs2010Integration/source.extension.vsixmanifest
  * IdeIntegration/NuGetIntegration/SpecFlow.nuspec
  * IdeIntegration/MonoDevelopIntegration/MonoDevelop.TechTalk.SpecFlow.addin.xml
* trigger nightly build on build server
* tag the source as "v1.2.3.0" (don't forget to push the tag)
* update version numbering on build server

### Publish Release

* Upload MSI and binary packages to github
* Upload NuGet package
* Update specflow.org website
* Send message to google groups: announcements, forum
* Tweet new version with @specflow account
