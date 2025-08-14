
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday </title>
    <style>
        body {
            margin: 0;
            padding: 0;
            background: #000;
            overflow: hidden;
            font-family: 'Comic Sans MS', cursive, sans-serif;
            text-align: center;
            height: 100vh;
            position: relative;
            transition: background 1s ease;
        }

        /* Background image with dark overlay */
        body.bg-image {
            background: linear-gradient(rgba(0,0,0,0.5), rgba(0,0,0,0.5)),
                        url('background.jpg') no-repeat center center/cover;
        }

        #startBtn {
            margin-top: 40vh;
            padding: 20px 40px;
            font-size: 1.5rem;
            background: #ff4b5c;
            color: white;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            box-shadow: 0 4px 10px rgba(0,0,0,0.3);
            transition: transform 0.2s;
            position: relative;
            z-index: 10;
        }
        #startBtn:hover {
            transform: scale(1.1);
        }

        #mainTitle {
            display: none;
            font-size: 3.5rem;
            color: purple;
            text-shadow: 0 0 15px rgba(128,0,128,0.5);
            margin-top: 20px;
            font-weight: bold;
        }
        #subTitle {
            display: none;
            font-size: 3rem;
            color: purple;
            text-shadow: 0 0 15px rgba(128,0,128,0.5);
            margin-top: 10px;
        }

        #paragraph {
            display: none;
            color: #ff1493; /* darker pink */
            font-size: 1.2rem;
            max-width: 90%;
            margin: 20px auto;
            text-align: center;
            text-shadow: 0 0 8px rgba(255,105,180,0.4);
            white-space: pre-wrap;
            position: relative;
            z-index: 5;
        }

        .balloon {
            position: absolute;
            bottom: -150px;
            border-radius: 50%;
            width: 50px;
            height: 60px;
            animation: floatUp 8s linear infinite;
        }
        .gift {
            position: absolute;
            bottom: -80px;
            width: 40px;
            height: 40px;
            background: gold;
            border: 2px solid #c97f02;
            border-radius: 5px;
        }

        @keyframes floatUp {
            0% { transform: translateY(0) rotate(0); opacity: 1; }
            100% { transform: translateY(-120vh) rotate(360deg); opacity: 0; }
        }

        canvas {
            position: absolute;
            top: 0;
            left: 0;
            pointer-events: none;
        }
    </style>
</head>
<body>
    <button id="startBtn">🎁 Press Me 🎁</button>
    <h1 id="mainTitle">HAPPY BIRTHDAY</h1>
    <h2 id="subTitle"> 💐</h2>
    <p id="paragraph"></p>
    <canvas id="fireworks"></canvas>

    <script>
        const startBtn = document.getElementById('startBtn');
        const mainTitle = document.getElementById('mainTitle');
        const subTitle = document.getElementById('subTitle');
        const paragraph = document.getElementById('paragraph');
        const canvas = document.getElementById('fireworks');
        const ctx = canvas.getContext('2d');

        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        const paraText = "Happy Bday,🙂! Ur smile outshines stars🌟, ur heart's pure magic💘. Not just older, but more amazing & beautiful🧿! Here's to a day as radiant as u, full of love❤️ & joy😼, my sweet Bhalu🧸..!";

        function typeWriter(text, element, speed) {
            let i = 0;
            element.style.display = 'block';
            element.innerHTML = ""; 
            function typing() {
                if (i < text.length) {
                    element.innerHTML += text.charAt(i);
                    i++;
                    setTimeout(typing, speed);
                }
            }
            typing();
        }

        function createGiftBalloon() {
            const balloon = document.createElement('div');
            balloon.classList.add('balloon');
            balloon.style.backgroundColor = `hsl(${Math.random() * 360}, 70%, 60%)`;
            balloon.style.left = `${Math.random() * 100}vw`;
            balloon.style.animationDuration = `${5 + Math.random() * 5}s`;

            const gift = document.createElement('div');
            gift.classList.add('gift');
            gift.style.left = balloon.style.left;

            document.body.appendChild(balloon);
            document.body.appendChild(gift);

            setTimeout(() => {
                explode(parseInt(balloon.style.left), Math.random() * window.innerHeight * 0.8);
                balloon.remove();
                gift.remove();
            }, 3000 + Math.random() * 3000);
        }

        let particles = [];
        function explode(x, y) {
            for (let i = 0; i < 30; i++) {
                particles.push({
                    x: x,
                    y: y,
                    radius: Math.random() * 3 + 2,
                    color: `hsl(${Math.random() * 360}, 70%, 60%)`,
                    velocity: {
                        x: (Math.random() - 0.5) * 5,
                        y: (Math.random() - 0.5) * 5
                    },
                    alpha: 1
                });
            }
        }

        function drawHeart(ctx, x, y, size, color, alpha) {
            ctx.save();
            ctx.translate(x, y);
            ctx.scale(size / 50, size / 50);
            ctx.beginPath();
            ctx.moveTo(0, 0);
            ctx.bezierCurveTo(0, -30, -25, -30, -25, 0);
            ctx.bezierCurveTo(-25, 20, 0, 30, 0, 50);
            ctx.bezierCurveTo(0, 30, 25, 20, 25, 0);
            ctx.bezierCurveTo(25, -30, 0, -30, 0, 0);
            ctx.fillStyle = color;
            ctx.globalAlpha = alpha;
            ctx.fill();
            ctx.restore();
        }

        function animateFireworks() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            particles.forEach((p, i) => {
                p.x += p.velocity.x;
                p.y += p.velocity.y;
                p.alpha -= 0.02;
                drawHeart(ctx, p.x, p.y, p.radius * 5, p.color, p.alpha);
                if (p.alpha <= 0) {
                    particles.splice(i, 1);
                }
            });
            requestAnimationFrame(animateFireworks);
        }
        animateFireworks();

        startBtn.addEventListener('click', () => {
            document.body.classList.add('bg-image');
            startBtn.style.display = 'none';
            mainTitle.style.display = 'block';
            subTitle.style.display = 'block';
            setTimeout(() => {
                typeWriter(paraText, paragraph, 40);
            }, 2000);
            setInterval(createGiftBalloon, 800);
        });
    </script>
</body>
</html>
