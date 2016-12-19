**THIS PAGE IS A WORK IN PROGRESS**

The Visual Studio integration includes a number of features that make it easier to edit Gherkin files and navigate to and from bindings in Visual Studio. You can also generate skeleton code including step definition methods from feature files. The Visual Studio integration also allows you to execute tests from Visual Studio's Test Explorer.

You can install the integration from [[Visual Studio Gallery|http://go.specflow.org/vsgallery]] or from the online search in Visual Studio under **Tools | Extensions and Updates** (search for "SpecFlow"). Detailed instructions can be found [[here|Install-IDE-Integration]].

The integration provides the following features:

* [[Editor|Visual-Studio-Integration-Editing-Features#editing]]
  * [[Gherkin syntax highlighting|Visual-Studio-Integration-Editing-Features#gherkin-syntax-highlighting]] in feature files, highlight unbound steps and parameters
  * [[Intellisense|Visual-Studio-Integration-Editing-Features#intellisense-auto-completion-for-keywords-and-steps]] (auto-completion) for keywords and steps
  * [[Outlining|Visual-Studio-Integration-Editing-Features#outlining-and-comments-in-feature-files]] (folding) sections of the feature file
  * [[Comment/uncomment|Visual-Studio-Integration-Editing-Features#outlining-and-comments-in-feature-files]] feature file lines
  * Automatic Gherkin [[table formatting|Visual-Studio-Integration-Editing-Features#table-formatting]]
* [[Navigation|Visual-Studio-Integration-Navigation-Features#navigation]]
  * Navigate from [[steps in scenarios to binding methods and vice versa|Visual-Studio-Integration-Navigation-Features#navigating-between-bindings-and-steps]]
  * Detect bindings from the SpecFlow project, from project references and from assembly references
  * Cached step analysis for faster solution startup
* Execution
  * Execute scenarios from the context menu: **Run SpecFlow Scenarios**, **Debug SpecFlow Scenarios**
  * Debugging
* Generic Test Runner Support (VS 2013 and Higher)
  * You can execute tests using the following test runners: Visual Studio, ReSharper and SpecRun. You can execute SpecFlow scenarios on all supported unit testing platforms (e.g. NUnit, xUnit, MSTest).
* [[Visual Studio Test Explorer Support]]  
  * Run/debug from feature file
  * Scenario title displayed in Test Explorer
  * Full access to Test Explorer functions
* Other
  * [[Generate skeleton step definition methods|Generating-Skeleton-Code]] from feature files
  * Re-generate feature files (from project node context menu and automatically on configuration change)
  * Configurable options
  * Support for ReSharper command shortcuts (when ReSharper is installed): commenting, navigation, test execution

