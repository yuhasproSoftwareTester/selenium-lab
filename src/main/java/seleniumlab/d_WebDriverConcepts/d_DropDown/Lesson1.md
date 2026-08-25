<div class="lesson-header">
<h1>DropDown Handling in Selenium</h1>
<a href="../dropdown.html" class="playground-button">
    Practice Playground →
</a>
</div>
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

