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
