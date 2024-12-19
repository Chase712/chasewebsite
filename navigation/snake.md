---
layout: page
title: Snake
search_exclude: true
permalink: /snake/
---

<style>
    body {
        text-align: center;
    }

    .wrap {
        margin-left: auto;
        margin-right: auto;
    }

    canvas {
        border-style: solid;
        border-width: 10px;
        border-color: rgb(30, 121, 44);
        display: block;
        margin: 0 auto;
    }

    #gameover p, #setting p, #menu p {
        font-size: 20px;
    }

    #gameover a, #setting a, #menu a {
        font-size: 30px;
        display: block;
    }

    #gameover a:hover, #setting a:hover, #menu a:hover {
        cursor: pointer;
    }

    #menu {
        display: block;
    }

    #gameover {
        display: none;
    }

    #setting {
        display: none;
    }
</style>

<h2>Snake Game</h2>
<div class="container">
    <header class="pb-3 mb-4 border-bottom border-primary text-dark">
        <p class="fs-4">Score: <span id="score_value">0</span></p>
    </header>
    <div class="container bg-secondary" style="text-align:center;">
        <div id="menu" class="py-4 text-light">
            <p>Welcome to Snake, press <span style="background-color: rgb(220,37,37); color: #000000">space</span> to begin</p>
            <a id="new_game" class="link-alert">new game</a>
            <a id="setting_menu" class="link-alert">settings</a>
        </div>
        <div id="gameover" class="py-4 text-light">
            <p>Game Over, press <span style="background-color:rgb(220, 37, 37); color: #000000">space</span> to try again</p>
            <a id="new_game1" class="link-alert">new game</a>
            <a id="setting_menu1" class="link-alert">settings</a>
        </div>
        <canvas id="snake" class="wrap" width="400" height="400" tabindex="1"></canvas>
        <div id="setting" class="py-4 text-light">
            <p>Settings Screen, press <span style="background-color:rgb(220, 37, 37); color: #000000">space</span> to go back to playing</p>
            <a id="new_game2" class="link-alert">new game</a>
            <br>
            <p>Speed:
                <input id="speed1" type="radio" name="speed" value="200" checked />
                <label for="speed1">Slow</label>
                <input id="speed2" type="radio" name="speed" value="150" />
                <label for="speed2">Normal</label>
                <input id="speed3" type="radio" name="speed" value="100" />
                <label for="speed3">Fast</label>
            </p>
            <p>Wall:
                <input id="wallon" type="radio" name="wall" value="1" checked />
                <label for="wallon">On</label>
                <input id="walloff" type="radio" name="wall" value="0" />
                <label for="walloff">Off</label>
            </p>
        </div>
    </div>
</div>

