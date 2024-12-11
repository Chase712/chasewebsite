---
layout: base
title: Student Home 
description: Home Page
hide: true
---

# Some things about me







_______________________________________________________________________________
I have two brothers one older and one younger.



<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Popup Button</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 50px;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            background-color: red;
            color: white;
            border: none;
            border-radius: 5px;
        }
        button:hover {
            background-color: darkred;
        }
    </style>
</head>
<body>

    <button onclick="showPopup()">Click Me</button>

    <script>
        function showPopup() {
            alert("My brothers' names are Spencer and Jaden");
        }
    </script>

</body>
</html>



_______________________________________________________________________________

<img src="images/three-happy-cartoon-boys-who-support-each-other-vector-9170265.jpg" alt="Description"
style="width:400px; height:auto;">








_______________________________________________________________________________
 



I was born on August 9th


_______________________________________________________________________________


<img src="images/birthday-cake-decorated-with-colorful-sprinkles-and-royalty-free-image-1653509348.jpg" alt="Description"
style="width:400px; height:auto;">


_______________________________________________________________________________


My favorite food is tacos.

_______________________________________________________________________________


<img src="images/iStock-960337396-3beef-barbacoa-tacos-e1695391119564-500x500.jpg" alt="Description"
style="width:400px; height:auto;">

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Snake Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f0f0f0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
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
        }

        #game-area {
            width: 400px;
            height: 400px;
            background-color: #000;
            position: relative;
            overflow: hidden;
        }

        .snake {
            width: 20px;
            height: 20px;
            background-color: green;
            position: absolute;
        }

        .food {
            width: 20px;
            height: 20px;
            background-color: red;
            position: absolute;
        }
    </style>
</head>
<body>

<div id="instruction-page" class="active">
    <h1>Welcome to Snake Game!</h1>
    <p>Your goal is to eat as many red food blocks as possible without hitting the walls or yourself. Use arrow keys to control the snake.</p>
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
    let direction = { x: 20, y: 0 }; // Start moving to the right by default
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
        direction = { x: 20, y: 0 }; // Reset direction
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
        const head = { x: snake[0].x + direction.x, y: snake[0].y + direction.y };
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
            case 'ArrowUp':
                if (direction.y === 0) direction = { x: 0, y: -20 };
                break;
            case 'ArrowDown':
                if (direction.y === 0) direction = { x: 0, y: 20 };
                break;
            case 'ArrowLeft':
                if (direction.x === 0) direction = { x: -20, y: 0 };
                break;
            case 'ArrowRight':
                if (direction.x === 0) direction = { x: 20, y: 0 };
                break;
        }
    });
</script>

</body>
</html>