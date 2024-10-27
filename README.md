<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Celebrity Bartender - Mix & Earn!</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        /* Importing Google Fonts */
        @import url('https://fonts.googleapis.com/css2?family=Pacifico&family=Roboto:wght@400;700&display=swap');

        /* Resetting default margins and paddings */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Roboto', sans-serif;
            background: linear-gradient(135deg, #f6d365 0%, #fda085 100%);
            color: #333;
            overflow-x: hidden;
        }

        h1 {
            font-family: 'Pacifico', cursive;
            color: #fff;
            text-align: center;
            margin: 20px 0;
            font-size: 3em;
            text-shadow: 0 0 5px rgba(255,255,255,0.8);
            position: relative;
        }

        /* Glimmering Stars */
        h1::before, h1::after {
            content: '✦';
            position: absolute;
            font-size: 1.5em;
            color: #fff;
            animation: twinkle 2s infinite;
        }

        h1::before {
            top: -10px;
            left: -30px;
            animation-delay: 0s;
        }

        h1::after {
            top: -10px;
            right: -30px;
            animation-delay: 1s;
        }

        @keyframes twinkle {
            0%, 100% { opacity: 0.2; transform: scale(1); }
            50% { opacity: 1; transform: scale(1.2); }
        }

        .game-container {
            max-width: 1000px;
            margin: 0 auto;
            padding: 0 20px;
        }

        .status-bar {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            background-color: rgba(255, 255, 255, 0.85);
            padding: 15px;
            border-radius: 15px;
            margin-bottom: 20px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .status-item {
            flex: 1 1 48%;
            margin: 10px 0;
            text-align: center;
        }

        .status-item p {
            font-size: 1.2em;
        }

        .money-display {
            font-size: 2em;
            color: #ff6b6b;
            font-weight: bold;
            text-shadow: 1px 1px #fff;
        }

        .buttons-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-around;
            margin-bottom: 20px;
        }

        button {
            background: linear-gradient(to bottom right, #ff9a9e, #fad0c4);
            color: #fff;
            border: none;
            border-radius: 50px;
            padding: 15px 25px;
            margin: 10px;
            font-size: 1em;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 6px 15px rgba(0,0,0,0.2);
            position: relative;
        }

        button::after {
            content: '';
            position: absolute;
            top: -5px;
            left: -5px;
            right: -5px;
            bottom: -5px;
            background: linear-gradient(45deg, transparent, rgba(255,255,255,0.3), transparent);
            border-radius: 50px;
            opacity: 0;
            transition: opacity 0.5s;
        }

        button:hover::after {
            opacity: 1;
        }

        button:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 20px rgba(0,0,0,0.3);
        }

        .order-display {
            background-color: rgba(255, 255, 255, 0.9);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 20px;
            position: relative;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            display: flex;
            align-items: flex-start;
            flex-direction: column;
        }

        .order-display h2 {
            margin-bottom: 15px;
            font-size: 1.5em;
            color: #ff6b6b;
        }

        .timer-bar {
            position: absolute;
            bottom: 0;
            left: 0;
            height: 8px;
            background-color: #4caf50;
            transition: width 0.1s linear;
            border-radius: 0 0 15px 15px;
        }

        .danger {
            background-color: #e74c3c !important;
            animation: dangerFlash 1s infinite;
        }

        @keyframes dangerFlash {
            0% { background-color: #e74c3c; }
            50% { background-color: #c0392b; }
            100% { background-color: #e74c3c; }
        }

        .ticket {
            background-color: #fff;
            padding: 15px;
            margin-bottom: 10px;
            border-left: 8px solid #ff6b6b;
            border-radius: 10px;
            position: relative;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
        }

        .ticket.stamped::after {
            content: attr(data-tip);
            position: absolute;
            top: -10px;
            right: -10px;
            background-color: #27ae60;
            color: #fff;
            padding: 5px 10px;
            transform: rotate(-20deg);
            font-weight: bold;
            border-radius: 5px;
            box-shadow: 0 3px 5px rgba(0,0,0,0.2);
        }

        .ingredients-container {
            margin-bottom: 20px;
        }

        .collapsible {
            background-color: #ff6b6b;
            color: #fff;
            cursor: pointer;
            padding: 15px;
            width: 100%;
            border: none;
            text-align: left;
            font-size: 1.2em;
            margin-bottom: 5px;
            border-radius: 10px;
            transition: background-color 0.3s ease;
        }

        .collapsible:hover, .collapsible.active {
            background-color: #ff7e7e;
        }

        .content {
            padding: 10px 20px;
            display: none;
            overflow: hidden;
            background-color: rgba(255, 255, 255, 0.9);
            border-radius: 0 0 10px 10px;
            margin-bottom: 10px;
            box-shadow: inset 0 3px 6px rgba(0,0,0,0.1);
        }

        .ingredient-button {
            background-color: #f0f0f0;
            color: #333;
            border: 2px solid #ccc;
            border-radius: 50px;
            padding: 10px 15px;
            margin: 5px;
            font-size: 0.9em;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .ingredient-button:hover {
            background-color: #e0e0e0;
            transform: translateY(-2px);
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        .ingredient-button.popular {
            font-size: 1em;
            background-color: #ffebcc;
        }

        .ingredient-button.required {
            font-size: 1.1em;
            background-color: #ffe0b3;
            border-color: #ff6b6b;
        }

        .ingredient-button.selected {
            background-color: #ff6b6b;
            color: #fff;
            border-color: #ff6b6b;
        }

        .rules {
            background-color: rgba(255, 255, 255, 0.9);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 20px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .rules h2 {
            margin-bottom: 15px;
            font-size: 1.5em;
            color: #ff6b6b;
        }

        .rules ul {
            list-style-type: disc;
            margin-left: 20px;
        }

        /* "Show Ingredients" Button */
        .show-ingredients-btn {
            background-color: #27ae60;
            color: #fff;
            border: none;
            border-radius: 30px;
            padding: 10px 15px;
            font-size: 0.9em;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-left: 10px;
        }

        .show-ingredients-btn:hover {
            background-color: #2ecc71;
            transform: translateY(-2px);
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        /* Search Bar */
        .search-container {
            margin: 20px 0;
            text-align: center;
        }

        .search-container input {
            width: 80%;
            padding: 10px;
            border-radius: 30px;
            border: 2px solid #ccc;
            font-size: 1em;
            outline: none;
        }

        /* Difficulty Selection Modal */
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            padding-top: 100px;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgba(0,0,0,0.7);
        }

        .modal-content {
            background-color: #fefefe;
            margin: auto;
            padding: 30px;
            border: 1px solid #888;
            width: 80%;
            max-width: 500px;
            border-radius: 10px;
            text-align: center;
        }

        .modal-content h2 {
            margin-bottom: 20px;
        }

        .difficulty-button {
            background-color: #ff6b6b;
            color: #fff;
            border: none;
            border-radius: 30px;
            padding: 15px 25px;
            margin: 10px;
            font-size: 1em;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        .difficulty-button:hover {
            background-color: #ff7e7e;
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .status-item {
                flex: 1 1 100%;
            }

            h1 {
                font-size: 2.5em;
            }

            .buttons-container button {
                flex: 1 1 45%;
                max-width: 100%;
            }

            .order-display {
                flex-direction: column;
                align-items: flex-start;
            }

            .show-ingredients-btn {
                margin-left: 0;
                margin-top: 10px;
            }
        }
    </style>
</head>
<body>
    <h1>Celebrity Bartender</h1>
    <div class="game-container">
        <!-- Status Bar -->
        <div class="status-bar">
            <div class="status-item">
                <p>Income per Second: $<span id="incomePerSecond">0</span></p>
            </div>
            <div class="status-item">
                <p>Tips Earned: $<span id="tips">0.00</span></p>
            </div>
            <div class="status-item">
                <p>Drinks Made: <span id="drinksMade">0</span></p>
            </div>
            <div class="status-item">
                <p class="money-display">Money: $<span id="money">0.00</span></p>
            </div>
            <div class="status-item">
                <p>Bartender Rank: <span id="bartenderRank">Barback Trainee</span></p>
            </div>
            <!-- New Status Items -->
            <div class="status-item">
                <p>Customer Satisfaction: <span id="customerSatisfaction">100%</span></p>
            </div>
            <div class="status-item">
                <p>Bar Popularity: <span id="barPopularity">50%</span></p>
            </div>
            <div class="status-item">
                <p>Bar Reputation: <span id="barReputation">Unknown</span></p>
            </div>
            <div class="status-item">
                <p>Time of Day: <span id="timeOfDay">Evening</span></p>
            </div>
            <div class="status-item">
                <p>Daily Sales: $<span id="dailySales">0.00</span></p>
            </div>
        </div>

        <!-- Buttons -->
        <div class="buttons-container">
            <button id="startGameBtn">🎬 Start Game</button>
            <button id="toggleIngredientsBtn">📝 Ingredients List</button>
            <button onclick="buyUpgrade('betterShaker')">🔧 Better Shaker ($200)</button>
            <button onclick="buyUpgrade('fancyGlassware')">🥂 Fancy Glassware ($500)</button>
            <button onclick="buyUpgrade('bartenderAssistant')">👥 Hire Assistant ($1000)</button>
        </div>

        <!-- Current Order Display -->
        <div class="order-display" id="currentOrderDisplay">
            <h2>Current Orders:</h2>
            <div id="orders"></div>
        </div>

        <!-- Ingredients List -->
        <div id="ingredientsList" style="display: none;">
            <!-- Search Bar -->
            <div class="search-container">
                <input type="text" id="ingredientSearch" placeholder="Search Ingredients..." oninput="filterIngredients()">
            </div>
            <!-- Ingredients buttons will be generated dynamically -->
        </div>

        <!-- Game Rules -->
        <div class="rules">
            <h2>Game Rules & Directions</h2>
            <p>Welcome to <strong>Celebrity Bartender</strong>! Here's how to play:</p>
            <ul>
                <li>🎬 <strong>Start Game:</strong> Click "Start Game" to begin your shift.</li>
                <li>📋 <strong>Take Orders:</strong> Orders will come in automatically; manage up to 3 at a time.</li>
                <li>🍹 <strong>Make Drinks:</strong> Select ingredients for each order by clicking on the ingredients list.</li>
                <li>⏳ <strong>Time Management:</strong> Serve each drink before its timer runs out to keep customers happy.</li>
                <li>💰 <strong>Earn Money:</strong> Correctly made drinks earn you money based on drink prices.</li>
                <li>🔧 <strong>Buy Upgrades:</strong> Use money to purchase upgrades and increase your income.</li>
                <li>🏆 <strong>Rank Up:</strong> Make more drinks to climb the ranks and improve your bar's reputation.</li>
                <li>📈 <strong>Manage Stock:</strong> Keep an eye on ingredient stock and restock when necessary.</li>
                <li>🎉 <strong>Special Events:</strong> Participate in Happy Hour and other events to boost sales.</li>
            </ul>
        </div>
    </div>

    <!-- Difficulty Selection Modal -->
    <div id="difficultyModal" class="modal">
        <div class="modal-content">
            <h2>Select Difficulty Level</h2>
            <button class="difficulty-button" onclick="selectDifficulty('Easy')">Easy</button>
            <button class="difficulty-button" onclick="selectDifficulty('Medium')">Medium</button>
            <button class="difficulty-button" onclick="selectDifficulty('Hard')">Hard</button>
        </div>
    </div>

    <!-- JavaScript Code -->
    <script>
        // Game Variables
        let tips = 0;
        let drinksMade = 0;
        let money = 0;
        let bartenderRank = "Barback Trainee";
        let incomePerSecond = 0;
        let selectedIngredients = [];
        let tipRange = [1, 10];
        let tipIncrementThreshold = 10;
        let ingredientsShown = false;
        let gameStarted = false;
        let difficulty = '';

        // New Game Variables
        let customerSatisfaction = 100; // Percentage
        let barPopularity = 50; // Scale from 0 to 100
        let ingredientStock = {};
        let barReputation = "Unknown";
        let employeeLevel = 1;
        let dailyExpenses = 0;
        let profit = 0;
        let happyHour = false;
        let timeOfDay = "Evening";
        let totalCustomersServed = 0;
        let vipCustomersServed = 0;
        let specialEvents = [];
        let customerFeedback = [];
        let upgradesPurchased = [];
        let dailySales = 0;
        let weeklyPerformance = [];
        let ingredientRestockThreshold = 5;
        let drinkPrices = {};
        let isWeekend = false;
        let barLevel = 1;
        let maxOrdersAtOnce = 3;
        let currentCustomers = [];
        let lostCustomers = 0;
        let consecutiveCorrectOrders = 0;
        let bonusTips = 0;
        let achievementsUnlocked = [];
        let orderInterval;

        // New Variables for Highlighting Feature
        let highlightingEnabled = true;
        let ordersServed = 0;
        const highlightingThreshold = 5; // Number of orders after which highlighting is disabled

        // Drink Recipes
        const drinkRecipes = {
            "Margarita": ["Tequila", "Triple Sec", "Lime Juice", "Salt Rim", "Margarita Glass"],
            "Old Fashioned": ["Bourbon or Rye Whiskey", "Angostura Bitters", "Sugar Cube", "Orange Peel", "Cherry", "Rocks Glass"],
            "Mojito": ["White Rum", "Lime Juice", "Mint Leaves", "Sugar", "Soda Water", "Collins Glass"],
            "Bloody Mary": ["Vodka", "Tomato Juice", "Lemon Juice", "Worcestershire Sauce", "Tabasco", "Celery Salt", "Black Pepper", "Celery Stick", "Highball Glass"],
            "Martini": ["Gin or Vodka", "Dry Vermouth", "Olive or Lemon Twist", "Martini Glass"],
            "Piña Colada": ["White Rum", "Pineapple Juice", "Coconut Cream", "Pineapple Wedge", "Hurricane Glass"],
            "Cosmopolitan": ["Vodka", "Triple Sec", "Cranberry Juice", "Lime Juice", "Martini Glass"],
            "Whiskey Sour": ["Whiskey", "Lemon Juice", "Simple Syrup", "Egg White (optional)", "Cherry", "Old Fashioned Glass"],
            "Long Island Iced Tea": ["Vodka", "Tequila", "White Rum", "Gin", "Triple Sec", "Lemon Juice", "Simple Syrup", "Cola", "Lemon Wedge", "Highball Glass"],
            "Gin and Tonic": ["Gin", "Tonic Water", "Lime Wedge", "Highball Glass"],
            "Daiquiri": ["White Rum", "Lime Juice", "Simple Syrup", "Cocktail Glass"],
            "Mai Tai": ["White Rum", "Dark Rum", "Orange Curaçao", "Lime Juice", "Orgeat Syrup", "Mint Sprig", "Old Fashioned Glass"],
            "Negroni": ["Gin", "Campari", "Sweet Vermouth", "Orange Peel", "Old Fashioned Glass"],
            "Moscow Mule": ["Vodka", "Lime Juice", "Ginger Beer", "Lime Wedge", "Copper Mug"],
            "Screwdriver": ["Vodka", "Orange Juice", "Orange Slice", "Highball Glass"],
            "Irish Coffee": ["Irish Whiskey", "Hot Coffee", "Brown Sugar", "Whipped Cream", "Irish Coffee Glass"],
            "Aperol Spritz": ["Aperol", "Prosecco", "Soda Water", "Orange Slice", "Wine Glass"],
            "Tequila Sunrise": ["Tequila", "Orange Juice", "Grenadine", "Orange Slice", "Cherry", "Highball Glass"],
            "Rum Punch": ["Dark Rum", "Light Rum", "Pineapple Juice", "Orange Juice", "Grenadine", "Nutmeg", "Hurricane Glass"],
            "Bellini": ["Prosecco", "Peach Purée", "Champagne Flute"],
            "Black Russian": ["Vodka", "Coffee Liqueur", "Old Fashioned Glass"],
            "Caipirinha": ["Cachaça", "Lime Wedges", "Sugar", "Old Fashioned Glass"],
            "Sidecar": ["Cognac", "Triple Sec", "Lemon Juice", "Sugar Rim", "Cocktail Glass"],
            "French 75": ["Gin", "Lemon Juice", "Simple Syrup", "Champagne", "Lemon Twist", "Champagne Flute"],
            "Sazerac": ["Rye Whiskey or Cognac", "Absinthe", "Sugar Cube", "Peychaud's Bitters", "Lemon Peel", "Old Fashioned Glass"],
            "Tom Collins": ["Gin", "Lemon Juice", "Simple Syrup", "Soda Water", "Lemon Slice", "Cherry", "Collins Glass"],
            "Amaretto Sour": ["Amaretto Liqueur", "Lemon Juice", "Simple Syrup", "Egg White (optional)", "Cherry", "Old Fashioned Glass"],
            "Mint Julep": ["Bourbon Whiskey", "Mint Leaves", "Sugar", "Crushed Ice", "Mint Sprig", "Julep Cup"],
            "Paloma": ["Tequila", "Grapefruit Juice", "Lime Juice", "Simple Syrup", "Soda Water", "Salt Rim", "Highball Glass"],
            "White Russian": ["Vodka", "Coffee Liqueur", "Heavy Cream", "Old Fashioned Glass"],
            "Singapore Sling": ["Gin", "Cherry Heering", "Benedictine", "Cointreau", "Pineapple Juice", "Lime Juice", "Grenadine", "Angostura Bitters", "Pineapple Slice", "Cherry", "Highball Glass"],
            "Sex on the Beach": ["Vodka", "Peach Schnapps", "Orange Juice", "Cranberry Juice", "Orange Slice", "Cherry", "Highball Glass"],
            "Gin Fizz": ["Gin", "Lemon Juice", "Simple Syrup", "Soda Water", "Lemon Slice", "Collins Glass"],
            "Boulevardier": ["Bourbon or Rye Whiskey", "Campari", "Sweet Vermouth", "Orange Peel", "Old Fashioned Glass"],
            "Planter's Punch": ["Dark Rum", "Orange Juice", "Pineapple Juice", "Lemon Juice", "Grenadine", "Angostura Bitters", "Nutmeg", "Hurricane Glass"],
            "Hurricane": ["Dark Rum", "White Rum", "Passion Fruit Juice", "Orange Juice", "Lime Juice", "Grenadine", "Simple Syrup", "Orange Slice", "Cherry", "Hurricane Glass"],
            "Dark 'n' Stormy": ["Dark Rum", "Ginger Beer", "Lime Wedge", "Highball Glass"],
            "Apple Martini": ["Vodka", "Apple Schnapps", "Cointreau", "Lemon Juice", "Apple Slice", "Martini Glass"],
            "Kamikaze": ["Vodka", "Triple Sec", "Lime Juice", "Lime Wedge", "Cocktail Glass"],
            "Sea Breeze": ["Vodka", "Cranberry Juice", "Grapefruit Juice", "Lime Wedge", "Highball Glass"],
            "B52": ["Coffee Liqueur", "Baileys Irish Cream", "Grand Marnier", "Shot Glass"],
            "Lemon Drop": ["Vodka", "Triple Sec", "Lemon Juice", "Simple Syrup", "Sugar Rim", "Cocktail Glass"],
            "Grasshopper": ["Crème de Menthe", "Crème de Cacao", "Cream", "Mint Leaf", "Cocktail Glass"],
            "Espresso Martini": ["Vodka", "Coffee Liqueur", "Espresso", "Simple Syrup", "Coffee Beans", "Martini Glass"]
        };

        // Difficulty Parameters
        const difficultySettings = {
            'Easy': {
                timePerOrder: 60,
                maxOrders: 2,
                availableDrinks: ['Gin and Tonic', 'Screwdriver', 'Margarita', 'Daiquiri', 'Whiskey Sour', 'Mojito'],
                ingredientRestockThreshold: 3
            },
            'Medium': {
                timePerOrder: 45,
                maxOrders: 3,
                availableDrinks: Object.keys(drinkRecipes),
                ingredientRestockThreshold: 5
            },
            'Hard': {
                timePerOrder: 30,
                maxOrders: 4,
                availableDrinks: Object.keys(drinkRecipes),
                ingredientRestockThreshold: 7
            }
        };

        // Popular Ingredients (for highlighting)
        const popularIngredients = ["Vodka", "Gin", "Rum", "Tequila", "Whiskey", "Triple Sec", "Lime Juice", "Lemon Juice", "Sugar", "Simple Syrup", "Orange Juice", "Cranberry Juice"];

        // Initialize Ingredient Stock and Drink Prices
        function initIngredientStockAndPrices() {
            const uniqueIngredients = new Set();
            const availableDrinks = difficultySettings[difficulty].availableDrinks;
            availableDrinks.forEach(drink => {
                const ingredients = drinkRecipes[drink];
                ingredients.forEach(ingredient => uniqueIngredients.add(ingredient));
                drinkPrices[drink] = calculateBaseDrinkPrice(ingredients);
            });
            uniqueIngredients.forEach(ingredient => {
                ingredientStock[ingredient] = 20; // Starting stock for each ingredient
            });
        }

        // Calculate Base Drink Price Based on Ingredients
        function calculateBaseDrinkPrice(ingredients) {
            return 5 + ingredients.length * 1.5; // Base price plus $1.5 per ingredient
        }

        // Update Game Statistics
        function updateStats() {
            document.getElementById("tips").innerText = tips.toFixed(2);
            document.getElementById("drinksMade").innerText = drinksMade;
            document.getElementById("money").innerText = money.toFixed(2);
            document.getElementById("bartenderRank").innerText = bartenderRank;
            document.getElementById("customerSatisfaction").innerText = customerSatisfaction + "%";
            document.getElementById("barPopularity").innerText = barPopularity + "%";
            document.getElementById("barReputation").innerText = barReputation;
            document.getElementById("dailySales").innerText = dailySales.toFixed(2);
            document.getElementById("timeOfDay").innerText = timeOfDay;
            document.getElementById("incomePerSecond").innerText = incomePerSecond;
        }

        // Generate Customer Order
        function generateOrder() {
            if (currentCustomers.length >= difficultySettings[difficulty].maxOrders) return;

            const drinks = difficultySettings[difficulty].availableDrinks;
            const newOrder = drinks[Math.floor(Math.random() * drinks.length)];
            currentCustomers.push({
                order: newOrder,
                timeRemaining: difficultySettings[difficulty].timePerOrder, // Time per order based on difficulty
                timerInterval: null,
                selectedIngredients: []
            });
            displayOrders();
            startCustomerTimer(currentCustomers.length - 1);
            updateIngredientButtons();
        }

        // Display Current Orders
        function displayOrders() {
            const ordersDiv = document.getElementById("orders");
            ordersDiv.innerHTML = "";
            currentCustomers.forEach((customer, index) => {
                const orderDiv = document.createElement("div");
                orderDiv.classList.add("ticket");
                orderDiv.innerHTML = `
                    <p><strong>Order ${index + 1}:</strong> ${customer.order}</p>
                    <p>Time Remaining: <span id="customerTime${index}">${customer.timeRemaining}</span> seconds</p>
                    <p>Required Ingredients: ${drinkRecipes[customer.order].join(", ")}</p>
                    <p>Selected Ingredients: <span id="customerIngredients${index}">${customer.selectedIngredients.join(", ")}</span></p>
                    <button onclick="submitDrink(${index})">Serve Drink</button>
                `;
                ordersDiv.appendChild(orderDiv);
            });
        }

        // Start Customer Timer
        function startCustomerTimer(customerIndex) {
            const customer = currentCustomers[customerIndex];
            customer.timerInterval = setInterval(() => {
                customer.timeRemaining--;
                document.getElementById(`customerTime${customerIndex}`).innerText = customer.timeRemaining;
                if (customer.timeRemaining <= 0) {
                    clearInterval(customer.timerInterval);
                    lostCustomers++;
                    customerSatisfaction -= 5;
                    checkCustomerSatisfaction();
                    alert(`Time's up for Order ${customerIndex + 1}! You lost a customer.`);
                    removeCustomer(customerIndex);
                }
            }, 1000);
        }

        // Remove Customer from Current Orders
        function removeCustomer(index) {
            clearInterval(currentCustomers[index].timerInterval);
            currentCustomers.splice(index, 1);
            displayOrders();
            updateIngredientButtons();
            generateOrder();
        }

        // Ingredient Selection for Specific Customer
        function selectIngredient(ingredient) {
            const customerIndex = prompt("Enter the order number to add this ingredient to:");
            const index = parseInt(customerIndex) - 1;
            if (index >= 0 && index < currentCustomers.length) {
                const customer = currentCustomers[index];
                if (ingredientStock[ingredient] <= 0) {
                    alert(`You are out of ${ingredient}!`);
                    return;
                }
                customer.selectedIngredients.push(ingredient);
                ingredientStock[ingredient]--;
                document.getElementById(`customerIngredients${index}`).innerText = customer.selectedIngredients.join(", ");
                checkIngredientStock();
            } else {
                alert("Invalid order number.");
            }
        }

        // Submit Drink for Specific Customer
        function submitDrink(customerIndex) {
            const customer = currentCustomers[customerIndex];
            clearInterval(customer.timerInterval);
            const correctIngredients = drinkRecipes[customer.order];
            const isCorrect = arraysEqual(
                customer.selectedIngredients.slice().sort(),
                correctIngredients.slice().sort()
            );

            if (isCorrect) {
                let basePrice = drinkPrices[customer.order];
                if (happyHour) basePrice *= 0.8; // 20% discount during happy hour
                tips += getRandomTip();
                bonusTips += calculateBonusTips();
                drinksMade++;
                money += basePrice;
                dailySales += basePrice;
                totalCustomersServed++;
                consecutiveCorrectOrders++;
                ordersServed++; // Increment orders served
                if (consecutiveCorrectOrders % 5 === 0) {
                    customerSatisfaction += 5;
                    barPopularity += 2;
                }
                customerFeedback.push("Satisfied");
                alert(`Great job! The customer is satisfied and paid $${basePrice.toFixed(2)}.`);
            } else {
                customerSatisfaction -= 10;
                consecutiveCorrectOrders = 0;
                customerFeedback.push("Unsatisfied");
                alert("Oh no! The customer didn't like the drink.");
            }

            // Disable highlighting after threshold is reached
            if (ordersServed >= highlightingThreshold) {
                highlightingEnabled = false;
            }

            checkCustomerSatisfaction();
            updateBartenderRank();
            updateStats();
            removeCustomer(customerIndex);
            updateIngredientButtons();
        }

        // Check Customer Satisfaction Levels
        function checkCustomerSatisfaction() {
            if (customerSatisfaction <= 0) {
                customerSatisfaction = 0;
                alert("Your customer satisfaction is at 0%! Game over.");
                resetGame();
            } else if (customerSatisfaction >= 100) {
                customerSatisfaction = 100;
            }
        }

        // Check Ingredient Stock and Restock if Necessary
        function checkIngredientStock() {
            for (const ingredient in ingredientStock) {
                if (ingredientStock[ingredient] <= difficultySettings[difficulty].ingredientRestockThreshold) {
                    restockIngredient(ingredient);
                }
            }
        }

        // Restock Ingredient
        function restockIngredient(ingredient) {
            const restockCost = 10; // Fixed cost for simplicity
            if (money >= restockCost) {
                money -= restockCost;
                ingredientStock[ingredient] += 20;
                alert(`Restocked ${ingredient} for $${restockCost}.`);
                updateStats();
            } else {
                alert(`Not enough money to restock ${ingredient}.`);
            }
        }

        // Calculate Bonus Tips
        function calculateBonusTips() {
            if (consecutiveCorrectOrders >= 5) {
                return 5; // Bonus tip of $5 for every 5 consecutive correct orders
            }
            return 0;
        }

        // Reset Game
        function resetGame() {
            tips = 0;
            drinksMade = 0;
            money = 0;
            customerSatisfaction = 100;
            barPopularity = 50;
            totalCustomersServed = 0;
            lostCustomers = 0;
            consecutiveCorrectOrders = 0;
            currentCustomers = [];
            clearInterval(orderInterval);
            gameStarted = false;
            highlightingEnabled = true; // Reset highlighting
            ordersServed = 0; // Reset orders served
            document.getElementById("startGameBtn").disabled = false;
            document.getElementById("ingredientsList").style.display = "none";
            ingredientsShown = false;
            updateStats();
            // Show the difficulty selection modal again
            document.getElementById("difficultyModal").style.display = "block";
        }

        // Update Bartender Rank
        function updateBartenderRank() {
            if (drinksMade >= 100) {
                bartenderRank = "Master Mixologist";
            } else if (drinksMade >= 70) {
                bartenderRank = "Expert Bartender";
            } else if (drinksMade >= 50) {
                bartenderRank = "Experienced Bartender";
            } else if (drinksMade >= 30) {
                bartenderRank = "Junior Bartender";
            } else if (drinksMade >= 10) {
                bartenderRank = "Bartender Trainee";
            } else {
                bartenderRank = "Barback Trainee";
            }
            document.getElementById("bartenderRank").innerText = bartenderRank;
        }

        // Show/Hide Ingredients List
        function toggleIngredients() {
            const ingredientsList = document.getElementById("ingredientsList");
            if (ingredientsShown) {
                ingredientsList.style.display = "none";
                ingredientsShown = false;
            } else {
                ingredientsList.style.display = "block";
                ingredientsShown = true;
            }
        }

        // Initialize Ingredients List
        function initIngredientsList() {
            const uniqueIngredients = new Set();
            const availableDrinks = difficultySettings[difficulty].availableDrinks;
            availableDrinks.forEach(drink => {
                drinkRecipes[drink].forEach(ingredient => uniqueIngredients.add(ingredient));
            });

            // Categorize ingredients into sections
            const categories = {
                Alcohols: [],
                'Mixers & Juices': [],
                'Garnishes & Others': [],
                Glassware: []
            };

            uniqueIngredients.forEach(ingredient => {
                // Categorize based on keywords
                if (ingredient.includes('Glass') || ingredient.includes('Mug') || ingredient.includes('Cup')) {
                    categories.Glassware.push(ingredient);
                } else if (['Vodka', 'Gin', 'Rum', 'Tequila', 'Whiskey', 'Bourbon', 'Cachaça', 'Scotch', 'Cognac', 'Brandy', 'Liqueur', 'Absinthe', 'Campari', 'Vermouth', 'Aperol', 'Prosecco', 'Champagne', 'Wine', 'Sherry', 'Port', 'Benedictine', 'Schnapps'].some(alcohol => ingredient.includes(alcohol))) {
                    categories.Alcohols.push(ingredient);
                } else if (['Juice', 'Soda', 'Water', 'Cola', 'Coffee', 'Tea', 'Milk', 'Cream', 'Syrup', 'Grenadine', 'Worcestershire Sauce', 'Tabasco', 'Bitters', 'Espresso'].some(mixer => ingredient.includes(mixer))) {
                    categories['Mixers & Juices'].push(ingredient);
                } else {
                    categories['Garnishes & Others'].push(ingredient);
                }
            });

            // Create collapsible sections and buttons
            const ingredientsList = document.getElementById("ingredientsList");
            ingredientsList.innerHTML = ""; // Clear previous list
            for (const [category, items] of Object.entries(categories)) {
                const collButton = document.createElement("button");
                collButton.className = "collapsible";
                collButton.innerText = category;
                ingredientsList.appendChild(collButton);

                const contentDiv = document.createElement("div");
                contentDiv.className = "content";

                // Popular ingredients first
                const popularItems = items.filter(item => popularIngredients.includes(item));
                const otherItems = items.filter(item => !popularIngredients.includes(item));

                popularItems.sort().forEach(ingredient => {
                    const btn = document.createElement("button");
                    btn.innerText = ingredient;
                    btn.classList.add("ingredient-button", "popular");
                    btn.onclick = () => selectIngredient(ingredient);
                    contentDiv.appendChild(btn);
                });

                otherItems.sort().forEach(ingredient => {
                    const btn = document.createElement("button");
                    btn.innerText = ingredient;
                    btn.classList.add("ingredient-button");
                    btn.onclick = () => selectIngredient(ingredient);
                    contentDiv.appendChild(btn);
                });

                ingredientsList.appendChild(contentDiv);
            }

            // Add event listeners to the new collapsible sections
            const collapsibles = document.getElementsByClassName("collapsible");
            for (let coll of collapsibles) {
                coll.addEventListener("click", function() {
                    this.classList.toggle("active");
                    const content = this.nextElementSibling;
                    if (content.style.display === "block") {
                        content.style.display = "none";
                    } else {
                        content.style.display = "block";
                    }
                });
            }
        }

        // Update Ingredient Buttons Based on Current Orders
        function updateIngredientButtons() {
            const requiredIngredients = new Set();
            currentCustomers.forEach(customer => {
                drinkRecipes[customer.order].forEach(ingredient => requiredIngredients.add(ingredient));
            });

            const buttons = document.querySelectorAll(".ingredient-button");
            buttons.forEach(button => {
                const ingredient = button.innerText;
                if (highlightingEnabled && requiredIngredients.has(ingredient)) {
                    button.classList.add("required");
                } else {
                    button.classList.remove("required");
                }
            });
        }

        // Filter Ingredients Based on Search Input
        function filterIngredients() {
            const searchInput = document.getElementById("ingredientSearch").value.toLowerCase();
            const buttons = document.querySelectorAll(".ingredient-button");
            buttons.forEach(button => {
                const ingredient = button.innerText.toLowerCase();
                if (ingredient.includes(searchInput)) {
                    button.style.display = "inline-block";
                } else {
                    button.style.display = "none";
                }
            });
        }

        // Get Random Tip
        function getRandomTip() {
            return Math.floor(Math.random() * (5 - 1 + 1)) + 1; // Random tip between $1 and $5
        }

        // Arrays Equal Function
        function arraysEqual(arr1, arr2) {
            if (arr1.length !== arr2.length) return false;
            arr1.sort();
            arr2.sort();
            for (let i = 0; i < arr1.length; i++) {
                if (arr1[i] !== arr2[i]) return false;
            }
            return true;
        }

        // Buy Upgrades
        function buyUpgrade(upgrade) {
            let cost = 0;
            let benefit = 0;
            switch (upgrade) {
                case 'betterShaker':
                    cost = 200;
                    benefit = 1;
                    break;
                case 'fancyGlassware':
                    cost = 500;
                    benefit = 2;
                    break;
                case 'bartenderAssistant':
                    cost = 1000;
                    benefit = 5;
                    break;
            }
            if (money >= cost) {
                money -= cost;
                incomePerSecond += benefit;
                alert(`Upgrade purchased: ${upgrade.replace(/([A-Z])/g, ' $1').trim()}! Income per second increased.`);
                document.getElementById("incomePerSecond").innerText = incomePerSecond;
                updateStats();
            } else {
                alert("Not enough money for this upgrade.");
            }
        }

        // Passive Income Generation
        setInterval(() => {
            money += incomePerSecond;
            document.getElementById("money").innerText = money.toFixed(2);
        }, 1000);

        // Start Game Function
        function startGame() {
            if (!gameStarted) {
                gameStarted = true;
                document.getElementById("startGameBtn").disabled = true;
                // Show Difficulty Modal
                document.getElementById("difficultyModal").style.display = "block";
            }
        }

        // Select Difficulty Level
        function selectDifficulty(selectedDifficulty) {
            difficulty = selectedDifficulty;
            document.getElementById("difficultyModal").style.display = "none";
            initIngredientStockAndPrices();
            initIngredientsList();
            updateStats();
            maxOrdersAtOnce = difficultySettings[difficulty].maxOrders;
            ingredientRestockThreshold = difficultySettings[difficulty].ingredientRestockThreshold;
            generateOrder();
            orderInterval = setInterval(generateOrder, 15000); // New customer every 15 seconds
            setInterval(updateTimeOfDay, 60000); // Update time of day every minute
            setInterval(checkSpecialEvents, 30000); // Check for special events every 30 seconds
        }

        // Update Time of Day
        function updateTimeOfDay() {
            const timesOfDay = ["Morning", "Afternoon", "Evening", "Night"];
            timeOfDay = timesOfDay[(timesOfDay.indexOf(timeOfDay) + 1) % timesOfDay.length];
            document.getElementById("timeOfDay").innerText = timeOfDay;
            if (timeOfDay === "Evening" || timeOfDay === "Night") {
                isWeekend = !isWeekend; // Toggle weekend status
            }
        }

        // Check for Special Events
        function checkSpecialEvents() {
            // Example: Happy Hour during Evening
            if (timeOfDay === "Evening" && !happyHour) {
                happyHour = true;
                alert("Happy Hour started! Drinks are 20% off.");
            } else if (timeOfDay !== "Evening" && happyHour) {
                happyHour = false;
                alert("Happy Hour ended.");
            }
        }

        // Initialize Event Listeners
        window.onload = function() {
            document.getElementById("startGameBtn").addEventListener("click", startGame);
            document.getElementById("toggleIngredientsBtn").addEventListener("click", toggleIngredients);
        };
    </script>
</body>
</html>
