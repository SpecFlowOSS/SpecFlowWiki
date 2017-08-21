_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Test-result]]. We use the GitHub wiki for authoring the documentation pages._

When SpecFlow tests are executed the execution engine processes the test steps, executes the necessary test logic and either finish successfully or fails with some reason. 

## Test Passes
While the tests are executed the engine also outputs useful information about the execution to the test output. Therefore in some cases it makes sense to investigate the test output even if the test was passing. 

The test output shows by default the executed test steps, the invoked test logic methods ([[bindings]]) and the execution time of the longer operations. The information displayed in the test output can also be configured. See [[&lt;trace&gt; configuration element|Configuration]].

## Test Fails because of a Test/Business Logic Error
A test can fail because the test/business logic reports an error. This is reported as a test error, you can investigate the test output for the detailed information (e.g. stack trace) of the error.

## Missing, Pending or Improperly Configured Bindings
The test can also fail because some parts of the test logic (bindings) were not implemented yet (or configured improperly). This is reported by default with the “inconclusive” result. You can change how SpecFlow should behave in this case. See [[&lt;runtime&gt; configuration element|Configuration]].

Some unit test framework does not support inconclusive result. In this case the problem is reported as an error by default.
The test output can be very useful for missing bindings as it contain a step binding method skeleton that you can copy to your project and fill-in with the test logic.

## Ignored Tests
Just like with normal unit tests, you can also ignore a SpecFlow test. This can be done by marking the scenario with the `@ignore` tag. Don't forget that ignoring a test will not solve the problem... ;-)
