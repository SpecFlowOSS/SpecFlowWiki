_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Step-Definition-Styles]]. We use the GitHub wiki for authoring the documentation pages._

[[Step definitions]] provide the connection between the free-text specification steps and the application interfaces. Step definitions are .NET methods that match to certain scenario steps.

The classic way of providing the match rules is to annotate the method with regular expressions. From SpecFlow 1.9 however, you can also create the step definitions without regex.

This page contains information about the **different styles**, the **step definition skeleton generation** and about the **custom templates**. For general rules of step definitions, please check the [[Step Definitions]] page.

## Step Definition Styles

### Regular expressions in attributes

This is the classic way of specifying the step definitions. The step definition method has to be annotated with one or more step definitions attribute, with regular expressions.

```c#
[Given(@"I have entered (.*) into the calculator")]
public void GivenIHaveEnteredNumberIntoTheCalculator(int number)
{
  ...
}
```

Regular expression matching rules:

* The regular expressions are always matching to the entire step text even if you not use the `^` and `$` markers.
* The match groups (`(…)`) of the regular expression define the arguments for the method based on the order (the match result of the first group becomes the first argument, etc.).
* You can use non-capturing groups `(?:regex)` in order to use groups without a method argument.

### Method name - underscores

Most of the step definitions can also be specified without regular expression: the method should be named with underscored naming style (or pascal-case, see below) and should be annotated with an empty `[Given]`, `[When]`, `[Then]` or `[StepDefinition]` attribute. You can refer to the method parameters with either the parameter name (ALL-CAPS) or the parameter index (zero-based) with the `P` prefix, e.g. `P0`.

```c#
[Given]
public void Given_I_have_entered_NUMBER_into_the_calculator(int number)
{
  ...
}
```

Matching rules:
* The match is case-insensitive.
* Underscore character is matching to one or more non-word character (eg. whitespace, punctuation): `\W+`.
* For accented characters in the step the method name should also contain the accented character (no substitution). 
* The step keyword (e.g. `Given`) can be omitted: `[Given] public void I_have_entered_NUMBER_...`.
* The step keyword can be specified in the local Gherkin language (or English). The language can be specified in the [[app config|Configuration]] as feature language or binding culture. E.g. the following step definition is a valid "Given" step with German language settings: `[When] public void Wenn_ich_addieren_drücke()`

See detailed examples in our specs: [[StepDefinitionsWithoutRegex.feature|https://github.com/techtalk/SpecFlow/blob/master/Tests/TechTalk.SpecFlow.Specs/Features/StepDefinitionsWithoutRegex.feature]].

### Method name - pascal-case

Similarly to the underscored naming style, you can also specify the step definitions with pascal-case method names. 

```c#
[Given]
public void GivenIHaveEnteredNUMBERIntoTheCalculator(int number)
{
  ...
}
```

Matching rules:
* All rules of "Method name - underscores" style applied.
* Any potential word boundary (e.g. number-letter, uppercase-lowercase, uppercase-uppercase) is matching to zero or more non-word character (eg. whitespace, punctuation): `\W*`.
* You can mix this style with underscores. For example, the parameter placeholders can be highlighted this way: `GivenIHaveEntered_P0_IntoTheCalculator(int number)`

### Method name - regex (F# only)

F# allows providing any characters in method names, so you can make the regular expression as the method name, if you use [[F# bindings||FSharp Support]].

```F#
let [<Given>] ``I have entered (.*) into the calculator``(number:int) = 
    Calculator.Push(number)
```

## Generating Step Definition Skeletons

The step definition method declarations (aka _step definition skeletons_) can be generated from Visual Studio. Select "Generate Step Definitions" from the context menu of the feature file and the appearing dialog will guide you how to create a new binding class with the step definitions for the selected unbound steps. The most common parameter usage patterns (quotes, apostrophes, numbers) are detected so SpecFlow generates the methods and the annotation with the these parameters.

The same skeleton generator engine is used by the SpecFlow runtime (when you execute a scenario with unbound steps) and also in the "Go To Definition" command. In these places you cannot select a step definition style, so a default style is used (see below).

### Specifying default style

The default step definition style is taken from the [[configuration]] (or uses the "Regular expressions in attributes" if not specified. The following example changes the default style to underscored method names (available options: `RegexAttribute`, `MethodNameUnderscores`, `MethodNamePascalCase`, `MethodNameRegex`)

```xml
<specFlow>
  <trace stepDefinitionSkeletonStyle="MethodNameUnderscores" />
</specFlow>
```

## Customizing Step Definition Skeleton Templates

If you want to include a custom using statement or a base class declaration to the generated step definition skeletons, you can also customize the templates. Just place a text file called `SkeletonTemplates.sftemplate` into the SpecFlow folder inside your local app data (e.g. `C:\Users\me\AppData\Local\SpecFlow\SkeletonTemplates.sftemplate`) to override the necessary templates.

The template file contains sections, one for each template. In the custom template file you can override one or more sections. For all other sections, the default template will be used. The sections are separated with the `>>>` line prefix followed by the identifier of the section. The templates can refer to different parameters with the `{param}` syntax.

The following example overrides the class generation skeleton for C# and specifies a custom comment in the file header:

```
>>>CSharp/StepDefinitionClass
/****************************
 *    SpecFlow Rocks!
 ****************************/
using System;
using TechTalk.SpecFlow;

namespace {namespace}
{
    [Binding]
    public class {className}
    {
{bindings}
    }
}
```

For the full list of available sections, parameters and for examples, check the [[default template|https://github.com/techtalk/SpecFlow/blob/master/TechTalk.SpecFlow/BindingSkeletons/DefaultSkeletonTemplates.sftemplate]].



