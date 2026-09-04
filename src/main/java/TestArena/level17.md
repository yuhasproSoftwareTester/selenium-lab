# Level 17 — Text Verification

## Mission

A report is displayed on the page.

Your Selenium script must verify **three pieces of information**:

1. Verify the page heading is: `Automation Test Report`
2. Verify the status is: `PASSED`
3. Verify the total score is: `85`

After verifying all three values, click **Verify Report**.

### Rules

* Use Selenium to read the text from the page.
* Do not use JavaScript to read the values.
* Do not hardcode the result of the challenge.
* Use assertions in your Selenium test.

---

## Unlock Level 17

Enter the key obtained from **Level 16**.

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

.selenium-game .game-input {
    width: 100%;
    max-width: 320px;
    padding: 6px 8px;
    margin: 3px 0 7px;
    border: 1px solid #cbd5e1;
    border-radius: 4px;
    font-size: 12px;
    box-sizing: border-box;
}

.selenium-game .game-input:focus {
    outline: none;
    border-color: #2563eb;
}

.selenium-game .report-box {
    max-width: 450px;
    margin: 8px 0;
    padding: 10px;
    border: 1px solid #d1d5db;
    border-radius: 5px;
}

.selenium-game .report-title {
    font-size: 15px;
    font-weight: 600;
}

.selenium-game .report-row {
    margin: 5px 0;
}

.selenium-game .label {
    display: inline-block;
    min-width: 90px;
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

.selenium-game .challenge-locked {
    opacity: 0.45;
    pointer-events: none;
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

.selenium-game .key {
    font-family: monospace;
    font-size: 12px;
    font-weight: bold;
}
</style>

<div class="selenium-game">

<input
type="text"
id="levelKey"
class="game-input"
placeholder="Enter Level 16 key"

>

<button
 id="unlockBtn"
 class="primary-button">
Unlock </button>

<button
 id="resetBtn"
 class="reset-button">
Reset </button>

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

<div class="report-box">


<div
    id="reportTitle"
    class="report-title">
    Automation Test Report
</div>

<div class="report-row">
    <span class="label">Tester:</span>
    <span id="testerName">Student</span>
</div>

<div class="report-row">
    <span class="label">Status:</span>
    <span id="testStatus">PASSED</span>
</div>

<div class="report-row">
    <span class="label">Score:</span>
    <span id="testScore">85</span>
</div>


</div>

<button
 id="verifyReport"
 class="primary-button"
 disabled>
Verify Report </button>

<p
    id="status"
    class="game-message">
    Challenge locked.
</p>

<div
    id="nextKey"
    class="key-box">


<strong>Level 17 Completed</strong>

<p>
    All report values were verified successfully.
</p>

<p>
    Use this key to unlock Level 18:
</p>

<span class="key">
    SEL-17-R8K3-P5M9
</span>


</div>

</div>

<script>
(function () {

    const LEVEL16_KEY = "SEL-16-B7M4-K9R2";

    const EXPECTED_TITLE = "Automation Test Report";
    const EXPECTED_STATUS = "PASSED";
    const EXPECTED_SCORE = "85";

    const levelKey = document.getElementById("levelKey");
    const unlockBtn = document.getElementById("unlockBtn");
    const resetBtn = document.getElementById("resetBtn");

    const unlockMsg = document.getElementById("unlockMsg");
    const challenge = document.getElementById("challenge");

    const reportTitle = document.getElementById("reportTitle");
    const testStatus = document.getElementById("testStatus");
    const testScore = document.getElementById("testScore");

    const verifyReport = document.getElementById("verifyReport");
    const status = document.getElementById("status");
    const nextKey = document.getElementById("nextKey");

    let unlocked = false;

    function lockChallenge() {
        unlocked = false;

        challenge.classList.add("challenge-locked");
        verifyReport.disabled = true;
    }

    function unlockChallenge() {
        unlocked = true;

        challenge.classList.remove("challenge-locked");
        verifyReport.disabled = false;

        status.textContent =
            "Read and verify all three report values.";

        status.className = "game-message";
    }

    unlockBtn.addEventListener("click", function () {

        if (levelKey.value.trim() === LEVEL16_KEY) {

            unlockChallenge();

            unlockMsg.textContent = "✓ Unlocked";
            unlockMsg.className = "game-message success";

        } else {

            unlockMsg.textContent = "✗ Incorrect key";
            unlockMsg.className = "game-message error";

            lockChallenge();
        }

    });

    verifyReport.addEventListener("click", function () {

        if (!unlocked) return;

        const title = reportTitle.textContent.trim();
        const reportStatus = testStatus.textContent.trim();
        const score = testScore.textContent.trim();

        if (
            title === EXPECTED_TITLE &&
            reportStatus === EXPECTED_STATUS &&
            score === EXPECTED_SCORE
        ) {

            status.textContent =
                "✓ All report values verified!";

            status.className =
                "game-message success";

            nextKey.style.display = "block";

        } else {

            status.textContent =
                "✗ Report verification failed.";

            status.className =
                "game-message error";
        }

    });

    resetBtn.addEventListener("click", function () {

        levelKey.value = "";

        unlockMsg.textContent = "";

        status.textContent = "Challenge locked.";
        status.className = "game-message";

        nextKey.style.display = "none";

        lockChallenge();
    });

    lockChallenge();

})();
</script>
