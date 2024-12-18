<style>
    body {
        background-color: #000000; /* Fixing background */
        color: #FFFFFF;
    }

    .container {
        text-align: center;
        margin-top: 50px;
    }

    #snake {
        border-style: solid;
        border-width: 10px;
        border-color: #FFFFFF;
    }

    #menu, #gameover, #setting {
        display: none;
    }

    #menu.active, #gameover.active, #setting.active {
        display: block;
    }

    .link-alert {
        cursor: pointer;
        font-size: 20px;
        color: #FFFFFF;
        margin: 10px 0;
    }

    .link-alert:hover {
        color: #FFD700;
    }
</style>

<div class="container">
    <h2>Snake</h2>
    <header class="pb-3 mb-4 border-bottom border-primary text-dark">
        <p class="fs-4">Score: <span id="score_value">0</span></p>
    </header>
    <div id="menu" class="active">
        <p>Press <span style="background-color: #FFFFFF; color: #000000">space</span> to start the game.</p>
        <a id="new_game" class="link-alert">New Game</a>
        <a id="setting_menu" class="link-alert">Settings</a>
    </div>
    <div id="gameover">
        <p>Game Over! Press <span style="background-color: #FFFFFF; color: #000000">space</span> to restart.</p>
        <a id="new_game1" class="link-alert">New Game</a>
        <a id="setting_menu1" class="link-alert">Settings</a>
    </div>
    <canvas id="snake" width="320" height="320" tabindex="1"></canvas>
    <div id="setting">
        <p>Settings:</p>
        <p>Speed:</p>
        <input type="radio" id="speed1" name="speed" value="120" checked>
        <label for="speed1">Slow</label>
        <input type="radio" id="speed2" name="speed" value="75">
        <label for="speed2">Normal</label>
        <input type="radio" id="speed3" name="speed" value="35">
        <label for="speed3">Fast</label>
        <p>Wall:</p>
        <input type="radio" id="wallon" name="wall" value="1" checked>
        <label for="wallon">On</label>
        <input type="radio" id="walloff" name="wall" value="0">
        <label for="walloff">Off</label>
        <a id="new_game2" class="link-alert">New Game</a>
    </div>
</div>

<script>
    (function () {
        const canvas = document.getElementById("snake");
        const ctx = canvas.getContext("2d");
        const scoreDisplay = document.getElementById("score_value");
        const screens = {
            menu: document.getElementById("menu"),
            gameover: document.getElementById("gameover"),
            setting: document.getElementById("setting"),
        };

        const buttons = {
            newGame: document.getElementById("new_game"),
            newGame1: document.getElementById("new_game1"),
            newGame2: document.getElementById("new_game2"),
            settingsMenu: document.getElementById("setting_menu"),
            settingsMenu1: document.getElementById("setting_menu1"),
        };

        let snake = [];
        let food = { x: 0, y: 0 };
        let direction = 1; // 0 - Up, 1 - Right, 2 - Down, 3 - Left
        let nextDirection = 1;
        let score = 0;
        let speed = 120;
        let wall = 1;

        function showScreen(screenName) {
            Object.values(screens).forEach((screen) => (screen.className = ""));
            screens[screenName].className = "active";
        }

        function startGame() {
            snake = [{ x: 15, y: 15 }];
            score = 0;
            updateScore();
            direction = 1;
            nextDirection = 1;
            placeFood();
            showScreen("menu");
            mainLoop();
        }

        function updateScore() {
            scoreDisplay.textContent = score;
        }

        function placeFood() {
            food.x = Math.floor(Math.random() * (canvas.width / 10));
            food.y = Math.floor(Math.random() * (canvas.height / 10));
        }

        function mainLoop() {
            ctx.fillStyle = "black";
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            ctx.fillStyle = "white";
            snake.forEach((segment) => {
                ctx.fillRect(segment.x * 10, segment.y * 10, 10, 10);
            });

            ctx.fillStyle = "red";
            ctx.fillRect(food.x * 10, food.y * 10, 10, 10);

            const head = { ...snake[0] };
            switch (direction) {
                case 0:
                    head.y--;
                    break;
                case 1:
                    head.x++;
                    break;
                case 2:
                    head.y++;
                    break;
                case 3:
                    head.x--;
                    break;
            }

            if (wall === 1 && (head.x < 0 || head.x >= 32 || head.y < 0 || head.y >= 32)) {
                showScreen("gameover");
                return;
            }

            if (wall === 0) {
                if (head.x < 0) head.x = 31;
                if (head.x >= 32) head.x = 0;
                if (head.y < 0) head.y = 31;
                if (head.y >= 32) head.y = 0;
            }

            if (snake.some((segment) => segment.x === head.x && segment.y === head.y)) {
                showScreen("gameover");
                return;
            }

            snake.unshift(head);

            if (head.x === food.x && head.y === food.y) {
                score++;
                updateScore();
                placeFood();
            } else {
                snake.pop();
            }

            setTimeout(mainLoop, speed);
        }

        buttons.newGame.addEventListener("click", startGame);
        buttons.newGame1.addEventListener("click", startGame);
        buttons.newGame2.addEventListener("click", startGame);

        buttons.settingsMenu.addEventListener("click", () => showScreen("setting"));
        buttons.settingsMenu1.addEventListener("click", () => showScreen("setting"));

        document.getElementsByName("speed").forEach((input) => {
            input.addEventListener("change", () => {
                speed = parseInt(input.value);
            });
        });

        document.getElementsByName("wall").forEach((input) => {
            input.addEventListener("change", () => {
                wall = parseInt(input.value);
            });
        });

        document.addEventListener("keydown", (event) => {
            if (event.code === "Space" && screens.menu.className === "active") {
                startGame();
            }

            const keyDirections = {
                ArrowUp: 0,
                ArrowRight: 1,
                ArrowDown: 2,
                ArrowLeft: 3,
            };

            if (keyDirections[event.key] !== undefined && Math.abs(direction - keyDirections[event.key]) !== 2) {
                nextDirection = keyDirections[event.key];
            }
        });

        startGame();
    })();
</script>
