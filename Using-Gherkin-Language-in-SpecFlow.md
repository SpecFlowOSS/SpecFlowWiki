_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Using-Gherkin-Language-in-SpecFlow]]. We use the GitHub wiki for authoring the documentation pages._

The feature files used by SpecFlow to store acceptance criteria for features (use cases, user stories) in your application are defined using the Gherkin syntax. The Gherkin language defines the structure and a basic syntax for describing tests. The Gherkin format was introduced by [[Cucumber|http://cukes.info/]] and is also used by other tools. 

The Gherkin language is maintained as a separate project on GitHub: [[https://github.com/cucumber/gherkin]]. A detailed description of the language can be found at [[https://github.com/cucumber/cucumber/wiki/Gherkin]].

This page focuses on how SpecFlow handles the different Gherkin language elements. 

##Features
The feature element provides a header for the feature file. The feature element includes the name and a high level description of corresponding feature in your application. For more details, see [[https://github.com/cucumber/cucumber/wiki/Feature-Introduction]].

SpecFlow generates a unit test class for the feature element, with the class name derived from the name of the feature.

##Scenarios
A feature file may contain multiple scenarios used to describe the feature's acceptance tests. Scenarios have a name and can consist of multiple scenario steps. For more details, see [[https://github.com/cucumber/cucumber/wiki/Feature-Introduction]].

SpecFlow generates a unit test method for each scenario, with the method name derived from the name of the scenario.

##Scenario Steps
Scenarios can contain multiple scenario steps. There are three types of steps that define either the preconditions, actions or verification steps that make up the acceptance test (these three types are also referred to as arrange, act and assert). The different types of steps begin with either the `Given`, `When` or `Then` keywords respectively (in English feature files), and subsequent steps of the same type can be linked using the `And` and `But` keywords. There may be other alternative keywords for specifying steps.

The Gherkin syntax allows any combination of these three types of steps, but a scenario usually has distinct blocks of `Given`, `When` and `Then` statements.

Scenario steps are defined using text and can have additional table or multi-line text arguments.

For more details, see [[https://github.com/cucumber/cucumber/wiki/Given-When-Then]].

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

To comment blocks you can use triple quotes (") to start and to finish the block comment.

"""

Given I want to comment this line

Given I want to comment this line

Given I want to comment this line

"""