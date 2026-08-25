<div class="lesson-header">
<h1>Alert & Popup Handling in Selenium</h1>
<a href="../alertpop.html" class="playground-button">
    Practice Playground →
</a>
</div>
## 1. What is an Alert?

- An **alert** is a small **popup message box** shown by the browser (via JavaScript) to warn, confirm, or ask the user for input.
- **Key problem:** While an alert is open, Selenium **cannot touch the main page** — any click/type gives `UnhandledAlertException`. You must **handle the alert first**.
- Alerts are **NOT HTML elements** — you can't inspect them or use locators. That's why we use the special **`Alert` interface** with `switchTo()`.

---

## 2. Three Types of Alerts 

| Type | Buttons | Purpose | Example |
|---|---|---|---|
| **Simple Alert** | OK only | Just shows a message | "Login successful!" |
| **Confirmation Alert** | OK + Cancel | Ask user to confirm | "Are you sure you want to delete?" |
| **Prompt Alert** | Textbox + OK + Cancel | Ask user for input | "Enter your name:" |

**How they look in JavaScript (HTML):**
```javascript
alert("Welcome!");                 // simple alert
confirm("Are you sure?");          // confirmation alert
prompt("Enter your name:");        // prompt alert
```

---

## 3. Alert Interface — Methods 

First switch to the alert:
```java
import org.openqa.selenium.Alert;

Alert alert = driver.switchTo().alert();
```

| Method | Purpose |
|---|---|
| `alert.getText()` | Read the alert **message** |
| `alert.accept()` | Click **OK**  |
| `alert.dismiss()` | Click **Cancel**  / close the alert |
| `alert.sendKeys("text")` | **Type** into a prompt alert |

---

## 4. Waiting for an Alert 

Alerts sometimes appear after a delay — clicking `switchTo().alert()` too early gives `NoAlertPresentException`. Wait for it:

```java
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));

Alert alert = wait.until(ExpectedConditions.alertIsPresent());
alert.accept();
```
