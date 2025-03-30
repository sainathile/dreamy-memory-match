<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dreamy Memory Match</title>
    <style>
        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #ffdde1, #ee9ca7);
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            text-align: center;
            color: #fff;
        }
        h1 {
            font-size: 28px;
        }
        .game-board {
            display: grid;
            grid-template-columns: repeat(4, 80px);
            gap: 10px;
            margin-top: 20px;
        }
        .card {
            width: 80px;
            height: 80px;
            background: white;
            color: #ff758c;
            font-size: 24px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 10px;
            cursor: pointer;
            transition: transform 0.4s;
        }
        .flipped {
            background: #ff758c;
            color: white;
            transform: rotateY(180deg);
        }
    </style>
</head>
<body>
    <h1>✨ Dreamy Memory Match ✨</h1>
    <div class="game-board" id="gameBoard"></div>
    <p id="message"></p>
    
    <script>
        const emojis = ['🌸', '💖', '☁️', '✨', '🌿', '🎶', '🌸', '💖', '☁️', '✨', '🌿', '🎶'];
        let shuffled = emojis.sort(() => 0.5 - Math.random());
        let selected = [];
        let matched = [];

        const board = document.getElementById('gameBoard');

        shuffled.forEach((emoji, index) => {
            let card = document.createElement('div');
            card.classList.add('card');
            card.dataset.index = index;
            card.onclick = flipCard;
            board.appendChild(card);
        });

        function flipCard() {
            if (selected.length < 2 && !this.classList.contains('flipped')) {
                this.classList.add('flipped');
                this.textContent = emojis[this.dataset.index];
                selected.push(this);
            }
            if (selected.length === 2) {
                setTimeout(checkMatch, 500);
            }
        }

        function checkMatch() {
            if (selected[0].textContent === selected[1].textContent) {
                matched.push(...selected);
            } else {
                selected.forEach(card => {
                    card.classList.remove('flipped');
                    card.textContent = '';
                });
            }
            selected = [];
            if (matched.length === emojis.length) {
                document.getElementById('message').textContent = '🎉 You matched all pairs! 🎉';
            }
        }
    </script>
</body>
</html>
