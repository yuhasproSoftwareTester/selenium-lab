# TestNG

## What is TestNG

TestNG is a testing framework for Java. The name stands for Test Next Generation. It was created to overcome the limitations of JUnit and to provide a more powerful and flexible way to write and run tests. It supports unit tests, integration tests, end-to-end tests, and data-driven tests. It is widely used with Selenium for automation testing.

---

## Advantages of TestNG over JUnit

| Aspect | TestNG | JUnit |
|--------|--------|-------|
| Annotations | More flexible and powerful annotations | Basic annotation set |
| Parallel execution | Built-in support for running tests in parallel | Limited or requires extra setup |
| Dependency testing | Allows one test to depend on another | Not supported |
| Grouping | Tests can be grouped and run selectively | Less flexible grouping |
| Data providers | Built-in data-driven testing with DataProvider | Requires external libraries or manual loops |
| Reporting | Generates detailed HTML reports by default | Basic reporting, needs plugins |
| Parameterization | Easy parameter passing via XML or DataProvider | Limited parameter support |
| Setup and teardown | Multiple levels: before suite, test, class, method | Fewer levels |
| Ignore tests | Skip tests dynamically | Basic ignore annotation |
| Exception testing | Detailed and flexible | Simpler approach |

TestNG is generally preferred for large automation projects because it handles complex test flows, dependencies, and data variations better than JUnit.

---

## TestNG Installation

TestNG is installed as a dependency in your Java project.

**Using Maven**: Add the TestNG dependency to your pom.xml file. Maven downloads it automatically.

**Using Gradle**: Add the TestNG dependency to your build.gradle file.

**Using Eclipse IDE**: Install the TestNG plugin from the Eclipse Marketplace. This adds TestNG options to the run menu.

**Using IntelliJ IDEA**: TestNG support is built-in. Just add the dependency to your build tool.

No manual download is needed if you use a build tool like Maven or Gradle.

---

## Features of TestNG

**Annotations**: TestNG uses annotations to mark methods as tests, setup methods, or teardown methods. This removes the need to follow specific naming conventions.

**Test Priority**: You can assign priority numbers to tests. Lower priority runs first. This helps when tests must run in a specific order.

**Grouping**: Tests can be tagged with group names like smoke, regression, or sanity. You can run only specific groups instead of the entire suite.

**Parallel Execution**: TestNG can run multiple tests or classes at the same time using multiple threads. This reduces total execution time significantly.

**DataProvider**: A single test method can run multiple times with different sets of data. This is the core of data-driven testing in TestNG.

**Dependencies**: You can specify that one test should only run if another test passes. If the first test fails, the dependent test is skipped.

**Listeners**: TestNG allows you to create custom listeners that perform actions before or after tests, suites, or methods. This is useful for logging, reporting, or taking screenshots.

**Retry mechanism**: Failed tests can be automatically retried a specified number of times before being marked as failed.

**Parameterization**: Values can be passed to tests from the testng.xml file. This is useful for environment-specific data like URLs or browser names.

**Assertions**: TestNG provides a rich set of assertion methods to validate expected outcomes against actual results.

**HTML Reports**: After execution, TestNG generates a detailed HTML report showing passed, failed, and skipped tests with execution times.

---

## Running Test Cases

There are multiple ways to run TestNG tests.

**From IDE**: Right-click on the test class or method and select Run as TestNG Test. This is used during development for quick feedback.

**From testng.xml**: Create an XML file that lists which classes or methods to run. Right-click the XML file and run it. This is the standard way to run suites.

**From Command Line**: Use Maven or Gradle commands to trigger TestNG execution. This is used in CI/CD pipelines.

**From Build Tools**: Maven uses the surefire plugin. Gradle has built-in TestNG support. Both can be configured to run tests automatically during the build.

---

## TestNG.xml File

The testng.xml file is the heart of TestNG execution. It is an XML configuration file that controls how tests are organized and executed.

**Purpose**: It defines the test suite, which contains one or more tests. Each test contains one or more classes. You can also define groups, parameters, listeners, and parallel settings in this file.

**Structure**: The file starts with a suite tag. Inside the suite, you define test tags. Inside each test, you define classes to run. You can also include or exclude specific methods or groups.

**Benefits**:
- You can run multiple test classes together without changing code.
- You can enable or disable tests by commenting them out.
- You can pass parameters like browser type or environment URL.
- You can configure parallel execution at suite, test, or class level.
- You can include or exclude groups dynamically.

**Example of what it controls**:
- Run only the smoke test group
- Run tests on Chrome and Firefox in parallel
- Pass the base URL as a parameter
- Include classes from different packages in one run
---
Without the testng.xml file, you would have to manually run each class or method from the IDE. The XML file makes test execution organized, repeatable, and suitable for automation pipelines.

---