<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Snake Game</title>
    <style>
        body {
            margin: 0;
            background-color: #008000; /* Green background */
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            font-family: Arial, sans-serif;
        }

        canvas {
            display: block;
            border: 5px solid white;
            background-color: #008000; /* Green background */
        }

        #score {
            position: absolute;
            top: 10px;
            left: 10px;
            font-size: 20px;
            color: white;
        }
    </style>
</head>
<body>
    <div id="score">Score: 0</div>
    <canvas id="gameCanvas" width="400" height="400"></canvas>

    <script>
        const canvas = document.getElementById("gameCanvas");
        const ctx = canvas.getContext("2d");

        const BLOCK_SIZE = 20;
        const canvasWidth = canvas.width / BLOCK_SIZE;
        const canvasHeight = canvas.height / BLOCK_SIZE;

        let snake = [{ x: 5, y: 5 }];
        let direction = { x: 1, y: 0 };
        let food = spawnFood();
        let score = 0;

        function drawSnake() {
            ctx.fillStyle = "#8B4513"; // Brown snake
            snake.forEach(block => {
                ctx.fillRect(block.x * BLOCK_SIZE, block.y * BLOCK_SIZE, BLOCK_SIZE, BLOCK_SIZE);
            });
        }

        function drawFood() {
            const { x, y } = food;
            ctx.fillStyle = "#FFFFFF"; // White food
            ctx.beginPath();
            ctx.arc(
                x * BLOCK_SIZE + BLOCK_SIZE / 2,
                y * BLOCK_SIZE + BLOCK_SIZE / 2,
                BLOCK_SIZE / 2,
                0,
                Math.PI * 2
            );
            ctx.fill();

            ctx.strokeStyle = "red"; // Red stitching
            ctx.beginPath();
            ctx.moveTo(x * BLOCK_SIZE + 5, y * BLOCK_SIZE + 5);
            ctx.lineTo(x * BLOCK_SIZE + 15, y * BLOCK_SIZE + 15);
            ctx.moveTo(x * BLOCK_SIZE + 15, y * BLOCK_SIZE + 5);
            ctx.lineTo(x * BLOCK_SIZE + 5, y * BLOCK_SIZE + 15);
            ctx.stroke();
        }

        function updateSnake() {
            const head = { x: snake[0].x + direction.x, y: snake[0].y + direction.y };

            // Check for wall collision
            if (head.x < 0 || head.x >= canvasWidth || head.y < 0 || head.y >= canvasHeight) {
                resetGame();
                return;
            }

            // Check for self-collision
            if (snake.some(block => block.x === head.x && block.y === head.y)) {
                resetGame();
                return;
            }

            snake.unshift(head);

            // Check for food collision
            if (head.x === food.x && head.y === food.y) {
                score++;
                document.getElementById("score").innerText = `Score: ${score}`;
                food = spawnFood();
            } else {
                snake.pop();
            }
        }

        function spawnFood() {
            return {
                x: Math.floor(Math.random() * canvasWidth),
                y: Math.floor(Math.random() * canvasHeight)
            };
        }

        function resetGame() {
            snake = [{ x: 5, y: 5 }];
            direction = { x: 1, y: 0 };
            food = spawnFood();
            score = 0;
            document.getElementById("score").innerText = "Score: 0";
        }

        function gameLoop() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            drawFood();
            drawSnake();
            updateSnake();
        }

        function changeDirection(event) {
            switch (event.key) {
                case "ArrowUp":
                    if (direction.y === 0) direction = { x: 0, y: -1 };
                    break;
                case "ArrowDown":
                    if (direction.y === 0) direction = { x: 0, y: 1 };
                    break;
                case "ArrowLeft":
                    if (direction.x === 0) direction = { x: -1, y: 0 };
                    break;
                case "ArrowRight":
                    if (direction.x === 0) direction = { x: 1, y: 0 };
                    break;
            }
        }

        document.addEventListener("keydown", changeDirection);

        setInterval(gameLoop, 100);
    </script>
</body>
</html>
