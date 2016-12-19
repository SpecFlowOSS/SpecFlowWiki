The Visual Studio integration includes the following features to make it easier to edit feature files and identify which steps have already been bound.

# Gherkin Syntax Highlighting
Various default styles have been defined for the Gherkin syntax. You can customise these colours in Visual Studio's settings (**Tools | Options | Environment | Fonts and Colors**). The names of the corresponding **Display items** in the list begin with "Gherkin".

In addition to highlighting keywords, comments, tags etc., unbound steps and parameters in feature files are highlighted when editing the file in Visual Studio. The following syntax highlighting is used by default:
* Purple: unbound steps
* Black: bound steps
* Grey italics: parameters in bound steps

You can thus tell immediately which steps in a feature file have been bound.

# Intellisense (auto-completion) for Keywords and Steps
IntelliSense makes SpecFlow easy to use when integrated with Visual Studio. Intellisense uses find-as-you-type to restrict the list of suggested entries.

##Gherkin Files
Intellisense is available in feature files for the following:
* Gherkin keywords (e.g. `Scenario`, `Given` etc.)
* Existing steps are listed after a `Given`, `When` or `Then` statement, providing quick access to your current steps definitions. Bound steps are indicated with "-->". Note that **all the steps in all "*.feature" files are displayed that match the current type** (Given, When, Then):  
[![Specflow Integrated with Visual Studio and IntelliSense](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/IntilliSense.png) ](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/IntilliSense.png)  
_(click image for full size)_  
The IntelliSense suggestions (red rectangle) for the **Given** step include the two existing Given steps in "GetProducts.feature" and "AddProducts.feature". Step definition methods have been defined for these steps; the entries in the list contain "-->" to indicate that the step has been bound.

##Code Files
Intellisense is also available for the Gherkin keywords in your code files.

# Outlining and Comments in Feature Files
Most of the items in the **Edit** menu work well with SpecFlow feature files, for example:

* You can comment and uncomment selected lines ('#' character) with the default shortcut for comments (Ctrl+K Ctrl+C/Ctrl+K Ctrl+U) or from the menu
* You can use the options in the **Edit | Outlining** menu to expand and contract sections of your feature files  
[![VS2010 Edit menu](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/Outlining.png)](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/Outlining.png)  
_(click image for full size)_

**NEED BETTER SCREENSHOT, maybe showing contracted sections**

#Table Formatting
Tables in SpecFlow are also expanded and formatted automatically as you enter column names and values (see Figure 3):

[![Formatted table](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/FormattedTable.png)](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/FormattedTable.png)  
_(click image for full size)_