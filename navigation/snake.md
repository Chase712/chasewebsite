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

    // Set snake color to light brown
    const snakeColor = "#D2B48C"; // Light brown

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
        SCREEN = 1; // Set screen to playing state
        screen_menu.style.display = "none";
        screen_game_over.style.display = "none";
        gameLoop();
    }

    function drawBackground() {
        ctx.fillStyle = "green";
        ctx.fillRect(0, 0, canvas.width, canvas.height); // Full green background
    }

    function drawSnake() {
        ctx.fillStyle = snakeColor; // Set snake color to light brown
        for (let i = 0; i < snake.length; i++) {
            ctx.fillRect(snake[i].x * BLOCK, snake[i].y * BLOCK, BLOCK, BLOCK);
        }
    }

    function drawFood() {
        // Draw food as a white circle (baseball)
        ctx.fillStyle = "white";
        ctx.beginPath();
        ctx.arc(food.x * BLOCK + BLOCK / 2, food.y * BLOCK + BLOCK / 2, BLOCK / 2, 0, 2 * Math.PI);
        ctx.fill();
        
        // Draw the red laces (stitching) of the baseball
        ctx.strokeStyle = "red";
        ctx.lineWidth = 2;

        // Left laces (curved stitching on one side of the ball)
        ctx.beginPath();
        ctx.arc(food.x * BLOCK + BLOCK / 2, food.y * BLOCK + BLOCK / 2, BLOCK / 2 - 3, Math.PI, 2 * Math.PI, false);
        ctx.stroke();

        // Right laces (curved stitching on the opposite side)
        ctx.beginPath();
        ctx.arc(food.x * BLOCK + BLOCK / 2, food.y * BLOCK + BLOCK / 2, BLOCK / 2 - 3, 0, Math.PI, true);
        ctx.stroke();

        // Draw small stitches along the curves to resemble baseball laces
        // Left side
        ctx.beginPath();
        ctx.moveTo(food.x * BLOCK + BLOCK / 2 - BLOCK / 4, food.y * BLOCK + BLOCK / 2 - BLOCK / 6);
        ctx.lineTo(food.x * BLOCK + BLOCK / 2 - BLOCK / 4, food.y * BLOCK + BLOCK / 2 - BLOCK / 4);
        ctx.stroke();

        ctx.beginPath();
        ctx.moveTo(food.x * BLOCK + BLOCK / 2 - BLOCK / 4, food.y * BLOCK + BLOCK / 2 + BLOCK / 6);
        ctx.lineTo(food.x * BLOCK + BLOCK / 2 - BLOCK / 4, food.y * BLOCK + BLOCK / 2 + BLOCK / 4);
        ctx.stroke();

        // Right side
        ctx.beginPath();
        ctx.moveTo(food.x * BLOCK + BLOCK / 2 + BLOCK / 4, food.y * BLOCK + BLOCK / 2 - BLOCK / 6);
        ctx.lineTo(food.x * BLOCK + BLOCK / 2 + BLOCK / 4, food.y * BLOCK + BLOCK / 2 - BLOCK / 4);
        ctx.stroke();

        ctx.beginPath();
        ctx.moveTo(food.x * BLOCK + BLOCK / 2 + BLOCK / 4, food.y * BLOCK + BLOCK / 2 + BLOCK / 6);
        ctx.lineTo(food.x * BLOCK + BLOCK / 2 + BLOCK / 4, food.y * BLOCK + BLOCK / 2 + BLOCK / 4);
        ctx.stroke();
    }

    function updateSnake() {
        const head = { ...snake[0] };

        // Update snake head direction
        if (snake_dir === "UP") head.y--;
        else if (snake_dir === "DOWN") head.y++;
        else if (snake_dir === "LEFT") head.x--;
        else if (snake_dir === "RIGHT") head.x++;

        // Check for wall collisions
        if (wall && (head.x < 0 || head.x >= canvas.width / BLOCK || head.y < 0 || head.y >= canvas.height / BLOCK)) {
            endGame();
            return;
        }

        // Check for self-collision
        for (let i = 0; i < snake.length; i++) {
            if (head.x === snake[i].x && head.y === snake[i].y) {
                endGame();
                return;
            }
        }

        snake.unshift(head); // Add the new head to the snake

        // Check if snake ate the food
        if (head.x === food.x && head.y === food.y) {
            score++;
            ele_score.innerHTML = score;
            food = { x: Math.floor(Math.random() * (canvas.width / BLOCK)), y: Math.floor(Math.random() * (canvas.height / BLOCK)) };
        } else {
            snake.pop(); // Remove the tail of the snake if it didn't eat food
        }
    }

    function endGame() {
        SCREEN = 0; // Game over state
        screen_game_over.style.display = "block";
    }

    function gameLoop() {
        if (SCREEN === 1) {
            drawBackground();
            drawSnake();
            drawFood();
            updateSnake();
            setTimeout(gameLoop, snake_speed); // Repeat the game loop based on the speed setting
        }
    }

    function changeDirection(event) {
        if (event.keyCode === 37 && snake_dir !== "RIGHT") {
            snake_next_dir = "LEFT";
        } else if (event.keyCode === 38 && snake_dir !== "DOWN") {
            snake_next_dir = "UP";
        } else if (event.keyCode === 39 && snake_dir !== "LEFT") {
            snake_next_dir = "RIGHT";
        } else if (event.keyCode === 40 && snake_dir !== "UP") {
            snake_next_dir = "DOWN";
        }
    }

    // Handling user input and transitions
    document.addEventListener("keydown", function (e) {
        if (SCREEN === 1) {
            changeDirection(e);
        } else if (e.keyCode === 32) {
            if (SCREEN === -1) {
                initGame();
            } else if (SCREEN === 0) {
                initGame();
            }
        }
    });

    // Start a new game when 'New Game' button is clicked
    button_new_game.addEventListener("click", initGame);
    button_new_game1.addEventListener("click", initGame);
    button_new_game2.addEventListener("click", initGame);
    button_setting_menu.addEventListener("click", function () {
        SCREEN = 2;
        screen_setting.style.display = "block";
    });

    button_setting_menu1.addEventListener("click", function () {
        SCREEN = 2;
        screen_setting.style.display = "block";
    });

    // Set initial menu
    screen_menu.style.display = "block";
})();
</script>
