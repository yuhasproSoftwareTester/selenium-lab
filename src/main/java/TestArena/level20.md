# Level 20 — FINAL BOSS: Selenium Automation Master

<div class="selenium-game">

<p>
This is the final challenge of the Selenium Lab.
</p>

<div class="task-box">

<strong>Mission</strong>

<p>
You are working as a QA Automation Engineer.
Your job is to automate the complete QA Automation Portal workflow.
</p>

<p>
This challenge combines the Selenium techniques you learned throughout
the previous levels.
</p>

<p>
<strong>Important:</strong> You are not given the Selenium method you should
use for each task. Decide which Selenium technique is appropriate.
</p>

</div>

<h3>Challenge Access</h3>

<p>Enter the key from Level 19:</p>

<input id="levelKey" type="text" placeholder="Enter Level 19 key">

<button id="unlockButton">Unlock Final Boss</button>

<p id="unlockMessage"></p>

<div id="challenge" class="challenge-locked">

<div class="boss-banner">

<h3>QA AUTOMATION PORTAL</h3>

<p><strong>FINAL BOSS</strong></p>

</div>

<div class="task-box">

<strong>Mission Requirements</strong>

<p>Complete the following workflow:</p>

<ol>
<li>Login successfully.</li>
<li>Verify the login result.</li>
<li>Select the correct department.</li>
<li>Select the required testing language.</li>
<li>Select the required automation tools.</li>
<li>Find the correct product from multiple products.</li>
<li>Use mouse interaction on the product.</li>
<li>Use keyboard interaction in the search field.</li>
<li>Wait for the dynamic test control.</li>
<li>Handle the dynamically generated element.</li>
<li>Work with the iframe.</li>
<li>Reveal and verify the hidden value.</li>
<li>Handle JavaScript alerts.</li>
<li>Find the correct test in the table.</li>
<li>Verify the final report.</li>
<li>Complete the final submission.</li>
</ol>

<p>
The order of the application workflow matters.
</p>

</div>


<!-- LOGIN -->

<div class="task-box">

<strong>1. Automation Portal Login</strong>

<p>Login using:</p>

<p><strong>Username:</strong> finaluser</p>

<p><strong>Password:</strong> Selenium@2026</p>

<input id="username" type="text" placeholder="Username">

<br><br>

<input id="password" type="password" placeholder="Password">

<br><br>

<button id="loginButton">Login</button>

<p id="loginMessage"></p>

</div>


<!-- DEPARTMENT -->

<div class="task-box">

<strong>2. Test Configuration</strong>

<p>Select the department:</p>

<select id="department">
    <option value="">-- Select Department --</option>
    <option value="development">Development</option>
    <option value="devops">DevOps</option>
    <option value="qa">QA Automation</option>
    <option value="security">Security</option>
</select>

<p>Select the programming language:</p>

<label>
    <input type="radio" name="language" id="javaRadio" value="java">
    Java
</label>

<label>
    <input type="radio" name="language" id="pythonRadio" value="python">
    Python
</label>

<p>Select the required automation tools:</p>

<label>
    <input type="checkbox" id="seleniumCheckbox">
    Selenium
</label>

<br>

<label>
    <input type="checkbox" id="testngCheckbox">
    TestNG
</label>

<br>

<label>
    <input type="checkbox" id="cucumberCheckbox">
    Cucumber
</label>

</div>


<!-- SEARCH -->

<div class="task-box">

<strong>3. Product Search</strong>

<p>
Use the search field to locate the required automation product.
</p>

<p>
Required product:
<strong>Selenium WebDriver Mastery</strong>
</p>

<input id="searchBox"
       type="text"
       placeholder="Search automation products">

<div id="productList">

<div class="product-item"
     data-product="java">

<p class="product-name">Java Programming Guide</p>

<button class="product-action">Select</button>

</div>

<div class="product-item"
     data-product="selenium">

<p class="product-name">Selenium WebDriver Mastery</p>

<button class="product-action"
        id="seleniumProductButton">
Select
</button>

</div>

<div class="product-item"
     data-product="testng">

<p class="product-name">TestNG Testing Guide</p>

<button class="product-action">Select</button>

</div>

<div class="product-item"
     data-product="cucumber">

<p class="product-name">Cucumber BDD Guide</p>

