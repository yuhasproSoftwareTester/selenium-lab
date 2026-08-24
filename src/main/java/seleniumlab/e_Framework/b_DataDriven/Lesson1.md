# Data-Driven Selenium 

A Data-Driven framework is a test automation approach where test data is stored separately from test scripts. The test logic is written once, but it runs multiple times using different sets of data.

Instead of hardcoding values like username and password inside the code, you keep them in external files such as Excel, CSV, JSON, or databases. The test script reads this data and executes the same steps for each row or record.

---

## Why Use Data-Driven Framework

| Reason | Explanation |
|--------|-------------|
| Reusability | One test script can handle hundreds of test cases by just changing the input data. |
| Easy Maintenance | If test data changes, you only update the external file, not the code. |
| Less Code Duplication | You do not write the same login test 50 times for 50 different users. |
| Better Coverage | You can test edge cases, invalid inputs, and boundary values easily by adding more rows to the data file. |
| Separation of Concerns | Test logic stays in code. Test data stays in files. Both can be managed independently. |
| Non-technical Friendly | Testers or business analysts can update data in Excel without touching Java code. |

---

## How It Works

1. Store test data in an external source (Excel, CSV, database).
2. Write one test script that accepts data as parameters.
3. The script loops through each row of data.
4. For each row, it performs the same actions but with different inputs.
5. Results are logged or reported for each data set separately.

---

## Simple Analogy

Think of a coffee machine. The machine itself is the test script. The coffee beans, water, and milk are the test data. You do not build a new machine for every type of coffee. You use the same machine and just change the ingredients. That is what a Data-Driven framework does.

---

## When to Use It

- Login forms with multiple valid and invalid credentials
- Registration forms with different user details
- Search functionality with various keywords
- Forms that accept multiple combinations of inputs

---

## When Not to Use It

- The test always uses the same fixed data
- The test logic itself changes for every scenario
- The test is a one-time execution with no variations

---

A Data-Driven framework is essential when you want to scale automation without multiplying code. It saves time, reduces errors, and makes test suites easier to manage.
This example uses only **Selenium WebDriver** and a simple loop to run login tests with multiple sets of data on **https://www.saucedemo.com/**.

---

## 1. Maven Dependency

```xml
<dependency>
    <groupId>org.seleniumhq.selenium</groupId>
    <artifactId>selenium-java</artifactId>
    <version>4.15.2</version>
</dependency>
```

---

## 2. Complete Example

```java
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.chrome.ChromeDriver;

public class DataDrivenLogin {
    public static void main(String[] args) {
        // Test data: username, password, expected outcome
        String[][] testData = {
            {"standard_user", "secret_sauce", "pass"},
            {"locked_out_user", "secret_sauce", "fail"},
            {"wrong_user", "wrong_pass", "fail"}
        };

        for (String[] row : testData) {
            String username = row[0];
            String password = row[1];
            String expected = row[2];

            WebDriver driver = new ChromeDriver();
            driver.manage().window().maximize();

            try {
                driver.get("https://www.saucedemo.com/");

                WebElement userBox = driver.findElement(By.id("user-name"));
                WebElement passBox = driver.findElement(By.id("password"));
                WebElement loginBtn = driver.findElement(By.id("login-button"));

                userBox.sendKeys(username);
                passBox.sendKeys(password);
                loginBtn.click();

                Thread.sleep(1000);

                String currentUrl = driver.getCurrentUrl();
                boolean isLoggedIn = currentUrl.contains("inventory");

                if (expected.equals("pass") && isLoggedIn) {
                    System.out.println("PASS: " + username + " logged in successfully.");
                } else if (expected.equals("fail") && !isLoggedIn) {
                    System.out.println("PASS: " + username + " failed to login as expected.");
                } else {
                    System.out.println("FAIL: " + username + " result did not match expectation.");
                }

            } catch (Exception e) {
                System.out.println("ERROR: " + username + " - " + e.getMessage());
            } finally {
                driver.quit();
            }
        }
    }
}
```

---

## 3. Console Output

```
PASS: standard_user logged in successfully.
PASS: locked_out_user failed to login as expected.
PASS: wrong_user failed to login as expected.
```

---

## 4. Using Excel Instead of Hardcoded Data

Since you already know Apache POI, replace the `String[][]` with an Excel reader inside the loop:

```java
// Read from Excel using XSSFWorkbook
XSSFWorkbook workbook = new XSSFWorkbook(new FileInputStream("login_data.xlsx"));
XSSFSheet sheet = workbook.getSheetAt(0);

for (int i = 1; i <= sheet.getLastRowNum(); i++) {
    XSSFRow row = sheet.getRow(i);
    String username = row.getCell(0).getStringCellValue();
    String password = row.getCell(1).getStringCellValue();
    String expected = row.getCell(2).getStringCellValue();

    // Same WebDriver code as above
}
```