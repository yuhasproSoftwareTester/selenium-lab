# Selenium Notes 

## 1. Selenium Components

Selenium is not a single tool — it's a **suite of 4 components**:

| Component | What it does |
|---|---|
| **Selenium IDE** | A browser extension (Chrome/Firefox) to **record and playback** tests. No coding needed. Good for beginners and quick prototypes. |
| **Selenium RC (Remote Control)** | The **old/legacy** tool. Used a server to inject JavaScript into the browser. Now **deprecated** (replaced by WebDriver). |
| **Selenium WebDriver** | The **core and most used** component. Automates the browser directly through code (Java, Python, C#, etc.). |
| **Selenium Grid** | Runs tests **in parallel** on multiple machines and browsers at the same time — saves time. |

---

## 2. How Selenium Differs from Other Automation Tools (e.g., QTP/UFT)

| Selenium | Other Tools (QTP/UFT) |
|---|---|
| **Free & open source** | Paid / licensed |
| Supports **many languages** (Java, Python, C#, Ruby, JS) | Mostly VBScript only |
| Works on **all major browsers** (Chrome, Firefox, Edge, Safari) | Limited browser support |
| Runs on **Windows, Mac, Linux** | Mostly Windows only |
| Automates **web applications only** | Can automate desktop apps too |
| Huge **community support** | Vendor support only |

---

## 3. Advantages of Selenium

1. **Free and open source** — no license cost.
2. **Multi-language support** — Java, Python, C#, Ruby, JavaScript.
3. **Multi-browser support** — Chrome, Firefox, Edge, Safari.
4. **Multi-platform** — Windows, macOS, Linux.
5. **Parallel execution** — using Selenium Grid (faster testing).
6. **Integrates easily** with frameworks like TestNG, JUnit, Maven, Jenkins (CI/CD).
7. **Large community** — easy to find help and resources.
8. **Flexible** — can be combined with other tools (e.g., AutoIT, Sikuli).

---

## 4. Selenium Architecture (Overview)

Selenium works on a simple flow:

```
Test Script (Java/Python…)  →  WebDriver  →  Browser Driver  →  Browser
```

- **Test Script** — your code with test steps.
- **WebDriver** — converts your commands into a form the browser understands.
- **Browser Driver** — a middleman specific to each browser (ChromeDriver, GeckoDriver, etc.).
- **Browser** — executes the actions and returns the result.

---

## 5. Selenium RC Architecture (Old)

RC had **two parts**:
1. **Selenium RC Server** — had to be **started manually** before running tests. It injected **JavaScript** into the browser to control it.
2. **Client Libraries** — for writing test scripts in different languages.

**Flow:**
```
Test Script → RC Server → Injects JavaScript → Browser
```

**Drawbacks of RC:**
- Server must be started before every test.
- Communication was **slow** (extra server layer).
- JavaScript injection caused **security limitations** (same-origin policy issues).
- Complex and not a real browser-like interaction.

*(RC is now deprecated — learn it only for theory/exams.)*

---

## 6. WebDriver Architecture (Modern)

WebDriver talks to the browser **directly** — no server needed.

**Components:**
1. **Client Library / Language Binding** (Java, Python, etc.) — your test script.
2. **JSON Wire Protocol / W3C Protocol** — converts commands into HTTP requests.
3. **Browser Driver** (ChromeDriver, GeckoDriver, EdgeDriver) — receives commands.
4. **Real Browser** — performs actions and sends the response back.

**Flow:**
```
Test Script → Browser Driver (via HTTP) → Real Browser → Response back
```

Key point: each browser has its **own driver**, and the browser treats commands as if a **real user** is operating it.

---

## 7. WebDriver vs Selenium RC

| Selenium RC | WebDriver |
|---|---|
| Needs a **separate server** to be started | **No server** needed |
| Controls browser via **JavaScript injection** | Talks to browser **directly** |
| **Slow** execution | **Faster** execution |
| Complex architecture | **Simple** architecture |
| Limited by same-origin policy | No such limitation |
| Cannot handle **mouse/keyboard events** realistically | Supports realistic user actions |
| **Deprecated** | Current standard (part of Selenium) |

---

## 8. Advantages of WebDriver 

1. **Direct communication** with the browser — faster than RC.
2. **Simple, compact API** — easy to learn and write code.
3. **No server installation/startup** required.
4. **Realistic user simulation** — handles keyboard, mouse, dropdowns, alerts, pop-ups.
5. **Supports dynamic web pages** (AJAX elements).
6. **Multiple browsers and languages** supported.
7. Can **take screenshots**, handle frames, windows, and cookies easily.
