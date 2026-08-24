<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For Yashi ♾️</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #ffe5ec, #ffc2d1);
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            position: relative;
            text-align: center;
            padding: 20px;
        }

        /* Floating Hearts Background */
        .heart {
            position: absolute;
            color: #ff4d6d;
            font-size: 24px;
            animation: float Up 5s linear infinite;
            opacity: 0.6;
            bottom: -50px;
            z-index: 1;
            pointer-events: none;
        }

        @keyframes floatUp {
            0% {
                transform: translateY(0) translateX(0) rotate(0deg);
                opacity: 0.6;
            }
            100% {
                transform: translateY(-105vh) translateX(100px) rotate(360deg);
                opacity: 0;
            }
        }

        /* Main Container */
        .container {
            background: rgba(255, 255, 255, 0.85);
            padding: 30px 20px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px);
            max-width: 90%;
            width: 350px;
            z-index: 10;
            transition: all 0.5s ease;
        }

        h1 {
            color: #ff0054;
            font-size: 1.8rem;
            margin-bottom: 30px;
            font-weight: 800;
            line-height: 1.4;
        }

        /* Buttons */
        .btn-container {
            display: flex;
            justify-content: space-around;
            align-items: center;
            height: 80px;
            position: relative;
        }

        .btn {
            padding: 12px 30px;
            font-size: 1.2rem;
            font-weight: bold;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: transform 0.1s ease;
            box-shadow: 0 5px 15px rgba(0,0,0,0.15);
        }

        #yesBtn {
            background-color: #ff4d6d;
            color: white;
            z-index: 11;
        }

        #noBtn {
            background-color: #6c757d;
            color: white;
            position: absolute;
            z-index: 12;
            touch-action: none; /* Prevents default mobile scrolling when touched */
        }

        /* Success Screen Styles */
        .success-text {
            color: #ff0054;
            font-size: 2.2rem;
            font-weight: 900;
            margin-bottom: 20px;
            display: none;
            animation: popIn 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .gif-container img {
            width: 80%;
            max-width: 200px;
            border-radius: 15px;
            display: none;
            margin: 0 auto;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        @keyframes popIn {
            0% { transform: scale(0.5); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }

        /* Graffiti Confetti Effect */
        .graffiti {
            position: absolute;
            font-size: 30px;
            font-weight: bold;
            pointer-events: none;
            z-index: 5;
            animation: explode 1s ease-out forwards;
        }

        @keyframes explode {
            0% { transform: translate(0, 0) scale(1); opacity: 1; }
            100% { transform: translate(var(--x), var(--y)) scale(1.5); opacity: 0; }
        }
    </style>
</head>
<body>

    <!-- Floating Hearts -->
    <div id="hearts-bg"></div>

    <!-- Interactive Card -->
    <div class="container" id="proposalCard">
        <h1 id="question">YASHI
        , WILL YOU BE MINE FOREVER ♾️?</h1>
        
        <div class="btn-container" id="btnContainer">
            <button class="btn" id="yesBtn">YES</button>
            <button class="btn" id="noBtn">NO</button>
        </div>

        <div class="success-text" id="successMsg">I KNEW YOU LOVE ME ❤️</div>
        <div class="gif-container">
            <!-- Using a widely available, cute wholesome dancing gif -->
            <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExMmszd3U0NTh3bXY2b3Z0b3BhbDZpMm9pMTZ4N2M5M3V5N3Nidm90MSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Rn/c7N3OfR9Wbyv3vO8I7/giphy.gif" id="danceGif" alt="Dancing Cute Character">
        </div>
    </div>

    <script>
        // 1. Generate Floating Hearts Background
        const heartsBg = document.getElementById('hearts-bg');
        const heartEmojis = ['❤️', '💖', '💝', '💕', '💗'];

        function createHeart() {
            const heart = document.createElement('div');
            heart.classList.add('heart');
            heart.innerText = heartEmojis[Math.floor(Math.random() * heartEmojis.length)];
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.animationDuration = (Math.random() * 3 + 3) + 's'; // 3s to 6s
            heart.style.fontSize = (Math.random() * 20 + 15) + 'px';
            heartsBg.appendChild(heart);

            setTimeout(() => {
                heart.remove();
            }, 6000);
        }
        setInterval(createHeart, 300);

        // 2. Make the NO Button Run Away (Cursor & Touch)
        const noBtn = document.getElementById('noBtn');
        const container = document.getElementById('proposalCard');

        function moveNoButton(e) {
            // Get container boundaries so button doesn't fly outside the card completely
            const padding = 20;
            const maxX = container.clientWidth - noBtn.clientWidth - padding;
            const maxY = container.clientHeight - noBtn.clientHeight - padding;

            // Generate completely random coordinates inside the card
            let randomX = Math.floor(Math.random() * maxX);
            let randomY = Math.floor(Math.random() * maxY);

            // Center readjustment so it behaves smoothly within position absolute
            noBtn.style.left = randomX + 'px';
            noBtn.style.top = randomY + 'px';
        }

        // Triggers for both Desktop mouse hover and Mobile touch screens
        noBtn.addEventListener('mouseenter', moveNoButton);
        noBtn.addEventListener('touchstart', function(e) {
            e.preventDefault(); // Prevents clicking action on mobile touch
            moveNoButton();
        });
        noBtn.addEventListener('click', function(e) {
            e.preventDefault(); // Ultimate fallback block
        });

        // 3. YES Button Action (Graffiti Explosion & Success State)
        const yesBtn = document.getElementById('yesBtn');
        const question = document.getElementById('question');
        const btnContainer = document.getElementById('btnContainer');
        const successMsg = document.getElementById('successMsg');
        const danceGif = document.getElementById('danceGif');

        const graffitiTexts = ['❤️', '✨', '🔥', 'XOXO', 'Mwah!', '💖', '♾️', 'MINE'];

        function spawnGraffiti() {
            for (let i = 0; i < 40; i++) {
                const item = document.createElement('div');
                item.classList.add('graffiti');
                item.innerText = graffitiTexts[Math.floor(Math.random() * graffitiTexts.length)];
                
                // Spawn near center
                item.style.left = '50vw';
                item.style.top = '50vh';
                
                // Set custom explosive trajectory
                const angle = Math.random() * Math.PI * 2;
                const distance = Math.random() * 200 + 100;
                const x = Math.cos(angle) * distance + 'px';
                const y = Math.sin(angle) * distance + 'px';
                
                item.style.setProperty('--x', x);
                item.style.setProperty('--y', y);
                item.style.color = `hsl(${Math.random() * 360}, 100%, 60%)`;

                document.body.appendChild(item);
                setTimeout(() => item.remove(), 1000);
            }
        }

        yesBtn.addEventListener('click', () => {
            // Hide Question and Buttons
            question.style.display = 'none';
            btnContainer.style.display = 'none';

            // Show Success Msg and Dancing GIF
            successMsg.style.display = 'block';
            danceGif.style.display = 'block';

            // Fire Graffiti Splatters immediately, then keep raining them!
            spawnGraffiti();
            setInterval(spawnGraffiti, 800);
        });
    </script>
</body>
</html>
