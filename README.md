<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Celebrity Bartender - Mix & Earn!</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Pacifico&family=Nunito:wght@400;700&display=swap');

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
            -webkit-user-select: none; /* Prevent text selection on tap */
            user-select: none;
        }

        body {
            font-family: 'Nunito', sans-serif;
            background: linear-gradient(135deg, #f6d365 0%, #fda085 100%);
            color: #333;
            overflow-x: hidden;
            touch-action: manipulation;
            -webkit-overflow-scrolling: touch; /* Smooth scrolling on iOS */
        }

        h1 {
            font-family: 'Pacifico', cursive;
            color: #fff;
            text-align: center;
            margin: 15px 0;
            font-size: 1.8em;
            text-shadow: 0 0 8px rgba(255,255,255,0.8);
            -webkit-text-stroke: 0.5px #333;
        }

        h1::before, h1::after {
            content: '✦';
            position: absolute;
            font-size: 1em;
            color: #fff;
            animation: twinkle 2s infinite;
        }

        h1::before { top: -6px; left: -15px; }
        h1::after { top: -6px; right: -15px; }

        @keyframes twinkle {
            0%, 100% { opacity: 0.2; transform: scale(1); }
            50% { opacity: 1; transform: scale(1.2); }
        }

        #welcome-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 2000;
        }

        #enter-btn {
            background: linear-gradient(to bottom right, #ff9a9e, #fad0c4);
            color: #fff;
            border: none;
            border-radius: 20px;
            padding: 10px 20px;
            font-size: 1.1em;
            cursor: pointer;
            box-shadow: 0 3px 8px rgba(0,0,0,0.2);
            transition: all 0.3s ease;
        }

        #enter-btn:hover, #enter-btn:active {
            transform: scale(1.05);
            box-shadow: 0 5px 12px rgba(0,0,0,0.3);
        }

        .popup {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: linear-gradient(135deg, #ffeb3b, #ff4081);
            padding: 12px;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.3), 0 0 15px #ff4081;
            z-index: 1000;
            text-align: center;
            opacity: 0;
            transition: opacity 0.5s ease;
            color: #fff;
            width: 85%;
            max-width: 300px;
            font-size: 0.85em;
        }

        .popup.show {
            opacity: 1;
        }

        .popup h2 {
            color: #fff;
            margin-bottom: 8px;
            text-shadow: 0 0 4px #ffeb3b;
            font-size: 1.1em;
        }

        .popup ul {
            list-style: none;
            text-align: left;
        }

        .popup li {
            padding: 3px 0;
            font-size: 0.85em;
            text-shadow: 0 0 2px #000;
        }

        .popup .close-btn {
            position: absolute;
            top: 6px;
            right: 6px;
            background: #ff4081;
            color: #fff;
            border: none;
            border-radius: 50%;
            width: 16px;
            height: 16px;
            cursor: pointer;
            box-shadow: 0 0 4px #ffeb3b;
            font-size: 0.7em;
            line-height: 16px;
        }

        #notification {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: linear-gradient(to right, #00e676, #00c853);
            color: #fff;
            padding: 12px 20px;
            border-radius: 20px;
            font-size: 0.9em;
            display: none;
            opacity: 0;
            transition: opacity 0.5s;
            z-index: 1001;
            box-shadow: 0 0 8px #00e676;
            max-width: 85%;
        }

        #tip-notification {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: linear-gradient(to right, #ffeb3b, #ff9100);
            color: #fff;
            padding: 15px 25px;
            border-radius: 25px;
            font-size: 1em;
            display: none;
            opacity: 0;
            transition: opacity 0.5s;
            z-index: 1002;
            animation: tipFlash 1s ease-in-out;
            box-shadow: 0 0 12px #ffeb3b;
            max-width: 85%;
        }

        @keyframes tipFlash {
            0% { transform: translate(-50%, -50%) scale(0.5); opacity: 0; }
            50% { transform: translate(-50%, -50%) scale(1.1); opacity: 1; }
            100% { transform: translate(-50%, -50%) scale(1); opacity: 1; }
        }

        .game-container {
            max-width: 100%;
            width: 100%;
            margin: 0 auto;
            padding: 5px;
            display: none;
        }

        .status-bar {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            background: rgba(255, 255, 255, 0.85);
            padding: 6px;
            border-radius: 8px;
            margin-bottom: 8px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
            font-size: 0.8em;
        }

        .status-item {
            flex: 1 1 45%;
            margin: 2px 0;
            text-align: center;
        }

        .money-display {
            font-size: 1em;
            color: #ff6b6b;
            font-weight: bold;
        }

        .buttons-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            margin-bottom: 8px;
        }

        button {
            background: linear-gradient(to bottom right, #ff9a9e, #fad0c4);
            color: #fff;
            border: none;
            border-radius: 20px;
            padding: 6px 12px;
            margin: 3px;
            cursor: pointer;
            transition: all 0.2s ease;
            box-shadow: 0 2px 6px rgba(0,0,0,0.2);
            font-size: 0.8em;
            touch-action: manipulation;
        }

        button:hover, button:active {
            transform: translateY(-1px);
            box-shadow: 0 4px 10px rgba(0,0,0,0.3);
        }

        .order-display {
            background: rgba(255, 255, 255, 0.9);
            padding: 8px;
            border-radius: 8px;
            margin-bottom: 8px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
        }

        .ticket {
            background: #fff;
            padding: 6px;
            margin-bottom: 6px;
            border-left: 3px solid #ff6b6b;
            border-radius: 4px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
            font-size: 0.75em;
        }

        .ticket.celebrity {
            border-left-color: #ffd700;
        }

        .ingredient-button {
            background: #f0f0f0;
            color: #333;
            border: 1px solid #ccc;
            border-radius: 18px;
            padding: 5px 10px;
            margin: 2px;
            cursor: pointer;
            transition: all 0.2s ease;
            font-size: 0.7em;
            touch-action: manipulation;
            min-width: 60px; /* Ensure tappable size */
            height: 30px; /* Consistent height */
            line-height: 20px;
            display: inline-block;
            text-align: center;
        }

        .ingredient-button:hover, .ingredient-button:active {
            background: #e0e0e0;
            transform: translateY(-1px);
        }

        .ingredient-button.selected {
            background: #ff6b6b;
            color: #fff;
            border-color: #ff6b6b;
        }

        .ingredient-button.required {
            border: 2px solid #ff6b6b;
        }

        .ingredient-button:disabled {
            background: #ccc;
            cursor: not-allowed;
        }

        .toggle-ingredients-btn {
            background: #ffcc00;
            color: #fff;
            border: none;
            border-radius: 18px;
            padding: 5px 10px;
            margin: 2px;
            cursor: pointer;
            font-size: 0.7em;
            min-width: 80px;
            height: 30px;
            line-height: 20px;
        }

        .toggle-ingredients-btn:hover, .toggle-ingredients-btn:active {
            background: #ffd633;
            transform: translateY(-1px);
        }

        #recap-screen {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: linear-gradient(135deg, #fff, #ffd1dc);
            padding: 15px;
            border-radius: 12px;
            box-shadow: 0 8px 15px rgba(0,0,0,0.3);
            z-index: 1000;
            width: 85%;
            max-width: 300px;
            text-align: center;
            display: none;
            font-size: 0.85em;
        }

        #recap-screen ul {
            list-style: none;
            margin: 10px 0;
            text-align: left;
        }

        #recap-screen li {
            padding: 3px 0;
            font-size: 0.85em;
        }

        @media (max-width: 600px) {
            h1 { font-size: 1.4em; }
            .status-item { flex: 1 1 100%; font-size: 0.75em; }
            .game-container { padding: 3px; }
            button { padding: 5px 10px; font-size: 0.7em; }
            .ingredient-button { padding: 4px 8px; font-size: 0.65em; min-width: 50px; height: 28px; line-height: 20px; }
            .ticket { font-size: 0.7em; }
            .toggle-ingredients-btn { min-width: 70px; }
        }
    </style>
