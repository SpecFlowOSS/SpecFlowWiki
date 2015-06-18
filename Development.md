_Note:_ This description is quite outdated. 

## Structure

The source code of SpecFlow is included in a single Visual Studio 2008 solution (TechTalk.SpecFlow.sln), located in the main folder.

Besides the source code, the SpecFlow reporsitory also contains a "Samples" folder where you can find code samples (might be included into the installer later).

The source code is divided into the following categories:

* Installer - All code related to the SpecFlow installer:
  * Location: "Installer" folder
  * Projects:
    * SpecFlowSetup - the setup project
    * DevenvSetupCustomAction - a custom action to call "devenv /setup" during installation 
* Generator (aka Parser) - All code related to generating unit test classes from feature files
  * Includes Gherkin parser
  * Does not have a static dependency on the "Runtime" components to allow side-by-side runtime versions
  * Location: "Parser" folder 
* VsIntegration - All code related to Visual Studio 2008 integration
  * Includes SingleFileGenerator for the ".feature" files
  * Location: "VsIntegration" folder 
* Runtime - All code related to the execution of the generated tests
  * Includes
    * the "TestRunner" class (entry point of the generated test methods)
    * the dynamic binding resolution and execution logic
    * the binding attributes
    * the FeatureContext/ScenarioContext classes
    * the tracing logic 
  * Location: "Runtime" folder 
* Tests - Unit tests for the generator and the runtime components
  * Location: Tests
  * Projects:
    * ParserTests - tests for the parser and the generator
    * RuntimeTests - test for the runtime component 
* Reporting - All code related to SpecFlow reports
  * Includes
    * Step Definition Report - a report about usage and binding of scenario steps
    * NUnit Execution Report - a report that visualizes the nunit execution result in SpecFlow style 
  * Does not have a static dependency on the "Runtime" components to allow side-by-side runtime versions
  * Location: "Reporitng" folder 

## Conventions

Here is a list of code structuring conventions that we follow:

* The projects are named, like the full namespace (e.g. TechTalk.SpecFlow.Parser), but located in a folder with the short name (e.g. Parser). This is useful to stay below the VS path length limit.
* All external dependency (like nunit.framework) is located in the "lib" folder.
* All project includes (as a link) the VersionInfo.cs file from the root folder (to make the version changes easier).
* If you have finished working on a branch (that has been pushed at least once), you should delete it after merging back. Here is a description how: [[Remove a remote branch|http://github.com/guides/remove-a-remote-branch]] 

## Smoke Test

**installer tests**

   1. Run the installer on a machine where one of the previous versions were installed
          * it should upgrade 

**basic tests with NUnit**

   1. Create a new solution with a new class library project
   2. Add references to TechTalk.SpecFlow.dll and nunit.framework.dll
   3. Add a new feature file from the VS "add new item" dialog
          * the generated classes should compile 
   4. Run the unit tests
          * there should be one test (AddTwoNumbers)
          * it should result in a pending state (no binding for steps) 
   5. Add a new "step definition" from the VS "add new item" dialog
          * project should compile 
   6. Comment out "pending" steps in the step definition file
   7. Run the unit tests
          * test should pass 
   8. Add a new "event definition" from the VS "add new item" dialog
          * project should compile 
   9. Run the unit tests
          * test should succeed 

**basic tests with MsTest**

   1. Add a test project to the solution (remove default items)
   2. Add references to TechTalk.SpecFlow.dll
   3. Add an App.config file to the project with the following settings

      <?xml version="1.0" encoding="utf-8" ?>
      <configuration>
        <configSections>
          <section name="specFlow" type="TechTalk.SpecFlow.Configuration.ConfigurationSectionHandler, TechTalk.SpecFlow"/>
        </configSections>

        <specFlow>
          <unitTestProvider name="MsTest" />
        </specFlow>
      </configuration>

   4. Add a new feature file from the VS "add new item" dialog
          * the generated classes should compile 
   5. Run the unit tests (Test/Run/All Tests in Solution)
          * there should be one test (AddTwoNumbers)
          * it should result in a pending state (no binding for steps) 
   6. Add a new "step definition" from the VS "add new item" dialog
          * project should compile 
   7. Run the unit tests
          * test should pass

## Release Process

 The following steps has to be done to release SpecFlow:

   1. make sure that the solution compiles and all unit tests pass
   2. define a new version number based on the VersioningPolicy
   3. review/update the changelog.txt file with the version number and the date
   4. update the VersionInfo?.cs file
   5. set the new version number in the SpecFlowSetup project properties
          * will ask to generate a new product code, allow it (required for upgrade install) 
   6. compile the SpecFlowSetup? project
   7. apply some SmokeTests for the created release
   8. compress the msi + setup.exe together to a zip file named like: SpecFlowSetup_v1.0.2.zip
   9. tag the master branch with a tag like "v1.0.2"
          * you can push local tags with "git push --tags" 
  10. publish the zip to the website (how?)
  11. announce the new release (how?) 

## Versioning Policy

Bugfix releases: increase the 3rd number (like 1.0.1 -> 1.1.2)

Minor feature releases: increase the 2nd number (like 1.0.2 -> 1.1.0)

Major feature releases: increase the 1st number (like 1.1.2 -> 2.0.0) 