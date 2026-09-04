# Level 03 — CSS Selector

## Mission

Before attempting this level, enter the unlock key from **Level 02**.
After unlocking, find the correct product and add it to the cart using Selenium.
**Important:** The target button does not have a useful ID. Practice using a **CSS Selector** to locate it.

---

## Unlock Level 03

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

.selenium-game .products {
    display: flex;
    flex-wrap: wrap;
    gap: 7px;
    margin-top: 8px;
}

.selenium-game .product {
    width: 180px;
    padding: 9px;
    border: 1px solid #cbd5e1;
    border-radius: 6px;
    background: white;
}

.selenium-game .product-name {
    font-weight: 600;
    margin-bottom: 5px;
    font-size: 13px;
}

.selenium-game .price {
    margin-bottom: 7px;
    font-size: 12px;
}

.selenium-game .cart {
    max-width: 400px;
    margin-top: 10px;
    padding: 9px;
    background: #f1f5f9;
    border-radius: 6px;
}
</style>

<div class="selenium-game">

<input
    type="text"
    id="levelKey"
    placeholder="Enter Level 02 Key"
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

Add the **Selenium Automation Book** to the cart.

<div
    id="challenge"
    class="selenium-game challenge-locked">

<div class="products">

<div class="product">

<div class="product-name">
Java Programming Book
</div>

<div class="price">
₹450
</div>

<button
    class="add-cart"
    data-product="java"
    disabled>
    Add to Cart
</button>

</div>

<div class="product">

<div class="product-name">
Selenium Automation Book
</div>

<div class="price">
₹599
</div>

<button
    class="add-cart"
    data-product="selenium"
    disabled>
    Add to Cart
</button>

</div>

<div class="product">

<div class="product-name">
Python Testing Book
</div>

<div class="price">
₹520
</div>

<button
    class="add-cart"
    data-product="python"
    disabled>
    Add to Cart
</button>

</div>

</div>

<div class="cart">

<strong>Shopping Cart</strong>

<p id="cartStatus">
Cart is empty.
</p>

</div>

<p
    id="cartMsg"
    class="game-message">
</p>

<div
    id="nextKey"
    class="key-box">

<strong>Level 03 Completed</strong>

<p>
Congratulations! You completed Level 03.
</p>

<p>
Use this key to unlock Level 04:
</p>

<span class="key">
SEL-03-R6N2-W8K5
</span>

</div>

</div>

<script>
(function () {

    const LEVEL2_KEY =
        "SEL-02-P8M4-X7Q1";

    const unlockBtn =
        document.getElementById("unlockBtn");

    const resetBtn =
        document.getElementById("resetBtn");

    const keyInput =
        document.getElementById("levelKey");

    const unlockMsg =
        document.getElementById("unlockMsg");

    const challenge =
        document.getElementById("challenge");

    const cartStatus =
        document.getElementById("cartStatus");

    const cartMsg =
        document.getElementById("cartMsg");

    const nextKey =
        document.getElementById("nextKey");

    const productButtons =
        document.querySelectorAll(".add-cart");


    function lockChallenge() {

        productButtons.forEach(
            function (button) {
                button.disabled = true;
            }
        );

        challenge.classList.add(
            "challenge-locked"
        );
    }


    function unlockChallenge() {

        productButtons.forEach(
            function (button) {
                button.disabled = false;
            }
        );

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

            if (enteredKey === LEVEL2_KEY) {

                unlockChallenge();

                unlockMsg.className =
                    "game-message success";

                unlockMsg.textContent =
                    "Level 03 unlocked.";

            } else {

                lockChallenge();

                unlockMsg.className =
                    "game-message error";

                unlockMsg.textContent =
                    "Invalid key.";
            }
        }
    );


    productButtons.forEach(
        function (button) {

            button.addEventListener(
                "click",
                function () {

                    const product =
                        button.dataset.product;

                    if (product === "selenium") {

                        cartStatus.textContent =
                            "Selenium Automation Book — ₹599";

                        cartMsg.className =
                            "game-message success";

                        cartMsg.textContent =
                            "Correct product added to cart.";

                        nextKey.style.display =
                            "block";

                    } else {

                        cartStatus.textContent =
                            "Wrong product.";

                        cartMsg.className =
                            "game-message error";

                        cartMsg.textContent =
                            "Wrong product. Try again.";

                        nextKey.style.display =
                            "none";
                    }
                }
            );
        }
    );


    resetBtn.addEventListener(
        "click",
        function () {

            keyInput.value = "";

            lockChallenge();

            unlockMsg.textContent = "";
            unlockMsg.className =
                "game-message";

            cartMsg.textContent = "";
            cartMsg.className =
                "game-message";

            cartStatus.textContent =
                "Cart is empty.";

            nextKey.style.display =
                "none";
        }
    );

})();
</script>