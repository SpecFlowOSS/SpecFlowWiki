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

Tag:
```
@MsTest:DeploymentItem:test.txt
```

Output:
```
[Microsoft.VisualStudio.TestTools.UnitTesting.DeploymentItemAttribute("test.txt")]
```