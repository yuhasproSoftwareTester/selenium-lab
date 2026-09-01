# TestNG Parameters

## What are Parameters

Parameters in TestNG are a way to pass values from outside the code into your test methods. Instead of hardcoding values like URLs, usernames, or browser names inside your Java class, you define them in the `testng.xml` file. TestNG reads these values and injects them into your test at runtime.

---

## Why Use Parameters

| Reason | Explanation |
|--------|-------------|
| No Hardcoding | Change values in XML without touching Java code. |
| Environment Flexibility | Use different XML files for dev, staging, and production. |
| Reusability | Same test class runs with different inputs by changing XML. |
| Clean Code | Test logic stays in Java. Configuration stays in XML. |

---

## How It Works

1. Define parameters in `testng.xml` using `<parameter name="key" value="value"/>`.
2. Use `@Parameters` annotation on the test method.
3. The method accepts arguments matching the parameter names.
4. TestNG automatically passes the values from XML to the method.

---

## Code Example

### Java Test Class

```java
import org.testng.annotations.Parameters;
import org.testng.annotations.Test;

public class ParameterDemo {

    @Test
    @Parameters({"browser", "url"})
    public void openWebsite(String browser, String url) {
        System.out.println("Browser: " + browser);
        System.out.println("URL: " + url);
    }
}
```

### testng.xml

```xml
<!DOCTYPE suite SYSTEM "https://testng.org/testng-1.0.dtd">
<suite name="ParameterSuite">
    <parameter name="browser" value="chrome"/>
    <parameter name="url" value="https://www.example.com"/>

    <test name="ParameterTest">
        <classes>
            <class name="ParameterDemo"/>
        </classes>
    </test>
</suite>
```

---

## Output

```
Browser: chrome
URL: https://www.example.com
```

---

## Suite-Level vs Test-Level Parameters

**Suite-level**: Defined inside `<suite>`. Available to all tests in the suite.

```xml
<suite name="Suite">
    <parameter name="env" value="production"/>
    ...
</suite>
```

**Test-level**: Defined inside `<test>`. Overrides suite-level if the same name is used.

```xml
<test name="DevTest">
    <parameter name="env" value="development"/>
    ...
</test>
```

---

## Parameters with @BeforeMethod

You can also use parameters in setup methods.

```java
@BeforeMethod
@Parameters("browser")
public void setUp(String browser) {
    System.out.println("Launching: " + browser);
}
```

---

## Quick Comparison

| Feature | @Parameters | @DataProvider |
|---------|-------------|---------------|
| Source | testng.xml | Java method |
| Data type | Single values | Multiple rows and columns |
| Best for | Environment config, single values | Multiple test data sets |
| Complexity | Simple | More flexible |
---
Use `@Parameters` for configuration values like URLs, browser names, or environment flags. Use `@DataProvider` when you need to run the same test with multiple rows of data like different login credentials.