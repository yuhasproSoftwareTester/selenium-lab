# Level 13 — Dynamic Element

## Mission

The button on this page has a **dynamic ID**.

Its ID changes every time the challenge starts.

Your task is to find and click the correct button without depending on its changing ID.

You can use:

- CSS selectors
- XPath
- `findElement()`
- Text or other stable attributes

Do **not** use the generated ID of the button.

---

## Unlock Level 13

Enter the key obtained from **Level 12**.

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

.selenium-game .target-label {
    display: block;
    margin: 6px 0;
    font-weight: 600;
}
</style>

<div class="selenium-game">

<input
    type="text"
    id="levelKey"
    class="game-input"
    placeholder="Enter Level 12 key"
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
        Find the button with the text:
    </p>

    <strong class="target-label">
        Complete Dynamic Challenge
    </strong>

    <button
        id="dynamicButton"
        class="primary-button"
        data-action="dynamic-complete"
        disabled>
        Complete Dynamic Challenge
    </button>

    <p
        id="status"
        class="game-message">
        Challenge locked.
    </p>

    <div
        id="nextKey"
        class="key-box">

        <strong>Level 13 Completed</strong>

        <p>
            You successfully located the dynamic element.
        </p>

        <p>
            Use this key to unlock Level 14:
        </p>

        <span class="key">
            SEL-13-D8K4-R6P2
        </span>

    </div>

</div>

<script>
(function () {

    /*
     * ==========================================
     * LEVEL 13 — DYNAMIC ELEMENT
     * ==========================================
     *
     * LEVEL 12 KEY
     * SEL-12-H5R9-X3M7
     *
     * TARGET
     * Complete Dynamic Challenge
     *
     * STABLE ATTRIBUTE
     * data-action="dynamic-complete"
     *
     * LEVEL 14 KEY
     * SEL-13-D8K4-R6P2
     * ==========================================
     */

    const LEVEL12_KEY =
        "SEL-12-H5R9-X3M7";


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

    const status =
        document.getElementById("status");

    const nextKey =
        document.getElementById("nextKey");


    let unlocked = false;


    /*
     * ==========================================
     * GENERATE RANDOM ID
     * ==========================================
     */

    function generateDynamicId() {

        return "btn-" +
            Math.random()
                .toString(36)
                .substring(2, 10);
    }


    /*
     * ==========================================
     * CREATE DYNAMIC BUTTON ID
     * ==========================================
     */

    function createDynamicButton() {

        const button =
            challenge.querySelector(
                '[data-action="dynamic-complete"]'
            );

        if (!button) {
            return;
        }

        button.id =
            generateDynamicId();
    }


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

        const button =
            challenge.querySelector(
                '[data-action="dynamic-complete"]'
            );

        if (button) {
            button.disabled = true;
        }
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

        const button =
            challenge.querySelector(
                '[data-action="dynamic-complete"]'
            );

        if (button) {
            button.disabled = false;
        }
    }


    /*
     * ==========================================
     * INITIAL STATE
     * ==========================================
     */

    createDynamicButton();

    lockChallenge();


    /*
     * ==========================================
     * UNLOCK LEVEL 13
     * ==========================================
     */

    unlockBtn.addEventListener(
        "click",
        function () {

            const enteredKey =
                levelKey.value.trim();

            if (enteredKey === LEVEL12_KEY) {

                unlockChallenge();

                unlockMsg.className =
                    "game-message success";

                unlockMsg.textContent =
                    "✓ Challenge unlocked.";

                status.className =
                    "game-message";

                status.textContent =
                    "Find the button without using its dynamic ID.";

            } else {

                lockChallenge();

                unlockMsg.className =
                    "game-message error";

                unlockMsg.textContent =
                    "✗ Incorrect Level 12 key.";

                status.className =
                    "game-message";

                status.textContent =
                    "Challenge locked.";
            }
        }
    );


    /*
     * ==========================================
     * HANDLE DYNAMIC BUTTON
     * ==========================================
     *
     * The completion logic intentionally checks
     * the stable data-action attribute rather
     * than the generated ID.
     * ==========================================
     */

    challenge.addEventListener(
        "click",
        function (event) {

            if (!unlocked) {
                return;
            }

            const button =
                event.target.closest(
                    '[data-action="dynamic-complete"]'
                );

            if (!button) {
                return;
            }

            status.className =
                "game-message success";

            status.textContent =
                "✓ Dynamic element found and clicked!";

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

            levelKey.value = "";

            lockChallenge();

            unlockMsg.textContent = "";
            unlockMsg.className =
                "game-message";

            status.textContent =
                "Challenge locked.";

            status.className =
                "game-message";

            nextKey.style.display =
                "none";

            /*
             * Generate a new ID so the target
             * changes every time the challenge
             * is reset.
             */

            createDynamicButton();
        }
    );

})();
</script>