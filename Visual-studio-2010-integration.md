## Introduction
This page will discuss some features of **Specflow 1.6.1** that is integrated with Microsoft Visual Studio 2010. 
Features like

* Visual Studio Intellisense (auto-completion)
* Auto formatting
* Goto Definition
* Debugging
* Resharper, AgUnit and Silverlight

because providing cool editor for Visual Studio is one of the goal of Specflow developers.

## Visual Studio Intellisense (auto-completion)
IntelliSense is one of the feature that makes Specflow easy to use when integrated with Visual Studio. It provides a lists available steps definition and possible sample. It's an auto complete because as you type it suggests based  on the typed characters. It does not only displays the steps in the current file but for all "*.feature" files, filtered by what type of step (either Given, When or Then)

_Figure 1: Specflow Integrated with Visual Studio and IntelliSense (click the image to see the full size)_
[![Specflow Integrated with Visual Studio and IntelliSense](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/IntilliSense.png) ](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/IntilliSense.png)


As you can see from the Figure 1, the IntelliSense feature pop up (shown with Red Rectangle) in the **Given** step and it suggests existing (the first two from the IntelliSense pop up) steps from "GetProducts.feature" and "AddProducts.feature". The step has already C# code definition that is why it also specified in the pop-up with "**-->**" characters

## Auto formatting
VS2010 "Edit-->Outlining" menu item works well with Specflow feature file. Even most of the items on "Edit" menu.
The "table" in Specflow is also formatted in a nice way with as you type for the column names and values, it automatically expands (shown in figure 3). 

_Figure 2: VS2010 Edit menu (click the image to see the full size)_
[![VS2010 Edit menu](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/Outlining.png)](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/Outlining.png)


_Figure 3: Formatted table (click the image to see the full size)_
[![Formatted table](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/FormattedTable.png)](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/FormattedTable.png)

## Goto Definition
Another sweet feature is the right-click "Goto Definition" of steps in *.feature file and it will automatically brings you to the C# code steps definition you have (Figure 4). And if the steps definition does not exists it show a message box and ask to copy to clipboard the template steps definition (Figure 5). One thing I notice if the the steps definition is in the partial class and sub-group (like the form1.designer.cs is subgroup of form.aspx) "Goto Definition" does not work


_Figure 4: Goto Definition (click the image to see the full size)_
[![Goto Definition](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/GotoDefinition.png)](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/GotoDefinition.png)


_Figure 5: Not existing steps definition (click the image to see the full size)_
[![Not existing steps definition](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/NotExistingDefinition.png)](http://i734.photobucket.com/albums/ww347/rommelmanalo/Specflow/NotExistingDefinition.png)


## Debugging
TODO

## Resharper, AgUnit and Silverlight
TODO