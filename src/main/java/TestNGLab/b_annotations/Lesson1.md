# TestNG Annotations

Annotations in TestNG are markers placed above methods to tell TestNG what role each method plays. They replace the old JUnit style of naming methods with `test` or `setUp` prefixes.

---

## Common Annotations

| Annotation | When It Runs |
|------------|--------------|
| `@BeforeSuite` | Once before all tests in the suite |
| `@BeforeTest` | Once before any test method in the current test tag |
| `@BeforeClass` | Once before the first test method in the current class |
| `@BeforeMethod` | Before every test method |
| `@Test` | Marks the actual test method |
| `@AfterMethod` | After every test method |
| `@AfterClass` | Once after all test methods in the current class |
| `@AfterTest` | Once after all test methods in the current test tag |
| `@AfterSuite` | Once after all tests in the suite |

---

## Simple Code Example

```java
import org.testng.annotations.*;

public class AnnotationDemo {

    @BeforeSuite
    public void beforeSuite() {
        System.out.println("Before Suite - Runs once at the very start");
    }

    @BeforeTest
    public void beforeTest() {
        System.out.println("Before Test - Runs once before test tag");
    }

    @BeforeClass
    public void beforeClass() {
        System.out.println("Before Class - Runs once before any test in this class");
    }

    @BeforeMethod
    public void beforeMethod() {
        System.out.println("Before Method - Runs before every @Test");
    }

    @Test
    public void testOne() {
        System.out.println("Test One");
    }

    @Test
    public void testTwo() {
        System.out.println("Test Two");
    }

    @AfterMethod
    public void afterMethod() {
        System.out.println("After Method - Runs after every @Test");
    }

    @AfterClass
    public void afterClass() {
        System.out.println("After Class - Runs once after all tests in this class");
    }

    @AfterTest
    public void afterTest() {
        System.out.println("After Test - Runs once after test tag");
    }

    @AfterSuite
    public void afterSuite() {
        System.out.println("After Suite - Runs once at the very end");
    }
}
```

---

## Execution Order

```
Before Suite
  Before Test
    Before Class
      Before Method
        Test One
      After Method
      Before Method
        Test Two
      After Method
    After Class
  After Test
After Suite
```

---

## Output

```
Before Suite - Runs once at the very start
Before Test - Runs once before test tag
Before Class - Runs once before any test in this class
Before Method - Runs before every @Test
Test One
After Method - Runs after every @Test
Before Method - Runs before every @Test
Test Two
After Method - Runs after every @Test
After Class - Runs once after all tests in this class
After Test - Runs once after test tag
After Suite - Runs once at the very end
```

---

## Tips

- Use `@BeforeMethod` and `@AfterMethod` to open and close the browser for each test.
- Use `@BeforeClass` and `@AfterClass` for one-time setup like reading config files.
- Use `@BeforeSuite` for initializing the test environment or report setup.
- Every method marked with `@Test` is counted as a separate test case.