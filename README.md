# Happy-birthday-cutie
 <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday Cutie Pie!</title>
    <link rel="stylesheet" href="styles.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css"/>
</head>
<body>
    <div id="initial-button" class="initial-container">
        <button onclick="startCelebration()">Press Me</button>
    </div>
    <div id="main-content" class="container" style="display: none;">
        <h1 id="birthday-text" class="animate__animated">Happy Birthday Cutie Pie 💐</h1>
        <p id="typewriter" class="message"></p>
        <button onclick="triggerFireworks()">More Fireworks!</button>
    </div>
    <canvas id="gift-canvas"></canvas>
    <audio id="background-music">
        <source src="music.mp3" type="audio/mpeg">
        Your browser does not support the audio element.
    </audio>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>
    <script src="script.js"></script>
</body>
</html>       
