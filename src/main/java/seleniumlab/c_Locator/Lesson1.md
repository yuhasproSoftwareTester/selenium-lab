# Locator Techniques 

## 1. Introduction — What is a Locator?

- A **locator** is an **address of an element** on a web page (like a house address).
- Selenium can't "see" the page like humans — it needs a locator to **find elements** (textbox, button, link, checkbox…) before it can click or type on them.
- In WebDriver we find elements using:
```java
driver.findElement(By.locatorName("value"));
```
- If the locator is **wrong or not unique** → you get `NoSuchElementException`. So choosing a **good, unique locator** is the most important skill in Selenium.

---

## 2. Different Locator Techniques (8 Types)

| # | Locator | Syntax Example | When to use |
|---|---|---|---|
| 1 | **ID** | `By.id("username")` |  **First choice** — fastest & unique |
| 2 | **Name** | `By.name("email")` | When element has a name attribute |
| 3 | **Class Name** | `By.className("btn-submit")` | When class is unique |
| 4 | **Tag Name** | `By.tagName("input")` | To get many elements (all links, inputs) |
| 5 | **Link Text** | `By.linkText("Forgot Password")` | Links with **exact** visible text |
| 6 | **Partial Link Text** | `By.partialLinkText("Forgot")` | Links with **part** of the text |
| 7 | **CSS Selector** | `By.cssSelector("#username")` | Fast, powerful, used when ID/name missing |
| 8 | **XPath** | `By.xpath("//input[@id='username']")` | Most flexible — works when nothing else does |

**Priority order in real projects:**
> **ID → Name → CSS Selector → XPath** (use XPath when others fail or element is dynamic)

**CSS Selector quick patterns:**
```java
By.cssSelector("#username")              // # = id
By.cssSelector(".btn-submit")            // . = class
By.cssSelector("input[name='email']")    // tag[attribute='value']
By.cssSelector("input[placeholder*='mail']")  // *= contains
```

---

## 3. XPath 

### What is XPath?
- **XML Path** — a way to travel through the **HTML structure** (like folders: parent → child) to find an element.
- Works even when the element has **no id, no name, no class**.

### Two Types of XPath

| Type | Starts with | Example | Note |
|---|---|---|---|
| **Absolute XPath** | `/` from root | `/html/body/div[2]/form/input[1]` |  Avoid — breaks if page structure changes |
| **Relative XPath** | `//` anywhere | `//input[@id='username']` |  Always use this |

---
## 4. Identify Elements and Objects

### How to identify an element manually (everyday practice):
1. Open the page → **Right-click** the element → **Inspect** (opens DevTools).
2. Look at the highlighted **HTML** for attributes: `id`, `name`, `class`, `type`, etc.
3. Press **Ctrl + F** inside DevTools → type your locator → it shows if it matches **1 element** (must be unique!).
4. Tools that help: **SelectorsHub**, **ChroPath** (browser extensions that auto-generate XPath/CSS).

### findElement vs findElements

| `findElement()` | `findElements()` |
|---|---|
| Returns **one** WebElement | Returns a **List** of WebElements |
| Throws error if not found | Returns **empty list** (no error) |
| Use for a single element | Use for counting links, rows, checkboxes |

**Example — count all links on a page:**
```java
List<WebElement> links = driver.findElements(By.tagName("a"));
System.out.println("Total links: " + links.size());
```

### What makes a GOOD locator? 
- **Unique** — matches exactly 1 element.
- **Stable** — doesn't change when page reloads (avoid auto-generated ids like `ext-gen-1045`).
- **Short** — shorter XPath breaks less.
- **Meaningful** — based on real attributes (id, name), not positions (`div[3]/div[1]`).
