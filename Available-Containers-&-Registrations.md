## Global Container

Captures global services for test execution and the step definition, hook and transformation discovery result (ie what step definitions you have).

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
* IRuntimePlugin.RegisterDependencies - for dependencies from RuntimePlugins
* (plugins)

##Test Thread Container (parent Container is the Global Container)

Captures services and state for executing the scenarios on a particular test thread. For parallel test execution, multiple test runner containers are created (one for each thread).

* ITestRunner
* IContextManager
* ITestExecutionEngine
* IStepArgumentTypeConverter
* IStepDefinitionMatchService
* ITraceListener
* ITestTracer

##Scenario Container (parent Container is the Test Runner Container)

Captures the state of a scenario execution. Disposed after the scenario is executed.

* (step definition classes)
* (dependencies of the step definition classes, aka context injection)