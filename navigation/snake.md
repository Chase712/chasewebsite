---
layout: base
title: Snake
permalink: /snake/
---

<style>

    body{
    }
    .wrap{
        margin-left: auto;
        margin-right: auto;
    }

    canvas{
        display: none;
        border-style: solid;
        border-width: 10px;
        border-color: #FFFFFF;
    }
    canvas:focus{
        outline: none;
    }

    /* All screens style */
    #gameover p, #setting p, #menu p{
        font-size: 20px;
    }

    #gameover a, #setting a, #menu a{
        font-size: 30px;
        display: block;
    }

    #gameover a:hover, #setting a:hover, #menu a:hover{
        cursor: pointer;
    }

    #gameover a:hover::before, #setting a:hover::before, #menu a:hover::before{
        content: ">";
        margin-right: 10px;
    }

    #menu{
        display: block;
    }

    #gameover{
        display: none;
    }

    #setting{
        display: none;
    }

    #setting input{
        display:none;
    }

    #setting label{
        cursor: pointer;
    }

    #setting input:checked + label{
        background-color: #FFF;
        color: #000;
    }
</style>

<h2>Snake</h2>
<div class="container">
    <header class="pb-3 mb-4 border-bottom border-primary text-dark">
        <p class="fs-4">Score: <span id="score_value">0</span></p>
    </header>
    <div class="container bg-secondary" style="text-align:center;">
        <!-- Main Menu -->
        <div id="menu" class="py-4 text-light">
            <p>Welcome to Snake, press <span style="background-color: #FFFFFF; color: #000000">space</span> to begin</p>
            <a id="new_game" class="link-alert">new game</a>
            <a id="setting_menu" class="link-alert">settings</a>
        </div>
        <!-- Game Over -->
        <div id="gameover" class="py-4 text-light">
            <p>Game Over, press <span style="background-color: #FFFFFF; color: #000000">space</span> to try again</p>
            <a id="new_game1" class="link-alert">new game</a>
            <a id="setting_menu1" class="link-alert">settings</a>
        </div>
        <!-- Play Screen -->
        <canvas id="snake" class="wrap" width="320" height="320" tabindex="1"></canvas>
        <!-- Settings Screen -->
        <div id="setting" class="py-4 text-light">
            <p>Settings Screen, press <span style="background-color: #FFFFFF; color: #000000">space</span> to go back to playing</p>
            <a id="new_game2" class="link-alert">new game</a>
            <br>
            <p>Speed:
                <input id="speed1" type="radio" name="speed" value="120" checked/>
                <label for="speed1">Slow</label>
                <input id="speed2" type="radio" name="speed" value="75"/>
                <label for="speed2">Normal</label>
                <input id="speed3" type="radio" name="speed" value="35"/>
                <label for="speed3">Fast</label>
            </p>
            <p>Wall:
                <input id="wallon" type="radio" name="wall" value="1" checked/>
                <label for="wallon">On</label>
                <input id="walloff" type="radio" name="wall" value="0"/>
                <label for="walloff">Off</label>
            </p>
        </div>
    </div>
</div>

<script>
    (function(){
        /* Attributes of Game */
        /////////////////////////////////////////////////////////////
        const canvas = document.getElementById("snake");
        const ctx = canvas.getContext("2d");

        const BLOCK = 10;   // Block size
        let SCREEN = 0;
        let snake = [];
        let snake_dir = 1;  // Default direction
        let snake_next_dir = 1;
        let snake_speed = 100;
        let food = {x: 0, y: 0};
        let score = 0;

        // Draw the snake
        let drawSnake = function(){
            ctx.fillStyle = "#8B4513"; // Brown for the snake
            for(let i = 0; i < snake.length; i++){
                ctx.fillRect(snake[i].x * BLOCK, snake[i].y * BLOCK, BLOCK, BLOCK);
            }
        }

        // Draw food (baseball)
        let drawFood = function(){
            ctx.fillStyle = "#FFFFFF"; // White for food
            ctx.beginPath();
            ctx.arc(food.x * BLOCK + BLOCK / 2, food.y * BLOCK + BLOCK / 2, BLOCK / 2, 0, 2 * Math.PI);
            ctx.fill();

            ctx.strokeStyle = "red"; // Red "stitches"
            ctx.beginPath();
            ctx.moveTo(food.x * BLOCK + 2, food.y * BLOCK + 2);
            ctx.lineTo(food.x * BLOCK + BLOCK - 2, food.y * BLOCK + BLOCK - 2);
            ctx.moveTo(food.x * BLOCK + BLOCK - 2, food.y * BLOCK + 2);
            ctx.lineTo(food.x * BLOCK + 2, food.y * BLOCK - 2);
            ctx.stroke();
        }

        // Main Game Loop
        let mainLoop = function(){
            let _x = snake[0].x;
            let _y = snake[0].y;
            snake_dir = snake_next_dir;

            switch(snake_dir){
                case 0: _y--; break; // Up
                case 1: _x++; break; // Right
                case 2: _y++; break; // Down
                case 3: _x--; break; // Left
            }

            snake.pop();
            snake.unshift({x: _x, y: _y});

            // Game over conditions
            if (_x < 0 || _x >= canvas.width / BLOCK || _y < 0 || _y >= canvas.height / BLOCK) {
                return;
            }

            // Check for food
            if (_x === food.x && _y === food.y) {
                snake.push({});
                score++;
                spawnFood();
            }

            // Draw everything
            ctx.fillStyle = "#008000"; // Green background
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            drawSnake();
            drawFood();

            setTimeout(mainLoop, snake_speed);
        }

        let spawnFood = function(){
            food.x = Math.floor(Math.random() * canvas.width / BLOCK);
            food.y = Math.floor(Math.random() * canvas.height / BLOCK);
        }

        let newGame = function(){
            snake = [{x: 5, y: 5}];
            snake_next_dir = 1;
            score = 0;
            spawnFood();
            mainLoop();
        }

        window.onload = function(){
            document.getElementById("new_game").onclick = newGame;
            newGame();
        }
    })();
</script>


