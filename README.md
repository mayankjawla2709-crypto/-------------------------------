<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Happy Birthday Cutie Pie</title>
<style>
  body {
    margin: 0;
    padding: 0;
    background: url('https://i.ibb.co/dkD0rWj/cartoon-birthday-bg.jpg') no-repeat center center/cover;
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

  #message {
    font-size: 3rem;
    color: white;
    text-shadow: 0 0 10px pink, 0 0 20px purple;
    display: none;
    margin-top: 30px;
    animation: glow 1.5s infinite alternate;
    z-index: 5;
    position: relative;
    opacity: 0;
  }
  @keyframes glow {
    from { text-shadow: 0 0 10px pink, 0 0 20px purple; }
    to   { text-shadow: 0 0 20px pink, 0 0 30px purple; }
  }
  @keyframes fadeIn { to { opacity: 1; } }

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
    animation: floatUp 8s linear forwards, sway 2s ease-in-out infinite alternate;
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
    0%   { transform: translateY(0) rotate(0); opacity: 1; }
    100% { transform: translateY(-120vh) rotate(360deg); opacity: 0; }
  }
  @keyframes sway {
    from { transform: translateX(-10px); }
    to   { transform: translateX(10px); }
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
<audio id="music" src="YOUR-MP3-LINK-HERE" preload="auto"></audio>
<canvas id="fireworks"></canvas>

<script>
const startBtn = document.getElementById('startBtn');
const message = document.getElementById('message');
const paragraph = document.getElementById('paragraph');
const music = document.getElementById('music');
const canvas = document.getElementById('fireworks');
const ctx = canvas.getContext('2d');
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

const paraText = "Happy Bday, maharani😁! Ur smile outshines stars, ur heart's pure magic. Not just older, but more amazing & beautiful! Here's to a day as radiant as u, full of love & joy, my sweet Bhalu🧸..!";

function typeWriter(text, element, speed) {
  let i = 0;
  element.innerHTML = '';
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

  const explodeTime = 3000 + Math.random() * 3000;
  setTimeout(() => {
    explode(parseFloat(balloon.style.left) * window.innerWidth / 100, Math.random() * window.innerHeight * 0.8);
    balloon.remove();
    gift.remove();
  }, explodeTime);
}

let particles = [];

function explode(x, y) {
  for (let i = 0; i < 20; i++) {
    particles.push({
      x: x,
      y: y,
      radius: Math.random() * 3 + 2,
      color: `hsl(${Math.random() * 50 + 330}, 70%, 60%)`,
      velocity: { x: (Math.random() - 0.5) * 5, y: (Math.random() - 0.5) * 5 },
      alpha: 1,
      shape: 'circle'
    });
  }
  // Hearts
  for (let i = 0; i < 10; i++) {
    particles.push({
      x: x,
      y: y,
      radius: Math.random() * 2 + 1,
      color: `hsl(${Math.random() * 50 + 330}, 70%, 60%)`,
      velocity: { x: (Math.random() - 0.5) * 3, y: (Math.random() - 0.5) * 3 },
      alpha: 1,
      shape: 'heart'
    });
  }
}

function drawHeart(ctx, x, y, size) {
  ctx.beginPath();
  ctx.moveTo(x, y);
  ctx.bezierCurveTo(x, y - size/2, x - size, y - size/2, x - size, y);
  ctx.bezierCurveTo(x - size, y + size/2, x, y + size, x, y + size*1.5);
  ctx.bezierCurveTo(x, y + size, x + size, y + size/2, x + size, y);
  ctx.bezierCurveTo(x + size, y - size/2, x, y - size/2, x, y);
  ctx.fill();
}

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
      ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2, false);
      ctx.fill();
    } else if (p.shape === 'heart') {
      drawHeart(ctx, p.x, p.y, p.radius * 2);
    }
    if (p.alpha <= 0) particles.splice(i, 1);
  });
  requestAnimationFrame(animateFireworks);
}
animateFireworks();

startBtn.addEventListener('click', () => {
  startBtn.style.display = 'none';
  message.style.display = 'block';
  message.style.animation = "fadeIn 2s forwards, glow 1.5s infinite alternate";
  if (music.src) music.play();
  setTimeout(() => {
    typeWriter(paraText, paragraph, 40);
  }, 2000);
  setInterval(createGiftBalloon, 800);
});
</script>
</body>
</html>
