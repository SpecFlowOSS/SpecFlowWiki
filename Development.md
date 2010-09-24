## Structure

The source code of SpecFlow is included in a single Visual Studio 2008 solution (TechTalk.SpecFlow.sln), located in the main folder.

Besides the source code, the SpecFlow reporsitory also contains a "Samples" folder where you can find code samples (might be included into the installer later).

The source code is divided into the following categories:

* Installer - All code related to the SpecFlow installer
          o Location: "Installer" folder
          o Projects:
                + SpecFlowSetup - the setup project
                + DevenvSetupCustomAction - a custom action to call "devenv /setup" during installation 
* Generator (aka Parser) - All code related to generating unit test classes from feature files
          o Includes Gherkin parser
          o Does not have a static dependency on the "Runtime" components to allow side-by-side runtime versions
          o Location: "Parser" folder 
* VsIntegration - All code related to Visual Studio 2008 integration
          o Includes SingleFileGenerator for the ".feature" files
          o Location: "VsIntegration" folder 
* Runtime - All code related to the execution of the generated tests
          o Includes
                + the "TestRunner" class (entry point of the generated test methods)
                + the dynamic binding resolution and execution logic
                + the binding attributes
                + the FeatureContext/ScenarioContext classes
                + the tracing logic 
          o Location: "Runtime" folder 
* Tests - Unit tests for the generator and the runtime components
          o Location: Tests
          o Projects:
                + ParserTests - tests for the parser and the generator
                + RuntimeTests - test for the runtime component 
* Reporting - All code related to SpecFlow reports
          o Includes
                + Step Definition Report - a report about usage and binding of scenario steps
                + NUnit Execution Report - a report that visualizes the nunit execution result in SpecFlow style 
          o Does not have a static dependency on the "Runtime" components to allow side-by-side runtime versions
          o Location: "Reporitng" folder 

## Conventions

Here is a list of code structuring conventions that we follow:

* The projects are named, like the full namespace (e.g. TechTalk.SpecFlow.Parser), but located in a folder with the short name (e.g. Parser). This is useful to stay below the VS path length limit.
* All external dependency (like nunit.framework) is located in the "lib" folder.
* All project includes (as a link) the VersionInfo.cs file from the root folder (to make the version changes easier).
* If you have finished working on a branch (that has been pushed at least once), you should delete it after merging back. Here is a description how: [[Remove a remote branch|http://github.com/guides/remove-a-remote-branch]] 