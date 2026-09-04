# Level 07 — Multiple JavaScript Alerts

## Mission

You have two JavaScript alerts to handle.

Your Selenium script must:

1. Click the **Simple Alert** button.
2. Read and verify the alert message.
3. Accept the alert.
4. Click the **Confirmation Alert** button.
5. Read and verify the confirmation message.
6. Accept the confirmation.

You must handle **both alerts** using Selenium.

---

## Unlock Level 07

Enter the key obtained from **Level 06**.

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
</style>

<div class="selenium-game">

<input
    type="text"
    id="levelKey"
    class="game-input"
    placeholder="Enter Level 06 key"
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

Handle both JavaScript alerts using Selenium.

<div
    id="challenge"
    class="selenium-game challenge-locked">

    <button
        type="button"
        id="simpleAlertButton"
        class="primary-button"
        disabled>
        Simple Alert
    </button>

    <button
        type="button"
        id="confirmAlertButton"
        class="primary-button"
        disabled>
        Confirmation Alert
    </button>

    <p
        id="alertStatus"
        class="game-message">
        Challenge locked.
    </p>

    <div
        id="nextKey"
        class="key-box">

        <strong>Level 07 Completed</strong>

        <p>
            Both JavaScript alerts were handled correctly.
        </p>

        <p>
            Use this key to unlock Level 08:
        </p>

        <span class="key">
            SEL-07-N5K8-R3T6
        </span>

    </div>

</div>

<script>
(function () {

    /*
     * ==========================================
     * LEVEL 07 — MULTIPLE JAVASCRIPT ALERTS
     * ==========================================
     *
     * LEVEL 06 KEY
     * SEL-06-C4R8-T2M7
     *
     * SIMPLE ALERT
     * Selenium Simple Alert
     *
     * CONFIRMATION ALERT
     * Selenium Confirmation Alert
     *
     * LEVEL 08 KEY
     * SEL-07-N5K8-R3T6
     * ==========================================
     */

    const LEVEL6_KEY =
        "SEL-06-C4R8-T2M7";

    const SIMPLE_ALERT_MESSAGE =
        "Selenium Simple Alert";

    const CONFIRM_ALERT_MESSAGE =
        "Selenium Confirmation Alert";


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

    const simpleAlertButton =
        document.getElementById("simpleAlertButton");

    const confirmAlertButton =
        document.getElementById("confirmAlertButton");

    const alertStatus =
        document.getElementById("alertStatus");

    const nextKey =
        document.getElementById("nextKey");


    let simpleAlertCompleted = false;
    let confirmAlertCompleted = false;


    /*
     * ==========================================
     * LOCK CHALLENGE
     * ==========================================
     */

    function lockChallenge() {

        simpleAlertButton.disabled = true;
        confirmAlertButton.disabled = true;

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

        simpleAlertButton.disabled = false;
        confirmAlertButton.disabled = false;

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
     * UNLOCK LEVEL 07
     * ==========================================
     */

    unlockBtn.addEventListener(
        "click",
        function () {

            const enteredKey =
                levelKey.value.trim();

            if (enteredKey === LEVEL6_KEY) {

                unlockChallenge();

                unlockMsg.className =
                    "game-message success";

                unlockMsg.textContent =
                    "✓ Challenge unlocked.";

                alertStatus.className =
                    "game-message";

                alertStatus.textContent =
                    "Handle both alerts using Selenium.";

            } else {

                lockChallenge();

                unlockMsg.className =
                    "game-message error";

                unlockMsg.textContent =
                    "✗ Incorrect Level 06 key.";

                alertStatus.className =
                    "game-message";

                alertStatus.textContent =
                    "Challenge locked.";
            }
        }
    );


    /*
     * ==========================================
     * SIMPLE ALERT
     * ==========================================
     */

    simpleAlertButton.addEventListener(
        "click",
        function () {

            alert(SIMPLE_ALERT_MESSAGE);

            simpleAlertCompleted = true;

            alertStatus.className =
                "game-message success";

            alertStatus.textContent =
                "✓ Simple alert handled. Now handle the confirmation alert.";

            checkCompletion();
        }
    );


    /*
     * ==========================================
     * CONFIRMATION ALERT
     * ==========================================
     */

    confirmAlertButton.addEventListener(
        "click",
        function () {

            const result =
                confirm(CONFIRM_ALERT_MESSAGE);

            if (result) {

                confirmAlertCompleted = true;

                alertStatus.className =
                    "game-message success";

                alertStatus.textContent =
                    "✓ Confirmation alert accepted.";

                checkCompletion();

            } else {

                confirmAlertCompleted = false;

                alertStatus.className =
                    "game-message error";

                alertStatus.textContent =
                    "✗ Confirmation alert was cancelled.";
            }
        }
    );


    /*
     * ==========================================
     * CHECK COMPLETION
     * ==========================================
     */

    function checkCompletion() {

        if (
            simpleAlertCompleted &&
            confirmAlertCompleted
        ) {

            alertStatus.className =
                "game-message success";

            alertStatus.textContent =
                "✓ Both alerts completed!";

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

            simpleAlertCompleted = false;
            confirmAlertCompleted = false;

            lockChallenge();

            unlockMsg.textContent = "";
            unlockMsg.className =
                "game-message";

            alertStatus.textContent =
                "Challenge locked.";

            alertStatus.className =
                "game-message";

            nextKey.style.display =
                "none";
        }
    );

})();
</script>