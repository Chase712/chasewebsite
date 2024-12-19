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
        border-color: #C19A6B;
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
        snake_speed = 150;
        if (speed_setting[0].checked) {
            snake_speed = 200;
        } else if (speed_setting[1].checked) {
            snake_speed = 150;
        } else if (speed_setting[2].checked) {
            snake_speed = 100;
        }
        if (wall_setting[0].checked) {
            wall = true;
        } else {
            wall = false;
        }
        SCREEN = 1;
        screen_menu.style.display = "none";
        screen_game_over.style.display = "none";
        gameLoop();
    }

    function drawBackground() {
        ctx.fillStyle = "green";
        ctx.fillRect(0, 0, canvas.width, canvas.height);

        const cornerSize = 20;
        ctx.fillStyle = "white";

        ctx.fillRect(0, 0, cornerSize, cornerSize);
        ctx.fillRect(canvas.width - cornerSize, 0, cornerSize, cornerSize);
        ctx.fillRect(0, canvas.height - cornerSize, cornerSize, cornerSize);
        ctx.fillRect(canvas.width - cornerSize, canvas.height - cornerSize, cornerSize, cornerSize);
    }

    function drawSnake() {
        ctx.fillStyle = "#D2B48C";
        for (let i = 0; i < snake.length; i++) {
            ctx.fillRect(snake[i].x * BLOCK, snake[i].y * BLOCK, BLOCK, BLOCK);
        }
    }

    function drawFood() {
        ctx.fillStyle = "white";
        ctx.beginPath();
        ctx.arc(food.x * BLOCK + BLOCK / 2, food.y * BLOCK + BLOCK / 2, BLOCK / 2, 0, 2 * Math.PI);
        ctx.fill();

        ctx.strokeStyle = "red";
        ctx.lineWidth = 2;

        ctx.beginPath();
        ctx.moveTo(food.x * BLOCK + BLOCK / 4, food.y * BLOCK + BLOCK / 2);
        ctx.lineTo(food.x * BLOCK + 3 * BLOCK / 4, food.y * BLOCK + BLOCK / 2);
        ctx.stroke();

        ctx.beginPath();
        ctx.moveTo(food.x * BLOCK + BLOCK / 2, food.y * BLOCK + BLOCK / 4);
        ctx.lineTo(food.x * BLOCK + BLOCK / 2, food.y * BLOCK + 3 * BLOCK / 4);
        ctx.stroke();
    }

    function updateSnakePosition() {
        let head = { ...snake[0] };

        if (snake_next_dir === "UP") head.y--;
        if (snake_next_dir === "DOWN") head.y++;
        if (snake_next_dir === "LEFT") head.x--;
        if (snake_next_dir === "RIGHT") head.x++;

        snake.unshift(head);

        if (head.x === food.x && head.y === food.y) {
            score++;
            ele_score.innerText = score;
            food = {
                x: Math.floor(Math.random() * (canvas.width / BLOCK)),
                y: Math.floor(Math.random() * (canvas.height / BLOCK))
            };
        } else {
            snake.pop();
        }

        if (wall && (head.x < 0 || head.x >= canvas.width / BLOCK || head.y < 0 || head.y >= canvas.height / BLOCK)) {
            gameOver();
        }

        for (let i = 1; i < snake.length; i++) {
            if (snake[i].x === head.x && snake[i].y === head.y) {
                gameOver();
            }
        }
    }

    function gameOver() {
        SCREEN = 2;
        screen_menu.style.display = "none";
        screen_game_over.style.display = "block";
    }

    function gameLoop() {
        if (SCREEN !== 1) return;

        drawBackground();
        drawSnake();
        drawFood();
        updateSnakePosition();

        setTimeout(gameLoop, snake_speed);
    }

    document.addEventListener("keydown", (e) => {
        if (SCREEN !== 1) return;

        if (e.key === "ArrowUp" && snake_dir !== "DOWN") {
            snake_next_dir = "UP";
        } else if (e.key === "ArrowDown" && snake_dir !== "UP") {
            snake_next_dir = "DOWN";
        } else if (e.key === "ArrowLeft" && snake_dir !== "RIGHT") {
            snake_next_dir = "LEFT";
        } else if (e.key === "ArrowRight" && snake_dir !== "LEFT") {
            snake_next_dir = "RIGHT";
        } else if (e.key === " " && SCREEN === -1) {
            initGame();
        }
    });

    button_new_game.addEventListener("click", initGame);
    button_new_game1.addEventListener("click", initGame);
    button_new_game2.addEventListener("click", initGame);
    button_setting_menu.addEventListener("click", () => {
        screen_menu.style.display = "none";
        screen_setting.style.display = "block";
    });
    button_setting_menu1.addEventListener("click", () => {
        screen_game_over.style.display = "none";
        screen_setting.style.display = "block";
    });
})();
</script>
