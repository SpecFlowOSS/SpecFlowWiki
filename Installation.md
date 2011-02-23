## Installation for Visual Studio 2008/2010 Professional, Premium, Ultimate
* SpecFlow is distributed as a Windows Installer MSI file which is the only way to install it. 
* SpecFlow can integrate to Visual Studio 2008 and Visual Studio 2010 - Professional, Premium and Ultimate.
* During the installation process you can decide whether to install the integration to the different Visual Studio versions.
* The installer deploys the necessary files to the specified folder (default: C:\Program Files\TechTalk\SpecFlow) and registers the Visual Studio Integration.

## Installation for Visual Studio 2008/2010 Express (Free)
* SpecFlow is designed to integrate into Visual Studio, and since Visual Studio Express [doesn't allow Add-Ins or Macros](http://stackoverflow.com/questions/86562/what-is-missing-in-the-visual-studio-2008-express-editions), you can't use it as designed.
* There are workarounds available, that essentially involve manually copying the template files to your system, and using the specflow.exe command line tool to generate and run SpecFlow tests.
* See this blog post for more detail: [http://watirmelon.com/2011/02/18/c-sharp-atdd-on-a-shoestring/](http://watirmelon.com/2011/02/18/c-sharp-atdd-on-a-shoestring/) 
