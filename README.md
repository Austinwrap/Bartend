<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Celebrity Bartender - Mix & Earn!</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        /* Importing Google Fonts */
        @import url('https://fonts.googleapis.com/css2?family=Pacifico&family=Nunito:wght@400;700&display=swap');

        /* Resetting default margins and paddings */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Nunito', sans-serif;
            background: linear-gradient(135deg, #f6d365 0%, #fda085 100%);
            color: #333;
            overflow-x: hidden;
        }

        h1 {
            font-family: 'Pacifico', cursive;
            color: #fff;
            text-align: center;
            margin: 20px 0;
            font-size: 2.5em;
            text-shadow: 0 0 10px rgba(255,255,255,0.8);
            position: relative;
            -webkit-text-stroke: 1px #333;
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
            max-width: 600px;
            margin: 0 auto;
            padding: 0 10px;
        }

        .status-bar {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            background-color: rgba(255, 255, 255, 0.85);
            padding: 10px;
            border-radius: 10px;
            margin-bottom: 15px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .status-item {
            flex: 1 1 45%;
            margin: 5px 0;
            text-align: center;
        }

        .status-item p {
            font-size: 1em;
        }

        .money-display {
            font-size: 1.5em;
            color: #ff6b6b;
            font-weight: bold;
            text-shadow: 1px 1px #fff;
        }

        .buttons-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            margin-bottom: 15px;
        }

        button {
            background: linear-gradient(to bottom right, #ff9a9e, #fad0c4);
            color: #fff;
            border: none;
            border-radius: 30px;
            padding: 10px 15px;
            margin: 5px;
            font-size: 0.9em;
            cursor: pointer;
            transition: all 0.2s ease;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
            position: relative;
        }

        button:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 15px rgba(0,0,0,0.3);
        }

        .order-display {
            background-color: rgba(255, 255, 255, 0.9);
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 15px;
            position: relative;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .order-display h2 {
            margin-bottom: 10px;
            font-size: 1.3em;
            color: #ff6b6b;
        }

        .ticket {
            background-color: #fff;
            padding: 10px;
            margin-bottom: 10px;
            border-left: 5px solid #ff6b6b;
            border-radius: 5px;
            position: relative;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
            width: 100%;
            overflow: hidden;
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
            margin-bottom: 15px;
        }

        .ingredient-button {
            background-color: #f0f0f0;
            color: #333;
            border: 1px solid #ccc;
            border-radius: 20px;
            padding: 7px 10px;
            margin: 3px;
            font-size: 0.8em;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .ingredient-button:hover {
            background-color: #e0e0e0;
            transform: translateY(-2px);
            box-shadow: 0 3px 7px rgba(0,0,0,0.1);
        }

        .ingredient-button.popular {
            background-color: #ffd1dc;
        }

        .ingredient-button.required {
            border-color: #ff6b6b;
        }

        .ingredient-button.selected {
            background-color: #ff6b6b;
            color: #fff;
            border-color: #ff6b6b;
        }

        .rules {
            background-color: rgba(255, 255, 255, 0.9);
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 15px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            display: none; /* Hidden by default */
            position: absolute;
            top: 10px;
            right: 10px;
            max-width: 250px;
            z-index: 1000;
        }

        .rules h2 {
            margin-bottom: 10px;
            font-size: 1.3em;
            color: #ff6b6b;
        }

        .rules ul {
            list-style-type: disc;
            margin-left: 20px;
        }

        .toggle-ingredients-btn {
            background-color: #ffcc00;
            color: #fff;
            border: none;
            border-radius: 20px;
            padding: 7px 10px;
            font-size: 0.8em;
            cursor: pointer;
            transition: all 0.2s ease;
            margin: 3px 0;
        }

        .toggle-ingredients-btn:hover {
            background-color: #ffd633;
            transform: translateY(-2px);
            box-shadow: 0 3px 7px rgba(0,0,0,0.1);
        }

        /* Notification Styles */
        #notification {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: rgba(255, 204, 0, 0.9);
            color: #333;
            padding: 20px 30px;
            border-radius: 30px;
            font-size: 1.2em;
            display: none;
            opacity: 0;
            transition: opacity 0.5s, top 0.5s;
            z-index: 1000;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            text-align: center;
        }

        /* Enhanced Tip Notification Styles */
        #tipNotification {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: radial-gradient(circle at center, #fffa65, #f39c12);
            color: #fff;
            padding: 30px 40px;
            border-radius: 50px;
            font-size: 2em;
            display: none;
            opacity: 0;
            transition: opacity 0.3s, transform 0.3s;
            z-index: 1001;
            box-shadow: 0 8px 20px rgba(0,0,0,0.3);
            text-align: center;
            animation: tipFlash 0.6s ease-in-out;
        }

        @keyframes tipFlash {
            0% { transform: translate(-50%, -50%) scale(0.5); opacity: 0; }
            50% { transform: translate(-50%, -50%) scale(1.4); opacity: 1; }
            100% { transform: translate(-50%, -50%) scale(1); opacity: 0; }
        }

        /* Animation for Level Up */
        @keyframes levelUpAnimation {
            0% { transform: scale(0.5); opacity: 0; }
            50% { transform: scale(1.2); opacity: 1; }
            100% { transform: scale(1); opacity: 0; }
        }

        /* Celebration Animation */
        @keyframes celebration {
            0% { opacity: 0; transform: scale(0.5); }
            50% { opacity: 1; transform: scale(1.2); }
            100% { opacity: 0; transform: scale(1); }
        }

        /* Modal Styles */
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgba(0,0,0,0.7);
        }

        .modal-content {
            background-color: #fff;
            margin: 20% auto;
            padding: 15px;
            border: 1px solid #ccc;
            width: 90%;
            max-width: 350px;
            text-align: center;
            border-radius: 10px;
            position: relative;
            color: #333;
        }

        .modal-content h2 {
            margin-bottom: 15px;
            color: #ff6b6b;
        }

        .modal-content input {
            width: 80%;
            padding: 8px;
            margin-bottom: 15px;
            font-size: 1em;
            border: 1px solid #ccc;
            border-radius: 5px;
            background-color: #f9f9f9;
            color: #333;
        }

        .modal-content button {
            width: 80%;
            padding: 10px;
            font-size: 1em;
            margin: 5px 0;
            background-color: #ff9a9e;
            color: #fff;
            border: none;
            border-radius: 30px;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .modal-content button:hover {
            background-color: #ffb0b5;
            transform: translateY(-2px);
            box-shadow: 0 3px 7px rgba(0,0,0,0.1);
        }

        .difficulty-button {
            width: 80%;
            padding: 10px;
            font-size: 1em;
            margin: 5px 0;
            background-color: #ffcc00;
            color: #fff;
            border: none;
            border-radius: 30px;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .difficulty-button:hover {
            background-color: #ffd633;
            transform: translateY(-2px);
            box-shadow: 0 3px 7px rgba(0,0,0,0.1);
        }

        /* Restock Modal */
        #restockModal .modal-content {
            max-width: 500px;
        }

        #restockModal table {
            width: 100%;
            border-collapse: collapse;
        }

        #restockModal th, #restockModal td {
            border: 1px solid #ccc;
            padding: 8px;
            text-align: center;
        }

        #restockModal th {
            background-color: #f2f2f2;
        }

        /* Game Over Modal */
        #gameOverModal .modal-content {
            max-width: 400px;
        }

        /* Celebration Modal */
        #celebrationModal .modal-content {
            max-width: 500px;
            background: linear-gradient(135deg, #ff9a9e, #fad0c4);
            color: #fff;
        }

        /* Fireworks Animation */
        .fireworks {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 999;
            background: url('https://i.imgur.com/3NZQqXG.gif') center center / cover no-repeat;
            opacity: 0;
            animation: fireworksAnimation 3s forwards;
        }

        @keyframes fireworksAnimation {
            0% { opacity: 0; }
            10% { opacity: 1; }
            90% { opacity: 1; }
            100% { opacity: 0; }
        }

        /* Directions Button */
        #directionsBtn {
            position: fixed;
            top: 10px;
            right: 10px;
            background-color: #ffcc00;
            color: #fff;
            border: none;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            font-size: 1.5em;
            cursor: pointer;
            box-shadow: 0 3px 7px rgba(0,0,0,0.2);
            z-index: 100;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        /* Next Level Modal */
        #nextLevelModal .modal-content {
            max-width: 400px;
        }

        /* Responsive Design */
        @media (max-width: 600px) {
            .status-item {
                flex: 1 1 100%;
            }

            h1 {
                font-size: 1.8em;
            }

            .buttons-container button {
                flex: 1 1 45%;
                max-width: 100%;
            }

            .order-display {
                flex-direction: column;
                align-items: flex-start;
            }

            .modal-content {
                margin: 30% auto;
            }
        }
    </style>
