# Level 06 — JavaScript Alert

## Mission

Before attempting this level, enter the unlock key from **Level 05**.
After unlocking:

1. Click the button to open a JavaScript alert.
2. The alert message is:
   `Selenium Alert Challenge`
3. Handle the alert using Selenium.
4. Verify the alert text.
5. Accept the alert.

After completing the challenge, the key for **Level 07** will be revealed.

---

## Unlock Level 06

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

.selenium-game input {
    width: 100%;
    max-width: 320px;
    padding: 6px 8px;
    margin: 3px 0 7px 0;
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

.selenium-game .alert-box {
    max-width: 450px;
    padding: 10px 12px;
    border: 1px solid #cbd5e1;
    border-radius: 6px;
    margin-top: 7px;
}

.selenium-game .alert-title {
    font-weight: 600;
    margin-bottom: 5px;
}
</style>

<div class="selenium-game">

<input
    type="text"
    id="levelKey"
    placeholder="Enter Level 05 Key"
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

## Challenge Playground

Handle the JavaScript alert using Selenium.

<div
    id="challenge"
    class="selenium-game challenge-locked">

    <div class="alert-box">

        <div class="alert-title">
            Alert Testing Panel
        </div>

        <p>
            Click the button below to open the alert.
        </p>

        <button
            type="button"
            id="alertButton"
            class="primary-button"
            disabled>
            Open Alert
        </button>

        <p
            id="alertStatus"
            class="game-message">
        </p>

    </div>

    <div
        id="nextKey"
        class="key-box">

        <strong>Level 06 Completed</strong>

        <p>
            Congratulations! You successfully
            handled the JavaScript alert.
        </p>

        <p>
            Use this key to unlock Level 07:
        </p>

        <span class="key">
            SEL-06-C4R8-T2M7
        </span>

    </div>

</div>

<script>
(function () {

    /*
     * ==========================================
     * LEVEL 06 — JAVASCRIPT ALERT
     * ==========================================
     *
     * LEVEL 05 KEY
     * SEL-05-B7K3-Q9M6
     *
     * ALERT MESSAGE
     * Selenium Alert Challenge
     *
     * LEVEL 07 KEY
     * SEL-06-C4R8-T2M7
     * ==========================================
     */

    const LEVEL5_KEY = "SEL-05-B7K3-Q9M6";

    const ALERT_MESSAGE = "Selenium Alert Challenge";

    const unlockBtn = document.getElementById("unlockBtn");
    const resetBtn = document.getElementById("resetBtn");
    const keyInput = document.getElementById("levelKey");
    const unlockMsg = document.getElementById("unlockMsg");

    const challenge = document.getElementById("challenge");
    const alertButton = document.getElementById("alertButton");
    const alertStatus = document.getElementById("alertStatus");
    const nextKey = document.getElementById("nextKey");


    /*
     * ==========================================
     * LOCK CHALLENGE
     * ==========================================
     */

    function lockChallenge() {

        alertButton.disabled = true;

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

        alertButton.disabled = false;

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
     * UNLOCK LEVEL 06
     * ==========================================
     */

    unlockBtn.addEventListener(
        "click",
        function () {

            const enteredKey =
                keyInput.value.trim();

            if (enteredKey === LEVEL5_KEY) {

                unlockChallenge();

                unlockMsg.className =
                    "game-message success";

                unlockMsg.textContent =
                    "✓ Level 06 unlocked.";

            } else {

                lockChallenge();

                unlockMsg.className =
                    "game-message error";

                unlockMsg.textContent =
                    "✗ Invalid key.";
            }
        }
    );


    /*
     * ==========================================
     * OPEN JAVASCRIPT ALERT
     * ==========================================
     */

    alertButton.addEventListener(
        "click",
        function () {

            alert(ALERT_MESSAGE);

            alertStatus.className =
                "game-message success";

            alertStatus.textContent =
                "✓ Alert handled.";

            /*
             * The browser page cannot directly
             * detect whether Selenium accepted
             * a native JavaScript alert.
             *
             * The key is therefore displayed
             * after the alert interaction.
             *
             * Students should still be graded on
             * their Selenium Alert handling code.
             */

            setTimeout(
                function () {

                    nextKey.style.display =
                        "block";

                },
                100
            );
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

            keyInput.value = "";

            lockChallenge();

            unlockMsg.textContent = "";
            unlockMsg.className =
                "game-message";

            alertStatus.textContent = "";
            alertStatus.className =
                "game-message";

            nextKey.style.display =
                "none";
        }
    );

})();
</script>