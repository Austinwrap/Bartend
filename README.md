<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>Celebrity Bartender - Mix & Earn!</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700&display=swap');

        body {
            font-family: 'Comic Sans MS', cursive, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            margin: 0;
            padding: 10px;
            background-color: #3c4a63;
            color: #e0e0e0;
        }
        .business-status {
            margin-bottom: 10px;
            text-align: center;
            border: 3px solid #506680;
            padding: 10px;
            background-color: #526e8f;
            border-radius: 10px;
            max-width: 90%;
            box-sizing: border-box;
        }
        .buttons-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 10px;
            max-width: 90%;
        }
        button, select {
            margin: 5px;
            padding: 15px;
            font-size: 16px;
            border: 2px solid #1f5b85;
            border-radius: 20px;
            background-color: #ff7f50;
            color: #ffffff;
            cursor: pointer;
            box-shadow: 2px 2px 10px #333;
            transition: transform 0.2s, background-color 0.3s;
            max-width: 200px;
        }
        button:hover, select:hover {
            background-color: #ff6347;
            transform: scale(1.1);
        }
        h1 {
            font-family: 'Playfair Display', serif;
            color: #ffc107;
            text-shadow: 2px 2px #000;
            font-size: 2.5em;
            letter-spacing: 1px;
            font-weight: bold;
            text-align: center;
        }
        .rules {
            border: 3px dashed #506680;
            padding: 15px;
            margin-top: 20px;
            background-color: #607d99;
            border-radius: 10px;
            max-width: 90%;
            box-sizing: border-box;
        }
        .tycoon-rank {
            font-weight: bold;
            font-size: 1.5em;
            color: #ffa500;
            text-shadow: 2px 2px 4px #000;
            letter-spacing: 1px;
        }
        .money-display {
            font-size: 1.8em;
            color: #ffd700;
            font-weight: bold;
            text-shadow: 1px 1px 3px #000;
            padding: 10px;
            background-color: #3f546d;
            border: 3px solid #1f5b85;
            border-radius: 10px;
            margin-top: 10px;
        }
        .order-display {
            font-size: 1.2em;
            font-weight: bold;
            margin-top: 15px;
            color: #ffcccb;
        }
        .ingredients-container {
            margin-top: 20px;
            padding: 15px;
            border: 3px solid #506680;
            background-color: #526e8f;
            border-radius: 10px;
            max-width: 90%;
            box-sizing: border-box;
        }
        .ingredient-section {
            margin-bottom: 20px;
        }
        .ingredient-section h3 {
            margin-bottom: 10px;
            font-size: 1.5em;
            color: #ffcccb;
        }
        .ingredient-button {
            margin: 5px;
            padding: 10px;
            font-size: 14px;
            border: 2px solid #1f5b85;
            border-radius: 15px;
            background-color: #4caf50;
            color: #ffffff;
            cursor: pointer;
            transition: transform 0.2s, background-color 0.3s;
        }
        .ingredient-button.selected {
            background-color: #8bc34a;
        }
        .danger-border {
            border: 5px solid red;
            animation: dangerFlash 0.5s alternate infinite;
        }
        @keyframes dangerFlash {
            0% { border-color: red; }
            100% { border-color: black; }
        }
        .notepad {
            border: 3px solid #1f5b85;
            padding: 15px;
            margin-top: 20px;
            background-color: #394b5f;
            color: #ffcccb;
            border-radius: 10px;
            max-width: 90%;
            box-sizing: border-box;
        }
        .notepad h2 {
            font-size: 1.5em;
            margin-bottom: 10px;
        }
        .notepad ul {
            list-style-type: none;
            padding-left: 0;
        }
        .notepad ul li {
            margin: 5px 0;
        }
    </style>
