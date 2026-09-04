# Level 01 — Basic Locator

## Mission

Your task is to find and click the **correct button** using Selenium.
There are multiple buttons on this page, but only one is the target.
After clicking the correct button, the challenge will be completed and you will receive the key for **Level 02**.

---

## Challenge Playground

Find and click the correct button.

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

.selenium-game .target-button {
    background: #2563eb;
    color: white;
    border-color: #2563eb;
}

.selenium-game .target-button:hover {
    background: #1d4ed8;
}

.selenium-game .game-message {
    margin: 8px 0;
    font-size: 12px;
}

.selenium-game .success {
    color: #16a34a;
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
</style>

<div class="selenium-game">

<button id="wrong-button-1">
    Cancel
</button>

<button id="wrong-button-2">
    Reset
</button>

<button
    id="selenium-target"
    class="target-button">
    Complete Challenge
</button>

<button id="wrong-button-3">
    Back
</button>

<p
    id="result"
    class="game-message">
</p>

<div
    id="nextKey"
    class="key-box">

    <strong>Level 01 Completed</strong>

    <p>
        Congratulations! You completed Level 01.
    </p>

    <p>
        Use this key to unlock Level 02:
    </p>

    <span class="key">
        SEL-01-A7X9-K4P2
    </span>

</div>

</div>

<script>
(function () {

    const targetButton =
        document.getElementById("selenium-target");

    const result =
        document.getElementById("result");

    const nextKey =
        document.getElementById("nextKey");

    targetButton.addEventListener(
        "click",
        function () {

            result.textContent =
                "Challenge completed!";

            result.classList.add("success");

            nextKey.style.display =
                "block";

        }
    );

})();
</script>