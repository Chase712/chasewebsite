<script>
    (function(){
        /* Attributes of Game */
        const canvas = document.getElementById("snake");
        const ctx = canvas.getContext("2d");
        const BLOCK = 10;   // size of block rendering
        let snake;
        let snake_dir;
        let snake_next_dir;
        let snake_speed;
        let food = {x: 0, y: 0};
        let score;
        let wall;

        const baseballImage = new Image();
        baseballImage.src = 'https://upload.wikimedia.org/wikipedia/commons/a/a1/Baseball_%28crop%29.png'; // Baseball image URL

        /* Display Control */
        let showScreen = function(screen_opt){
            const screen_snake = document.getElementById("snake");
            const screen_menu = document.getElementById("menu");
            const screen_game_over = document.getElementById("gameover");
            const screen_setting = document.getElementById("setting");
            switch(screen_opt){
                case 0:
                    screen_snake.style.display = "block";
                    screen_menu.style.display = "none";
                    screen_setting.style.display = "none";
                    screen_game_over.style.display = "none";
                    break;
                case 1:
                    screen_snake.style.display = "block";
                    screen_menu.style.display = "none";
                    screen_setting.style.display = "none";
                    screen_game_over.style.display = "block";
                    break;
                case 2:
                    screen_snake.style.display = "none";
                    screen_menu.style.display = "none";
                    screen_setting.style.display = "block";
                    screen_game_over.style.display = "none";
                    break;
            }
        }

        /* Main Game Loop */
        let mainLoop = function(){
            let _x = snake[0].x;
            let _y = snake[0].y;
            snake_dir = snake_next_dir;
            switch(snake_dir){
                case 0: _y--; break;
                case 1: _x++; break;
                case 2: _y++; break;
                case 3: _x--; break;
            }
            snake.pop(); // remove tail
            snake.unshift({x: _x, y: _y}); // add new head
            // Wall Checker
            if (wall === 1) {
                if (_x < 0 || _x >= canvas.width / BLOCK || _y < 0 || _y >= canvas.height / BLOCK) {
                    showScreen(1); // Game over
                    return;
                }
            } else {
                if (_x < 0) _x = canvas.width / BLOCK - 1;
                if (_x >= canvas.width / BLOCK) _x = 0;
                if (_y < 0) _y = canvas.height / BLOCK - 1;
                if (_y >= canvas.height / BLOCK) _y = 0;
            }

            for (let i = 1; i < snake.length; i++) {
                if (_x === snake[i].x && _y === snake[i].y) {
                    showScreen(1); // Game over
                    return;
                }
            }

            if (checkBlock(_x, _y, food.x, food.y)) {
                snake.push({x: _x, y: _y});
                score++;
                addFood();
            }

            // Draw background
            ctx.fillStyle = "green";
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            // Draw snake
            ctx.fillStyle = "brown";
            for (let i = 0; i < snake.length; i++) {
                ctx.fillRect(snake[i].x * BLOCK, snake[i].y * BLOCK, BLOCK, BLOCK);
            }

            // Draw food (baseball)
            ctx.drawImage(baseballImage, food.x * BLOCK, food.y * BLOCK, BLOCK, BLOCK);

            setTimeout(mainLoop, snake_speed);
        }

        /* Random food placement */
        let addFood = function(){
            food.x = Math.floor(Math.random() * (canvas.width / BLOCK));
            food.y = Math.floor(Math.random() * (canvas.height / BLOCK));
        }

        /* Check collision */
        let checkBlock = function(x, y, _x, _y){
            return (x === _x && y === _y);
        }

        /* New Game setup */
        let newGame = function(){
            score = 0;
            snake = [{x: 5, y: 5}];
            snake_next_dir = 1;
            addFood();
            mainLoop();
        }

        /* Event Listener */
        window.onload = function(){
            newGame();
        }
    })();
</script>


