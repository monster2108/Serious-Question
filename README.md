<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Serious Question</title>
    <meta property="og:title" content="Serious Question">
    <meta property="og:description" content="I have something important to ask you...">
    <meta name="description" content="I have something important to ask you...">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #ffeef8 0%, #ffe0f0 100%);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        .container {
            background: white;
            padding: 60px 40px;
            border-radius: 30px;
            box-shadow: 0 20px 60px rgba(255, 105, 180, 0.3);
            text-align: center;
            max-width: 500px;
            width: 100%;
            position: relative;
        }

        h1 {
            color: #ff1493;
            font-size: 2.5em;
            margin-bottom: 40px;
            text-shadow: 2px 2px 4px rgba(255, 105, 180, 0.2);
        }

        .buttons-container {
            display: flex;
            gap: 20px;
            justify-content: center;
            margin-bottom: 30px;
            position: relative;
            min-height: 120px;
            align-items: center;
        }

        button {
            padding: 15px 40px;
            font-size: 1.2em;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            transition: transform 0.2s, box-shadow 0.2s;
        }

        #yesBtn {
            background: linear-gradient(135deg, #ff1493 0%, #ff69b4 100%);
            color: white;
        }

        #yesBtn:hover {
            transform: scale(1.1);
            box-shadow: 0 10px 30px rgba(255, 20, 147, 0.4);
        }

        #noBtn {
            background: linear-gradient(135deg, #ddd 0%, #bbb 100%);
            color: #666;
            position: absolute;
            transition: all 0.3s ease;
        }

        .subtitle {
            color: #ff69b4;
            font-size: 1.1em;
            font-style: italic;
            margin-top: 20px;
        }

        .celebration {
            display: none;
        }

        .celebration.show {
            display: block;
            animation: fadeIn 0.5s;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: scale(0.8); }
            to { opacity: 1; transform: scale(1); }
        }

        .celebration h2 {
            color: #ff1493;
            font-size: 2em;
            margin-bottom: 20px;
        }

        .celebration img {
            max-width: 100%;
            border-radius: 20px;
            margin-top: 20px;
        }

        .hearts {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            overflow: hidden;
            z-index: 1000;
        }

        .heart {
            position: absolute;
            font-size: 30px;
            animation: float 4s ease-in-out infinite;
            opacity: 0;
        }

        @keyframes float {
            0% {
                transform: translateY(100vh) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(-100px) rotate(360deg);
                opacity: 0;
            }
        }
    </style>
</head>
<body>
    <div class="hearts" id="hearts"></div>
    
    <div class="container">
        <div id="question">
            <h1>Paula, would you be my Valentine? 💕</h1>
            <div class="buttons-container">
                <button id="yesBtn" onclick="handleYes()">Yes</button>
                <button id="noBtn" onmouseover="moveButton()" onclick="moveButton()">No</button>
            </div>
            <p class="subtitle">No seems very shy</p>
        </div>

        <div id="celebration" class="celebration">
            <h2>Yay! 🎉💕</h2>
            <p style="font-size: 1.3em; color: #ff69b4; margin: 20px 0;">You've made me the happiest!</p>
            <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExbTBkdmR6Y3RqZnJhcnl6dHN5Yzl6N2x6NjZxMzZtdGNhZmtlZ2JkcSZlcD12MV9naWZzX3NlYXJjaCZjdD1n/MDJ9IbxxvDUQM/giphy.gif" alt="Celebration" onerror="this.src='https://media.giphy.com/media/UVk5yzljef0kGiayL1/giphy.gif'">
        </div>
    </div>

    <script>
        function moveButton() {
            const noBtn = document.getElementById('noBtn');
            const container = document.querySelector('.buttons-container');
            const containerRect = container.getBoundingClientRect();
            
            // Get random position within container bounds
            const maxX = containerRect.width - noBtn.offsetWidth - 20;
            const maxY = containerRect.height - noBtn.offsetHeight - 20;
            
            const randomX = Math.random() * maxX;
            const randomY = Math.random() * maxY;
            
            noBtn.style.left = randomX + 'px';
            noBtn.style.top = randomY + 'px';
        }

        function handleYes() {
            document.getElementById('question').style.display = 'none';
            document.getElementById('celebration').classList.add('show');
            createHearts();
        }

        function createHearts() {
            const heartsContainer = document.getElementById('hearts');
            const heartSymbols = ['💕', '💖', '💗', '💓', '💘', '❤️'];
            
            for (let i = 0; i < 30; i++) {
                setTimeout(() => {
                    const heart = document.createElement('div');
                    heart.className = 'heart';
                    heart.textContent = heartSymbols[Math.floor(Math.random() * heartSymbols.length)];
                    heart.style.left = Math.random() * 100 + '%';
                    heart.style.animationDelay = Math.random() * 2 + 's';
                    heart.style.animationDuration = (Math.random() * 3 + 3) + 's';
                    heartsContainer.appendChild(heart);
                    
                    setTimeout(() => heart.remove(), 7000);
                }, i * 100);
            }
        }

        // Initialize No button position
        window.addEventListener('load', () => {
            const noBtn = document.getElementById('noBtn');
            noBtn.style.position = 'absolute';
            noBtn.style.right = '20px';
        });
    </script>
</body>
</html>
