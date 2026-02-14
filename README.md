<!DOCTYPE html>
<html lang="pl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Walentynka ❤️</title>

  <style>
    * { box-sizing: border-box; }

    body {
      margin: 0;
      min-height: 100vh;
      font-family: Arial, sans-serif;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 24px;
      overflow: hidden;

      /* tło w serduszka */
      background:
        radial-gradient(circle at 20px 20px, rgba(255,0,80,0.18) 10px, transparent 11px),
        radial-gradient(circle at 60px 60px, rgba(255,0,80,0.14) 10px, transparent 11px),
        radial-gradient(circle at 100px 30px, rgba(255,0,80,0.12) 10px, transparent 11px),
        #fff3f7;
      background-size: 120px 120px;
    }

    .card {
      width: min(720px, 95vw);
      background: rgba(255, 255, 255, 0.92);
      border-radius: 22px;
      padding: 28px 22px;
      text-align: center;
      box-shadow: 0 20px 60px rgba(0,0,0,0.15);
      position: relative;
      z-index: 2;
    }

    h1 {
      margin: 0 0 12px;
      font-size: clamp(24px, 4vw, 38px);
    }

    .sticker {
      display: inline-block;
      padding: 10px 14px;
      border-radius: 999px;
      background: #fff;
      border: 2px dashed rgba(255, 0, 90, 0.35);
      font-weight: 700;
      transform: rotate(-4deg);
      margin-bottom: 18px;
      user-select: none;
    }

    .buttons {
      margin-top: 18px;
      display: flex;
      gap: 14px;
      justify-content: center;
      align-items: center;
      flex-wrap: wrap;
      position: relative;
      min-height: 80px;
    }

    button {
      border: none;
      padding: 14px 22px;
      border-radius: 14px;
      font-size: 18px;
      font-weight: 700;
      cursor: pointer;
      transition: transform 0.12s ease;
    }

    button:active { transform: scale(0.98); }

    #yesBtn {
      background: #1fbf4a; /* zielony */
      color: white;
    }

    #noBtn {
      background: #ff3b3b;
      color: white;
      position: absolute; /* żeby mógł uciekać */
      left: 52%;
      top: 12px;
      transform: translateX(-50%);
    }

    .result {
      display: none;
      margin-top: 22px;
      padding: 18px;
      border-radius: 18px;
      background: rgba(255, 0, 90, 0.06);
      border: 2px solid rgba(255, 0, 90, 0.18);
    }

    .result p {
      margin: 0 0 14px;
      font-size: 18px;
      line-height: 1.35;
      font-weight: 700;
    }

    .photo {
      width: min(420px, 85vw);
      border-radius: 18px;
      box-shadow: 0 14px 40px rgba(0,0,0,0.18);
      border: 4px solid rgba(255, 0, 90, 0.12);
    }

    .footer {
      margin-top: 14px;
      opacity: 0.7;
      font-size: 13px;
    }

    /* confetti canvas */
    #confettiCanvas {
      position: fixed;
      inset: 0;
      width: 100vw;
      height: 100vh;
      pointer-events: none;
      z-index: 9999;
    }

    /* LECĄCE SERDUSZKA ❤️ */
    .heart {
      position: fixed;
      left: 50%;
      bottom: -30px;
      font-size: 22px;
      pointer-events: none;
      z-index: 9998;
      animation: floatUp 2.6s ease-in forwards;
      filter: drop-shadow(0 6px 10px rgba(0,0,0,0.18));
      user-select: none;
    }

    @keyframes floatUp {
      0% {
        transform: translate(-50%, 0) scale(0.9);
        opacity: 0;
      }
      10% {
        opacity: 1;
      }
      100% {
        transform: translate(var(--x), -85vh) rotate(var(--r)) scale(var(--s));
        opacity: 0;
      }
    }
  </style>
</head>

