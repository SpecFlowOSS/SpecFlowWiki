If you want to contribute on the VS2010 integration development, here are some useful trick how you can work and test the integration and have the official SpecFlow release installed at the same time.

You have to do the following steps to setup your environment:
1. Install SpecFlow (official release)
1. Close all VS2010 instances
1. Move folder "**TechTalk**" from "**C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\Extensions**" to "**C:\Users\*youruser*\AppData\Local\Microsoft\VisualStudio\10.0\Extensions\TechTalk\SpecFlow**"
1. Open the file "**C:\Program Files (x86)\TechTalk\SpecFlow\extension.vsixmanifest**" in a text editor (Admin Mode) and change the setting **<InstalledByMsi>** to **false**
1. Start VS2010, go to **Tools/Extension Manager...** and enable the SpecFlow extension (as you have changed the InstalledByMsi setting, the "Uninstall" is also enabled here, but you should not use it, but uninstall SpecFlow from the add/remove programs)
1. Restart VS2010, check in the extension manager that the SpecFlow extension is enabled
1. Start VS2010 Experimental instance - SpecFlow should not be listed in the extension manager here, so you are ready to test your own compilation

Steps to compile & test VS2010 integration changes
1. Open the SpecFlow solution
1. Select the "VS2010IntegrationTest" solution configuration
1. Apply cnahges in the VS2010 integration & build the solution - this will register the VS2010 integration for the experimental instance
1. Start VS2010 Experimental instance and test/debug your changes
