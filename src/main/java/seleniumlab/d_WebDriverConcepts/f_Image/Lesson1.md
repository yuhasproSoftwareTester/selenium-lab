# Image Handling & Taking Screenshots in Selenium 
---

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

<style>
.image-playground {
    max-width: 650px;
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 8px;
}

.image-group {
    margin-bottom: 20px;
}

.practice-image {
    width: 150px;
    height: 150px;
    object-fit: contain;
    border: 1px solid #999;
    border-radius: 5px;
    padding: 5px;
}

.image-button {
    padding: 9px 18px;
    border: 1px solid #999;
    border-radius: 5px;
    background: #eee;
    cursor: pointer;
    margin-right: 8px;
}

.image-button:hover {
    background: #ddd;
}

.image-result {
    margin-top: 15px;
}
</style>

<div class="image-playground">

    <h3>Image & Screenshot Playground</h3>

    <!-- Image 1 -->
    <div class="image-group">

        <img
            id="seleniumLogo"
            class="practice-image"
            src="https://www.selenium.dev/images/selenium_logo_square_green.svg"
            alt="Selenium Logo">

    </div>

    <!-- Image 2 -->
    <div class="image-group">

        <img
            id="secondImage"
            class="practice-image"
            src="https://www.selenium.dev/images/selenium_logo_square_green.svg"
            alt="Practice Image">

    </div>

    <!-- Buttons -->
    <div class="image-group">

        <button
            id="imageInfoButton"
            type="button"
            class="image-button">

            Get Image Information

        </button>

        <button
            id="imageVisibilityButton"
            type="button"
            class="image-button">

            Check Image

        </button>

    </div>

    <p
        id="imageResult"
        class="image-result">
    </p>

</div>

<script>
document.getElementById("imageInfoButton").addEventListener("click", function () {

    const image =
        document.getElementById("seleniumLogo");

    const src =
        image.getAttribute("src");

    const alt =
        image.getAttribute("alt");

    const width =
        image.getSize ? image.offsetWidth : 0;

    const height =
        image.offsetHeight;

    document.getElementById("imageResult").textContent =
        "Alt: " + alt +
        " | Width: " + width +
        " | Height: " + height;

});


document.getElementById("imageVisibilityButton").addEventListener("click", function () {

    const image =
        document.getElementById("seleniumLogo");

    document.getElementById("imageResult").textContent =
        image.complete
            ? "Image is loaded."
            : "Image is not loaded.";

});
</script>