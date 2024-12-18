<script>
    (function () {
        const canvas = document.getElementById("snake");
        const ctx = canvas.getContext("2d");
        const scoreDisplay = document.getElementById("score_value");
        const screens = {
            menu: document.getElementById("menu"),
            gameover: document.getElementById("gameover"),
            setting: document.getElementById("setting"),
        };

        const buttons = {
            newGame: document.getElementById("new_game"),
            newGame1: document.getElementById("new_game1"),
            newGame2: document.getElementById("new_game2"),
            settingsMenu: document.getElementById("setting_menu"),
            settingsMenu1: document.getElementById("setting_menu1"),
        };

        let snake = [];
        let food = { x: 0, y: 0 };
        let direction = 1; // 0 - Up, 1 - Right, 2 - Down, 3 - Left
        let nextDirection = 1;
        let score = 0;
        let speed = 120;
        let wall = 1;

        function showScreen(screenName) {
            Object.values(screens).forEach((screen) => (screen.style.display = "none"));
            screens[screenName].style.display = "block";
        }

        function startGame() {
            snake = [{ x: 15, y: 15 }];
            score = 0;
            updateScore();
            direction = 1;
            nextDirection = 1;
            placeFood();
            showScreen("menu");
            mainLoop();
        }

        function updateScore() {
            scoreDisplay.textContent = score;
        }

        function placeFood() {
            food.x = Math.floor(Math.random() * (canvas.width / 10));
            food.y = Math.floor(Math.random() * (canvas.height / 10));
        }

        function mainLoop() {
            ctx.fillStyle = "black"; // Background color
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            ctx.fillStyle = "brown"; // Snake color
            snake.forEach((segment) => {
                ctx.fillRect(segment.x * 10, segment.y * 10, 10, 10);
            });

            ctx.fillStyle = "red";
            ctx.fillRect(food.x * 10, food.y * 10, 10, 10);

            const head = { ...snake[0] };
            switch (direction) {
                case 0:
                    head.y--;
                    break;
                case 1:
                    head.x++;
                    break;
                case 2:
                    head.y++;
                    break;
                case 3:
                    head.x--;
                    break;
            }

            if (wall === 1 && (head.x < 0 || head.x >= 32 || head.y < 0 || head.y >= 32)) {
                showScreen("gameover");
                return;
            }

            if (wall === 0) {
                if (head.x < 0) head.x = 31;
                if (head.x >= 32) head.x = 0;
                if (head.y < 0) head.y = 31;
                if (head.y >= 32) head.y = 0;
            }

            if (snake.some((segment) => segment.x === head.x && segment.y === head.y)) {
                showScreen("gameover");
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

            setTimeout(mainLoop, speed);
        }

        buttons.newGame.addEventListener("click", startGame);
        buttons.newGame1.addEventListener("click", startGame);
        buttons.newGame2.addEventListener("click", startGame);

        buttons.settingsMenu.addEventListener("click", () => showScreen("setting"));
        buttons.settingsMenu1.addEventListener("click", () => showScreen("setting"));

        document.getElementsByName("speed").forEach((input) => {
            input.addEventListener("change", () => {
                speed = parseInt(input.value);
            });
        });

        document.getElementsByName("wall").forEach((input) => {
            input.addEventListener("change", () => {
                wall = parseInt(input.value);
            });
        });

        document.addEventListener("keydown", (event) => {
            if (event.code === "Space" && screens.menu.style.display === "block") {
                startGame();
            }

            const keyDirections = {
                ArrowUp: 0,
                ArrowRight: 1,
                ArrowDown: 2,
                ArrowLeft: 3,
            };

            if (keyDirections[event.key] !== undefined && Math.abs(direction - keyDirections[event.key]) !== 2) {
                nextDirection = keyDirections[event.key];
            }
        });

        startGame();
    })();
</script>
