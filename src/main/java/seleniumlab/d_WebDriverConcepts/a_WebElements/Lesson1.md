<div class="lesson-header">
<h1>WebElements</h1>
<a href="../WebElements.html" class="playground-button">
    Practice Playground →
</a>
</div>
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
