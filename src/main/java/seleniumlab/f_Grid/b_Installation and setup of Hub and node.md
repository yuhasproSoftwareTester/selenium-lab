# Selenium Grid 4 - Installation and Setup

## Prerequisites

- Java JDK 8 or higher installed
- `JAVA_HOME` environment variable set
- Chrome, Firefox, or Edge browsers installed on the node machines
- ChromeDriver, GeckoDriver, or EdgeDriver downloaded and placed in system PATH

---

## Step 1: Download Selenium Server

Download the latest `selenium-server-4.x.x.jar` from the official Selenium website:

```
https://www.selenium.dev/downloads/
```

Place the JAR file in a folder, for example:
```
C:\selenium\selenium-server-4.15.2.jar
```

---

## Method 1: Standalone Mode (Single Machine)

This is the easiest way. It starts a hub and a node together on the same machine.

Open a terminal and run:

```bash
java -jar selenium-server-4.15.2.jar standalone
```

By default, the Grid runs at:
```
http://localhost:4444
```

Open a browser and visit `http://localhost:4444` to see the Grid console.

---

## Method 2: Hub and Nodes on Separate Machines

### Step 2: Start the Hub

On the central machine (Hub), run:

```bash
java -jar selenium-server-4.15.2.jar hub
```

The hub starts and listens on port 4444 by default.

---

### Step 3: Start a Node

On another machine (Node), run:

```bash
java -jar selenium-server-4.15.2.jar node --hub http://<HUB_IP>:4444
```

Replace `<HUB_IP>` with the actual IP address of the hub machine.

Example:
```bash
java -jar selenium-server-4.15.2.jar node --hub http://192.168.1.10:4444
```

You can start multiple nodes on different machines using the same command.

---

## Step 4: Verify the Grid

Open a browser and go to:
```
http://<HUB_IP>:4444/ui
```

You will see:
- The hub status
- List of connected nodes
- Available browsers and sessions

---

## Step 5: Run a Test on the Grid

```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.chrome.ChromeOptions;
import org.openqa.selenium.remote.RemoteWebDriver;
import java.net.URL;

public class GridTest {
    public static void main(String[] args) throws Exception {
        ChromeOptions options = new ChromeOptions();

        WebDriver driver = new RemoteWebDriver(
            new URL("http://localhost:4444/wd/hub"),
            options
        );

        driver.get("https://www.google.com");
        System.out.println("Title: " + driver.getTitle());

        driver.quit();
    }
}
```

If the Grid is running, the test executes on a connected node instead of your local browser.

---

## Common Commands Summary

| Command | Purpose |
|---------|---------|
| `java -jar selenium-server.jar standalone` | Start hub and node together |
| `java -jar selenium-server.jar hub` | Start only the hub |
| `java -jar selenium-server.jar node --hub http://IP:4444` | Connect a node to the hub |


---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| `Connection refused` | Check if the hub is running and the IP is correct |
| `Session not created` | Ensure browser drivers are in the system PATH on the node |
| `Port 4444 already in use` | Kill the existing process or use `--port 4445` |
| Node not visible on console | Check firewall settings and ensure ports are open |

---

## Folder Structure Example

```
C:\selenium\
    selenium-server-4.15.2.jar
    chromedriver.exe
    geckodriver.exe
    msedgedriver.exe
```

Make sure all driver executables are either in this folder and added to PATH, or placed in a folder already in your system PATH.

---

Once the Grid is running and the node is connected, you can run hundreds of tests in parallel across multiple machines and browsers.

---

<style>
.grid-playground {
    max-width: 700px;
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 8px;
}

.grid-section {
    margin-bottom: 22px;
}

.grid-section label {
    display: block;
    margin-bottom: 6px;
    font-weight: 500;
}

.grid-input,
.grid-select {
    padding: 9px;
    width: 300px;
    border: 1px solid #999;
    border-radius: 5px;
}

.grid-button {
    padding: 9px 18px;
    border: none;
    border-radius: 5px;
    background: #1976d2;
    color: white;
    cursor: pointer;
    margin-top: 10px;
}

