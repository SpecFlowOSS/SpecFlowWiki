CreateInstance<T>
---
**CreateInstance<T>** is an extension method off of the Table object that will convert the table data to an object.  For example, if you have the following step:

	Given I entered the following data into the new account form:
	| Field              | Value      |
	| Name               | John Galt  |
	| Birthdate          | 2/2/1902   |
	| HeightInInches     | 72         |
	| BankAccountBalance | 1234.56    |

You can convert the data in the table to an instance of an object like so:

	[Given(@"Given I entered the following data into the new account form:")]
	public void x(Table table)
	{
		var account = table.CreateInstance<Account>();
		// ...
	}

The CreateInstance<T> method will create the Account object and fill the values according to any matching names it finds.  It also will use the appropriate casting or conversion to turn your string into the appropriate type.

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

The CreateSet<T> method will return an IEnumerable<T> based on the data that matches in the table.  It will fill the values for each object, doing the appropriate conversions from string to the related property.