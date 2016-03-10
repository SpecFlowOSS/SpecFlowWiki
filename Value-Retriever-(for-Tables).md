# Value Retrievers

SpecFlow can turn properties in a table like this:

```gherkin
Given I have the following people
| First Name | Last Name | Age | IsAdmin |
| John       | Galt      | 40  | true    |
```

Into an object like this:

```c#
public class Person
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public int Age { get; set; }
    public bool IsAdmin { get; set; }
}
```

With commands like these:

```c#
    [Given(@"I have the following people")]
    public void x(Table table)
    {
        var person = table.CreateInstance<Person>();
        // OR
        var people = table.CreateSet<Person>();
    }

```

But how does SpecFlow match the values in the table with the values in the object?  It does so with Value Retrievers.  There are value retrievers defined for almost every C# base type, so mapping most basic POCOs can be done with SpecFlow without any modification.

## Extending with your own value retrievers

Often you might have a more complicated POCO type, one that is not comprised solely of C# base types.  Like this one:

```c#
    public class Shirt
    {
        public Guid Id { get; set; }
        public string Name { get; set; }
        public Color Color { get; set; }
    }

    public class Color
    {
        public string Name { get; set; }
    }
```
