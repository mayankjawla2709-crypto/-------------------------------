
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Happy Birthday Cutie Pie</title>
<style>
    body {
        margin: 0;
        padding: 0;
        background:
            url('https://i.ibb.co/dkD0rWj/cartoon-birthday-bg.jpg') no-repeat center center / cover,
            linear-gradient(135deg, #ffdde1, #ee9ca7);
        overflow: hidden;
        font-family: 'Comic Sans MS', cursive, sans-serif;
        text-align: center;
        height: 100vh;
        position: relative;
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
        z-index: 10;
    }
    #startBtn:hover { transform: scale(1.1); }
    h1 {
        font-size: 3rem;
        color: white;
        text-shadow: 0 0 10px pink, 0 0 20px purple;
        display: none;
        margin-top: 30px;
        animation: fadeIn 2s ease forwards, glow 1.5s infinite alternate;
        z-index: 5;
        position: relative;
    }
    @keyframes glow {
        from { text-shadow: 0 0 10px pink, 0 0 20px purple; }
        to { text-shadow: 0 0 20px pink, 0 0 30px purple; }
    }
    @keyframes fadeIn {
        from { opacity: 0; }
        to { opacity: 1; }
    }
    #paragraph {
        display: none;
        color: white;
        font-size: 1.2rem;
        max-width: 90%;
        margin: 20px auto;
        text-shadow: 0 0 8px pink, 0 0 16px purple;
        white-space: pre-wrap;
        z-index: 5;
        position: relative;
    }
    .balloon {
        position: absolute;
        bottom: -150px;
        border-radius: 50%;
        width: 50px;
        height: 60px;
        animation: floatUp 8s linear forwards;
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
<h1 id="message">Happy Birthday Cutie Pie 💐</h1>
<p id="paragraph"></p>

<!-- Add your MP3 link below in src="" if you get one -->
<!-- <audio id="music" src="YOUR-MP3-LINK.mp3"></audio> -->

<canvas id="fireworks"></canvas>

<script>
const startBtn = document.getElementById('startBtn');
const message = document.getElementById('message');
const paragraph = document.getElementById('paragraph');
const canvas = document.getElementById('fireworks');
const ctx = canvas.getContext('2d');

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

const paraText = "Happy Bday, maharani😁! Ur smile outshines stars, ur heart's pure magic. Not just older, but more amazing & beautiful! Here's to a day as radiant as u, full of love & joy, my sweet Bhalu🧸..!";

// Typewriter effect
function typeWriter(text, element, speed) {
    let i = 0;
    element.style.display = 'block';
    function typing() {
        if (i < text.length) {
            element.innerHTML += text.charAt(i);
            i++;
            setTimeout(typing, speed);
        }
    }
    typing();
}

// Create balloons & gifts
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

// Fireworks particles
let particles = [];
function explode(x, y) {
    // Hearts
    for (let i = 0; i < 15; i++) {
        particles.push({
            x, y,
            shape: 'heart',
            size: 8,
            color: `hsl(${Math.random() * 50 + 330}, 80%, 60%)`,
            velocity: {
                x: (Math.random() - 0.5) * 6,
                y: (Math.random() - 0.5) * 6
            },
            alpha: 1
        });
    }
    // Circles
    for (let i = 0; i < 15; i++) {
        particles.push({
            x, y,
            shape: 'circle',
            radius: Math.random() * 3 + 2,
            color: `hsl(${Math.random() * 50 + 330}, 80%, 60%)`,
            velocity: {
                x: (Math.random() - 0.5) * 6,
                y: (Math.random() - 0.5) * 6
            },
            alpha: 1
        });
    }
}

// Animate fireworks
function animateFireworks() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    particles.forEach((p, i) => {
        p.x += p.velocity.x;
        p.y += p.velocity.y;
        p.alpha -= 0.02;
        ctx.globalAlpha = p.alpha;
        ctx.fillStyle = p.color;

        if (p.shape === 'circle') {
            ctx.beginPath();
            ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2);
            ctx.fill();
        } else if (p.shape === 'heart') {
            ctx.beginPath();
            ctx.moveTo(p.x, p.y);
            ctx.bezierCurveTo(p.x, p.y - p.size / 2, p.x - p.size, p.y - p.size, p.x - p.size, p.y);
            ctx.bezierCurveTo(p.x - p.size, p.y + p.size, p.x, p.y + p.size * 1.5, p.x, p.y + p.size * 2);
            ctx.bezierCurveTo(p.x, p.y + p.size * 1.5, p.x + p.size, p.y + p.size, p.x + p.size, p.y);
            ctx.bezierCurveTo(p.x + p.size, p.y - p.size, p.x, p.y - p.size / 2, p.x, p.y);
            ctx.fill();
        }

        if (p.alpha <= 0) particles.splice(i, 1);
    });
    requestAnimationFrame(animateFireworks);
}
animateFireworks();

// Start event
startBtn.addEventListener('click', () => {
    startBtn.style.display = 'none';
    message.style.display = 'block';
    // Uncomment to play music: document.getElementById('music').play();
    setTimeout(() => { typeWriter(paraText, paragraph, 40); }, 2000);
    setInterval(createGiftBalloon, 800);
});
</script>
</body>
</html>
