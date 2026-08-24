# Selenium Grid - Introduction

## What is Selenium Grid

Selenium Grid is a server that allows you to run tests on multiple machines and browsers in parallel. Instead of running tests one by one on your local machine, Grid distributes them across different computers, operating systems, and browser versions.

---

## Why Use It

| Reason | Explanation |
|--------|-------------|
| Parallel Execution | Run many tests at the same time, reducing total execution time. |
| Cross-Browser Testing | Test on Chrome, Firefox, Edge, Safari simultaneously. |
| Cross-Platform Testing | Run tests on Windows, Linux, and macOS from one machine. |
| Resource Utilization | Use old or spare computers as test nodes. |
| Scalability | Add more machines to the grid as your test suite grows. |

---

## How It Works

- **Hub**: The central server that receives test requests and assigns them to available nodes.
- **Node**: A machine connected to the hub that actually runs the browser and executes the test.
- **Client**: Your test script that sends commands to the hub instead of a local browser.

```
Your Test Script  -->  Hub  -->  Node 1 (Chrome on Windows)
                         -->  Node 2 (Firefox on Linux)
                         -->  Node 3 (Safari on macOS)
```

---

## Simple Analogy

Think of a call center. The hub is the operator who receives all calls. The nodes are the agents who handle the actual work. The caller does not need to know which agent answers. The operator routes the call to whoever is free.

---

## When to Use It

- Your test suite takes hours to run and you need faster feedback
- You need to verify the same test across multiple browsers
- Your team has multiple machines available to share the load
- You want to run tests on a browser or OS that your local machine does not support

---

## When Not to Use It

- You have only a few tests that run quickly on one browser
- You do not have multiple machines or virtual machines available
- Setting up and maintaining nodes is more effort than the time saved

---

## Quick Setup (Selenium 4)

Selenium 4 combines hub and node into one command. You no longer need to start them separately.

**Start the Grid server:**
```
java -jar selenium-server-4.x.x.jar standalone
```

**Connect your test to the Grid:**

```java
ChromeOptions options = new ChromeOptions();
WebDriver driver = new RemoteWebDriver(new URL("http://localhost:4444"), options);
```

The test runs on the Grid instead of your local browser.

---

## Grid 4 vs Grid 3

| Feature | Grid 3 | Grid 4 |
|---------|--------|--------|
| Setup | Separate hub and node commands | Single standalone command |
| Architecture | Hub-Node only | Hub, Node, Distributor, Router, Session Queue |
| Docker Support | Manual | Built-in Docker support |
| Kubernetes | Not supported | Native support |

---

## Key Terms

| Term | Meaning |
|------|---------|
| Hub | Central command center that routes tests |
| Node | Machine that runs the actual browser |
| Session | One active test running on a node |
| Capabilities | Browser name, version, and platform you request |
| RemoteWebDriver | The class used to connect to the Grid |
---

Selenium Grid is essential when you need speed and coverage across many environments. For small projects, local execution is enough. For large teams and CI/CD pipelines, Grid is the standard solution.

---