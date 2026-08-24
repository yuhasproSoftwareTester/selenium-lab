# Handling Multiple Windows in Selenium 

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

<style>
.window-playground {
    max-width: 650px;
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 8px;
}

.window-section {
    margin-bottom: 20px;
}

.window-button {
    display: block;
    padding: 10px 16px;
    margin-bottom: 12px;
    border: none;
    border-radius: 5px;
    background: #1976d2;
    color: white;
    font-size: 15px;
    cursor: pointer;
}

.window-button:hover {
    background: #1565c0;
}

.window-info {
    padding: 12px;
    margin-top: 15px;
    border-radius: 5px;
    background: #f3f3f3;
}

.window-message {
    margin-top: 10px;
    font-weight: 500;
}
</style>


<div class="window-playground">

    <h3>Multiple Windows Playground</h3>

    <!-- Main Window Information -->
    <div class="window-section">

        <strong>Main Window</strong>

        <p>
            This is the original browser window.
        </p>

        <button
            id="mainWindowInfo"
            type="button"
            class="window-button">

            Show Main Window Information

        </button>

    </div>


    <!-- New Tab -->
    <div class="window-section">

        <strong>1. Open New Tab</strong>

        <button
            id="newTab"
            type="button"
            class="window-button">

            New Tab

        </button>

    </div>


    <!-- New Window -->
    <div class="window-section">

        <strong>2. Open New Window</strong>

        <button
            id="newWindow"
            type="button"
            class="window-button">

            New Window

        </button>

    </div>


    <!-- New Window With Elements -->
    <div class="window-section">

        <strong>3. Open Window With Message</strong>

        <button
            id="newWindowMessage"
            type="button"
            class="window-button">

            New Window Message

        </button>

    </div>


    <!-- Multiple Windows -->
    <div class="window-section">
    <strong>4. Open Multiple Windows</strong>
    <button
        id="openWindow1"
        type="button"
        class="window-button">
        Open Window 1
    </button>
    <button
        id="openWindow2"
        type="button"
        class="window-button">
        Open Window 2
    </button>
    <button
        id="openWindow3"
        type="button"
        class="window-button">
        Open Window 3
    </button>
</div>


    <!-- Result -->
    <div
        id="windowInfo"
        class="window-info">

        Use the buttons above to create new tabs and windows.

    </div>

</div>


<script>

/* -----------------------------------
   MAIN WINDOW INFORMATION
----------------------------------- */

document
    .getElementById("mainWindowInfo")
    .addEventListener("click", function () {

        document.getElementById("windowInfo").textContent =
            "You are currently on the main Selenium Lab window.";

    });


/* -----------------------------------
   NEW TAB
----------------------------------- */

document
    .getElementById("newTab")
    .addEventListener("click", function () {

        const newTab = window.open(
            "",
            "_blank"
        );

        newTab.document.write(`

            <!DOCTYPE html>

            <html>

            <head>

                <title>Practice New Tab</title>

            </head>

            <body>

                <h1 id="tabTitle">
                    Practice New Tab
                </h1>

                <p id="tabMessage">
                    This page was opened in a new browser tab.
                </p>

            </body>

            </html>

        `);

    });


/* -----------------------------------
   NEW WINDOW
----------------------------------- */

document
    .getElementById("newWindow")
    .addEventListener("click", function () {

        const newWindow = window.open(
            "",
            "_blank",
            "width=800,height=600"
        );

        newWindow.document.write(`

            <!DOCTYPE html>

            <html>

            <head>

                <title>Practice New Window</title>

            </head>

            <body>

                <h1 id="windowTitle">
                    Practice New Window
                </h1>

                <p id="windowText">
                    This is a separate browser window.
                </p>

            </body>

            </html>

        `);

    });


/* -----------------------------------
   NEW WINDOW WITH ELEMENTS
----------------------------------- */

document
    .getElementById("newWindowMessage")
    .addEventListener("click", function () {

        const newWindow = window.open(
            "",
            "_blank",
            "width=800,height=600"
        );

        newWindow.document.write(`

            <!DOCTYPE html>

            <html>

            <head>

                <title>Window Message</title>

            </head>

            <body>

                <h1 id="messageTitle">
                    Practice Window Message
                </h1>

                <p id="windowMessage">
                    You successfully switched to the new window!
                </p>

                <input
                    id="windowInput"
                    type="text"
                    placeholder="Enter something">

                <br><br>

                <button
                    id="windowButton"
                    type="button">

                    Practice Button

                </button>

                <p id="buttonMessage"></p>

                <script>

                    document
                        .getElementById("windowButton")
                        .addEventListener("click", function () {

                            document
                                .getElementById("buttonMessage")
                                .textContent =
                                "Button clicked successfully!";

                        });

                <\/script>

            </body>

            </html>

        `);

    });


document.getElementById("openWindow1").addEventListener("click", function () {

    const newWindow = window.open(
        "",
        "_blank",
        "width=700,height=500"
    );

    newWindow.document.write(`
        <!DOCTYPE html>
        <html>
        <head>
            <title>Practice Window 1</title>
        </head>

        <body>

            <h1 id="window1Title">
                Practice Window 1
            </h1>

            <p id="window1Message">
                This is the first practice window.
            </p>

        </body>
        </html>
    `);

});


document.getElementById("openWindow2").addEventListener("click", function () {

    const newWindow = window.open(
        "",
        "_blank",
        "width=700,height=500"
    );

    newWindow.document.write(`
        <!DOCTYPE html>
        <html>
        <head>
            <title>Practice Window 2</title>
        </head>

        <body>

            <h1 id="window2Title">
                Practice Window 2
            </h1>

            <p id="window2Message">
                This is the second practice window.
            </p>

        </body>
        </html>
    `);

});


document.getElementById("openWindow3").addEventListener("click", function () {

    const newWindow = window.open(
        "",
        "_blank",
        "width=700,height=500"
    );

    newWindow.document.write(`
        <!DOCTYPE html>
        <html>
        <head>
            <title>Practice Window 3</title>
        </head>

        <body>

            <h1 id="window3Title">
                Practice Window 3
            </h1>

            <p id="window3Message">
                This is the third practice window.
            </p>

        </body>
        </html>
    `);

});

</script>