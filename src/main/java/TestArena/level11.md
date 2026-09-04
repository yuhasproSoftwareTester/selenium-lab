# Level 11 — Multiple Elements

## Mission

This page contains multiple products with the same CSS class.
Your task is to find the product named:

**Selenium WebDriver**

There are several products on the page, and all of their buttons use the same locator.

You must use Selenium to:

1. Find all matching product elements.
2. Loop through the elements.
3. Find **Selenium WebDriver**.
4. Click its **Add to Cart** button.

Do not directly locate the Selenium WebDriver button using a unique ID.

---

## Unlock Level 11

Enter the key obtained from **Level 10**.

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

.selenium-game .product {
    max-width: 420px;
    padding: 8px 10px;
    margin: 5px 0;
    border: 1px solid #cbd5e1;
    border-radius: 6px;
}

.selenium-game .product-name {
    font-weight: 600;
    margin-bottom: 4px;
}
</style>

<div class="selenium-game">

<input
    type="text"
    id="levelKey"
    class="game-input"
    placeholder="Enter Level 10 key"
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
        Find the product <strong>Selenium WebDriver</strong>
        and add it to the cart.
    </p>

    <div class="product product-item">

        <div class="product-name">
            Java Programming
        </div>

        <button
            type="button"
            class="add-cart"
            disabled>
            Add to Cart
        </button>

    </div>


    <div class="product product-item">

        <div class="product-name">
            Python Automation
        </div>

        <button
            type="button"
            class="add-cart"
            disabled>
            Add to Cart
        </button>

    </div>


    <div class="product product-item">

        <div class="product-name">
            Selenium WebDriver
        </div>

        <button
            type="button"
            class="add-cart"
            disabled>
            Add to Cart
        </button>

    </div>


    <div class="product product-item">

        <div class="product-name">
            TestNG Framework
        </div>

        <button
            type="button"
            class="add-cart"
            disabled>
            Add to Cart
        </button>

    </div>


    <div class="product product-item">

        <div class="product-name">
            Cucumber
        </div>

        <button
            type="button"
            class="add-cart"
            disabled>
            Add to Cart
        </button>

    </div>


    <p
        id="status"
        class="game-message">
        Challenge locked.
    </p>


    <div
        id="nextKey"
        class="key-box">

        <strong>Level 11 Completed</strong>

        <p>
            You successfully found the correct element
            from multiple elements.
        </p>

        <p>
            Use this key to unlock Level 12:
        </p>

        <span class="key">
            SEL-11-V6R2-K8P5
        </span>

    </div>

</div>

<script>
(function () {

    /*
     * ==========================================
     * LEVEL 11 — MULTIPLE ELEMENTS
     * ==========================================
     *
     * LEVEL 10 KEY
     * SEL-10-Q7N4-L2M8
     *
     * TARGET PRODUCT
     * Selenium WebDriver
     *
     * LEVEL 12 KEY
     * SEL-11-V6R2-K8P5
     * ==========================================
     */

    const LEVEL10_KEY =
        "SEL-10-Q7N4-L2M8";

    const TARGET_PRODUCT =
        "Selenium WebDriver";


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

    const products =
        document.querySelectorAll(".product-item");

    const buttons =
        document.querySelectorAll(".add-cart");


    let unlocked = false;


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

        buttons.forEach(
            function (button) {
                button.disabled = true;
            }
        );
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

        buttons.forEach(
            function (button) {
                button.disabled = false;
            }
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
     * UNLOCK LEVEL 11
     * ==========================================
     */

    unlockBtn.addEventListener(
        "click",
        function () {

            const enteredKey =
                levelKey.value.trim();

            if (enteredKey === LEVEL10_KEY) {

                unlockChallenge();

                unlockMsg.className =
                    "game-message success";

                unlockMsg.textContent =
                    "✓ Challenge unlocked.";

                status.className =
                    "game-message";

                status.textContent =
                    "Find Selenium WebDriver from the multiple elements.";

            } else {

                lockChallenge();

                unlockMsg.className =
                    "game-message error";

                unlockMsg.textContent =
                    "✗ Incorrect Level 10 key.";

                status.className =
                    "game-message";

                status.textContent =
                    "Challenge locked.";
            }
        }
    );


    /*
     * ==========================================
     * PRODUCT BUTTONS
     * ==========================================
     *
     * Students should use Selenium to:
     *
     * 1. Find all .product-item elements.
     * 2. Loop through them.
     * 3. Read .product-name.
     * 4. Find Selenium WebDriver.
     * 5. Click the .add-cart button.
     *
     * ==========================================
     */

    buttons.forEach(
        function (button, index) {

            button.addEventListener(
                "click",
                function () {

                    if (!unlocked) {
                        return;
                    }

                    const product =
                        products[index];

                    const productName =
                        product
                            .querySelector(
                                ".product-name"
                            )
                            .textContent
                            .trim();


                    if (
                        productName === TARGET_PRODUCT
                    ) {

                        status.className =
                            "game-message success";

                        status.textContent =
                            "✓ Correct element found!";

                        nextKey.style.display =
                            "block";

                    } else {

                        status.className =
                            "game-message error";

                        status.textContent =
                            "✗ Wrong product. Keep searching.";
                    }
                }
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

            levelKey.value = "";

            lockChallenge();

            unlockMsg.textContent = "";
            unlockMsg.className =
                "game-message";

            status.className =
                "game-message";

            status.textContent =
                "Challenge locked.";

            nextKey.style.display =
                "none";
        }
    );

})();
</script>