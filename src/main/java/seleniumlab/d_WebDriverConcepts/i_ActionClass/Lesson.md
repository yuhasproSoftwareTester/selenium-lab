<div class="lesson-header">
<h1>Action Class in Selenium</h1>
<a href="../Action.html" class="playground-button">
    Practice Playground →
</a>
</div>

## 1. What is the Action Class?

- The **Actions class** handles **mouse and keyboard interactions** that simple `click()` / `sendKeys()` can't do.
- Used for: Hover menus, drag & drop, double-click, right-click, slider movements, key combinations (Ctrl+A, Ctrl+C).
- **Key point:** Actions perform **composite actions** — a sequence of low-level events that are built first, then performed together.

| Interaction | Normal WebDriver | Actions class |
|---|---|---|
| Single click | `element.click()` | Works, but not needed |
| Double-click |  Not possible | `doubleClick()` |
| Right-click (context click) |  Not possible | `contextClick()` |
| Mouse hover |  Not possible | `moveToElement()` |
| Drag & drop |  Not possible | `dragAndDrop()` |
| Ctrl + click (multi-select) |  Not possible | `keyDown(Keys.CONTROL)` + click |

---

## 2. Creating the Actions Object

**Import and create object:**
```java
import org.openqa.selenium.interactions.Actions;

Actions act = new Actions(driver);   // pass the WebDriver into Actions
```

>  The Actions class takes the **WebDriver** (not a WebElement) — you tell it *which element* inside each method.

**Two ways to run an action:**

```java
// ① Single action — perform() alone is enough
act.moveToElement(menu).perform();

// ② Multiple actions — build() chains them, then perform() executes all
act.moveToElement(menu)
   .click(link)
   .build()
   .perform();
```

>  In Selenium 4, `perform()` automatically calls `build()` internally, so `build()` is optional — but writing it makes chained actions explicit and readable.

---

## 3. Mouse Actions 

```java
Actions act = new Actions(driver);

act.click(element).perform();              // ① left click
act.contextClick(element).perform();       // ② right click
act.doubleClick(element).perform();        // ③ double click
act.moveToElement(element).perform();      // ④ hover over element
act.clickAndHold(element).perform();       // ⑤ press and hold (sliders)
act.release(element).perform();            // ⑥ release the held mouse
act.dragAndDrop(src, dest).perform();      // ⑦ drag & drop in one step
```

| Method | What it does | Common use |
|---|---|---|
| `click()` | Left click | Normal clicking |
| `contextClick()` | Right click | Custom context menus |
| `doubleClick()` | Double click | Opening items, selecting words |
| `moveToElement()` | Move mouse to element | Hover menus, tooltips |
| `clickAndHold()` / `release()` | Hold then release | Sliders, resizable elements |
| `dragAndDrop(src, dst)` | Drag source onto target | Kanban boards, sortable lists |

**Manual drag & drop (when `dragAndDrop()` doesn't work):**
```java
act.clickAndHold(src)
   .moveToElement(dest)
   .release(dest)
   .build()
   .perform();
```

>  If `moveToElement()` seems to miss the element, add an offset: `moveToElement(el, xOffset, yOffset)` — useful for elements whose clickable area isn't centered.

---

## 4. Keyboard Actions 

```java
import org.openqa.selenium.Keys;

Actions act = new Actions(driver);

act.sendKeys(Keys.ARROW_DOWN).perform();           // ① press a single key
act.keyDown(Keys.CONTROL)                          // ② press AND HOLD a key
   .sendKeys("a")
   .keyUp(Keys.CONTROL)                            //    release it after
   .perform();

act.sendKeys("Hello World").perform();             // ③ type like a real user
```

| Method | Based on | Example |
|---|---|---|
| `sendKeys()` | Press + release a key | `Keys.ENTER`, `"text"` |
| `keyDown()` | Hold key **down** | `Keys.CONTROL`, `Keys.SHIFT` |
| `keyUp()` | Release the held key | `keyUp(Keys.CONTROL)` |

>  `keyDown()` **must** be paired with `keyUp()` — otherwise Ctrl stays held and breaks every following action.

**Real combo — select all text and copy:**
```java
act.keyDown(Keys.CONTROL)
   .sendKeys("a")
   .sendKeys("c")
   .keyUp(Keys.CONTROL)
   .build()
   .perform();
```

---

## 5. Combining Hover + Click (Hidden Menus)

Hover menus hide the menu items until you hover the parent:

```java
Actions act = new Actions(driver);

WebElement menu   = driver.findElement(By.id("menu"));
WebElement subItem = driver.findElement(By.id("sub-item"));

act.moveToElement(menu)      // hover → submenu appears
   .pause(500)               // small wait for animation
   .click(subItem)           // click the now-visible item
   .build()
   .perform();
```

>  If the submenu isn't rendered until hover, use `pause()` or chain everything **in one perform()** — finding the element after a separate `perform()` may throw `ElementNotInteractableException`.

---

## 6. Important Rules

- **Chained actions are one unit** — nothing executes until `perform()` is called.
- `Actions` (the class, used for building) vs `Action` (the interface returned by `build()`) — you'll almost always just use `Actions` + `perform()`.
- Works only on elements that are **visible and in view** — combine with `scrollIntoView()` if needed.
- On single-select dropdowns built with `<select>`, prefer the **Select class** — Actions is for custom (Bootstrap) dropdowns and non-standard widgets.