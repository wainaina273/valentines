<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Valentine's Special 💘</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Comic Sans MS', cursive;
            background: linear-gradient(45deg, #ff3385, #ff69b4, #ff1493);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            touch-action: manipulation;
        }

        .container {
            background: rgba(255, 255, 255, 0.95);
            padding: 2rem;
            border-radius: 20px;
            box-shadow: 0 0 40px rgba(255, 0, 102, 0.3);
            text-align: center;
            margin: 20px;
            position: relative;
            animation: heartbeat 1.2s infinite, float 3s ease-in-out infinite;
            max-width: 95%;
        }

        h1 {
            color: #ff0066;
            font-size: 2.5rem;
            margin-bottom: 2rem;
            text-shadow: 2px 2px 4px rgba(255, 0, 102, 0.2);
            animation: textGlow 2s ease-in-out infinite;
        }

        .buttons {
            display: flex;
            gap: 20px;
            justify-content: center;
            flex-wrap: wrap;
        }

        button {
            padding: 15px 30px;
            font-size: 1.3rem;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            transition: all 0.3s ease;
            min-width: 140px;
            position: relative;
            overflow: hidden;
        }

        #yesBtn {
            background: linear-gradient(45deg, #ff0066, #ff3385);
            color: white;
            box-shadow: 0 4px 15px rgba(255, 0, 102, 0.3);
            animation: pulse 2s infinite;
        }

        #noBtn {
            background: linear-gradient(45deg, #ff6666, #ff9999);
            color: white;
            box-shadow: 0 4px 15px rgba(255, 0, 102, 0.3);
        }

        /* Animations */
        @keyframes heartbeat {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.03); }
        }

        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        @keyframes textGlow {
            0%, 100% { text-shadow: 0 0 10px rgba(255,0,102,0.2); }
            50% { text-shadow: 0 0 20px rgba(255,0,102,0.4); }
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .hearts span {
            position: absolute;
            animation: heartFloat 4s linear infinite;
            font-size: 2rem;
        }

        @keyframes heartFloat {
            0% { transform: translateY(110vh) rotate(0deg); opacity: 0; }
            30% { opacity: 1; }
            100% { transform: translateY(-10vh) rotate(360deg); opacity: 0; }
        }

        @media (max-width: 600px) {
            h1 { font-size: 1.8rem; }
            button { font-size: 1.1rem; padding: 12px 25px; }
            .container { padding: 1.5rem; }
        }
    </style>
</head>
<body>
    <div class="hearts" id="hearts"></div>
    
    <div class="container">
        <h1>💖 Will You Be My Valentine? 💖</h1>
        <div class="buttons">
            <button id="yesBtn">YES! 💘</button>
            <button id="noBtn" onmouseover="dodge()" ontouchstart="dodge()">No? 😏</button>
        </div>
    </div>

    <script>
        // Create floating hearts
        function createHearts() {
            const hearts = ['💖', '❤️', '💗', '💕', '💓'];
            const container = document.getElementById('hearts');
            
            setInterval(() => {
                const heart = document.createElement('span');
                heart.textContent = hearts[Math.floor(Math.random() * hearts.length)];
                heart.style.left = Math.random() * 100 + '%';
                heart.style.animationDuration = (Math.random() * 3 + 2) + 's';
                heart.style.fontSize = (Math.random() * 2 + 1) + 'rem';
                container.appendChild(heart);
                
                setTimeout(() => heart.remove(), 5000);
            }, 300);
        }

        // Yes button handler
        document.getElementById('yesBtn').addEventListener('click', () => {
            // Confetti effect
            for(let i = 0; i < 50; i++) {
                const confetti = document.createElement('div');
                confetti.textContent = '🎉';
                confetti.style.position = 'fixed';
                confetti.style.left = Math.random() * 100 + '%';
                confetti.style.top = Math.random() * 100 + '%';
                confetti.style.animation = `confettiFall ${Math.random() * 2 + 1}s linear`;
                document.body.appendChild(confetti);
                setTimeout(() => confetti.remove(), 2000);
            }
            
            alert("🎉 Yay! You've made my heart flutter! 💞\nLet's make magical memories! 🌟");
        });

        // No button dodge mechanics
        let dodgeCount = 0;
        const messages = ["Nope! 😜", "you dont mean that! ", "Not Today! 😈", "Can't Catch Me! 🏃♂️"];
        
        function dodge() {
            const noBtn = document.getElementById('noBtn');
            dodgeCount++;
            
            // Animate button movement
            noBtn.style.transform = `translate(
                ${Math.random() * 80 - 40}px, 
                ${Math.random() * 80 - 40}px
            )`;
            
            // Update button text
            noBtn.textContent = messages[Math.min(dodgeCount, messages.length - 1)];
            
            // Add shake animation after 2 tries
            if(dodgeCount >= 2) {
                noBtn.style.animation = 'shake 0.5s';
                setTimeout(() => noBtn.style.animation = '', 500);
            }
            
            // Escape animation after 4 tries
            if(dodgeCount >= 4) {
                noBtn.style.animation = 'escape 1.5s forwards';
                setTimeout(() => {
                    noBtn.style.display = 'none';
                    alert("The 'No' option escaped! 😉 Only YES remains! 💘");
                }, 1500);
            }
        }

        // Start animations
        createHearts();

        // Add escape animation
        const style = document.createElement('style');
        style.textContent = `
            @keyframes shake {
                0%, 100% { transform: translateX(0); }
                25% { transform: translateX(-15px); }
                75% { transform: translateX(15px); }
            }
            @keyframes escape {
                to { transform: translate(150vw, -150vh) rotate(720deg); opacity: 0; }
            }
            @keyframes confettiFall {
                to { transform: translateY(100vh) rotate(360deg); }
            }
        `;
        document.head.appendChild(style);
    </script>
</body>FROM WAINAINAS LABS
</html>
