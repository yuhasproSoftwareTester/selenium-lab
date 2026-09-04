# Level 09 — Mouse Actions

## Mission

This level introduces Selenium's **Actions class**.
You must use mouse actions to complete four tasks:

1. Move the mouse over the target area.
2. Click the target.
3. Double-click the target.
4. Right-click the target.

Use Selenium's `Actions` class to perform the mouse actions.

---

## Unlock Level 09

Enter the key obtained from **Level 08**.

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

.selenium-game .game-input {
    width: 100%;
    max-width: 320px;
    padding: 6px 8px;
    margin: 3px 0 7px 0;
    border: 1px solid #cbd5e1;
    border-radius: 5px;
    font-size: 12px;
    box-sizing: border-box;
}

.selenium-game .game-input:focus {
    outline: none;
    border-color: #2563eb;
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

.selenium-game .mouse-area {
    width: 260px;
    height: 120px;
    margin-top: 8px;
    border: 2px dashed #94a3b8;
    border-radius: 7px;
    display: flex;
    align-items: center;
    justify-content: center;
    user-select: none;
    transition: 0.2s;
    font-size: 12px;
}

.selenium-game .mouse-area:hover {
    border-color: #2563eb;
}

.selenium-game .action-status {
    margin-top: 7px;
    font-size: 12px;
}

.selenium-game ul {
    margin-top: 5px;
    padding-left: 22px;
}

.selenium-game li {
    margin: 2px 0;
    font-size: 12px;
}
</style>

<div class="selenium-game">

<input
    type="text"
    id="levelKey"
    class="game-input"
    placeholder="Enter Level 08 key"
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

Complete all four mouse actions on the target.

<div
    id="challenge"
    class="selenium-game challenge-locked">

    <p>
        Use Selenium's <strong>Actions</strong> class to complete the target.
    </p>

    <div
        id="mouseTarget"
        class="mouse-area">

        Mouse Action Target

    </div>

    <p
        id="actionStatus"
        class="action-status">
        Challenge locked.
    </p>

    <p>
        Actions completed:
    </p>

    <ul>
        <li id="moveStatus">Move: Not completed</li>
        <li id="clickStatus">Click: Not completed</li>
        <li id="doubleClickStatus">Double Click: Not completed</li>
        <li id="rightClickStatus">Right Click: Not completed</li>
    </ul>

    <div
        id="nextKey"
        class="key-box">

        <strong>Level 09 Completed</strong>

        <p>
            All mouse actions were completed successfully.
        </p>

        <p>
            Use this key to unlock Level 10:
        </p>

        <span class="key">
            SEL-09-M4X7-P2K8
        </span>

    </div>

</div>

<script>
(function () {

    /*
     * ==========================================
     * LEVEL 09 — MOUSE ACTIONS
     * ==========================================
     *
     * LEVEL 08 KEY
     * SEL-08-F2L7-K9P4
     *
     * REQUIRED ACTIONS
     * Move
     * Click
     * Double Click
     * Right Click
     *
     * LEVEL 10 KEY
     * SEL-09-M4X7-P2K8
     * ==========================================
     */

    const LEVEL8_KEY =
        "SEL-08-F2L7-K9P4";


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

    const mouseTarget =
        document.getElementById("mouseTarget");

    const actionStatus =
        document.getElementById("actionStatus");

    const moveStatus =
        document.getElementById("moveStatus");

    const clickStatus =
        document.getElementById("clickStatus");

    const doubleClickStatus =
        document.getElementById("doubleClickStatus");

    const rightClickStatus =
        document.getElementById("rightClickStatus");

    const nextKey =
        document.getElementById("nextKey");


    let unlocked = false;

    let moveCompleted = false;
    let clickCompleted = false;
    let doubleClickCompleted = false;
    let rightClickCompleted = false;


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
    }


    /*
     * ==========================================
     * INITIAL STATE
     * ==========================================
     */

    lockChallenge();


    /*
     * ==========================================
     * UNLOCK LEVEL 09
     * ==========================================
     */

    unlockBtn.addEventListener(
        "click",
        function () {

            const enteredKey =
                levelKey.value.trim();

            if (enteredKey === LEVEL8_KEY) {

                unlockChallenge();

                unlockMsg.className =
                    "game-message success";

                unlockMsg.textContent =
                    "✓ Challenge unlocked.";

                actionStatus.className =
                    "action-status";

                actionStatus.textContent =
                    "Use mouse actions to complete the target.";

            } else {

                lockChallenge();

                unlockMsg.className =
                    "game-message error";

                unlockMsg.textContent =
                    "✗ Incorrect Level 08 key.";

                actionStatus.className =
                    "action-status";

                actionStatus.textContent =
                    "Challenge locked.";
            }
        }
    );


    /*
     * ==========================================
     * MOUSE MOVE
     * ==========================================
     */

    mouseTarget.addEventListener(
        "mouseenter",
        function () {

            if (!unlocked) {
                return;
            }

            moveCompleted = true;

            moveStatus.textContent =
                "Move: ✓ Completed";

            checkCompletion();
        }
    );


    /*
     * ==========================================
     * MOUSE CLICK
     * ==========================================
     */

    mouseTarget.addEventListener(
        "click",
        function () {

            if (!unlocked) {
                return;
            }

            clickCompleted = true;

            clickStatus.textContent =
                "Click: ✓ Completed";

            checkCompletion();
        }
    );


    /*
     * ==========================================
     * DOUBLE CLICK
     * ==========================================
     */

    mouseTarget.addEventListener(
        "dblclick",
        function () {

            if (!unlocked) {
                return;
            }

            doubleClickCompleted = true;

            doubleClickStatus.textContent =
                "Double Click: ✓ Completed";

            checkCompletion();
        }
    );


    /*
     * ==========================================
     * RIGHT CLICK
     * ==========================================
     */

    mouseTarget.addEventListener(
        "contextmenu",
        function (event) {

            event.preventDefault();

            if (!unlocked) {
                return;
            }

            rightClickCompleted = true;

            rightClickStatus.textContent =
                "Right Click: ✓ Completed";

            checkCompletion();
        }
    );


    /*
     * ==========================================
     * CHECK COMPLETION
     * ==========================================
     */

    function checkCompletion() {

        if (
            moveCompleted &&
            clickCompleted &&
            doubleClickCompleted &&
            rightClickCompleted
        ) {

            actionStatus.className =
                "action-status success";

            actionStatus.textContent =
                "✓ All mouse actions completed!";

            nextKey.style.display =
                "block";
        }
    }


    /*
     * ==========================================
     * RESET
     * ==========================================
     */

    resetBtn.addEventListener(
        "click",
        function () {

            levelKey.value = "";

            moveCompleted = false;
            clickCompleted = false;
            doubleClickCompleted = false;
            rightClickCompleted = false;

            lockChallenge();

            unlockMsg.textContent = "";
            unlockMsg.className =
                "game-message";

            actionStatus.className =
                "action-status";

            actionStatus.textContent =
                "Challenge locked.";

            moveStatus.textContent =
                "Move: Not completed";

            clickStatus.textContent =
                "Click: Not completed";

            doubleClickStatus.textContent =
                "Double Click: Not completed";

            rightClickStatus.textContent =
                "Right Click: Not completed";

            nextKey.style.display =
                "none";
        }
    );

})();
</script>