The “generate all” command can be also invoked from MsBuild. This way the unit test files can be updated before compiling the solution. This can be useful if the feature files are regularly modified outside of Visual Studio.

In order to enable this in your project, you have to modify the project file containing the feature files (e.g. with notepad). You have to add only one line to the end of project file as the following example shows.

```xml
  ...
  </ItemGroup>
  <Import Project="$(MSBuildBinPath)\Microsoft.CSharp.targets" />
  <Import Project="$(ProgramFiles)\TechTalk\SpecFlow\TechTalk.SpecFlow.targets"/>
  ...
</Project>
```

In order to be able to build your application in any environment independent of the SpecFlow installation it is recommended to store the SpecFlow tools together with your sources and use a relative path for the import.

```xml
<Import Project="..\lib\SpecFlow\TechTalk.SpecFlow.targets"/>
```

The TechTalk.SpecFlow.targets file can be investigated for further possibilities of calling this command from MsBuild.

See example at: [[https://github.com/techtalk/SpecFlow-Examples/tree/master/BowlingKata/BowlingKata-GenateTestsFromMsBuild]] (project Bowling.SpecFlow)

If the feature files are not only edited, but also added, renamed or deleted outside of Visual Studio, you can include them into the project dynamically. For this, you have to again change the project file directly once an include the following lines:

```xml
<ItemGroup>
  <!-- include all feature files from the folder "FeatureFiles" -->
  <None Include="FeatureFiles\**\*.feature" /> 
</ItemGroup>
<ItemGroup>
  <!-- include the generated test classes -->
  <Compile Include="FeatureFiles\**\*.cs">
    <Visible>false</Visible> <!-- the generated files can be hidden in Visual Studio -->
  </Compile>
</ItemGroup>
```

See example at: [[https://github.com/techtalk/SpecFlow-Examples/tree/master/BowlingKata/BowlingKata-GenateTestsFromMsBuild]] (project Bowling.SpecFlow.DynamicallyIncludedFeatureFiles)

