The feature files that are used by SpecFlow to store the acceptance criteria of the features (use cases, user stories) of your application are described in a format that is called Gherkin. The Gherkin language defines the structure and a basic syntax for describing the tests. The Gherkin format was introduced by [[Cucumber|http://cukes.info/]] is also used by other tools. 

The Gherkin language is maintained as a separate project on GitHub: [[https://github.com/cucumber/gherkin]]. A detailed description of the language can be found at [[https://github.com/cucumber/cucumber/wiki/Gherkin]].

In this page we focus on the how SpecFlow handles the different Gherkin language elements. 

##Features
The feature element provides the header or frame for the feature file. The feature has a title and a free-text high level description of the feature of your application that is detailed in the file. See more details at [[https://github.com/cucumber/cucumber/wiki/Feature-Introduction]].

SpecFlow generates a unit-test class for the feature element. The class name will be derived from the title of the feature.

##Scenarios
The feature file may contain multiple scenarios. The scenarios can be used to describe the acceptance tests of the feature. The scenario has a title and multiple scenario steps. See more details at [[https://github.com/cucumber/cucumber/wiki/Feature-Introduction]].

SpecFlow generates a unit test method for each scenario. The method name will be derived from the title of the scenario.

##Scenario Steps
The scenarios may contain multiple scenario steps. These steps describe the preconditions, the actions and the verification steps of the acceptance test (other terminologies are using arrange, act and assert for these parts). These steps are introduced with the `Given`, `When` and `Then` keywords (in English feature files), but subsequent steps of the same kind can be also specified with the `And` and the `But` keyword. There may be other alternative keywords for specifying the steps.

The Gherkin syntax allows any combination or mixture of these three concepts, but usually the scenarios have a given, a when and a then block (set of steps).

The scenario steps are defined with a step text and can have additional table or multi-line text arguments.

See more details at [[https://github.com/cucumber/cucumber/wiki/Given-When-Then]].

SpecFlow generates a call inside the unit test method for each scenario step. The call is performed by the SpecFlow runtime that will execute the binding matching to the scenario step. The matching is done at runtime, so the generated tests can be compiled and executed even if the binding is not yet implemented. Read more about execution of test before the binding has been implemented: [[Missing, Pending or Improperly Configured Bindings|Test Result]].

The scenario steps are primary way to execute any custom code to automate the application. You can read more about the different bindings in the [[Bindings]] page.

##Table and multi-line text arguments
The scenario steps can have table or multi-line text arguments additionally to the step text (that can also contain arguments for the bindings, see [[Step Bindings]]). These are described in the subsequent lines of the scenario step and passed as additional Table and string arguments to the step bindings.

See more details at [[https://github.com/cucumber/cucumber/wiki/multiline-step-arguments]]

##Tags
Tags are markers that can be applied to features and scenarios. Applying a tag on a feature is equivalent to apply the tag to all scenarios in the feature file. See more details at [[https://github.com/cucumber/cucumber/wiki/Tags]].

If the [[unit test framework|Unit Test Providers]] supports it, SpecFlow generates categories from the tags. The generated category name is the tag name, without the leading `@` sign. With the generated unit test categories you can filter or group the tests being executed. For example by marking crucial test with the `@important` tag, you can execute these tests more frequently.

Even if the unit test framework does not support categories, you can use the tags to execute special logic for the tagged scenarios in [[event bindings]], [[scoped bindings]] or in the step bindings by investigating the `ScenarioContext.Current.ScenarioInfo.Tags` property. 

The `@ignore` tag is handled specially by SpecFlow. From the scenarios marked with this tag SpecFlow generates an ignored unit test method. See [[Ignored Tests|Test Result]].

##Background
The background language element allows specifying a common precondition for all scenarios in a feature file. The background part of the file can contain one or more scenario steps that are executed before any other steps of the scenarios. See more details at [[https://github.com/cucumber/cucumber/wiki/Background]]

SpecFlow generates a method from the background elements that is invoked from all unit tests generated for the scenarios.

##Scenario Outlines
Scenario outlines can be used to define data-driven acceptance tests. They can be also seen as scenario templates. The scenario outline always consists of a scenario template specification (a scenario with data placeholders using the `<placeholder>` syntax) and a set of examples that provide values for the placeholders. See more details at [[https://github.com/cucumber/cucumber/wiki/Scenario-outlines]].

If the [[unit test framework|Unit Test Providers]] supports it, SpecFlow generates row based tests from scenario outlines. Otherwise it generates a parameterized unit test logic method for a scenario outline and an individual unit test method for each example set. 

For better traceability, the generated unit test method names are derived from the scenario outline title and the first value of the examples (first column of the examples table). Therefore it is a good practice to choose a unique and descriptive parameter as the first column of the example set. As the Gherkin syntax does not enforce that all example columns have the matching placeholder in the scenario outline, you can even introduce an arbitrary column in the example sets for better test method name readability. 

SpecFlow performs the placeholder substitution as a separate phase before the step binding match would be applied. Therefore the implementation and the parameters of the step bindings are independent of whether they are executed through a direct scenario or a scenario outline. This leaves the option to specify further examples to the acceptance tests later without changing the step bindings.

Hint: In certain cases, when using the regular expression method of generating method names, SpecFlow is unable to generate the correct parameter signatures for unit test logic methods without a little help. Placing single quotation marks `'` around placeholders (eg. `'<placeholder>'`)improves SpecFlow's ability to parse the scenario outline and generate a more accurate regular expression and test method signature.

##Comments
You can add comment lines to the feature files at any place starting the line with the `#` sign. Be careful however, as comments in the specification are often signs of wrongly specified acceptance criteria. 

The comment lines are ignored by SpecFlow.