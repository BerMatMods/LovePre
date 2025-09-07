
    let isPlaying = false;
    const musicBtn = document.getElementById('musicBtn');

    function playMusic() {
      audio.play().then(() => {
        musicBtn.textContent = '❚❚';
        isPlaying = true;
      }).catch(e => {
        console.log("Autoplay bloqueado. Haz clic manualmente.");
        musicBtn.textContent = '♪';
      });
    }

    // Intentar autoplay
    document.addEventListener('click', playMusicOnce);
    function playMusicOnce() {
      playMusic();
      document.removeEventListener('click', playMusicOnce);
    }

    musicBtn.addEventListener('click', () => {
      if (isPlaying) {
        audio.pause();
        musicBtn.textContent = '♪';
      } else {
        playMusic();
      }
      isPlaying = !isPlaying;
    });

    // --- Pantalla de carga ---
    const loader = document.getElementById('loader');
    const progressBar = document.getElementById('progressBar');
    let width = 0;
    const interval = setInterval(() => {
      if (width >= 100) {
        clearInterval(interval);
        loader.style.opacity = '0';
        setTimeout(() => {
          loader.style.display = 'none';
          document.body.style.overflow = 'auto';
          document.getElementById('mainCard').classList.add('show');
          typeWriter(document.getElementById('loveMessage'), "Desde que llegaste, cada día tiene más color, más sentido, más amor. Eres mi refugio, mi alegría, mi razón de sonreír.", 60);
        }, 600);
      } else {
        width++;
        progressBar.style.width = width + '%';
      }
    }, 50);

    // --- Lluvia de palabras ---
    const romanticWords = ["Te amo", "Eres mi todo", "Mi corazón", "Para siempre", "Mi vida", "Gracias por existir", "Eres mi hogar", "Mi alma", "Mi paz", "Siempre contigo"];
    const loveRain = document.getElementById('loveRain');
    setInterval(() => {
      const word = document.createElement('div');
      word.className = 'love-word';
      word.textContent = romanticWords[Math.floor(Math.random() * romanticWords.length)];
      word.style.left = Math.random() * 100 + 'vw';
      word.style.animationDuration = 8 + Math.random() * 10 + 's';
      word.style.fontSize = (18 + Math.random() * 10) + 'px';
      loveRain.appendChild(word);
      setTimeout(() => word.remove(), 16000);
    }, 500);

    // --- Explosión de corazones ---
    document.body.addEventListener('click', (e) => {
      const hearts = ['❤️', '💖', '💗', '💕', '💞', '💘', '💓', '💝', '💟', '💘'];
      for (let i = 0; i < 30; i++) {
        const heart = document.createElement('div');
        heart.className = 'heart-particle';
        heart.textContent = hearts[Math.floor(Math.random() * hearts.length)];
        heart.style.left = `${e.clientX}px`;
        heart.style.top = `${e.clientY}px`;
        document.body.appendChild(heart);
        gsap.to(heart, {
          x: (Math.random() - 0.5) * 200,
          y: -120 - Math.random() * 100,
          opacity: 0,
          duration: 1.8 + Math.random() * 0.4,
          ease: 'power2.out',
          onComplete: () => heart.remove()
        });
      }
    });

    // --- Menú ---
    document.getElementById('menuToggle').addEventListener('click', () => {
      document.getElementById('menuToggle').classList.toggle('active');
      document.getElementById('menu').classList.toggle('active');
    });

    // --- Carta con corazones ---
    document.getElementById('heartBtn').addEventListener('click', () => {
      document.getElementById('letterModal').style.display = 'flex';
      typeWriterWithHearts(document.getElementById('letterText'), `Desde el primer momento supe que eras especial...`);
    });

    document.getElementById('closeBtn').addEventListener('click', () => {
      document.getElementById('letterModal').style.display = 'none';
    });

    function typeWriter(element, text, speed = 50) {
      let i = 0;
      element.textContent = '';
      const timer = setInterval(() => {
        if (i < text.length) {
          element.textContent += text.charAt(i);
          i++;
        } else {
          element.classList.add('show');
          clearInterval(timer);
        }
      }, speed);
    }

    function typeWriterWithHearts(element, text, speed = 45) {
      let i = 0;
      element.textContent = '';
      const hearts = ['❤️', '💖', '💗', '💕', '💞'];
      const container = document.querySelector('.modal-content');
      const timer = setInterval(() => {
        if (i < text.length) {
          element.textContent += text.charAt(i);
          i++;
          if (i % 10 === 0) {
            const heart = document.createElement('div');
            heart.className = 'typing-heart';
            heart.textContent = hearts[Math.floor(Math.random() * hearts.length)];
            heart.style.left = (Math.random() * 80 + 10) + 'vw';
            heart.style.top = (Math.random() * 60 + 20) + 'vh';
            container.appendChild(heart);
            setTimeout(() => heart.remove(), 3000);
          }
        } else {
          clearInterval(timer);
        }
      }, speed);
    }

    // --- Corazones flotantes ---
    window.onload = () => {
      const container = document.getElementById('floatingHearts');
      const hearts = ['❤', '💖', '💗', '💕', '💞'];
      setInterval(() => {
        const h = document.createElement('div');
        h.className = 'heart-float';
        h.textContent = hearts[Math.floor(Math.random() * hearts.length)];
        h.style.left = Math.random() * 100 + 'vw';
        h.style.fontSize = (20 + Math.random() * 12) + 'px';
        h.style.animationDuration = '14s, 3s';
        container.appendChild(h);
        setTimeout(() => h.remove(), 18000);
      }, 800);
    };
  </script>
