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

Some of this features are described in more detail below.

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

## Highlight unbound steps and step parameters in the editor

Do you want to check the binding status of the steps in a scenario? Do you want to have better readable scenarios by highlighting the parameters? This is now possible with this new editor feature: the parameters of the bound steps will be highlighted and unbound steps will be displayed in purple. (You can configure the colors of course.)

## Intellisense (auto-completion) for keywords and steps
IntelliSense is one of the feature that makes Specflow easy to use when integrated with Visual Studio. It provides a lists available steps definition and possible sample. It's an auto complete because as you type it suggests based  on the typed characters. It does not only displays the steps in the current file but for all "*.feature" files, filtered by what type of step (either Given, When or Then)

_Figure 1: Specflow Integrated with Visual Studio and IntelliSense (click the image to see the full size)_
[![Specflow Integrated with Visual Studio and IntelliSense](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/IntilliSense.png) ](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/IntilliSense.png)


As you can see from the Figure 1, the IntelliSense feature pop up (shown with Red Rectangle) in the **Given** step and it suggests existing (the first two from the IntelliSense pop up) steps from "GetProducts.feature" and "AddProducts.feature". The step has already C# code definition that is why it also specified in the pop-up with "**-->**" characters

## Outlining (folding) sections of the feature file
VS2010 "Edit-->Outlining" menu item works well with Specflow feature file. Even most of the items on "Edit" menu.
The "table" in Specflow is also formatted in a nice way with as you type for the column names and values, it automatically expands (shown in figure 3). 

_Figure 2: VS2010 Edit menu (click the image to see the full size)_
[![VS2010 Edit menu](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/Outlining.png)](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/Outlining.png)


_Figure 3: Formatted table (click the image to see the full size)_
[![Formatted table](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/FormattedTable.png)](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/FormattedTable.png)

## Navigation from scenarios to step definitions (Alt+Ctrl+Shift+S)
Another sweet feature is the right-click "Goto Definition" of steps in *.feature file and it will automatically brings you to the C# code steps definition you have (Figure 4). And if the steps definition does not exists it show a message box and ask to copy to clipboard the template steps definition (Figure 5). One thing I notice if the the steps definition is in the partial class and sub-group (like the form1.designer.cs is subgroup of form.aspx) "Goto Definition" does not work


_Figure 4: Goto Definition (click the image to see the full size)_
[![Goto Definition](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/GotoDefinition.png)](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/GotoDefinition.png)


_Figure 5: Not existing steps definition (click the image to see the full size)_
[![Not existing steps definition](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/NotExistingDefinition.png)](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/NotExistingDefinition.png)



