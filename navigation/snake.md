<script>
    (function () {
        /* Attributes of Game */
        /////////////////////////////////////////////////////////////
        // Canvas & Context
        const canvas = document.getElementById("snake");
        const ctx = canvas.getContext("2d");

        // HTML Game IDs
        const SCREEN_SNAKE = 0;
        const screen_snake = document.getElementById("snake");
        const ele_score = document.getElementById("score_value");
        const speed_setting = document.getElementsByName("speed");
        const wall_setting = document.getElementsByName("wall");

        // HTML Screen IDs (div)
        const SCREEN_MENU = -1, SCREEN_GAME_OVER = 1, SCREEN_SETTING = 2;
        const screen_menu = document.getElementById("menu");
        const screen_game_over = document.getElementById("gameover");
        const screen_setting = document.getElementById("setting");

        // HTML Event IDs (a tags)
        const button_new_game = document.getElementById("new_game");
        const button_new_game1 = document.getElementById("new_game1");
        const button_new_game2 = document.getElementById("new_game2");
        const button_setting_menu = document.getElementById("setting_menu");
        const button_setting_menu1 = document.getElementById("setting_menu1");

        // Game Control
        const BLOCK = 10;   // size of block rendering
        let SCREEN = SCREEN_MENU;
        let snake;
        let snake_dir;
        let snake_next_dir;
        let snake_speed;
        let food = { x: 0, y: 0 };
        let score;
        let wall;

        // Food Image Setup
        const foodImage = new Image();
        foodImage.src = "/chasewebsite/images/360_F_197537431_bL6Gy5AbpxZyVNCzL421DJ1MoHiaq7YH.jpg";
        let foodImageLoaded = false;

        foodImage.onload = function () {
            foodImageLoaded = true;
            console.log("Food image loaded successfully.");
        };

        foodImage.onerror = function () {
            console.error("Failed to load food image. Falling back to rectangle rendering.");
        };

        /* Display Control */
        /////////////////////////////////////////////////////////////
        let showScreen = function (screen_opt) {
            SCREEN = screen_opt;
            switch (screen_opt) {
                case SCREEN_SNAKE:
                    screen_snake.style.display = "block";
                    screen_menu.style.display = "none";
                    screen_setting.style.display = "none";
                    screen_game_over.style.display = "none";
                    break;
                case SCREEN_GAME_OVER:
                    screen_snake.style.display = "block";
                    screen_menu.style.display = "none";
                    screen_setting.style.display = "none";
                    screen_game_over.style.display = "block";
                    break;
                case SCREEN_SETTING:
                    screen_snake.style.display = "none";
                    screen_menu.style.display = "none";
                    screen_setting.style.display = "block";
                    screen_game_over.style.display = "none";
                    break;
            }
        };

        /* Dot for Food or Snake Part */
        /////////////////////////////////////////////////////////////
        let activeDot = function (x, y, isFood = false) {
            if (isFood && foodImageLoaded) {
                // Draw food as an image
                ctx.drawImage(foodImage, x * BLOCK, y * BLOCK, BLOCK, BLOCK);
            } else if (isFood) {
                // Fallback to red rectangle for food
                ctx.fillStyle = "red";
                ctx.fillRect(x * BLOCK, y * BLOCK, BLOCK, BLOCK);
            } else {
                // Draw snake as a brown rectangle
                ctx.fillStyle = "#964B00";
                ctx.fillRect(x * BLOCK, y * BLOCK, BLOCK, BLOCK);
            }
        };

        /* Random Food Placement */
        /////////////////////////////////////////////////////////////
        let addFood = function () {
            food.x = Math.floor(Math.random() * ((canvas.width / BLOCK) - 1));
            food.y = Math.floor(Math.random() * ((canvas.height / BLOCK) - 1));
            for (let i = 0; i < snake.length; i++) {
                if (checkBlock(food.x, food.y, snake[i].x, snake[i].y)) {
                    addFood();
                }
            }
        };

        /* Collision Detection */
        /////////////////////////////////////////////////////////////
        let checkBlock = function (x, y, _x, _y) {
            return (x === _x && y === _y);
        };

        /* Update Score */
        /////////////////////////////////////////////////////////////
        let altScore = function (score_val) {
            ele_score.innerHTML = String(score_val);
        };

        /* Main Loop */
        /////////////////////////////////////////////////////////////
        let mainLoop = function () {
            let _x = snake[0].x;
            let _y = snake[0].y;
            snake_dir = snake_next_dir;

            // Direction 0 - Up, 1 - Right, 2 - Down, 3 - Left
            switch (snake_dir) {
                case 0: _y--; break;
                case 1: _x++; break;
                case 2: _y++; break;
                case 3: _x--; break;
            }

            snake.pop(); // Remove tail
            snake.unshift({ x: _x, y: _y }); // Add new head

            // Wall Collision Check
            if (wall === 1) {
                if (_x < 0 || _x === canvas.width / BLOCK || _y < 0 || _y === canvas.height / BLOCK) {
                    showScreen(SCREEN_GAME_OVER);
                    return;
                }
            } else {
                // Wrap Around
                if (_x < 0) _x += canvas.width / BLOCK;
                if (_x >= canvas.width / BLOCK) _x -= canvas.width / BLOCK;
                if (_y < 0) _y += canvas.height / BLOCK;
                if (_y >= canvas.height / BLOCK) _y -= canvas.height / BLOCK;
            }

            // Self Collision
            for (let i = 1; i < snake.length; i++) {
                if (snake[0].x === snake[i].x && snake[0].y === snake[i].y) {
                    showScreen(SCREEN_GAME_OVER);
                    return;
                }
            }

            // Food Collision
            if (checkBlock(snake[0].x, snake[0].y, food.x, food.y)) {
                snake.push({ x: snake[0].x, y: snake[0].y });
                altScore(++score);
                addFood();
            }

            // Clear Canvas
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Draw Snake
            for (let i = 0; i < snake.length; i++) {
                activeDot(snake[i].x, snake[i].y);
            }

            // Draw Food
            activeDot(food.x, food.y, true);

            setTimeout(mainLoop, snake_speed);
        };

        /* New Game */
        /////////////////////////////////////////////////////////////
        let newGame = function () {
            showScreen(SCREEN_SNAKE);
            screen_snake.focus();

            score = 0;
            altScore(score);

            snake = [{ x: 5, y: 5 }];
            snake_dir = 1;
            snake_next_dir = 1;

            addFood();
            mainLoop();
        };

        /* Initialization */
        /////////////////////////////////////////////////////////////
        window.onload = function () {
            button_new_game.onclick = newGame;
            button_new_game1.onclick = newGame;
            button_new_game2.onclick = newGame;

            setSnakeSpeed(100);
            setWall(1);
        };

        /* Utility Functions */
        /////////////////////////////////////////////////////////////
        let setSnakeSpeed = function (speed) {
            snake_speed = speed;
        };

        let setWall = function (wall_value) {
            wall = wall_value;
            screen_snake.style.borderColor = wall ? "#FFFFFF" : "#606060";
        };
    })();
</script>
