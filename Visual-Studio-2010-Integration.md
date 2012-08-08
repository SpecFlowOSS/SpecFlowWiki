SpecFlow Visual Studio 2010 integration provides many useful features to make the usage of SpecFlow easier.

The Visual Studio 2010 support can be installed from [[Visual Studio Gallery|http://go.specflow.org/vsgallery]] or from the online search in Visual Studio / Tools / Extensions and Updates. (You have to search for "SpecFlow" :).

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

You can find detailed information about some of these features in below.

## Navigation from step definitions to step usages (Alt+Ctrl+Shift+S)

With this feature, you can track how your step definitions are used in the feature files. Just place your cursor into a step definition method and invoke "Go To SpecFlow Step Definition Usages" from the context menu or simply press Alt+Ctrl+Shift+S (configurable). You will be given a list of usages that you can use to jump to the feature files immediately.

If you are already in the feature file, you can use the Alt+Ctrl+Shift+S keyboard shortcut (or invoke "Go To Step Definition" from the context menu) to jump back to the code.

##Generate step definition skeletons from feature files (with custom templates)

The step definition method declarations (aka _step definition skeletons_) can be generated from Visual Studio. Select "Generate Step Definitions" from the context menu of the feature file and the appearing dialog will guide you how to create a new binding class with the step definitions for the selected unbound steps. The most common parameter usage patterns (quotes, apostrophes, numbers) are detected so SpecFlow generates the methods and the annotation with the these parameters. You can also choose from different [[step definition styles]], including the new regex-less formats.

Read more about the options and the custom templates in the [[Step Definition Styles]] page.

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

