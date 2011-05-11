To avoid communication errors introduced by translations, it is recommended to keep the specification and the acceptance test descriptions in the language of the business. The Gherkin format supports many natural languages besides English, like German, Spanish or French. See more about the supported languages at [[https://github.com/aslakhellesoy/cucumber/wiki/Spoken-languages]]. 

The language of the feature files can be either specified globally in the configuration (see [[&lt;language&gt; element|Configuration]]) or in the header of the feature file with the `#language` syntax. The language has to be specified using the ISO language names used by the `CultureInfo` class of the .NET Framework (like `en-US`). 

```
#language: de-DE
Funktionalität: Addition
...
```

SpecFlow uses the feature file language to use the right set of keywords when parsing the file, but the language setting is also used as a default when any parameter conversion has to be done by the SpecFlow runtime. The culture for binding execution and parameter conversion can be specified explicitly, see [[&lt;bindingCulture&gt; element|Configuration]].

As data conversion can only be done using a specific culture in the .NET Framework it is recommended to use the specific culture name (`en-US`) instead of the neutral culture names (`en`). If a neutral culture is used, SpecFlow uses a default specific culture for data conversions (e.g. uses the `en-US` for conversion if the `en` language was used).
