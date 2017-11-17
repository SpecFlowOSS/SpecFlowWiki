_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Configuration]]. We use the GitHub wiki for authoring the documentation pages._

SpecFlow's behaviour can be configured extensively using the standard .NET configuration file, `App.config`, which is automatically added to your project. SpecFlow processes this configuration file in test projects containing feature files.

Unlike other runtime-only tools, SpecFlow also processes the configuration file when generating the unit tests from feature files (which usually happens when you save the feature file). This means that once you have changed the configuration file, you may need to force the unit test to be regenerated if the configuration change affects the generated tests. The [[Visual Studio integration]] can detect changes to the configuration file and will prompt you to regenerate the tests. To force the unit tests to be regenerated, right-click on your project in Visual Studio's Solution Explorer and select **Regenerate Feature Files** from the menu.

## Default Configuration

All SpecFlow configuration options have a default setting. In general, configuring your unit test provider is the most important configuration option required, and simple SpecFlow projects may not require any more configuration. The following example shows a simple configuration file.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <section name="specFlow"
      type="TechTalk.SpecFlow.Configuration.ConfigurationSectionHandler, TechTalk.SpecFlow"/>
  </configSections>
  <specFlow>
    <unitTestProvider name="MsTest" />
  </specFlow>
</configuration>
```

The following example shows all possible configuration options with their default values (the `<configSections>` element has been omitted for better readability).

```xml
<specFlow>
  <language feature="en-US" tool="{not-specified}" />
  <bindingCulture name="{not-specified}" />
  <unitTestProvider name="NUnit" />
  <generator 
      allowDebugGeneratedFiles="false" 
      allowRowTests="true"
      generateAsyncTests="false"
      path="{not-specified}" />
  <runtime 
      stopAtFirstError="false"
      missingOrPendingStepsOutcome="Inconclusive" />
  <trace 
      traceSuccessfulSteps="true"
      traceTimings="false"
      minTracedDuration="0:0:0.1"
      stepDefinitionSkeletonStyle="RegexAttribute" />
  <stepAssemblies>
    <!-- <stepAssembly assembly="{name-of-assembly-containing-bindings}" /> -->
  </stepAssemblies>
  <plugins>
    <!-- <add name="{plugin-name}" /> -->
  </plugins>
