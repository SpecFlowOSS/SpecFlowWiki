_Editor note: We recommend reading this documentation entry at [[http://www.specflow.org/documentation/Parallel-Execution]]. We use the GitHub wiki for authoring the documentation pages._

SpecFlow is mainly used to drive integration test that have external dependencies and driving applications with complex internal architecture. Because of this, it is generally not easy to execute these tests parallel.

## Parallel Execution with memory (AppDomain) isolation

If there are no external dependencies or can be cloned for parallel execution, but the application architecture depends on static state (caches, etc.), the best way is to execute them in parallel in AppDomain isolation. This way every test execution thread will be hosted in a separate AppDomain, so the memory (e.g. static fields) are isolated. SpecFlow can be used for such cases without extra consideration. SpecFlow+ Runner supports such parallel execution with AppDomain or Process isolation.

_Note:_ The `[BeforeTestRun]` and `[AfterTestRun]` hooks are executed for each individual test execution thread (AppDomain), so you can use them to initialize/reset shared memory. 

## Parallel Execution without memory isolation

If the tests do not depend on any static state (ie. do not store any test-specific information in static fields), you can run the tests parallel without AppDomain isolation. The memory and the initialization footprint of this kind of execution is smaller.

To run SpecFlow tests parallel without memory isolation you

- need a test runner that has such feature (currently NUnit v3 (`nunit`), xUnit v2 (`xunit`) and SpecFlow+ Runner v2 (`specrun`) can be used)
- must not use the static context properties: `ScenarioContext.Current`, `FeatureContext.Current` or `ScenarioStepContext.Current` (see examples below).
 
### Execution Behavior

-	`[BeforeTestRun]` and `[AfterTestRun]` hooks (events) are executed only once, on the first thread that initializes the framework first. The test execution on the other threads are blocked until the hoods fully executed on the first thread.
-	Each thread manages its own enter/exit feature execution workflow. The `[BeforeFeature]` and `[AfterFeature]` hooks might be executed multiple times on different threads, if the different threads run scenarios from the same feature file. The execution of these hooks do not block each-other, but within a single thread the Before/After feature hooks are running in pairs (the `[BeforeFeature]` hook of the next scenario never executed earlier than the `[AfterFeature]` hook of the previous one). Each thread has a separate (and isolated) `FeatureContext`.
-	The execution of the scenarios with the related hooks (Before/After scenario, scenario block, step) are running isolated in the different threads and do not block each-other. Each thread has a separate (and isolated) `ScenarioContext`.
-	The test trace listener (that emits scenario execution trace to console by default) is invoked asynchronously from the multiple threads and the trace messages are queued and passed to the listener serialized. If the test trace listener implements `TechTalk.SpecFlow.Tracing.IThreadSafeTraceListener`, the messages are sent directly from the threads. 
-	The binding registry (that holds the step definitions, hooks, etc.) and some other core services are shared across test threads.

### Notes for NUnit v3 Support

Currently the NUnit v3 unit test provider (`nunit`) does not generate `[Parallelizable]` attributes on feature classes or scenario methods. The parallelization has to be configured by setting an assembly-level attribute in the SpecFlow project.

```c#
[assembly: Parallelizable(ParallelScope.Fixtures)]
```

### Using ScenarioContext, FeatureContext and ScenarioStepContext in a thread-safe way

Context injection is a type safe state sharing method, that is thread-safe, so it is recommended to use that also in non-parallel execution scenarios. 

In parallel execution, if the generic contexts has to be used, instead of accessing the  `ScenarioContext.Current`, `FeatureContext.Current` or `ScenarioStepContext.Current` static properties, the context classes have to be injected to the binding class, or the instance properties of the `Steps` base class can be used. Accessing the static properties during parallel execution throws a `SpecFlowException`.

#### Injecting ScenarioContext to the binding class

```c#
[Binding]
public class StepsWithScenarioContext
{
	private readonly ScenarioContext scenarioContext;

	public StepsWithScenarioContext(ScenarioContext scenarioContext)
	{
		if (scenarioContext == null) throw new ArgumentNullException("scenarioContext");
		this.scenarioContext = scenarioContext;
	}

	[Given(@"I put something into the context")]
	public void GivenIPutSomethingIntoTheContext()
	{
		scenarioContext.Set("test-value", "test-key");
	}
}
```

Injecting `FeatureContext` can be done similarly, and for accessing the `ScenarioStepContext` the `StepContext` property of the injected `ScenarioContext` can be used.

#### Using ScenarioContext from the Steps base class

```c#
[Binding]
public class StepsWithScenarioContext : Steps
{
	[Given(@"I put something into the context")]
	public void GivenIPutSomethingIntoTheContext()
	{
		this.ScenarioContext.Set("test-value", "test-key");
	}
}
```

The other contexts can be accessed with the `FeatureContext` and the `StepContext` properties.