<button class="product-action">Select</button>

</div>

</div>

<p id="productMessage"></p>

</div>


<!-- MOUSE -->

<div class="task-box">

<strong>4. Mouse Actions</strong>

<p>
Perform the required mouse interaction on the target below.
</p>

<div id="mouseTarget">

Double Click This Target

</div>

<p id="mouseMessage"></p>

</div>


<!-- KEYBOARD -->

<div class="task-box">

<strong>5. Keyboard Actions</strong>

<p>
The following field contains text that must be replaced using keyboard
interaction.
</p>

<input id="keyboardBox"
       type="text"
       value="WRONG VALUE">

<p>
Required value:
<strong>SELENIUM FINAL BOSS</strong>
</p>

<p>
Use keyboard actions to select and replace the existing text.
</p>

</div>


<!-- DYNAMIC -->

<div class="task-box">

<strong>6. Dynamic Test Control</strong>

<p>
A test control will appear after a short delay.
</p>

<div id="dynamicArea"></div>

<p id="dynamicMessage"></p>

</div>


<!-- IFRAME -->

<div class="task-box">

<strong>7. Automation Verification Frame</strong>

<p>
The verification form is located inside an iframe.
</p>

<iframe id="verificationFrame"
        title="Automation Verification Frame"
        srcdoc='
        <html>
        <body style="font-family:Arial;padding:10px;">
        <p><strong>Verification Frame</strong></p>

        <input id="frameInput"
               type="text"
               placeholder="Enter verification code">

        <button id="frameButton">
        Verify
        </button>

        <p id="frameMessage"></p>

        <script>
        document.getElementById("frameButton")
        .addEventListener("click", function(){

            const input =
                document.getElementById("frameInput").value;

            if(input === "FRAME-2026"){
                document.getElementById("frameMessage")
                .textContent = "FRAME VERIFIED";
            } else {
                document.getElementById("frameMessage")
                .textContent = "INVALID FRAME CODE";
            }

        });
        <\/script>

        </body>
        </html>
        '>
</iframe>

</div>


<!-- HIDDEN ELEMENT -->

<div class="task-box">

<strong>8. Hidden Security Token</strong>

<p>
A security token is hidden inside the page.
You must reveal it before verifying it.
</p>

<input id="hiddenToken"
       type="text"
       value="FINAL-SELENIUM-TOKEN"
       style="display:none;">

<button id="revealTokenButton">
Reveal Token
</button>

<button id="verifyTokenButton">
Verify Token
</button>

<p id="tokenMessage"></p>

</div>


<!-- ALERTS -->

<div class="task-box">

<strong>9. Security Alerts</strong>

<p>
The portal requires two security confirmations.
</p>

<button id="simpleAlertButton">
Security Alert
</button>

<button id="confirmAlertButton">
Security Confirmation
</button>

<p id="alertMessage"></p>

</div>


<!-- TABLE -->

<div class="task-box">

<strong>10. Test Execution Table</strong>

<p>
Find the test where:
</p>

<ul>
<li>Test Name = Checkout Validation</li>
<li>Framework = Selenium</li>
<li>Status = Ready</li>
</ul>

<p>
Run the test from the correct row.
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
    <td>Checkout Validation</td>
    <td>JUnit</td>
    <td>Ready</td>
    <td>
        <button class="runTest">Run Test</button>
    </td>
</tr>

<tr>
    <td>Login Validation</td>
    <td>Selenium</td>
    <td>Ready</td>
    <td>
        <button class="runTest">Run Test</button>
    </td>
</tr>

<tr>
    <td>Checkout Validation</td>
    <td>Selenium</td>
    <td>Completed</td>
    <td>
        <button class="runTest">Run Test</button>
    </td>
</tr>

<tr>
    <td>Checkout Validation</td>
    <td>Selenium</td>
    <td>Ready</td>
    <td>
        <button class="runTest">Run Test</button>
    </td>
</tr>

<tr>
    <td>Search Validation</td>
    <td>Selenium</td>
    <td>Ready</td>
    <td>
        <button class="runTest">Run Test</button>
    </td>
</tr>

</tbody>

</table>

<p id="tableMessage"></p>

<p id="testResult" style="display:none;">
<strong>Test Execution Result: PASSED</strong>
</p>

</div>


<!-- REPORT -->

