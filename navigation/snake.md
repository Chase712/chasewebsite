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
    let food = [];
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
        food = [
            { x: Math.floor(Math.random() * (canvas.width / BLOCK)), y: Math.floor(Math.random() * (canvas.height / BLOCK)) },
            { x: Math.floor(Math.random() * (canvas.width / BLOCK)), y: Math.floor(Math.random() * (canvas.height / BLOCK)) }
        ];
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
        food.forEach((item) => {
            ctx.fillStyle = "white";
            ctx.beginPath();
            ctx.arc(item.x * BLOCK + BLOCK / 2, item.y * BLOCK + BLOCK / 2, BLOCK / 2, 0, 2 * Math.PI);
            ctx.fill();
        });
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

        // Check if snake ate any food
        for (let i = 0; i < food.length; i++) {
            if (head.x === food[i].x && head.y === food[i].y) {
                score++;
                ele_score.innerHTML = score;
                food[i] = { x: Math.floor(Math.random() * (canvas.width / BLOCK)), y: Math.floor(Math.random() * (canvas.height / BLOCK)) };
            }
        }

        // If no food eaten, remove the tail of the snake
        snake.pop();
    }

    function endGame() {
        SCREEN = 0; // Game over state
        screen_game_over.style.display = "block";
    }

    function gameLoop() {
        if (SCREEN === 1) {
            // Update direction only when snake_dir and snake_next_dir are different
            if (snake_dir !== snake_next_dir) {
                snake_dir = snake_next_dir;
            }

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
