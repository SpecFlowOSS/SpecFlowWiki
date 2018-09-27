_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/FeatureContext]]. We use the GitHub wiki for authoring the documentation pages._

SpecFlow provides access to the current test context using both `FeatureContext` and the more commonly used [[ScenarioContext]]. `FeatureContext` persists for the duration of the execution of an entire feature, whereas `ScenarioContext` only persists for the duration of a scenario.

## FeatureContext.Current

`FeatureContext.Current` accesses a Dictionary, but otherwise works the same way as [[ScenarioContext.Current]].


## FeatureContext.FeatureInfo

`FeatureInfo` provides more information than `ScenarioInfo`, but it works the same:

In the .feature file:

        Scenario: Showing information of the feature
	  When I execute any scenario in the feature
	  Then the FeatureInfo contains the following information
		| Field          | Value                               |
		| Tags           | showUpInScenarioInfo, andThisToo    |
		| Title          | FeatureContext features             |
		| TargetLanguage | CSharp                              |
		| Language       | en-US                               |
		| Description    | In order to                         |

and in the step definition:

        private class FeatureInformation
        {
            public string Title { get; set; }
            public GenerationTargetLanguage TargetLanguage { get; set; }
            public string Description { get; set; }
            public string Language { get; set; }
            public string[] Tags { get; set; }
        }

        [When(@"I execute any scenario in the feature")]
        public void ExecuteAnyScenario() { }

        [Then(@"the FeatureInfo contains the following information")]
        public void FeatureInfoContainsInterestingInformation(Table table)
        {
            // Create our small DTO for the info from the step
            var fromStep =  table.CreateInstance<FeatureInformation>();
            fromStep.Tags = table.Rows[0]["Value"].Split(',');

            var fi = FeatureContext.Current.FeatureInfo;
            
            // Assertions
            fi.Title.Should().Equal(fromStep.Title);
            fi.GenerationTargetLanguage.Should().Equal(fromStep.TargetLanguage);
            fi.Description.Should().StartWith(fromStep.Description);
            fi.Language.IetfLanguageTag.Should().Equal(fromStep.Language);
            for (var i = 0; i < fi.Tags.Length - 1; i++)
            {
                fi.Tags[i].Should().Equal(fromStep.Tags[i]);
            }
        }


`FeatureContext` exposes a Binding Culture property that simply points to the culture the feature is written in (en-US in our example).