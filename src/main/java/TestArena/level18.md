# Level 18 — Login Validation

## Mission

You are testing a login page.

The page accepts a username and password. Your Selenium test must perform **two login attempts**.

### Attempt 1 — Invalid Login

Use any incorrect username or password.

Verify that the page displays:

`Invalid username or password`

### Attempt 2 — Valid Login

Use:

**Username:** `selenium`
**Password:** `webdriver123`

Verify that the page displays:

`Login successful`

Then click **Continue**.

---

## Unlock Level 18

Enter the key obtained from **Level 17**.

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

.selenium-game .login-box {
    max-width: 350px;
    padding: 10px;
    margin: 8px 0;
    border: 1px solid #d1d5db;
    border-radius: 5px;
}

.selenium-game .login-box label {
    font-size: 12px;
    font-weight: 600;
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
placeholder="Enter Level 17 key"

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

<div class="login-box">

<label for="username">
    Username
</label>

<input
 type="text"
 id="username"
 class="game-input"
 disabled>

<label for="password">
    Password
</label>

<input
 type="password"
 id="password"
 class="game-input"
 disabled>

<button
 id="loginButton"
 class="primary-button"
 disabled>
Login </button>

<p
    id="loginStatus"
    class="game-message">
    Challenge locked.
</p>

</div>

<p>
    <strong>Required sequence:</strong>
</p>

<p id="attempt1">
    1. Invalid login: Not completed
</p>

<p id="attempt2">
    2. Valid login: Not completed
</p>

<p id="continueStatus">
    3. Continue: Not completed
</p>

<button
 id="continueButton"
 class="primary-button"
 disabled>
Continue </button>

<div
    id="nextKey"
    class="key-box">


<strong>Level 18 Completed</strong>

<p>
    Both login scenarios were tested successfully.
</p>

<p>
    Use this key to unlock Level 19:
</p>

<span class="key">
    SEL-18-J4P7-R9K2
</span>


</div>

</div>

<script>
(function () {

    const LEVEL17_KEY = "SEL-17-R8K3-P5M9";

    const VALID_USERNAME = "selenium";
    const VALID_PASSWORD = "webdriver123";

    const INVALID_MESSAGE =
        "Invalid username or password";

    const SUCCESS_MESSAGE =
        "Login successful";

    const levelKey = document.getElementById("levelKey");
    const unlockBtn = document.getElementById("unlockBtn");
    const resetBtn = document.getElementById("resetBtn");

    const unlockMsg = document.getElementById("unlockMsg");
    const challenge = document.getElementById("challenge");

    const username = document.getElementById("username");
    const password = document.getElementById("password");
    const loginButton = document.getElementById("loginButton");
    const loginStatus = document.getElementById("loginStatus");

    const attempt1 = document.getElementById("attempt1");
    const attempt2 = document.getElementById("attempt2");
    const continueStatus = document.getElementById("continueStatus");

    const continueButton = document.getElementById("continueButton");
    const nextKey = document.getElementById("nextKey");

    let unlocked = false;
    let invalidCompleted = false;
    let validCompleted = false;

    function lockChallenge() {
        unlocked = false;
        invalidCompleted = false;
        validCompleted = false;

        challenge.classList.add("challenge-locked");

        username.disabled = true;
        password.disabled = true;
        loginButton.disabled = true;
        continueButton.disabled = true;
    }

    function unlockChallenge() {
        unlocked = true;

        challenge.classList.remove("challenge-locked");

        username.disabled = false;
        password.disabled = false;
        loginButton.disabled = false;

        loginStatus.textContent =
            "Perform the invalid login first.";

        loginStatus.className =
            "game-message";
    }

    unlockBtn.addEventListener("click", function () {

        if (levelKey.value.trim() === LEVEL17_KEY) {

            unlockChallenge();

            unlockMsg.textContent = "✓ Unlocked";
            unlockMsg.className = "game-message success";

        } else {

            unlockMsg.textContent = "✗ Incorrect key";
            unlockMsg.className = "game-message error";

            lockChallenge();
        }

    });

    loginButton.addEventListener("click", function () {

        if (!unlocked) return;

        const enteredUsername = username.value;
        const enteredPassword = password.value;

        /*
         * Attempt 1 — Invalid Login
         */

        if (
            enteredUsername !== VALID_USERNAME ||
            enteredPassword !== VALID_PASSWORD
        ) {

            invalidCompleted = true;

            loginStatus.textContent = INVALID_MESSAGE;
            loginStatus.className = "game-message error";

            attempt1.textContent =
                "1. Invalid login: ✓ Completed";

            if (!validCompleted) {
                loginStatus.textContent +=
                    " — Now enter the correct credentials.";
            }

            return;
        }

        /*
         * Attempt 2 — Valid Login
         */

        if (
            invalidCompleted &&
            enteredUsername === VALID_USERNAME &&
            enteredPassword === VALID_PASSWORD
        ) {

            validCompleted = true;

            loginStatus.textContent = SUCCESS_MESSAGE;
            loginStatus.className = "game-message success";

            attempt2.textContent =
                "2. Valid login: ✓ Completed";

            continueButton.disabled = false;
        }

    });

    continueButton.addEventListener("click", function () {

        if (!invalidCompleted || !validCompleted) {
            return;
        }

        continueStatus.textContent =
            "3. Continue: ✓ Completed";

        continueStatus.className =
            "game-message success";

        nextKey.style.display = "block";
    });

    resetBtn.addEventListener("click", function () {

        levelKey.value = "";

        username.value = "";
        password.value = "";

        unlockMsg.textContent = "";

        loginStatus.textContent =
            "Challenge locked.";

        loginStatus.className =
            "game-message";

        attempt1.textContent =
            "1. Invalid login: Not completed";

        attempt2.textContent =
            "2. Valid login: Not completed";

        continueStatus.textContent =
            "3. Continue: Not completed";

        continueStatus.className =
            "game-message";

        nextKey.style.display = "none";

        lockChallenge();
    });

    lockChallenge();

})();
</script>
