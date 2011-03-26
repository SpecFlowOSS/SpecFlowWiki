There is a FeatureContext as well as the more commonly used [[ScenarioContext]]. The difference of course is that the FeatureContext exists during the execution of the complete feature while the ScenarioContext only exists during a scenario.

##FeatureContext.Current

FeatureContext also have a Current property which holds a Dictionary. But I works in exactly the same way as the [[ScenarioContext.Current]] so I won’t go into details of it. It’s actually implemented with the same class SpecFlowContext so it IS the same behavior.


##FeatureContext.FeatureInfo

The FeatureInfo is a bit more elaborative than the ScenarioInfo, but it works in the same manner:

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
`

Also I should mention here that FeatureContext exposes a Binding Culture property that simply points to the culture the feature is written in (en-US in our example).