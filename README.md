# EVNFM Performance Testing

## How to setup a new test plan

1. Create a new folder under `src/test/jmeter/plans`
2. Name the folder carefully since this folder name will be used as execution parameter for this test plan. For example. if the folder name
   is`performance-test`, execution parameter for the test will be: `-Dtest-name=performance-test`
3. Create the test plan in JMeter gui and save it in this folder. File name should be same as folder created for this test plan. For example. if
   folder name is `performance-test`, test plan should be saved as `performance-test.jmx`. This will be needed when running plugin's gui goal.
4. Create test specific configuration file if needed and save it in your test plan folder. Note: Configuration file name should be `user.properties`
   since jmeter plugin expects that file for parameters.
5. After setting up, run the gui (see `How to run gui`) and do necessary adjustments in the test plan. Running from plugin is needed since plugin
   configure the global and user properties for tests can be executed.

**Note:** Any JMeter properties will be residing in the `user.properties` or `global.properties` can be accessed using read property function built in
JMeter.

**Example:** `${__P(host)}` or `${__property(username)}`

## How to execute JMeter Test Plans

### With Maven plugin

When running JMeter tests with maven plugin, test execution becomes fully automated.
With plugin, **JMeter variables** can be initialized in the test plan, and they can be used during the test execution. They can be considered 
similar to environment variables that are accessible from outside of Test plan files (`.jmx`).

Additional to using JMeter variables;
 - Multiple tests can be executed with single `mvn` command.
 - Reports can be generated and collected for each test execution.

#### mvn CLI

- Update the global environment values in the `global.properties` file located in the `configuration` folder. 
- Update test specific JMeter properties in the `user.properties` file located in the test plan folder.
- Run the `verify` phase for configuring and executing tests in the test plan folder.

``mvn clean verify -Pperformance -Dtest-name=<created test folder name>``

Example:

``mvn clean verify -Pperformance -Dtest-name=1000-cluster``

#### JMeter GUI

When using JMeter maven plugin JMeter GUI also, needs to be executed by the plugin itself. Maven plugin allows the configuration to be loaded into 
the user interface, so they can be accessible when running tests from GUI.

To execute tests using JMeter gui, properties needs to be initialized/configured first. Without configuring global properties, jmeter cannot find the
properties and test executions will be unsuccessful. First maven configure goal needs to be executed for setting required parameters, then gui can run
the tests created as jmx files. 

 - Configure JMeter variables. -> `jmeter:configure` 
 - Execute JMeter GUI jar -> `jmeter:gui`
   
Run the command below to open GUI automatically.

##### How to run GUI

``mvn jmeter:configure jmeter:gui -Pperformance -pl eric-eo-evnfm-acceptance-testware-performance -Dtest-name=<test-file-name>``

Example:

``mvn jmeter:configure jmeter:gui -Pperformance -pl eric-eo-evnfm-acceptance-testware-performance -Dtest-name=1000-clusters``

> Note: `-pl eric-eo-evnfm-acceptance-testware-performance` command is not needed if you `cd` into `eric-eo-evnfm-acceptance-testware-performance` module folder.
### Test Results

#### Results

Results will be saved in the `/target/performance/results` path. (`<jmeter.results>`)

By default, results are in `.csv` format with basic information about test execution.

#### Reports

Reports will be saved in the `/target/performance/reports` path. (`<jmeter.reports>`)

Report Dashboard is saved in `html` format and has more detailed information about test execution.

### JMeter Maven Properties

#### Default Properties

```
<jmeter.results>${project.basedir}/target/performance/results</jmeter.results>
<jmeter.results.format>csv</jmeter.results.format>
<jmeter.reports>${project.basedir}/target/performance/reports</jmeter.reports>
<jmeter.version>5.4.2</jmeter.version>
<jmeter.global.props>${project.basedir}/src/test/jmeter/configuration/global.properties</jmeter.global.props>
<jmeter.plugin.version>3.5.0</jmeter.plugin.version>
```

### Without Maven Plugin

#### JMeter CLI

Tests also can be run using JMeter cli using terminal.

``jmeter -n -t EVNFM_performance_lightweight_last.jmx -l results-lightweight-disabled.jtl``

#### JMeter Gui (Without maven plugin)

If any JMeter property is set in the test plan, they should be updated when running JMeter GUI without initializing (Without maven plugin).
Example: Replace any `${__P(host)}` with the corresponding value in the GUI, because, the maven plugin replaces these values in the configuration
phase and set the JMeter properties to be used in the test plan. (i.e. `global.properties`)

**!! Important: JMeter GUI should never be used for actual execution of any tests. GUI only should be used for debugging purposes.**
