<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Flash Games</title>
    <script src="https://unpkg.com/@ruffle-rs/ruffle"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }

        .header {
            text-align: center;
            color: white;
            padding: 40px 20px 20px;
        }

        .header h1 {
            font-size: 3em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
        }

        .games-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 30px;
            padding: 40px 20px;
            max-width: 1400px;
            margin: 0 auto;
        }

        .game-card {
            background: white;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            cursor: pointer;
        }

        .game-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 15px 40px rgba(0,0,0,0.4);
        }

        .game-thumbnail {
            width: 100%;
            height: 180px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 4em;
            position: relative;
        }

        .game-thumbnail.pizza { background: linear-gradient(135deg, #ff6b6b 0%, #feca57 100%); }
        .game-thumbnail.burger { background: linear-gradient(135deg, #ff9a56 0%, #ff6b81 100%); }
        .game-thumbnail.ice { background: linear-gradient(135deg, #a8edea 0%, #fed6e3 100%); }
        .game-thumbnail.taco { background: linear-gradient(135deg, #ffd89b 0%, #19547b 100%); }
        .game-thumbnail.pancake { background: linear-gradient(135deg, #f6d365 0%, #fda085 100%); }
        .game-thumbnail.pasta { background: linear-gradient(135deg, #ff6e7f 0%, #bfe9ff 100%); }
        .game-thumbnail.cupcake { background: linear-gradient(135deg, #fccb90 0%, #d57eeb 100%); }
        .game-thumbnail.donut { background: linear-gradient(135deg, #fa709a 0%, #fee140 100%); }

        .game-info {
            padding: 20px;
        }

        .game-title {
            font-size: 1.3em;
            font-weight: bold;
            color: #333;
            margin-bottom: 8px;
        }

        .game-description {
            color: #666;
            font-size: 0.9em;
            line-height: 1.5;
        }

        /* Fullscreen game container */
        .game-fullscreen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            background: #1a1a1a;
            z-index: 1000;
            display: none;
            flex-direction: column;
        }

        .game-fullscreen.active {
            display: flex;
        }

        .game-header {
            background: rgba(0, 0, 0, 0.95);
            padding: 15px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            color: white;
            box-shadow: 0 2px 10px rgba(0,0,0,0.5);
        }

        .game-header h2 {
            font-size: 1.3em;
        }

        .controls {
            display: flex;
            gap: 10px;
        }

        .btn {
            background: #667eea;
            border: none;
            color: white;
            padding: 10px 20px;
            border-radius: 5px;
            font-size: 14px;
            cursor: pointer;
            transition: background 0.2s;
            font-weight: 600;
        }

        .btn:hover {
            background: #5568d3;
        }

        .btn.close {
            background: #ff4757;
        }

        .btn.close:hover {
            background: #ff3838;
        }

        .game-container {
            flex: 1;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 0;
            background: #000;
        }

        #ruffleContainer {
            width: 100%;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .loading {
            color: white;
            font-size: 1.5em;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>🎮 My Flash Games Collection</h1>
        <p>Click any game to play fullscreen</p>
    </div>

    <div class="games-grid">
        <div class="game-card" onclick="loadGame('Papa\'s Pizzeria', 'games/papas-pizzeria.swf')">
            <div class="game-thumbnail pizza">🍕</div>
            <div class="game-info">
                <div class="game-title">Papa's Pizzeria</div>
                <div class="game-description">Take orders, prepare pizzas, and serve customers!</div>
            </div>
        </div>

        <div class="game-card" onclick="loadGame('Papa\'s Burgeria', 'games/papas-burgeria.swf')">
            <div class="game-thumbnail burger">🍔</div>
            <div class="game-info">
                <div class="game-title">Papa's Burgeria</div>
                <div class="game-description">Grill burgers and stack them perfectly!</div>
            </div>
        </div>

        <div class="game-card" onclick="loadGame('Papa\'s Freezeria', 'games/papas-freezeria.swf')">
            <div class="game-thumbnail ice">🍦</div>
            <div class="game-info">
                <div class="game-title">Papa's Freezeria</div>
                <div class="game-description">Mix delicious ice cream sundaes for beachgoers!</div>
            </div>
        </div>

        <div class="game-card" onclick="loadGame('Papa\'s Taco Mia', 'games/papas-taco-mia.swf')">
            <div class="game-thumbnail taco">🌮</div>
            <div class="game-info">
                <div class="game-title">Papa's Taco Mia</div>
                <div class="game-description">Build perfect tacos with all the fixings!</div>
            </div>
        </div>

        <div class="game-card" onclick="loadGame('Papa\'s Pancakeria', 'games/papas-pancakeria.swf')">
            <div class="game-thumbnail pancake">🥞</div>
            <div class="game-info">
                <div class="game-title">Papa's Pancakeria</div>
                <div class="game-description">Flip pancakes and create breakfast masterpieces!</div>
            </div>
        </div>

        <div class="game-card" onclick="loadGame('Papa\'s Pastaria', 'games/papas-pastaria.swf')">
            <div class="game-thumbnail pasta">🍝</div>
            <div class="game-info">
                <div class="game-title">Papa's Pastaria</div>
                <div class="game-description">Cook pasta and serve Italian dishes!</div>
            </div>
        </div>

        <div class="game-card" onclick="loadGame('Papa\'s Cupcakeria', 'games/papas-cupcakeria.swf')">
            <div class="game-thumbnail cupcake">🧁</div>
            <div class="game-info">
                <div class="game-title">Papa's Cupcakeria</div>
                <div class="game-description">Bake and decorate delicious cupcakes!</div>
            </div>
        </div>

        <div class="game-card" onclick="loadGame('Papa\'s Donuteria', 'games/papas-donuteria.swf')">
            <div class="game-thumbnail donut">🍩</div>
            <div class="game-info">
                <div class="game-title">Papa's Donuteria</div>
                <div class="game-description">Fry donuts and add tasty toppings!</div>
            </div>
        </div>
    </div>

    <div class="game-fullscreen" id="gameContainer">
        <div class="game-header">
            <h2 id="gameTitle">Loading Game...</h2>
            <div class="controls">
                <button class="btn" onclick="toggleFullscreen()">⛶ Fullscreen</button>
                <button class="btn close" onclick="closeGame()">✕ Close (ESC)</button>
            </div>
        </div>
        <div class="game-container">
            <div id="ruffleContainer">
                <div class="loading">Loading game...</div>
            </div>
        </div>
    </div>

    <script>
        let currentPlayer = null;

        function loadGame(title, swfPath) {
            const ruffle = window.RufflePlayer.newest();
            const player = ruffle.createPlayer();
            const container = document.getElementById("ruffleContainer");
            const gameContainer = document.getElementById('gameContainer');
            const titleEl = document.getElementById('gameTitle');
            
            // Clear previous game
            container.innerHTML = "";
            if (currentPlayer) {
                currentPlayer.destroy();
            }
            
            // Set up new player
            container.appendChild(player);
            currentPlayer = player;
            
            // Style the player
            player.style.width = "100%";
            player.style.height = "100%";
            
            // Update title and show container
            titleEl.textContent = title;
            gameContainer.classList.add('active');
            
            // Load the SWF file
            player.load(swfPath).catch(err => {
                container.innerHTML = `<div class="loading" style="color: #ff4757;">Error loading game: ${err.message}<br><br>Make sure the SWF file exists at: ${swfPath}</div>`;
            });
        }

        function closeGame() {
            const gameContainer = document.getElementById('gameContainer');
            gameContainer.classList.remove('active');
            
            if (currentPlayer) {
                currentPlayer.destroy();
                currentPlayer = null;
            }
            
            const container = document.getElementById("ruffleContainer");
            container.innerHTML = '<div class="loading">Loading game...</div>';
        }

        function toggleFullscreen() {
            if (!document.fullscreenElement) {
                document.getElementById('gameContainer').requestFullscreen();
            } else {
                document.exitFullscreen();
            }
        }

        // Close game with ESC key
        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape' && !document.fullscreenElement) {
                closeGame();
            }
        });

        // Handle fullscreen changes
        document.addEventListener('fullscreenchange', () => {
            // Game container adapts automatically
        });
    </script>
</body>
</html>
