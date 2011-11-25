Using ToProjection<T>, ToProjectionOfSet<T> and ToProjectionOfInstance<T> extension methods for LINQ-based instance and set comparison
---
**SpecFlow.Assist CompareToSet** Table extension method only checks for equivalence of collections which is a reasonable default. **SpecFlow.Assist** namespace also contains extension methods for With based operations.

Consider the following steps:

    Scenario: Match
    When I have a collection
    | Artist | Album |
    | Beatles | Rubber Soul |
    | Pink Floyd | Animals |
    | Muse | Absolution |
    Then it should match
    | Artist | Album |
    | Beatles | Rubber Soul |
    | Pink Floyd | Animals |
    | Muse | Absolution |
    And it should match
    | Artist | Album |
    | Beatles | Rubber Soul |
    | Muse | Absolution |
    | Pink Floyd | Animals |
    And it should exactly match
    | Artist | Album |
    | Beatles | Rubber Soul |
    | Pink Floyd | Animals |
    | Muse | Absolution |
    But it should not match
    | Artist | Album |
    | Beatles | Rubber Soul |
    | Queen | Jazz |
    | Muse | Absolution |
    And it should not match
    | Artist | Album |
    | Beatles | Rubber Soul |
    | Muse | Absolution |
    And it should not exactly match
    | Artist | Album |
    | Beatles | Rubber Soul |
    | Muse | Absolution |
    | Pink Floyd | Animals |

With LINQ-based operations each of the above comparisons can be expressed using a single line of code

    [When(@"I have a collection")]
    public void WhenIHaveACollection(Table table)
    {
    	var collection = table.CreateSet<Item>();
    	ScenarioContext.Current.Add("Collection", collection);
    }
 
    [Then(@"it should match")]
    public void ThenItShouldMatch(Table table)
    {
    	var collection = ScenarioContext.Current["Collection"] as IEnumerable<Item>;
    	Assert.IsTrue(table.RowCount == collection.Count() && table.ToProjection<Item>().Except(collection.ToProjection()).Count() == 0);
    }
 
    [Then(@"it should exactly match")]
    public void ThenItShouldExactlyMatch(Table table)
    {
    	var collection = ScenarioContext.Current["Collection"] as IEnumerable<Item>;
    	Assert.IsTrue(table.ToProjection<Item>().SequenceEqual(collection.ToProjection()));
    }
 
    [Then(@"it should not match")]
    public void ThenItShouldNotMatch(Table table)
    {
    	var collection = ScenarioContext.Current["Collection"] as IEnumerable<Item>;
    	Assert.IsFalse(table.RowCount == collection.Count() && table.ToProjection<Item>().Except(collection.ToProjection()).Count() == 0);
    }
 
    [Then(@"it should not exactly match")]
    public void ThenItShouldNotExactlyMatch(Table table)
    {
    	var collection = ScenarioContext.Current["Collection"] as IEnumerable<Item>;
    	Assert.IsFalse(table.ToProjection<Item>().SequenceEqual(collection.ToProjection()));
    }

In a similar way we can implement containment validation:

    Scenario: Containment
    When I have a collection
    | Artist | Album |
    | Beatles | Rubber Soul |
    | Pink Floyd | Animals |
    | Muse | Absolution |
    Then it should contain all items
    | Artist | Album |
    | Beatles | Rubber Soul |
    | Muse | Absolution |
    But it should not contain all items
    | Artist | Album |
    | Beatles | Rubber Soul |
    | Muse | Resistance |
    And it should not contain any of items
    | Artist | Album |
    | Beatles | Abbey Road |
    | Muse | Resistance |

    [Then(@"it should contain all items")]
    public void ThenItShouldContainAllItems(Table table)
    {
        var collection = ScenarioContext.Current["Collection"] as IEnumerable<Item>;
        Assert.IsTrue(table.ToProjection<Item>().Except(collection.ToProjection()).Count() == 0);
    }
 
    [Then(@"it should not contain all items")]
    public void ThenItShouldNotContainAllItems(Table table)
    {
        var collection = ScenarioContext.Current["Collection"] as IEnumerable<Item>;
        Assert.IsFalse(table.ToProjection<Item>().Except(collection.ToProjection()).Count() == 0);
    }
 
    [Then(@"it should not contain any of items")]
    public void ThenItShouldNotContainAnyOfItems(Table table)
    {
        var collection = ScenarioContext.Current["Collection"] as IEnumerable<Item>;
        Assert.IsTrue(table.ToProjection<Item>().Except(collection.ToProjection()).Count() == table.RowCount);
    }

What if Artist and Album are properties of different entities? Look at this piece of code:

    var collection = from x in ctx.Artists
                 where x.Name == "Muse"
                 join y in ctx.Albums on
                 x.ArtistId equals y.ArtistId
                 select new
                 {
                     Artist = x.Name,
                     Album = y.Name
                 };


**SpecFlow.Assist** has a generic class **EnumerableProjection<T>**. If a type “T” is known at compile time, **ToProjection** method converts a table or a collection straight to an instance of **EnumerableProjection**:

    table.ToProjection<Item>();

But if we need to compare a table with the collection of anonymous types from the example above, we need to express this type in some way so ToProjection will be able to build an instance of specialized **EnumerableProjection**. This is done by sending a collection as an argument to **ToProjection**. And to support both sets and instances and avoid naming ambiguity, corresponding methods are called **ToProjectionOfSet** and **ToProjectionOfInstance**:

    table.ToProjectionOfSet(collection);
    table.ToProjectionOfInstance(instance);

Here are the definitions of SpecFlow Table extensions methods that convert tables and collections of IEnumerables to EnumerableProjection:

    public static IEnumerable<Projection<T>> ToProjection<T>(this IEnumerable<T> collection, Table table = null)
    {
        return new EnumerableProjection<T>(table, collection);
    }
 
    public static IEnumerable<Projection<T>> ToProjection<T>(this Table table)
    {
        return new EnumerableProjection<T>(table);
    }
 
    public static IEnumerable<Projection<T>> ToProjectionOfSet<T>(this Table table, IEnumerable<T> collection)
    {
        return new EnumerableProjection<T>(table);
    }
 
    public static IEnumerable<Projection<T>> ToProjectionOfInstance<T>(this Table table, T instance)
    {
        return new EnumerableProjection<T>(table);
    }

Note that last arguments of **ToProjectionOfSet** and **ToProjectionOfInstance** methods are not used in method implementation. Their only purpose is to bring information about “T”, so the **EnumerableProjection** adapter class can be built properly. Now we can perform the following comparisons with anomymous types collections and instances:

    [Test]
    public void Table_with_subset_of_columns_with_matching_values_should_match_collection()
    {
        var table = CreateTableWithSubsetOfColumns();
        table.AddRow(1.ToString(), "a");
        table.AddRow(2.ToString(), "b");
 
        var query = from x in testCollection
                select new { x.GuidProperty, x.IntProperty, x.StringProperty };
 
        Assert.AreEqual(0, table.ToProjectionOfSet(query).Except(query.ToProjection()).Count());
    }
 
    [Test]
    public void Table_with_subset_of_columns_should_be_equal_to_matching_instance()
    {
        var table = CreateTableWithSubsetOfColumns();
        table.AddRow(1.ToString(), "a");
 
        var instance = new { IntProperty = testInstance.IntProperty, StringProperty = testInstance.StringProperty };
 
        Assert.AreEqual(table.ToProjectionOfInstance(instance), instance);
    }
