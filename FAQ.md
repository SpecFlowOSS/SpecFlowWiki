<h1 id="General">General</h1>
##What is SpecFlow?

SpecFlow allows .NET development teams to define, manage and execute automated acceptance tests as business readable specifications. It is based on [[Gherkin|https://github.com/cucumber/gherkin/wiki]] and part of the [[Cucumber|https://cucumber.io/]] eco system.  
 
SpecFlow aims to bridge the communication gap between domain experts and developers. Acceptance tests in SpecFlow follow the BDD paradigm of defining specifications with examples, so that they are also understandable to business users. Acceptance tests can then be tested automatically as needed, while their specification serves as a living documentation of the system. 

SpecFlow integrates with Visual Studio, but can be also used from the command line (e.g. on a build server). 

[[SpecFlow+|http://www.specflow.org/plus/]] adds additional functionality to SpecFlow, such as a stand-alone IDE for Gherkin specifications, advanced reporting and much more.

##How do I install SpecFlow?
To install SpecFlow and SpecFlow+, you first need to [[install the SpecFlow Visual Studio integration|Install-IDE-Integration]]. Once you have done this, you can then add SpecFlow to each of your projects using NuGet.  For more details, see the [[Getting Started|http://www.specflow.org/plus/runner/getting-started/]] article.

##What is the difference between SpecFlow and SpecFlow+?
SpecFlow is open source and free of charge. It covers all your basic needs for managing and testing specifications by example. 

SpecFlow+ is a series of extensions that introduce additional features, such as a stand-alone IDE for Gherkin specifications, advanced reporting, specify and execute Gherkin in Excel, execute tests in multiple threads, and define complex filters to determine which tests to run.  

SpecFlow+ requires a license to be [[purchased|https://www.swreg.org/cgi-bin/s.cgi?s=138662&p=138662-1&v=0&d=0&q=1&t=remove%20extended%20download%20service%20from%20baske]]. For more information on licensing, see the [[Licensing section in the SpecFlow+ FAQ|http://www.specflow.org/plus/documentation/FAQ/]] and [[here|http://www.specflow.org/plus/licensing/]].

For an overview of the differences between SpecFlow and SpecFlow+, see the [[comparison of features|http://www.specflow.org/plus/]].

<h1 id="Support">Support</h1>
##Where can I find training material online?
We’ve listed the most important resources [[here|http://www.specflow.org/resources/]]. Many of them are free or inexpensive.

We also run regular training classes, which are listed [[here|http://www.specflow.org/training/]]

##I have a feature request; how can I submit it?
We currently have a long list of features awaiting implementation and are therefore limited in our capacity to implement feature requests. However, as SpecFlow is open source, you can implement new features yourself (more information available [[here|https://github.com/techtalk/SpecFlow/wiki/Contributing]]).

If you require a specific feature but are unable to develop it yourself, you can also sponsor the feature for the benefit of the community or pay outright for development services provided by [[TechTalk|http://www.techtalk.at]].

##I have found an issue with SpecFlow. How can I get support? 
SpecFlow is an open source project, and you can get free support from the SpecFlow community by submitting an issue on [[GitHub|https://github.com/techtalk/SpecFlow/issues]]. When submitting an issue, please provide as much information and context as possible, and ideally a code sample that allows the issue to be reproduced. The easier you make it for contributors to diagnose and fix your issue, the more likely you are to see results. 

Once you have submitted an issue relating to a bug, a contributor needs to take on the issue and provide a pull request containing a fix. Depending on the nature of your issue, how well it is described and how easy it is to reproduce, a fix may be delivered quickly or take a long time. 

If time is of the essence, TechTalk can offer paid support and deliver fixes for a fee invoiced either by effort or per incident. Details on the associated costs are available [[here|http://www.specflow.org/professional-support/]].

<h1 id="Support">Development</h1>
##How can I contribute to SpecFlow's development?
Details on how you can contribute to SpecFlow's development can be found [[here|https://github.com/techtalk/SpecFlow/wiki/Contributing]].

##Who are the developers behind SpecFlow?
SpecFlow was originally created by Gáspár Nagy and used internally by [[TechTalk|http://www.techtalk.at]] in various software development projects. Since then developers from around the world have contributed to the open source project; an overview can be found [[here|https://github.com/techtalk/SpecFlow/graphs/contributors]].

##Can I use the SpecFlow name for my own projects based on SpecFlow? 
We are always happy to see projects that extend SpecFlow’s feature set, and SpecFlow is open source to specifically encourage such contributions from the community. We have however reserved the rights to the name “SpecFlow” as well as the official SpecFlow logo. We need to retain control over this aspect of the project, as we share responsibility for supporting and maintaining SpecFlow, along with all other contributors in the community. 

When naming your project, one of our primary concerns is therefore that the name of your project avoids any confusion concerning project ownership and avoids creating the impression that your project is officially supported by us. Of course this is benefits you as well - we surely both want to ensure that feedback concerning your project is directed to the right place, and prevent users from submitting support issues to the SpecFlow community that concern third-party projects.

If you want to use “SpecFlow” in the name of your project, we would suggest naming your project something along the lines of “XXX for SpecFlow”. Please avoid names that start with “SpecFlow” as this suggests an official affiliation with the SpecFlow project (similar to SpecFlow, SpecFlow+, SpecFlow+ Runner etc.). 

If you are unsure as to whether your preferred project name meets these guidelines, you can always contact us to make sure. We are always happy to hear about new projects that benefit the SpecFlow community, and if your project is well received and proves popular, we may approach you about the possibility of integrating your project within the official SpecFlow project.

<h1 id="Features">Features</h1>

##Does SpecFlow support coded UI tests?
Coded UI tests include special coded UI attributes that can only be interpreted by MS Test. If you are using coded UI tests, you can only execute them using the MS Test test runner. For more details on getting coded UI working with SpecFlow, see [[this blog post|http://blog.majcica.com/2015/05/07/getting-started-with-specflow-and-codedui/]] (thanks to Mario Majčica).

<h1 id="Troubleshooting>Troubleshooting</h1>

## After upgrading to SpecFlow 2 from 1.9, I get the message "Trace listener failed. -> The ScenarioContext.Current static accessor cannot be used in multi-threaded execution. Try injecting the scenario context to the binding class. See http://go.specflow.org/doc-multithreaded for details."

Make sure you have regenerated the `.feature.cs` files after upgrading. If you do not do this, you will receive this exception when accessing ScenarioContext.Current.

To regenerate these files:  
* Open a feature file in your solution. If you see a popup informing you that the feature files were generated with an earlier version of SpecFlow, click on **Yes** to regenerate these files. Depending on the size of your project, this may take a while.
* If you are using an earlier version of Visual Studio, you need to force the feature files to be regenerated. Right-click on your project, and select **Regenerate Feature Files** from the menu.
