<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Clicker Game</title>
    <style>
        .sparkle {
            position: fixed;
            width: 10px;
            height: 10px;
            border-radius: 50%;
            pointer-events: none;
            animation: sparkle-fall 1s ease-out forwards;
        }

        @keyframes sparkle-fall {
            0% {
                transform: translate(0, 0) scale(1);
                opacity: 1;
            }
            100% {
                transform: translate(var(--randomX, 0), 100px) scale(0);
                opacity: 0;
            }
        }

        body {
            font-family: 'Consolas', 'Courier New', monospace;
            background-color: white;
            color: black;
            max-width: 600px;
            margin: 50px auto;
            padding: 20px;
        }
        
        #click-button {
            font-family: 'Consolas', 'Courier New', monospace;
            font-size: 24px;
            padding: 30px 60px;
            margin: 20px 0;
            cursor: pointer;
            background-color: white;
            color: black;
            border: 2px solid black;
        }
        
        #click-button:hover {
            background-color: black;
            color: white;
        }
        
        .upgrade {
            font-family: 'Consolas', 'Courier New', monospace;
            font-size: 16px;
            padding: 15px;
            margin: 10px 0;
            cursor: pointer;
            background-color: white;
            color: black;
            border: 2px solid black;
            display: block;
            width: 100%;
            text-align: left;
        }
        
        .upgrade:hover {
            background-color: black;
            color: white;
        }
        
        .upgrade:disabled {
            cursor: not-allowed;
            opacity: 0.5;
        }
        
        h1, h2 {
            font-weight: normal;
        }
    </style>
</head>
<body>
    <h1>CLICKER GAME</h1>
    
    <h2>Points: <span id="points">0</span></h2>
    <h2>Points Per Click: <span id="click-value">1</span></h2>
    
    <button id="click-button">CLICK ME</button>
    
    <h2>UPGRADES</h2>
    
    <button class="upgrade" id="double-upgrade">
        Double Click Value - Cost: <span id="double-cost">10</span>
    </button>
    <button class="upgrade" id="auto-upgrade">
        Auto-Clicker (+<span id="auto-value">1</span>/sec) - Cost: <span id="auto-cost">50</span> - Owned: <span id="auto-owned">0</span>
    </button>

    <script>
        // Game variables
        let points = 0;
        let clickValue = 1;
        let doubleCost = 10;

        let autoClickerCost = 50;
        let autoClickerOwned = 0;
        let autoClickerValue = 1;

        // Get elements
        const pointsDisplay = document.getElementById('points');
        const clickValueDisplay = document.getElementById('click-value');
        const clickButton = document.getElementById('click-button');
        const doubleUpgrade = document.getElementById('double-upgrade');
        const doubleCostDisplay = document.getElementById('double-cost');

        const autoUpgrade = document.getElementById('auto-upgrade');
        const autoCostDisplay = document.getElementById('auto-cost');
        const autoOwnedDisplay = document.getElementById('auto-owned');
        const autoValueDisplay = document.getElementById('auto-value');

        // Click button function
        clickButton.addEventListener('click', function(event) {
            points += clickValue;
            updateDisplay();
            createSparkles(event);
        });

        // Double click upgrade function
        doubleUpgrade.addEventListener('click', function() {
            if (points >= doubleCost) {
                points -= doubleCost;
                // Increase click power
                clickValue = Math.floor(clickValue * 1.2);
                // Increase cost
                doubleCost = Math.floor(doubleCost * 1.5);
                updateDisplay();
            }
        });

        // Auto-clicker upgrade function
        autoUpgrade.addEventListener('click', function() {
            if (points >= autoClickerCost) {
                points -= autoClickerCost;

                // Increase how many auto-clickers you own
                autoClickerOwned += 1;

                // Optional: increase strength per auto-clicker
                autoClickerValue = 1; // keep 1 each, or change to grow if you want

                // Increase cost for next auto-clicker
                autoClickerCost = Math.floor(autoClickerCost * 1.2);

                updateDisplay();
            }
        });

        // Create sparkles function
        function createSparkles(event) {
            const colors = ['#4169E1', '#9370DB', '#FFD700'];
            const sparkleCount = 8;
            
            for (let i = 0; i < sparkleCount; i++) {
                const sparkle = document.createElement('div');
                sparkle.className = 'sparkle';
                
                const randomColor = colors[Math.floor(Math.random() * colors.length)];
                sparkle.style.backgroundColor = randomColor;
                
                sparkle.style.left = event.pageX + 'px';
                sparkle.style.top = event.pageY + 'px';
                
                const randomX = (Math.random() - 0.5) * 100;
                sparkle.style.setProperty('--randomX', randomX + 'px');
                
                document.body.appendChild(sparkle);
                
                setTimeout(function() {
                    sparkle.remove();
                }, 1000);
            }
        }

        // Update display function
        function updateDisplay() {
            pointsDisplay.textContent = points;
            clickValueDisplay.textContent = clickValue;
            doubleCostDisplay.textContent = doubleCost;

            autoCostDisplay.textContent = autoClickerCost;
            autoOwnedDisplay.textContent = autoClickerOwned;
            autoValueDisplay.textContent = autoClickerValue;

            // Disable upgrade buttons if not enough points
            doubleUpgrade.disabled = points < doubleCost;
            autoUpgrade.disabled = points < autoClickerCost;
        }
        
        // Auto-clicker timer
        setInterval(function() {
            if (autoClickerOwned > 0) {
                points += autoClickerOwned * autoClickerValue;
                updateDisplay();
            }
        }, 1000);

        // Initialize display
        updateDisplay();
    </script>
</body>
</html>
