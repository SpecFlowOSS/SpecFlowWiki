# Test Class Attributes

The MsTest Generator can generate test class attributes from tags specified on a feature.

## Owner

Tag:
```
@Owner:John
```

Output:
```
[Microsoft.VisualStudio.TestTools.UnitTesting.OwnerAttribute("John")]
```

## WorkItem

Tag:
```
@WorkItem:123
```

Output:
```
[Microsoft.VisualStudio.TestTools.UnitTesting.WorkItemAttribute(123)]
```

## DeploymentItem

**New in SpecFlow 2.2.0**

### Example 1 : Copy a file to the same directory as the deployed test assemblies

Tag:
```
@MsTest:DeploymentItem:test.txt
```

Output:
```
[Microsoft.VisualStudio.TestTools.UnitTesting.DeploymentItemAttribute("test.txt")]
```

### Example 2 : Copy a file to a sub-directory relative to the deployment directory

**New in SpecFlow 2.2.1**

Tag:
```
@MsTest:DeploymentItem:Resources\DeploymentItemTestFile.txt:Data
```

Output:
```
[Microsoft.VisualStudio.TestTools.UnitTesting.DeploymentItemAttribute("Resources\\DeploymentItemTestFile.txt", "Data")]
```

# Accessing `TestContext`

**New in SpecFlow 2.2.1**

## Using Context Injection

```
public class MyStepDefs
{
    private readonly TestContext _testContext;
    public MyStepDefs(TestContext testContext) // use it as ctor parameter
    { 
        _testContext = testContext;
    }

    [BeforeScenario()]
    public void BeforeScenario()
    {
        //now you can access the TestContext
    } 
}
```

## Using the Scenario Container

```
[Given(@"my test step definition")]
public void MyStepDefinition()
{
   var testContext = ScenarioContext.Current.ScenarioContainer.Resolve<Microsoft.VisualStudio.TestTools.UnitTesting.TestContext>();
}
```