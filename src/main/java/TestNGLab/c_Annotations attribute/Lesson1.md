# TestNG Annotation Attributes

Attributes are extra settings added inside parentheses after an annotation. They control how the annotation behaves.

---

## 1. priority

Controls the order in which tests run. Lower number runs first. Default is 0.

```java
@Test(priority = 1)
public void login() {
    System.out.println("Login test");
}

@Test(priority = 2)
public void addToCart() {
    System.out.println("Add to cart test");
}

@Test(priority = 3)
public void checkout() {
    System.out.println("Checkout test");
}
```

Execution order: login, addToCart, checkout.

---

## 2. dependsOnMethods

A test only runs if the specified method passes. If it fails, this test is skipped.

```java
@Test
public void login() {
    System.out.println("Login");
    Assert.fail("Login failed");
}

@Test(dependsOnMethods = "login")
public void searchProduct() {
    System.out.println("Search product");
}
```

If login fails, searchProduct is skipped.

---

## 3. dependsOnGroups

A test depends on all methods in a group passing.

```java
@Test(groups = "init")
public void openBrowser() {
    System.out.println("Browser opened");
}

@Test(groups = "init")
public void login() {
    System.out.println("Logged in");
}

@Test(dependsOnGroups = "init")
public void placeOrder() {
    System.out.println("Order placed");
}
```

If any method in the init group fails, placeOrder is skipped.

---

## 4. groups

Assigns a test to one or more groups. You can run specific groups from testng.xml.

```java
@Test(groups = "smoke")
public void testLogin() {
    System.out.println("Smoke test - Login");
}

@Test(groups = "regression")
public void testCheckout() {
    System.out.println("Regression test - Checkout");
}

@Test(groups = {"smoke", "regression"})
public void testSearch() {
    System.out.println("Both smoke and regression");
}
```

---

## 5. enabled

Set to false to skip a test without deleting it.

```java
@Test(enabled = false)
public void oldFeatureTest() {
    System.out.println("This test is skipped");
}

@Test
public void newFeatureTest() {
    System.out.println("This test runs");
}
```

---

## 6. description

Adds a human-readable description for reporting.

```java
@Test(description = "Verify user can login with valid credentials")
public void validLoginTest() {
    System.out.println("Login with valid data");
}
```

This appears in the HTML report.

---

## 7. invocationCount

Runs the same test multiple times.

```java
@Test(invocationCount = 5)
public void stressTest() {
    System.out.println("Running stress test");
}
```

This test runs 5 times.

---

## 8. timeOut

Fails the test if it takes longer than the specified milliseconds.

```java
@Test(timeOut = 2000)
public void slowTest() throws InterruptedException {
    Thread.sleep(3000);
    System.out.println("This will fail due to timeout");
}
```

Fails because 3000 ms exceeds 2000 ms limit.

---

## 9. expectedExceptions

Expects the test to throw a specific exception. If it throws that exception, the test passes.

```java
@Test(expectedExceptions = ArithmeticException.class)
public void divideByZero() {
    int result = 10 / 0;
}
```

Test passes because dividing by zero throws ArithmeticException.

---

## 10. alwaysRun

Used with @BeforeMethod and @AfterMethod. Forces the method to run even if a test is skipped.

```java
@BeforeMethod(alwaysRun = true)
public void setup() {
    System.out.println("Setup runs even for skipped tests");
}
```

---

## 11. dataProvider

Links a test to a DataProvider method.

```java
@DataProvider(name = "loginData")
public Object[][] getData() {
    return new Object[][] {
        {"user1", "pass1"},
        {"user2", "pass2"}
    };
}

@Test(dataProvider = "loginData")
public void loginTest(String user, String pass) {
    System.out.println("Testing login with " + user + " / " + pass);
}
```

---

## Quick Reference Table

| Attribute | Used With | Purpose |
|-----------|-----------|---------|
| priority | @Test | Set execution order |
| dependsOnMethods | @Test | Run only if another method passes |
| dependsOnGroups | @Test | Run only if a group passes |
| groups | @Test | Assign to a group |
| enabled | @Test | Enable or disable the test |
| description | @Test | Add description for reports |
| invocationCount | @Test | Run multiple times |
| timeOut | @Test | Maximum allowed time in ms |
| expectedExceptions | @Test | Expect a specific exception |
| alwaysRun | @BeforeMethod, @AfterMethod | Run even if test is skipped |
| dataProvider | @Test | Link to a data source |
| name | @DataProvider | Name the data provider |
| parallel | @DataProvider | Run data sets in parallel |