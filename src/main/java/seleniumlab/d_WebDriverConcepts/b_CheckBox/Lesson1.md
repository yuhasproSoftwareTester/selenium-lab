<div class="lesson-header">
<h1>Checkbox Handling in Selenium</h1>
<a href="../checkbox.html" class="playground-button">
    Practice Playground →
</a>
</div>
## 1. What is a Checkbox?

- A **checkbox** is a small square box that can be **ticked (selected)** or **unticked (deselected)**.
- Used for: "Remember Me", "I agree to Terms", selecting hobbies, multiple choices in a form.
- **Key point:** Unlike radio buttons, **multiple checkboxes can be selected at the same time**.

**HTML of a checkbox:**
```html
<input type="checkbox" id="rememberMe" name="remember">
```

---

## 2. Methods Used with Checkboxes

| Method | Purpose |
|---|---|
| `click()` | Tick or untick the checkbox (toggles) |
| `isSelected()` | Returns `true` if ticked, `false` if not |
| `isDisplayed()` | Is checkbox visible on page? |
| `isEnabled()` | Is checkbox clickable (not greyed out)? |

