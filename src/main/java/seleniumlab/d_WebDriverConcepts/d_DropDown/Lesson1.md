# DropDown Handling in Selenium

## 1. What is a DropDown?

- A **dropdown** is a list that shows options when clicked — user picks **one** (or sometimes **multiple**) options.
- Used for: Country selection, Date of Birth (Day/Month/Year), City, Category.
- **Key point:** In HTML there are **two types** of dropdowns, and they are handled **differently**:

| Type | HTML | How to handle |
|---|---|---|
| **Standard dropdown** | `<select>` + `<option>` tags | Use the **Select class**  |
| **Custom dropdown** (Bootstrap etc.) | `<div>`, `<ul>`, `<li>` tags | Click like normal elements  Select class won't work |

**HTML of a standard dropdown:**
```html
<select id="country" name="country">
  <option value="IN">India</option>
  <option value="US">USA</option>
  <option value="UK">UK</option>
</select>
```

---

## 2. The Select Class (For `<select>` Dropdowns)

**Import and create object:**
```java
import org.openqa.selenium.support.ui.Select;

WebElement drop = driver.findElement(By.id("country"));
Select sel = new Select(drop);      // pass the WebElement into Select
```

>  The Select class works **only** if the element is a `<select>` tag. Otherwise you get: `UnexpectedTagNameException`.

---

## 3. Three Ways to Select an Option 

```java
Select sel = new Select(driver.findElement(By.id("country")));

sel.selectByVisibleText("India");   // ① by text the user SEES
sel.selectByValue("IN");            // ② by the value attribute
sel.selectByIndex(2);               // ③ by position (starts from 0!)
```

| Method | Based on | Example |
|---|---|---|
| `selectByVisibleText()` | Text shown on page | `"India"` |
| `selectByValue()` | `value` attribute in HTML | `"IN"` |
| `selectByIndex()` | Position number | `0` = first option |

> 💡 Prefer `selectByVisibleText()` or `selectByValue()` — **index is risky** because option order can change.

---

## 4. Multi-Select DropDown 

Some dropdowns allow selecting **many options** (with Ctrl+click). HTML has `multiple` attribute:
```html
<select id="skills" multiple>
```

**Selecting multiple options:**
```java
Select sel = new Select(driver.findElement(By.id("skills")));

System.out.println(sel.isMultiple());     // true

sel.selectByVisibleText("Java");
sel.selectByVisibleText("Python");
sel.selectByIndex(3);
```

**Deselecting (only works for multi-select):**
```java
sel.deselectByVisibleText("Java");
sel.deselectByIndex(3);
sel.deselectByValue("py");
sel.deselectAll();                       // remove all selections
```

**Get all SELECTED options:**
```java
List<WebElement> chosen = sel.getAllSelectedOptions();
for (WebElement c : chosen) {
    System.out.println(c.getText());
}
```

>  `deselect` methods throw an error on a **single-select** dropdown — check `isMultiple()` first.

<style>
.dropdown-playground {
    max-width: 650px;
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 8px;
}

.dropdown-group {
    margin-bottom: 20px;
}

.dropdown-group label {
    display: block;
    margin-bottom: 6px;
    font-weight: 500;
}

.practice-select {
    padding: 8px;
    min-width: 220px;
    border: 1px solid #999;
    border-radius: 5px;
    background: #eee;
}

.dropdown-button {
    padding: 9px 18px;
    border: 1px solid #999;
    border-radius: 5px;
    background: #eee;
    cursor: pointer;
}

.dropdown-button:hover {
    background: #ddd;
}

.dropdown-message {
    margin-top: 12px;
    font-weight: 500;
}
</style>

<div class="dropdown-playground">
    <h3>Dropdown Playground</h3>
    <!-- Country -->
    <div class="dropdown-group">
        <label for="country">
            Country
        </label>
        <select
            id="country"
            name="country"
            class="practice-select">
            <option value="">
                Select Country
            </option>
            <option value="india">
                India
            </option>
            <option value="usa">
                USA
            </option>
            <option value="uk">
                United Kingdom
            </option>
            <option value="canada">
                Canada
            </option>
            <option value="australia">
                Australia
            </option>
        </select>
    </div>
    <!-- Pre-selected -->
    <div class="dropdown-group">
        <label for="browser">
            Browser
        </label>
        <select
            id="browser"
            name="browser"
            class="practice-select">
            <option value="chrome" selected>
                Chrome
            </option>
            <option value="firefox">
                Firefox
            </option>
            <option value="edge">
                Edge
            </option>
            <option value="safari">
                Safari
            </option>
        </select>
    </div>
    <!-- Disabled -->
    <div class="dropdown-group">
        <label for="accountType">
            Account Type
        </label>
        <select
            id="accountType"
            name="accountType"
            class="practice-select"
            disabled>
            <option value="free">
                Free
            </option>
            <option value="premium">
                Premium
            </option>
        </select>
    </div>
    <!-- Multi Select -->
    <div class="dropdown-group">
        <label for="skills">
            Skills
        </label>
        <select
            id="skills"
            name="skills"
            class="practice-select"
            multiple
            size="4">
            <option value="java">
                Java
            </option>
            <option value="selenium">
                Selenium
            </option>
            <option value="testng">
                TestNG
            </option>
            <option value="sql">
                SQL
            </option>
            <option value="api">
                API Testing
            </option>
        </select>
    </div>
    <!-- Button -->
    <div class="dropdown-group">
        <button
            id="checkDropdown"
            type="button"
            class="dropdown-button">
            Check Selection
        </button>
        <p
            id="dropdownMessage"
            class="dropdown-message"
            style="display:none;">
        </p>
    </div>
</div>
<script>
document.getElementById("checkDropdown").addEventListener("click", function () {
    const country =
        document.getElementById("country");
    const browser =
        document.getElementById("browser");
    const skills =
        document.getElementById("skills");
    const message =
        document.getElementById("dropdownMessage");
    let selectedSkills = [];
    for (let option of skills.selectedOptions) {
        selectedSkills.push(option.text);
    }
    message.innerHTML =
        "Country: " + country.options[country.selectedIndex].text +
        " | Browser: " + browser.options[browser.selectedIndex].text +
        " | Skills: " +
        (selectedSkills.length > 0
            ? selectedSkills.join(", ")
            : "None");
    message.style.display = "block";
});
</script>