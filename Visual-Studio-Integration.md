**THIS PAGE IS A WORK IN PROGRESS**

The SpecFlow Visual Studio integration provides a number of features to make using SpecFlow easier with Visual Studio.

You can install the integration from [[Visual Studio Gallery|http://go.specflow.org/vsgallery]] or from the online search in Visual Studio under **Tools | Extensions and Updates** (search for "SpecFlow").

The integration provides the following features:

* Editor
  * Gherkin (feature file) editor with syntax coloring
  * Intellisense (auto-completion) for keywords and steps
  * Outlining (folding) sections of the feature file
  * Highlight unbound steps and step parameters in the editor
  * Comment/uncomment feature file lines
  * Automatic Gherkin table formatting
* Navigation
  * Navigation from scenarios to step definitions: _Go To Step Definition_ (Alt+Ctrl+Shift+S)
  * Navigation from step definitions to step usages: _Go To SpecFlow Step Definition Usages_ (Alt+Ctrl+Shift+S) 
  * Detect bindings from the SpecFlow project, from project references and from assembly references
  * Cached step analysis for faster solution startup
* Execution
  * Scenario execution from context menu: _Run SpecFlow Scenarios_, _Debug SpecFlow Scenarios_
  * Debugging
* Other
  * Generate step definition skeletons from feature files: _Generate Step Definitions_
  * Re-generate feature files (from project node context menu and automatically on configuration change)
  * Configurable options
  * Support for ReSharper command shortcuts (when ReSharper is installed): commenting, navigation, test execution

##Generic Test Runner Support (VS 2013 and Higher)

From Visual Studio 2013 on, you can execute tests using the Visual Studio test runner infrastructure with the SpecFlow IDE. The following test runners are supported: Visual Studio, ReSharper and SpecRun. You can execute SpecFlow scenarios on all supported unit testing platforms (e.g. NUnit, xUnit, MS-Test), and jump from the test explorer directly to the related feature files.

### Visual Studio Test Window Support

The Visual Studio integration supports executing SpecFlow scenarios from the Visual Studio Test Explorer. The basic features work with all unit test providers, although you may need to install additional Visual Studio connectors, depending on the unit test framework. Full integration is provided for [[SpecRun|http://www.specrun.com]], meaning you can run and debug your scenarios as first class citizens:

* Run or debug individual scenarios or scenario outline examples from the feature file editor (choose "Run/Debug SpecFlow Scenarios" from the context menu)
* Scenarios are displayed in the Test Explorer with the scenario title
* Functions in the Test Explorer: 
  * Group scenarios by tags (choose "Traits" grouping) and features (choose "Class")
  * Filter scenarios by various criteria
  * Run/debug selected or all scenarios
  * Jump to the scenario in the feature file
  * View test execution results
* Specify the processor architecture (x86/x64), .NET platform and many other details for the test execution, including special config file transformations used by your tests.

**OLD: Some of this features are described in more detail below.**

## Navigating between Bindings to Steps 
**OLD: Navigation from step definitions to step usages (Alt+Ctrl+Shift+S)**

You can navigate between step definition methods in your bindings and the associated steps in your Gherkin feature files. 

###Navigating from a step definition method to steps in Gherkin files
To navigate from a step definition method to the matching step(s) in your Gherkin feature file(s):  

1. Place your cursor in a step definition method. 
1. Right-click and select "Go To SpecFlow Step Definition Usages" from the context menu, or simply press Alt+Ctrl+Shift+S (configurable). 
1. If only one match exists, the feature file is opened. If more than one matching step is defined in your feature files **NOT TESTED**, select the corresponding feature file from the list to switch to it.

###Navigating from Gherkin step to a binding
To navigate from a step in a Gherkin feature file to the corresponding step definition method: 

1. Place your curosr in the step in your feature file.
1. Right-click and select "Go To Step Definition" from the context menu, or use the Alt+Ctrl+Shift+S.
1. The file containing the binding is opened at the appropriate step definition method.

##Generating Skeleton Step Definitions from Feature Files (with custom templates)

Step definition method declarations (aka _step definition skeletons_) can be generated automatically in Visual Studio. To do so:
1. Open your feature file.
1. Select "Generate Step Definitions" from the context menu of the feature file. 
1. A dialog is displayed with a list of the steps in your feature file. Use the check boxes to determine which steps you want to generate skeleton code for.
1. Enter a name for your class in the **Class name** field.
1. Choose your desired [[step definition style]] (which include regex-less formats). Click on **Preview** to preview the output.
1. Either  
  * Click on **Generate** to add a new .cs file with your class to your project. This file will contain the skeleton step definitions for your selected steps.  
  * Click on **Copy methods to clipboard** to copy the generated skeleton code to the clipboard. You can then paste it to the file of your choosing.

The most common parameter usage patterns (quotes, apostrophes, numbers) are detected automatically. SpecFlow generates methods and the regular expressions using these parameters. 

For more information on the available options and custom templates, refer to the [[Step Definition Styles]] page.

## Highlighting Unbound steps and Parameters

Unbound steps and parameters in feature files are highlighted when editing the file in Visual Studio. The following syntax highlighting is used by default:
* Purple: unbound steps
* Black: bound steps
* Grey italics: parameters in bound steps

You can customise these colours in Visual Studio's settings (**Tools | Options | Environment | Fonts and Colors**). The names of the corresponding **Display items** in the list begin with "Gherkin"

## Intellisense (auto-completion) for Keywords and Steps
IntelliSense makes SpecFlow easy to use when integrated with Visual Studio, providing quick access to the available steps definitions. Intellisense uses find-as-you-type to restrict the list of suggested entries. Note that all the steps in all "*.feature" files are displayed, filtered by type (Given, When, Then).

_Figure 1: Specflow Integrated with Visual Studio and IntelliSense (click the image to see the full size)_
[![Specflow Integrated with Visual Studio and IntelliSense](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/IntilliSense.png) ](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/IntilliSense.png)


As you can see in Figure 1, the IntelliSense (red rectangle) is displayed in the **Given** step, and suggests the two existing Given steps in "GetProducts.feature" and "AddProducts.feature". Because step definition methods have been defined for these steps, the entry in the list contains "-->" to indicate that the step has been bound.

## Outlining (folding) sections of the feature file
The **Edit | Outlining** menu options work well with Specflow feature files, as do most of the items in **Edit** menu.

_Figure 2: VS2010 Edit menu (click the image to see the full size)_
[![VS2010 Edit menu](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/Outlining.png)](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/Outlining.png)

Tables in SpecFlow are also expanded and formatted automatically as you enter column names and values (see Figure 3). 

_Figure 3: Formatted table (click the image to see the full size)_
[![Formatted table](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/FormattedTable.png)](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/FormattedTable.png)


**THIS WAS ALREADY COVERED ABOVE **
## Navigation from scenarios to step definitions (Alt+Ctrl+Shift+S)
Another sweet feature is the right-click "Goto Definition" of steps in *.feature file and it will automatically brings you to the C# code steps definition you have (Figure 4). And if the steps definition does not exists it show a message box and ask to copy to clipboard the template steps definition (Figure 5). One thing I notice if the the steps definition is in the partial class and sub-group (like the form1.designer.cs is subgroup of form.aspx) "Goto Definition" does not work


_Figure 4: Goto Definition (click the image to see the full size)_
[![Goto Definition](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/GotoDefinition.png)](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/GotoDefinition.png)


_Figure 5: Not existing steps definition (click the image to see the full size)_
[![Not existing steps definition](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/NotExistingDefinition.png)](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/NotExistingDefinition.png)



