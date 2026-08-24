# TestNG Listeners

## What are Listeners

Listeners in TestNG are classes that monitor the test execution process. They listen to events like when a test starts, passes, fails, or skips. Based on these events, they perform custom actions automatically without changing your test code.

Think of them as security cameras in a building. They watch everything happening and record or alert when something important occurs. You do not tell the camera what to do for each person. It just watches and reacts.

---

## Why Use Listeners

| Reason | Explanation |
|--------|-------------|
| Custom Logging | Write your own logs before or after each test. |
| Screenshot on Failure | Automatically capture a screenshot when a test fails. |
| Custom Reports | Generate your own report format beyond the default HTML. |
| Retry Failed Tests | Automatically rerun failed tests a set number of times. |
| Send Notifications | Email or Slack alerts when tests finish or fail. |
| Track Execution Time | Measure how long each test takes and flag slow ones. |

---


## Simple Example: ITestListener

This listener prints a message and takes action when a test fails.

### Listener Class

```java
import org.testng.ITestListener;
import org.testng.ITestResult;

public class TestListener implements ITestListener {

    @Override
    public void onTestStart(ITestResult result) {
        System.out.println("Test Started: " + result.getName());
    }

    @Override
    public void onTestSuccess(ITestResult result) {
        System.out.println("Test Passed: " + result.getName());
    }

    @Override
    public void onTestFailure(ITestResult result) {
        System.out.println("Test Failed: " + result.getName());
        // Here you can add code to take a screenshot
    }

    @Override
    public void onTestSkipped(ITestResult result) {
        System.out.println("Test Skipped: " + result.getName());
    }
}
```

### Test Class

```java
import org.testng.Assert;
import org.testng.annotations.Test;

public class DemoTest {

    @Test
    public void testPass() {
        System.out.println("Running testPass");
        Assert.assertTrue(true);
    }

    @Test
    public void testFail() {
        System.out.println("Running testFail");
        Assert.assertTrue(false);
    }

    @Test(dependsOnMethods = "testFail")
    public void testSkip() {
        System.out.println("Running testSkip");
    }
}
```

---

## How to Attach the Listener

### Method 1: Using @Listeners Annotation

Add this above your test class:

```java
import org.testng.annotations.Listeners;

@Listeners(TestListener.class)
public class DemoTest {
    // your tests
}
```

### Method 2: Using testng.xml (Recommended)

```xml
<!DOCTYPE suite SYSTEM "https://testng.org/testng-1.0.dtd">
<suite name="ListenerSuite">
    <listeners>
        <listener class-name="TestListener"/>
    </listeners>

    <test name="DemoTest">
        <classes>
            <class name="DemoTest"/>
        </classes>
    </test>
</suite>
```

Using XML is better because one listener applies to all classes in the suite without editing each file.

---

## Output

```
Test Started: testPass
Running testPass
Test Passed: testPass
Test Started: testFail
Running testFail
Test Failed: testFail
Test Skipped: testSkip
```

---

## Real-World Use: Retry Failed Tests

A common listener pattern is to automatically retry failed tests.

```java
import org.testng.IRetryAnalyzer;
import org.testng.ITestResult;

public class RetryAnalyzer implements IRetryAnalyzer {
    int counter = 0;
    int retryLimit = 2;

    @Override
    public boolean retry(ITestResult result) {
        if (counter < retryLimit) {
            counter++;
            System.out.println("Retrying " + result.getName() + " - Attempt " + counter);
            return true; // retry the test
        }
        return false; // stop retrying
    }
}
```

Attach it to any test:

```java
@Test(retryAnalyzer = RetryAnalyzer.class)
public void flakyTest() {
    // test that sometimes fails due to timing
}
```

If the test fails, it automatically runs again up to 2 more times.

---

## Tips

- Listeners run automatically. You do not call them directly.
- One listener class can handle events for the entire test suite.
- Use `ITestResult` to get the test name, status, and execution time.
- Listeners are the backbone of custom reporting tools like Extent Reports.
