# Level 15 — Web Table

## Mission

You are given a table containing student automation results.

Find the student whose:

* **Name:** Rahul
* **Course:** Selenium
* **Status:** Passed

Then click **View Result** for that student.

### Rules

* Do not use the student's row ID.
* Do not directly locate the `View Result` button.
* Use the table rows and cells to find the correct row.

---

## Unlock Level 15

Enter the key obtained from **Level 14**.

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

.selenium-game .table-wrapper {
    max-width: 650px;
    overflow-x: auto;
    margin-top: 8px;
}

.selenium-game table {
    border-collapse: collapse;
    width: 100%;
    font-size: 12px;
}

.selenium-game th,
.selenium-game td {
    padding: 6px 8px;
    border: 1px solid #d1d5db;
    text-align: left;
}

.selenium-game th {
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
placeholder="Enter Level 14 key"

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

<p>
Find Rahul's Selenium result where the status is Passed.
</p>

<div class="table-wrapper">

<table id="studentTable">

<thead>
<tr>
    <th>Name</th>
    <th>Course</th>
    <th>Score</th>
    <th>Status</th>
    <th>Action</th>
</tr>
</thead>

<tbody>

<tr data-row="student-1">
    <td>Arjun</td>
    <td>Java</td>
    <td>82</td>
    <td>Passed</td>
    <td>
        <button class="result-button" disabled>
            View Result
        </button>
    </td>
</tr>

<tr data-row="student-2">
    <td>Priya</td>
    <td>Selenium</td>
    <td>74</td>
    <td>Failed</td>
    <td>
        <button class="result-button" disabled>
            View Result
        </button>
    </td>
</tr>

<tr data-row="student-3">
    <td>Rahul</td>
    <td>Java</td>
    <td>91</td>
    <td>Passed</td>
    <td>
        <button class="result-button" disabled>
            View Result
        </button>
    </td>
</tr>

<tr data-row="student-4">
    <td>Neha</td>
    <td>Selenium</td>
    <td>88</td>
    <td>Passed</td>
    <td>
        <button class="result-button" disabled>
            View Result
        </button>
    </td>
</tr>

<tr data-row="student-5">
    <td>Rahul</td>
    <td>Selenium</td>
    <td>95</td>
    <td>Passed</td>
    <td>
        <button class="result-button" disabled>
            View Result
        </button>
    </td>
</tr>

<tr data-row="student-6">
    <td>Vikram</td>
    <td>Python</td>
    <td>79</td>
    <td>Passed</td>
    <td>
        <button class="result-button" disabled>
            View Result
        </button>
    </td>
</tr>

</tbody>
</table>

</div>

<p
    id="status"
    class="game-message">
    Challenge locked.
</p>

<div
    id="nextKey"
    class="key-box">


<strong>Level 15 Completed</strong>

<p>
    You found the correct table row.
</p>

<p>
    Use this key to unlock Level 16:
</p>

<span class="key">
    SEL-15-T4K8-N6P2
</span>


</div>

</div>

<script>
(function () {

    const LEVEL14_KEY = "SEL-14-Z6P3-M8K1";

    const TARGET_NAME = "Rahul";
    const TARGET_COURSE = "Selenium";
    const TARGET_STATUS = "Passed";

    const levelKey = document.getElementById("levelKey");
    const unlockBtn = document.getElementById("unlockBtn");
    const resetBtn = document.getElementById("resetBtn");

    const unlockMsg = document.getElementById("unlockMsg");
    const challenge = document.getElementById("challenge");
    const status = document.getElementById("status");
    const nextKey = document.getElementById("nextKey");

    const buttons = document.querySelectorAll(".result-button");

    let unlocked = false;

    function lockChallenge() {
        unlocked = false;

        challenge.classList.add("challenge-locked");

        buttons.forEach(function (button) {
            button.disabled = true;
        });
    }

    function unlockChallenge() {
        unlocked = true;

        challenge.classList.remove("challenge-locked");

        buttons.forEach(function (button) {
            button.disabled = false;
        });
    }

    unlockBtn.addEventListener("click", function () {

        if (levelKey.value.trim() === LEVEL14_KEY) {

            unlockChallenge();

            unlockMsg.textContent = "✓ Unlocked";
            unlockMsg.className = "game-message success";

            status.textContent =
                "Search the table for the correct row.";
            status.className = "game-message";

        } else {

            unlockMsg.textContent = "✗ Incorrect key";
            unlockMsg.className = "game-message error";

            lockChallenge();
        }

    });

    buttons.forEach(function (button) {

        button.addEventListener("click", function () {

            if (!unlocked) return;

            const row = button.closest("tr");
            const cells = row.querySelectorAll("td");

            const name = cells[0].textContent.trim();
            const course = cells[1].textContent.trim();
            const rowStatus = cells[3].textContent.trim();

            if (
                name === TARGET_NAME &&
                course === TARGET_COURSE &&
                rowStatus === TARGET_STATUS
            ) {

                status.textContent =
                    "✓ Correct student found!";

                status.className =
                    "game-message success";

                nextKey.style.display = "block";

            } else {

                status.textContent =
                    "✗ Wrong row. Check all three conditions.";

                status.className =
                    "game-message error";
            }

        });

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
