# Level 08 — IFrame Handling

## Mission

A form is hidden inside an **iframe**.

Your task is to use Selenium to:

1. Enter the access code `SELENIUM-IFRAME` inside the iframe.
2. Click the **Verify Code** button.
3. Verify the success message.
4. Return to the main page.

You must switch into the iframe before interacting with its elements.

---

## Unlock Level 08

Enter the key obtained from **Level 07**.

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

.selenium-game iframe {
    width: 100%;
    max-width: 500px;
    height: 150px;
    border: 1px solid #cbd5e1;
    border-radius: 6px;
    margin-top: 7px;
}
</style>

<div class="selenium-game">

<input
    type="text"
    id="levelKey"
    class="game-input"
    placeholder="Enter Level 07 key"
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

The form below is inside an iframe.

<div
    id="challenge"
    class="selenium-game challenge-locked">

    <iframe
        id="seleniumFrame"
        title="Selenium IFrame Challenge">
    </iframe>

    <p
        id="status"
        class="game-message">
        Challenge locked.
    </p>

    <div
        id="nextKey"
        class="key-box">

        <strong>Level 08 Completed</strong>

        <p>
            You successfully handled the iframe.
        </p>

        <p>
            Use this key to unlock Level 09:
        </p>

        <span class="key">
            SEL-08-F2L7-K9P4
        </span>

    </div>

</div>

<script>
(function () {

    /*
     * ==========================================
     * LEVEL 08 — IFRAME HANDLING
     * ==========================================
     *
     * LEVEL 07 KEY
     * SEL-07-N5K8-R3T6
     *
     * FRAME CODE
     * SELENIUM-IFRAME
     *
     * LEVEL 09 KEY
     * SEL-08-F2L7-K9P4
     * ==========================================
     */

    const LEVEL7_KEY =
        "SEL-07-N5K8-R3T6";

    const FRAME_CODE =
        "SELENIUM-IFRAME";


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

    const frame =
        document.getElementById("seleniumFrame");

    const status =
        document.getElementById("status");

    const nextKey =
        document.getElementById("nextKey");


    /*
     * ==========================================
     * LOAD IFRAME CONTENT
     * ==========================================
     */

    function loadFrame() {

        frame.srcdoc = `
            <!DOCTYPE html>

            <html>

            <head>

                <style>

                    body {
                        font-family: Arial, sans-serif;
                        padding: 12px;
                        font-size: 13px;
                    }

                    input {
                        padding: 6px 8px;
                        width: 200px;
                        border: 1px solid #ccc;
                        border-radius: 4px;
                        box-sizing: border-box;
                    }

                    button {
                        padding: 6px 10px;
                        margin-left: 4px;
                        background: #2563eb;
                        color: white;
                        border: none;
                        border-radius: 4px;
                        cursor: pointer;
                        font-size: 12px;
                    }

                    button:disabled {
                        opacity: 0.5;
                        cursor: not-allowed;
                    }

                    #frameResult {
                        margin-top: 8px;
                        font-weight: bold;
                    }

                </style>

            </head>

            <body>

                <strong>
                    IFrame Verification
                </strong>

                <p>
                    Enter the verification code:
                </p>

                <input
                    id="frameCode"
                    type="text"
                    disabled
                >

                <button
                    id="frameSubmit"
                    disabled>
                    Verify Code
                </button>

                <p id="frameResult"></p>

            </body>

            </html>
        `;
    }


    /*
     * ==========================================
     * LOCK CHALLENGE
     * ==========================================
     */

    function lockChallenge() {

        challenge.classList.add(
            "challenge-locked"
        );

        const frameDoc =
            frame.contentDocument;

        if (frameDoc) {

            const code =
                frameDoc.getElementById(
                    "frameCode"
                );

            const submit =
                frameDoc.getElementById(
                    "frameSubmit"
                );

            if (code) {
                code.disabled = true;
            }

            if (submit) {
                submit.disabled = true;
            }
        }
    }


    /*
     * ==========================================
     * UNLOCK CHALLENGE
     * ==========================================
     */

    function unlockChallenge() {

        challenge.classList.remove(
            "challenge-locked"
        );

        const frameDoc =
            frame.contentDocument;

        if (frameDoc) {

            const code =
                frameDoc.getElementById(
                    "frameCode"
                );

            const submit =
                frameDoc.getElementById(
                    "frameSubmit"
                );

            if (code) {
                code.disabled = false;
            }

            if (submit) {
                submit.disabled = false;
            }
        }
    }


    /*
     * ==========================================
     * INITIAL LOAD
     * ==========================================
     */

    loadFrame();


    /*
     * ==========================================
     * IFRAME LOAD EVENT
     * ==========================================
     */

    frame.addEventListener(
        "load",
        function () {

            const frameDoc =
                frame.contentDocument;

            if (!frameDoc) {
                return;
            }

            const submit =
                frameDoc.getElementById(
                    "frameSubmit"
                );

            const code =
                frameDoc.getElementById(
                    "frameCode"
                );

            const result =
                frameDoc.getElementById(
                    "frameResult"
                );


            /*
             * Keep iframe locked until
             * Level 07 key is entered.
             */

            if (
                !challenge.classList.contains(
                    "challenge-locked"
                )
            ) {

                code.disabled = false;
                submit.disabled = false;

            } else {

                code.disabled = true;
                submit.disabled = true;
            }


            /*
             * Verify iframe code
             */

            submit.addEventListener(
                "click",
                function () {

                    if (
                        code.value === FRAME_CODE
                    ) {

                        result.textContent =
                            "✓ Verification successful!";

                        result.style.color =
                            "#16a34a";

                        window.parent.postMessage(
                            "iframe-completed",
                            "*"
                        );

                    } else {

                        result.textContent =
                            "✗ Incorrect verification code.";

                        result.style.color =
                            "#dc2626";
                    }
                }
            );
        }
    );


    /*
     * ==========================================
     * UNLOCK LEVEL 08
     * ==========================================
     */

    unlockBtn.addEventListener(
        "click",
        function () {

            const enteredKey =
                levelKey.value.trim();

            if (enteredKey === LEVEL7_KEY) {

                unlockChallenge();

                unlockMsg.className =
                    "game-message success";

                unlockMsg.textContent =
                    "✓ Challenge unlocked.";

                status.className =
                    "game-message";

                status.textContent =
                    "Switch into the iframe and complete the form.";

            } else {

                lockChallenge();

                unlockMsg.className =
                    "game-message error";

                unlockMsg.textContent =
                    "✗ Incorrect Level 07 key.";

                status.className =
                    "game-message";

                status.textContent =
                    "Challenge locked.";
            }
        }
    );


    /*
     * ==========================================
     * DETECT IFRAME COMPLETION
     * ==========================================
     */

    window.addEventListener(
        "message",
        function (event) {

            if (
                event.data === "iframe-completed"
            ) {

                status.className =
                    "game-message success";

                status.textContent =
                    "✓ IFrame challenge completed!";

                nextKey.style.display =
                    "block";
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

            challenge.classList.add(
                "challenge-locked"
            );

            unlockMsg.textContent = "";
            unlockMsg.className =
                "game-message";

            status.textContent =
                "Challenge locked.";

            status.className =
                "game-message";

            nextKey.style.display =
                "none";

            loadFrame();
        }
    );

})();
</script>