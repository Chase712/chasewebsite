<script>
    (function(){
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
        const SCREEN_MENU = -1, SCREEN_GAME_OVER=1, SCREEN_SETTING=2;
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
        let food = {x: 0, y: 0};
        let score;
        let wall;
        /* Display Control */
        /////////////////////////////////////////////////////////////
        let showScreen = function(screen_opt){
            SCREEN = screen_opt;
            switch(screen_opt){
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
        }
        /* Actions and Events  */
        /////////////////////////////////////////////////////////////
        window.onload = function(){
            button_new_game.onclick = button_new_game1.onclick = button_new_game2.onclick = newGame;
            button_setting_menu.onclick = button_setting_menu1.onclick = function(){showScreen(SCREEN_SETTING);};
            setSnakeSpeed(150);
            for(let i = 0; i < speed_setting.length; i++){
                speed_setting[i].addEventListener("click", function(){
                    setSnakeSpeed(speed_setting[i].value);
                });
            }
            setWall(1);
            for(let i = 0; i < wall_setting.length; i++){
                wall_setting[i].addEventListener("click", function(){
                    setWall(wall_setting[i].value);
                });
            }
            window.addEventListener("keydown", function(evt) {
                if(evt.code === "Space" && SCREEN !== SCREEN_SNAKE)
                    newGame();
            }, true);
        }
        /* Snake Movement and Game Logic */
        /////////////////////////////////////////////////////////////
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
            snake.pop();
            snake.unshift({x: _x, y: _y});
            if(wall === 1){
                if (_x < 0 || _x === canvas.width / BLOCK || _y < 0 || _y === canvas.height / BLOCK){
                    showScreen(SCREEN_GAME_OVER);
                    return;
                }
            } else {
                for(let i = 0; i < snake.length; i++){
                    snake[i].x = (snake[i].x + (canvas.width / BLOCK)) % (canvas.width / BLOCK);
                    snake[i].y = (snake[i].y + (canvas.height / BLOCK)) % (canvas.height / BLOCK);
                }
            }
            for(let i = 1; i < snake.length; i++){
                if (_x === snake[i].x && _y === snake[i].y){
                    showScreen(SCREEN_GAME_OVER);
                    return;
                }
            }
            if(checkBlock(_x, _y, food.x, food.y)){
                snake.push({});
                altScore(++score);
                addFood();
            }
            ctx.fillStyle = "green";
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            for(let i = 0; i < snake.length; i++){
                ctx.fillStyle = "brown";
                ctx.fillRect(snake[i].x * BLOCK, snake[i].y * BLOCK, BLOCK, BLOCK);
            }
            drawFood(food.x, food.y);
            setTimeout(mainLoop, snake_speed);
        }
        /* Food Rendering */
        /////////////////////////////////////////////////////////////
        let drawFood = function(x, y){
            ctx.fillStyle = "white";
            ctx.beginPath();
            ctx.arc(x * BLOCK + BLOCK / 2, y * BLOCK + BLOCK / 2, BLOCK / 2, 0, Math.PI * 2);
            ctx.fill();
            ctx.strokeStyle = "red";
            ctx.lineWidth = 2;
            ctx.beginPath();
            ctx.arc(x * BLOCK + BLOCK / 2, y * BLOCK + BLOCK / 2, BLOCK / 2, 0, Math.PI);
            ctx.stroke();
        }
        let addFood = function(){
            food.x = Math.floor(Math.random() * (canvas.width / BLOCK));
            food.y = Math.floor(Math.random() * (canvas.height / BLOCK));
            for(let i = 0; i < snake.length; i++){
                if(checkBlock(food.x, food.y, snake[i].x, snake[i].y)){
                    addFood();
                }
            }
        }
        let checkBlock = function(x, y, _x, _y){
            return x === _x && y === _y;
        }
        let newGame = function(){
            showScreen(SCREEN_SNAKE);
            screen_snake.focus();
            score = 0;
            altScore(score);
            snake = [{x: 0, y: 15}];
            snake_next_dir = 1;
            addFood();
            canvas.onkeydown = function(evt) { changeDir(evt.keyCode); }
            mainLoop();
        }
        let changeDir = function(key){
            if(key === 37 && snake_dir !== 1) snake_next_dir = 3;
            if(key === 38 && snake_dir !== 2) snake_next_dir = 0;
            if(key === 39 && snake_dir !== 3) snake_next_dir = 1;
            if(key === 40 && snake_dir !== 0) snake_next_dir = 2;
        }
        let altScore = function(score_val){ ele_score.innerHTML = String(score_val); }
        let setSnakeSpeed = function(speed_value){ snake_speed = speed_value; }
        let setWall = function(wall_value){ wall = wall_value; }
    })();
</script>

