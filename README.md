# Happy-birthday-2
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Happy Birthday Shaurya</title>
<style>
  body {
    margin: 0;
    padding: 0;
    background: linear-gradient(to bottom, #ffdde1, #ee9ca7);
    overflow: hidden;
    font-family: 'Comic Sans MS', cursive, sans-serif;
    text-align: center;
    height: 100vh;
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
  }
  #startBtn:hover {
    transform: scale(1.1);
  }
  h1 {
    font-size: 3rem;
    color: #fff;
    text-shadow: 2px 2px 5px #000;
    animation: glow 1.5s infinite alternate;
    display: none;
    margin-top: 30px;
  }
  @keyframes glow {
    from { text-shadow: 2px 2px 5px #000, 0 0 10px #ff4b5c; }
    to { text-shadow: 2px 2px 10px #fff, 0 0 20px #ff4b5c; }
  }
  .balloon {
    position: absolute;
    bottom: -150px;
    background-color: red;
    border-radius: 50%;
    width: 40px;
    height: 50px;
    animation: floatUp 6s linear infinite;
  }
  @keyframes floatUp {
    0% { transform: translateY(0) rotate(0); opacity: 1; }
    100% { transform: translateY(-120vh) rotate(360deg); opacity: 0; }
  }
</style>
</head>
<body>

<button id="startBtn">🎁 Press Me 🎁</button>
<h1 id="message">Happy Birthday Shaurya! 🎉🎈</h1>
<audio id="music" src="https://www.bensound.com/bensound-music/bensound-romantic.mp3"></audio>

<script>
const startBtn = document.getElementById('startBtn');
const message = document.getElementById('message');
const music = document.getElementById('music');

function createBalloon() {
  const balloon = document.createElement('div');
  balloon.classList.add('balloon');
  balloon.style.backgroundColor = `hsl(${Math.random() * 360}, 70%, 60%)`;
  balloon.style.left = `${Math.random() * 100}vw`;
  balloon.style.animationDuration = `${5 + Math.random() * 5}s`;
  document.body.appendChild(balloon);

  setTimeout(() => {
    balloon.remove();
  }, 10000);
}

startBtn.addEventListener('click', () => {
  startBtn.style.display = 'none';
  message.style.display = 'block';
  music.play();
  setInterval(createBalloon, 300);
});
</script>

</body>
</html>