</head>
<body>
    <h1>Celebrity Bartender</h1>
    <button id="directionsBtn">?</button>
    <div class="game-container">
        <!-- Status Bar -->
        <div class="status-bar">
            <div class="status-item">
                <p>Username: <span id="username">Player123</span></p>
            </div>
            <div class="status-item">
                <p>Level: <span id="playerLevel">1</span> - <span id="bartenderTitle">Novice Mixer</span></p>
            </div>
            <div class="status-item">
                <p>Income/sec: $<span id="incomePerSecond">0</span></p>
            </div>
            <div class="status-item">
                <p>Tips: $<span id="tips">0.00</span></p>
            </div>
            <div class="status-item">
                <p>Drinks Made: <span id="drinksMade">0</span></p>
            </div>
            <div class="status-item">
                <p class="money-display">Money: $<span id="money">0.00</span></p>
            </div>
            <div class="status-item">
                <p>Total Profit: $<span id="totalProfit">0.00</span></p>
            </div>
            <div class="status-item">
                <p>Round: <span id="currentRound">1</span></p>
            </div>
            <div class="status-item">
                <p>Level Timer: <span id="roundTimer">0s</span></p>
            </div>
        </div>

        <!-- Buttons -->
        <div class="buttons-container">
            <button id="startGameBtn">Start Game</button>
            <button onclick="buyUpgrade('betterShaker')">Better Shaker ($200)</button>
            <button onclick="buyUpgrade('fancyGlassware')">Fancy Glassware ($500)</button>
            <button onclick="buyUpgrade('bartenderAssistant')">Hire Assistant ($1000)</button>
            <button onclick="openRestockModal()">Restock Ingredients</button>
        </div>

        <!-- Current Order Display -->
        <div class="order-display" id="currentOrderDisplay">
            <h2>Current Orders:</h2>
            <div id="orders"></div>
        </div>

        <!-- Game Rules -->
        <div class="rules" id="rules">
            <h2>Game Rules & Directions</h2>
            <p>Welcome to <strong>Celebrity Bartender</strong>! Here's how to play:</p>
            <ul>
                <li><strong>Start Game:</strong> Click "Start Game" to begin your shift.</li>
                <li><strong>Levels:</strong> Complete levels of 10 drinks as quickly as possible to earn bonuses.</li>
                <li><strong>Take Orders:</strong> Orders will come in automatically; manage up to the maximum orders allowed.</li>
                <li><strong>Make Drinks:</strong> Select ingredients for each order by clicking on the ingredients under each order.</li>
                <li><strong>Show/Hide Ingredients:</strong> Use the "Show/Hide Ingredients" button to view or hide the required ingredients for each drink.</li>
                <li><strong>Celebrities:</strong> Occasionally, a celebrity will order a special drink. Serve them correctly for big rewards!</li>
                <li><strong>Earn Money:</strong> Correctly made drinks earn you money based on drink prices and tips.</li>
                <li><strong>Buy Upgrades:</strong> Use money to purchase upgrades and increase your income.</li>
                <li><strong>Restock Ingredients:</strong> Use the "Restock Ingredients" button to purchase more ingredients.</li>
                <li><strong>Level Up:</strong> Make drinks to advance levels and earn new bartender titles.</li>
                <li><strong>Win the Game:</strong> Reach $10 trillion to become the Ultimate Fame Bartender and win the game!</li>
            </ul>
        </div>
    </div>

    <!-- Notification Elements -->
    <div id="notification"></div>
    <div id="tipNotification"></div>

    <!-- Fireworks -->
    <div id="fireworks" class="fireworks"></div>

    <!-- Username Modal -->
    <div id="usernameModal" class="modal">
        <div class="modal-content">
            <h2>Welcome to Celebrity Bartender!</h2>
            <p>Please enter your username or leave it blank for a random one.</p>
            <input type="text" id="usernameInput" placeholder="Enter your username">
            <button onclick="setUsername()">Continue</button>
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

    <!-- Restock Ingredients Modal -->
    <div id="restockModal" class="modal">
        <div class="modal-content">
            <h2>Restock Ingredients</h2>
            <table>
                <thead>
                    <tr>
                        <th>Ingredient</th>
                        <th>Stock</th>
                        <th>Restock Amount</th>
                        <th>Cost</th>
                        <th>Action</th>
                    </tr>
                </thead>
                <tbody id="restockTableBody">
                    <!-- Rows will be populated dynamically -->
                </tbody>
            </table>
            <button onclick="restockAll()">Restock All</button>
            <button onclick="closeRestockModal()">Close</button>
        </div>
    </div>

    <!-- Next Level Modal -->
    <div id="nextLevelModal" class="modal">
        <div class="modal-content">
            <h2>Level <span id="nextLevelNumber">1</span> Completed!</h2>
            <p>You completed the level in <span id="levelTime">0</span> seconds.</p>
            <p>Prepare for the next level!</p>
            <p>Level Recap:</p>
            <ul>
                <li>Drinks Served: <span id="levelDrinksServed">0</span></li>
                <li>Tips Earned: $<span id="levelTipsEarned">0.00</span></li>
                <li>Total Sales: $<span id="levelTotalSales">0.00</span></li>
            </ul>
            <button onclick="continueToNextLevel()">Continue to Next Level (<span id="countdown">15</span>)</button>
        </div>
    </div>

    <!-- Game Over Modal -->
    <div id="gameOverModal" class="modal">
        <div class="modal-content">
            <h2>Game Over!</h2>
            <p>Thanks for playing!</p>
            <p>Final Score: <span id="finalScore">0</span></p>
            <p>Total Tips: $<span id="finalTips">0.00</span></p>
            <p>Total Sales: $<span id="finalSales">0.00</span></p>
            <p>Tip Percentage: <span id="tipPercentage">0%</span></p>
            <button onclick="restartGame()">Play Again</button>
        </div>
    </div>

    <!-- Celebration Modal -->
    <div id="celebrationModal" class="modal">
        <div class="modal-content">
            <h2>Congratulations, <span id="celebrationUsername">Player</span>!</h2>
            <p>You have become the <strong>Ultimate Fame Bartender</strong>!</p>
            <p>You reached $<span id="finalMoney">10 Trillion</span>!</p>
            <p>Your journey has been legendary. Thank you for playing!</p>
            <button onclick="restartGame()">Play Again</button>
        </div>
    </div>

    <!-- JavaScript Code -->
    <script>
        // Game Variables
        let username = '';
        let tips = 0;
        let drinksMade = 0;
        let money = 0; // Starting money adjusted to $0
        let totalProfit = 0;
        let bartenderRank = "Barback Trainee";
        let incomePerSecond = 0;
        let selectedIngredients = [];
        let gameStarted = false;
        let difficulty = '';
        let playerLevel = 1;
        let bartenderTitle = "Novice Mixer";
        let currentRound = 1;
        let roundStartTime = 0;
        let roundTimerInterval;
        let levelCountdownInterval;
        let levelCountdown = 15;
        let levelDrinksServed = 0;
        let levelTipsEarned = 0;
        let levelTotalSales = 0;

        // New Game Variables
        let customerSatisfaction = 100; // Percentage
        let barPopularity = 50; // Scale from 0 to 100
        let ingredientStock = {};
        let dailySales = 0;
        let ingredientRestockThreshold = 5;
        let drinkPrices = {};
        let timeOfDay = "Evening";
        let isWeekend = false;
        let maxOrdersAtOnce = 3;
        let currentCustomers = [];
        let lostCustomers = 0;
        let consecutiveCorrectOrders = 0;
        let bonusTips = 0;
        let orderInterval;
        let happyHour = false;
        let celebrityChance = 0.1; // 10% chance for a celebrity to appear
        let celebrities = [
            "Brad Pitt", "Beyoncé", "Leonardo DiCaprio", "Taylor Swift", "Dwayne Johnson",
            "Jennifer Lawrence", "Chris Hemsworth", "Scarlett Johansson", "Tom Hanks", "Emma Stone",
            "Will Smith", "Angelina Jolie", "Johnny Depp", "Meryl Streep", "Robert Downey Jr.",
            "Rihanna", "Ed Sheeran", "Ariana Grande", "Justin Bieber", "Lady Gaga",
            "Kanye West", "Kim Kardashian", "Drake", "Kendrick Lamar", "Katy Perry",
            "Bruno Mars", "Selena Gomez", "Cardi B", "Billie Eilish", "Post Malone"
        ];
        let servedCelebrities = new Set();
        let celebrityOrders = {};
        let celebrityTip = 50;

        // New Variables for Highlighting Feature
        let highlightingEnabled = true;
        let ordersServed = 0;
        const highlightingThreshold = 5; // Number of orders after which highlighting is disabled

        // Drink Recipes
        const drinkRecipes = {
            // Level 1 Drinks
            "Water": ["Water", "Glass"],
            "Soda": ["Soda", "Ice", "Glass"],
            "Beer": ["Beer", "Glass"],
            "Juice": ["Fruit Juice", "Glass"],
            "Milk": ["Milk", "Glass"],
            "Lemonade": ["Lemon Juice", "Sugar", "Water", "Ice", "Glass"],
            // Level 2 Drinks
            "Iced Tea": ["Tea", "Lemon Juice", "Sugar", "Ice", "Glass"],
            "Coffee": ["Coffee", "Water", "Glass"],
            "Hot Chocolate": ["Cocoa Powder", "Milk", "Sugar", "Glass"],
            // Level 3 Drinks
            "Gin and Tonic": ["Gin", "Tonic Water", "Lime Wedge", "Highball Glass"],
            "Screwdriver": ["Vodka", "Orange Juice", "Orange Slice", "Highball Glass"],
            // Level 4 Drinks
            "Margarita": ["Tequila", "Triple Sec", "Lime Juice", "Salt Rim", "Margarita Glass"],
            "Daiquiri": ["White Rum", "Lime Juice", "Simple Syrup", "Cocktail Glass"],
            // Level 5 Drinks
            "Whiskey Sour": ["Whiskey", "Lemon Juice", "Simple Syrup", "Egg White (optional)", "Cherry", "Old Fashioned Glass"],
            "Mojito": ["White Rum", "Lime Juice", "Mint Leaves", "Sugar", "Soda Water", "Collins Glass"],
            // Level 6 Drinks
            "Cosmopolitan": ["Vodka", "Triple Sec", "Cranberry Juice", "Lime Juice", "Martini Glass"],
            "Piña Colada": ["White Rum", "Pineapple Juice", "Coconut Cream", "Pineapple Wedge", "Hurricane Glass"],
            // Level 7 Drinks
            "Martini": ["Gin or Vodka", "Dry Vermouth", "Olive or Lemon Twist", "Martini Glass"],
            "Old Fashioned": ["Bourbon or Rye Whiskey", "Angostura Bitters", "Sugar Cube", "Orange Peel", "Cherry", "Rocks Glass"],
            // Level 8 Drinks
            "Long Island Iced Tea": ["Vodka", "Tequila", "White Rum", "Gin", "Triple Sec", "Lemon Juice", "Simple Syrup", "Cola", "Lemon Wedge", "Highball Glass"],
            "Negroni": ["Gin", "Campari", "Sweet Vermouth", "Orange Peel", "Old Fashioned Glass"],
            // Level 9 Drinks
            "Bloody Mary": ["Vodka", "Tomato Juice", "Lemon Juice", "Worcestershire Sauce", "Tabasco", "Celery Salt", "Black Pepper", "Celery Stick", "Highball Glass"],
            "Moscow Mule": ["Vodka", "Lime Juice", "Ginger Beer", "Lime Wedge", "Copper Mug"],
            // Level 10 Drinks
            "Singapore Sling": ["Gin", "Cherry Heering", "Benedictine", "Cointreau", "Pineapple Juice", "Lime Juice", "Grenadine", "Angostura Bitters", "Pineapple Slice", "Cherry", "Highball Glass"],
            "Hurricane": ["Dark Rum", "White Rum", "Passion Fruit Juice", "Orange Juice", "Lime Juice", "Grenadine", "Simple Syrup", "Orange Slice", "Cherry", "Hurricane Glass"],
        };

        // Level Mapping
        const levelDrinks = {
            1: ["Water", "Soda", "Beer", "Juice", "Milk", "Lemonade"],
            2: ["Iced Tea", "Coffee", "Hot Chocolate"],
            3: ["Gin and Tonic", "Screwdriver"],
            4: ["Margarita", "Daiquiri"],
            5: ["Whiskey Sour", "Mojito"],
            6: ["Cosmopolitan", "Piña Colada"],
            7: ["Martini", "Old Fashioned"],
            8: ["Long Island Iced Tea", "Negroni"],
            9: ["Bloody Mary", "Moscow Mule"],
            10: ["Singapore Sling", "Hurricane"],
        };

        // Difficulty Parameters
        const difficultySettings = {
            'Easy': {
                timePerOrder: 60, // Not used now
                maxOrders: 2,
                ingredientRestockThreshold: 3
            },
            'Medium': {
                timePerOrder: 60,
                maxOrders: 3,
                ingredientRestockThreshold: 5
            },
            'Hard': {
                timePerOrder: 60,
                maxOrders: 4,
                ingredientRestockThreshold: 7
            }
        };

        // Bartender Titles
        const bartenderTitles = {
            1: "Novice Mixer",
            2: "Apprentice Bartender",
            3: "Junior Bartender",
            4: "Bartender",
            5: "Senior Bartender",
            6: "Mixologist",
            7: "Expert Mixologist",
            8: "Head Bartender",
            9: "Master Mixologist",
            10: "World-Class Bartender"
        };

        // Initialize Ingredient Stock and Drink Prices
        function initIngredientStockAndPrices() {
            const uniqueIngredients = new Set();
            const potentialDrinks = getPotentialDrinks();
            potentialDrinks.forEach(drink => {
                const ingredients = drinkRecipes[drink];
                ingredients.forEach(ingredient => uniqueIngredients.add(ingredient));
                drinkPrices[drink] = calculateBaseDrinkPrice(ingredients);
            });
            uniqueIngredients.forEach(ingredient => {
                if (!isEssentialIngredient(ingredient)) {
                    if (!ingredientStock[ingredient]) {
                        ingredientStock[ingredient] = 20; // Starting stock for consumable ingredients
                    }
                }
            });
        }

        // Get Potential Drinks Based on Player Level and Possible Orders
        function getPotentialDrinks() {
            let drinks = [];
            for (let i = 1; i <= playerLevel; i++) {
                drinks = drinks.concat(levelDrinks[i]);
            }
            // Include Level 2 drinks if playerLevel is 1, since generateOrder() can include Level 2 drinks
            if (playerLevel === 1) {
                drinks = drinks.concat(levelDrinks[2]);
            }
            return drinks;
        }

        // Get Available Drinks Based on Player Level
        function getAvailableDrinks() {
            let drinks = [];
            for (let i = 1; i <= playerLevel; i++) {
                drinks = drinks.concat(levelDrinks[i]);
            }
            return drinks;
        }

        // Calculate Base Drink Price Based on Ingredients
        function calculateBaseDrinkPrice(ingredients) {
            return 5 + ingredients.length * 1.5; // Base price plus $1.5 per ingredient
        }

        // Update Game Statistics
        function updateStats() {
            document.getElementById("tips").innerText = tips.toFixed(2);
            document.getElementById("drinksMade").innerText = drinksMade;
            document.getElementById("money").innerText = formatNumber(money);
            document.getElementById("totalProfit").innerText = formatNumber(totalProfit);
            document.getElementById("bartenderTitle").innerText = bartenderTitle;
            document.getElementById("incomePerSecond").innerText = incomePerSecond;
            document.getElementById("playerLevel").innerText = playerLevel;
            document.getElementById("username").innerText = username;
            document.getElementById("currentRound").innerText = currentRound;

            // Check for game completion
            if (money >= 1e13) { // 10 trillion
                gameOver(true);
            }
        }

        // Format large numbers with suffixes
        function formatNumber(num) {
            if (num >= 1e12) return (num / 1e12).toFixed(2) + 'T';
            if (num >= 1e9) return (num / 1e9).toFixed(2) + 'B';
            if (num >= 1e6) return (num / 1e6).toFixed(2) + 'M';
            return num.toFixed(2);
        }

        // Set Username
        function setUsername() {
            const input = document.getElementById("usernameInput").value.trim();
            username = input || generateRandomUsername();
            document.getElementById("username").innerText = username;
            document.getElementById("usernameModal").style.display = "none";
            // Show Difficulty Modal
            document.getElementById("difficultyModal").style.display = "block";
        }

        // Generate Random Username
        function generateRandomUsername() {
            const adjectives = ["Speedy", "Happy", "Mighty", "Brave", "Cool", "Clever"];
            const nouns = ["Mixer", "Shaker", "Pourer", "Stirrer", "Sipper", "Bartender"];
            return adjectives[Math.floor(Math.random() * adjectives.length)] + " " + nouns[Math.floor(Math.random() * nouns.length)] + Math.floor(Math.random() * 100);
        }

        // Generate Customer Order
        function generateOrder() {
            if (currentCustomers.length >= maxOrdersAtOnce) return;

            let isCelebrity = Math.random() < celebrityChance;
            const availableDrinks = getAvailableDrinks();
            let potentialDrinks = [...availableDrinks];

            // Include Level 2 drinks in Level 1 with lower probability
            if (playerLevel === 1) {
                potentialDrinks = potentialDrinks.concat(levelDrinks[2]);
            }

            let newOrder;

            // Ensure more easy drinks in early levels with occasional harder ones
            if (playerLevel === 1) {
                if (Math.random() < 0.8) {
                    newOrder = levelDrinks[1][Math.floor(Math.random() * levelDrinks[1].length)];
                } else {
                    newOrder = levelDrinks[2][Math.floor(Math.random() * levelDrinks[2].length)];
                }
            } else {
                newOrder = potentialDrinks[Math.floor(Math.random() * potentialDrinks.length)];
            }

            let customerName = "Customer";
            if (isCelebrity && servedCelebrities.size < celebrities.length) {
                let availableCelebrities = celebrities.filter(c => !servedCelebrities.has(c));
                customerName = availableCelebrities[Math.floor(Math.random() * availableCelebrities.length)];
                celebrityOrders[newOrder] = true;
                servedCelebrities.add(customerName);
            } else if (isCelebrity) {
                customerName = celebrities[Math.floor(Math.random() * celebrities.length)] + " (Round Two)";
            }

            currentCustomers.push({
                order: newOrder,
                selectedIngredients: [],
                showIngredients: false,
                customerName: customerName,
                isCelebrity: isCelebrity,
            });
            displayOrders();
        }

        // Display Current Orders
        function displayOrders() {
            const ordersDiv = document.getElementById("orders");
            ordersDiv.innerHTML = "";
            currentCustomers.forEach((customer, index) => {
                const orderDiv = document.createElement("div");
                orderDiv.classList.add("ticket");
                if (customer.isCelebrity) {
                    orderDiv.style.borderLeftColor = "#ffd700";
                }
                orderDiv.innerHTML = `
                    <p><strong>${customer.isCelebrity ? 'Celebrity Order' : 'Order'} ${index + 1}:</strong> ${customer.isCelebrity ? customer.customerName + ' wants a ' : ''}${customer.order}</p>
                    <p>Selected: <span id="customerIngredients${index}">${customer.selectedIngredients.join(", ")}</span></p>
                    <button class="toggle-ingredients-btn" onclick="toggleIngredients(${index})">Show/Hide Ingredients</button>
                    <div class="required-ingredients" id="requiredIngredients${index}" style="display: none;">
                        <p><strong>Required:</strong> ${drinkRecipes[customer.order].join(", ")}</p>
                    </div>
                    <div class="ingredients-list" id="ingredientsList${index}"></div>
                    <button onclick="submitDrink(${index})">Serve Drink</button>
                `;
                ordersDiv.appendChild(orderDiv);

                // Generate ingredients buttons for this order
                generateIngredientsListForOrder(index);
            });
        }

        // Toggle Ingredients Visibility
        function toggleIngredients(orderIndex) {
            const customer = currentCustomers[orderIndex];
            customer.showIngredients = !customer.showIngredients;
            const requiredDiv = document.getElementById(`requiredIngredients${orderIndex}`);
            requiredDiv.style.display = customer.showIngredients ? 'block' : 'none';
        }

        function generateIngredientsListForOrder(orderIndex) {
            const customer = currentCustomers[orderIndex];
            const ingredientsDiv = document.getElementById(`ingredientsList${orderIndex}`);
            ingredientsDiv.innerHTML = '';

            // Get the unique ingredients available for the game
            const uniqueIngredients = new Set();
            const potentialDrinks = getPotentialDrinks();
            potentialDrinks.forEach(drink => {
                drinkRecipes[drink].forEach(ingredient => uniqueIngredients.add(ingredient));
            });

            // Create buttons for each ingredient
            uniqueIngredients.forEach(ingredient => {
                const btn = document.createElement("button");
                btn.innerText = ingredient;
                btn.classList.add("ingredient-button");
                btn.onclick = () => selectIngredientForOrder(ingredient, orderIndex);

                // Highlight required ingredients in initial levels
                if (highlightingEnabled && ordersServed < highlightingThreshold) {
                    if (drinkRecipes[customer.order].includes(ingredient)) {
                        btn.classList.add("required");
                    }
                }

                // Indicate if the ingredient is out of stock
                if (!isEssentialIngredient(ingredient) && ingredientStock[ingredient] <= 0) {
                    btn.disabled = true;
                    btn.classList.add("out-of-stock");
                }

                // Indicate if the ingredient is already selected
                if (customer.selectedIngredients.includes(ingredient)) {
                    btn.classList.add("selected");
                }

                ingredientsDiv.appendChild(btn);
            });
        }

        // Select Ingredient for a Specific Order
        function selectIngredientForOrder(ingredient, orderIndex) {
            const customer = currentCustomers[orderIndex];

            if (customer.selectedIngredients.includes(ingredient)) {
                showNotification(`You have already added ${ingredient} to this drink.`);
                return;
            }

            if (!isEssentialIngredient(ingredient)) {
                if (ingredientStock[ingredient] <= 0) {
                    showNotification(`You are out of ${ingredient}!`);
                    return;
                }
                ingredientStock[ingredient]--;
            }

            customer.selectedIngredients.push(ingredient);
            document.getElementById(`customerIngredients${orderIndex}`).innerText = customer.selectedIngredients.join(", ");
            checkIngredientStock();
            // Update the ingredient buttons to reflect stock changes
            generateIngredientsListForOrder(orderIndex);
        }

        // Remove Customer from Current Orders
        function removeCustomer(index) {
            currentCustomers.splice(index, 1);
            displayOrders();
            // No need to check for game over here
        }

        // Submit Drink for Specific Customer
        function submitDrink(customerIndex) {
            const customer = currentCustomers[customerIndex];
            const correctIngredients = drinkRecipes[customer.order];
            const isCorrect = arraysEqual(
                customer.selectedIngredients.slice().sort(),
                correctIngredients.slice().sort()
            );

            if (isCorrect) {
                let basePrice = drinkPrices[customer.order];
                if (happyHour) basePrice *= 0.8; // 20% discount during happy hour
                if (customer.isCelebrity) {
                    celebrityTip = getRandomTip(true); // Higher tip for celebrities
                    tips += celebrityTip;
                    money += celebrityTip; // Add tip to money
                    totalProfit += basePrice + celebrityTip;
                    showTipNotification(`+ $${formatNumber(celebrityTip)} Tip from ${customer.customerName}!`);
                } else {
                    const tipAmount = getRandomTip();
                    tips += tipAmount;
                    money += tipAmount; // Add tip to money
                    totalProfit += basePrice + tipAmount;
                    showTipNotification(`+ $${formatNumber(tipAmount)} Tip!`);
                }
                bonusTips += calculateBonusTips();
                drinksMade++;
                levelDrinksServed++;
                money += basePrice;
                totalProfit += basePrice;
                dailySales += basePrice;
                levelTipsEarned += tips;
                levelTotalSales += basePrice;
                consecutiveCorrectOrders++;
                ordersServed++; // Increment orders served

                // Level Up Check
                if (drinksMade % 10 === 0 && playerLevel < 10) {
                    playerLevel++;
                    bartenderTitle = bartenderTitles[playerLevel];
                    showLevelUpNotification(`Level ${playerLevel}: ${bartenderTitle}!`);
                }

                // Level Completion Check
                if (drinksMade % 10 === 0) {
                    completeLevel();
                    return; // Do not generate new order after level completion
                }
            } else {
                customerSatisfaction -= 10;
                consecutiveCorrectOrders = 0;
                showNotification("Oh no! The customer didn't like the drink.");
            }

            // Disable highlighting after threshold is reached
            if (ordersServed >= highlightingThreshold) {
                highlightingEnabled = false;
            }

            checkCustomerSatisfaction();
            updateStats();
            removeCustomer(customerIndex);
            // Generate a new order if possible
            generateOrder();
        }

        // Complete Level
        function completeLevel() {
            clearInterval(roundTimerInterval);
            const roundTime = (Date.now() - roundStartTime) / 1000; // in seconds
            document.getElementById("nextLevelNumber").innerText = currentRound;
            document.getElementById("levelTime").innerText = roundTime.toFixed(2);
            document.getElementById("levelDrinksServed").innerText = levelDrinksServed;
            document.getElementById("levelTipsEarned").innerText = formatNumber(levelTipsEarned);
            document.getElementById("levelTotalSales").innerText = formatNumber(levelTotalSales);

            document.getElementById("nextLevelModal").style.display = "block";
            levelCountdown = 15;
            document.getElementById("countdown").innerText = levelCountdown;
            levelCountdownInterval = setInterval(() => {
                levelCountdown--;
                document.getElementById("countdown").innerText = levelCountdown;
                if (levelCountdown <= 0) {
                    clearInterval(levelCountdownInterval);
                    continueToNextLevel();
                }
            }, 1000);

            // Reset level-specific variables
            levelDrinksServed = 0;
            levelTipsEarned = 0;
            levelTotalSales = 0;
        }

        // Continue to Next Level
        function continueToNextLevel() {
            document.getElementById("nextLevelModal").style.display = "none";
            clearInterval(levelCountdownInterval);
            currentRound++;
            document.getElementById("currentRound").innerText = currentRound;
            startRoundTimer();
            generateOrder();
        }

        // Start Round Timer
        function startRoundTimer() {
            roundStartTime = Date.now();
            if (roundTimerInterval) clearInterval(roundTimerInterval);
            roundTimerInterval = setInterval(() => {
                const elapsedTime = (Date.now() - roundStartTime) / 1000; // in seconds
                document.getElementById("roundTimer").innerText = `${elapsedTime.toFixed(1)}s`;
            }, 100);
        }

        // Check Customer Satisfaction Levels
        function checkCustomerSatisfaction() {
            if (customerSatisfaction <= 0) {
                customerSatisfaction = 0;
                showNotification("Customer satisfaction is at 0%! Game over.");
                gameOver();
            } else if (customerSatisfaction >= 100) {
                customerSatisfaction = 100;
            }
        }

        // Check if Game Over
        function checkGameOver() {
            // Game over conditions can be added here if needed
        }

        // Game Over Function
        function gameOver(gameCompleted = false) {
            clearInterval(orderInterval);
            clearInterval(roundTimerInterval);
            if (gameCompleted) {
                document.getElementById("celebrationUsername").innerText = username;
                document.getElementById("finalMoney").innerText = formatNumber(money);
                document.getElementById("celebrationModal").style.display = "block";
                document.getElementById("fireworks").style.display = "block";
                setTimeout(() => {
                    document.getElementById("fireworks").style.display = "none";
                }, 3000);
            } else {
                document.getElementById("finalScore").innerText = drinksMade;
                document.getElementById("finalTips").innerText = formatNumber(tips);
                document.getElementById("finalSales").innerText = formatNumber(dailySales);
                const tipPercentage = ((tips / totalProfit) * 100).toFixed(2);
                document.getElementById("tipPercentage").innerText = tipPercentage + "%";
                document.getElementById("gameOverModal").style.display = "block";
            }
        }

        // Restart Game
        function restartGame() {
            document.getElementById("gameOverModal").style.display = "none";
            document.getElementById("celebrationModal").style.display = "none";
            resetGame();
        }

        // Check Ingredient Stock and Restock if Necessary
        function checkIngredientStock() {
            for (const ingredient in ingredientStock) {
                if (ingredientStock[ingredient] <= 0) {
                    showNotification(`You have run out of ${ingredient}! Please restock.`);
                    openRestockModal();
                    break;
                }
            }
        }

        // Open Restock Modal
        function openRestockModal() {
            const restockTableBody = document.getElementById("restockTableBody");
            restockTableBody.innerHTML = '';
            for (const ingredient in ingredientStock) {
                const row = document.createElement("tr");
                const restockCost = calculateRestockCost(ingredient);
                row.innerHTML = `
                    <td>${ingredient}</td>
                    <td>${ingredientStock[ingredient]}</td>
                    <td>+20</td>
                    <td>$${restockCost}</td>
                    <td><button onclick="restockIngredient('${ingredient}')">Restock</button></td>
                `;
                restockTableBody.appendChild(row);
            }
            document.getElementById("restockModal").style.display = "block";
        }

        // Close Restock Modal
        function closeRestockModal() {
            document.getElementById("restockModal").style.display = "none";
        }

        // Restock Ingredient
        function restockIngredient(ingredient) {
            const restockCost = calculateRestockCost(ingredient);
            if (money >= restockCost) {
                money -= restockCost;
                ingredientStock[ingredient] += 20;
                showNotification(`Restocked ${ingredient} for $${restockCost}.`);
                updateStats();
                openRestockModal(); // Refresh the modal
                displayOrders(); // Update ingredient buttons
            } else {
                showNotification(`Not enough money to restock ${ingredient}.`);
            }
        }

        // Restock All Ingredients
        function restockAll() {
            let totalCost = 0;
            for (const ingredient in ingredientStock) {
                totalCost += calculateRestockCost(ingredient);
            }
            if (money >= totalCost) {
                for (const ingredient in ingredientStock) {
                    ingredientStock[ingredient] += 20;
                }
                money -= totalCost;
                showNotification(`Restocked all ingredients for $${totalCost}.`);
                updateStats();
                closeRestockModal();
                displayOrders();
            } else {
                showNotification(`Not enough money to restock all ingredients.`);
            }
        }

        // Calculate Restock Cost Based on Ingredient and Level
        function calculateRestockCost(ingredient) {
            const baseCost = 10;
            const levelMultiplier = playerLevel * 0.5;
            return Math.ceil(baseCost * levelMultiplier);
        }

        // Check if an Ingredient is Essential
        function isEssentialIngredient(ingredient) {
            const essentialIngredients = ["Glass", "Highball Glass", "Margarita Glass", "Old Fashioned Glass", "Collins Glass", "Martini Glass", "Rocks Glass", "Hurricane Glass", "Copper Mug", "Cocktail Glass"];
            return essentialIngredients.includes(ingredient);
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
            money = 0; // Reset starting money to $0
            totalProfit = 0;
            customerSatisfaction = 100;
            barPopularity = 50;
            totalCustomersServed = 0;
            lostCustomers = 0;
            consecutiveCorrectOrders = 0;
            currentCustomers = [];
            clearInterval(orderInterval);
            clearInterval(roundTimerInterval);
            gameStarted = false;
            highlightingEnabled = true; // Reset highlighting
            ordersServed = 0; // Reset orders served
            playerLevel = 1;
            bartenderTitle = bartenderTitles[playerLevel];
            currentRound = 1;
            servedCelebrities.clear();
            updateStats();
            // Show Username Modal
            document.getElementById("usernameModal").style.display = "block";
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

        // Get Random Tip
        function getRandomTip(isCelebrity = false) {
            let minTip = 1 + playerLevel; // Tips increase with level
            let maxTip = 5 + playerLevel * 2;
            if (isCelebrity) {
                minTip *= 2;
                maxTip *= 2;
            }
            return Math.floor(Math.random() * (maxTip - minTip + 1)) + minTip;
        }

        // Buy Upgrades
        function buyUpgrade(upgrade) {
            let cost = 0;
            let benefit = 0;
            switch (upgrade) {
                case 'betterShaker':
                    cost = 200;
                    benefit = 5;
                    break;
                case 'fancyGlassware':
                    cost = 500;
                    benefit = 10;
                    break;
                case 'bartenderAssistant':
                    cost = 1000;
                    benefit = 20;
                    break;
            }
            if (money >= cost) {
                money -= cost;
                incomePerSecond += benefit;
                showNotification(`Upgrade purchased: ${upgrade.replace(/([A-Z])/g, ' $1').trim()}! Income per second increased.`);
                document.getElementById("incomePerSecond").innerText = incomePerSecond;
                updateStats();
            } else {
                showNotification("Not enough money for this upgrade.");
            }
        }

        // Passive Income Generation
        setInterval(() => {
            money += incomePerSecond;
            totalProfit += incomePerSecond;
            document.getElementById("money").innerText = formatNumber(money);
            document.getElementById("totalProfit").innerText = formatNumber(totalProfit);
            updateStats();
        }, 1000);

        // Start Game Function
        function startGame() {
            if (!gameStarted) {
                gameStarted = true;
                document.getElementById("startGameBtn").disabled = true;
                // Show Username Modal
                document.getElementById("usernameModal").style.display = "block";
            }
        }

        // Select Difficulty Level
        function selectDifficulty(selectedDifficulty) {
            difficulty = selectedDifficulty;
            document.getElementById("difficultyModal").style.display = "none";
            initIngredientStockAndPrices();
            updateStats();
            maxOrdersAtOnce = difficultySettings[difficulty].maxOrders;
            ingredientRestockThreshold = difficultySettings[difficulty].ingredientRestockThreshold;
            generateOrder();
            orderInterval = setInterval(() => {
                generateOrder();
                // Randomize order interval for variable flow
            }, Math.floor(Math.random() * (10000 - 5000 + 1)) + 5000); // New customer every 5-10 seconds
            startRoundTimer(); // Start the round timer
        }

        // Show Notification
        function showNotification(message) {
            const notification = document.getElementById("notification");
            notification.innerText = message;
            notification.style.backgroundColor = "rgba(255, 204, 0, 0.9)";
            notification.style.display = "block";
            notification.style.opacity = "1";
            notification.style.top = "50%";

            setTimeout(() => {
                notification.style.opacity = "0";
                notification.style.top = "40%";
                setTimeout(() => {
                    notification.style.display = "none";
                }, 500);
            }, 2000);
        }

        // Show Tip Notification
        function showTipNotification(message) {
            const notification = document.getElementById("tipNotification");
            notification.innerText = message;
            notification.style.display = "block";
            notification.style.opacity = "1";
            notification.style.transform = "translate(-50%, -50%) scale(1.4)";

            setTimeout(() => {
                notification.style.opacity = "0";
                notification.style.transform = "translate(-50%, -50%) scale(1)";
                setTimeout(() => {
                    notification.style.display = "none";
                }, 300);
            }, 600);
        }

        // Show Level Up Notification
        function showLevelUpNotification(message) {
            const notification = document.getElementById("notification");
            notification.innerText = `Level Up! ${message}`;
            notification.style.backgroundColor = "rgba(255, 85, 85, 0.9)";
            notification.style.display = "block";
            notification.style.opacity = "1";
            notification.style.top = "50%";
            notification.style.animation = "levelUpAnimation 2s forwards";

            setTimeout(() => {
                notification.style.opacity = "0";
                notification.style.top = "40%";
                setTimeout(() => {
                    notification.style.display = "none";
                    notification.style.animation = ""; // Reset animation
                }, 500);
            }, 2500);
        }

        // Toggle Rules Display
        function toggleRules() {
            const rulesDiv = document.getElementById("rules");
            rulesDiv.style.display = rulesDiv.style.display === 'block' ? 'none' : 'block';
        }

        // Initialize Event Listeners
        window.onload = function() {
            document.getElementById("startGameBtn").addEventListener("click", startGame);
            document.getElementById("directionsBtn").addEventListener("click", toggleRules);
        };
    </script>
</body>
</html>