</head>
<body>
    <h1>Celebrity Bartender - Mix & Earn!</h1>
    <div class="business-status">
        <p>Income per Second: $<span id="incomePerSecond">0</span></p>
        <p>Tips Earned: $<span id="tips">0</span></p>
        <p>Drinks Made: <span id="drinksMade">0</span></p>
        <p class="money-display">Money: $<span id="money">0</span></p>
        <p>Bartender Rank: <span id="bartenderRank" class="tycoon-rank">Barback Trainee</span></p>
    </div>

    <div class="buttons-container">
        <button onclick="takeOrder()">📋 Take New Order</button>
        <button onclick="makeDrink()">🍹 Make Drink</button>
        <button onclick="buyUpgrade('betterShaker')">🔧 Upgrade: Better Shaker ($200)</button>
        <button onclick="buyUpgrade('fancyGlassware')">🥂 Upgrade: Fancy Glassware ($500)</button>
        <button onclick="buyUpgrade('bartenderAssistant')">👥 Hire Bartender Assistant ($1000)</button>
    </div>

    <div class="order-display" id="currentOrder"></div>

    <div class="notepad" id="notepad">
        <h2>Pending Orders</h2>
        <ul id="pendingOrders"></ul>
    </div>

    <div class="ingredients-container">
        <h2>Select Ingredients to Make the Drink:</h2>
        <div class="ingredient-section">
            <h3>Alcohols</h3>
            <button class="ingredient-button" onclick="selectIngredient('Vodka')">Vodka</button>
            <button class="ingredient-button" onclick="selectIngredient('Tequila')">Tequila</button>
            <button class="ingredient-button" onclick="selectIngredient('White Rum')">White Rum</button>
            <button class="ingredient-button" onclick="selectIngredient('Dark Rum')">Dark Rum</button>
            <button class="ingredient-button" onclick="selectIngredient('Whiskey')">Whiskey</button>
            <button class="ingredient-button" onclick="selectIngredient('Irish Whiskey')">Irish Whiskey</button>
            <button class="ingredient-button" onclick="selectIngredient('Gin')">Gin</button>
            <button class="ingredient-button" onclick="selectIngredient('Vermouth')">Vermouth</button>
            <button class="ingredient-button" onclick="selectIngredient('Cachaça')">Cachaça</button>
            <button class="ingredient-button" onclick="selectIngredient('Aperol')">Aperol</button>
            <button class="ingredient-button" onclick="selectIngredient('Campari')">Campari</button>
        </div>
        <div class="ingredient-section">
            <h3>Mixers & Juices</h3>
            <button class="ingredient-button" onclick="selectIngredient('Triple Sec')">Triple Sec</button>
            <button class="ingredient-button" onclick="selectIngredient('Lime Juice')">Lime Juice</button>
            <button class="ingredient-button" onclick="selectIngredient('Lemon Juice')">Lemon Juice</button>
            <button class="ingredient-button" onclick="selectIngredient('Cranberry Juice')">Cranberry Juice</button>
            <button class="ingredient-button" onclick="selectIngredient('Pineapple Juice')">Pineapple Juice</button>
            <button class="ingredient-button" onclick="selectIngredient('Orange Juice')">Orange Juice</button>
            <button class="ingredient-button" onclick="selectIngredient('Tomato Juice')">Tomato Juice</button>
            <button class="ingredient-button" onclick="selectIngredient('Tonic Water')">Tonic Water</button>
            <button class="ingredient-button" onclick="selectIngredient('Soda Water')">Soda Water</button>
            <button class="ingredient-button" onclick="selectIngredient('Ginger Beer')">Ginger Beer</button>
            <button class="ingredient-button" onclick="selectIngredient('Cola')">Cola</button>
            <button class="ingredient-button" onclick="selectIngredient('Club Soda')">Club Soda</button>
            <button class="ingredient-button" onclick="selectIngredient('Peach Puree')">Peach Puree</button>
            <button class="ingredient-button" onclick="selectIngredient('Simple Syrup')">Simple Syrup</button>
            <button class="ingredient-button" onclick="selectIngredient('Grenadine')">Grenadine</button>
            <button class="ingredient-button" onclick="selectIngredient('Coconut Cream')">Coconut Cream</button>
        </div>
        <div class="ingredient-section">
            <h3>Beers</h3>
            <button class="ingredient-button" onclick="selectIngredient('Light Beer')">Light Beer</button>
            <button class="ingredient-button" onclick="selectIngredient('Dark Beer')">Dark Beer</button>
            <button class="ingredient-button" onclick="selectIngredient('IPA Beer')">IPA Beer</button>
        </div>
        <div class="ingredient-section">
            <h3>Wines & Seltzers</h3>
            <button class="ingredient-button" onclick="selectIngredient('Red Wine')">Red Wine</button>
            <button class="ingredient-button" onclick="selectIngredient('White Wine')">White Wine</button>
            <button class="ingredient-button" onclick="selectIngredient('Rosé Wine')">Rosé Wine</button>
            <button class="ingredient-button" onclick="selectIngredient('Prosecco')">Prosecco</button>
            <button class="ingredient-button" onclick="selectIngredient('White Claw')">White Claw</button>
            <button class="ingredient-button" onclick="selectIngredient('Truly')">Truly</button>
        </div>
        <div class="ingredient-section">
            <h3>Garnishes & Other Ingredients</h3>
            <button class="ingredient-button" onclick="selectIngredient('Mint')">Mint</button>
            <button class="ingredient-button" onclick="selectIngredient('Olive')">Olive</button>
            <button class="ingredient-button" onclick="selectIngredient('Cherry')">Cherry</button>
            <button class="ingredient-button" onclick="selectIngredient('Egg White')">Egg White</button>
            <button class="ingredient-button" onclick="selectIngredient('Sugar')">Sugar</button>
            <button class="ingredient-button" onclick="selectIngredient('Cream')">Cream</button>
            <button class="ingredient-button" onclick="selectIngredient('Coffee')">Coffee</button>
        </div>
        <div class="ingredient-section">
            <h3>Glassware</h3>
            <button class="ingredient-button" onclick="selectIngredient('Tall Glass')">Tall Glass</button>
            <button class="ingredient-button" onclick="selectIngredient('Short Glass')">Short Glass</button>
            <button class="ingredient-button" onclick="selectIngredient('Martini Glass')">Martini Glass</button>
            <button class="ingredient-button" onclick="selectIngredient('Mug')">Mug</button>
            <button class="ingredient-button" onclick="selectIngredient('Champagne Flute')">Champagne Flute</button>
        </div>
    </div>

    <div class="rules">
        <h2>Game Rule Book & Directions</h2>
        <p>Welcome to Celebrity Bartender! Here's how to play:</p>
        <ul>
            <li>Start as a Barback Trainee and work your way up to become the ultimate Celebrity Bartender!</li>
            <li>Take drink orders, mix drinks, and earn tips.</li>
            <li>Buy upgrades to improve your bartending skills and efficiency.</li>
        </ul>
    </div>

    <script>
        let tips = 0;
        let drinksMade = 0;
        let money = 0;
        let bartenderRank = "Barback Trainee";
        let currentOrder = "";
        let pendingOrders = [];
        let incomePerDrink = 10;
        let currentOrderIngredients = [];
        let selectedIngredients = [];
        let orderTimer = null;

        const drinkRecipes = {
            "Margarita": ["Tequila", "Triple Sec", "Lime Juice", "Tall Glass"],
            "Old Fashioned": ["Whiskey", "Bitters", "Sugar", "Short Glass"],
            "Mojito": ["White Rum", "Lime Juice", "Mint", "Soda Water", "Tall Glass"],
            "Bloody Mary": ["Vodka", "Tomato Juice", "Lemon Juice", "Celery", "Tall Glass"],
            "Martini": ["Gin", "Vermouth", "Olive", "Martini Glass"],
            "Pina Colada": ["White Rum", "Pineapple Juice", "Coconut Cream", "Tall Glass"],
            "Cosmopolitan": ["Vodka", "Triple Sec", "Cranberry Juice", "Lime Juice", "Martini Glass"],
            "Whiskey Sour": ["Whiskey", "Lemon Juice", "Sugar", "Egg White", "Short Glass"],
            "Long Island Iced Tea": ["Vodka", "Tequila", "White Rum", "Gin", "Triple Sec", "Cola", "Tall Glass"],
            "Gin Tonic": ["Gin", "Tonic Water", "Lime Juice", "Tall Glass"],
            "Daiquiri": ["White Rum", "Lime Juice", "Simple Syrup", "Short Glass"],
            "Mai Tai": ["Dark Rum", "White Rum", "Lime Juice", "Triple Sec", "Grenadine", "Tall Glass"],
            "Negroni": ["Gin", "Campari", "Vermouth", "Short Glass"],
            "Moscow Mule": ["Vodka", "Lime Juice", "Ginger Beer", "Mug"],
            "Screwdriver": ["Vodka", "Orange Juice", "Tall Glass"],
            "Irish Coffee": ["Irish Whiskey", "Coffee", "Cream", "Mug"],
            "Aperol Spritz": ["Aperol", "Prosecco", "Soda Water", "Champagne Flute"],
            "Tequila Sunrise": ["Tequila", "Orange Juice", "Grenadine", "Tall Glass"],
            "Rum Punch": ["Dark Rum", "Pineapple Juice", "Orange Juice", "Grenadine", "Tall Glass"]
        };

        function takeOrder() {
            const drinks = Object.keys(drinkRecipes);
            const randomDrink = drinks[Math.floor(Math.random() * drinks.length)];
            currentOrder = randomDrink;
            currentOrderIngredients = drinkRecipes[randomDrink];
            pendingOrders.push(currentOrder);
            updatePendingOrders();
            displayCurrentOrder();
            startOrderTimer();
        }

        function displayCurrentOrder() {
            document.getElementById("currentOrder").innerText = `Order: ${currentOrder} - Ingredients: ${currentOrderIngredients.join(", ")}`;
        }

        function updatePendingOrders() {
            const pendingOrdersList = document.getElementById("pendingOrders");
            pendingOrdersList.innerHTML = "";
            pendingOrders.forEach((order, index) => {
                const li = document.createElement("li");
                li.innerText = order;
                pendingOrdersList.appendChild(li);
            });
        }

        function selectIngredient(ingredient) {
            if (selectedIngredients.includes(ingredient)) {
                selectedIngredients = selectedIngredients.filter(item => item !== ingredient);
                document.querySelector(`[onclick="selectIngredient('${ingredient}')"]`).classList.remove("selected");
            } else {
                selectedIngredients.push(ingredient);
                document.querySelector(`[onclick="selectIngredient('${ingredient}')"]`).classList.add("selected");
            }
        }

        function makeDrink() {
            if (currentOrder === "") {
                alert("No order taken!");
                return;
            }

            if (arraysEqual(selectedIngredients, currentOrderIngredients)) {
                tips += incomePerDrink;
                drinksMade++;
                money += incomePerDrink;
                pendingOrders.shift();
                resetOrder();
                alert("Drink made perfectly! You earned a tip!");
            } else {
                tips += incomePerDrink / 2;
                drinksMade++;
                pendingOrders.shift();
                resetOrder();
                alert("Drink made incorrectly. Partial tip received.");
            }

            updateGameStatus();
        }

        function resetOrder() {
            currentOrder = "";
            currentOrderIngredients = [];
            selectedIngredients = [];
            updatePendingOrders();
            displayCurrentOrder();
            clearIngredientSelections();
            clearOrderTimer();
        }

        function clearIngredientSelections() {
            document.querySelectorAll(".ingredient-button").forEach(button => {
                button.classList.remove("selected");
            });
        }

        function arraysEqual(arr1, arr2) {
            if (arr1.length !== arr2.length) return false;
            return arr1.sort().every((value, index) => value === arr2.sort()[index]);
        }

        function updateGameStatus() {
            document.getElementById("tips").innerText = tips;
            document.getElementById("drinksMade").innerText = drinksMade;
            document.getElementById("money").innerText = money;
            updateBartenderRank();
        }

        function updateBartenderRank() {
            if (drinksMade >= 50) {
                bartenderRank = "Celebrity Bartender";
            } else if (drinksMade >= 30) {
                bartenderRank = "Master Mixologist";
            } else if (drinksMade >= 15) {
                bartenderRank = "Experienced Bartender";
            } else if (drinksMade >= 5) {
                bartenderRank = "Junior Bartender";
            } else {
                bartenderRank = "Barback Trainee";
            }
            document.getElementById("bartenderRank").innerText = bartenderRank;
        }

        function startOrderTimer() {
            if (orderTimer) {
                clearTimeout(orderTimer);
            }
            orderTimer = setTimeout(() => {
                document.body.classList.add("danger-border");
                alert("Time's up! You lost the opportunity for a tip!");
                resetOrder();
            }, 30000);
        }

        function clearOrderTimer() {
            if (orderTimer) {
                clearTimeout(orderTimer);
                document.body.classList.remove("danger-border");
                orderTimer = null;
            }
        }

        function buyUpgrade(upgrade) {
            switch (upgrade) {
                case 'betterShaker':
                    if (money >= 200) {
                        money -= 200;
                        incomePerDrink += 5;
                        alert("Upgrade purchased: Better Shaker! Increased tip earnings.");
                    } else {
                        alert("Not enough money for this upgrade.");
                    }
                    break;
                case 'fancyGlassware':
                    if (money >= 500) {
                        money -= 500;
                        incomePerDrink += 10;
                        alert("Upgrade purchased: Fancy Glassware! Customers are tipping more.");
                    } else {
                        alert("Not enough money for this upgrade.");
                    }
                    break;
                case 'bartenderAssistant':
                    if (money >= 1000) {
                        money -= 1000;
                        incomePerDrink += 20;
                        alert("Upgrade purchased: Bartender Assistant! More tips for faster service.");
                    } else {
                        alert("Not enough money for this upgrade.");
                    }
                    break;
                default:
                    alert("Unknown upgrade.");
            }
            updateGameStatus();
        }
    </script>
</body>
</html>
