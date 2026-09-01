## 1. Why Do We Need Waits?

- Web pages are **dynamic** — elements load at different speeds (AJAX, animations, API calls).
- Selenium runs **faster than the page loads** — without waits you get:
  - `NoSuchElementException` — element not in DOM yet
  - `ElementNotInteractableException` — in DOM but hidden/loading
  - `StaleElementReferenceException` — element was re-rendered
- **Key point:** There are **three types of waits**, and hard-coded `Thread.sleep()` is the one to avoid.

| Type | Behavior | Use when |
|---|---|---|
| `Thread.sleep()` | **Always** waits full time | Never (debugging only) |
| **Implicit Wait** | Waits up to N sec for **every** element lookup | Global default for the whole session |
| **Explicit Wait** | Waits up to N sec for a **specific condition** | Slow-loading elements, dynamic content |

**The problem with sleep:**
```java
Thread.sleep(5000);   //  waits 5 sec ALWAYS — even if element loaded in 0.2 sec
```

---

## 2. Implicit Wait

Set **once**, applies to **every** `findElement()` call for the driver's lifetime:

```java
driver.manage().timeouts().implicitlyWait(Duration.ofSeconds(10));

WebElement el = driver.findElement(By.id("username"));  // waits up to 10s, then throws
```

**Behavior:**
- Polls the DOM until the element **exists** or time expires.
- If found in 2 sec → continues in 2 sec (doesn't wait the full 10).
- If not found in 10 sec → throws `NoSuchElementException`.

>  Implicit wait only checks for **presence in DOM** — an invisible or disabled element still fails. It also can't wait for custom conditions.

**Import:**
```java
import java.time.Duration;   // Selenium 4 — no more TimeUnit.SECONDS
```

---

## 3. Explicit Wait (WebDriverWait)

Waits for a **specific condition** on a **specific element**:

```java
import org.openqa.selenium.support.ui.WebDriverWait;
import org.openqa.selenium.support.ui.ExpectedConditions;

WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));

wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("welcome")));
```

**Behavior:**
- Polls the condition (every 500ms by default) until it's **true** or timeout.
- Timeout throws `TimeoutException` — handle with try/catch if needed.
- Applies **only** to the condition you write — other `findElement()` calls are unaffected.

**Most used ExpectedConditions:**

```java
wait.until(ExpectedConditions.elementToBeClickable(By.id("submit")));
wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("msg")));
wait.until(ExpectedConditions.presenceOfElementLocated(By.id("row")));
wait.until(ExpectedConditions.invisibilityOfElementLocated(By.id("spinner")));
wait.until(ExpectedConditions.textToBePresentInElementLocated(By.id("status"), "Done"));
wait.until(ExpectedConditions.alertIsPresent());
wait.until(ExpectedConditions.titleContains("Dashboard"));
wait.until(ExpectedConditions.urlContains("/home"));
wait.until(ExpectedConditions.numberOfElementsToBe(By.tagName("tr"), 10));
```

| Condition | Waits for |
|---|---|
| `presenceOfElementLocated` | Element **exists** in DOM (may be invisible) |
| `visibilityOfElementLocated` | Exists **and** visible (displayed, size > 0) |
| `elementToBeClickable` | Visible **and** enabled |
| `invisibilityOfElementLocated` | Element gone or hidden (spinners, loaders) |
| `alertIsPresent()` | JS alert popup |
| `frameToBeAvailableAndSwitchToIt` | iframe ready + auto-switches into it |

---

## 4. Waiting for an Element You Already Found

```java
WebElement btn = driver.findElement(By.id("submit"));

wait.until(ExpectedConditions.elementToBeClickable(btn)).click();   // ① by element
wait.until(ExpectedConditions.visibilityOf(btn));                    // ② visibility only
wait.until(ExpectedConditions.elementToBeSelected(btn));             // ③ checkbox/radio
```

>  Note the naming difference: methods taking `By` say `...ElementLocated`, methods taking an already-found `WebElement` say just `visibilityOf` / `elementToBeClickable`.

---

## 5. Custom ExpectedCondition + Lambda

When no built-in condition fits, write your own:

```java
// Java 8 lambda — wait until a spinner's class changes
wait.until(d -> d.findElement(By.id("spinner")).getAttribute("class").contains("done"));

// Wait until element count stops changing (dynamic table finished loading)
wait.until(d -> {
    int count = d.findElements(By.tagName("tr")).size();
    return count == prevCount && count > 0;
});
```

>  A lambda takes the `driver` as input and returns a value — non-null / true = condition met.

---

## 6. FluentWait (Explicit Wait with Full Control)

**FluentWait** is the parent class of `WebDriverWait` — adds custom **polling interval** and **exception ignoring**:

```java
import org.openqa.selenium.support.ui.FluentWait;

Wait<WebDriver> wait = new FluentWait<>(driver)
        .withTimeout(Duration.ofSeconds(30))          // max total wait
        .pollingEvery(Duration.ofSeconds(3))          // check every 3 sec (default 500ms)
        .ignoring(NoSuchElementException.class);      // keep trying through this exception

wait.until(ExpectedConditions.visibilityOfElementLocated(By.id("dynamic")));
```

| Setting | Default (WebDriverWait) | FluentWait |
|---|---|---|
| Timeout | `Duration` — set | `withTimeout()` — set |
| Polling interval | 500ms | `pollingEvery()` — custom |
| Ignored exceptions | `NotFoundException` only | `ignoring()` — any |

>  Use FluentWait when the element appears **slowly or intermittently** (e.g., polling a status API every few seconds) or when a specific exception must be tolerated.

---

## 7. Implicit vs Explicit — Rules

- **Don't mix them.** Selenium waits for implicit + explicit **added together** → unpredictable long waits.
  - Common practice: **implicit = 0**, use **explicit waits everywhere** (or small implicit like 5s + explicit for slow elements only).
- Explicit > Implicit in precision: explicit waits for a *condition*, implicit only for *existence*.
- **Never** mix `Thread.sleep()` into real tests — it's the #1 cause of both flaky failures and pointlessly slow suites.
- Default polling of `WebDriverWait` is **500ms** — don't add sleeps "to be safe"; make the condition specific instead.

---

## 8. Real-World Pattern

```java
WebDriverWait wait = new WebDriverWait(driver, Duration.ofSeconds(10));

// ① Click a button that triggers a spinner, then a result table
driver.findElement(By.id("searchBtn")).click();

// ② Wait for the loading spinner to disappear
wait.until(ExpectedConditions.invisibilityOfElementLocated(By.id("loading")));

// ③ Wait for results to be visible AND clickable
wait.until(ExpectedConditions.elementToBeClickable(By.cssSelector(".result-row")))
     .click();
```

>  This three-step pattern (act → wait for loader to vanish → wait for result) eliminates most `NoSuchElementException` and `ElementClickInterceptedException` failures.