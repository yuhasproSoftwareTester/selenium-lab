# TestNG Groups

## What are Groups

Groups in TestNG are labels assigned to test methods. You can tag tests with names like smoke, regression, sanity, or login. Later, you choose which group to run instead of running all tests.

---

## Why Use Groups

| Reason | Explanation |
|--------|-------------|
| Selective Execution | Run only relevant tests during development or release. |
| Organized Testing | Separate fast checks (smoke) from full checks (regression). |
| CI/CD Integration | Run smoke tests on every build, regression only at night. |
| Team Collaboration | Different teams own different groups. |

---

## How to Define Groups

Use the `groups` attribute inside `@Test`.

```java
import org.testng.annotations.Test;

public class GroupDemo {

    @Test(groups = "smoke")
    public void testLogin() {
        System.out.println("Smoke - Login test");
    }

    @Test(groups = "smoke")
    public void testLogout() {
        System.out.println("Smoke - Logout test");
    }

    @Test(groups = "regression")
    public void testCheckout() {
        System.out.println("Regression - Checkout test");
    }

    @Test(groups = "regression")
    public void testPayment() {
        System.out.println("Regression - Payment test");
    }

    @Test(groups = {"smoke", "regression"})
    public void testSearch() {
        System.out.println("Both - Search test");
    }
}
```

---

## How to Run Specific Groups

Create a `testng.xml` file. Use `<groups>` to include or exclude.

```xml
<!DOCTYPE suite SYSTEM "https://testng.org/testng-1.0.dtd">
<suite name="Suite">
    <test name="SmokeTests">
        <groups>
            <run>
                <include name="smoke"/>
            </run>
        </groups>
        <classes>
            <class name="GroupDemo"/>
        </classes>
    </test>
</suite>
```

Only methods tagged with `smoke` will run.

---

## Include and Exclude Together

```xml
<groups>
    <run>
        <include name="regression"/>
        <exclude name="smoke"/>
    </run>
</groups>
```

Runs regression tests but skips those also tagged as smoke.

---

## Group Execution Order

When you run the smoke group from the example above, the output is:

```
Smoke - Login test
Smoke - Logout test
Both - Search test
```

`testSearch` runs because it belongs to both smoke and regression.

---

## Tips

- A test can belong to multiple groups using `groups = {"a", "b"}`.
- Use `@BeforeGroups` to run setup code before a specific group.
---