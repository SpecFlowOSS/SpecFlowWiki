_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/SpecFlow-Assist-Helpers]]. We use the GitHub wiki for authoring the documentation pages._

To use these helpers, we need to add the ```TechTalk.SpecFlow.Assist``` namespace to the project.

CreateInstance<T>
---
**CreateInstance<T>** is an extension method off of the Table object that will convert the table data to an object.  For example, if you list data in a table that lists the values of your object like this:

	Given I entered the following data into the new account form:
	| Field              | Value      |
	| Name               | John Galt  |
	| Birthdate          | 2/2/1902   |
	| HeightInInches     | 72         |
	| BankAccountBalance | 1234.56    |

or in a horizontal table like this:

	Given I entered the following data into the new account form:
	| Name      | Birthdate | HeightInInches | BankAccountBalance |
	| John Galt | 2/2/1902  | 72             | 1234.56            |

You can convert the data in the table to an instance of an object like so:

	[Given(@"Given I entered the following data into the new account form:")]
	public void x(Table table)
	{
		var account = table.CreateInstance<Account>();
		// account.Name will equal "John Galt", HeightInInches will equal 72, etc.
	}

The **CreateInstance<T>** method will create the Account object and set properties according to what can be read from the table.  It also will use the appropriate casting or conversion to turn your string into the appropriate type.

The headers in this table can be "Field" and "Value," or anything that you want.  What matters is that the first column has the property name and the second column has the value.

***

CreateSet<T>
---
**CreateSet<T>** is an extension method off of the Table object that will convert the table data to a set of objects.  For example, if you have the following step:

	Given these products exist
	| Sku              | Name             | Price |
	| BOOK1            | Atlas Shrugged   | 25.04 |
	| BOOK2            | The Fountainhead | 20.15 |

You can convert the data in the table to a set of objects like so:

	[Given(@"Given these products exist")]
	public void x(Table table)
	{
		var products = table.CreateSet<Product>();
		// ...
	}

The **CreateSet<T>** method will return an IEnumerable<T> based on the data that matches in the table.  It will fill the values for each object, doing the appropriate conversions from string to the related property.

***

CompareToInstance<T>
---
**CompareToInstance<T>** makes it easy to compare the properties of an object against a table. For example, say you have a class like this:

    public class Person {
      public string FirstName { get; set;}  
      public string LastName { get; set; }
      public int YearsOld { get; set; }
    }

and you want to compare it to a table in a step like this:

    Then the person should have the following values
    | Field     | Value |
    | FirstName | John  |
    | LastName  | Galt  |
    | YearsOld  | 54    |
  
You can assert that the properties match with this simple step definition:
  
    [Then("the person should have the following values")]
    public void x(Table table){
      // you don't have to get person this way, this is just for demo
      var person = ScenarioContext.Current.Get<Person>(); 
      
      table.CompareToInstance<Person>(person);
    }

If FirstName does not match "John", LastName does not match "Galt", or YearsOld does not match 54, a descriptive error showing the differences will be thrown.

If they do match, no exception will be thrown and SpecFlow will continue to process your scenario.

~~**Note: The headers on the table must be "Field" and "Value".**~~ Like mentioned above, Field/Value can be replaced with any words.  Plus, your values can be listened horizontally in a table.

***

CompareToSet<T> extension methods off of SpecFlow.Table
---
**CompareToSet<T>** makes it easy to compare the values in a table to a set of objects.  For example, say you have a class like this:

    public class Account {
      public string Id { get; set;}
      public string FirstName { get; set;}
      public string LastName { get; set;}
      public string MiddleName { get; set;}
    }

And you want to test that your system returns a specific set of accounts, like so:

    Then I get back the following accounts
    | Id     | FirstName | LastName |
    | 1      | John      | Galt     |
    | 2      | Howard    | Roark    |

You can test you results with one call to CompareToSet<T>, like so:

    [Then("I get back the following accounts")]
    public void x(Table table){
      var accounts = ScenarioContext.Current.Get<IEnumerable<Account>>();
      
      table.CompareToSet<Account>(accounts)
    }

In this example, CompareToSet<T> will test that two accounts were returned, and it will test only the properties that you define in the table.  **It does not test the order of the objects, only that one was found that matches.**  If it cannot find a record that matches the properties in your table, the exception that is thrown will return the row number(s) that did not match.

Column naming
---
The SpecFlow Assist helpers use the values found in your table to determine what properties to set on your object.  However, the names on the column do not have to be an exact match.  For example, this table:

    | FirstName | LastName | DateOfBirth | HappinessRating |

... will be evaluated the same as this table:

    | First name | Last name | Date of birth | HAPPINESS rating |

Matches against properties on your object are case-insensitive and ignore spaces.  This allows you to make your tables more readable to others.