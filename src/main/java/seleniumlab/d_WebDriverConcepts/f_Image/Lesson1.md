<div class="lesson-header">
<h1>Image Handling & Taking Screenshots in Selenium</h1>
<a href="../img.html" class="playground-button">
    Practice Playground →
</a>
</div>
## PART A: Image Handling 

## 1. What is an Image WebElement?

- Images are defined by the **`<img>` tag** in HTML.
- In Selenium, an image is just another **WebElement** — find it with a locator, then read its properties.
```html
<img id="logo" src="images/logo.png" alt="Company Logo" width="200" height="80">
```

---

## 2. Operations on Images 

```java
WebElement img = driver.findElement(By.id("logo"));
```

| Operation | Code | Purpose |
|---|---|---|
| Is image displayed? | `img.isDisplayed()` | Verify logo/banner visible |
| Get image path | `img.getAttribute("src")` | Which image file is loaded |
| Get alt text | `img.getAttribute("alt")` | Alternative text of image |
| Get size | `img.getSize()` | Height & width |
| Click image | `img.click()` | Image used as a link/button |

**Example — verify logo on a page:**
```java
WebElement logo = driver.findElement(By.id("logo"));

if (logo.isDisplayed()) {
    System.out.println("Logo is visible ✔");
    System.out.println("Image source: " + logo.getAttribute("src"));
} else {
    System.out.println("Logo missing ✘");
}
```

---
## PART B: Taking Screenshots 

## 1. Why Take Screenshots?

- **Proof of test failure** — when a test fails, a screenshot shows exactly what was on screen.
- **Reporting** — attach screenshots to test reports (very common in real projects).
- **Visual verification** — compare how the page looks.

---

## 2. TakesScreenshot Interface — Full Page Screenshot

Selenium has a built-in interface called **`TakesScreenshot`**.

**Steps:**
1. Convert the driver into `TakesScreenshot` type.
2. Call `getScreenshotAs()` → returns a **File**.
3. Copy that file to your desired location.

```java
import org.openqa.selenium.TakesScreenshot;
import org.openqa.selenium.OutputType;
import org.apache.commons.io.FileUtils;
import java.io.File;

// 1. Convert driver to TakesScreenshot
TakesScreenshot ts = (TakesScreenshot) driver;

// 2. Take screenshot (stored as temp file)
File srcFile = ts.getScreenshotAs(OutputType.FILE);

// 3. Copy to your folder
File destFile = new File("C:\\Screenshots\\homepage.png");
FileUtils.copyFile(srcFile, destFile);

System.out.println("Screenshot saved ✔");
```

>  Reusable method you can call anytime:
```java
public static void captureScreenshot(WebDriver driver, String fileName) throws IOException {
    TakesScreenshot ts = (TakesScreenshot) driver;
    File src = ts.getScreenshotAs(OutputType.FILE);
    FileUtils.copyFile(src, new File("C:\\Screenshots\\" + fileName + ".png"));
}

// usage:
captureScreenshot(driver, "login_page");
```

---

## 6. Screenshot of a SPECIFIC Element (Selenium 4)

Instead of the whole page, capture just one element (logo, error message, captcha):

```java
WebElement logo = driver.findElement(By.id("logo"));

File src = logo.getScreenshotAs(OutputType.FILE);
FileUtils.copyFile(src, new File("C:\\Screenshots\\logo.png"));
```