</body>
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>Para Mi Novia BCode</title>
  <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Nunito:wght@600;700&family=Great+Vibes&family=Montserrat:wght@400;500&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      -webkit-tap-highlight-color: transparent;
    }

    html, body {
      height: 100%;
      overflow: hidden;
      font-family: 'Montserrat', sans-serif;
      background: #1a0020;
      color: #ff80c4;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    /* Fondo rosado saturado y brillante */
    body::before {
      content: '';
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: radial-gradient(circle at center,
        rgba(255, 80, 160, 0.5) 0%,
        rgba(230, 50, 140, 0.6) 70%,
        rgba(180, 20, 100, 0.7) 100%);
      z-index: -2;
    }

    body::after {
      content: '';
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(255, 100, 180, 0.3);
      backdrop-filter: blur(15px);
      z-index: -1;
    }

    /* Lluvia de palabras amorosas */
    .love-rain {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: -1;
      display: flex;
      justify-content: center;
    }

    .love-word {
      position: absolute;
      color: #ff6b9e;
      font-size: 1.5rem;
      font-weight: bold;
      opacity: 0.95;
      text-shadow: 0 0 15px rgba(255, 107, 158, 0.8);
      animation: fall linear infinite;
      white-space: nowrap;
      font-family: 'Nunito', cursive;
      transform: translateX(-50%);
    }

    @keyframes fall {
      to { transform: translateY(100vh) translateX(-50%); }
    }

    /* Pantalla de carga */
    #loader {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(20, 5, 30, 0.98);
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      z-index: 2000;
      text-align: center;
      padding: 20px;
    }

    .loader-title {
      font-family: 'Great Vibes', cursive;
      font-size: 3.8rem;
      background: linear-gradient(45deg, #ff6b9e, #ff9ec6);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
      margin-bottom: 30px;
      text-shadow: 0 0 20px rgba(255, 107, 158, 0.7);
    }

    .loader-text {
      font-size: 1.8rem;
      color: #ff80c4;
      margin-bottom: 50px;
      font-weight: 500;
      text-shadow: 0 0 12px rgba(255, 107, 158, 0.6);
    }

    .progress-bar {
      width: 90%;
      max-width: 500px;
      height: 22px;
      background: rgba(255, 107, 158, 0.4);
      border-radius: 11px;
      overflow: hidden;
      margin: 45px 0;
      box-shadow: 0 0 18px rgba(255, 107, 158, 0.6) inset;
    }

    .progress {
      width: 0%;
      height: 100%;
      background: linear-gradient(90deg, #ff6b9e, #ff33cc);
      border-radius: 11px;
      transition: width 0.1s linear;
      box-shadow: 0 0 25px rgba(255, 107, 158, 0.9);
    }

    .loader-info {
      margin-top: 50px;
      font-size: 1.4rem;
      color: #ff80c4;
      max-width: 90%;
      line-height: 1.9;
      text-shadow: 0 0 10px rgba(255, 107, 158, 0.6);
    }

    .loader-info a {
      color: #ff6b9e;
      text-decoration: none;
      font-weight: bold;
      border-bottom: 2px dotted #ff6b9e;
      padding-bottom: 4px;
    }

    .loader-info a:hover {
      color: #fff;
      text-shadow: 0 0 15px rgba(255, 107, 158, 0.8);
    }

    /* Corazones flotantes */
    .floating-hearts {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: 1;
    }

    .heart-float {
      position: absolute;
      font-size: 28px;
      opacity: 0;
      animation: floatUp 18s infinite, blink 3s infinite;
      text-shadow: 0 0 20px #ff9ec6;
      z-index: 1;
    }

    @keyframes floatUp {
      0% { transform: translateY(100vh); opacity: 0; }
      10% { opacity: 1; }
      90% { opacity: 1; }
      100% { transform: translateY(-30vh); opacity: 0; }
    }

    @keyframes blink {
      0%, 100% { opacity: 0.6; }
      50% { opacity: 1; }
    }

    /* Menú de 3 rayas */
    .menu-toggle {
      position: fixed;
      top: 25px;
      left: 25px;
      width: 50px;
      height: 50px;
      background: rgba(255, 107, 158, 0.2);
      border-radius: 50%;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      cursor: pointer;
      z-index: 100;
      box-shadow: 0 0 20px rgba(255, 107, 158, 0.7);
      border: 3px solid #ff6b9e;
    }

    .bar {
      width: 24px;
      height: 4px;
      background: #ff9ec6;
      margin: 5px auto;
      border-radius: 2px;
      box-shadow: 0 0 6px rgba(255, 0, 255, 0.6);
    }

    .menu {
      position: fixed;
      top: 90px;
      left: 25px;
      width: 270px;
      background: rgba(30, 5, 40, 0.95);
      backdrop-filter: blur(12px);
      border-radius: 18px;
      padding: 22px;
      box-shadow: 0 0 30px rgba(255, 107, 158, 0.6);
      z-index: 99;
      opacity: 0;
      visibility: hidden;
      transform: translateY(-15px);
      transition: all 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);
    }

    .menu.active {
      opacity: 1;
      visibility: visible;
      transform: translateY(0);
    }

    .menu a {
      display: block;
      color: #ff80c4;
      text-decoration: none;
      font-size: 18px;
      font-weight: bold;
      padding: 16px 20px;
      border-radius: 14px;
      margin-bottom: 14px;
      background: rgba(255, 107, 158, 0.15);
      text-align: center;
      transition: all 0.3s ease;
      border: 2px solid rgba(255, 107, 158, 0.4);
    }

    .menu a:hover {
      background: rgba(255, 107, 158, 0.4);
      transform: scale(1.1);
      color: #fff;
      box-shadow: 0 0 25px rgba(255, 0, 255, 0.7);
    }

    /* Botón de música */
    .music-btn {
      position: fixed;
      top: 25px;
      right: 25px;
      width: 55px;
      height: 55px;
      background: rgba(255, 107, 158, 0.25);
      border: 3px solid #ff6b9e;
      color: #ff9ec6;
      border-radius: 50%;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 1.5rem;
      cursor: pointer;
      z-index: 100;
      box-shadow: 0 0 25px rgba(255, 107, 158, 0.8);
    }

    .music-btn:hover {
      transform: scale(1.15);
      background: rgba(255, 107, 158, 0.4);
    }

    /* Contenedor principal */
    .container {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 100%;
      height: 100%;
      text-align: center;
    }

    /* Tarjeta principal */
    .card {
      width: 90%;
      max-width: 560px;
      background: rgba(40, 10, 50, 0.92);
      border-radius: 26px;
      border: 4px solid #ff6b9e;
      box-shadow: 
        0 0 40px rgba(255, 107, 158, 0.8),
        inset 0 0 25px rgba(255, 107, 158, 0.6);
      padding: 45px 40px;
      position: relative;
      z-index: 10;
      backdrop-filter: blur(10px);
      opacity: 0;
      transform: scale(0.9);
      transition: all 0.9s ease;
    }

    .card.show {
      opacity: 1;
      transform: scale(1);
    }

    .header h1 {
      font-family: 'Great Vibes', cursive;
      font-size: 3.3rem;
      background: linear-gradient(45deg, #ff6b9e, #ff9ec6);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
      margin-bottom: 35px;
      text-shadow: 0 0 20px rgba(255, 107, 158, 0.7);
      line-height: 1.3;
    }

    .photo-frame {
      width: 180px;
      height: 180px;
      margin: 30px auto 40px;
      border-radius: 50%;
      border: 6px solid transparent;
      background: linear-gradient(45deg, #ff6b9e, #ff9ec6) border-box;
      box-shadow: 0 0 40px #ff6b9e;
      padding: 12px;
      position: relative;
      animation: pulse 2s infinite alternate;
      overflow: hidden;
    }

    @keyframes pulse {
      from { box-shadow: 0 0 25px #ff6b9e; }
      to { box-shadow: 0 0 60px #ff6b9e; }
    }

    .photo-frame img {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      object-fit: cover;
      border: 4px solid #fff;
      animation: rotate 12s linear infinite;
    }

    @keyframes rotate {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    .message {
      font-family: 'Nunito', cursive;
      font-size: 1.4rem;
      line-height: 1.95;
      color: #ff80c4;
      margin: 35px auto;
      max-width: 95%;
      opacity: 0;
    }

    .message.show {
      animation: fadeInUp 1.5s ease forwards;
    }

    @keyframes fadeInUp {
      to { opacity: 1; transform: translateY(0); }
    }

    .heart-btn {
      background: linear-gradient(145deg, #d6006c, #ff00ff);
      color: white;
      border: none;
      padding: 20px 45px;
      border-radius: 60px;
      font-size: 1.4rem;
      cursor: pointer;
      margin: 40px auto 35px;
      box-shadow: 0 0 35px rgba(255, 0, 255, 0.8);
      transition: all 0.3s ease;
      font-weight: bold;
      display: block;
      text-shadow: 0 0 8px rgba(255, 255, 255, 0.9);
    }

    .heart-btn:hover {
      transform: scale(1.12);
      box-shadow: 0 0 50px rgba(255, 0, 255, 0.95);
    }

    .footer-credit {
      font-family: 'Dancing Script', cursive;
      font-size: 1.5rem;
      color: #ff80c4;
      margin-top: 40px;
      text-shadow: 0 0 15px rgba(255, 107, 158, 0.7);
    }

    /* Modal de carta */
    .modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(30, 5, 40, 0.96);
      z-index: 1000;
      justify-content: center;
      align-items: center;
      overflow-y: auto;
      padding: 20px;
    }

    .modal-content {
      width: 90%;
      max-width: 700px;
      background: rgba(40, 10, 50, 0.95);
      border-radius: 26px;
      border: 4px solid #ff6b9e;
      box-shadow: 0 0 50px rgba(255, 107, 158, 0.8);
      padding: 60px 50px;
      color: #ff80c4;
      text-align: center;
      position: relative;
      animation: fadeIn 0.9s ease;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: scale(0.9); }
      to { opacity: 1; transform: scale(1); }
    }

    .letter-title {
      font-family: 'Great Vibes', cursive;
      font-size: 3.6rem;
      background: linear-gradient(45deg, #ff6b9e, #ff9ec6);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
      margin-bottom: 45px;
      text-shadow: 0 0 20px rgba(255, 107, 158, 0.7);
    }

    .letter-content {
      font-family: 'Nunito', cursive;
      font-size: 1.4rem;
      line-height: 2.1;
      text-align: left;
      color: #ff80c4;
      margin-bottom: 40px;
      padding: 0 35px;
      position: relative;
      z-index: 1;
    }

    .close-btn {
      position: fixed;
      top: 30px;
      right: 30px;
      width: 65px;
      height: 65px;
      background: rgba(30, 5, 40, 0.92);
      border: 3px solid #ff6b9e;
      color: #ff9ec6;
      border-radius: 50%;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 36px;
      cursor: pointer;
      z-index: 1001;
      box-shadow: 0 0 30px rgba(255, 107, 158, 0.8);
    }

    .close-btn:hover {
      transform: scale(1.18);
      color: #ff6b9e;
    }

    /* Explosiones de corazones */
    .heart-particle {
      position: absolute;
      font-size: 34px;
      pointer-events: none;
      z-index: 1000;
      user-select: none;
      animation: floatHeart 2.4s forwards;
    }

    @keyframes floatHeart {
      0% { transform: translateY(0) rotate(0deg); opacity: 1; }
      100% { transform: translateY(-150px) rotate(360deg); opacity: 0; }
    }

    /* Corazones al escribir */
    .typing-heart {
      position: absolute;
      font-size: 22px;
      opacity: 0;
      pointer-events: none;
      animation: floatTyping 3.2s forwards;
      z-index: 2;
    }

    @keyframes floatTyping {
      0% { transform: translateY(0) rotate(0deg); opacity: 0; }
      50% { opacity: 1; }
      100% { transform: translateY(-90px) rotate(360deg); opacity: 0; }
    }
  </style>
</head>
<body>

  <!-- Lluvia de palabras amorosas -->
  <div class="love-rain" id="loveRain"></div>
  <div class="floating-hearts" id="floatingHearts"></div>

  <!-- Pantalla de carga -->
  <div id="loader">
    <div style="text-align: center;">
      <div class="loader-title">Tu Sorpresa de Amor</div>
      <div class="loader-text">Cargando tu regalo...</div>
      <div class="progress-bar">
        <div class="progress" id="progressBar"></div>
      </div>
      <div class="loader-info">
        Creado con amor por <strong>AnthZz Berrocal BerMatMods</strong><br>
        <a href="https://wa.me/51930569195" target="_blank">💬 Personaliza tu versión</a>
      </div>
    </div>
  </div>

  <!-- Menú y música -->
  <div class="menu-toggle" id="menuToggle">
    <div class="bar"></div>
    <div class="bar"></div>
    <div class="bar"></div>
  </div>

  <div class="menu" id="menu">
    <a href="https://wa.me/51930569195" target="_blank">💬 Personaliza tu versión</a>
    <a href="https://wa.me/51930569195" target="_blank">📩 Escríbeme por WhatsApp</a>
    <a href="https://wa.me/51930569195" target="_blank">❤️ Haz tu propia sorpresa</a>
  </div>

  <button class="music-btn" id="musicBtn">♪</button>

  <!-- Contenedor principal -->
  <div class="container">
    <div class="card" id="mainCard">
      <div class="header">
        <h1>Mi Amor, Eres Mi Todo</h1>
      </div>

      <div class="photo-frame">
        <img src="https://media1.giphy.com/media/v1.Y2lkPTZjMDliOTUyMXUxZTF5aHFocWVodnY0bnc1bG1kcGk0dm1rZ2dwNG5hemw1NjJzdSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/10l8fc00NMNJNm/giphy.gif" alt="Corazón animado">
      </div>

      <p class="message" id="loveMessage"></p>

      <button class="heart-btn" id="heartBtn">Ver Carta de Amor</button>
      <div class="footer-credit">By AnthZz Berrocal BerMatMods</div>
    </div>
  </div>

  <!-- Modal de carta -->
  <div class="modal" id="letterModal">
    <div class="modal-content">
      <h2 class="letter-title">Mi Amor...</h2>
      <div class="letter-content" id="letterText"></div>
    </div>
    <div class="close-btn" id="closeBtn">×</div>
  </div>

  <!-- Scripts -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
  <script>
    // ✅ Música segura para GitHub Pages
    const audio = new Audio('https://assets.mixkit.co/sfx/preview/mixkit-single-celestial-ding-269.mp3'); // ← Segura
    // Cambia por './music/those-eyes.mp3' cuando subas tu archivo

    let isPlaying = false;
    const musicBtn = document.getElementById('musicBtn');

    function playMusic() {
      audio.play().then(() => {
        musicBtn.textContent = '❚❚';
        isPlaying = true;
      }).catch(e => {
        console.log("Autoplay bloqueado. Haz clic manualmente.");
        musicBtn.textContent = '♪';
      });
    }

    // Intentar autoplay al primer clic
    document.addEventListener('click', playMusicOnce);
    function playMusicOnce() {
      playMusic();
      document.removeEventListener('click', playMusicOnce);
    }

    musicBtn.addEventListener('click', () => {
      if (isPlaying) {
        audio.pause();
        musicBtn.textContent = '♪';
      } else {
        playMusic();
      }
      isPlaying = !isPlaying;
    });

    // --- Pantalla de carga ---
    const loader = document.getElementById('loader');
    const progressBar = document.getElementById('progressBar');
    let width = 0;
    const interval = setInterval(() => {
      if (width >= 100) {
        clearInterval(interval);
        loader.style.opacity = '0';
        setTimeout(() => {
          loader.style.display = 'none';
          document.body.style.overflow = 'auto';
          document.getElementById('mainCard').classList.add('show');
          typeWriter(document.getElementById('loveMessage'), "Desde que llegaste, cada día tiene más color, más sentido, más amor. Eres mi refugio, mi alegría, mi razón de sonreír.", 60);
        }, 600);
      } else {
        width++;
        progressBar.style.width = width + '%';
      }
    }, 50);

    // --- Lluvia de palabras ---
    const romanticWords = ["Te amo", "Eres mi todo", "Mi corazón", "Para siempre", "Mi vida", "Gracias por existir", "Eres mi hogar", "Mi alma", "Mi paz", "Siempre contigo", "Te extraño", "Eres perfecta", "Eres mi sueño", "Mi eternidad"];
    const loveRain = document.getElementById('loveRain');
    setInterval(() => {
      const word = document.createElement('div');
      word.className = 'love-word';
      word.textContent = romanticWords[Math.floor(Math.random() * romanticWords.length)];
      word.style.left = Math.random() * 100 + 'vw';
      word.style.animationDuration = 8 + Math.random() * 10 + 's';
      word.style.fontSize = (20 + Math.random() * 10) + 'px';
      loveRain.appendChild(word);
      setTimeout(() => word.remove(), 16000);
    }, 500);

    // --- Explosión de 30 corazones en cada toque ---
    document.body.addEventListener('click', (e) => {
      const hearts = ['❤️', '💖', '💗', '💕', '💞', '💘', '💓', '💝', '💟', '💘'];
      for (let i = 0; i < 30; i++) {
        const heart = document.createElement('div');
        heart.className = 'heart-particle';
        heart.textContent = hearts[Math.floor(Math.random() * hearts.length)];
        heart.style.left = `${e.clientX}px`;
        heart.style.top = `${e.clientY}px`;
        document.body.appendChild(heart);
        gsap.to(heart, {
          x: (Math.random() - 0.5) * 200,
          y: -130 - Math.random() * 100,
          opacity: 0,
          duration: 1.8 + Math.random() * 0.4,
          ease: 'power2.out',
          onComplete: () => heart.remove()
        });
      }
    });

    // --- Menú ---
    document.getElementById('menuToggle').addEventListener('click', () => {
      document.getElementById('menuToggle').classList.toggle('active');
      document.getElementById('menu').classList.toggle('active');
    });

    // --- Carta con texto completo y corazones ---
    document.getElementById('heartBtn').addEventListener('click', () => {
      document.getElementById('letterModal').style.display = 'flex';
      typeWriterWithHearts(document.getElementById('letterText'), `Desde el primer momento supe que eras especial. No por lo que dices, sino por cómo me hace sentir tu presencia. Tu mirada calma mis tormentas, tu voz es mi canción favorita, y tu amor es el único hogar que he conocido.

Cada día a tu lado es un regalo. No necesito palabras grandiosas para decirte lo que siento, porque cada gesto, cada sonrisa, cada silencio entre nosotros, habla de un amor verdadero.

No quiero un amor de momentos, quiero un amor de toda la vida. Quiero amarte en las mañanas con café, en las noches con abrazos, en los días difíciles con fuerza, y en los felices con más risas.

Eres mi todo. Mi presente, mi futuro, mi eternidad. Y si el universo me da la oportunidad, elegiría mil veces volver a encontrarte, mil veces volver a enamorarme de ti.

Gracias por ser tú, por amar, por existir. Este regalo es solo una pequeña muestra de lo que siento.`, 45);
    });

    document.getElementById('closeBtn').addEventListener('click', () => {
      document.getElementById('letterModal').style.display = 'none';
    });

    // --- Efecto de escritura ---</html>
