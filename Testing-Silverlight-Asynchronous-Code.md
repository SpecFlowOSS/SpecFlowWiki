**Coming!** Version 1.7 will also support testing Silverlight asynchronous code with the help of the Silverlight Unit Test Framework. You can read about the background [[Ryan's post|http://rburnham.wordpress.com/2011/05/13/testing-silverlight-asynchronous-code-with-specflow/]].

The facts (please consider them as beta):
## Configure Specflow project to use async testing

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <section name="specFlow"
      type="TechTalk.SpecFlow.Configuration.ConfigurationSectionHandler, TechTalk.SpecFlow"/>
  </configSections>
  <specFlow>
    <unitTestProvider name="MSTest.Silverlight4" />
    <generator generateAsyncTests="true" />
  </specFlow>
</configuration>
```

## Use async operations from your step bindigns

The async support provides you several API methods for doing that.
<table>
    <tr>
        <th>API Method</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>void EnqueueCallback(Action callback)</td>
        <td>Enqueues an action to be executed asynchronously.<td>
    </tr>
    <tr>
        <td>void EnqueueCallback(params Action[] callbacks)</td>
        <td>Enqueues a number of actions to be executed asynchronously, but consecutively.<td>
    </tr>
    <tr>
        <td>void EnqueueConditional(Func<bool> continueUntil)</td>
        <td>Enqueues an asynchronous and non-blocking wait until the condition returns true.
The `continueUntil` predicate that must return true before the work queue is continued.<td>
    </tr>
    <tr>
        <td>void EnqueueDelay(TimeSpan delay)</td>
        <td>Enqueues an asynchronous and non-blocking wait for at least the given time before continuing. The delay is approximate, and not intended to be highly accurate.<td>
    </tr>
    <tr>
        <td>void EnqueueDelay(double milliseconds)</td>
        <td>Enqueues an asynchronous and non-blocking wait for at least the given time before continuing. The delay is approximate, and not intended to be highly accurate.<td>
    </tr>
</table>

For accessing these API methods, you have two options currently.

1. Derive your step binding class from `TechTalk.SpecFlow.Async.AsyncTests` and use the methods inherited from the base class.
2. Use `AsyncContext.Current` to access the API methods.


NOTE: The class TechTalk.SpecFlow.Async.AsyncTests doesn't exist in either 1.7.1 or 1.8.1