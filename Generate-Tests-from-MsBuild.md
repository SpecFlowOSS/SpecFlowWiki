_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Generate-Tests-from-MsBuild]]. We use the GitHub wiki for authoring the documentation pages._

SpecFlow's `generateall` function can also be used with MSBuild, allowing you to re-generate the class files before compiling the solution. This can be particularly useful if feature files are regularly modified outside of Visual Studio. More information on the `generateall` function can be found [[here|Tools]].

To be able to use this function, you need to update your project file. There are also a number of other options you can configure.

## Edit Your Project File
In order to use the `generateall` function with MSBuild, you need to update your project file. Add the following line to the end of the Visual Studio project file of the project containing the feature files (e.g. with notepad):

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

The [[SpecFlow NuGet package|NuGet Integration]] contains all files required by MsBuild to generate the tests in the `tools` folder. In order to be able to build your application in any environment, we recommend storing the contents of this directory together with your sources and to use a relative path.


## Change the Feature File Settings (optional)

When adding a feature file, Visual Studio automatically enters "SpecFlowSingleFileGenerator" as the **Custom Tool** in the file's properties. This ensures that the class files are re-generated whenever the feature file is saved. You can remove the custom tool to prevent this from occurring, as any class files that are not up-to-date will be generated during the build process anyway:

<img src=http://www.specflow.org/screenshots/CustomTool.png>

If you remove the code generator, or are also adding, renaming or deleting feature files outside of Visual Studio, you can include these files in your project dynamically. To do so, add the following lines to your project file (.csproj) in a text editor:

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