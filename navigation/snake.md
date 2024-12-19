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

    function drawBases() {
        // Increase base size and spread them out to form a pattern of 4 dots
        const baseSize = 10;
        const baseColor = "white";

        // Spread out the bases in a diamond pattern around the center
        const centerX = canvas.width / 2;
        const centerY = canvas.height / 2;
        const offset = 50; // Distance between each base

        const bases = [
            { x: centerX - offset, y: centerY - offset },  // Home plate (top-left)
            { x: centerX + offset, y: centerY - offset },  // First base (top-right)
            { x: centerX + offset, y: centerY + offset },  // Second base (bottom-right)
            { x: centerX - offset, y: centerY + offset },  // Third base (bottom-left)
        ];

        // Draw the bases as large circles
        ctx.fillStyle = baseColor;
        bases.forEach(base => {
            ctx.beginPath();
            ctx.arc(base.x, base.y, baseSize, 0, 2 * Math.PI); // Large circles as bases
            ctx.fill();
        });
    }

    function drawSnake() {
        ctx.fillStyle = snakeColor; // Set snake color to light brown
        for (let i = 0; i < snake.length; i++) {
            ctx.fillRect(snake[i].x * BLOCK, snake[i].y * BLOCK, BLOCK, BLOCK);
        }
    }

    function drawFood() {
        // Draw food as a white circle with red stitches
        ctx.fillStyle = "white";
        ctx.beginPath();
        ctx.arc(food.x * BLOCK + BLOCK / 2, food.y * BLOCK + BLOCK / 2, BLOCK / 2, 0, 2 * Math.PI);
        ctx.fill();
        
        // Draw the red stitches (lines) of the baseball
        ctx.strokeStyle = "red";
        ctx.lineWidth = 2;
        
        // Drawing two lines crossing to simulate the stitches of a baseball
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

        // Update head position based on direction
        if (snake_next_dir === "UP") head.y--;
        if (snake_next_dir === "DOWN") head.y++;
        if (snake_next_dir === "LEFT") head.x--;
        if (snake_next_dir === "RIGHT") head.x++;

        snake.unshift(head); // Add the new head

        // If snake eats food, increase score and spawn new food
        if (head.x === food.x && head.y === food.y) {
            score++;
            ele_score.innerText = score;
            food = {
                x: Math.floor(Math.random() * (canvas.width / BLOCK)),
                y: Math.floor(Math.random() * (canvas.height / BLOCK))
            };
        } else {
            snake.pop(); // Remove the last part of the snake
        }

        // Wall collision check (if enabled)
        if (wall) {
            if (head.x < 0 || head.x >= canvas.width / BLOCK || head.y < 0 || head.y >= canvas.height / BLOCK) {
                gameOver();
            }
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
        screen_game_over.style.display = "block";
    }

    function gameLoop() {
        if (SCREEN !== 1) return;

        // Game screen logic
        drawBackground();
        drawBases(); // Draw bigger and spread out bases
        drawSnake();
        drawFood();
        updateSnakePosition();

        setTimeout(gameLoop, snake_speed);
    }

    // Event listeners for controls
    window.addEventListener("keydown", (e) => {
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

    // Game start buttons
    button_new_game.addEventListener("click", initGame);
    button_new_game1.addEventListener("click", initGame);
    button_new_game2.addEventListener("click", initGame);

    button_setting_menu.addEventListener("click", () => {
        screen_menu.style.display = "none";
        screen_setting.style.display = "block";
    });
})();
</script>
