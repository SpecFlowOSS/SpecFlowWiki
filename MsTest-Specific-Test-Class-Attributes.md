# MsTest Specific Test Class Attributes

SpecFlow can generate MsTest specific test class attributes from tags specified on a feature.

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

Tag:
```
@MsTest:DeploymentItem:Resources\DeploymentItemTestFile.txt:Data
```

Output:
```
[Microsoft.VisualStudio.TestTools.UnitTesting.DeploymentItemAttribute("Resources\\DeploymentItemTestFile.txt", "Data")]
```