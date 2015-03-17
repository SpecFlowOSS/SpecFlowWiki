_Important:_ There is a new Gherkin parser in a preparation phase currently: [Gherkin3 GitHib repo](https://github.com/cucumber/gherkin3). The new parser will allow changing the keywords without creating a new release. 

The description below is valid for the old Gherkin parser used by SpecFlow 1.9.

Under the hood SpecFlow uses the parser of the [Gherkin project](https://github.com/aslakhellesoy/gherkin) for parsing feature files.

The Gherkin project publishes a .NET dll of the parser as part of their release process.

Some steps are necessary to import this dll into the SpecFlow project. This is the process:

0. compile SpecFlow
1. download gherkin-x.y.z.dll from [gherkin github](https://github.com/aslakhellesoy/gherkin/downloads) to lib\\gherkin
2. in a command prompt, go to: Installer\\ImportGherkinParser\\bin\\Debug
3. run import.cmd gherkin-x.y.z.dll
4. run all the SpecFlow tests
5. remove the old gherkin dll from lib\\gherkin
6. update changelog