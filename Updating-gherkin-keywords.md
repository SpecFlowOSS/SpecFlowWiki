_Important:_ There is a new Gherkin parser in a preparation phase currently: [Gherkin3 GitHib repo](https://github.com/cucumber/gherkin3). The new parser will allow changing the keywords without creating a new release. 

The description below is valid for the old Gherkin parser used by SpecFlow 1.9.

The keywords that SpecFlow uses are defined by the Gherkin project [[https://github.com/cucumber/gherkin]]. Gherkin defines an established language that is used in a lot of tools. It is currently not the goal nor in the scope of the SpecFlow project
to define or change that language.

Please submit a change request for the Gherkin project and as soon as it is fixed in Gherkin, SpecFlow can upgrade to use that one. 

Once the change has been done in the Gherkin project the [[Updating the Gherkin Parser]] describes the merge process.