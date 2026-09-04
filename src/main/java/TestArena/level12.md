# Level 12 — Explicit Wait

## Mission

The target button is **not available immediately**.

Wait for the button to appear and become clickable.

Your Selenium script should use:

- `WebDriverWait`
- `ExpectedConditions`
- `elementToBeClickable`

Do not use `Thread.sleep()`.

---

## Unlock Level 12

Enter the key obtained from **Level 11**.

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

.selenium-game .delayed-button {
    display: none;
}

.selenium-game .timer-text {
    font-size: 12px;
}
</style>

<div class="selenium-game">

<input
    type="text"
    id="levelKey"
    class="game-input"
    placeholder="Enter Level 11 key"
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

<div
    id="challenge"
    class="selenium-game challenge-locked">

    <p>
        The target button will appear after a short delay.
    </p>

    <p
        id="timerText"
        class="timer-text">
        Waiting to start...
    </p>

    <button
        type="button"
        id="delayedButton"
        class="primary-button delayed-button">
        Click After Waiting
    </button>

    <p
        id="status"
        class="game-message">
        Challenge locked.
    </p>

    <div
        id="nextKey"
        class="key-box">

        <strong>Level 12 Completed</strong>

        <p>
            You successfully handled the delayed element.
        </p>

        <p>
            Use this key to unlock Level 13:
        </p>

        <span class="key">
            SEL-12-H5R9-X3M7
        </span>

    </div>

</div>

<script>
(function () {

    /*
     * ==========================================
     * LEVEL 12 — EXPLICIT WAIT
     * ==========================================
     *
     * LEVEL 11 KEY
     * SEL-11-V6R2-K8P5
     *
     * REQUIRED SELENIUM CONCEPTS
     * WebDriverWait
     * ExpectedConditions
     * elementToBeClickable
     *
     * DO NOT USE
     * Thread.sleep()
     *
     * LEVEL 13 KEY
     * SEL-12-H5R9-X3M7
     * ==========================================
     */

    const LEVEL11_KEY =
        "SEL-11-V6R2-K8P5";


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

    const delayedButton =
        document.getElementById("delayedButton");

    const timerText =
        document.getElementById("timerText");

    const status =
        document.getElementById("status");

    const nextKey =
        document.getElementById("nextKey");


    let unlocked = false;
    let timer = null;


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

        delayedButton.style.display =
            "none";
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
     * UNLOCK LEVEL 12
     * ==========================================
     */

    unlockBtn.addEventListener(
        "click",
        function () {

            const enteredKey =
                levelKey.value.trim();

            if (enteredKey === LEVEL11_KEY) {

                unlockChallenge();

                unlockMsg.className =
                    "game-message success";

                unlockMsg.textContent =
                    "✓ Challenge unlocked.";

                status.className =
                    "game-message";

                status.textContent =
                    "Wait for the button to appear, then click it.";

                startDelay();

            } else {

                lockChallenge();

                unlockMsg.className =
                    "game-message error";

                unlockMsg.textContent =
                    "✗ Incorrect Level 11 key.";

                status.className =
                    "game-message";

                status.textContent =
                    "Challenge locked.";
            }
        }
    );


    /*
     * ==========================================
     * START DELAY
     * ==========================================
     */

    function startDelay() {

        if (timer) {
            clearInterval(timer);
        }

        delayedButton.style.display =
            "none";

        let seconds = 4;

        timerText.textContent =
            "Button appears in " +
            seconds +
            " seconds";


        timer = setInterval(
            function () {

                seconds--;

                if (seconds > 0) {

                    timerText.textContent =
                        "Button appears in " +
                        seconds +
                        " seconds";

                } else {

                    clearInterval(timer);

                    timer = null;

                    timerText.textContent =
                        "The button is now available.";

                    delayedButton.style.display =
                        "inline-block";
                }

            },
            1000
        );
    }


    /*
     * ==========================================
     * TARGET BUTTON
     * ==========================================
     */

    delayedButton.addEventListener(
        "click",
        function () {

            if (!unlocked) {
                return;
            }

            status.className =
                "game-message success";

            status.textContent =
                "✓ Delayed element clicked successfully!";

            nextKey.style.display =
                "block";
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

            if (timer) {
                clearInterval(timer);
                timer = null;
            }

            levelKey.value = "";

            lockChallenge();

            unlockMsg.textContent = "";
            unlockMsg.className =
                "game-message";

            timerText.textContent =
                "Waiting to start...";

            status.textContent =
                "Challenge locked.";

            status.className =
                "game-message";

            nextKey.style.display =
                "none";
        }
    );

})();
</script>