## Configuration

The behavior of SpecFlow can be extensively configured through .NET configuration files. SpecFlow
processes the configuration file of the acceptance test projects (the projects that contain the feature
files). The configuration has to be placed in a file called “App.Config” (the standard configuration file
convention for .NET).

Unlike other runtime-only tools, SpecFlow processes the configuration file also while it generates the
unit-tests from the feature files (this happens usually when you save the feature file). This means
that after you have changed the configuration file, you might need to force re-generation of the unit
test (if the configuration change affects the generated tests). See Regenerate Unit Tests for details
about how this can be done.

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
      type="TechTalk.SpecFlow.Configuration.ConfigurationSectionHandler,
      TechTalk.SpecFlow"/>
  </configSections>
  <specFlow>
    <unitTestProvider name="MsTest" />
  </specFlow>
</configuration>
```
The following example shows all possible configuration option with their default values.

```xml
<specFlow>
<language feature="en-US" tool="" />
<unitTestProvider name="NUnit" />
<generator allowDebugGeneratedFiles="false" />
<runtime detectAmbiguousMatches="true"
stopAtFirstError="false"
missingOrPendingStepsOutcome="Inconclusive" />
<trace traceSuccessfulSteps="true"
traceTimings="false"
minTracedDuration="0:0:0.1"
listener="TechTalk.SpecFlow.Tracing.DefaultListener,
TechTalk.SpecFlow" />
</specFlow>
```
### Configuration Elements
`<language>`
This section can be used to define the default language for the feature files and other languagerelated
settings. Learn more about the language settings in the Feature Language section.

<table>
    <tr>
        <th>Attribute</th>
        <th>Value</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>Feature</td>
        <td>culture name (“en-US”)</td>
        <td>The default language of the feature files added to the project.
            It is recommended to use specific culture names (e.g.: “en-
            US”) and not generic (neutral) cultures (e.g.: “en”).
            Default: en-US</td>
    </tr>
    <tr>
        <td>Tool</td>
        <td>empty or culture name</td>
        <td>Specifies the language that SpecFlow uses for messages and
            tracing. Uses the default feature language if empty. (Currently
            only English is used for messages.)
            Default: empty</td>
    </tr>
</table>



