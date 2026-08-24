# Selenium Frameworks 

## 1. What is a Selenium Framework?

A Selenium framework is a structured way to organize your test code. It separates test logic, data, and execution to make automation reusable, maintainable, and easy to read.

---

## 2. Types of Selenium Frameworks

### 1. Data-Driven Framework

Test data is stored outside the test scripts, usually in Excel, CSV, or databases. The same test runs with multiple sets of data.

**Use when:** You need to run the same test with different inputs.

---

### 2. Keyword-Driven Framework

Tests are written using keywords (actions like "click", "type", "verify") stored in an external file. The framework reads keywords and performs actions.

**Use when:** Non-programmers need to write or understand test cases.

---

### 3. Hybrid Framework

Combines Data-Driven and Keyword-Driven approaches. Uses external files for both test data and keywords.

**Use when:** You need maximum flexibility and reusability.

---

### 4. Page Object Model (POM)

The most popular design pattern. Each web page has a separate Java class. Page classes contain web elements and actions. Test classes only contain assertions and flow.

**Use when:** You want clean, maintainable, and scalable code.

---

## 3. Popular Tools Used with Selenium Frameworks

| Tool | Purpose |
|------|---------|
| TestNG / JUnit | Test execution, assertions, annotations |
| Maven / Gradle | Build and dependency management |
| Apache POI | Read test data from Excel |
| Log4j | Logging test execution |
| Extent Reports / Allure | Generate HTML test reports |
| Cucumber | BDD-style test writing (Gherkin syntax) |

---

## 4. Why Use a Framework?

- Code reusability across multiple tests
- Easy maintenance when UI changes
- Separation of test logic and test data
- Better reporting and logging
- Multiple people can work on the same project easily

---

## 5. Quick Comparison

| Framework | Best For | Complexity |
|-----------|----------|------------|
| POM | Most projects | Low |
| Data-Driven | Multiple data sets | Medium |
| Keyword-Driven | Non-coder teams | High |
| Hybrid | Large enterprise projects | High |
