# Parallel Script Execution in TestNG

## What is Parallel Execution

Parallel execution means running multiple tests at the same time instead of one after another. TestNG creates multiple threads, and each thread runs a different test or class simultaneously. This reduces the total execution time from hours to minutes.

---

## Why Use It

| Reason | Explanation |
|--------|-------------|
| Faster Feedback | A suite of 100 tests that takes 2 hours can finish in 20 minutes. |
| Better Resource Use | Multiple CPU cores are used instead of leaving them idle. |
| CI/CD Friendly | Builds complete faster, allowing quicker deployments. |
| Scalability | Add more threads as your test suite grows. |

---

## Levels of Parallelism

TestNG supports parallel execution at different levels:

| Level | What Runs in Parallel |
|-------|----------------------|
| methods | Every @Test method runs on its own thread. |
| classes | Each test class runs on its own thread. |
| tests | Each <test> tag in testng.xml runs on its own thread. |
| instances | Each instance of a test class runs separately. |

---

## How to Enable It

Parallel execution is controlled through the `testng.xml` file. You set two attributes on the `<suite>` tag:

- `parallel="methods"` (or classes, tests)
- `thread-count="5"` (number of simultaneous threads)

Example configuration:
```xml
<suite name="ParallelSuite" parallel="methods" thread-count="4">
    <test name="ParallelTest">
        <classes>
            <class name="TestClassOne"/>
            <class name="TestClassTwo"/>
        </classes>
    </test>
</suite>
```

This runs all test methods across 4 threads at the same time.

---

## Important Considerations

| Consideration | Explanation |
|---------------|-------------|
| Thread Safety | Tests must not share variables or data. Each test should be independent. |
| Browser Conflicts | If tests share the same browser instance, they will interfere. Each test needs its own WebDriver object. |
| Data Providers | Use `parallel=true` inside @DataProvider to run data iterations in parallel. |
| Order Independence | Tests cannot depend on each other when running in parallel. |

---

## Parallel Data Provider

You can also run data-driven tests in parallel:

```java
@DataProvider(name = "data", parallel = true)
public Object[][] getData() {
    return new Object[][] { {"user1"}, {"user2"}, {"user3"} };
}
```

Each data row runs on a separate thread.

---

# TestNG HTML Reports

## What are HTML Reports

After every test execution, TestNG automatically generates HTML reports. These reports provide a visual summary of what happened during the test run. They are saved in a folder called `test-output` inside your project directory.

---

## How to Access Them

After running tests through testng.xml or Maven/Gradle, navigate to:
```
ProjectFolder/test-output/index.html
```

Open this file in any web browser to view the report.

---

## What the Report Contains

| Section | Content |
|---------|---------|
| Summary | Total tests run, passed, failed, and skipped with percentages. |
| Test Classes | List of all classes that were executed. |
| Methods | Each test method with its status (green for pass, red for fail). |
| Execution Time | How long each test and the entire suite took. |
| Error Details | Stack traces and error messages for failed tests. |
| Groups | Which tests belong to which groups. |
| Reporter Output | Custom messages logged using Reporter.log(). |

---

## Types of Reports Generated

| Report File | Purpose |
|-------------|---------|
| index.html | Main dashboard with overall summary. |
| emailable-report.html | Compact report designed to be emailed to stakeholders. |
| testng-results.xml | Machine-readable XML format for CI/CD tools. |
| SuiteName.html | Individual report for each suite. |

---


## Quick Tips

- The `test-output` folder is overwritten on every run. Archive old reports if needed.
- The emailable-report.html is useful for sharing results with managers via email.
- For professional dashboards, combine TestNG with Extent Reports instead of relying solely on default HTML.
- Parallel execution reports still show individual test results clearly, making it easy to identify which thread failed.