<div class="task-box">

<strong>11. Final Automation Report</strong>

<div id="report">

<p>
<strong>Automation Test Report</strong>
</p>

<p>
Status:
<span id="reportStatus">PASSED</span>
</p>

<p>
Automation Score:
<span id="reportScore">100</span>
</p>

<p>
Framework:
<span id="reportFramework">Selenium WebDriver</span>
</p>

</div>

<p>
Verify the report information before completing the challenge.
</p>

</div>


<!-- FINAL -->

<div class="task-box">

<strong>12. Final Submission</strong>

<p>
You have completed the automation workflow.
Perform the final verification.
</p>

<button id="finalSubmit">
SUBMIT FINAL BOSS
</button>

<p id="finalMessage"></p>

<div id="finalKey" style="display:none;">

<p><strong>CONGRATULATIONS!</strong></p>

<p>
You have completed the Selenium Automation Lab.
</p>

<p>
<strong>FINAL BOSS DEFEATED</strong>
</p>

<div class="key-box">
SEL-20-FINAL-M9X7-BOSS
</div>

<p>
This is the final key.
There is no Level 21.
</p>

</div>

</div>


<button id="resetButton">
Reset Challenge
</button>

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
    max-width: 650px;
    margin: 7px 0;
    padding: 8px 10px;
    border: 1px solid #ddd;
    border-radius: 6px;
}

.selenium-game .challenge-locked {
    opacity: .45;
}

.selenium-game .boss-banner {
    max-width: 650px;
    margin: 10px 0;
    padding: 12px;
    text-align: center;
    border: 2px solid #777;
    border-radius: 6px;
}

.selenium-game .boss-banner h3 {
    margin: 2px 0;
}

.selenium-game .product-item {
    max-width: 450px;
    margin: 6px 0;
    padding: 7px 9px;
    border: 1px solid #ddd;
    border-radius: 5px;
}

.selenium-game .product-name {
    display: inline-block;
    min-width: 220px;
    margin: 0;
}

.selenium-game #mouseTarget {
    display: inline-block;
    padding: 18px 30px;
    margin: 8px 0;
    border: 2px solid #777;
    border-radius: 6px;
    cursor: pointer;
    user-select: none;
}

.selenium-game iframe {
    width: 100%;
    max-width: 500px;
    height: 130px;
    border: 1px solid #ccc;
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
.selenium-game #loginMessage,
.selenium-game #productMessage,
.selenium-game #mouseMessage,
.selenium-game #dynamicMessage,
.selenium-game #tokenMessage,
.selenium-game #alertMessage,
.selenium-game #tableMessage,
.selenium-game #finalMessage {
    font-size: 12px;
    margin: 6px 0;
}

</style>


<script>

