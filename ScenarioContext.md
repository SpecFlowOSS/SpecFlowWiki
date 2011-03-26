Most of us has at least seen the ScenarioContext from the the code that SpecFlow generates when a missing step definition is found: ScenarioContext.Current.Pending();

But there are some other interesting stuff you can do with and get from that object. I’ve tried to write scenarios that show that off. You can find the code here.

## ScenarioContext.Pending

Well – this method is known to most of us, as I said. This is default behavior for a missing step definition, but you can also use it directly if (why?) you want to. Like this:


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

This is a very useful feature of the ScenarioContext that helps you to store values in a Dictionary between the steps. This helps you to organize your step definitions better that if you would use private variables in the step definition class.

There are some type safe extension methods that helps you to get values in and out of the dictionary in a safer way. To get that you need to include the namespace TechTalk.SpecFlow.Assist, since they are extension methods on the ScenarioContext.

[[https://github.com/techtalk/SpecFlow/wiki/ScenarioContext.Current]]

##ScenarioContext.ScenarioInfo

You can also get hold of some information about the scenario you’re executing right now. For example the title and the tags of it:


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
``        public void AfterScenario()
        {
            if(ScenarioContext.Current.TestError != null)
            {
                WebBrowser.Driver.CaptureScreenShot(ScenarioContext.Current.ScenarioInfo.Title);
            }
        }

Here I am using MvcContrib to capture the screen of the failing test, and naming the screen shot after the title of the Scenario. So by combining the use of hooks and the knowledge of ScenarioContext when can do some interesting stuff, don’t you think?


##ScenarioContext.Current.CurrentScenarioBlock

You can also get hold of the “type” of step your on (Given, When or Then) which is pretty cool, but I cannot see and immediate use of it.
`

        [Given("I have a (.*) step")]
        [Given("I have another (.*) step")]
        [When("I have a (.*) step")]
        [Then("I have a (.*) step")]
        public void ReportStepTypeName(string expectedStepType)
        {
            var stepType = ScenarioContext.Current.CurrentScenarioBlock.ToString();
            stepType.Should().Equal(expectedStepType);
        }
`

