# Level 14 — Multi-Step Automation

## Mission

Complete all tasks in the correct order.

1. Select **QA Automation**.
2. Select **Selenium WebDriver**.
3. Enter **Selenium Automation Expert**.
4. Double-click **Double Click Me** using `Actions`.
5. Submit the challenge.

---

## Unlock Level 14

Enter the key obtained from **Level 13**.

<style>
.selenium-game {
    font-size: 13px;
}

.selenium-game button {
    padding: 5px 10px;
    margin: 3px 3px 3px 0;
    border: 1px solid #cbd5e1;
    border-radius: 4px;
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

.selenium-game .game-input,
.selenium-game select {
    width: 100%;
    max-width: 320px;
    padding: 6px 8px;
    margin: 3px 0 7px;
    border: 1px solid #cbd5e1;
    border-radius: 4px;
    font-size: 12px;
    box-sizing: border-box;
}

.selenium-game .game-input:focus,
.selenium-game select:focus {
    outline: none;
    border-color: #2563eb;
}

.selenium-game .task-box {
    max-width: 450px;
    margin: 7px 0;
    padding: 8px 10px;
    border: 1px solid #d1d5db;
    border-radius: 5px;
}

.selenium-game .task-title {
    font-size: 13px;
    font-weight: 600;
}

.selenium-game .game-message {
    margin: 5px 0;
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
    max-width: 450px;
    margin-top: 10px;
    padding: 8px 10px;
    border-left: 3px solid #16a34a;
    background: #f0fdf4;
    font-size: 12px;
}

.selenium-game .key-box p {
    margin: 5px 0;
}

.selenium-game .key {
    font-family: monospace;
    font-size: 12px;
    font-weight: bold;
}

.selenium-game .challenge-locked {
    opacity: 0.45;
}

.selenium-game .double-target {
    display: inline-block;
    padding: 7px 12px;
    margin: 3px 0;
    border: 1px dashed #94a3b8;
    border-radius: 5px;
    font-size: 12px;
    user-select: none;
}

.selenium-game p {
    margin: 5px 0;
}
</style>

<div class="selenium-game">

<input
    type="text"
    id="levelKey"
    class="game-input"
    placeholder="Enter Level 13 key"
    autocomplete="off"
>

<button
    type="button"
    id="unlockBtn"
    class="primary-button">
    Unlock
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

<div
    id="challenge"
    class="selenium-game challenge-locked">

    <div class="task-box">

        <div class="task-title">
            Task 1 — Department
        </div>

        <p>
            Select <strong>QA Automation</strong>.
        </p>

        <select
            id="department"
            disabled>

            <option value="">
                Select Department
            </option>

            <option value="development">
                Software Development
            </option>

            <option value="testing">
                Software Testing
            </option>

            <option value="qa">
                QA Automation
            </option>

            <option value="management">
                Management
            </option>

        </select>

        <p
            id="task1Status"
            class="game-message">
            Not completed
        </p>

    </div>


    <div class="task-box">

        <div class="task-title">
            Task 2 — Checkbox
        </div>

        <p>
            Select <strong>Selenium WebDriver</strong>.
        </p>

        <label>
            <input
                type="checkbox"
                id="seleniumCheckbox"
                disabled>

            Selenium WebDriver
        </label>

        <p
            id="task2Status"
            class="game-message">
            Not completed
        </p>

    </div>


    <div class="task-box">

        <div class="task-title">
            Task 3 — Text Input
        </div>

        <p>
            Enter <strong>Selenium Automation Expert</strong>.
        </p>

        <input
            type="text"
            id="textInput"
            class="game-input"
            disabled>

        <p
            id="task3Status"
            class="game-message">
            Not completed
        </p>

    </div>


    <div class="task-box">

        <div class="task-title">
            Task 4 — Double Click
        </div>

        <p>
            Double-click the target using
            <strong>Actions</strong>.
        </p>

        <div
            id="doubleClickTarget"
            class="double-target">

            Double Click Me

        </div>

        <p
            id="task4Status"
            class="game-message">
            Not completed
        </p>

    </div>


    <div class="task-box">

        <div class="task-title">
            Task 5 — Submit
        </div>

        <button
            type="button"
            id="submitChallenge"
            class="primary-button"
            disabled>
            Submit
        </button>

        <p
            id="task5Status"
            class="game-message">
            Complete all tasks first.
        </p>

    </div>


    <p
        id="mainStatus"
        class="game-message">
        Challenge locked.
    </p>


    <div
        id="nextKey"
        class="key-box">

        <strong>Level 14 Completed</strong>

        <p>
            All tasks completed successfully.
        </p>

        <p>
            Level 15 key:
        </p>

        <span class="key">
            SEL-14-Z6P3-M8K1
        </span>

    </div>

</div>

<script>
(function () {

    /*
     * ==========================================
     * LEVEL 14 — MULTI-STEP AUTOMATION
     * ==========================================
     *
     * LEVEL 13 KEY
     * SEL-13-D8K4-R6P2
     *
     * REQUIRED TEXT
     * Selenium Automation Expert
     *
     * REQUIRED DEPARTMENT
     * QA Automation
     *
     * REQUIRED CHECKBOX
     * Selenium WebDriver
     *
     * REQUIRED ACTION
     * Double Click using Actions
     *
     * LEVEL 15 KEY
     * SEL-14-Z6P3-M8K1
     * ==========================================
     */

    const LEVEL13_KEY =
        "SEL-13-D8K4-R6P2";

    const REQUIRED_TEXT =
        "Selenium Automation Expert";


    const levelKey =
        document.getElementById("levelKey");

    const unlockBtn =
        document.getElementById("unlockBtn");

    const resetBtn =
        document.getElementById("resetBtn");

    const unlockMsg =
        document.getElementById("unlockMsg");

    const challenge =
        document.getElementById("challenge");

    const department =
        document.getElementById("department");

    const seleniumCheckbox =
        document.getElementById(
            "seleniumCheckbox"
        );

    const textInput =
        document.getElementById("textInput");

    const doubleClickTarget =
        document.getElementById(
            "doubleClickTarget"
        );

    const submitChallenge =
        document.getElementById(
            "submitChallenge"
        );

    const task1Status =
        document.getElementById("task1Status");

    const task2Status =
        document.getElementById("task2Status");

    const task3Status =
        document.getElementById("task3Status");

    const task4Status =
        document.getElementById("task4Status");

    const task5Status =
        document.getElementById("task5Status");

    const mainStatus =
        document.getElementById("mainStatus");

    const nextKey =
        document.getElementById("nextKey");


    let unlocked = false;

    let task1Completed = false;
    let task2Completed = false;
    let task3Completed = false;
    let task4Completed = false;


    /*
     * ==========================================
     * LOCK CHALLENGE
     * ==========================================
     */

    function lockChallenge() {

        unlocked = false;

        challenge.classList.add(
            "challenge-locked"
        );

        department.disabled = true;
        seleniumCheckbox.disabled = true;
        textInput.disabled = true;
        submitChallenge.disabled = true;
    }


    /*
     * ==========================================
     * UNLOCK CHALLENGE
     * ==========================================
     */

    function unlockChallenge() {

        unlocked = true;

        challenge.classList.remove(
            "challenge-locked"
        );

        department.disabled = false;
        seleniumCheckbox.disabled = false;
        textInput.disabled = false;
        submitChallenge.disabled = false;
    }


    /*
     * ==========================================
     * INITIAL STATE
     * ==========================================
     */

    lockChallenge();


    /*
     * ==========================================
     * UNLOCK LEVEL 14
     * ==========================================
     */

    unlockBtn.addEventListener(
        "click",
        function () {

            const enteredKey =
                levelKey.value.trim();

            if (enteredKey === LEVEL13_KEY) {

                unlockChallenge();

                unlockMsg.className =
                    "game-message success";

                unlockMsg.textContent =
                    "✓ Unlocked";

                mainStatus.className =
                    "game-message";

                mainStatus.textContent =
                    "Complete all five tasks.";

            } else {

                lockChallenge();

                unlockMsg.className =
                    "game-message error";

                unlockMsg.textContent =
                    "✗ Incorrect key.";
            }
        }
    );


    /*
     * ==========================================
     * TASK 1 — DEPARTMENT
     * ==========================================
     */

    department.addEventListener(
        "change",
        function () {

            if (!unlocked) {
                return;
            }

            if (department.value === "qa") {

                task1Completed = true;

                task1Status.className =
                    "game-message success";

                task1Status.textContent =
                    "✓ Completed";

            } else {

                task1Completed = false;

                task1Status.className =
                    "game-message error";

                task1Status.textContent =
                    "✗ Wrong department";
            }
        }
    );


    /*
     * ==========================================
     * TASK 2 — CHECKBOX
     * ==========================================
     */

    seleniumCheckbox.addEventListener(
        "change",
        function () {

            if (!unlocked) {
                return;
            }

            if (seleniumCheckbox.checked) {

                task2Completed = true;

                task2Status.className =
                    "game-message success";

                task2Status.textContent =
                    "✓ Completed";

            } else {

                task2Completed = false;

                task2Status.className =
                    "game-message";

                task2Status.textContent =
                    "Not completed";
            }
        }
    );


    /*
     * ==========================================
     * TASK 3 — TEXT INPUT
     * ==========================================
     */

    textInput.addEventListener(
        "input",
        function () {

            if (!unlocked) {
                return;
            }

            if (
                textInput.value === REQUIRED_TEXT
            ) {

                task3Completed = true;

                task3Status.className =
                    "game-message success";

                task3Status.textContent =
                    "✓ Completed";

            } else {

                task3Completed = false;

                task3Status.className =
                    "game-message";

                task3Status.textContent =
                    "Not completed";
            }
        }
    );


    /*
     * ==========================================
     * TASK 4 — DOUBLE CLICK
     * ==========================================
     *
     * Students should use Selenium:
     *
     * Actions actions = new Actions(driver);
     * actions.doubleClick(element).perform();
     *
     * ==========================================
     */

    doubleClickTarget.addEventListener(
        "dblclick",
        function () {

            if (!unlocked) {
                return;
            }

            task4Completed = true;

            task4Status.className =
                "game-message success";

            task4Status.textContent =
                "✓ Completed";
        }
    );


    /*
     * ==========================================
     * TASK 5 — SUBMIT
     * ==========================================
     */

    submitChallenge.addEventListener(
        "click",
        function () {

            if (!unlocked) {
                return;
            }

            if (
                task1Completed &&
                task2Completed &&
                task3Completed &&
                task4Completed
            ) {

                task5Status.className =
                    "game-message success";

                task5Status.textContent =
                    "✓ Submitted successfully";

                mainStatus.className =
                    "game-message success";

                mainStatus.textContent =
                    "✓ Level completed!";

                nextKey.style.display =
                    "block";

            } else {

                task5Status.className =
                    "game-message error";

                task5Status.textContent =
                    "✗ Complete all previous tasks";
            }
        }
    );


    /*
     * ==========================================
     * RESET
     * ==========================================
     */

    resetBtn.addEventListener(
        "click",
        function () {

            levelKey.value = "";

            task1Completed = false;
            task2Completed = false;
            task3Completed = false;
            task4Completed = false;

            department.value = "";

            seleniumCheckbox.checked = false;

            textInput.value = "";

            lockChallenge();

            unlockMsg.textContent = "";
            unlockMsg.className =
                "game-message";

            task1Status.className =
                "game-message";

            task1Status.textContent =
                "Not completed";

            task2Status.className =
                "game-message";

            task2Status.textContent =
                "Not completed";

            task3Status.className =
                "game-message";

            task3Status.textContent =
                "Not completed";

            task4Status.className =
                "game-message";

            task4Status.textContent =
                "Not completed";

            task5Status.className =
                "game-message";

            task5Status.textContent =
                "Complete all tasks first.";

            mainStatus.className =
                "game-message";

            mainStatus.textContent =
                "Challenge locked.";

            nextKey.style.display =
                "none";
        }
    );

})();
</script>