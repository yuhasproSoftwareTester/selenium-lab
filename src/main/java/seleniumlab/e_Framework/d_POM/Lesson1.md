# Page Object Model (POM)

## What is POM

Page Object Model is a design pattern in Selenium where each web page of the application has a dedicated Java class. This class contains all the web elements (locators) and actions (methods) related to that page. Test scripts only use these page classes to perform actions and verify results.

The core idea is simple: if the login page changes, you update only one file (LoginPage.java) instead of updating every test that uses the login page.

---

## Why Use POM

| Reason | Explanation |
|--------|-------------|
| Code Reusability | The same page class is used by multiple test scripts. |
| Easy Maintenance | UI changes are fixed in one place, not scattered across tests. |
| Clean Test Scripts | Tests read like plain English: loginPage.login(user, pass). |
| Separation of Concerns | Page logic is separate from test logic. |
| Reduced Duplication | You do not write findElement code again and again in every test. |

---

## How It Works

1. Create one Java class for each web page (LoginPage, HomePage, CartPage).
2. Inside the class, declare all web elements as variables using locators.
3. Create methods that perform actions on those elements (type, click, select).
4. In the test script, create an object of the page class and call its methods.
5. If a locator changes, update only the page class.

---

## Simple Analogy

Think of a restaurant menu. The menu lists all available dishes with their descriptions. You order by name, and the kitchen handles the cooking. You do not need to know the recipe or ingredients. In POM, the page class is the menu, and the test script is the customer ordering from it.

---

## Pure Selenium Example

### LoginPage.java

```java
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class LoginPage {
    WebDriver driver;

    // Locators
    By usernameField = By.id("user-name");
    By passwordField = By.id("password");
    By loginButton = By.id("login-button");
    By errorMessage = By.cssSelector("[data-test='error']");

    // Constructor
    public LoginPage(WebDriver driver) {
        this.driver = driver;
    }

    // Actions
    public void enterUsername(String username) {
        driver.findElement(usernameField).clear();
        driver.findElement(usernameField).sendKeys(username);
    }

    public void enterPassword(String password) {
        driver.findElement(passwordField).clear();
        driver.findElement(passwordField).sendKeys(password);
    }

    public void clickLogin() {
        driver.findElement(loginButton).click();
    }

    public void login(String username, String password) {
        enterUsername(username);
        enterPassword(password);
        clickLogin();
    }

    public boolean isErrorDisplayed() {
        return driver.findElements(errorMessage).size() > 0;
    }
}
```

### InventoryPage.java

```java
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;

public class InventoryPage {
    WebDriver driver;

    By pageTitle = By.className("title");
    By menuButton = By.id("react-burger-menu-btn");

    public InventoryPage(WebDriver driver) {
        this.driver = driver;
    }

    public boolean isOnInventoryPage() {
        return driver.getCurrentUrl().contains("inventory");
    }

    public String getPageTitle() {
        return driver.findElement(pageTitle).getText();
    }
}
```

### Test Script

```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeDriver;

public class POMTest {
    public static void main(String[] args) {
        WebDriver driver = new ChromeDriver();
        driver.manage().window().maximize();

        try {
            driver.get("https://www.saucedemo.com/");

            // Use page objects
            LoginPage loginPage = new LoginPage(driver);
            loginPage.login("standard_user", "secret_sauce");

            InventoryPage inventoryPage = new InventoryPage(driver);

            if (inventoryPage.isOnInventoryPage()) {
                System.out.println("PASS: Login successful. Title: " + inventoryPage.getPageTitle());
            } else {
                System.out.println("FAIL: Login failed.");
            }

        } catch (Exception e) {
            System.out.println("ERROR: " + e.getMessage());
        } finally {
            driver.quit();
        }
    }
}
```

---

## Console Output

```
PASS: Login successful. Title: Products
```

---

## Comparison with Other Patterns

| Aspect | Data-Driven | Keyword-Driven | POM |
|--------|-------------|----------------|-----|
| What it solves | Multiple data sets | Multiple action sequences | UI maintenance and reuse |
| Where data lives | External files (Excel) | External files (keyword sheets) | Java classes (page objects) |
| Main benefit | Test many inputs | Non-coders can write tests | Clean, maintainable code |
| Best for | Forms with data variations | Complex workflows | Any project with multiple pages |

---

## When to Use POM

- The application has multiple pages or sections
- The same page is accessed by many test scripts
- UI elements change frequently
- The team wants clean and readable test code
- The project is medium to large in size

---

## When Not to Use It

- The application is a single page with only a few elements
- The project is a quick one-time script
- Adding extra classes feels like unnecessary overhead for the task

---

## Best Practices

- One class per page. If a page is very large, split it into sections.
- Page classes should contain actions, not assertions. Assertions belong in test scripts.
- Use meaningful method names like login, searchProduct, addToCart.
- Keep locators private or protected. Expose only methods to the test scripts.

---
