Besides the execution of the acceptance criteria of the application, SpecFlow supports the development process with further useful tools. This additional tools can be invoked through the `specflow.exe` command-line tool. The tool has to be parametrized from command line arguments. Executing the tool without any argument displays the possible commands. The `help` command can be used to display the detailed usage of the specific commands.
 
One part of the available tools are to provide different reports. The page [[Reporting]] discusses these options.

##Generate All Tool

The `generateall` command can be used to re-generate all outdated unit test classes based on the feature file. This tool can be useful when upgrading to a newer SpecFlow version or when the feature files are modified outside of Visual Studio.

The following table contains the possible arguments for this command.

<table>
    <tr>
        <th>Attribute</th>
        <th>Value</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>projectFile</td>
        <td></td>
        <td>A path of the project file containing the feature files. This is a mandatory argument.</td>
    </tr>
    <tr>
        <td>/force</td>
        <td>-</td>
        <td>Forces re-generation even if the generated class is up-to-date based on the file modification time and the SpecFlow generator version.<br/>
            Default: disabled (only outdated files are generated)</td>
    </tr>
    <tr>
        <td>/verbose</td>
        <td>-</td>
        <td>Displays detailed information about the generation process.<br/>
            Default: disabled</td>
    </tr>
</table>

The following example shows how to regenerate the unit tests for the BookShop sample application.

```
specflow.exe generateall BookShop.AcceptanceTests.csproj
```

