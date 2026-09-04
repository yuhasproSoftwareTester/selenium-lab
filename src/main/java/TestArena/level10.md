# Level 10 — Keyboard Actions

## Mission

This level introduces **keyboard actions** using Selenium's `Actions` class.
You have two challenges.

### Challenge 1 — Cut and Paste

Cut the text from the **Source Textbox** and paste it into the **Destination Textbox**.
You must use keyboard actions such as:

- `CTRL + A`
- `CTRL + X`
- `CTRL + V`

Do not simply type the text into the destination textbox.

### Challenge 2 — Mixed Case

Use Selenium's `Actions` class to type the following exactly:
`SeLeNiUm AuToMaTiOn`
Pay attention to the uppercase and lowercase letters.

---

## Unlock Level 10

Enter the key obtained from **Level 09**.

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

.selenium-game .game-textbox {
    width: 100%;
    max-width: 320px;
    padding: 6px 8px;
    margin: 3px 0 7px 0;
    border: 1px solid #cbd5e1;
    border-radius: 5px;
    font-size: 12px;
    box-sizing: border-box;
}

.selenium-game .game-textbox:focus {
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

.selenium-game .challenge-section {
    max-width: 450px;
    margin-top: 10px;
}

.selenium-game .challenge-section strong {
    font-size: 13px;
}
</style>

<div class="selenium-game">

<input
    type="text"
    id="levelKey"
    class="game-input"
    placeholder="Enter Level 09 key"
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

    <div class="challenge-section">

        <strong>Challenge 1 — Cut and Paste</strong>

        <p>
            Cut the text from the source textbox and paste it into
            the destination textbox using keyboard actions.
        </p>

        <label for="sourceBox">
            Source Textbox
        </label>

        <input
            type="text"
            id="sourceBox"
            class="game-textbox"
            value="SELENIUM KEYBOARD ACTION"
            disabled
        >

        <label for="destinationBox">
            Destination Textbox
        </label>

        <input
            type="text"
            id="destinationBox"
            class="game-textbox"
            disabled
        >

        <p
            id="cutPasteStatus"
            class="game-message">
            Challenge locked.
        </p>

    </div>


    <div class="challenge-section">

        <strong>Challenge 2 — Mixed Case</strong>

        <p>
            Use keyboard actions to type:
            <strong>SeLeNiUm AuToMaTiOn</strong>
        </p>

        <input
            type="text"
            id="mixedCaseBox"
            class="game-textbox"
            placeholder="Type the required text"
            disabled
        >

        <p
            id="mixedCaseStatus"
            class="game-message">
        </p>

    </div>


    <div
        id="nextKey"
        class="key-box">

        <strong>Level 10 Completed</strong>

        <p>
            Both keyboard challenges were completed successfully.
        </p>

        <p>
            Use this key to unlock Level 11:
        </p>

        <span class="key">
            SEL-10-Q7N4-L2M8
        </span>

    </div>

</div>

<script>
(function () {

    /*
     * ==========================================
     * LEVEL 10 — KEYBOARD ACTIONS
     * ==========================================
     *
     * LEVEL 09 KEY
     * SEL-09-M4X7-P2K8
     *
     * CUT TEXT
     * SELENIUM KEYBOARD ACTION
     *
     * MIXED CASE TEXT
     * SeLeNiUm AuToMaTiOn
     *
     * LEVEL 11 KEY
     * SEL-10-Q7N4-L2M8
     * ==========================================
     */

    const LEVEL9_KEY =
        "SEL-09-M4X7-P2K8";

    const CUT_TEXT =
        "SELENIUM KEYBOARD ACTION";

    const MIXED_TEXT =
        "SeLeNiUm AuToMaTiOn";


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

    const sourceBox =
        document.getElementById("sourceBox");

    const destinationBox =
        document.getElementById("destinationBox");

    const mixedCaseBox =
        document.getElementById("mixedCaseBox");

    const cutPasteStatus =
        document.getElementById("cutPasteStatus");

    const mixedCaseStatus =
        document.getElementById("mixedCaseStatus");

    const nextKey =
        document.getElementById("nextKey");


    let unlocked = false;
    let cutPasteCompleted = false;
    let mixedCaseCompleted = false;


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

        sourceBox.disabled = true;
        destinationBox.disabled = true;
        mixedCaseBox.disabled = true;
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

        sourceBox.disabled = false;
        destinationBox.disabled = false;
        mixedCaseBox.disabled = false;
    }


    /*
     * ==========================================
     * INITIAL STATE
     * ==========================================
     */

    lockChallenge();


    /*
     * ==========================================
     * UNLOCK LEVEL 10
     * ==========================================
     */

    unlockBtn.addEventListener(
        "click",
        function () {

            const enteredKey =
                levelKey.value.trim();

            if (enteredKey === LEVEL9_KEY) {

                unlockChallenge();

                unlockMsg.className =
                    "game-message success";

                unlockMsg.textContent =
                    "✓ Challenge unlocked.";

                cutPasteStatus.className =
                    "game-message";

                cutPasteStatus.textContent =
                    "Cut the source text and paste it into the destination.";

                mixedCaseStatus.className =
                    "game-message";

                mixedCaseStatus.textContent =
                    "Type the required mixed-case text.";

            } else {

                lockChallenge();

                unlockMsg.className =
                    "game-message error";

                unlockMsg.textContent =
                    "✗ Incorrect Level 09 key.";
            }
        }
    );


    /*
     * ==========================================
     * CHECK CUT & PASTE
     * ==========================================
     */

    destinationBox.addEventListener(
        "input",
        function () {

            if (!unlocked) {
                return;
            }

            if (
                destinationBox.value === CUT_TEXT &&
                sourceBox.value === ""
            ) {

                cutPasteCompleted = true;

                cutPasteStatus.className =
                    "game-message success";

                cutPasteStatus.textContent =
                    "✓ Cut and paste completed.";

                checkCompletion();
            }
        }
    );


    /*
     * ==========================================
     * CHECK MIXED CASE
     * ==========================================
     */

    mixedCaseBox.addEventListener(
        "input",
        function () {

            if (!unlocked) {
                return;
            }

            if (
                mixedCaseBox.value === MIXED_TEXT
            ) {

                mixedCaseCompleted = true;

                mixedCaseStatus.className =
                    "game-message success";

                mixedCaseStatus.textContent =
                    "✓ Correct uppercase and lowercase pattern.";

                checkCompletion();
            }
        }
    );


    /*
     * ==========================================
     * CHECK LEVEL COMPLETION
     * ==========================================
     */

    function checkCompletion() {

        if (
            cutPasteCompleted &&
            mixedCaseCompleted
        ) {

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

            cutPasteCompleted = false;
            mixedCaseCompleted = false;

            sourceBox.value =
                CUT_TEXT;

            destinationBox.value =
                "";

            mixedCaseBox.value =
                "";

            lockChallenge();

            unlockMsg.textContent = "";
            unlockMsg.className =
                "game-message";

            cutPasteStatus.className =
                "game-message";

            cutPasteStatus.textContent =
                "Challenge locked.";

            mixedCaseStatus.className =
                "game-message";

            mixedCaseStatus.textContent =
                "";

            nextKey.style.display =
                "none";
        }
    );

})();
</script>