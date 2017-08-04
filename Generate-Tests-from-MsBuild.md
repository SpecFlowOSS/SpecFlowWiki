_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Generate-Tests-from-MsBuild]]. We use the GitHub wiki for authoring the documentation pages._

You can invoke the “generate all” command from MsBuild. This allows you to update the unit test files before compiling the solution, which can be useful if feature files are regularly modified outside of Visual Studio. 

## Feature File Settings

When adding a feature file, Visual Studio automatically enters "SpecFlowSingleFileGenerator" as the **Custom Tool** in the file's properties. You need to remove the custom tool in all your feature files:

<img src=http://www.specflow.org/screenshots/CustomTool.png>


## Editing Your Project

You need to add the following line to the end of the project file containing the feature files (e.g. with notepad):

```xml
<Import Project="..\packages\SpecFlow.2.2.0\tools\TechTalk.SpecFlow.targets" Condition="Exists('..\packages\SpecFlow.2.2.0\tools\TechTalk.SpecFlow.targets')" />
```

**Example:**

```xml
...
</ItemGroup>
<Import Project="$(MSBuildBinPath)\Microsoft.CSharp.targets" />
<Import Project="..\packages\SpecFlow.2.2.0\tools\TechTalk.SpecFlow.targets" Condition="Exists('..\packages\SpecFlow.2.2.0\tools\TechTalk.SpecFlow.targets')" />
...
</Project>
```

The [[SpecFlow NuGet package|NuGet Integration]] contains all necessary files to support MsBuild generation in the `tools` folder. In order to be able to build your application in any environment, we recommend storing the SpecFlow tools together with your sources and using a relative path. 

<!--
REMOVED DUE TO  NOT CONTAINING ANY PERTINENT INFO. IF YOU KNOW WHAT THESE "FURTHER POSSIBILITIES" ARE, PLEASE ADD THEM HERE.
The TechTalk.SpecFlow.targets file can be investigated for further possibilities of calling this command from MsBuild.


See example at: [[https://github.com/techtalk/SpecFlow-Examples/tree/master/BowlingKata/BowlingKata-GenateTestsFromMsBuild]] (project Bowling.SpecFlow)
-->

**WARNING:** If you are using NuGet package restore, restart Visual Studio and reopen your project. This is necessary so that Visual Studio can re-evaluate the project file and import the TechTalk.SpecFlow.targets.

## Including Feature Files Dynamically
If you are also adding, renaming or deleting feature files outside of Visual Studio, you can include these files in your project dynamically. To do so, add the following lines to your project file in a text editor:

```xml
<ItemGroup>
  <!-- include all feature files from the folder "FeatureFiles" -->
  <None Include="FeatureFiles\**\*.feature" /> 
</ItemGroup>
<Target Name="AfterUpdateFeatureFilesInProject">
    <!-- include any files that specflow generated into the compilation of the project -->
    <ItemGroup>
        <Compile Include="@(SpecFlowGeneratedFiles)" />
    </ItemGroup>
</Target>
```

An example can be found at: [[here|https://github.com/techtalk/SpecFlow-Examples/tree/master/BowlingKata/BowlingKata-GenateTestsFromMsBuild]] (project Bowling.SpecFlow.DynamicallyIncludedFeatureFiles)

## Processing the Generated Files

You can also further process the generated files. The `TechTalk.SpecFlow.targets` file defines two targets (`BeforeUpdateFeatureFilesInProject` and `AfterUpdateFeatureFilesInProject`) that can be overridden. Furthermore it outputs the list of generated files for the MsBuild item `@(SpecFlowGeneratedFiles)`.

The following example shows an overridden `AfterUpdateFeatureFilesInProject` target that moves the generated files to a separate folder:

```xml
<Target Name="AfterUpdateFeatureFilesInProject">
  <Move 
    SourceFiles="@(SpecFlowGeneratedFiles)" 
    DestinationFolder="MyGeneratedFiles" 
    OverwriteReadOnlyFiles="true" />
</Target>
```