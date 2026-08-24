# Hybrid Framework

## What is Hybrid Framework

A Hybrid framework is a combination of multiple frameworks. It merges the best features of Page Object Model (POM), Data-Driven, and Keyword-Driven approaches into one structure.

In a Hybrid setup:
- **POM** handles the web elements and page actions in dedicated classes.
- **Keyword-Driven** handles the test flow using action keywords in external files.
- **Data-Driven** feeds multiple sets of test data from external sources like Excel.

The result is a system where testers can write test cases using keywords and data in Excel, while the underlying code uses page objects to perform the actual work.

---

## Why Use Hybrid Framework

| Reason | Explanation |
|--------|-------------|
| Maximum Reusability | Page classes, keywords, and data are all reusable across projects. |
| Non-technical Friendly | Testers write test cases in Excel using keywords without touching Java code. |
| Easy Maintenance | UI changes are fixed in page classes. Flow changes are fixed in keyword sheets. Data changes are fixed in data sheets. |
| Scalable | Supports hundreds of test cases with minimal code growth. |
| Clean Architecture | Each layer has a single responsibility: pages handle locators, engine handles logic, sheets handle flow and data. |

---

## How It Works

1. **Page Layer**: Java classes store locators and actions for each web page (POM).
2. **Keyword Layer**: An engine reads keywords like OPEN, TYPE, CLICK, VERIFY and calls matching methods.
3. **Data Layer**: External files provide input values and expected results for each test case.
4. **Test Layer**: The main script or runner reads the keyword and data sheets, then executes them using the page layer.

---

## Simple Analogy

Think of a factory assembly line. The machines (page classes) perform specific tasks. The instruction manual (keyword sheet) tells the operator which machine to use and in what order. The parts list (data sheet) tells what raw material to feed into each machine. The operator (engine) simply follows the manual. If you want to build a different product, you change the manual and parts list, not the machines.

---

## Pure Selenium Example

This example combines POM, Keyword-Driven, and Data-Driven concepts. It runs two login test cases with different credentials using the same keyword sequence.

```java
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class HybridFramework {

    // 1. PAGE LAYER (POM)
    static class LoginPage {
        WebDriver driver;
        By usernameField = By.id("user-name");
        By passwordField = By.id("password");
        By loginButton = By.id("login-button");

        public LoginPage(WebDriver driver) {
            this.driver = driver;
        }

        public void open(String url) {
            driver.get(url);
        }

        public void typeUsername(String user) {
            driver.findElement(usernameField).clear();
            driver.findElement(usernameField).sendKeys(user);
        }

        public void typePassword(String pass) {
            driver.findElement(passwordField).clear();
            driver.findElement(passwordField).sendKeys(pass);
        }

        public void clickLogin() {
            driver.findElement(loginButton).click();
        }

        public boolean isLoggedIn() {
            return driver.getCurrentUrl().contains("inventory");
        }
    }

    // 2. KEYWORD ENGINE
    static class Engine {
        WebDriver driver;
        LoginPage loginPage;

        public Engine() {
            driver = new ChromeDriver();
            driver.manage().window().maximize();
            loginPage = new LoginPage(driver);
        }

        public void execute(String keyword, String value) {
            switch (keyword) {
                case "OPEN":
                    loginPage.open(value);
                    System.out.println("Opened: " + value);
                    break;
                case "USER":
                    loginPage.typeUsername(value);
                    System.out.println("Entered username: " + value);
                    break;
                case "PASS":
                    loginPage.typePassword(value);
                    System.out.println("Entered password");
                    break;
                case "CLICK":
                    loginPage.clickLogin();
                    System.out.println("Clicked login");
                    break;
                case "VERIFY":
                    boolean result = loginPage.isLoggedIn();
                    System.out.println("Login result: " + result);
                    break;
                case "CLOSE":
                    driver.quit();
                    System.out.println("Browser closed");
                    break;
                default:
                    System.out.println("Unknown keyword: " + keyword);
            }
        }
    }

    // 3. TEST LAYER (Data-Driven + Keyword-Driven)
    public static void main(String[] args) throws Exception {
        // Multiple test cases with different data
        String[][][] testCases = {
            {   // Test Case 1: Valid login
                {"OPEN", "https://www.saucedemo.com/"},
                {"USER", "standard_user"},
                {"PASS", "secret_sauce"},
                {"CLICK", ""},
                {"VERIFY", ""},
                {"CLOSE", ""}
            },
            {   // Test Case 2: Invalid login
                {"OPEN", "https://www.saucedemo.com/"},
                {"USER", "wrong_user"},
                {"PASS", "wrong_pass"},
                {"CLICK", ""},
                {"VERIFY", ""},
                {"CLOSE", ""}
            }
        };

        for (int i = 0; i < testCases.length; i++) {
            System.out.println("=== Running Test Case " + (i + 1) + " ===");
            Engine engine = new Engine();

            for (String[] step : testCases[i]) {
                engine.execute(step[0], step[1]);
                Thread.sleep(800);
            }
            System.out.println();
        }
    }
}
```

---

## Console Output

```
=== Running Test Case 1 ===
Opened: https://www.saucedemo.com/
Entered username: standard_user
Entered password
Clicked login
Login result: true
Browser closed

=== Running Test Case 2 ===
Opened: https://www.saucedemo.com/
Entered username: wrong_user
Entered password
Clicked login
Login result: false
Browser closed
```

---

## Real Project Structure

In a real project, the 3D array is replaced by Excel sheets:

| Sheet 1: Keywords (Flow) | | |
|--------------------------|---|---|
| Step | Keyword | Value |
| 1 | OPEN | https://www.saucedemo.com/ |
| 2 | USER | {data:username} |
| 3 | PASS | {data:password} |
| 4 | CLICK | |
| 5 | VERIFY | |
| 6 | CLOSE | |

| Sheet 2: Data (Test Cases) | | |
|----------------------------|---|---|
| TestCase | username | password |
| TC_001 | standard_user | secret_sauce |
| TC_002 | locked_out_user | secret_sauce |
| TC_003 | wrong_user | wrong_pass |

The engine reads the keyword sheet to know what to do, and the data sheet to know what values to use. This is the true power of a Hybrid framework.

---

## Comparison of All Frameworks

| Framework | Core Idea | External Files | Best For |
|-----------|-----------|----------------|----------|
| POM | One class per page | None | Code organization and maintenance |
| Data-Driven | Same test, different data | Excel/CSV with data | Testing forms with many inputs |
| Keyword-Driven | Same engine, different steps | Excel with keywords | Non-coders writing test flows |
| Hybrid | POM + Keywords + Data | Excel with both keywords and data | Large enterprise projects |

---

## When to Use Hybrid

- The project has many web pages and complex test flows
- Multiple testers need to write cases, including manual testers
- Test data and test steps change frequently
- The team wants a single framework that handles everything
- You need to generate detailed reports for hundreds of test cases

---

## When Not to Use It

- The project is small with less than 10 test cases
- The team has no experience with framework design
- Setting up Excel readers and keyword engines feels like overkill for the task
- Quick one-time automation scripts are needed

---

## Best Practices

- Keep page classes independent. They should not know about keywords or Excel.
- The engine should only route keywords to page methods. It should not contain locators.
- Use separate Excel sheets for keywords and data. Do not mix them in one sheet.
- Always use `try-finally` or proper cleanup to close browsers, even if a keyword fails.
- Name keywords in plain English: TYPE, CLICK, SELECT, VERIFY, WAIT.

---