<body>
  <canvas id="confettiCanvas"></canvas>

  <div class="card">
    <h1>Czy zostaniesz moją Walentynką? ❤️</h1>

    <div class="sticker">💘 Uwaga! Kliknięcie „Nie” jest podejrzane 😄</div>

    <div class="buttons" id="btnArea">
      <button id="yesBtn">TAK 💚</button>
      <button id="noBtn">NIE 😈</button>
    </div>

    <div class="result" id="resultBox">
      <p>
        Super, jesteś już moją Walentynką od prawie 10 lat i chcę, żeby tak zostało.
        Kocham Cię. ❤️
      </p>
      <img class="photo" src="zdjecie.jpg" alt="Zdjęcie" />
      <div class="footer">Miłego dnia, Walentynko 😘</div>
    </div>
  </div>

  <script>
    const noBtn = document.getElementById("noBtn");
    const yesBtn = document.getElementById("yesBtn");
    const btnArea = document.getElementById("btnArea");
    const resultBox = document.getElementById("resultBox");

    function moveNoButton() {
      const areaRect = btnArea.getBoundingClientRect();
      const btnRect = noBtn.getBoundingClientRect();

      const maxX = areaRect.width - btnRect.width;
      const maxY = areaRect.height - btnRect.height;

      const x = Math.random() * Math.max(10, maxX);
      const y = Math.random() * Math.max(10, maxY);

      noBtn.style.left = `${x}px`;
      noBtn.style.top = `${y}px`;
    }

    noBtn.addEventListener("mouseenter", moveNoButton);

    noBtn.addEventListener("touchstart", (e) => {
      e.preventDefault();
      moveNoButton();
    }, { passive: false });

    // -------------------------
    // CONFETTI 🎉
    // -------------------------
    const canvas = document.getElementById("confettiCanvas");
    const ctx = canvas.getContext("2d");

    function resizeCanvas() {
      canvas.width = window.innerWidth * devicePixelRatio;
      canvas.height = window.innerHeight * devicePixelRatio;
      ctx.setTransform(devicePixelRatio, 0, 0, devicePixelRatio, 0, 0);
    }
    window.addEventListener("resize", resizeCanvas);
    resizeCanvas();

    let confettiPieces = [];
    let confettiRunning = false;

    function random(min, max) {
      return Math.random() * (max - min) + min;
    }

    function createConfetti(count = 160) {
      confettiPieces = [];
      for (let i = 0; i < count; i++) {
        confettiPieces.push({
          x: random(0, window.innerWidth),
          y: random(-window.innerHeight, 0),
          w: random(6, 12),
          h: random(10, 18),
          vx: random(-2.5, 2.5),
          vy: random(3, 7),
          rot: random(0, Math.PI * 2),
          vr: random(-0.2, 0.2),
          shape: Math.random() > 0.5 ? "rect" : "circle"
        });
      }
    }

    function drawConfetti() {
      ctx.clearRect(0, 0, window.innerWidth, window.innerHeight);

      for (const p of confettiPieces) {
        ctx.save();
        ctx.translate(p.x, p.y);
        ctx.rotate(p.rot);

        const hue = Math.floor((p.x + p.y) % 360);
        ctx.fillStyle = `hsl(${hue}, 90%, 60%)`;

        if (p.shape === "rect") {
          ctx.fillRect(-p.w / 2, -p.h / 2, p.w, p.h);
        } else {
          ctx.beginPath();
          ctx.arc(0, 0, p.w / 2, 0, Math.PI * 2);
          ctx.fill();
        }

        ctx.restore();
      }
    }

    function updateConfetti() {
      for (const p of confettiPieces) {
        p.x += p.vx;
        p.y += p.vy;
        p.rot += p.vr;

        if (p.y > window.innerHeight + 30) {
          p.y = random(-200, -50);
          p.x = random(0, window.innerWidth);
        }
        if (p.x < -30) p.x = window.innerWidth + 30;
        if (p.x > window.innerWidth + 30) p.x = -30;
      }
    }

    function runConfetti(durationMs = 3500) {
      confettiRunning = true;
      createConfetti(180);

      const start = performance.now();

      function loop(now) {
        if (!confettiRunning) return;

        updateConfetti();
        drawConfetti();

        if (now - start < durationMs) {
          requestAnimationFrame(loop);
        } else {
          confettiRunning = false;
          ctx.clearRect(0, 0, window.innerWidth, window.innerHeight);
        }
      }

      requestAnimationFrame(loop);
    }

    // -------------------------
    // LECĄCE SERDUSZKA ❤️
    // -------------------------
    function spawnHearts(durationMs = 4200) {
      const start = performance.now();

      const interval = setInterval(() => {
        const heart = document.createElement("div");
        heart.className = "heart";

        // różne serduszka
        const hearts = ["❤️","💖","💘","💗","💕","💞"];
        heart.textContent = hearts[Math.floor(Math.random() * hearts.length)];

        // losowe parametry lotu
        const x = Math.floor(random(-220, 220)) + "px";
        const r = Math.floor(random(-35, 35)) + "deg";
        const s = random(0.8, 1.6);

        heart.style.setProperty("--x", x);
        heart.style.setProperty("--r", r);
        heart.style.setProperty("--s", s);

        // start z losowego miejsca na dole
        heart.style.left = random(15, 85) + "vw";
        heart.style.fontSize = random(18, 34) + "px";

        document.body.appendChild(heart);

        // usuń po animacji
        setTimeout(() => heart.remove(), 2800);

        // stop po czasie
        if (performance.now() - start > durationMs) {
          clearInterval(interval);
        }
      }, 90);
    }

    // klik TAK
    yesBtn.addEventListener("click", () => {
      resultBox.style.display = "block";
      btnArea.style.display = "none";

      runConfetti(4200);
      spawnHearts(4200);
    });
  </script>
</body>
</html>