(function () {

    const previousKey = "SEL-19-BOSS-X7K4-M2P9";
    const finalKey = "SEL-20-FINAL-M9X7-BOSS";

    const levelKey = document.getElementById("levelKey");
    const unlockButton = document.getElementById("unlockButton");
    const unlockMessage = document.getElementById("unlockMessage");

    const challenge = document.getElementById("challenge");

    const username = document.getElementById("username");
    const password = document.getElementById("password");
    const loginButton = document.getElementById("loginButton");
    const loginMessage = document.getElementById("loginMessage");

    const department = document.getElementById("department");
    const javaRadio = document.getElementById("javaRadio");
    const seleniumCheckbox =
        document.getElementById("seleniumCheckbox");

    const testngCheckbox =
        document.getElementById("testngCheckbox");

    const cucumberCheckbox =
        document.getElementById("cucumberCheckbox");

    const searchBox = document.getElementById("searchBox");
    const productItems =
        document.querySelectorAll(".product-item");

    const productMessage =
        document.getElementById("productMessage");

    const seleniumProductButton =
        document.getElementById("seleniumProductButton");

    const mouseTarget =
        document.getElementById("mouseTarget");

    const mouseMessage =
        document.getElementById("mouseMessage");

    const keyboardBox =
        document.getElementById("keyboardBox");

    const dynamicArea =
        document.getElementById("dynamicArea");

    const dynamicMessage =
        document.getElementById("dynamicMessage");

    const hiddenToken =
        document.getElementById("hiddenToken");

    const revealTokenButton =
        document.getElementById("revealTokenButton");

    const verifyTokenButton =
        document.getElementById("verifyTokenButton");

    const tokenMessage =
        document.getElementById("tokenMessage");

    const simpleAlertButton =
        document.getElementById("simpleAlertButton");

    const confirmAlertButton =
        document.getElementById("confirmAlertButton");

    const alertMessage =
        document.getElementById("alertMessage");

    const runTests =
        document.querySelectorAll(".runTest");

    const tableMessage =
        document.getElementById("tableMessage");

    const testResult =
        document.getElementById("testResult");

    const reportStatus =
        document.getElementById("reportStatus");

    const reportScore =
        document.getElementById("reportScore");

    const reportFramework =
        document.getElementById("reportFramework");

    const finalSubmit =
        document.getElementById("finalSubmit");

    const finalMessage =
        document.getElementById("finalMessage");

    const finalKeyBox =
        document.getElementById("finalKey");

    const resetButton =
        document.getElementById("resetButton");


    let loggedIn = false;
    let productSelected = false;
    let mouseCompleted = false;
    let dynamicCompleted = false;
    let frameCompleted = false;
    let tokenCompleted = false;

    let simpleAlertCompleted = false;
    let confirmAlertCompleted = false;

    let correctTestRun = false;
    let finalSubmitted = false;


    function setChallengeEnabled(enabled) {

        const controls =
            challenge.querySelectorAll(
                "input, select, button"
            );

        controls.forEach(function (control) {

            control.disabled = !enabled;

        });

        if (enabled) {

            challenge.classList.remove(
                "challenge-locked"
            );

        } else {

            challenge.classList.add(
                "challenge-locked"
            );

        }

    }


    setChallengeEnabled(false);


    /* UNLOCK */

    unlockButton.addEventListener(
        "click",
        function () {

            if (
                levelKey.value.trim() === previousKey
            ) {

                unlockMessage.textContent =
                    "Correct key. FINAL BOSS unlocked.";

                setChallengeEnabled(true);

            } else {

                unlockMessage.textContent =
                    "Incorrect Level 19 key.";

            }

        }
    );


    /* LOGIN */

    loginButton.addEventListener(
        "click",
        function () {

            if (
                username.value === "finaluser" &&
                password.value === "Selenium@2026"
            ) {

                loggedIn = true;

                loginMessage.textContent =
                    "Login successful.";

            } else {

                loggedIn = false;

                loginMessage.textContent =
                    "Invalid username or password.";

            }

        }
    );


    /* PRODUCT */

    productItems.forEach(
        function (item) {

            const button =
                item.querySelector(
                    ".product-action"
                );

            button.addEventListener(
                "click",
                function () {

                    const product =
                        item.dataset.product;

                    if (product === "selenium") {

                        productSelected = true;

                        productMessage.textContent =
                            "Correct product selected.";

                    } else {

                        productSelected = false;

                        productMessage.textContent =
                            "Wrong product.";

                    }

                }
            );

        }
    );


    /* MOUSE */

    mouseTarget.addEventListener(
        "dblclick",
        function () {

            mouseCompleted = true;

            mouseMessage.textContent =
                "Mouse action accepted.";

        }
    );


    /* DYNAMIC ELEMENT */

    setTimeout(
        function () {

            const randomId =
                "dynamic-" +
                Math.random()
                    .toString(36)
                    .substring(2, 9);

            const button =
                document.createElement("button");

            button.id = randomId;

            button.dataset.action =
                "final-dynamic";

            button.textContent =
                "Complete Dynamic Test";

            dynamicArea.appendChild(button);

            button.addEventListener(
                "click",
                function () {

                    dynamicCompleted = true;

                    dynamicMessage.textContent =
                        "Dynamic test completed.";

                }
            );

        },
        4000
    );


    /* HIDDEN TOKEN */

    revealTokenButton.addEventListener(
        "click",
        function () {

            hiddenToken.style.display =
                "inline-block";

        }
    );


    verifyTokenButton.addEventListener(
        "click",
        function () {

            if (
                hiddenToken.value ===
                "FINAL-SELENIUM-TOKEN"
            ) {

                tokenCompleted = true;

                tokenMessage.textContent =
                    "Security token verified.";

            } else {

                tokenCompleted = false;

                tokenMessage.textContent =
                    "Invalid security token.";

            }

        }
    );


    /* ALERT */

    simpleAlertButton.addEventListener(
        "click",
        function () {

            alert(
                "FINAL BOSS SECURITY ALERT"
            );

            simpleAlertCompleted = true;

            alertMessage.textContent =
                "Security alert handled.";

        }
    );


    /* CONFIRM */

    confirmAlertButton.addEventListener(
        "click",
        function () {

            const answer =
                confirm(
                    "Confirm final automation access?"
                );

            if (answer) {

                confirmAlertCompleted = true;

                alertMessage.textContent =
                    "Security confirmation accepted.";

            } else {

                confirmAlertCompleted = false;

                alertMessage.textContent =
                    "Security confirmation rejected.";

            }

        }
    );


    /* TEST TABLE */

    runTests.forEach(
        function (button) {

            button.addEventListener(
                "click",
                function () {

                    const row =
                        button.closest("tr");

                    const cells =
                        row.querySelectorAll("td");

                    const testName =
                        cells[0]
                            .textContent
                            .trim();

                    const framework =
                        cells[1]
                            .textContent
                            .trim();

                    const status =
                        cells[2]
                            .textContent
                            .trim();


                    if (
                        testName ===
                            "Checkout Validation" &&
                        framework ===
                            "Selenium" &&
                        status ===
                            "Ready"
                    ) {

                        correctTestRun = true;

                        tableMessage.textContent =
                            "Correct test selected. Executing...";

                        testResult.style.display =
                            "none";


                        setTimeout(
                            function () {

                                testResult.style.display =
                                    "block";

                                tableMessage.textContent =
                                    "Test execution completed.";

                            },
                            3000
                        );

                    } else {

                        correctTestRun = false;

                        tableMessage.textContent =
                            "Wrong test selected.";

                    }

                }
            );

        }
    );


    /* FINAL SUBMISSION */

    finalSubmit.addEventListener(
        "click",
        function () {

            const departmentCorrect =
                department.value === "qa";

            const languageCorrect =
                javaRadio.checked;

            const toolsCorrect =
                seleniumCheckbox.checked &&
                testngCheckbox.checked &&
                !cucumberCheckbox.checked;

            const keyboardCorrect =
                keyboardBox.value ===
                "SELENIUM FINAL BOSS";

            const reportCorrect =
                reportStatus.textContent.trim() ===
                    "PASSED" &&
                reportScore.textContent.trim() ===
                    "100" &&
                reportFramework.textContent.trim() ===
                    "Selenium WebDriver";


            if (
                loggedIn &&
                departmentCorrect &&
                languageCorrect &&
                toolsCorrect &&
                productSelected &&
                mouseCompleted &&
                keyboardCorrect &&
                dynamicCompleted &&
                frameCompleted &&
                tokenCompleted &&
                simpleAlertCompleted &&
                confirmAlertCompleted &&
                correctTestRun &&
                testResult.style.display === "block" &&
                reportCorrect
            ) {

                finalSubmitted = true;

                finalMessage.textContent =
                    "FINAL BOSS DEFEATED.";

                finalKeyBox.style.display =
                    "block";

                finalSubmit.disabled = true;

            } else {

                finalMessage.textContent =
                    "FINAL BOSS NOT COMPLETED. Check every requirement.";

            }

        }
    );


    /* FRAME DETECTION */

    const frame =
        document.getElementById(
            "verificationFrame"
        );

    frame.addEventListener(
        "load",
        function () {

            try {

                const frameDocument =
                    frame.contentDocument ||
                    frame.contentWindow.document;

                const frameButton =
                    frameDocument.getElementById(
                        "frameButton"
                    );

                const frameMessage =
                    frameDocument.getElementById(
                        "frameMessage"
                    );


                frameButton.addEventListener(
                    "click",
                    function () {

                        setTimeout(
                            function () {

                                if (
                                    frameMessage.textContent
                                    === "FRAME VERIFIED"
                                ) {

                                    frameCompleted =
                                        true;

                                }

                            },
                            50
                        );

                    }
                );

            } catch (e) {

                console.log(
                    "Frame initialization error"
                );

            }

        }
    );


    /* RESET */

    resetButton.addEventListener(
        "click",
        function () {

            location.reload();

        }
    );

})();

</script>

</div>