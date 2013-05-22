The behavior of SpecFlow can be extensively configured through .NET configuration files. SpecFlow
processes the configuration file of the acceptance test projects (the projects that contain the feature
files). The configuration has to be placed in a file called “App.config” (the standard configuration file
convention for .NET).

Unlike other runtime-only tools, SpecFlow processes the configuration file also while it generates the
unit-tests from the feature files (this happens usually when you save the feature file). This means
that after you have changed the configuration file, you might need to force re-generation of the unit
test (if the configuration change affects the generated tests). The [[Visual Studio integration|Visual Studio 2010 Integration]] can detect the change of the configuration file and offers re-generation. In Visual Studio you can also force re-generation from the context menu of the project node in the solution explorer.

## Default Configuration

In SpecFlow every configuration option has a default setting, so in an extreme case you don’t need to
specify any configuration file.
Commonly the most important thing to configure is the unit test provider. Therefore simple
SpecFlow projects configure only this aspect. The following example shows such a simple
configuration.

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

The following example shows all possible configuration option with their default values (the config section definition has been omitted for better readability).

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
    <!-- <stepAssembly assembly="{name-of-assembly-containing-bindgins}" /> -->
  </stepAssemblies>
  <plugins>
    <!-- <add name="{plugin-name}" /> -->
  </plugins>
