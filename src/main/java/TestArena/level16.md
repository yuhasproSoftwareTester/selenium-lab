# Level 16 — Hidden Element

## Mission

Some elements on this page are hidden.

Your task is to:

1. Find the hidden input.
2. Use the **Reveal Element** button.
3. Enter the required value into the revealed input.
4. Click **Verify**.

### Required value

`SELENIUM-HIDDEN`

The important part is understanding that the element exists in the DOM but is initially hidden.

---

## Unlock Level 16

Enter the key obtained from **Level 15**.

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

.selenium-game .hidden-input {
    display: none;
}

.selenium-game .revealed-input {
    display: inline-block;
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
placeholder="Enter Level 15 key"

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
Find the hidden input and complete the verification.
</p>

<button
 id="revealButton"
 class="primary-button"
 disabled>
Reveal Element </button>

<input
 type="text"
 id="hiddenInput"
 class="game-input hidden-input"
 placeholder="Enter verification value"
 disabled>

<button
 id="verifyButton"
 class="primary-button"
 disabled>
Verify </button>

<p
    id="status"
    class="game-message">
    Challenge locked.
</p>

<div
    id="nextKey"
    class="key-box">


<strong>Level 16 Completed</strong>

<p>
    You successfully handled the hidden element.
</p>

<p>
    Use this key to unlock Level 17:
</p>

<span class="key">
    SEL-16-B7M4-K9R2
</span>


</div>

</div>

<script>
(function () {

    const LEVEL15_KEY = "SEL-15-T4K8-N6P2";
    const REQUIRED_VALUE = "SELENIUM-HIDDEN";

    const levelKey = document.getElementById("levelKey");
    const unlockBtn = document.getElementById("unlockBtn");
    const resetBtn = document.getElementById("resetBtn");

    const unlockMsg = document.getElementById("unlockMsg");
    const challenge = document.getElementById("challenge");

    const revealButton = document.getElementById("revealButton");
    const hiddenInput = document.getElementById("hiddenInput");
    const verifyButton = document.getElementById("verifyButton");

    const status = document.getElementById("status");
    const nextKey = document.getElementById("nextKey");

    let unlocked = false;
    let revealed = false;

    function lockChallenge() {
        unlocked = false;
        revealed = false;

        challenge.classList.add("challenge-locked");

        revealButton.disabled = true;
        hiddenInput.disabled = true;
        verifyButton.disabled = true;

        hiddenInput.value = "";

        hiddenInput.classList.remove("revealed-input");
        hiddenInput.classList.add("hidden-input");
    }

    function unlockChallenge() {
        unlocked = true;

        challenge.classList.remove("challenge-locked");

        revealButton.disabled = false;

        status.textContent = "Find the hidden input.";
        status.className = "game-message";
    }

    unlockBtn.addEventListener("click", function () {

        if (levelKey.value.trim() === LEVEL15_KEY) {

            unlockChallenge();

            unlockMsg.textContent = "✓ Unlocked";
            unlockMsg.className = "game-message success";

        } else {

            unlockMsg.textContent = "✗ Incorrect key";
            unlockMsg.className = "game-message error";

            lockChallenge();
        }

    });

    revealButton.addEventListener("click", function () {

        if (!unlocked) return;

        revealed = true;

        hiddenInput.classList.remove("hidden-input");
        hiddenInput.classList.add("revealed-input");

        hiddenInput.disabled = false;
        verifyButton.disabled = false;

        status.textContent =
            "✓ Element revealed. Enter the required value.";

        status.className =
            "game-message success";
    });

    verifyButton.addEventListener("click", function () {

        if (!unlocked || !revealed) return;

        if (hiddenInput.value.trim() === REQUIRED_VALUE) {

            status.textContent =
                "✓ Hidden element completed!";

            status.className =
                "game-message success";

            nextKey.style.display = "block";

        } else {

            status.textContent =
                "✗ Incorrect value.";

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
