## Global Container

Captures global services for test execution and the step definition, hook and transformation discovery result (i.e. what step definitions you have).

* IRuntimeConfigurationProvider
* ITestRunnerManager
* IStepFormatter
* ITestTracer
* ITraceListener
* ITraceListenerQueue
* IErrorProvider
* IRuntimeBindingSourceProcessor
* IRuntimeBindingRegistryBuilder
* IBindingRegistry
* IBindingFactory
* IStepDefinitionRegexCalculator
* IBindingInvoker
* IStepDefinitionSkeletonProvider
* ISkeletonTemplateProvider
* IStepTextAnalyzer
* IRuntimePluginLoader
* IBindingAssemblyLoader
* IBindingInstanceResolver
* [RuntimePlugins](https://github.com/techtalk/SpecFlow/blob/master/TechTalk.SpecFlow/Plugins/IRuntimePlugin.cs)
 * RegisterGlobalDependencies- Event
 * CustomizeGlobalDependencies- Event


## Test Thread Container (parent Container is the Global Container)

Captures services and state for executing the scenarios on a particular test thread. For parallel test execution, multiple test runner containers are created, one for each thread.

* ITestRunner
* IContextManager
* ITestExecutionEngine
* IStepArgumentTypeConverter
* IStepDefinitionMatchService
* ITraceListener
* ITestTracer
* [RuntimePlugins](https://github.com/techtalk/SpecFlow/blob/master/TechTalk.SpecFlow/Plugins/IRuntimePlugin.cs)
 * CustomizeTestThreadDependencies- Event


## Feature Container (parent Container is the Test Thread Container)

Captures a feature's execution state. Disposed after the feature is executed.

* (step definition classes)
* (dependencies of the step definition classes, aka context injection)
* FeatureContext (also available from the *Test Thread Container* through `IContextManager`)
* [RuntimePlugins] 
 * CustomizeFeatureDependencies- Event


## Scenario Container (parent Container is the Test Thread Container)

Captures the state of a scenario execution. Disposed after the scenario is executed.

* (step definition classes)
* (dependencies of the step definition classes, aka context injection)
* ScenarioContext (also available from the *Test Thread Container* through `IContextManager`)
* [RuntimePlugins] 
 * CustomizeScenarioDependencies- Event