</specFlow>
```
### Configuration Elements
#### `<language>`
This section can be used to define the default language for the feature files and other language-related
settings. Read more about the language settings in the [[Feature Language]] page.

<table>
    <tr>
        <th>Attribute</th>
        <th>Value</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>feature</td>
        <td>culture name (“en-US”)</td>
        <td>The default language of the feature files added to the project.
            It is recommended to use specific culture names (e.g.: “en-
            US”) and not generic (neutral) cultures (e.g.: “en”). <br/>
            Default: en-US</td>
    </tr>
    <tr>
        <td>tool</td>
        <td>empty or culture name</td>
        <td>Specifies the language that SpecFlow uses for messages and
            tracing. Uses the default feature language if empty if supported otherwise 
            the messages are displayed in English. (Currently only English is supported.)<br/>
            Default: empty</td>
    </tr>
</table>

#### `<bindingCulture>`

This section can be used to define the culture for executing binding methods and for converting step arguments. Read more about the language settings in the [[Feature Language]] page.

<table>
    <tr>
        <th>Attribute</th>
        <th>Value</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>name</td>
        <td>culture name (“en-US”)</td>
        <td>Specifies a culture to be used to execute binding methods and convert step arguments. If not specified, the feature language is used.<br/>
            Default: not specified</td>
    </tr>
</table>

#### `<unitTestProvider>`

This section can be used to specify the unit-test framework SpecFlow uses to execute the acceptance criteria. You can either use one of the built-in unit-test providers or you can specify the classes that implement the custom unit test providers.

<table>
    <tr>
        <th>Attribute</th>
        <th>Value</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>name</td>
        <td>Name of the unit test provider. See [[Unit Test Providers]].</td>
        <td>The name of the built-in unit test provider. If you specify this attribute, 
            you don’t have to specify the other two.<br/>
            Default: NUnit</td>
    </tr>
    <tr>
        <td>generatorProvider</td>
        <td>class name</td>
        <td>Obsolete, will be removed in v2.0. Use [[<code>&lt;plugins&gt;</code>|Plugins]] instead.</td>
    </tr>
    <tr>
        <td>runtimeProvider</td>
        <td>class name</td>
        <td>Obsolete, will be removed in v2.0. Use [[<code>&lt;plugins&gt;</code>|Plugins]] instead.</td>
    </tr>
</table>

#### `<generator>`

This section can be used to specify various unit-test generation options.

<table>
    <tr>
        <th>Attribute</th>
        <th>Value</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>allowDebugGeneratedFiles</td>
        <td>true|false</td>
        <td>The debugger is by default configured to step through the generated code. This helps to debug from the feature files directly to the bindings (see [[Debugging Tests]]). This feature can be disabled by setting this attribute to “true”.<br/>
            Default: false</td>
    </tr>
    <tr>
        <td>allowRowTests</td>
        <td>true|false</td>
        <td>Specifies if "row tests" should be generated for [[scenario outlines|Using Gherkin Language in SpecFlow]]. This setting is ignored if the [[unit test framework|Unit Test Providers]] does not support row based testing.<br/>
            Default: true</td>
    </tr>
    <tr>
        <td>generateAsyncTests</td>
        <td>true|false</td>
        <td>Specifies if the generated tests should support [[testing asynchronous code|Testing Silverlight Asynchronous Code]]. This setting is currently supported only for the Silverlight platform.<br/>
            Default: false</td>
    </tr>
    <tr>
        <td>path</td>
        <td>path relative to the project folder</td>
        <td>Specifies the custom folder of the SpecFlow generator to be used if it is not in the standard path search list. See [[Setup SpecFlow Projects]] for details.<br/>
            Default: not specified</td>
    </tr>
    <tr>
        <td>dependencies</td>
        <td>custom dependencies</td>
        <td>Specifies the custom dependencies SpecFlow generator. See [[Plugins]] for details.<br/>
            Default: not specified</td>
    </tr>
</table>

#### `<runtime>`

This section can be used to specify various test execution options.

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
            Default: true</td>
    </tr>
    <tr>
        <td>stopAtFirstError</td>
        <td>true|false</td>
        <td>Specifies whether the execution should stop at the first error or should continue to try matching the subsequent steps (in order to detect missing steps).<br/>
            Default: false</td>
    </tr>
    <tr>
        <td>missingOrPendingStepsOutcome</td>
        <td>Inconclusive|<br/>Ignore|<br/>Error</td>
        <td>Specifies how SpecFlow should behave if a step binding is not implemented or pending. See [[Missing, Pending or Improperly Configured Bindings|Test Result]].<br/>
            Default: Inconclusive</td>
    </tr>
    <tr>
        <td>dependencies</td>
        <td>custom dependencies</td>
        <td>Specifies the custom dependencies SpecFlow runtime. See [[Plugins]] for details.<br/>
            Default: not specified</td>
    </tr>
</table>

#### `<trace>`

This section can be used to configure how and what should SpecFlow trace out to the unit test output.

<table>
    <tr>
        <th>Attribute</th>
        <th>Value</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>traceSuccessfulSteps</td>
        <td>true|false</td>
        <td>Specifies whether SpecFlow should trace successful step binding executions. <br/>
            Default: true</td>
    </tr>
    <tr>
        <td>traceTimings</td>
        <td>true|false</td>
        <td>Specifies whether SpecFlow should trace execution time of the binding methods (only if the execution time is longer than the minTracedDuration value).<br/>
            Default: false</td>
    </tr>
    <tr>
        <td>minTracedDuration</td>
        <td>TimeSpan (0:0:0.1)</td>
        <td>Specifies a threshold for tracing the binding execution times.<br/>
            Default: 0:0:0.1 (100 ms)</td>
    </tr>
    <tr>
        <td>stepDefinitionSkeletonStyle</td>
        <td>RegexAttribute|<br/>MethodNameUnderscores|<br/>MethodNamePascalCase|<br/>MethodNameRegex</td>
        <td>Specifies the default [[step definition style|Step Definition Styles]].<br/>
            Default: RegexAttribute</td>
    </tr>
    <tr>
        <td>Listener</td>
        <td>class name</td>
        <td>Obsolete, will be removed in v2.0. Use [[<code>&lt;plugins&gt;</code>|Plugins]] instead.</td>
    </tr>
</table>

#### `<stepAssemblies>`

This section can be used to configure additional assemblies that contain bindings ([[external binding assemblies|
Use Bindings from External Assemblies]]). The assembly of the SpecFlow project (the project with the the feature files) is automatically included. The binding assemblies have to be placed in the output folder (e.g. bin/Debug) of the SpecFlow project, for example by adding a reference to the assembly from the project too. 

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

This section can be used to configure plugins that contain customizations. See [[Plugins]] page for details.

```xml
<specFlow>
  <plugins>
    <add name="MyPlugin" />
  </plugins>
</specFlow>
```

The `<plugins>` can contain multiple `<add>` elements (one for each plugin), with the following attributes.

<table>
    <tr>
        <th>Attribute</th>
        <th>Value</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>name</td>
        <td>plugins name</td>
        <td>The name of the plugin containing customizations.</td>
    </tr>
    <tr>
        <td>path</td>
        <td>path relative to the project folder</td>
        <td>Specifies the custom folder of the SpecFlow plugin to be used if it is not in the standard path search list. See [[Plugins]] for details.<br/>
            Default: not specified</td>
    </tr>
    <tr>
        <td>type</td>
        <td>Generator|<br/>Runtime|<br/>GeneratorAndRuntime</td>
        <td>Specifies whether the plugin customizes the generator, the runtime or both.<br/>
            Default: GeneratorAndRuntime</td>
    </tr>
</table>

