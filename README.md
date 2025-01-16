<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Surprise Gift</title>
  <style>
    /* General Styling */
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background: linear-gradient(135deg, #FFC371, #FF5F6D);
      color: white;
      overflow: hidden;
    }

    h1 {
      text-align: center;
      margin: 20px 0;
      font-size: 2em;
    }

    /* Music Box */
    .music-box {
      background-color: #333;
      color: white;
      width: 300px;
      margin: 20px auto;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 12px rgba(255, 255, 255, 0.3);
      text-align: center;
    }

    .music-box h2 {
      font-size: 1.5em;
      margin: 0;
    }

    .music-box p {
      font-size: 1em;
      margin: 10px 0;
      color: #bbb;
    }

    .cover-circle {
      width: 150px;
      height: 150px;
      margin: 20px auto;
      border-radius: 50%;
      background: url('yellow.jpg') no-repeat center center;
      background-size: cover;
      animation: rotateCover 8s linear infinite;
      box-shadow: 0 0 10px rgba(255, 255, 255, 0.5);
    }

    @keyframes rotateCover {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    .progress-container {
      width: 100%;
      background-color: #444;
      height: 5px;
      border-radius: 5px;
      position: relative;
      margin-top: 20px;
    }

    .progress-bar {
      height: 100%;
      background-color: #4CAF50;
      width: 0;
      border-radius: 5px;
    }

    .time-container {
      display: flex;
      justify-content: space-between;
      font-size: 0.8em;
      color: #bbb;
      margin-top: 5px;
    }

    .controls {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 10px;
    }

    .control-btn {
      width: 50px;
      height: 50px;
      border: none;
      background-color: black;
      border-radius: 50%;
      color: white;
      font-size: 1.5em;
      cursor: pointer;
      box-shadow: 0 0 10px rgba(255, 255, 255, 0.3);
    }

    .control-btn:hover {
      background-color: #555;
    }

    /* Password Box */
    .password-box {
      background-color: #333;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 12px rgba(255, 255, 255, 0.3);
      width: 300px;
      margin: 20px auto;
    }

    .password-box input {
      padding: 10px;
      border-radius: 8px;
      border: 2px solid #ddd;
      width: 70%;
      margin-bottom: 10px;
      font-size: 1em;
    }

    .password-box button {
      background-color: #4CAF50;
      color: white;
      padding: 10px 15px;
      border: none;
      border-radius: 8px;
      font-size: 1em;
      cursor: pointer;
    }

    .password-box button:hover {
      background-color: #45a049;
    }

    /* Surprise Message */
    .message-box {
      background-color: #333;
      color: white;
      width: 300px;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 12px rgba(255, 255, 255, 0.3);
      margin: 20px auto;
      display: none;
      animation: zoomIn 0.8s ease-in-out;
    }

    .message-box h3 {
      font-size: 1.5em;
      margin: 0;
    }

    .message-box p {
      font-size: 1.2em;
      margin: 10px 0;
    }

    @keyframes zoomIn {
      from {
        transform: scale(0.8);
        opacity: 0;
      }
      to {
        transform: scale(1);
        opacity: 1;
      }
    }

    /* Confetti Effect */
    #confetti-container {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
    }

    .confetti {
      position: absolute;
      width: 10px;
      height: 10px;
      background-color: #FFD700;
      animation: fall 4s ease-in-out infinite;
    }

    @keyframes fall {
      0% { transform: translateY(-100%); opacity: 1; }
      100% { transform: translateY(100%); opacity: 0; }
    }
  </style>
</head>
<body>
  <h1>Birthday Surprise!</h1>

  <div class="music-box">
    <h2>SWEETEST THING</h2>
    <p>by Seventeen</p>
    <div class="cover-circle"></div>
    <div class="time-container">
      <span id="start-time">00:00</span>
      <span id="end-time">00:00</span>
    </div>
    <div class="progress-container">
      <div class="progress-bar" id="progress-bar"></div>
    </div>
    <div class="controls">
      <button class="control-btn" id="rewind-btn">⏪</button>
      <button class="control-btn" id="play-btn">▶️</button>
      <button class="control-btn" id="forward-btn">⏩</button>
    </div>
  </div>

  <div class="password-box">
    <p>Enter password:</p>
    <input type="password" id="password-input" placeholder="Password">
    <button id="password-btn">Unlock</button>
  </div>

  <div class="message-box" id="message-box">
    <h3>PESAN HARI INI ❤️</h3>
    <p>Semoga hari ini penuh dengan damai dan sukacita dari Tuhan!🌟 Tuhan itu dekat dengan orang yang patah hati, dan menyelamatkan orang yang remuk jiwanya. (Mazmur 34:18) Ketika hati merasa lelah, ingatlah bahwa Tuhan selalu dekat dan siap memberikan kekuatan. Terus semangat, Kak! Tuhan memberkati!🌿💛</p>
  </div>

  <div id="confetti-container"></div>

  <script>
    const audio = new Audio('SWEETEST THING.mp3');
    const playBtn = document.getElementById('play-btn');
    const rewindBtn = document.getElementById('rewind-btn');
    const forwardBtn = document.getElementById('forward-btn');
    const progressBar = document.getElementById('progress-bar');
    const startTime = document.getElementById('start-time');
    const endTime = document.getElementById('end-time');
    const passwordBtn = document.getElementById('password-btn');
    const passwordInput = document.getElementById('password-input');
    const messageBox = document.getElementById('message-box');
    const confettiContainer = document.getElementById('confetti-container');

    playBtn.onclick = () => {
      if (audio.paused) {
        audio.play();
        playBtn.textContent = '⏸️';
      } else {
        audio.pause();
        playBtn.textContent = '▶️';
      }
    };

    audio.ontimeupdate = () => {
      const progress = (audio.currentTime / audio.duration) * 100;
      progressBar.style.width = `${progress}%`;

      const currentMinutes = Math.floor(audio.currentTime / 60);
      const currentSeconds = Math.floor(audio.currentTime % 60);
      startTime.textContent = `${currentMinutes}:${currentSeconds < 10 ? '0' : ''}${currentSeconds}`;

      const durationMinutes = Math.floor(audio.duration / 60);
      const durationSeconds = Math.floor(audio.duration % 60);
      endTime.textContent = `${durationMinutes}:${durationSeconds < 10 ? '0' : ''}${durationSeconds}`;
    };

    audio.onended = () => {
      showConfetti();
      messageBox.style.display = 'block';
    };

    passwordBtn.onclick = () => {
      if (passwordInput.value === '17031999') {
        messageBox.style.display = 'block';
      } else {
        alert('Wrong password!');
      }
    };

    function showConfetti() {
      for (let i = 0; i < 50; i++) {
        const confetti = document.createElement('div');
        confetti.className = 'confetti';
        confetti.style.left = `${Math.random() * 100}vw`;
        confetti.style.animationDuration = `${2 + Math.random() * 3}s`;
        confettiContainer.appendChild(confetti);

        setTimeout(() => confetti.remove(), 4000);
      }
    }
  </script>
</body>
</html>
