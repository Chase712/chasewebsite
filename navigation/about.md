---
layout: page
title: Fun Game
permalink: /about/
---


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Snake Game</title>
    <style>
        body {
            font-family: 'Courier New', Courier, monospace;
            margin: 0;
            padding: 0;
            background-color: #1a1a1a;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            color: #ffffff;
        }

        #instruction-page, #game-page {
            display: none;
            text-align: center;
        }

        #instruction-page.active, #game-page.active {
            display: block;
        }

        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            background-color: #4caf50;
            color: white;
            border: none;
            border-radius: 5px;
            transition: transform 0.2s, background-color 0.2s;
        }

        button:hover {
            transform: scale(1.1);
            background-color: #45a049;
        }

        #game-area {
            width: 400px;
            height: 400px;
            background: linear-gradient(135deg, #1e3c72, #2a5298);
            position: relative;
            overflow: hidden;
            border: 5px solid #fff;
            box-shadow: 0px 0px 15px 3px rgba(255, 255, 255, 0.5);
        }

        .snake {
            width: 20px;
            height: 20px;
            background-color: #32cd32;
            position: absolute;
            border-radius: 3px;
            box-shadow: 0 0 5px #32cd32;
        }

        .food {
            width: 20px;
            height: 20px;
            background-color: #ff4500;
            position: absolute;
            border-radius: 50%;
            box-shadow: 0 0 5px #ff4500;
        }
    </style>
</head>
<body>

<div id="instruction-page" class="active">
    <h1>Welcome to Snake Game!</h1>
    <p>Your goal is to eat as many glowing food orbs as possible without hitting the walls or yourself.</p>
    <p>Use the <b>W</b>, <b>A</b>, <b>S</b>, <b>D</b> keys to move the snake:</p>
    <ul>
        <li><b>W:</b> Move Up</li>
        <li><b>A:</b> Move Left</li>
        <li><b>S:</b> Move Down</li>
        <li><b>D:</b> Move Right</li>
    </ul>
    <p>Press the "Start Game" button to begin!</p>
    <button onclick="startGame()">Start Game</button>
</div>

<div id="game-page">
    <h1>Score: <span id="score">0</span></h1>
    <div id="game-area"></div>
</div>

<script>
    let score = 0;
    let snake = [{ x: 200, y: 200 }];
    let food = { x: 0, y: 0 };
    let direction = null; // No direction initially
    let gameInterval;

    const instructionPage = document.getElementById('instruction-page');
    const gamePage = document.getElementById('game-page');
    const scoreElement = document.getElementById('score');
    const gameArea = document.getElementById('game-area');

    function startGame() {
        instructionPage.classList.remove('active');
        gamePage.classList.add('active');
        score = 0;
        snake = [{ x: 200, y: 200 }];
        direction = null; // Reset direction
        placeFood();
        updateScore();
        drawGame();
        gameInterval = setInterval(updateGame, 100);
    }

    function updateScore() {
        scoreElement.textContent = score;
    }

    function drawGame() {
        gameArea.innerHTML = '';
        snake.forEach(segment => {
            const snakeElement = document.createElement('div');
            snakeElement.style.left = `${segment.x}px`;
            snakeElement.style.top = `${segment.y}px`;
            snakeElement.classList.add('snake');
            gameArea.appendChild(snakeElement);
        });
        const foodElement = document.createElement('div');
        foodElement.style.left = `${food.x}px`;
        foodElement.style.top = `${food.y}px`;
        foodElement.classList.add('food');
        gameArea.appendChild(foodElement);
    }

    function updateGame() {
        if (!direction) return; // Skip update if no direction

        const head = { x: snake[0].x + direction.x * 20, y: snake[0].y + direction.y * 20 };
        if (head.x < 0 || head.y < 0 || head.x >= 400 || head.y >= 400 || snake.some(segment => segment.x === head.x && segment.y === head.y)) {
            endGame();
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
        drawGame();
    }

    function placeFood() {
        food.x = Math.floor(Math.random() * 20) * 20;
        food.y = Math.floor(Math.random() * 20) * 20;
        if (snake.some(segment => segment.x === food.x && segment.y === food.y)) {
            placeFood();
        }
    }

    function endGame() {
        clearInterval(gameInterval);
        alert(`Game Over! Your final score is: ${score}`);
        gamePage.classList.remove('active');
        instructionPage.classList.add('active');
    }

    document.addEventListener('keydown', e => {
        switch (e.key) {
            case 'w':
            case 'W':
                if (direction?.y !== 1) direction = { x: 0, y: -1 };
                break;
            case 's':
            case 'S':
                if (direction?.y !== -1) direction = { x: 0, y: 1 };
                break;
            case 'a':
            case 'A':
                if (direction?.x !== 1) direction = { x: -1, y: 0 };
                break;
            case 'd':
            case 'D':
                if (direction?.x !== -1) direction = { x: 1, y: 0 };
                break;
        }
    });
</script>

</body>
</html>
