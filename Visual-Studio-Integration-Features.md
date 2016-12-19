The Visual Studio integration includes a number of features that make it easier to edit Gherkin files and navigate to and from bindings in Visual Studio. You can also generate skeleton code including step definition methods from feature files.

#Editing

## Gherkin Syntax Highlighting
Various default styles have been defined for the Gherkin syntax. You can customise these colours in Visual Studio's settings (**Tools | Options | Environment | Fonts and Colors**). The names of the corresponding **Display items** in the list begin with "Gherkin".

In addition to highlighting keywords, comments, tags etc., unbound steps and parameters in feature files are highlighted when editing the file in Visual Studio. The following syntax highlighting is used by default:
* Purple: unbound steps
* Black: bound steps
* Grey italics: parameters in bound steps

You can thus tell immediately which steps in a feature file have been bound.

## Intellisense (auto-completion) for Keywords and Steps
IntelliSense makes SpecFlow easy to use when integrated with Visual Studio. Intellisense uses find-as-you-type to restrict the list of suggested entries.

###Gherkin Files
Intellisense is available in feature files for the following:
* Gherkin keywords (e.g. `Scenario`, `Given` etc.)
* Existing steps are listed after a `Given`, `When` or `Then` statement, providing quick access to your current steps definitions. Bound steps are indicated with "-->". Note that **all the steps in all "*.feature" files are displayed that match the current type** (Given, When, Then):  
[![Specflow Integrated with Visual Studio and IntelliSense](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/IntilliSense.png) ](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/IntilliSense.png)  
_(click the image to see the full size)_  
The IntelliSense suggestions (red rectangle) for the **Given** step include the two existing Given steps in "GetProducts.feature" and "AddProducts.feature". Step definition methods have been defined for these steps; the entries in the list contain "-->" to indicate that the step has been bound.

###Code Files
Intellisense is also available for the Gherkin keywords in your code files.

## Outlining (folding) sections of the feature file
The **Edit | Outlining** menu options work well with Specflow feature files, as do most of the items in **Edit** menu.

_Figure 2: VS2010 Edit menu (click the image to see the full size)_
[![VS2010 Edit menu](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/Outlining.png)](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/Outlining.png)

**NEED BETTER SCREENSHOT, maybe showing contracted sections**

##Data Tables
Tables in SpecFlow are also expanded and formatted automatically as you enter column names and values (see Figure 3). 

_Figure 3: Formatted table (click the image to see the full size)_
[![Formatted table](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/FormattedTable.png)](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/FormattedTable.png)

#Navigating

## Navigating between Bindings and Steps 
You can navigate between the methods in your bindings and the associated steps in your Gherkin feature files. 

###Navigating from a Binding to Steps in Gherkin Files
To navigate from a step definition method to the matching step(s) in your Gherkin feature file(s):  

1. Place your cursor in a step definition method. 
1. Right-click and select "Go To SpecFlow Step Definition Usages" from the context menu, or simply press Alt+Ctrl+Shift+S (configurable). 
1. If only one match exists, the feature file is opened. If more than one matching step is defined in your feature files **NOT TESTED**, select the corresponding feature file from the list to switch to it.

###Navigating from a Gherkin Step to a Binding
To navigate from a step in a Gherkin feature file to the corresponding step definition method: 

1. Place your curosr in the step in your feature file.
1. Right-click and select "Go To Step Definition" from the context menu, or use the Alt+Ctrl+Shift+S.
1. The file containing the binding is opened at the appropriate step definition method.

#Skeleton Code Generation
##Generating Skeleton Bindings from Feature Files
Skeleton step definition methods can be generated automatically in Visual Studio. To do so:

1. Open your feature file.
1. Select "Generate Step Definitions" from the context menu of the feature file. 
1. A dialog is displayed with a list of the steps in your feature file. Use the check boxes to determine which steps you want to generate skeleton code for.
1. Enter a name for your class in the **Class name** field.
1. Choose your desired [[step definition style|step definition styles]] (including formats without regular expressions). Click on **Preview** to preview the output.
1. Either  
  * Click on **Generate** to add a new .cs file with your class to your project. This file will contain the skeleton step definitions for your selected steps.  
  * Click on **Copy methods to clipboard** to copy the generated skeleton code to the clipboard. You can then paste it to the file of your choosing. Use this method to extend your bindings if new steps have been added to a feature file that already contains bound steps.

The most common parameter usage patterns (quotes, apostrophes, numbers) are detected automatically. SpecFlow generates methods and the regular expressions using these parameters. 

For more information on the available options and custom templates, refer to the [[Step Definition Styles]] page.


**THIS WAS ALREADY COVERED ABOVE **
## Navigation from scenarios to step definitions (Alt+Ctrl+Shift+S)
Another sweet feature is the right-click "Goto Definition" of steps in *.feature file and it will automatically brings you to the C# code steps definition you have (Figure 4). And if the steps definition does not exists it show a message box and ask to copy to clipboard the template steps definition (Figure 5). One thing I notice if the the steps definition is in the partial class and sub-group (like the form1.designer.cs is subgroup of form.aspx) "Goto Definition" does not work


_Figure 4: Goto Definition (click the image to see the full size)_
[![Goto Definition](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/GotoDefinition.png)](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/GotoDefinition.png)


_Figure 5: Not existing steps definition (click the image to see the full size)_
[![Not existing steps definition](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/NotExistingDefinition.png)](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/NotExistingDefinition.png)



