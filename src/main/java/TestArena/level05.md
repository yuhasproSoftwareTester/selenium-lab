# Level 05 — Radio Buttons & Checkboxes

## Mission

Before attempting this level, enter the unlock key from **Level 04**.After unlocking, complete the testing profile using Selenium.

**Requirements**

- Select **Java** as the programming language.
- Select **Selenium WebDriver** as the automation tool.
- Submit the form.

---

## Unlock Level 05

<style>
.selenium-game {
    font-size: 13px;
}

.selenium-game button {
    padding: 6px 11px;
    margin: 3px 4px 3px 0;
    border: 1px solid #cbd5e1;
    border-radius: 5px;
    background: #e5e7eb;
    color: #1f2937;
    font-size: 12px;
    cursor: pointer;
}

.selenium-game button:hover {
    background: #d1d5db;
}

.selenium-game .primary-button {
    background: #2563eb;
    color: white;
    border-color: #2563eb;
}

.selenium-game .primary-button:hover {
    background: #1d4ed8;
}

.selenium-game .reset-button {
    background: #dc2626;
    color: white;
    border-color: #dc2626;
}

.selenium-game .reset-button:hover {
    background: #b91c1c;
}

.selenium-game input[type="text"] {
    width: 100%;
    max-width: 320px;
    padding: 6px 8px;
    margin: 3px 0 7px;
    border: 1px solid #cbd5e1;
    border-radius: 5px;
    font-size: 12px;
    box-sizing: border-box;
}

.selenium-game .game-message {
    margin: 7px 0;
    font-size: 12px;
}

.selenium-game .success {
    color: #16a34a;
    font-weight: 600;
}

.selenium-game .error {
    color: #dc2626;
    font-weight: 600;
}

.selenium-game .key-box {
    display: none;
    max-width: 430px;
    margin-top: 10px;
    padding: 9px 11px;
    border-left: 3px solid #16a34a;
    background: #f0fdf4;
    font-size: 12px;
}

.selenium-game .key-box p {
    margin: 5px 0;
}

.selenium-game .key {
    font-family: monospace;
    font-weight: bold;
}

.selenium-game .challenge-locked {
    opacity: 0.45;
}

.selenium-game .option-group {
    margin: 10px 0;
}

.selenium-game .option-group p {
    margin: 0 0 5px;
    font-weight: 600;
    font-size: 13px;
}

.selenium-game .option {
    display: block;
    margin: 5px 0;
    font-size: 12px;
}

.selenium-game .option input {
    margin-right: 6px;
}
</style>

<div class="selenium-game">

<input
    type="text"
    id="levelKey"
    placeholder="Enter Level 04 Key"
    autocomplete="off"
>

<button
    type="button"
    id="unlockBtn"
    class="primary-button">
    Unlock Challenge
</button>

<button
    type="button"
    id="resetBtn"
    class="reset-button">
    Reset
</button>

<p
    id="unlockMsg"
    class="game-message">
</p>

</div>

---

## Challenge Playground

Complete the testing profile.

<div
    id="challenge"
    class="selenium-game challenge-locked">

<div class="option-group">

<p>Programming Language</p>

<label class="option">

<input
    type="radio"
    name="language"
    id="languageJava"
    value="java"
    disabled
>

Java

</label>

<label class="option">

<input
    type="radio"
    name="language"
    id="languagePython"
    value="python"
    disabled
>

Python

</label>

<label class="option">

<input
    type="radio"
    name="language"
    id="languageJavaScript"
    value="javascript"
    disabled
>

JavaScript

</label>

</div>

<div class="option-group">

<p>Automation Tools</p>

<label class="option">

<input
    type="checkbox"
    id="seleniumTool"
    value="selenium"
    disabled
>

Selenium WebDriver

</label>

<label class="option">

<input
    type="checkbox"
    id="testngTool"
    value="testng"
    disabled
>

TestNG

</label>

<label class="option">

<input
    type="checkbox"
    id="cucumberTool"
    value="cucumber"
    disabled
