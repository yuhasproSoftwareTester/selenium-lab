<div class="lesson-header">
<h1>Handling Multiple Windows in Selenium </h1>
<a href="../windows.html" class="playground-button">
    Practice Playground →
</a>
</div>

## 1. What is a Window Handle?

- When a website opens a **new window or tab** (e.g., clicking "Terms & Conditions" opens a popup), Selenium's focus stays on the **main window** — it can't see the new one.
- Every window opened by the browser gets a **unique ID** called a **window handle** (a string like `CDwindow-4F3A2B1C...`).
- To work on another window, we must **switch** the driver's focus to it using its handle.

>  Think of it like TV channels  — the remote (driver) can watch only one channel at a time; the window handle is the **channel number**.

---

## 2. Key Methods 

| Method | Returns | Purpose |
|---|---|---|
| `driver.getWindowHandle()` | **String** | Handle of the **current** window |
| `driver.getWindowHandles()` | **Set of Strings** | Handles of **ALL** open windows/tabs |
| `driver.switchTo().window(handle)` | — | Move focus to a specific window |
| `driver.close()` | — | Close the **current** window only |
| `driver.quit()` | — | Close **ALL** windows & end session |

>  Why a **Set**? Because all handles are **unique** — no duplicates, and no fixed order.

---

## 3. Basic Two-Window Handling 

**Scenario:** Main page → click a link → new window opens → work in it → close it → return to main page.

```java
// 1. Save the MAIN window handle BEFORE clicking
String mainWindow = driver.getWindowHandle();

// 2. Click the link that opens a new window
driver.findElement(By.linkText("Terms & Conditions")).click();

// 3. Get ALL window handles
Set<String> allWindows = driver.getWindowHandles();

// 4. Switch to the NEW window (the one that's NOT main)
for (String win : allWindows) {
    if (!win.equals(mainWindow)) {
        driver.switchTo().window(win);
    }
}

// 5. Now work in the new window
System.out.println("Popup title: " + driver.getTitle());

// 6. Close the popup and go back to main window
driver.close();                            // closes current (popup)
driver.switchTo().window(mainWindow);      // back to main window 
```

>  **Most common mistake:** after `driver.close()`, the driver has **no focus** — you MUST switch back to the main window, or you get `NoSuchWindowException`.

---

## 4. Handling MORE Than Two Windows

With 3+ windows, switch based on the **page title** (safest way):

```java
Set<String> allWindows = driver.getWindowHandles();

for (String win : allWindows) {
    driver.switchTo().window(win);
    if (driver.getTitle().equals("Contact Us")) {
        break;      // found the window we want — stay here
    }
}
```

**Print all open windows (useful for debugging):**
```java
Set<String> allWindows = driver.getWindowHandles();
System.out.println("Total windows: " + allWindows.size());

for (String win : allWindows) {
    driver.switchTo().window(win);
    System.out.println(win + " → " + driver.getTitle());
}
```

---

## 5. Opening a New Tab / Window Yourself (Selenium 4) 

Selenium 4 lets you **open** a new tab or window directly:

```java
// Open a NEW TAB and switch to it
driver.switchTo().newWindow(WindowType.TAB);
driver.get("https://www.google.com");

// Open a NEW WINDOW and switch to it
driver.switchTo().newWindow(WindowType.WINDOW);
driver.get("https://www.facebook.com");
```

---


## 6. Window vs Tab vs Frame vs Alert — Don't Confuse! 

| Thing | How to switch |
|---|---|
| **Window / Tab** | `driver.switchTo().window(handle)` |
| **Frame / iFrame** (inside the page) | `driver.switchTo().frame(...)` |
| **Alert popup** | `driver.switchTo().alert()` |
| **Back to main page from frame** | `driver.switchTo().defaultContent()` |
| **Back to main window** | `driver.switchTo().window(mainWindowHandle)` |

