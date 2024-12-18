---
layout: base
title: Snake
permalink: /snake/
---

<style>
    body {
        margin: 0;
        font-family: Arial, sans-serif;
        background-color: #282c34;
        color: white;
        text-align: center;
    }
    .wrap {
        margin: 0 auto;
    }
    canvas {
        display: none;
        border: 10px solid #FFFFFF;
    }
    canvas:focus {
        outline: none;
    }
    /* Screen styles */
    #gameover p, #setting p, #menu p {
        font-size: 20px;
    }
    #gameover a, #setting a, #menu a {
        font-size: 30px;
        display: block;
        text-decoration: none;
        color: white;
    }
    #gameover a:hover, #setting a:hover, #menu a:hover {
        cursor: pointer;
    }
    #gameover a:hover::before, #setting a:hover::before, #menu a:hover::before {
        content: ">";
        margin-right: 10px;
    }
    #menu {
        display: block;
    }
    #gameover, #setting {
        display: none;
    }
    #setting input {
        display: none;
    }
    #setting label {
        cursor: pointer;
        padding: 5px 10px;
        border: 1px solid white;
        margin: 5px;
    }
    #setting input:checked + label {
        background-color: #FFF;
        color: #000;
    }
</style>

<h2>Snake</h2>
<div class="container">
    <header class="pb-3 mb-4 border-bottom border-primary text-dark">
        <p class="fs-4">Score: <span id="score_value">0</span></p>
    </header>
    <div class="container bg-secondary" style="text-align: center;">
        <!-- Main Menu -->
        <div id="menu" class="py-4 text-light">
            <p>Welcome to Snake, press <span style="background-color: #FFFFFF; color: #000000">space</span> to begin</p>
            <a id="new_game" href="#" class="link-alert">New Game</a>
            <a id="setting_menu" href="#" class="link-alert">Settings</a>
        </div>
        <!-- Game Over -->
        <div id="gameover" class="py-4 text-light">
            <p>Game Over, press <span style="background-color: #FFFFFF; color: #000000">space</span> to try again</p>
            <a id="new_game1" href="#" class="link-alert">New Game</a>
            <a id="setting_menu1" href="#" class="link-alert">Settings</a>
        </div>
        <!-- Play Screen -->
        <canvas id="snake" class="wrap" width="320" height="320" tabindex="1"></canvas>
        <!-- Settings Screen -->
        <div id="setting" class="py-4 text-light">
            <p>Settings Screen, press <span style="background-color: #FFFFFF; color: #000000">space</span> to go back to playing</p>
            <a id="new_game2" href="#" class="link-alert">New Game</a>
            <br>
            <p>Speed:</p>
            <input id="speed1" type="radio" name="speed" value="120" checked />
            <label for="speed1">Slow</label>
            <input id="speed2" type="radio" name="speed" value="75" />
            <label for="speed2">Normal</label>
            <input id="speed3" type="radio" name="speed" value="35" />
            <label for="speed3">Fast</label>
            <p>Wall:</p>
            <input id="wallon" type="radio" name="wall" value="1" checked />
            <label for="wallon">On</label>
            <input id="walloff" type="radio" name="wall" value="0" />
            <label for="walloff">Off</label>
        </div>
    </div>
</div>

<script>
    (function () {
        const canvas = document.getElementById("snake");
        const ctx = canvas.getContext("2d");

        // Screens
        const SCREEN_MENU = -1, SCREEN_SNAKE = 0, SCREEN_GAME_OVER = 1, SCREEN_SETTING = 2;
        const screen_snake = document.getElementById("snake");
        const screen_menu = document.getElementById("menu");
        const screen_game_over = document.getElementById("gameover");
        const screen_setting = document.getElementById("setting");

        const button_new_game = document.getElementById("new_game");
        const button_new_game1 = document.getElementById("new_game1");
        const button_new_game2 = document.getElementById("new_game2");
        const button_setting_menu = document.getElementById("setting_menu");
        const button_setting_menu1 = document.getElementById("setting_menu1");

        const speed_setting = document.getElementsByName("speed");
        const wall_setting = document.getElementsByName("wall");

        let SCREEN = SCREEN_MENU;
        let snake, snake_dir, snake_next_dir, snake_speed, food = { x: 0, y: 0 }, score, wall;

        const showScreen = (screen) => {
            SCREEN = screen;
            screen_menu.style.display = screen === SCREEN_MENU ? "block" : "none";
            screen_snake.style.display = screen === SCREEN_SNAKE ? "block" : "none";
            screen_game_over.style.display = screen === SCREEN_GAME_OVER ? "block" : "none";
            screen_setting.style.display = screen === SCREEN_SETTING ? "block" : "none";
        };

        const newGame = () => {
            showScreen(SCREEN_SNAKE);
            screen_snake.focus();
            score = 0;
            document.getElementById("score_value").textContent = score;
            snake = [{ x: 0, y: 15 }];
            snake_next_dir = 1;
            addFood();
            mainLoop();
        };

        const mainLoop = () => {
            // Update snake position
            // Game logic here...
            setTimeout(mainLoop, snake_speed);
        };

        const addFood = () => {
            food.x = Math.floor(Math.random() * (canvas.width / 10 - 1));
            food.y = Math.floor(Math.random() * (canvas.height / 10 - 1));
        };

        const setSnakeSpeed = (speed) => { snake_speed = speed; };
        const setWall = (value) => { wall = value; };

        window.onload = () => {
            button_new_game.onclick = button_new_game1.onclick = button_new_game2.onclick = (event) => {
                event.preventDefault();
                newGame();
            };
            button_setting_menu.onclick = button_setting_menu1.onclick = (event) => {
                event.preventDefault();
                showScreen(SCREEN_SETTING);
            };

            speed_setting.forEach((radio) => radio.onclick = () => setSnakeSpeed(radio.value));
            wall_setting.forEach((radio) => radio.onclick = () => setWall(radio.value));

            window.addEventListener("keydown", (evt) => {
                if (evt.code === "Space" && SCREEN !== SCREEN_SNAKE) newGame();
            });
        };
    })();
</script>
