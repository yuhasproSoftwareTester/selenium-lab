 
<div class="lesson-header">
<h1>Radio Button Handling in Selenium</h1>
<a href="../radiobutton.html" class="playground-button">
    Practice Playground →
</a>
</div>
## 1. What is a Radio Button?

- A **radio button** is a small **round circle**  that lets the user select **only ONE option** from a group.
- Used for: Gender (Male/Female), Payment mode (Card/UPI/Cash), Yes/No questions.
- **Key point:** Selecting one option **automatically deselects** the others in the same group. A selected radio **cannot be unselected** by clicking it again.

**HTML of radio buttons:**
```html
<input type="radio" name="gender" value="male" id="male"> Male
<input type="radio" name="gender" value="female" id="female"> Female
```
> All radio buttons in a group share the **same `name` attribute** (`name="gender"`) — that's what links them together as one group.

---

## 2. Methods Used with Radio Buttons

| Method | Purpose |
|---|---|
| `click()` | Select the radio button |
| `isSelected()` | Returns `true` if selected, `false` if not |
| `isDisplayed()` | Is it visible on the page? |
| `isEnabled()` | Is it clickable (not greyed out)? |

>  Same as checkbox — there is **NO `select()` method**, only `click()`.

---

## 3. Select a Radio Button 

```java
WebElement male = driver.findElement(By.id("male"));

if (!male.isSelected()) {
    male.click();      // select only if not already selected
}
```

>  Safe practice: check `isDisplayed()` and `isEnabled()` before clicking:
```java
WebElement male = driver.findElement(By.id("male"));

if (male.isDisplayed() && male.isEnabled() && !male.isSelected()) {
    male.click();
}
```

---

## 4. Verify Which Option is Selected 

**Scenario:** Check which gender is selected on the form:

```java
WebElement male   = driver.findElement(By.id("male"));
WebElement female = driver.findElement(By.id("female"));

if (male.isSelected()) {
    System.out.println("Male is selected");
} else if (female.isSelected()) {
    System.out.println("Female is selected");
} else {
    System.out.println("Nothing selected");
}
```

**Verify selection after clicking (test validation):**
```java
WebElement female = driver.findElement(By.id("female"));
female.click();

if (female.isSelected()) {
    System.out.println("Radio selected — Test PASSED ✔");
} else {
    System.out.println("Radio NOT selected — Test FAILED ✘");
}
```

---
## 5. Common Mistakes & Tips 

| Mistake | Fix |
|---|---|
| Using `findElement` when you need the whole group | Use `findElements(By.name("..."))` to get the group |
| Expecting `click()` to unselect a radio | Radios can't be unselected — only switch options |
| Clicking without checking state | Use `isSelected()` first |
| `ElementNotInteractableException` | Radio hidden behind a styled label → click the **label**: `driver.findElement(By.xpath("//label[@for='male']")).click();` |
| Radio inside a **frame** | Switch first: `driver.switchTo().frame(0);` |

