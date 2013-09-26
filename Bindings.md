_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Bindings]]. We use the GitHub wiki for authoring the documentation pages._

The [[Gherkin feature files|Using Gherkin Language in SpecFlow]] are closer to free-text than to code – they cannot be executed as they are. The automation that connects the specification to the application interface has to be developed first. This automation is also called _binding_ in general. The binding classes and methods can be defined in the SpecFlow project or in [[external binding assemblies|
Use Bindings from External Assemblies]].

There are several kinds of bindings in SpecFlow. The most important one is the [[step definition|Step Definitions]] that automates the scenario at step-level. This means that instead of providing the automation for the entire scenario, this has to be done for each different step. The benefit of this model is that the step definitions can be reused in other scenarios, so it is possible to construct further scenarios partly from existing steps with less (or no) automation effort. See [[Step Definitions]] for details.

SpecFlow allows three additional advanced binding techniques. 

1. The [[hooks]] can be used to perform additional automation logic on specific events, like before the execution of a scenario.

2. The [[step argument transformations|Step Argument Conversions]] can be used to apply a conversion step for the arguments of the step definitions. The step argument transformation is a method that provides a conversion from text (specified by a regular expression) to an arbitrary .NET type. 

3. With [[scoped bindings]], one can restrict the applicability of a step definition or hook. The restriction can be defined as scope rules. Each scope rule can restrict for feature title, scenario title or tags. With scoped step bindings it is possible to provide different automation logic for the same step depending on where it was used. 

In many cases the different bindings have to exchange data during execution. See [[Sharing Data between Bindings]] for details about this.
