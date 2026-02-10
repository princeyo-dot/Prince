<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Can You Be My Valentine?</title>

  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #ff9a9e, #fad0c4);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      text-align: center;
      color: #fff;
      overflow: hidden;
    }

    /* Floating hearts */
    .heart {
      position: absolute;
      bottom: -20px;
      font-size: 20px;
      animation: floatUp 6s linear infinite;
      opacity: 0.7;
    }

    @keyframes floatUp {
      0% {
        transform: translateY(0) scale(1);
        opacity: 0.7;
      }
      100% {
        transform: translateY(-110vh) scale(1.5);
        opacity: 0;
      }
    }

    .card {
      background: rgba(255, 255, 255, 0.15);
      backdrop-filter: blur(12px);
      border-radius: 25px;
      padding: 40px 30px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.25);
      width: 90%;
      max-width: 400px;
      z-index: 2;
    }

    h1 {
      font-size: 28px;
      margin-bottom: 30px;
    }

    .buttons {
      position: relative;
      height: 120px;
    }

    button {
      border: none;
      border-radius: 999px;
      padding: 12px 24px;
      font-size: 18px;
      cursor: pointer;
      transition: all 0.2s ease;
      position: absolute;
    }

    #yesBtn {
      background: #ff4d6d;
      color: white;
      left: 30%;
      transform: translateX(-50%);
    }

    #noBtn {
      background: #ffffff;
      color: #ff4d6d;
      left: 70%;
      transform: translateX(-50%);
    }

    #message {
      margin-top: 20px;
      font-size: 18px;
      min-height: 24px;
    }
  </style>
</head>
<body>
  <!-- Background music -->
  <audio id="bgMusic" autoplay loop>
    <source src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_115b9b0c1a.mp3" type="audio/mpeg" />
  </audio>

  <div class="card">
    <h1>Can you be my Valentine, Beance? 💖</h1>

    <div class="buttons">
      <button id="yesBtn">Yes 🥺</button>
      <button id="noBtn">No 😭</button>
    </div>

    <div id="message"></div>
  </div>

  <script>
    const noBtn = document.getElementById('noBtn');
    const yesBtn = document.getElementById('yesBtn');
    const message = document.getElementById('message');

    const noMessages = [
      "Why naman ganon 😭",
      "Are you sureeee? 🥺",
      "Di ka ba maaawa sa baby na 'to? 🥹",
      "Last na tanong… sure ka na ba talaga? 😭",
      "Please click Yes na oh 😔"
    ];

    let noClicks = 0;

    noBtn.addEventListener('click', () => {
      const msg = noMessages[noClicks % noMessages.length];
      message.textContent = msg;
      noClicks++;

      // Move NO button randomly
      const x = Math.random() * 250 - 125;
      const y = Math.random() * 60 - 30;
      noBtn.style.transform = `translate(${x}px, ${y}px)`;

      // Make YES button bigger
      const scale = 1 + noClicks * 0.18;
      yesBtn.style.transform = `translateX(-50%) scale(${scale})`;
    });

    yesBtn.addEventListener('click', () => {
      document.body.innerHTML = `
        <div style="
          height: 100vh;
          display: flex;
          justify-content: center;
          align-items: center;
          background: linear-gradient(135deg, #ff4d6d, #ff758c);
          color: white;
          font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
          text-align: center;
          padding: 20px;
          flex-direction: column;
        ">
          <h1 style="font-size: 38px; margin-bottom: 10px;">YAYYY 💖</h1>
          <p style="font-size: 20px; max-width: 400px;">
            You just made me the happiest person today 🥺<br/>
            Thank you for saying yes, Beance 💐
          </p>
        </div>
      `;
    });

    // Generate floating hearts
    function createHeart() {
      const heart = document.createElement('div');
      heart.className = 'heart';
      heart.innerHTML = '💖';
      heart.style.left = Math.random() * 100 + 'vw';
      heart.style.fontSize = 14 + Math.random() * 20 + 'px';
      heart.style.animationDuration = 4 + Math.random() * 4 + 's';
      document.body.appendChild(heart);

      setTimeout(() => heart.remove(), 8000);
    }

    setInterval(createHeart, 400);

    // Try to play music (some browsers need interaction)
    document.addEventListener('click', () => {
      const music = document.getElementById('bgMusic');
      music.play().catch(() => {});
    });
  </script>
</body>
</html>
