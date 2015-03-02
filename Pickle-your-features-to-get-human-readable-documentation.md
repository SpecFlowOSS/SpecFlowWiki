# Pickles - the fast route to human readable documentation
So you have a folder of [SpecFlow](http://www.specflow.org) features and but your end-users and stakeholders doesn't really like the text-only format. You want to create some dazzling documentation in no time. No problem - [Pickles](http://www.picklesdoc.com/) is here to help - and it's free too. 

Pickles has a lot of other ways and parameters - below is the simplest way to get started. We made a few assumptions on your environment though, see below.

# Four (or three really) simple steps to dazzling documentation
1. Install the Pickles Console NuGet package: ``` Install-Package Pickles.CommandLine ``` in the [Package Manager Console](https://docs.nuget.org/consume/package-manager-console) for example

2. Open a [command prompt at your solution root](http://www.hanselman.com/blog/QuakeModeConsoleForVisualStudioOpenACommandPromptWithAHotkey.aspx)

3. Enter this command: ``` .\packages\Pickles.CommandLine.1.0.0\tools\pickles.exe --feature-directory=.\Specs\features --output-directory=.\documentation --link-results-file=.\Specs\bin\Debug\TestResult.xml ```

4. Type ``` documentation/index.html ``` to view the generated documentation.

You are done!

There are loads of more configuration parameters and options that you can read about in the [documentation](http://docs.picklesdoc.com/en/latest/)

# Assumptions
In the examples above we made some assumptions about your environment:

* Firstly, for this we expect that your solution directory looks something like this:
	* solution.root
		* Specs - class library for SpecFlow specifications
			* features - the directory with your .feature-files in it
			* bin
				* Debug
					* TestResult.xml - [test result file](http://docs.picklesdoc.com/en/latest/ArgumentsTestResultsFile/) for NUnit.

* We expect that all your .feature files is found in the features-folder and subfolders.

* To generate the TestResult.xml file you can use [NUnit’s console-runner](http://www.nunit.org/index.php?p=nunit-console&r=2.6.4) or run the tests via the NUnit GUI

* We also assumed that you are using [NUnit](http://www.nunit.org/) as your test framework. If not check change the [Test Results Format](http://docs.picklesdoc.com/en/latest/ArgumentsTestResultsFormat/) parameter.

# Extra points
If you want to show off you can try this as next steps.

## Another format
Try adding ```--documentation-format=Word ``` at the end of your command, to produce a Word-document. Or to ```dhtml``` to generate a snazzier site with search capabilities. Read about all the [documentation formats here](http://docs.picklesdoc.com/en/latest/ArgumentsDocumentationFormat/).

## Do it again
This only produced a one-off generation. If you want to you can tweak the command to your content and then copy it into a .bat-file so that you can run it over and over.

```bat
.\packages\Pickles.CommandLine.1.0.0\tools\pickles.exe^
	--feature-directory=.\DemoPickles\features^
	--output-directory=.\documentation^
	--link-results-file=.\DemoPickles\bin\Debug\TestResult.xml
	--documentation-format=dhtml
```

## Check the right stuff in
Store the .bat-file mentioned above in source control.

*Don’t* store the documentation in source control, but rather generate it as needed, so that it’s always fresh and synchronized with the .feature-files. The .feature-files is the master - the generated documentation is just a view of those files.

## Automate the documentation generation
If you have an automated build or continuous integration mechanism see how you can trigger the documentation generation as part of that. Here is how to do it with [Team City](http://docs.picklesdoc.com/en/latest/HowToGeneratePicklesDocOnTeamCity/)
