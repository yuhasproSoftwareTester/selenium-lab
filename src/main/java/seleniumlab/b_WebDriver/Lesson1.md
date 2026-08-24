# WebDriver Notes 

## 1. WebDriver Introduction

- **WebDriver** is the **core component of Selenium** used to automate web applications.
- It is a **programming interface** (API) — not a tool with a UI. You write code to control the browser.
- It communicates with the browser **directly**, so it's **fast and reliable**.
- Supports many languages: **Java, Python, C#, Ruby, JavaScript**.
- Supports all major browsers: **Chrome, Firefox, Edge, Safari**.
- It behaves like a **real user** — clicking, typing, scrolling, etc.

**Basic example (Java):**
```java
WebDriver driver = new ChromeDriver();   // open Chrome
driver.get("https://www.google.com");    // open a website
driver.quit();                           // close browser
```

---

## 2. Methods in WebDriver (Common Ones)

| Method | What it does |
|---|---|
| `get(url)` | Opens a URL in the browser |
| `getTitle()` | Returns the **title** of the current page |
| `getCurrentUrl()` | Returns the **URL** of the current page |
| `getPageSource()` | Returns the **HTML source** of the page |
| `findElement(By...)` | Finds **one** element on the page |
| `findElements(By...)` | Finds **multiple** elements (returns a list) |
| `close()` | Closes the **current window/tab** only |
| `quit()` | Closes **all windows** and ends the session |
| `navigate().to(url)` | Opens a URL (similar to get, but keeps history) |
| `navigate().back()` | Goes back to the previous page |
| `navigate().forward()` | Goes forward |
| `navigate().refresh()` | Refreshes the page |
| `manage().window().maximize()` | Maximizes the browser window |
| `switchTo()` | Switches between frames, windows, alerts |

**WebElement methods** (after finding an element):

| Method | What it does |
|---|---|
| `click()` | Clicks a button/link |
| `sendKeys("text")` | Types text into a field |
| `clear()` | Clears a text field |
| `getText()` | Gets visible text of an element |
| `getAttribute("value")` | Gets an attribute value |
| `isDisplayed()` | Checks if element is visible |
| `isEnabled()` | Checks if element is enabled |
| `isSelected()` | Checks checkbox/radio selection |
| `submit()` | Submits a form |

---

## 3. WebDriver Commands

WebDriver commands are grouped into **4 categories**:

### a) Browser Commands 
Control the browser itself:
```java
driver.get("https://example.com");        // open page
driver.getTitle();                        // get title
driver.getCurrentUrl();                   // get current URL
driver.close();                           // close current tab
driver.quit();                            // close everything
driver.manage().window().maximize();      // maximize window
```

### b) Navigation Commands 
Move between pages like using browser buttons:
```java
driver.navigate().to("https://example.com");
driver.navigate().back();      // browser back button
driver.navigate().forward();   // browser forward button
driver.navigate().refresh();   // reload page
```
> **Difference:** `get()` waits for the page to fully load; `navigate().to()` doesn't necessarily wait and maintains browser history.

### c) Element Commands 
### d) Wait Commands 
---

## 4. Handling Different Browsers

Each browser needs its **own driver executable** that acts as a bridge between WebDriver and the browser:

| Browser | Driver | Class name |
|---|---|---|
| Chrome | ChromeDriver | `ChromeDriver` |
| Firefox | GeckoDriver | `FirefoxDriver` |
| Edge | EdgeDriver | `EdgeDriver` |
| Safari | safaridriver (built-in) | `SafariDriver` |

**Code for each browser (Java):**

```java
// CHROME
System.setProperty("webdriver.chrome.driver", "path/chromedriver.exe");
WebDriver driver = new ChromeDriver();

// FIREFOX
System.setProperty("webdriver.gecko.driver", "path/geckodriver.exe");
WebDriver driver = new FirefoxDriver();

// EDGE
System.setProperty("webdriver.edge.driver", "path/msedgedriver.exe");
WebDriver driver = new EdgeDriver();
```

> **Modern shortcut (Selenium 4.x / WebDriverManager):** no manual driver download needed —
> ```java
> WebDriverManager.chromedriver().setup();
> WebDriver driver = new ChromeDriver();
> ```

**Running the same test on any browser (cross-browser testing):**
```java
WebDriver driver;
String browser = "chrome";

if (browser.equals("chrome")) {
    driver = new ChromeDriver();
} else if (browser.equals("firefox")) {
    driver = new FirefoxDriver();
} else {
    driver = new EdgeDriver();
}
```
 Same script, different browser — this is called **cross-browser testing**, and combined with **Selenium Grid**, all browsers can run **in parallel**.
