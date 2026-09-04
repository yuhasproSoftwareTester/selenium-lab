# Level 19 — Semi Boss: Automation Workflow

<div class="selenium-game">

<p>
You have reached the first major boss challenge.
This challenge combines several Selenium skills from previous levels.
</p>

<div class="task-box">

<strong>Objective</strong>

<p>
Complete the entire automation workflow correctly.
You must interact with the application in the correct order and verify the required information before completing the challenge.
</p>

</div>

<h3>Challenge Access</h3>

<p>Enter the key from Level 18:</p>

<input id="levelKey" type="text" placeholder="Enter Level 18 key">

<button id="unlockButton">Unlock Challenge</button>

<p id="unlockMessage"></p>

<div id="challenge" class="challenge-locked">

<h3>Automation Workflow</h3>

<div class="task-box">

<strong>Step 1 — Login</strong>

<p>
Username:
<code>bossuser</code>
</p>

<p>
Password:
<code>seleniumBoss123</code>
</p>

<input id="username" type="text" placeholder="Username">
<br><br>
<input id="password" type="password" placeholder="Password">

</div>

<div class="task-box">

<strong>Step 2 — Select Department</strong>

<p>
Select <strong>QA Automation</strong>.
</p>

<select id="department">
    <option value="">-- Select Department --</option>
    <option value="development">Development</option>
    <option value="qa">QA Automation</option>
    <option value="devops">DevOps</option>
</select>

</div>

<div class="task-box">

<strong>Step 3 — Enable Automation Tools</strong>

<p>Select both required tools:</p>

<label>
    <input type="checkbox" id="seleniumTool">
    Selenium WebDriver
</label>

<br>

<label>
    <input type="checkbox" id="testngTool">
    TestNG
</label>

</div>

<div class="task-box">

<strong>Step 4 — Find the Correct Test</strong>

<p>
The test table contains multiple tests.
Find the row where:
</p>

<ul>
<li>Test Name = Login Validation</li>
<li>Framework = Selenium</li>
<li>Status = Ready</li>
</ul>

<p>
Click <strong>Run Test</strong> in that row.
</p>

<table id="testTable">
<thead>
<tr>
    <th>Test Name</th>
    <th>Framework</th>
    <th>Status</th>
    <th>Action</th>
</tr>
</thead>

<tbody>

<tr>
    <td>Login Validation</td>
    <td>JUnit</td>
    <td>Ready</td>
    <td><button class="run-test">Run Test</button></td>
</tr>

<tr>
    <td>Checkout Validation</td>
    <td>Selenium</td>
    <td>Completed</td>
    <td><button class="run-test">Run Test</button></td>
</tr>

<tr>
    <td>Login Validation</td>
    <td>Selenium</td>
    <td>Ready</td>
    <td><button class="run-test">Run Test</button></td>
</tr>

<tr>
    <td>Search Validation</td>
    <td>Selenium</td>
    <td>Ready</td>
    <td><button class="run-test">Run Test</button></td>
</tr>

</tbody>
</table>

<p id="testMessage"></p>

</div>

<div class="task-box">

<strong>Step 5 — Wait for Test Result</strong>

<p>
After the correct test is started, the test result will appear after a short delay.
</p>

<p id="testResult" style="display:none;">
<strong>Test Result:</strong> PASSED
</p>

<p>
Verify that the result is <strong>PASSED</strong>.
</p>

</div>

<div class="task-box">

<strong>Step 6 — Final Verification</strong>

<p>
After completing all previous steps, click the verification button.
</p>

<button id="verifyBoss">Complete Semi Boss</button>

<p id="result"></p>

<div id="bossKey" style="display:none;">

<p><strong>Congratulations!</strong></p>

<p>You defeated the Semi Boss.</p>

<p>Your Level 20 key is:</p>

<div class="key-box">
    SEL-19-BOSS-X7K4-M2P9
</div>

<p>
Use this key to unlock the FINAL BOSS.
</p>

</div>

</div>

<button id="resetButton">Reset</button>

</div>

<style>
.selenium-game {
    font-size: 13px;
}

.selenium-game button {
    padding: 5px 10px;
    font-size: 12px;
    cursor: pointer;
}