</head>
<body>
    <div id="welcome-screen">
        <h1>Celebrity Bartender</h1>
        <button id="enter-btn">Enter</button>
    </div>

    <div id="instructions" class="popup">
        <button class="close-btn" onclick="hidePopup('instructions')">X</button>
        <h2>Welcome!</h2>
        <ul>
            <li>5 Levels, 10 Drinks Each</li>
            <li>Serve Orders Fast</li>
            <li>Time Resets Per Level</li>
            <li>First 3 Drinks Highlighted</li>
            <li>Show Ingredients? Less Tips</li>
            <li>Celebrity Orders = Big Tips</li>
            <li>Restock Ingredients</li>
            <li>Buy Upgrades</li>
            <li>Final Recap After Level 5</li>
        </ul>
    </div>

    <div id="level-transition" class="popup">
        <button class="close-btn" onclick="hidePopup('level-transition'); startLevel();">X</button>
        <h2>Level <span id="next-level-num"></span></h2>
        <ul id="level-desc"></ul>
    </div>

    <div class="game-container" id="game-container">
        <h1>Celebrity Bartender</h1>
        <div class="status-bar">
            <div class="status-item"><p>Level: <span id="current-level">1</span> - <span id="bartender-title">Novice Mixer</span></p></div>
            <div class="status-item"><p>Drinks Made: <span id="drinks-made">0</span>/10</p></div>
            <div class="status-item"><p>Timer: <span id="level-timer">60</span>s</p></div>
            <div class="status-item"><p>Tips: $<span id="tips">0.00</span></p></div>
            <div class="status-item"><p>Income/sec: $<span id="income-per-second">0</span></p></div>
            <div class="status-item"><p class="money-display">Money: $<span id="money">0.00</span></p></div>
        </div>

        <div class="buttons-container">
            <button onclick="openRestockModal()">Restock Ingredients</button>
            <div id="upgrades-container"></div>
        </div>

        <div class="order-display" id="current-orders">
            <h2>Current Orders:</h2>
            <div id="orders"></div>
        </div>
    </div>

    <div id="notification"></div>
    <div id="tip-notification"></div>

    <div id="restock-modal" class="popup">
        <button class="close-btn" onclick="closeRestockModal()">X</button>
        <h2>Restock Ingredients</h2>
        <table id="restock-table">
            <thead>
                <tr><th>Ingredient</th><th>Stock</th><th>Cost</th><th>Action</th></tr>
            </thead>
            <tbody id="restock-table-body"></tbody>
        </table>
        <button onclick="restockAll()">Restock All</button>
    </div>

    <div id="recap-screen">
        <h2>Game Recap - Cheers!</h2>
        <ul id="recap-list"></ul>
        <button onclick="restartGame()">Play Again</button>
    </div>

    <script>
        const gameState = {
            currentLevel: 1,
            maxLevels: 5,
            drinksPerLevel: 10,
            drinksMade: 0,
            totalTips: 0,
            money: 0,
            incomePerSecond: 0,
            levelTimeRemaining: 60,
            ordersCompleted: [],
            timerInterval: null,
            orderInterval: null,
            currentOrders: [],
            ingredientStock: {},
            playerLevel: 1,
            bartenderTitle: "Novice Mixer",
            ordersServedThisLevel: 0,
            highlightingEnabled: true
        };

        const drinkRecipes = {
            1: {
                "Soda": ["Soda", "Ice", "Glass"],
                "Beer": ["Beer", "Glass"],
                "Juice": ["Juice", "Glass"]
            },
            2: {
                "Lemonade": ["Lemon Juice", "Sugar", "Water", "Ice", "Glass"],
                "Iced Tea": ["Tea", "Ice", "Sugar", "Glass"]
            },
            3: {
                "Gin Tonic": ["Gin", "Tonic Water", "Lime", "Glass"],
                "Screwdriver": ["Vodka", "Orange Juice", "Glass"]
            },
            4: {
                "Margarita": ["Tequila", "Lime Juice", "Triple Sec", "Salt Rim", "Glass"],
                "Mojito": ["Rum", "Mint", "Lime Juice", "Sugar", "Soda Water", "Glass"]
            },
            5: {
                "Cosmopolitan": ["Vodka", "Cranberry Juice", "Lime Juice", "Triple Sec", "Glass"],
                "Pina Colada": ["Rum", "Pineapple Juice", "Coconut Cream", "Ice", "Glass"]
            }
        };

        const levelDescriptions = {
            1: ["Easy Drinks", "60 Seconds", "2 Orders Max", "Low Celebrity Chance"],
            2: ["More Ingredients", "55 Seconds", "2 Orders Max", "Slight Celebrity Boost"],
            3: ["Tricky Mixes", "50 Seconds", "3 Orders Max", "More Celebrities"],
            4: ["Complex Cocktails", "45 Seconds", "3 Orders Max", "Higher Celebrity Chance"],
            5: ["Master Level", "40 Seconds", "4 Orders Max", "Celebrity Frenzy"]
        };

        const bartenderTitles = {
            1: "Novice Mixer",
            2: "Apprentice Bartender",
            3: "Junior Bartender",
            4: "Senior Bartender",
            5: "Master Mixologist"
        };

        const celebrities = ["Brad Pitt", "Beyoncé", "Leonardo DiCaprio", "Taylor Swift", "Dwayne Johnson"];
        const levelSettings = {
            1: { time: 60, celebrityChance: 0.1, maxOrders: 2, orderInterval: 5000 },
            2: { time: 55, celebrityChance: 0.15, maxOrders: 2, orderInterval: 4500 },
            3: { time: 50, celebrityChance: 0.2, maxOrders: 3, orderInterval: 4000 },
            4: { time: 45, celebrityChance: 0.25, maxOrders: 3, orderInterval: 3500 },
            5: { time: 40, celebrityChance: 0.3, maxOrders: 4, orderInterval: 3000 }
        };

        const upgrades = [
            { name: "Fancy Glassware", cost: 50, benefit: 2, purchased: false },
            { name: "Bartender Assistant", cost: 200, benefit: 5, purchased: false },
            { name: "Live Music", cost: 500, benefit: 10, purchased: false }
        ];

        const allIngredients = [...new Set(Object.values(drinkRecipes).flatMap(level => Object.values(level).flat()))];
        allIngredients.forEach(ing => {
            if (!["Glass"].includes(ing)) gameState.ingredientStock[ing] = 20;
        });

        document.getElementById('enter-btn').addEventListener('click', () => {
            document.getElementById('welcome-screen').style.display = 'none';
            document.getElementById('game-container').style.display = 'block';
            showPopup('instructions');
            startLevel();
            renderUpgrades();
        });

        document.getElementById('enter-btn').addEventListener('touchstart', (e) => {
            e.preventDefault();
            document.getElementById('welcome-screen').style.display = 'none';
            document.getElementById('game-container').style.display = 'block';
            showPopup('instructions');
            startLevel();
            renderUpgrades();
        });

        function showPopup(id) {
            const popup = document.getElementById(id);
            popup.classList.add('show');
            if (id !== 'level-transition') setTimeout(() => hidePopup(id), 5000);
        }

        function hidePopup(id) {
            const popup = document.getElementById(id);
            popup.classList.remove('show');
        }

        function startLevel() {
            gameState.drinksMade = 0;
            gameState.ordersServedThisLevel = 0;
            gameState.highlightingEnabled = true;
            gameState.levelTimeRemaining = levelSettings[gameState.currentLevel].time;
            gameState.currentOrders = [];
            gameState.playerLevel = gameState.currentLevel;
            gameState.bartenderTitle = bartenderTitles[gameState.currentLevel];
            updateStats();
            startTimer();
            generateOrder();
            if (gameState.orderInterval) clearInterval(gameState.orderInterval);
            gameState.orderInterval = setInterval(generateOrder, levelSettings[gameState.currentLevel].orderInterval);
        }

        function showLevelTransition(nextLevel) {
            document.getElementById('next-level-num').textContent = nextLevel;
            const descList = document.getElementById('level-desc');
            descList.innerHTML = '';
            levelDescriptions[nextLevel].forEach(desc => {
                const li = document.createElement('li');
                li.textContent = desc;
                descList.appendChild(li);
            });
            showPopup('level-transition');
        }

        function updateStats() {
            document.getElementById('current-level').textContent = gameState.currentLevel;
            document.getElementById('bartender-title').textContent = gameState.bartenderTitle;
            document.getElementById('drinks-made').textContent = `${gameState.drinksMade}/${gameState.drinksPerLevel}`;
            document.getElementById('level-timer').textContent = gameState.levelTimeRemaining;
            document.getElementById('tips').textContent = gameState.totalTips.toFixed(2);
            document.getElementById('income-per-second').textContent = gameState.incomePerSecond.toFixed(2);
            document.getElementById('money').textContent = gameState.money.toFixed(2);
        }

        function startTimer() {
            if (gameState.timerInterval) clearInterval(gameState.timerInterval);
            gameState.timerInterval = setInterval(() => {
                gameState.levelTimeRemaining--;
                gameState.money += gameState.incomePerSecond / 10;
                updateStats();
                if (gameState.levelTimeRemaining <= 0 && gameState.drinksMade < gameState.drinksPerLevel) {
                    clearInterval(gameState.timerInterval);
                    showNotification("Time's up! Level restarting...");
                    setTimeout(startLevel, 2000);
                }
            }, 1000);
        }

        function generateOrder() {
            if (gameState.currentOrders.length >= levelSettings[gameState.currentLevel].maxOrders || gameState.drinksMade >= gameState.drinksPerLevel) return;
            const drinks = Object.keys(drinkRecipes[gameState.currentLevel]);
            const drink = drinks[Math.floor(Math.random() * drinks.length)];
            const isCelebrity = Math.random() < levelSettings[gameState.currentLevel].celebrityChance;
            const customerName = isCelebrity ? celebrities[Math.floor(Math.random() * celebrities.length)] : "Customer";
            gameState.currentOrders.push({
                drink,
                isCelebrity,
                customerName,
                selectedIngredients: [],
                showIngredients: false,
                tipPenaltyApplied: false
            });
            displayOrders();
        }

        function displayOrders() {
            const ordersDiv = document.getElementById('orders');
            ordersDiv.innerHTML = '';
            gameState.currentOrders.forEach((order, index) => {
                const ticket = document.createElement('div');
                ticket.className = `ticket ${order.isCelebrity ? 'celebrity' : ''}`;
                ticket.innerHTML = `
                    <p><strong>${order.isCelebrity ? order.customerName : 'Customer'} Wants:</strong> ${order.drink}</p>
                    <p>Selected: <span id="selected-${index}">${order.selectedIngredients.join(', ')}</span></p>
                    <button class="toggle-ingredients-btn" data-index="${index}">Show Ingredients</button>
                    <div id="required-${index}" style="display: ${order.showIngredients ? 'block' : 'none'}">
                        <p><strong>Required:</strong> ${drinkRecipes[gameState.currentLevel][order.drink].join(', ')}</p>
                    </div>
                    <div id="ingredients-${index}" style="overflow-x: auto; white-space: nowrap;"></div>
                    <button data-index="${index}" class="serve-btn">Serve</button>
                `;
                ordersDiv.appendChild(ticket);
                generateIngredients(index);

                ticket.querySelector('.toggle-ingredients-btn').addEventListener('click', () => toggleIngredients(index));
                ticket.querySelector('.toggle-ingredients-btn').addEventListener('touchstart', (e) => {
                    e.preventDefault();
                    toggleIngredients(index);
                });
                ticket.querySelector('.serve-btn').addEventListener('click', () => serveDrink(index));
                ticket.querySelector('.serve-btn').addEventListener('touchstart', (e) => {
                    e.preventDefault();
                    serveDrink(index);
                });
            });
        }

        function toggleIngredients(orderIndex) {
            const order = gameState.currentOrders[orderIndex];
            order.showIngredients = !order.showIngredients;
            order.tipPenaltyApplied = order.showIngredients;
            displayOrders();
        }

        function generateIngredients(orderIndex) {
            const ingredientsDiv = document.getElementById(`ingredients-${orderIndex}`);
            ingredientsDiv.innerHTML = '';
            const requiredIngredients = drinkRecipes[gameState.currentLevel][gameState.currentOrders[orderIndex].drink];
            allIngredients.forEach(ing => {
                const btn = document.createElement('button');
                btn.textContent = ing;
                btn.className = 'ingredient-button';
                btn.dataset.ingredient = ing;
                btn.dataset.index = orderIndex;
                if (gameState.currentOrders[orderIndex].selectedIngredients.includes(ing)) btn.classList.add('selected');
                if (gameState.highlightingEnabled && gameState.ordersServedThisLevel < 3 && requiredIngredients.includes(ing)) btn.classList.add('required');
                if (!["Glass"].includes(ing) && gameState.ingredientStock[ing] <= 0) btn.disabled = true;
                btn.addEventListener('click', (e) => {
                    e.preventDefault(); // Prevent default click behavior
                    selectIngredient(ing, orderIndex);
                });
                btn.addEventListener('touchstart', (e) => {
                    e.preventDefault();
                    selectIngredient(ing, orderIndex);
                });
                ingredientsDiv.appendChild(btn);
            });
        }

        function selectIngredient(ingredient, orderIndex) {
            const order = gameState.currentOrders[orderIndex];
            if (order.selectedIngredients.includes(ingredient)) {
                showNotification(`Already added ${ingredient}!`);
                return;
            }
            if (!["Glass"].includes(ingredient)) {
                if (gameState.ingredientStock[ingredient] <= 0) {
                    showNotification(`Out of ${ingredient}! Restock!`);
                    return;
                }
                gameState.ingredientStock[ingredient]--;
            }
            order.selectedIngredients.push(ingredient);
            displayOrders();
        }

        function serveDrink(orderIndex) {
            const order = gameState.currentOrders[orderIndex];
            const correctIngredients = drinkRecipes[gameState.currentLevel][order.drink];
            const isCorrect = arraysEqual(order.selectedIngredients.sort(), correctIngredients.sort());

            const basePrice = correctIngredients.length * 2;
            let tip = isCorrect ? (order.isCelebrity ? Math.random() * 50 + 20 : Math.random() * 10 + 2) : 0;
            if (isCorrect && order.tipPenaltyApplied) tip *= 0.5;

            if (isCorrect) {
                gameState.totalTips += tip;
                gameState.money += basePrice + tip;
                gameState.drinksMade++;
                gameState.ordersServedThisLevel++;
                showTipNotification(`+$${tip.toFixed(2)} Tip${order.isCelebrity ? ` from ${order.customerName}` : ''}!`);
            } else {
                showNotification("Wrong mix! No tip.");
            }

            gameState.ordersCompleted.push({
                level: gameState.currentLevel,
                drink: order.drink,
                correct: isCorrect,
                tip: tip,
                earnings: isCorrect ? basePrice : 0,
                isCelebrity: order.isCelebrity
            });

            gameState.currentOrders.splice(orderIndex, 1);
            updateStats();
            displayOrders();

            if (gameState.drinksMade >= gameState.drinksPerLevel) {
                clearInterval(gameState.orderInterval);
                if (gameState.currentOrders.length === 0) {
                    if (gameState.currentLevel < gameState.maxLevels) {
                        gameState.currentLevel++;
                        showLevelTransition(gameState.currentLevel);
                    } else {
                        endGame();
                    }
                }
            }
        }

        function arraysEqual(arr1, arr2) {
            if (arr1.length !== arr2.length) return false;
            return arr1.every((item, idx) => item === arr2[idx]);
        }

        function showNotification(message) {
            const notif = document.getElementById('notification');
            notif.textContent = message;
            notif.style.display = 'block';
            notif.style.opacity = '1';
            setTimeout(() => {
                notif.style.opacity = '0';
                setTimeout(() => notif.style.display = 'none', 500);
            }, 2000);
        }

        function showTipNotification(message) {
            const notif = document.getElementById('tip-notification');
            notif.textContent = message;
            notif.style.display = 'block';
            notif.style.opacity = '1';
            setTimeout(() => {
                notif.style.opacity = '0';
                setTimeout(() => notif.style.display = 'none', 500);
            }, 2000);
        }

        function openRestockModal() {
            const tbody = document.getElementById('restock-table-body');
            tbody.innerHTML = '';
            for (const [ing, stock] of Object.entries(gameState.ingredientStock)) {
                const cost = 10 * gameState.currentLevel;
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${ing}</td>
                    <td>${stock}</td>
                    <td>$${cost}</td>
                    <td><button class="restock-btn" data-ing="${ing}" data-cost="${cost}">Restock</button></td>
                `;
                tbody.appendChild(row);
                row.querySelector('.restock-btn').addEventListener('click', () => restockIngredient(ing, cost));
                row.querySelector('.restock-btn').addEventListener('touchstart', (e) => {
                    e.preventDefault();
                    restockIngredient(ing, cost);
                });
            }
            showPopup('restock-modal');
        }

        function restockIngredient(ingredient, cost) {
            if (gameState.money >= cost) {
                gameState.money -= cost;
                gameState.ingredientStock[ingredient] += 20;
                updateStats();
                openRestockModal();
                displayOrders();
            } else {
                showNotification("Not enough money!");
            }
        }

        function restockAll() {
            const totalCost = Object.keys(gameState.ingredientStock).length * 10 * gameState.currentLevel;
            if (gameState.money >= totalCost) {
                gameState.money -= totalCost;
                for (const ing in gameState.ingredientStock) {
                    gameState.ingredientStock[ing] += 20;
                }
                updateStats();
                hidePopup('restock-modal');
                displayOrders();
            } else {
                showNotification("Not enough money!");
            }
        }

        function closeRestockModal() {
            hidePopup('restock-modal');
        }

        function renderUpgrades() {
            const container = document.getElementById('upgrades-container');
            container.innerHTML = '';
            upgrades.forEach((upgrade, index) => {
                if (!upgrade.purchased) {
                    const btn = document.createElement('button');
                    btn.textContent = `${upgrade.name} ($${upgrade.cost})`;
                    btn.addEventListener('click', () => buyUpgrade(index));
                    btn.addEventListener('touchstart', (e) => {
                        e.preventDefault();
                        buyUpgrade(index);
                    });
                    container.appendChild(btn);
                }
            });
        }

        function buyUpgrade(index) {
            const upgrade = upgrades[index];
            if (gameState.money >= upgrade.cost && !upgrade.purchased) {
                gameState.money -= upgrade.cost;
                gameState.incomePerSecond += upgrade.benefit;
                upgrade.purchased = true;
                showNotification(`${upgrade.name} purchased!`);
                updateStats();
                renderUpgrades();
            } else {
                showNotification("Not enough money or already purchased!");
            }
        }

        function endGame() {
            clearInterval(gameState.timerInterval);
            clearInterval(gameState.orderInterval);
            document.getElementById('game-container').style.display = 'none';
            const recapScreen = document.getElementById('recap-screen');
            recapScreen.style.display = 'block';

            const recapList = document.getElementById('recap-list');
            recapList.innerHTML = `
                <li>Total Tips Earned: $${gameState.totalTips.toFixed(2)}</li>
                <li>Total Money Earned: $${gameState.money.toFixed(2)}</li>
                <li>Levels Completed: ${gameState.currentLevel}</li>
                <li>Total Drinks Served: ${gameState.ordersCompleted.length}</li>
                <li>Correct Drinks: ${gameState.ordersCompleted.filter(o => o.correct).length}</li>
                <li>Incorrect Drinks: ${gameState.ordersCompleted.filter(o => !o.correct).length}</li>
                <li>Celebrity Orders Served: ${gameState.ordersCompleted.filter(o => o.isCelebrity).length}</li>
                <li>Final Title: ${gameState.bartenderTitle}</li>
            `;
        }

        function restartGame() {
            gameState.currentLevel = 1;
            gameState.drinksMade = 0;
            gameState.totalTips = 0;
            gameState.money = 0;
            gameState.incomePerSecond = 0;
            gameState.ordersCompleted = [];
            gameState.playerLevel = 1;
            gameState.bartenderTitle = "Novice Mixer";
            gameState.ordersServedThisLevel = 0;
            gameState.highlightingEnabled = true;
            upgrades.forEach(u => u.purchased = false);
            allIngredients.forEach(ing => {
                if (!["Glass"].includes(ing)) gameState.ingredientStock[ing] = 20;
            });
            document.getElementById('recap-screen').style.display = 'none';
            document.getElementById('game-container').style.display = 'block';
            startLevel();
            renderUpgrades();
        }
    </script>
</body>
</html>
