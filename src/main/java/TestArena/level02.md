# Level 02 — Form Filling

## Mission

Before attempting this level, enter the unlock key from **Level 01**.
After unlocking, use Selenium to fill and submit the login form.

**Credentials**

- Username: `student`
- Password: `selenium123`

---

## Unlock Level 02

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
    margin: 3px 0 7px;
    border: 1px solid #cbd5e1;
    border-radius: 5px;
    font-size: 12px;
    box-sizing: border-box;
}

.selenium-game .game-label {
    display: block;
    font-size: 12px;
    margin-top: 7px;
    margin-bottom: 3px;
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
    placeholder="Enter Level 01 Key"
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

Enter the correct username and password using Selenium.

<div
    id="challenge"
    class="selenium-game challenge-locked">

<label
    for="studentUsername"
    class="game-label">
    Username
</label>

<input
    type="text"
    id="studentUsername"
    name="username"
    placeholder="Username"
    autocomplete="off"
    disabled
>

<label
    for="studentPassword"
    class="game-label">
    Password
</label>

<input
    type="password"
    id="studentPassword"
    name="password"
    placeholder="Password"
    autocomplete="off"
    disabled
>

<button
    type="button"
    id="loginBtn"
    class="primary-button"
    disabled>
    Login
</button>

<p
    id="loginMsg"
    class="game-message">
</p>

<div
    id="nextKey"
    class="key-box">

    <strong>Level 02 Completed</strong>

    <p>
        Congratulations! You completed Level 02.
    </p>

    <p>
        Use this key to unlock Level 03:
    </p>

    <span class="key">
        SEL-02-P8M4-X7Q1
    </span>

</div>

</div>

<script>
(function () {

    const LEVEL1_KEY = "SEL-01-A7X9-K4P2";

    const unlockBtn =
        document.getElementById("unlockBtn");

    const resetBtn =
        document.getElementById("resetBtn");

    const unlockMsg =
        document.getElementById("unlockMsg");

    const challenge =
        document.getElementById("challenge");

    const keyInput =
        document.getElementById("levelKey");

    const username =
        document.getElementById("studentUsername");

    const password =
        document.getElementById("studentPassword");

    const loginBtn =
        document.getElementById("loginBtn");

    const loginMsg =
        document.getElementById("loginMsg");

    const nextKey =
        document.getElementById("nextKey");


    function lockChallenge() {

        username.disabled = true;
        password.disabled = true;
        loginBtn.disabled = true;

        challenge.classList.add(
            "challenge-locked"
        );
    }


    function unlockChallenge() {

        username.disabled = false;
        password.disabled = false;
        loginBtn.disabled = false;

        challenge.classList.remove(
            "challenge-locked"
        );
    }


    lockChallenge();


    unlockBtn.addEventListener(
        "click",
        function () {

            const enteredKey =
                keyInput.value.trim();

            if (enteredKey === LEVEL1_KEY) {

                unlockChallenge();

                unlockMsg.className =
                    "game-message success";

                unlockMsg.textContent =
                    "Level 02 unlocked.";

            } else {

                lockChallenge();

                unlockMsg.className =
                    "game-message error";

                unlockMsg.textContent =
                    "Invalid key.";
            }
        }
    );


    loginBtn.addEventListener(
        "click",
        function () {

            const enteredUsername =
                username.value;

            const enteredPassword =
                password.value;


            if (
                enteredUsername === "student" &&
                enteredPassword === "selenium123"
            ) {

                loginMsg.className =
                    "game-message success";

                loginMsg.textContent =
                    "Login successful.";

                nextKey.style.display =
                    "block";

            } else {

                loginMsg.className =
                    "game-message error";

                loginMsg.textContent =
                    "Incorrect username or password.";

                nextKey.style.display =
                    "none";
            }
        }
    );


    resetBtn.addEventListener(
        "click",
        function () {

            keyInput.value = "";
            username.value = "";
            password.value = "";

            lockChallenge();

            unlockMsg.textContent = "";
            unlockMsg.className =
                "game-message";

            loginMsg.textContent = "";
            loginMsg.className =
                "game-message";

            nextKey.style.display =
                "none";
        }
    );

})();
</script>