.selenium-game input,
.selenium-game select {
    max-width: 320px;
    padding: 6px 8px;
    font-size: 12px;
}

.selenium-game .task-box {
    max-width: 600px;
    margin: 7px 0;
    padding: 8px 10px;
    border: 1px solid #ddd;
    border-radius: 6px;
}

.selenium-game table {
    border-collapse: collapse;
    margin-top: 8px;
}

.selenium-game th,
.selenium-game td {
    padding: 5px 8px;
    border: 1px solid #ccc;
}

.selenium-game .challenge-locked {
    opacity: .45;
}

.selenium-game .key-box {
    display: inline-block;
    padding: 7px 10px;
    margin-top: 5px;
    border: 1px solid #ccc;
    border-radius: 5px;
    font-family: monospace;
    font-weight: bold;
}

.selenium-game #unlockMessage,
.selenium-game #testMessage,
.selenium-game #result {
    font-size: 12px;
    margin: 6px 0;
}
</style>

<script>
(function () {

    const previousKey = "SEL-18-J4P7-R9K2";
    const nextKey = "SEL-19-BOSS-X7K4-M2P9";

    const levelKey = document.getElementById("levelKey");
    const unlockButton = document.getElementById("unlockButton");
    const unlockMessage = document.getElementById("unlockMessage");
    const challenge = document.getElementById("challenge");

    const username = document.getElementById("username");
    const password = document.getElementById("password");
    const department = document.getElementById("department");

    const seleniumTool = document.getElementById("seleniumTool");
    const testngTool = document.getElementById("testngTool");

    const testButtons = document.querySelectorAll(".run-test");
    const testMessage = document.getElementById("testMessage");
    const testResult = document.getElementById("testResult");

    const verifyBoss = document.getElementById("verifyBoss");
    const result = document.getElementById("result");
    const bossKey = document.getElementById("bossKey");
    const resetButton = document.getElementById("resetButton");

    let testStarted = false;
    let correctTestRun = false;

    function setChallengeEnabled(enabled) {

        const controls = challenge.querySelectorAll(
            "input, select, button"
        );

        controls.forEach(control => {
            control.disabled = !enabled;
        });

        if (enabled) {
            challenge.classList.remove("challenge-locked");
        } else {
            challenge.classList.add("challenge-locked");
        }
    }

    setChallengeEnabled(false);

    unlockButton.addEventListener("click", function () {

        if (levelKey.value.trim() === previousKey) {

            unlockMessage.textContent =
                "Correct key. Semi Boss unlocked.";

            challenge.classList.remove("challenge-locked");

            const controls = challenge.querySelectorAll(
                "input, select, button"
            );

            controls.forEach(control => {
                control.disabled = false;
            });

        } else {

            unlockMessage.textContent =
                "Incorrect key.";

        }

    });

    testButtons.forEach(function (button) {

        button.addEventListener("click", function () {

            const row = button.closest("tr");

            const cells = row.querySelectorAll("td");

            const testName = cells[0].textContent.trim();
            const framework = cells[1].textContent.trim();
            const status = cells[2].textContent.trim();

            testStarted = true;

            if (
                testName === "Login Validation" &&
                framework === "Selenium" &&
                status === "Ready"
            ) {

                correctTestRun = true;

                testMessage.textContent =
                    "Correct test selected. Running test...";

                testResult.style.display = "none";

                setTimeout(function () {

                    testResult.style.display = "block";

                    testMessage.textContent =
                        "Test execution completed.";

                }, 3000);

            } else {

                correctTestRun = false;

                testMessage.textContent =
                    "Wrong test selected.";

            }

        });

    });

    verifyBoss.addEventListener("click", function () {

        if (
            username.value === "bossuser" &&
            password.value === "seleniumBoss123" &&
            department.value === "qa" &&
            seleniumTool.checked &&
            testngTool.checked &&
            testStarted &&
            correctTestRun &&
            testResult.style.display === "block"
        ) {

            result.textContent =
                "SEMI BOSS DEFEATED.";

            bossKey.style.display = "block";

            verifyBoss.disabled = true;

        } else {

            result.textContent =
                "Workflow incomplete. Check every step.";

        }

    });

    resetButton.addEventListener("click", function () {

        location.reload();

    });

})();
</script>