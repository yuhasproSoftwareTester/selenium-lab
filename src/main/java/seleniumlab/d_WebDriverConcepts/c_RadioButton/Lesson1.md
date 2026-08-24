# Radio Button Handling in Selenium 

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

<style>
.radio-playground {
    max-width: 650px;
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 8px;
}

.radio-group {
    margin-bottom: 20px;
}

.radio-group label {
    margin-left: 6px;
    margin-right: 15px;
}

.radio-button {
    padding: 9px 18px;
    border: 1px solid #999;
    border-radius: 5px;
    background: #eee;
    cursor: pointer;
}

.radio-button:hover {
    background: #ddd;
}

.radio-message {
    margin-top: 12px;
    font-weight: 500;
}
</style>

<div class="radio-playground">
    <h3>Radio Button Playground</h3>
    <!-- Gender -->
    <div class="radio-group">
        <strong>Gender</strong><br>
        <input
            id="male"
            name="gender"
            type="radio"
            value="Male">
        <label for="male">Male</label>
        <input
            id="female"
            name="gender"
            type="radio"
            value="Female">
        <label for="female">Female</label>
        <input
            id="other"
            name="gender"
            type="radio"
            value="Other">
        <label for="other">Other</label>
    </div>
    <!-- Payment -->
    <div class="radio-group">
        <strong>Payment Method</strong><br>
        <input
            id="card"
            name="payment"
            type="radio"
            value="Card">
        <label for="card">Card</label>
        <input
            id="upi"
            name="payment"
            type="radio"
            value="UPI">
        <label for="upi">UPI</label>
        <input
            id="cash"
            name="payment"
            type="radio"
            value="Cash">
        <label for="cash">Cash</label>
    </div>
    <!-- Pre-selected -->
    <div class="radio-group">
        <strong>Experience Level</strong><br>
        <input
            id="beginner"
            name="experience"
            type="radio"
            value="Beginner"
            checked>
        <label for="beginner">Beginner</label>
        <input
            id="intermediate"
            name="experience"
            type="radio"
            value="Intermediate">
        <label for="intermediate">Intermediate</label>
        <input
            id="advanced"
            name="experience"
            type="radio"
            value="Advanced">
        <label for="advanced">Advanced</label>
    </div>
    <!-- Disabled -->
    <div class="radio-group">
        <strong>Account Type</strong><br>
        <input
            id="free"
            name="account"
            type="radio"
            value="Free">
        <label for="free">Free</label>
        <input
            id="premium"
            name="account"
            type="radio"
            value="Premium"
            disabled>
        <label for="premium">Premium (Disabled)</label>
    </div>
    <div>
        <strong>Are you having fun??</strong><br>
        <input id="yes" name="question" type="radio" value="Yes"><label for="yes">Yes</label>
        <input id="no" name="question1" type="radio" value="No"><label for="no">NO</label>
    </div>
    <!-- Button -->
    <div class="radio-group">
        <button
            id="checkRadioButton"
            type="button"
            class="radio-button">
            Check Selection
        </button>
        <p
            id="radioMessage"
            class="radio-message"
            style="display:none;">
        </p>
    </div>
</div>

<script>
document.getElementById("checkRadioButton").addEventListener("click", function () {

    const gender =
        document.querySelector('input[name="gender"]:checked');

    const payment =
        document.querySelector('input[name="payment"]:checked');

    const experience =
        document.querySelector('input[name="experience"]:checked');

    const message =
        document.getElementById("radioMessage");
    
    const question=document.querySelector('input[name="question"]:checked');
    const question1=document.querySelector('input[name="question1"]:checked');

    let result = [];

    result.push(
        "Gender: " +
        (gender ? gender.value : "Not selected")
    );

    result.push(
        "Payment: " +
        (payment ? payment.value : "Not selected")
    );

    result.push(
        "Experience: " +
        (experience ? experience.value : "Not selected")
    );
    result.push(
        "Question: " +
        (question ? question.value : "Not selected"),
        (question1 ? question1.value : "Not selected")
    );
        

    message.textContent = result.join(" | ");

    message.style.display = "block";
});
</script>