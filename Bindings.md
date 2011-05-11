The [[Gherkin feature files|Using Gherkin Language in SpecFlow]] are more close to free-text than to code – they cannot be executed as they are. The automation that connects the specification to the application interface has to be developed first. 

This automation (called binding) is done in step-level. This means that instead of providing the binding for the entire scenario, the automation has to be done for each different step. The benefit of this model is, that the bound steps can be reused in other scenarios, so it is possible to construct further scenarios partly from existing steps with less (or no) automation effort. See [[Step Bindings]] for details.

SpecFlow allows three additional advanced binding techniques. 
1. The [[event bindings]] can be used to perform additional automation logic on specific events, like before the execution of a scenario.
2. The [[step argument transformations|Step Argument Conversion]] can be used to apply a conversion step for the arguments of the step bindings. The step argument transformation is a method that provides a conversion from text (specified by a regular expression) to an arbitrary .NET type. 
3. With [[scoped step bindings]], one can restrict the applicability of a step binding. The restriction can be defined as scope rules. Each scope rule can restrict for feature title, scenario title or tags. With scoped step bindings it is possible to provide different automation logic for the same step depending on where it was used. 

In many cases the different bindings have to exchange data during execution. See [[Sharing Data in Bindings]] for details about this.