</specFlow>
```
### Configuration Elements

#### `<language>`

Use this section to define the default language for feature files and other language-related settings. For more details on language settings, see [[Feature Language]].

<table>
    <tr>
        <th>Attribute</th>
        <th>Value</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>feature</td>
        <td>culture name (“en-US”)</td>
        <td>The default language of feature files added to the project. We recommend using specific culture names (e.g.: “en-US”) rather than generic (neutral) cultures (e.g.: “en”). <br/>
            <b>Default:</b> en-US</td>
    </tr>
    <tr>
        <td>tool</td>
        <td>empty or culture name</td>
        <td>Specifies the language that SpecFlow uses for messages and tracing. Uses the default feature language if empty and that language is supported; otherwise messages are displayed in English. (<b>Note:</b> Only English is currently supported.)<br/>
            <b>Default:</b> empty</td>
    </tr>
</table>

#### `<bindingCulture>`

Use this section to define the culture for executing binding methods and converting step arguments. For more details on language settings, see [[Feature Language]].

<table>
    <tr>
        <th>Attribute</th>
        <th>Value</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>name</td>
        <td>culture name (“en-US”)</td>
        <td>Specifies the culture to be used to execute binding methods and convert step arguments. If not specified, the feature language is used.<br/>
            <b>Default:</b> not specified</td>
    </tr>
</table>

#### `<unitTestProvider>`

Use this section to specify the unit test framework used by SpecFlow to execute acceptance criteria. You can either use one of the built-in unit test providers or you can specify the classes that implement custom unit test providers.

<table>
    <tr>
        <th>Attribute</th>
        <th>Value</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>name</td>
        <td>Name of the unit test provider. See [[Unit Test Providers]].</td>
        <td>The name of the built-in unit test provider. If you specify this attribute, you don’t have to specify the other two.<br/><br />
            <b>Default:</b> nunit
<br /><br />

The following lists all supported providers with their name and generator provider class name:

<table>
 <tr>
  <th>Name</th>
  <th>Runtime Provider</th>
 </tr>
 <tr>
  <td>specrun</td>
  <td>SpecRunTestGeneratorProvider, see [[the SpecFlow+ documentation|https://specflow.org/plus/documentation/]]</td>
 </tr>
 <tr>
  <td>nunit</td>
  <td>NUnit3TestGeneratorProvider</td>
 </tr>
 <tr>
  <td>nunit.2</td>
  <td>NUnit2TestGeneratorProvider</td>
 </tr>
 <tr>
  <td>mbunit</td>
  <td>MbUnitTestGeneratorProvider</td>
 </tr>
 <tr>
  <td>mbunit.3</td>
  <td>MbUnit3TestGeneratorProvider</td>
 </tr>
 <tr>
  <td>xunit.1</td>
  <td>XUnitGeneratorProvider</td>
 </tr>
 <tr>
  <td>xunit</td>
  <td>XUnit2GeneratorProvider</td>
 </tr>
 <tr>
  <td>mstest.2008</td>
  <td>MsTestGeneratorProvider</td>
 </tr>
 <tr>
  <td>mstest</td>
  <td>MsTest2010GeneratorProvider</td>
 </tr>
</table>
</td>
    </tr>
    <tr>
        <td>generatorProvider</td>
        <td>class name</td>
        <td>Obsolete; will be removed in v2.0. Use [[<code>&lt;plugins&gt;</code>|Plugins]] instead.</td>
    </tr>
    <tr>
        <td>runtimeProvider</td>
        <td>class name</td>
        <td>Obsolete; will be removed in v2.0. Use [[<code>&lt;plugins&gt;</code>|Plugins]] instead.</td>
    </tr>
</table>



#### `<generator>`

Use this section to define unit test generation options.

<table>
    <tr>
        <th>Attribute</th>
        <th>Value</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>allowDebugGeneratedFiles</td>
        <td>true|false</td>
        <td>By default, the debugger is configured to step through the generated code. This helps you debug your feature files and bindings (see [[Debugging Tests]]). Disabled this option by setting this attribute to “true”.<br/>
            <b>Default:</b> false</td>
    </tr>
    <tr>
        <td>allowRowTests</td>
        <td>true|false</td>
        <td>Determines whether "row tests" should be generated for [[scenario outlines|Using Gherkin Language in SpecFlow]]. This setting is ignored if the [[unit test framework|Unit Test Providers]] does not support row based testing.<br/>
            <b>Default:</b> true</td>
    </tr>
    <tr>
        <td>generateAsyncTests</td>
        <td>true|false</td>
        <td>Determines whether the generated tests should support [[testing asynchronous code|Testing Silverlight Asynchronous Code]]. This setting is currently only supported for the Silverlight platform.<br/>
            <b>Default:</b> false</td>
    </tr>
    <tr>
        <td>path</td>
        <td>path relative to the project folder</td>
        <td>Specifies the custom folder of the SpecFlow generator to be used if it is not in the standard path search list. See [[Setup SpecFlow Projects]] for details.<br/>
            <b>Default:</b> not specified</td>
    </tr>
    <tr>
        <td>dependencies</td>
        <td>custom dependencies</td>
        <td>Specifies the custom dependencies for the SpecFlow generator. See [[Plugins]] for details.<br/>
            <b>Default:</b> not specified</td>
    </tr>
</table>

#### `<runtime>`

Use this section to specify various test execution options.

<table>
    <tr>
        <th>Attribute</th>
        <th>Value</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>detectAmbiguousMatches</td>
        <td>true|false</td>
        <td>Obsolete, will be removed in v2.0.<br/>
            <b>Default:</b> true</td>
    </tr>
    <tr>
        <td>stopAtFirstError</td>
        <td>true|false</td>
        <td>Determines whether the execution should stop when encountering the first error, or whether it should attempt to try and match subsequent steps (in order to detect missing steps).<br/>
            <b>Default:</b> false</td>
    </tr>
    <tr>
        <td>missingOrPendingStepsOutcome</td>
        <td>Inconclusive|<br/>Ignore|<br/>Error</td>
        <td>Determines how SpecFlow behaves if a step binding is not implemented or pending. See [[Missing, Pending or Improperly Configured Bindings|Test Result]].<br/>
            <b>Default:</b> Inconclusive</td>
    </tr>
    <tr>
        <td>dependencies</td>
        <td>custom dependencies</td>
        <td>Specifies custom dependencies for the SpecFlow runtime. See [[Plugins]] for details.<br/>
            <b>Default:</b> not specified</td>
    </tr>
</table>

#### `<trace>`

Use this section to determine the SpecFlow trace output.

<table>
    <tr>
        <th>Attribute</th>
        <th>Value</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>traceSuccessfulSteps</td>
        <td>true|false</td>
        <td>Determines whether SpecFlow should trace successful step binding executions. <br/>
            <b>Default:</b> true</td>
    </tr>
    <tr>
        <td>traceTimings</td>
        <td>true|false</td>
        <td>Determines whether SpecFlow should trace execution time of the binding methods (only if the execution time is longer than the minTracedDuration value).<br/>
            <b>Default:</b> false</td>
    </tr>
    <tr>
        <td>minTracedDuration</td>
        <td>TimeSpan (0:0:0.1)</td>
        <td>Specifies a threshold for tracing the binding execution times.<br/>
            <b>Default:</b> 0:0:0.1 (100 ms)</td>
    </tr>
    <tr>
        <td>stepDefinitionSkeletonStyle</td>
        <td>RegexAttribute|<br/>MethodNameUnderscores|<br/>MethodNamePascalCase|<br/>MethodNameRegex</td>
        <td>Specifies the default [[step definition style|Step Definition Styles]].<br/>
            <b>Default:</b> RegexAttribute</td>
    </tr>
    <tr>
        <td>Listener</td>
        <td>class name</td>
        <td>Obsolete, will be removed in v2.0. Use [[<code>&lt;plugins&gt;</code>|Plugins]] instead.</td>
    </tr>
</table>

#### `<stepAssemblies>`

This section can be used to configure additional assemblies that contain [[external binding assemblies|Use Bindings from External Assemblies]]. The assembly of the SpecFlow project (the project containing the feature files) is automatically included. The binding assemblies must be placed in the output folder (e.g. bin/Debug) of the SpecFlow project, for example by adding a reference to the assembly from the project. 

The following example registers an additional binding assembly (MySharedBindings.dll). 

```xml
<specFlow>
  <stepAssemblies>
    <stepAssembly assembly="MySharedBindings" />
  </stepAssemblies>
