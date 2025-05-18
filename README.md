<!DOCTYPE html>
<html lang="tr">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Romantik Gizli Site</title>
<style>
  body, html {
    margin: 0; padding: 0; height: 100%;
    background: radial-gradient(circle at center, #ffe6e6, #ffb3b3);
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    overflow: hidden;
    color: #fff;
  }

  #login {
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background: rgba(0,0,0,0.4);
    backdrop-filter: blur(10px);
    padding: 20px;
  }

  #login input {
    padding: 15px;
    font-size: 18px;
    border-radius: 10px;
    border: none;
    width: 80%;
    max-width: 300px;
    text-align: center;
    margin-bottom: 15px;
  }

  #login button {
    padding: 15px 30px;
    font-size: 18px;
    background: #ff4d6d;
    border: none;
    border-radius: 10px;
    color: white;
    cursor: pointer;
    transition: background 0.3s ease;
  }

  #login button:hover {
    background: #e60039;
  }

  #error {
    color: #ffd6d6;
    margin-top: 10px;
    text-align: center;
  }

  #romantic-scene {
    display: none;
    height: 100vh;
    background: linear-gradient(to top right, #ffccd5, #ff4d6d);
    flex-direction: column;
    justify-content: center;
    align-items: center;
    position: relative;
    overflow: hidden;
    text-align: center;
    padding: 20px;
    backdrop-filter: blur(3px);
  }

  h1 {
    font-size: 3rem;
    margin-bottom: 1rem;
    text-shadow: 0 0 15px #fff;
  }

  p {
    font-size: 1.5rem;
    max-width: 700px;
    line-height: 1.5;
    text-shadow: 0 0 8px #fff;
  }

  .heart {
    position: absolute;
    bottom: -50px;
    width: 30px;
    height: 30px;
    background-color: #ff1a3c;
    transform: rotate(45deg);
    animation: flyUp linear forwards;
    opacity: 0.8;
  }

  .heart:before,
  .heart:after {
    content: "";
    position: absolute;
    width: 30px;
    height: 30px;
    background-color: #ff1a3c;
    border-radius: 50%;
  }

  .heart:before { top: -15px; left: 0; }
  .heart:after { left: 15px; top: 0; }

  @keyframes flyUp {
    0% { transform: translateY(0) rotate(45deg); opacity: 0.9; }
    100% { transform: translateY(-900px) rotate(45deg); opacity: 0; }
  }

  #romantic-gif {
    width: 200px;
    height: auto;
    margin-top: 30px;
    border-radius: 50%;
    box-shadow: 0 0 40px rgba(255, 77, 109, 0.8);
    border: 4px solid #fff;
  }

  @media (max-width: 600px) {
    h1 { font-size: 2rem; }
    p { font-size: 1.2rem; }
    #login input, #login button { font-size: 16px; width: 90%; }
  }
</style>
</head>
<body>

<div id="login">
  <h2>🔒 Romantik Portal Girişi</h2>
  <input type="password" id="password" placeholder="Şifreni yaz..." />
  <button onclick="checkPassword()">Giriş Yap</button>
  <p id="error"></p>
</div>

<div id="romantic-scene">
  <h1>Sonsuz Aşkımıza ❤️</h1>
  <p>Gözlerin parlayan bir yıldız gibi...<br>Kalbim, seninle tamamlanan bir şiir.<br>Hayatımda olduğun için şükrediyorum...</p>
  <h2 id="final-message" style="display:none; font-size: 2rem; color: #fff; margin-top: 30px; text-shadow: 0 0 20px #ff4d6d;">
    💖 Artık Kalbimin Sahibisin 💖
  </h2>
  <img id="romantic-gif" style="display: none;" src="https://media.giphy.com/media/3og0IPxMM0erATueVW/giphy.gif" alt="Kalp Gif">
  <canvas id="confetti-canvas" style="position:absolute; top:0; left:0; width:100%; height:100%; pointer-events:none;"></canvas>
</div>

<script>
  const correctPassword = "AŞKIM";

  function checkPassword() {
    const input = document.getElementById("password").value;
    const error = document.getElementById("error");
    if (input === correctPassword) {
      document.getElementById("login").style.display = "none";
      const scene = document.getElementById("romantic-scene");
      scene.style.display = "flex";
      error.textContent = "";
      createHearts();
      showFinalMessage();
      startConfetti();
    } else {
      error.textContent = "⚠️ Şifre yanlış, tekrar dene!";
    }
  }

  function createHearts() {
    const scene = document.getElementById("romantic-scene");
    setInterval(() => {
      const heart = document.createElement("div");
      heart.classList.add("heart");
      heart.style.left = Math.random() * window.innerWidth + "px";
      heart.style.animationDuration = (3 + Math.random() * 3) + "s";
      scene.appendChild(heart);
      setTimeout(() => heart.remove(), 6000);
    }, 300);
  }

  function showFinalMessage() {
    setTimeout(() => {
      document.getElementById("final-message").style.display = "block";
      document.getElementById("romantic-gif").style.display = "block";
    }, 2000);
  }

  function startConfetti() {
    const canvas = document.getElementById("confetti-canvas");
    const ctx = canvas.getContext("2d");
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    window.addEventListener("resize", () => {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    });

    const particles = [];
    for (let i = 0; i < 150; i++) {
      particles.push({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        r: Math.random() * 6 + 2,
        dx: Math.random() * 4 - 2,
        dy: Math.random() * -3 - 2,
        color: `hsl(${Math.random() * 360}, 100%, 70%)`
      });
    }

    function draw() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      particles.forEach(p => {
        ctx.beginPath();
        ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
        ctx.fillStyle = p.color;
        ctx.fill();
      });
    }

    function update() {
      particles.forEach(p => {
        p.x += p.dx;
        p.y += p.dy;
        if (p.y < 0) {
          p.y = canvas.height;
          p.x = Math.random() * canvas.width;
        }
      });
    }

    function animate() {
      draw();
      update();
      requestAnimationFrame(animate);
    }

    animate();
  }
</script>

</body>
</html>
