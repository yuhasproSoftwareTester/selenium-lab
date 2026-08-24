# WebElements

## 1. What is a WebElement?

- A **WebElement** is **anything you see on a web page** — textbox, button, link, checkbox, radio button, dropdown, image, table, etc.
- In Selenium, every element is represented as a **WebElement object**.
- Two steps always: **Find it** (locator) → **Act on it** (method).

```java
WebElement element = driver.findElement(By.id("username"));
element.sendKeys("admin");
```

---

## 2. Common WebElement Operations (Methods)

| Method | Purpose | Returns |
|---|---|---|
| `click()` | Click on element | — |
| `sendKeys("text")` | Type text into a field | — |
| `clear()` | Clear existing text | — |
| `getText()` | Get visible text | String |
| `getAttribute("value")` | Get attribute value (id, class, href…) | String |
| `getTagName()` | Get HTML tag name | String |
| `getSize()` | Height & width of element | Dimension |
| `getLocation()` | X,Y position on page | Point |
| `isDisplayed()` | Element visible on page? | true/false |
| `isEnabled()` | Element clickable/editable? | true/false |
| `isSelected()` | Checkbox/radio selected? | true/false |
| `submit()` | Submit a form | — |

>  `getText()` vs `getAttribute("value")`:
> - `getText()` → text **shown between tags** → `<button>Login</button>` gives "Login"
> - `getAttribute("value")` → text **typed inside a textbox** → `<input value="admin">`

---

## 3. Handling Each Type of WebElement

### Textbox / Text Field 
```java
WebElement box = driver.findElement(By.id("username"));
box.clear();                     // remove old text first
box.sendKeys("admin");           // type text
System.out.println(box.getAttribute("value"));   // read typed text
```

###  Button 
```java
driver.findElement(By.id("loginBtn")).click();

// check before clicking
WebElement btn = driver.findElement(By.id("loginBtn"));
if (btn.isDisplayed() && btn.isEnabled()) {
    btn.click();
}
```

###  Link 
```java
driver.findElement(By.linkText("Forgot Password?")).click();
// or partial text
driver.findElement(By.partialLinkText("Forgot")).click();

// get where the link points
String url = driver.findElement(By.linkText("Home")).getAttribute("href");
```

---

## 4. Verification Methods — isDisplayed / isEnabled / isSelected

These three are used for **validation** in tests:

| Method | Checks | Example use |
|---|---|---|
| `isDisplayed()` | Element **visible** on page? | Logo appears after login? |
| `isEnabled()` | Element **active/editable**? | Submit button enabled only after filling form? |
| `isSelected()` | Checkbox/radio/dropdown **chosen**? | "Agree to terms" checked? |

```java
WebElement logo = driver.findElement(By.id("logo"));
if (logo.isDisplayed()) {
    System.out.println("Login successful ");
}
```
<style>
.web-element-playground {
    max-width: 650px;
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 8px;
}

.practice-field {
    margin-bottom: 15px;
}

.practice-field label {
    display: block;
    margin-bottom: 5px;
    font-weight: 500;
}

.text-box,
.text-area,
.number-box,
.date-box,
.select-box {
    padding: 8px;
    border: 1px solid #999;
    border-radius: 5px;
}

.text-box,
.text-area {
    width: 300px;
}

.text-area {
    height: 80px;
}

.practice-button {
    padding: 10px 20px;
    border: 1px solid #999;
    border-radius: 5px;
    background: #eee;
    cursor: pointer;
}

.practice-button:hover {
    background: #ddd;
}

.practice-link {
    display: inline-block;
    margin-top: 10px;
}

.practice-group {
    margin-bottom: 15px;
}

.practice-image {
    width: 150px;
}
</style>
        
<div class="web-element-playground">
    <h3>WebElements Playground</h3>
    <!-- Text Box -->
    <div class="practice-field">
        <label>First Name</label>
        <input
            id="firstName"
            name="firstName"
            type="text"
            class="text-box"
            placeholder="Enter first name">
    </div>
    <!-- Password -->
    <div class="practice-field">
        <label>Password</label>
        <input
            id="password"
            name="password"
            type="password"
            class="text-box"
            placeholder="Enter password">
    </div>
    <!-- Textarea -->
    <div class="practice-field">
        <label>Comments</label>
        <textarea
            id="comments"
            name="comments"
            class="text-area"
            placeholder="Enter your comments"></textarea>
    </div>
    <!-- Number -->
    <div class="practice-field">
        <label>Age</label>
        <input
            id="age"
            name="age"
            type="number"
            class="number-box"
            min="1"
            max="100"
            value="25">
    </div>
    <!-- Date -->
    <div class="practice-field">
        <label>Date of Birth</label>
        <input
            id="dob"
            name="dob"
            type="date"
            class="date-box">
    </div>
    <!-- File -->
    <div class="practice-field">
        <label>Upload File</label>
        <input
            id="document"
            name="document"
            type="file">
    </div>
    <!-- Button -->
    <div class="practice-field">
        <button
            id="submitButton"
            name="submit"
            type="button"
            class="practice-button">
            Submit
        </button>
        <p id="successMessage" style="display:none;">Form submitted successfully!</p>
    </div>
    <!-- Disabled Button -->
    <div class="practice-field">
        <button
            id="disabledButton"
            type="button"
            class="practice-button"
            disabled>
            Disabled Button
        </button>
    </div>
    <!-- Link -->
    <div class="practice-field">
        <a
            id="seleniumLink"
            href="https://www.selenium.dev/"
            target="_blank"
            class="practice-link">
            Visit Selenium Website
        </a>
    </div>
    <!-- Image -->
    <div class="practice-field">
        <img
            id="practiceImage"
            class="practice-image"
            src="https://www.selenium.dev/images/selenium_logo_square_green.svg"
            alt="Selenium Logo">
    </div>
    <!-- Text -->
    <h3 id="practiceHeading">
        Practice Heading
    </h3>
    <p id="practiceText">
        This is sample text for practicing getText().
    </p>

</div>
<script>
    document.getElementById("submitButton").addEventListener("click", function () {
        document.getElementById("successMessage").style.display = "block";
    });
</script>