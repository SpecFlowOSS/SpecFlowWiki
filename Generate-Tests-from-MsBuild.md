_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Generate-Tests-from-MsBuild]]. We use the GitHub wiki for authoring the documentation pages._

## General

To get your code- behind- files generated at compile time, you need to simply add the [SpecFlow.Tools.MsBuild.Generation nuget package](https://www.nuget.org/packages/SpecFlow.Tools.MsBuild.Generation/) to your project.

## Removing the custom tool and include the generated files (optional)

When adding a feature file, Visual Studio automatically enters "SpecFlowSingleFileGenerator" as the **Custom Tool** in the file's properties. This ensures that the class files are re-generated whenever the feature file is saved. You can remove the custom tool to prevent this from occurring, as any class files that are not up-to-date will be generated during the build process anyway:

<img src=http://www.specflow.org/screenshots/CustomTool.png>

If you remove the code generator you have to include the generated files in your project dynamically. To do so, add the following lines to your project file (.csproj) in a text editor:

```xml
<Target Name="AfterUpdateFeatureFilesInProject">
    <!-- include any files that specflow generated into the compilation of the project -->
    <ItemGroup>
        <Compile Include="@(SpecFlowGeneratedFiles)" />
    </ItemGroup>
</Target>
```

## Define Additional Options (optional)
The `TechTalk.SpecFlow.targets` file defines a number of default options in the following section:

```xml
<PropertyGroup>
    <ShowTrace Condition="'$(ShowTrace)'==''">false</ShowTrace>
    <OverwriteReadOnlyFiles Condition="'$(OverwriteReadOnlyFiles)'==''">false</OverwriteReadOnlyFiles>
    <ForceGeneration Condition="'$(ForceGeneration)'==''">false</ForceGeneration>
    <VerboseOutput Condition="'$(VerboseOutput)'==''">false</VerboseOutput>
</PropertyGroup>
```
* `ShowTrace`: Set this to true to output trace information.
* `OverwriteReadOnlyFiles`: Set this to true to overwrite any read-only files in the target directory. This can be useful if your feature files are read-only and part of your repository.
* `ForceGeneration`: Set this to true to forces the code-behind files to be regenerated, even if the content of the feature has not changed. 
* `VerboseOutput`: Set to true to enable verbose output for troubleshooting.

To change these options, add the corresponding element to your project file **before** the `<Import>` element you added earlier.

**Example:**

```xml
<PropertyGroup>
  <ShowTrace>true</ShowTrace>
  <VerboseOutput>true</VerboseOutput>
</PropertyGroup>
...
</ItemGroup>
<Import Project="$(MSBuildBinPath)\Microsoft.CSharp.targets" />
<Import Project="..\packages\SpecFlow.2.2.0\tools\TechTalk.SpecFlow.tasks"  Condition="Exists('..\packages\SpecFlow.2.2.0\tools\TechTalk.SpecFlow.tasks')" />
<Import Project="..\packages\SpecFlow.2.2.0\tools\TechTalk.SpecFlow.targets" Condition="Exists('..\packages\SpecFlow.2.2.0\tools\TechTalk.SpecFlow.targets')" />
...
</Project>
```

You can find an example [[here|https://github.com/techtalk/SpecFlow-Examples/tree/master/BowlingKata/BowlingKata-GenateTestsFromMsBuild]] (project Bowling.SpecFlow)

<!--
## Including Feature Files Dynamically
If you are also adding, renaming or deleting feature files outside of Visual Studio, you can include these files in your project dynamically. To do so, add the following lines to your project file in a text editor:

An example can be found [[here|https://github.com/techtalk/SpecFlow-Examples/tree/master/BowlingKata/BowlingKata-GenateTestsFromMsBuild]] (project Bowling.SpecFlow.DynamicallyIncludedFeatureFiles)
-->

## Process the Generated Files (optional)

You can further process the generated files. The `TechTalk.SpecFlow.targets` file defines two targets (`BeforeUpdateFeatureFilesInProject` and `AfterUpdateFeatureFilesInProject`) that can be overridden. Furthermore it outputs the list of generated files for the MsBuild item `@(SpecFlowGeneratedFiles)`.

The following example shows an overridden `AfterUpdateFeatureFilesInProject` target that moves the generated files to a separate folder:

```xml
<Target Name="AfterUpdateFeatureFilesInProject">
  <Move 
    SourceFiles="@(SpecFlowGeneratedFiles)" 
    DestinationFolder="MyGeneratedFiles" 
    OverwriteReadOnlyFiles="true" />
</Target>
```