.grid-button:hover {
    background: #1565c0;
}

.grid-result {
    margin-top: 12px;
    padding: 10px;
    background: #f3f3f3;
    border-radius: 5px;
}

.grid-status {
    font-weight: bold;
}
</style>

<div class="grid-playground">

    <h3>Selenium Grid Playground</h3>

    <!-- Grid Connection -->

    <div class="grid-section">

        <label for="hubUrl">
            Grid Hub URL
        </label>

        <input
            id="hubUrl"
            class="grid-input"
            type="text"
            value="http://localhost:4444">

        <br>

        <button
            id="checkGrid"
            type="button"
            class="grid-button">

            Check Grid

        </button>

        <div
            id="gridResult"
            class="grid-result">

            Grid status: Not checked

        </div>

    </div>


    <!-- Node Command -->

    <div class="grid-section">

        <h4>Node Configuration</h4>

        <label for="nodeIp">
            Hub IP
        </label>

        <input
            id="nodeIp"
            class="grid-input"
            type="text"
            value="192.168.1.10">

        <br>

        <label for="browser">
            Browser
        </label>

        <select
            id="browser"
            class="grid-select">

            <option value="chrome">
                Chrome
            </option>

            <option value="firefox">
                Firefox
            </option>

            <option value="MicrosoftEdge">
                Edge
            </option>

        </select>

        <br>

        <button
            id="generateNode"
            type="button"
            class="grid-button">

            Generate Node Command

        </button>

        <div
            id="nodeResult"
            class="grid-result">
        </div>

    </div>


    <!-- Remote Test -->

    <div class="grid-section">

        <h4>Remote Test</h4>

        <label for="remoteBrowser">
            Browser
        </label>

        <select
            id="remoteBrowser"
            class="grid-select">

            <option value="ChromeOptions">
                Chrome
            </option>

            <option value="FirefoxOptions">
                Firefox
            </option>

            <option value="EdgeOptions">
                Edge
            </option>

        </select>

        <br>

        <button
            id="generateRemote"
            type="button"
            class="grid-button">

            Generate RemoteWebDriver Code

        </button>

        <div
            id="remoteResult"
            class="grid-result">
        </div>

    </div>

</div>

<script>

document
    .getElementById("checkGrid")
    .addEventListener("click", function () {

        const url =
            document.getElementById("hubUrl").value.trim();

        const result =
            document.getElementById("gridResult");

        result.innerHTML =
            "Grid URL to verify:<br><br>" +
            "<strong>" + url + "</strong>" +
            "<br><br>" +
            "Open this URL in your browser and check the Grid console.";

    });


document
    .getElementById("generateNode")
    .addEventListener("click", function () {

        const ip =
            document.getElementById("nodeIp").value.trim();

        const browser =
            document.getElementById("browser").value;

        document
            .getElementById("nodeResult")
            .innerHTML =
            "<strong>Node Command:</strong><br><br>" +

            "java -jar selenium-server-4.x.x.jar " +
            "node --hub http://" +
            ip +
            ":4444" +

            "<br><br>" +

            "Browser: " +
            browser;

    });


document
    .getElementById("generateRemote")
    .addEventListener("click", function () {

        const browser =
            document.getElementById("remoteBrowser").value;

        document
            .getElementById("remoteResult")
            .innerHTML =
            "<strong>RemoteWebDriver Example:</strong><br><br>" +

            "WebDriver driver = new RemoteWebDriver(" +
            "<br>" +
            "    new URL(\"http://localhost:4444/wd/hub\")," +
            "<br>" +
            "    new " + browser + "()" +
            "<br>" +
            ");";

    });

</script>
<div class="grid-section">

    <h3>Grid Console</h3>

    <p>
        Start Selenium Grid first, then open the Grid Console.
    </p>

    <a
        href="http://localhost:4444/ui"
        target="_blank"
        class="grid-button"
        style="display:inline-block;text-decoration:none;">

        Open Selenium Grid Console

    </a>

</div>