_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Feature-Language]]. We use the GitHub wiki for authoring the documentation pages._

To avoid communication errors introduced by translations, it is recommended to keep the specification and the acceptance test descriptions in the language of the business. The Gherkin format supports many natural languages besides English, like German, Spanish or French. More details about the supported languages are available [[here|https://github.com/cucumber/cucumber/wiki/Spoken-languages]]. 

The language of the feature files can be either specified globally in your configuration (see [[&lt;language&gt; element|Configuration]]), or in the feature file's header using the `#language` syntax. Specify the language using the ISO language names used by the `CultureInfo` class of the .NET Framework (e.g. `en-US`). 

```
#language: de-DE
Funktionalität: Addition
...
```

SpecFlow uses the feature file language to determine the set of keywords used to parse the file, but the language setting is also used as the default setting for converting parameters by the SpecFlow runtime. The culture for binding execution and parameter conversion can be specified explicitly, see [[&lt;bindingCulture&gt; element|Configuration]].

As data conversion can only be done using a specific culture in the .NET Framework it is recommended to use the specific culture name (e.g. `en-US`) instead of the neutral culture names (e.g. `en`). If a neutral culture is used, SpecFlow uses a specific default culture to convert data (e.g. `en-US` is used to convert data if the `en` language was used).