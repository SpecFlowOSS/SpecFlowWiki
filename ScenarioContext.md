_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/ScenarioContext]]. We use the GitHub wiki for authoring the documentation pages._

Most of us have at least seen the ScenarioContext from the the code that SpecFlow generates when a missing step definition is found: ScenarioContext.Current.Pending();

But there is some other interesting stuff you can do with and get from that object. I’ve tried to write scenarios that show that off. You can find the code here.

## ScenarioContext.Pending

Well – this method is known to most of us, as I said. This is default behavior for a missing step definition, but you can also use it directly if (why?) you want to. Like this:

in the .feature:

        Scenario: Pending step
	    When I set the ScenarioContext.Current to pending
	    Then this step will not even be executed

and the step definition:

        [When("I set the ScenarioContext.Current to pending")]
        public void WhenIHaveAPendingStep()
        {
            ScenarioContext.Current.Pending();
        }

        [Then("this step will not even be executed")]
        public void ThisStepWillNotBeExecuted()
        {
            throw new Exception("See!? This wasn't even thrown");
        }


##ScenarioContext.Current

This is a very useful feature of the [[ScenarioContext.Current]] that helps you to store values in a Dictionary between the steps. This helps you to organize your step definitions better that if you would use private variables in the step definition class.

There are some type safe extension methods that helps you to get values in and out of the dictionary in a safer way. To get that you need to include the namespace TechTalk.SpecFlow.Assist, since they are extension methods on the [[ScenarioContext.Current]].

##ScenarioContext.ScenarioInfo

You can also get hold of some information about the scenario you’re executing right now. For example the title and the tags of it:

In the .feature file:

        @showUpInScenarioInfo @andThisToo
        Scenario: Showing information of the scenario
	  When I execute any scenario
	  Then the ScenarioInfo contains the following information
		| Field | Value                               |
		| Tags  | showUpInScenarioInfo, andThisToo    |
		| Title | Showing information of the scenario |

and in the step definition:

        private class ScenarioInformation
        {
            public string Title { get; set; }
            public string[] Tags { get; set; }
        }

        [When(@"I execute any scenario")]
        public void ExecuteAnyScenario(){}

        [Then(@"the ScenarioInfo contains the following information")]
        public void ScenarioInfoContainsInterestingInformation(Table table)
        {
            // Create our small DTO for the info from the step
            var fromStep = table.CreateInstance<ScenarioInformation>();
            fromStep.Tags =  table.Rows[0]["Value"].Split(',');

            // Short-hand to the scenarioInfo
            var si = ScenarioContext.Current.ScenarioInfo;

            // Assertions
            si.Title.Should().Equal(fromStep.Title);
            for (var i = 0; i < si.Tags.Length -1; i++)
            {
                si.Tags[i].Should().Equal(fromStep.Tags[i]);
            }
        }

More interesting maybe is the ability to check if an error has occurred. That’s done with the ScenarioContext.Current.TestError property, which simply is the exception that has occurred.

You can use that to do some interesting “error handling” as I told you above. Here is an un-interesting version:

in the .feature file:

         #This is not so easy to write a scenario for but I've created an AfterScenario-hook
         @showingErrorHandling 
         Scenario: Display error information in AfterScenario
	    When an error occurs in a step

and the step definition:

        [When("an error occurs in a step")]
        public void AnErrorOccurs()
        {
            "not correct".Should().Equal("correct");
        }

        [AfterScenario("showingErrorHandling")]
        public void AfterScenarioHook()
        {
            if(ScenarioContext.Current.TestError != null)
            {
                var error = ScenarioContext.Current.TestError;
                Console.WriteLine("An error ocurred:" + error.Message);
                Console.WriteLine("It was of type:" + error.GetType().Name);
            }
        }

This is another example, that might be more useful:


       [AfterScenario]
       public void AfterScenario()
        {
            if(ScenarioContext.Current.TestError != null)
            {
                WebBrowser.Driver.CaptureScreenShot(ScenarioContext.Current.ScenarioInfo.Title);
            }
        }

Here I am using MvcContrib to capture the screen of the failing test, and naming the screen shot after the title of the Scenario. So by combining the use of hooks and the knowledge of ScenarioContext when can do some interesting stuff, don’t you think?


##ScenarioContext.Current.CurrentScenarioBlock

You can also get hold of the “type” of step your on (Given, When or Then) which is pretty cool and, for example, can be used to execute additional setup/cleanup code right before or after Given, When or Then block.

in the .feature file:

        Scenario: Show the type of step we're currently on
	     Given I have a Given step
		  And I have another Given step
	     When I have a When step
	     Then I have a Then step

and the step definition:

        [Given("I have a (.*) step")]
        [Given("I have another (.*) step")]
        [When("I have a (.*) step")]
        [Then("I have a (.*) step")]
        public void ReportStepTypeName(string expectedStepType)
        {
            var stepType = ScenarioContext.Current.CurrentScenarioBlock.ToString();
            stepType.Should().Equal(expectedStepType);
        }

##ScenarioContext.Current.StepContext

Sometimes you need to access the currently executed step, e.g. to improve tracing. Use the `ScenarioContext.Current.StepContext` property for this purpose.

##Injecting ScenarioContext

Using the static `ScenarioContext.Current` accessor may result in test automation code that is hard to follow, and does not work with [[parallel execution]]. In such cases, you can let SpecFlow inject the current scenario context into your binding class using the [[context injection]] mechanism by declaring a `ScenarioContext` parameter in the constructor, e.g.:

```c#
public class MyBindingClass
{
  private ScenarioContext scenarioContext;

  public MyBindingClass(ScenarioContext scenarioContext)
  {
    this.scenarioContext = scenarioContext;
  }

  [When("I say hello to ScenarioContext")]
  public void WhenISayHello()
  {
    scenarioContext["say"] = "hello";
  }
}
```
