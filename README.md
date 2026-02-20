<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>A Special Message for Leena</title>
    <style>
        :root {
            --pink-bg: #ffe4e1;
            --dark-pink: #ff69b4;
            --heart-color: #ff4d6d;
            --envelope-color: #f39c12;
        }

        body, html {
            margin: 0;
            padding: 0;
            height: 100%;
            width: 100%;
            background-color: var(--pink-bg);
            font-family: 'Arial', sans-serif;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        /* Envelope Styling */
        .envelope-wrapper {
            position: relative;
            cursor: pointer;
            transition: transform 0.5s;
            z-index: 100;
        }

        .envelope {
            position: relative;
            width: 300px;
            height: 200px;
            background: #fff;
            border-bottom-left-radius: 10px;
            border-bottom-right-radius: 10px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.1);
        }

        .envelope::before {
            content: "";
            position: absolute;
            top: 0;
            z-index: 2;
            border-top: 110px solid #f1f1f1;
            border-left: 150px solid transparent;
            border-right: 150px solid transparent;
            transform-origin: top;
            transition: all 0.5s ease-in-out;
        }

        .envelope::after {
            content: "";
            position: absolute;
            z-index: 1;
            width: 0;
            height: 0;
            border-top: 100px solid transparent;
            border-left: 150px solid #e0e0e0;
            border-right: 150px solid #e0e0e0;
            border-bottom: 100px solid #e0e0e0;
            border-bottom-left-radius: 10px;
            border-bottom-right-radius: 10px;
        }

        .heart-seal {
            position: absolute;
            top: 90px;
            left: 135px;
            width: 30px;
            height: 30px;
            background: var(--heart-color);
            z-index: 3;
            transform: rotate(45deg);
            box-shadow: 0 2px 5px rgba(0,0,0,0.2);
            transition: all 0.5s ease-in-out;
        }

        .heart-seal::before, .heart-seal::after {
            content: "";
            width: 30px;
            height: 30px;
            background: var(--heart-color);
            border-radius: 50%;
            position: absolute;
        }

        .heart-seal::before { left: -15px; }
        .heart-seal::after { top: -15px; }

        /* Animation when opening */
        .opened .envelope::before {
            transform: rotateX(180deg);
            z-index: 0;
        }

        .opened .heart-seal {
            opacity: 0;
            transform: translateY(-50px) rotate(45deg);
        }

        /* Background Scene (Hidden initially) */
        #mainContent {
            display: none;
            opacity: 0;
            transition: opacity 1s ease-in;
            text-align: center;
        }

        /* --- Reuse previous styles for content --- */
        .cloud { position: absolute; width: 200px; height: 60px; background: #fff; border-radius: 200px; opacity: 0.6; animation: moveClouds 20s linear infinite; }
        .cloud::after, .cloud::before { content: ''; position: absolute; background: #fff; width: 100px; height: 100px; border-radius: 50%; top: -50px; left: 50px; }
        .cloud::before { width: 120px; height: 120px; top: -70px; left: 10px; }
        @keyframes moveClouds { from { transform: translateX(-300px); } to { transform: translateX(calc(100vw + 300px)); } }

        .cupid { position: absolute; font-size: 50px; animation: floatCupid 5s ease-in-out infinite; }
        @keyframes floatCupid { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-30px); } }

        .container { background: white; padding: 40px; border-radius: 20px; box-shadow: 0 10px 30px rgba(0,0,0,0.1); max-width: 450px; z-index: 10; border: 3px solid var(--dark-pink); }
        .heart-particle { position: absolute; color: var(--heart-color); animation: fall linear forwards; }
        @keyframes fall { to { transform: translateY(110vh) rotate(360deg); } }
        button { padding: 12px 25px; border-radius: 20px; border: none; cursor: pointer; margin: 10px; font-weight: bold; }
        #yesBtn { background: var(--heart-color); color: white; }
    </style>
</head>
<body>

    <div class="envelope-wrapper" id="envelopeWrapper" onclick="openEnvelope()">
        <div class="heart-seal"></div>
        <div class="envelope"></div>
        <p style="text-align: center; margin-top: 20px; color: var(--dark-pink); font-weight: bold;">Click to open your letter, Leena</p>
    </div>

    <div id="mainContent">
        <div class="cloud" style="top: 10%; left: -100px;"></div>
        <div class="cloud" style="top: 30%; left: -250px; animation-delay: 5s;"></div>
        <div class="cupid" style="top: 15%; right: 20%;">👼🏹</div>

        <div class="container">
            <h1 style="color: var(--dark-pink);">Dear Leena...</h1>
            <p>"My heart is yours forever, Leena! I love you more than words can say 🫣 Will you marry me 🥹😻 I don't know it's right or wrong but "From this day forward, I want to share every moment of my life with you!, I need Your warmth Forever in end of my death.""!"</p>
            <p style="font-size: 1.3rem; font-weight: bold; color: var(--heart-color);">Will you be my Valentine?</p>
            <div class="btn-group">
                <button id="yesBtn" onclick="celebrate()">YES!</button>
                <button id="noBtn" onmouseover="moveButton()">NO</button>
            </div>
        </div>
    </div>

    <script>
        function openEnvelope() {
            const wrapper = document.getElementById('envelopeWrapper');
            wrapper.classList.add('opened');
            
            setTimeout(() => {
                wrapper.style.display = 'none';
                const main = document.getElementById('mainContent');
                main.style.display = 'block';
                setTimeout(() => main.style.opacity = '1', 50);
                startHearts();
            }, 800);
        }

        function createHeart() {
            const heart = document.createElement('div');
            heart.classList.add('heart-particle');
            heart.innerHTML = '❤️';
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.top = '-20px';
            heart.style.fontSize = (Math.random() * 30 + 10) + 'px';
            heart.style.animationDuration = (Math.random() * 3 + 2) + 's';
            document.body.appendChild(heart);
            setTimeout(() => heart.remove(), 5000);
        }

        function startHearts() {
            setInterval(createHeart, 300);
        }

        function moveButton() {
            const btn = document.getElementById('noBtn');
            btn.style.position = 'absolute';
            btn.style.left = Math.random() * 80 + 'vw';
            btn.style.top = Math.random() * 80 + 'vh';
        }

        function celebrate() {
            document.querySelector('.container').innerHTML = `
                <h1 style="color: var(--heart-color);">Forever Yours! ❤️</h1>
                <p>You've made me the happiest person in the world,I cannot express enough thanks to you for allowing me to be myself and not running away from my over-loving. I was always afraid to be vulnerable, but now I feel safe to express myself without any fears. I will cherish every day, love every day, and smile every day. Leena!</p>
                <div style="font-size: 40px;">💍🌹✨</div>
            `;
            setInterval(createHeart, 50);
        }
    </script>
    
