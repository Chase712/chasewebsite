<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Snake Game</title>
    <style>
        body {
            text-align: center;
        }
        #menu, #gameover {
            display: block;
        }
        #snake {
            display: none;
        }
        canvas {
            margin: 20px auto;
            background-color: green; /* Green background */
        }
        .button {
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
            font-size: 16px;
        }
    </style>
</head>
<body>

<!-- Main Menu -->
<div id="menu">
    <h1>Snake Game</h1>
    <button class="button" id="new_game">Start Game</button>
</div>

<!-- Game Over Screen -->
<div id="gameover" style="display:none;">
    <h2>Game Over!</h2>
    <button class="button" id="new_game1">Restart Game</button>
</div>

<!-- Canvas for Snake Game -->
<canvas id="snake" width="600" height="400"></canvas>

<script>
    (function () {
        const canvas = document.getElementById("snake");
        const ctx = canvas.getContext("2d");
        const BLOCK = 20;
        const button_new_game = document.getElementById("new_game");
        const button_new_game1 = document.getElementById("new_game1");

        let SCREEN = 0; // 0 for menu, 1 for game
        let snake;
        let snake_dir;
        let snake_speed;
        let food = { x: 0, y: 0 };
        let score = 0;

        const snakeColor = "#D2B48C"; // Light brown for snake

        // Initialize game
        function initGame() {
            snake = [
                { x: 5, y: 5 },
                { x: 4, y: 5 },
                { x: 3, y: 5 }
            ];
            snake_dir = "RIGHT";
            score = 0;
            food = {
                x: Math.floor(Math.random() * (canvas.width / BLOCK)),
                y: Math.floor(Math.random() * (canvas.height / BLOCK))
            };
            snake_speed = 150; // Default speed
            SCREEN = 1; // Switch to game screen
            document.getElementById("menu").style.display = "none";
            document.getElementById("gameover").style.display = "none";
            canvas.style.display = "block"; // Show canvas
            gameLoop();
        }

        function drawBackground() {
            ctx.fillStyle = "green";
            ctx.fillRect(0, 0, canvas.width, canvas.height); // Full green background
        }

        function drawSnake() {
            ctx.fillStyle = snakeColor; // Snake color
            for (let i = 0; i < snake.length; i++) {
                ctx.fillRect(snake[i].x * BLOCK, snake[i].y * BLOCK, BLOCK, BLOCK);
            }
        }

        function drawFood() {
            ctx.fillStyle = "white";
            ctx.beginPath();
            ctx.arc(food.x * BLOCK + BLOCK / 2, food.y * BLOCK + BLOCK / 2, BLOCK / 2, 0, 2 * Math.PI);
            ctx.fill();
        }

        function updateSnakePosition() {
            let head = { ...snake[0] };

            // Update head position based on direction
            if (snake_dir === "UP") head.y--;
            if (snake_dir === "DOWN") head.y++;
            if (snake_dir === "LEFT") head.x--;
            if (snake_dir === "RIGHT") head.x++;

            snake.unshift(head); // Add the new head

            // If snake eats food, increase score and spawn new food
            if (head.x === food.x && head.y === food.y) {
                score++;
                food = {
                    x: Math.floor(Math.random() * (canvas.width / BLOCK)),
                    y: Math.floor(Math.random() * (canvas.height / BLOCK))
                };
            } else {
                snake.pop(); // Remove the last part of the snake
            }

            // Wall collision check
            if (head.x < 0 || head.x >= canvas.width / BLOCK || head.y < 0 || head.y >= canvas.height / BLOCK) {
                gameOver();
            }

            // Self-collision check
            for (let i = 1; i < snake.length; i++) {
                if (head.x === snake[i].x && head.y === snake[i].y) {
                    gameOver();
                }
            }
        }

        function gameOver() {
            SCREEN = 0;
            document.getElementById("gameover").style.display = "block"; // Show game over screen
        }

        function gameLoop() {
            if (SCREEN !== 1) return;

            drawBackground();
            drawSnake();
            drawFood();
            updateSnakePosition();

            setTimeout(gameLoop, snake_speed); // Loop every 'snake_speed' milliseconds
        }

        // Event listeners for snake controls
        window.addEventListener("keydown", (e) => {
            if (e.key === "ArrowUp" && snake_dir !== "DOWN") {
                snake_dir = "UP";
            } else if (e.key === "ArrowDown" && snake_dir !== "UP") {
                snake_dir = "DOWN";
            } else if (e.key === "ArrowLeft" && snake_dir !== "RIGHT") {
                snake_dir = "LEFT";
            } else if (e.key === "ArrowRight" && snake_dir !== "LEFT") {
                snake_dir = "RIGHT";
            }
        });

        // Start new game from menu
        button_new_game.addEventListener("click", initGame);
        // Restart game after game over
        button_new_game1.addEventListener("click", initGame);
    })();
</script>

</body>
</html>
