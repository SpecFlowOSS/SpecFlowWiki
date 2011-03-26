With Cucumber, the Ruby testing framework that SpecFlow closely mirrors, variables can be passed between different step definition files.  Here is a very simple example:

    # steps1.rb
    Given /^a person exists by the name of John Galt$/ do
      @person = Person.new
      @person.name = 'John Galt'
    end

    # steps2.rb
    Then /^his name should be John Galt$/ do
      @person.name.should == 'John Galt'
    end

Thanks to Cucumber and Ruby, setting @person in one method causes @person to be available in a completely separate file.  How do we achieve the same result with SpecFlow and C#?  We use **ScenarioContext**.

**ScenarioContext** is a class that stores information relative to the state of the current scenario.  One of its greatest uses is to pass values between steps.  The code above can be implemented in SpecFlow like so:

    // step1.cs
    [Given(@"a person exists by the name of John Galt")]
    public void x(){
       var person = new Person{ Name = "John Galt"};
       ScenarioContext.Current["APerson"] = person;
       // or: ScenarioContext.Current.Set<Person>(person);
    }

    // step2.cs
    [Then(@"his name should be John Galt"]
    public void y(){
      var person = ScenarioContext.Current["APerson"];
      // or: var person = ScenarioContext.Current.Get<Person>();
      person.Name.ShouldEqual("John Galt");
    }

**ScenarioContext.Current** can be used as an IDictionary<string, object> to store values.  Those values will be retained for the life of the scenario run, and its contents will be cleared when the next scenario is run.

Loading values into ScenarioContext.Current can be done like so:
    ScenarioContext.Current["id"] = "value";
    ScenarioContext.Current["another_id"] = new ComplexObject();
    ScenarioContext.Current.Set<AnotherComplexObject>(new ComplexObject());
    ScenarioContext.Current.Set<AnotherComplexObject>(new AnotherComplexObject(), "special id");

And retrieving values from ScenarioContext can be done like so:
    var id = ScenarioContext.Current["id"];
    var complexObject = ScenarioContext.Current["another_id"] As ComplexObject;
    var anotherComplexObject = ScenarioContext.Current.Get<AnotherComplexObject>();
    var special = ScenarioContext.Current.Get<AnotherComplexObject>("special id");