</specFlow>
```

The `<stepAssemblies>` can contain multiple `<stepAssembly>` elements (one for each assembly), with the following attributes.

<table>
    <tr>
        <th>Attribute</th>
        <th>Value</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>assembly</td>
        <td>assembly name</td>
        <td>The name of the assembly containing bindings.</td>
    </tr>
</table>

#### `<plugins>`

This section can be used to configure plugins that contain customisations. See [[Plugins]] for more details.

```xml
<specFlow>
  <plugins>
    <add name="MyPlugin" />
  </plugins>
</specFlow>
```

The `<plugins>` element can contain multiple `<add>` elements (one for each plugin), with the following attributes:

<table>
    <tr>
        <th>Attribute</th>
        <th>Value</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>name</td>
        <td>plugin name</td>
        <td>The name of the plugin containing the customisations.</td>
    </tr>
    <tr>
        <td>path</td>
        <td>path relative to the project folder</td>
        <td>Specifies the custom folder of the SpecFlow plugin to be used if it is not in the standard path search list. See [[Plugins]] for details.<br/>
            <b>Default:</b> not specified</td>
    </tr>
    <tr>
        <td>type</td>
        <td>Generator|<br/>Runtime|<br/>GeneratorAndRuntime</td>
        <td>Specifies whether the plugin customises the generator, the runtime or both.<br/>
            <b>Default:</b> GeneratorAndRuntime</td>
    </tr>
</table>
