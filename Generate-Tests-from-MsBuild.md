_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Generate-Tests-from-MsBuild]]. We use the GitHub wiki for authoring the documentation pages._

The “generate all” command can be also invoked from MsBuild. This way the unit test files can be updated before compiling the solution. This can be useful if the feature files are regularly modified outside of Visual Studio.

In order to enable this in your project, you have to modify the project file containing the feature files (e.g. with notepad). You have to add only one line to the end of project file as the following example shows.

In order to be able to build your application in any environment independent of the SpecFlow installation it is recommended to store the SpecFlow tools together with your sources and use a relative path for the import. The [[SpecFlow NuGet package|NuGet Integration]] also contains all necessary files to support MsBuild generation (`tools` folder).

```xml
  ...
  </ItemGroup>
  <Import Project="$(MSBuildBinPath)\Microsoft.CSharp.targets" />
  <Import Project="..\packages\SpecFlow.2.2.0\tools\TechTalk.SpecFlow.targets" Condition="Exists('..\packages\SpecFlow.2.2.0\tools\TechTalk.SpecFlow.targets')" />
  ...
</Project>
```

The TechTalk.SpecFlow.targets file can be investigated for further possibilities of calling this command from MsBuild.

See example at: [[https://github.com/techtalk/SpecFlow-Examples/tree/master/BowlingKata/BowlingKata-GenateTestsFromMsBuild]] (project Bowling.SpecFlow)

**Attention:**
If you are using NuGet package restore, you have to restart Visual Studio and reopen your project, so that Visual Studio can reevaluate the project file and import the TechTalk.SpecFlow.targets.

If the feature files are not only edited, but also added, renamed or deleted outside of Visual Studio, you can include them into the project dynamically. For this, you have to again change the project file directly once an include the following lines:

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

See example at: [[https://github.com/techtalk/SpecFlow-Examples/tree/master/BowlingKata/BowlingKata-GenateTestsFromMsBuild]] (project Bowling.SpecFlow.DynamicallyIncludedFeatureFiles)

It is also possible (from v1.8) to further process the generated files. The `TechTalk.SpecFlow.targets` file defines two targets (`BeforeUpdateFeatureFilesInProject` and `AfterUpdateFeatureFilesInProject`) that can be overridden. Furthermore it populates the list of generated files to the MsBuild item `@(SpecFlowGeneratedFiles)`.

The following example shows an overridden `AfterUpdateFeatureFilesInProject` target that moves the generated files to a separate folder.

```xml
<Target Name="AfterUpdateFeatureFilesInProject">
  <Move 
    SourceFiles="@(SpecFlowGeneratedFiles)" 
    DestinationFolder="MyGeneratedFiles" 
    OverwriteReadOnlyFiles="true" />
</Target>
```