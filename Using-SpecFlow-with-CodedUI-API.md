## Introduction

The Microsoft Coded UI API can be used to create automated tests in Visual Studio, but is not compatible directly with SpecFlow as each Test Class needs to have an attribute [CodedUITest], and SpecFlow doesn't generate this by default.

Big thanks to Thomy Kay for [pointing me in the right direction](http://groups.google.com/group/specflow/browse_thread/thread/e162fc98c1d7c119/0bf231a65195b375?lnk=gst&q=SpecFlow+with+VS2010+CodedUI+tests+#0bf231a65195b375).

## Solution

You need to ensure SpecFlow generates this attribute, and ensure that any SpecFlow hooks also ensure the CodedUI API is initialized.

### Getting SpecFlow to generate the [CodedUITest] attribute with VS2010 and MSTest

1. Create a new VS project to generate an assembly that contains the following class.
This will need to have the have a reference to the `TechTalk.SpecFlow.Generator.dll` in the SpecFlow directory. If you are using version 1.7 or higher you will also need to add a reference to `TechTalk.SpecFlow.Utils.dll`
2. Add the following class to your new VS project

**Specflow version 1.6**
```csharp
namespace My.SpecFlow
{
    using System.CodeDom;
    using TechTalk.SpecFlow.Generator.UnitTestProvider;

    public class MsTest2010CodedUiGeneratorProvider : MsTest2010GeneratorProvider
    {
        public override void SetTestFixture(System.CodeDom.CodeTypeDeclaration typeDeclaration, string title, string description)
        {
            base.SetTestFixture(typeDeclaration, title, description);
            foreach (CodeAttributeDeclaration customAttribute in typeDeclaration.CustomAttributes)
            {
                if (customAttribute.Name == "Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute")
                {
                    typeDeclaration.CustomAttributes.Remove(customAttribute);
                    break;
                }
            }

            typeDeclaration.CustomAttributes.Add(new CodeAttributeDeclaration(new CodeTypeReference("Microsoft.VisualStudio.TestTools.UITesting.CodedUITestAttribute")));
        }
    } 
}
```
**Specflow version 1.7**
```csharp
   using System.CodeDom;
using TechTalk.SpecFlow.Generator.UnitTestProvider;

namespace SpecflowCodedUIGenerator
{
    public class MsTest2010CodedUiGeneratorProvider : MsTest2010GeneratorProvider
    {
        public override void SetTestClass(TechTalk.SpecFlow.Generator.TestClassGenerationContext generationContext, string featureTitle, string featureDescription)
        {
            base.SetTestClass(generationContext, featureTitle, featureDescription);

            foreach (CodeAttributeDeclaration customAttribute in generationContext.TestClass.CustomAttributes)
            {
                if (customAttribute.Name == "Microsoft.VisualStudio.TestTools.UnitTesting.TestClassAttribute")
                {
                    generationContext.TestClass.CustomAttributes.Remove(customAttribute);
                    break;
                }
            }

            generationContext.TestClass.CustomAttributes.Add(new CodeAttributeDeclaration(new CodeTypeReference("Microsoft.VisualStudio.TestTools.UITesting.CodedUITestAttribute")));
        }
    }
} 
```
3. Build the project to generate an assembly (.dll) file, make sure this is built against the same version of .net that SpecFlow is which is currently 3.5 - and copy this file into your SpecFlow installation directory.
4. Add a config item to your CodedUI project's `App.Config` file
```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <section name="specFlow"
    type="TechTalk.SpecFlow.Configuration.ConfigurationSectionHandler,
TechTalk.SpecFlow"/>
  </configSections>
  <specFlow>
    <unitTestProvider name="MsTest.2010"
  generatorProvider="My.SpecFlow.MsTest2010CodedUiGeneratorProvider,
My.SpecFlow"
  runtimeProvider="TechTalk.SpecFlow.UnitTestProvider.MsTest2010RuntimeProvider,
TechTalk.SpecFlow"/>
  </specFlow>
</configuration>
```
5. Now when you generate a new feature file, it will add the appropriate attributes.

### Ensuring the SpecFlow hooks can use the CodedUI API

If you want to use any of the SpecFlow Hooks as steps such as [BeforeTestRun],[BeforeFeature], [BeforeScenario], [AfterTestRun], [AfterFeature] or [AfterScenario], unless you add specific code you will receive an error:
`Microsoft.VisualStudio.TestTools.UITest.Extension.TechnologyNotSupportedException: The browser  is currently not supported`

This is resolved by adding a `Playback.Initialize();` call in your [BeforeTestRun] step, and a `            Playback.Cleanup();` in your [AfterTestRun] step.

## Other Information
[Blog series on using Specflow with Coded UI Test API] (http://rburnham.wordpress.com/2011/03/15/bdd-ui-automation-with-specflow-and-coded-ui-tests/)
