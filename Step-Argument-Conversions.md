The [[step bindings]] can define parameters for better reusability. The arguments to execute the step bindings are calculated from the step text (with the regular expression groups) or the additional multi-line text or table arguments. These original arguments are provided as strings or `TechTalk.SpecFlow.Table` instances.

To avoid cumbersome conversions in the step binding methods, SpecFlow can do automatic conversion from the original argument to the parameter type of the method. 

All conversions are performed with the culture of the feature file, unless the [[&lt;bindingCulture&gt; element|Configuration]] is used in the configuration. See [[Feature Language]] for details.

The following conversions can be performed by SpecFlow (in the following precedence):

* no conversion, if the argument is an instance of the parameter type (e.g. the parameter type is `object` or `string`)
* step argument transformation
* standard conversion

##Standard Conversion

A standard conversion is performed by SpecFlow in the following cases:

* the argument can be converted to the parameter type with `Convert.ChangeType()`
* the parameter type is an `enum` type and the (string) argument is an enum value
* the parameter type is `Guid` and the argument contains a full GUID string or a GUID string prefix. In the later case the value will be filled with trailing zeroes.

##Step Argument Transformation

The step argument transformations can be used to apply a custom conversion step for the arguments of the step definitions. The step argument transformation is a method that provides a conversion from text (specified by a regular expression) or form a `Table` instance to an arbitrary .NET type. 

A step argument transformation is selected for converting an argument when

* the return type of the transformation is the same as the parameter type
* the regular expression (if specified) is matching to the original (string) argument
* if there are multiple matching transformation available, a warning is provided in the trace and the first transformation is used

The following example defines a transformation to a `DateTime` structure from relative day specifications, like `in 3 days`.

```c#
[StepArgumentTransformation(@"in (\d+) days?")]
public DateTime InXDaysTransform(int days)
{
  return DateTime.Today.AddDays(days);
}
```

The following example defines a transformation from any string input (no regex provided) to an `XmlDocument`.

```c#
[StepArgumentTransformation]
public XmlDocument XmlTransform(string xml)
{
  XmlDocument result = new XmlDocument();
  result.LoadXml(xml);
  return result;
}
```

The following example defines a transformation from a table argument to a list of `Book` entities (using the [[SpecFlow Assist Helpers]]). 

```c#
[StepArgumentTransformation]
public IEnumerable<Book> BooksTransform(Table booksTable)
{
  return table.CreateSet<Books>();
}
```

