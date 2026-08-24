# Alert & Popup Handling in Selenium — Beginner Notes

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
<style>
.alert-playground {
    max-width: 650px;
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 8px;
}

.alert-group {
    margin-bottom: 15px;
}

.alert-button {
    padding: 10px 18px;
    margin-right: 8px;
    margin-bottom: 8px;
    border: 1px solid #999;
    border-radius: 5px;
    background: #eee;
    cursor: pointer;
}

.alert-button:hover {
    background: #ddd;
}

.alert-result {
    margin-top: 15px;
    font-weight: 500;
}
</style>

<div class="alert-playground">

    <h3>Alert Popup Playground</h3>

    <!-- Simple Alert -->
    <div class="alert-group">

        <button
            id="simpleAlert"
            type="button"
            class="alert-button">

            Simple Alert

        </button>

    </div>

    <!-- Confirmation Alert -->
    <div class="alert-group">

        <button
            id="confirmAlert"
            type="button"
            class="alert-button">

            Confirmation Alert

        </button>

    </div>

    <!-- Prompt Alert -->
    <div class="alert-group">

        <button
            id="promptAlert"
            type="button"
            class="alert-button">

            Prompt Alert

        </button>

    </div>

    <!-- Normal Button -->
    <div class="alert-group">

        <button
            id="normalButton"
            type="button"
            class="alert-button">

            Normal Button

        </button>

    </div>

    <p
        id="alertResult"
        class="alert-result">
    </p>
</div>

<script>

document.getElementById("simpleAlert").addEventListener("click", function () {

    alert("Registration completed successfully!");

});


document.getElementById("confirmAlert").addEventListener("click", function () {

    let result = confirm("Are you sure you want to continue?");

    const message =
        document.getElementById("alertResult");

    if (result) {

        message.textContent =
            "You clicked OK.";

    } else {

        message.textContent =
            "You clicked Cancel.";

    }

});


document.getElementById("promptAlert").addEventListener("click", function () {

    let name =
        prompt("Enter your name:");

    const message =
        document.getElementById("alertResult");

    if (name === null) {

        message.textContent =
            "Prompt was cancelled.";

    } else {

        message.textContent =
            "Hello, " + name + "!";

    }

});


document.getElementById("normalButton").addEventListener("click", function () {

    document.getElementById("alertResult").textContent =
        "This is a normal HTML button. No alert was created.";

});

</script>