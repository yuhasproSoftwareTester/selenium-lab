# Keyword-Driven Framework

## What is Keyword-Driven Framework

A Keyword-Driven framework is a test automation approach where test steps are defined as keywords (actions) in an external source. Each keyword represents a specific action like open, type, click, or verify. A central engine reads these keywords one by one and executes the corresponding method.

The test script does not contain hardcoded steps. Instead, it contains a list of keywords that tell the framework what to do. The actual implementation of each keyword is written separately in reusable methods.

---

## Why Use Keyword-Driven Framework

| Reason | Explanation |
|--------|-------------|
| No Coding Required for Tests | Testers can write test cases using simple keywords without knowing Java. |
| High Reusability | One keyword like "TYPE" or "CLICK" is written once and reused across all tests. |
| Easy Maintenance | If a locator changes, you update only the keyword method, not every test. |
| Readable Test Cases | A test case looks like a plain list of actions: OPEN, TYPE, CLICK, VERIFY. |
| Separation of Logic and Flow | The engine handles how to do things. The keyword sheet handles what to do. |

---

## How It Works

1. Create a library of reusable keywords (OPEN, TYPE, CLICK, VERIFY, CLOSE).
2. Store test cases as a sequence of keywords in a table or file.
3. The engine reads each row: keyword, locator, and value.
4. Based on the keyword, the engine calls the matching method.
5. The method performs the actual Selenium action.

---

## Simple Analogy

Think of a remote control. The buttons are keywords: Power, Volume Up, Channel Down. You press a button and the TV knows what to do. You do not need to understand the circuitry inside the TV. In the same way, a tester writes "CLICK login-button" without writing the actual Selenium click code.

---

## Pure Selenium Example

```java
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class KeywordDrivenLogin {

    WebDriver driver;

    public void execute(String keyword, String locator, String value) {
        switch (keyword) {
            case "OPEN":
                driver = new ChromeDriver();
                driver.manage().window().maximize();
                driver.get(value);
                System.out.println("Opened: " + value);
                break;

            case "TYPE":
                driver.findElement(By.id(locator)).clear();
                driver.findElement(By.id(locator)).sendKeys(value);
                System.out.println("Typed '" + value + "' into " + locator);
                break;

            case "CLICK":
                driver.findElement(By.id(locator)).click();
                System.out.println("Clicked: " + locator);
                break;

            case "VERIFY":
                boolean present = driver.findElements(By.id(locator)).size() > 0;
                System.out.println("Verify " + locator + ": " + present);
                break;

            case "CLOSE":
                driver.quit();
                System.out.println("Browser closed.");
                break;

            default:
                System.out.println("Unknown keyword: " + keyword);
        }
    }

    public static void main(String[] args) {
        KeywordDrivenLogin engine = new KeywordDrivenLogin();

        String[][] testSteps = {
            {"OPEN", "", "https://www.saucedemo.com/"},
            {"TYPE", "user-name", "standard_user"},
            {"TYPE", "password", "secret_sauce"},
            {"CLICK", "login-button", ""},
            {"VERIFY", "inventory_container", ""},
            {"CLOSE", "", ""}
        };

        for (String[] step : testSteps) {
            engine.execute(step[0], step[1], step[2]);
        }
    }
}
```

---

## Console Output

```
Opened: https://www.saucedemo.com/
Typed 'standard_user' into user-name
Typed 'secret_sauce' into password
Clicked: login-button
Verify inventory_container: true
Browser closed.
```

---

## Extending to Excel

In real projects, the `testSteps` array is replaced by rows from an Excel file:

| Keyword | Locator | Value |
|---------|---------|-------|
| OPEN | | https://www.saucedemo.com/ |
| TYPE | user-name | standard_user |
| TYPE | password | secret_sauce |
| CLICK | login-button | |
| CLOSE | | |

Using Apache POI, you read each row and pass it to the `execute` method. Testers can add new test cases by adding rows to the Excel sheet without changing any Java code.

---

## Data-Driven vs Keyword-Driven

| Aspect | Data-Driven | Keyword-Driven |
|--------|-------------|----------------|
| What changes | Input data (username, password) | Actions (type, click, verify) |
| Focus | Multiple sets of data for same test | Multiple sequences of actions |
| Test case look | Same steps, different values | Different steps, different actions |
| Who writes tests | Programmer or tester | Non-programmer can write keyword sheets |
| Best for | Forms with many data combinations | Workflows with varying steps |

---

## When to Use Keyword-Driven

- Test cases have different flows and steps
- Manual testers need to create automation without coding
- The application has many reusable actions across different features
- You want test cases to be readable as plain English steps

---

## When Not to Use It

- The application is small with only a few simple tests
- The team has strong programming skills and prefers direct coding
- Overhead of maintaining keyword sheets is not justified for the project size

---