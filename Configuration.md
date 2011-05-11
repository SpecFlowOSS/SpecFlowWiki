## Configuration

The behavior of SpecFlow can be extensively configured through .NET configuration files. SpecFlow
processes the configuration file of the acceptance test projects (the projects that contain the feature
files). The configuration has to be placed in a file called “App.config” (the standard configuration file
convention for .NET).

Unlike other runtime-only tools, SpecFlow processes the configuration file also while it generates the
unit-tests from the feature files (this happens usually when you save the feature file). This means
that after you have changed the configuration file, you might need to force re-generation of the unit
test (if the configuration change affects the generated tests). The [[Visual Studio 2010 Integration]] can 
detect the change of the configuration file and offers re-generation.

## Default Configuration

In SpecFlow all configuration option has a default setting, so in an extreme case you don’t need to
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
      allowRowTests="true" />
  <runtime 
      detectAmbiguousMatches="true"
      stopAtFirstError="false"
      missingOrPendingStepsOutcome="Inconclusive" />
  <trace 
      traceSuccessfulSteps="true"
      traceTimings="false"
      minTracedDuration="0:0:0.1"
      listener="TechTalk.SpecFlow.Tracing.DefaultListener, TechTalk.SpecFlow" />
  <stepAssemblies>
    <!-- <stepAssembly assembly="{name-of-assembly-containing-bindgins}" /> -->
  </stepAssemblies>
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
        <td>An assembly qualified class name of a class that implements 
            <code>TechTalk.SpecFlow.Generator.UnitTestProvider.IUnitTestGeneratorProvider</code>
            interface.</td>
    </tr>
    <tr>
        <td>runtimeProvider</td>
        <td>class name</td>
        <td>An assembly qualified class name of a class that implements 
            <code>TechTalk.SpecFlow.UnitTestProvider.IUnitTestRuntimeProvider</code>
            interface.</td>
    </tr>
</table>

#### `<generator>`

#### `<runtime>`

#### `<trace>`

#### `<stepAssemblies>`