# Happy-birthday-cutie
 <!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Happy Birthday!</title>
<style>
body {
font-family: 'Arial', sans-serif;
margin: 0;
overflow: hidden; /* Hide scrollbars during animation /
background-color: #f0f8ff; / Initial soft background /
display: flex;
justify-content: center;
align-items: center;
min-height: 100vh;
}
#start-button {
padding: 15px 30px;
font-size: 1.2em;
cursor: pointer;
background-color: #ff6347;
color: white;
border: none;
border-radius: 8px;
box-shadow: 2px 2px 5px rgba(0,0,0,0.2);
transition: background-color 0.3s ease;
}
#start-button:hover {
background-color: #e74c3c;
}
#birthday-scene {
position: absolute;
top: 0;
left: 0;
width: 100%;
height: 100%;
display: none; / Hidden by default /
flex-direction: column;
align-items: center;
justify-content: center;
z-index: -1;
}
#background {
position: absolute;
top: 0;
left: 0;
width: 100%;
height: 100%;
background-image: url('birthday_background.jpg'); / Replace with your image /
background-size: cover;
opacity: 0;
transition: opacity 1s ease-in-out;
z-index: -2;
}
#music {
display: none;
}
.gift-box {
position: absolute;
bottom: -50px;
width: 50px;
height: 50px;
background-color: gold;
border: 2px solid #ccac00;
box-sizing: border-box;
border-radius: 5px;
transform: translateY(0);
opacity: 0;
}
.balloon {
position: absolute;
width: 30px;
height: 40px;
border-radius: 50%;
background-color: red;
bottom: -40px;
transform: translateY(0);
opacity: 0;
}
.firework {
position: absolute;
width: 10px;
height: 10px;
border-radius: 50%;
background-color: #ff4d4d;
opacity: 0;
}
#birthday-message-container {
position: absolute;
top: 50%;
left: 50%;
transform: translate(-50%, -50%);
text-align: center;
color: #ff69b4; / Romantic shade /
font-size: 2.5em;
opacity: 0;
transition: opacity 1s ease-in-out;
z-index: 10;
}
#birthday-message {
text-shadow: 0 0 10px #ff69b4; / Glowing effect */
}
#personal-message {
color: #333;
font-size: 1.2em;
margin-top: 15px;
}
</style>
</head>
<body>
<button id="start-button">Press Me</button>
<div id="birthday-scene">
<div id="background"></div>
<audio id="music" src="16_candles.mp3"></audio> <div id="birthday-message-container">
<h1 id="birthday-message">Happy birthday cutie pie 💐</h1>
<p id="personal-message"></p>
</div>
</div>
