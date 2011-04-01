You can use SpecFlow for developing Windows Phone 7 applications. Just do these simple steps.

*(Windows Phone 7 support for SpecFlow was done by Max Paulousky [[http://www.maxpaulousky.com]])*

### Install prerequisites

- [[Windows Phone Developer Tools RTW|http://www.microsoft.com/downloads/en/details.aspx?FamilyID=04704acf-a63a-4f97-952c-8b51b34b00ce&displaylang=en]]
- [[Windows Phone Developer Tools January 2011 Update|http://www.microsoft.com/downloads/en/details.aspx?FamilyID=49b9d0c5-6597-4313-912a-f0cca9c7d277&displaylang=en]] (optional)
- [[Silverlight Unit Test Framework |http://code.msdn.microsoft.com/silverlightut]]

### Create unit test project
- You can find a good description about this at [[http://www.smartypantscoding.com/a-cheat-sheet-for-unit-testing-silverlight-apps-on-windows-phone-7]]

### SpecFlow runtime for WP7

- Add a reference to `TechTalk.Specflow.WindowsPhone7.dll` to the test project.

### Configure SpecFlow

- Add an app.config to the project (even if it’s not supported by WP7), with the following content:

```
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <configSections>
        <section name="specFlow" type="TechTalk.SpecFlow.Configuration.ConfigurationSectionHandler, TechTalk.SpecFlow"/>
      </configSections>

      <specFlow>
        <unitTestProvider name="MsTest.WindowsPhone7"/>
      </specFlow>
    </configuration>
```

### Start writing specs

Add feature files and step definitions to the test project. You can use the templates in “Add → New Item…” for that.

### Run your tests

Set the project as a startup one and execute it. If you use a device, unlock the screen before starting tests. You should see the result of the test execution displayed on the screen of your device or simulator.

### SpecFlow WP7 sample

See [[BowlingKata-WindowsPhone7-MsTest project|https://github.com/techtalk/SpecFlow-Examples]]  as a Windows Phone 7 example