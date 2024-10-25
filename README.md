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
            "Mojito": ["White Rum", "Sugar", "Mint", "Soda Water", "Tall Glass"],
            "Cosmopolitan": ["Vodka", "Triple Sec", "Cranberry Juice", "Lime Juice", "Martini Glass"],
            "Whiskey Sour": ["Whiskey", "Lemon Juice", "Sugar", "Short Glass"],
            "Martini": ["Gin", "Vermouth", "Olive", "Martini Glass"],
            "Daiquiri": ["White Rum", "Lime Juice", "Sugar", "Short Glass"],
            "Pina Colada": ["White Rum", "Coconut Cream", "Pineapple Juice", "Tall Glass"],
            "Gin Tonic": ["Gin", "Tonic Water", "Lime Juice", "Tall Glass"],
            "Bloody Mary": ["Vodka", "Tomato Juice", "Lemon Juice", "Tall Glass"],
            "Mai Tai": ["White Rum", "Dark Rum", "Lime Juice", "Triple Sec", "Tall Glass"],
            "Negroni": ["Gin", "Campari", "Vermouth", "Short Glass"],
            "Moscow Mule": ["Vodka", "Lime Juice", "Ginger Beer", "Mug"],
            "Bellini": ["Prosecco", "Peach Puree", "Champagne Flute"],
            "Irish Coffee": ["Coffee", "Irish Whiskey", "Sugar", "Cream", "Mug"],
            "Long Island Iced Tea": ["Vodka", "Tequila", "White Rum", "Triple Sec", "Gin", "Cola", "Tall Glass"],
            "Caipirinha": ["Cachaça", "Sugar", "Lime Juice", "Short Glass"],
            "Screwdriver": ["Vodka", "Orange Juice", "Tall Glass"],
            "Aperol Spritz": ["Aperol", "Prosecco", "Club Soda", "Tall Glass"],
            "Whiskey Smash": ["Whiskey", "Lemon Juice", "Mint", "Short Glass"]
        };

        function takeOrder() {
            if (currentOrder) {
                pendingOrders.push(currentOrder);
                updatePendingOrders();
            }
            let drinks = Object.keys(drinkRecipes);
            currentOrder = drinks[Math.floor(Math.random() * drinks.length)];
            currentOrderIngredients = drinkRecipes[currentOrder];
            document.getElementById("currentOrder").innerText = `New Order: ${currentOrder} - Ingredients: ${currentOrderIngredients.join(", ")}`;
            startOrderTimer();
        }

        function makeDrink() {
            if (currentOrder) {
                if (arraysEqual(selectedIngredients, currentOrderIngredients)) {
                    tips += incomePerDrink;
                    drinksMade++;
                    money += incomePerDrink;
                    showMessage(`Perfect! You made a ${currentOrder} and earned $${incomePerDrink}`);
                } else {
                    showMessage(`Oops! The ${currentOrder} wasn't quite right. You earned less tips.`);
                    tips += incomePerDrink / 2;
                    money += incomePerDrink / 2;
                }
                selectedIngredients = [];
                currentOrder = "";
                document.getElementById("currentOrder").innerText = "";
                updateBusinessStatus();
                clearOrderTimer();
            } else {
                showMessage("No current order to make!");
            }
        }

        function selectIngredient(ingredient) {
            if (!selectedIngredients.includes(ingredient)) {
                selectedIngredients.push(ingredient);
                showMessage(`Selected: ${ingredient}`);
            } else {
                showMessage(`${ingredient} is already selected!`);
            }
        }

        function updatePendingOrders() {
            const pendingOrdersList = document.getElementById("pendingOrders");
            pendingOrdersList.innerHTML = "";
            pendingOrders.forEach(order => {
                const li = document.createElement("li");
                li.textContent = order;
                pendingOrdersList.appendChild(li);
            });
        }

        function updateBusinessStatus() {
            document.getElementById("tips").innerText = tips;
            document.getElementById("drinksMade").innerText = drinksMade;
            document.getElementById("money").innerText = money;
            updateBartenderRank();
        }

        function updateBartenderRank() {
            if (money >= 1000) {
                bartenderRank = "Mixologist";
            } else if (money >= 500) {
                bartenderRank = "Bartender Extraordinaire";
            } else if (money >= 200) {
                bartenderRank = "Junior Bartender";
            }
            document.getElementById("bartenderRank").innerText = bartenderRank;
        }

        function buyUpgrade(upgrade) {
            if (upgrade === 'betterShaker' && money >= 200) {
                money -= 200;
                incomePerDrink += 5;
                showMessage("Purchased Better Shaker! Income per drink increased.");
            } else if (upgrade === 'fancyGlassware' && money >= 500) {
                money -= 500;
                incomePerDrink += 10;
                showMessage("Purchased Fancy Glassware! Income per drink increased.");
            } else if (upgrade === 'bartenderAssistant' && money >= 1000) {
                money -= 1000;
                incomePerDrink += 20;
                showMessage("Hired Bartender Assistant! Income per drink increased.");
            } else {
                showMessage("Not enough money for this upgrade!");
            }
            updateBusinessStatus();
        }

        function showMessage(message) {
            const currentOrderDisplay = document.getElementById("currentOrder");
            currentOrderDisplay.innerText = message;
        }

        function startOrderTimer() {
            clearOrderTimer();
            orderTimer = setTimeout(() => {
                showMessage("Time's up! You missed the order.");
                currentOrder = "";
                updatePendingOrders();
            }, 30000); // 30 seconds to complete the order
        }

        function clearOrderTimer() {
            if (orderTimer) {
                clearTimeout(orderTimer);
                orderTimer = null;
            }
        }

        function arraysEqual(a, b) {
            if (a.length !== b.length) return false;
            a.sort();
            b.sort();
            for (let i = 0; i < a.length; i++) {
                if (a[i] !== b[i]) return false;
            }
            return true;
        }
    </script>
</body>
</html>