>

Cucumber

</label>

</div>

<button
    type="button"
    id="submitProfile"
    class="primary-button"
    disabled>
    Submit Profile
</button>

<p
    id="profileMsg"
    class="game-message">
</p>

<div
    id="nextKey"
    class="key-box">

<strong>Level 05 Completed</strong>

<p>
Congratulations! You completed Level 05.
</p>

<p>
Use this key to unlock Level 06:
</p>

<span class="key">
SEL-05-B7K3-Q9M6
</span>

</div>

</div>

<script>
(function () {

    const LEVEL4_KEY =
        "SEL-04-H3T7-M9Q2";

    const unlockBtn =
        document.getElementById("unlockBtn");

    const resetBtn =
        document.getElementById("resetBtn");

    const keyInput =
        document.getElementById("levelKey");

    const unlockMsg =
        document.getElementById("unlockMsg");

    const challenge =
        document.getElementById("challenge");

    const javaRadio =
        document.getElementById("languageJava");

    const pythonRadio =
        document.getElementById("languagePython");

    const javascriptRadio =
        document.getElementById("languageJavaScript");

    const seleniumCheckbox =
        document.getElementById("seleniumTool");

    const testngCheckbox =
        document.getElementById("testngTool");

    const cucumberCheckbox =
        document.getElementById("cucumberTool");

    const submitButton =
        document.getElementById("submitProfile");

    const profileMsg =
        document.getElementById("profileMsg");

    const nextKey =
        document.getElementById("nextKey");


    const challengeInputs = [
        javaRadio,
        pythonRadio,
        javascriptRadio,
        seleniumCheckbox,
        testngCheckbox,
        cucumberCheckbox
    ];


    function lockChallenge() {

        challengeInputs.forEach(
            function (input) {
                input.disabled = true;
            }
        );

        submitButton.disabled = true;

        challenge.classList.add(
            "challenge-locked"
        );
    }


    function unlockChallenge() {

        challengeInputs.forEach(
            function (input) {
                input.disabled = false;
            }
        );

        submitButton.disabled = false;

        challenge.classList.remove(
            "challenge-locked"
        );
    }


    lockChallenge();


    unlockBtn.addEventListener(
        "click",
        function () {

            const enteredKey =
                keyInput.value.trim();

            if (enteredKey === LEVEL4_KEY) {

                unlockChallenge();

                unlockMsg.className =
                    "game-message success";

                unlockMsg.textContent =
                    "Level 05 unlocked.";

            } else {

                lockChallenge();

                unlockMsg.className =
                    "game-message error";

                unlockMsg.textContent =
                    "Invalid key.";
            }
        }
    );


    submitButton.addEventListener(
        "click",
        function () {

            const correctLanguage =
                javaRadio.checked;

            const correctTool =
                seleniumCheckbox.checked;

            const wrongLanguage =
                pythonRadio.checked ||
                javascriptRadio.checked;


            if (
                correctLanguage &&
                correctTool &&
                !wrongLanguage
            ) {

                profileMsg.className =
                    "game-message success";

                profileMsg.textContent =
                    "Correct profile submitted.";

                nextKey.style.display =
                    "block";

            } else {

                profileMsg.className =
                    "game-message error";

                profileMsg.textContent =
                    "Incorrect selection. Check your profile and try again.";

                nextKey.style.display =
                    "none";
            }
        }
    );


    resetBtn.addEventListener(
        "click",
        function () {

            keyInput.value = "";

            javaRadio.checked = false;
            pythonRadio.checked = false;
            javascriptRadio.checked = false;

            seleniumCheckbox.checked = false;
            testngCheckbox.checked = false;
            cucumberCheckbox.checked = false;

            lockChallenge();

            unlockMsg.textContent = "";
            unlockMsg.className =
                "game-message";

            profileMsg.textContent = "";
            profileMsg.className =
                "game-message";

            nextKey.style.display =
                "none";
        }
    );

})();
</script>