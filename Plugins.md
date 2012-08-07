SpecFlow is providing an improved plugin infrastructure for customization. You can implement SpecFlow plugins that can change the behavior of the built-in generator and runtime components. A typical plugin can for example provide support for a new unit testing framework.

To use a custom plugin it has to be enabled in the [[configuration]] of the SpecFlow project:

```xml
<specFlow>
  <plugins>
    <add name="MyPlugin" />
  </plugins>
</specFlow>
```

Note: More information about plugins comes soon!