<script>
(function () {
    const canvas = document.getElementById("snake");
    const ctx = canvas.getContext("2d");
    const BLOCK = 20;
    const ele_score = document.getElementById("score_value");
    const speed_setting = document.getElementsByName("speed");
    const wall_setting = document.getElementsByName("wall");
    const screen_menu = document.getElementById("menu");
    const screen_game_over = document.getElementById("gameover");
    const screen_setting = document.getElementById("setting");
    const button_new_game = document.getElementById("new_game");
    const button_new_game1 = document.getElementById("new_game1");
    const button_new_game2 = document.getElementById("new_game2");
    const button_setting_menu = document.getElementById("setting_menu");
    const button_setting_menu1 = document.getElementById("setting_menu1");

    let SCREEN = -1;
    let snake;
    let snake_dir;
    let snake_next_dir;
    let snake_speed;
    let food = { x: 0, y: 0 };
    let score;
    let wall;

    // Load a different baseball image
    const foodImage = new Image();
    foodImage.src = "https://upload.wikimedia.org/wikipedia/commons/0/05/Baseball_-_Cropped.jpg"; // Updated baseball image

    // Set snake color
    const snakeColor = "brown";

    // Game logic
    function initGame() {
        snake = [
            { x: 5, y: 5 },
            { x: 4, y: 5 },
            { x: 3, y: 5 }
        ];
        snake_dir = "RIGHT";
        snake_next_dir = "RIGHT";
        score = 0;
        food = {
            x: Math.floor(Math.random() * (canvas.width / BLOCK)),
            y: Math.floor(Math.random() * (canvas.height / BLOCK))
        };
        snake_speed = 150; // Default speed
        if (speed_setting[0].checked) {
            snake_speed = 200; // Slow
        } else if (speed_setting[1].checked) {
            snake_speed = 150; // Normal
        } else if (speed_setting[2].checked) {
            snake_speed = 100; // Fast
        }
        if (wall_setting[0].checked) {
            wall = true;
        } else {
            wall = false;
        }
        gameLoop();
    }

    function drawBackground() {
        ctx.fillStyle = "green";
        ctx.fillRect(0, 0, canvas.width, canvas.height); // Draw full green background
    }

    function drawSnake() {
        ctx.fillStyle = snakeColor;
        for (let i = 0; i < snake.length; i++) {
            ctx.fillRect(snake[i].x * BLOCK, snake[i].y * BLOCK, BLOCK, BLOCK);
        }
    }

    function drawFood() {
        ctx.drawImage(foodImage, food.x * BLOCK, food.y * BLOCK, BLOCK, BLOCK); // Draw food image
    }

    function gameLoop() {
        drawBackground(); // Draw the green background
        drawSnake(); // Draw snake
        drawFood(); // Draw food
        moveSnake(); // Move snake
        checkCollisions(); // Check for collisions
        ele_score.innerText = score; // Update score
        setTimeout(gameLoop, snake_speed); // Continue game loop
    }

    function moveSnake() {
        let head = { ...snake[0] };
        switch (snake_next_dir) {
            case "UP":
                head.y--;
                break;
            case "DOWN":
                head.y++;
                break;
            case "LEFT":
                head.x--;
                break;
            case "RIGHT":
                head.x++;
                break;
        }

        snake.unshift(head);

        if (head.x === food.x && head.y === food.y) {
            score++;
            food = {
                x: Math.floor(Math.random() * (canvas.width / BLOCK)),
                y: Math.floor(Math.random() * (canvas.height / BLOCK))
            };
        } else {
            snake.pop();
        }

        snake_dir = snake_next_dir;
    }

    function checkCollisions() {
        let head = snake[0];

        // Check for wall collisions
        if (wall && (head.x < 0 || head.x >= canvas.width / BLOCK || head.y < 0 || head.y >= canvas.height / BLOCK)) {
            endGame();
        }

        // Check for self collisions
        for (let i = 1; i < snake.length; i++) {
            if (head.x === snake[i].x && head.y === snake[i].y) {
                endGame();
            }
        }
    }

    function endGame() {
        SCREEN = 1; // Game Over screen
        screen_game_over.style.display = "block";
        screen_menu.style.display = "none";
        screen_setting.style.display = "none";
    }

    // Event Listeners for controls and settings
    document.addEventListener("keydown", (e) => {
        if (e.key === "ArrowUp" && snake_dir !== "DOWN") {
            snake_next_dir = "UP";
        } else if (e.key === "ArrowDown" && snake_dir !== "UP") {
            snake_next_dir = "DOWN";
        } else if (e.key === "ArrowLeft" && snake_dir !== "RIGHT") {
            snake_next_dir = "LEFT";
        } else if (e.key === "ArrowRight" && snake_dir !== "LEFT") {
            snake_next_dir = "RIGHT";
        } else if (e.key === " " && SCREEN === 1) {
            initGame(); // Start new game
            screen_game_over.style.display = "none";
        }
    });

    button_new_game.addEventListener("click", initGame);
    button_new_game1.addEventListener("click", initGame);
    button_new_game2.addEventListener("click", initGame);
})();
</script>
