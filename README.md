<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Sorry Message</title>
  <style>
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(135deg, #1a1a2e, #16213e);
      color: #ffffff;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      overflow: hidden;
      flex-direction: column;
      text-align: center;
      transition: background 0.5s, color 0.5s;
    }
    .hidden {
      display: none;
    }
    .unlock-section, .letter {
      background: rgba(255, 255, 255, 0.05);
      padding: 3rem;
      border-radius: 20px;
      box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
      backdrop-filter: blur(8px);
      -webkit-backdrop-filter: blur(8px);
      border: 1px solid rgba(255, 255, 255, 0.18);
    }
    .game-section {
      text-align: center;
    }
    .letter {
      animation: fadeIn 1s ease-in-out;
      font-size: 1.1rem;
      line-height: 1.8;
      max-width: 700px;
    }
    .unlock-button, .theme-toggle {
      background: #3498db;
      color: white;
      padding: 0.8rem 2rem;
      border: none;
      border-radius: 12px;
      font-size: 1rem;
      cursor: pointer;
      margin-top: 1.5rem;
      transition: 0.3s;
    }
    .unlock-button:hover, .theme-toggle:hover {
      background: #2980b9;
    }
    input[type="password"] {
      padding: 0.7rem;
      font-size: 1rem;
      border-radius: 8px;
      border: none;
      margin-top: 1rem;
      width: 80%;
      background: #eeeeee;
    }
    .gift {
      width: 80px;
      position: absolute;
      top: 100px;
      left: 100px;
      cursor: pointer;
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }
    .theme-toggle {
      position: absolute;
      top: 20px;
      right: 20px;
    }
    .heart {
      position: fixed;
      bottom: -20px;
      width: 15px;
      height: 15px;
      background: pink;
      transform: rotate(45deg);
      animation: floatUp 5s linear forwards;
      opacity: 0.7;
      z-index: 1;
      pointer-events: none;
    }
    .heart::before, .heart::after {
      content: '';
      position: absolute;
      width: 15px;
      height: 15px;
      background: inherit;
      border-radius: 50%;
    }
    .heart::before {
      top: -7.5px;
      left: 0;
    }
    .heart::after {
      left: 7.5px;
      top: 0;
    }
    @keyframes floatUp {
      0% { transform: translateY(0) rotate(45deg); opacity: 0.7; }
      100% { transform: translateY(-600px) rotate(45deg); opacity: 0; }
    }
  </style>
</head>
<body>
  <!-- Background Music -->
  <audio id="bg-music" src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-17.mp3" loop></audio>

  <button class="theme-toggle" onclick="toggleTheme()">Toggle Theme</button>

  <div class="unlock-section" id="unlockSection">
    <h2>Write the password</h2>
    <input type="password" id="password" placeholder="Enter the password...">
    <br>
    <button class="unlock-button" onclick="checkPassword()">Unlock</button>
    <p id="hint" class="hidden" style="color: #4fc3f7; margin-top: 1rem;"></p>
  </div>

  <div class="game-section hidden" id="gameSection">
    <h2 style="color: #4fc3f7;">Catch the 🌷 Tulip if you can! 😝</h2>
    <span class="gift" id="gift">🌷</span>
  </div>

  <div class="letter hidden" id="letter">
    <h2 id="letterTitle" style="color: #4fc3f7;">Mrooosh xofi ana 3rf bli ghlt bzf o am srry 3la kolchi drto lik</h2>
    <div id="letterContent"></div>
  </div>

  <script>
    const unlockSection = document.getElementById('unlockSection');
    const gameSection = document.getElementById('gameSection');
    const letter = document.getElementById('letter');
    const hint = document.getElementById('hint');
    const gift = document.getElementById('gift');
    const bgMusic = document.getElementById('bg-music');
    const letterContent = document.getElementById('letterContent');
    let attempts = 0;
    let isDarkMode = true;

    const validPasswords = ["27/5/2024"];

    function showGame() {
      unlockSection.style.display = 'none';
      gameSection.classList.remove('hidden');
    }

    function checkPassword() {
      const input = document.getElementById('password').value;
      if (validPasswords.includes(input)) {
        showGame();
      } else {
        attempts++;
        if (attempts >= 3) {
          hint.classList.remove('hidden');
          hint.innerText = "Hint: lyom li tsa7bna fih ❤️";
        }
        alert("Wrong password 😔 Try again or catch the tulip!");
      }
    }

    function moveGiftRandomly() {
      const x = Math.random() * (window.innerWidth - 80);
      const y = Math.random() * (window.innerHeight - 80);
      gift.style.left = `${x}px`;
      gift.style.top = `${y}px`;
    }

    gift.addEventListener('click', () => {
      gameSection.style.display = 'none';
      letter.classList.remove('hidden');
      bgMusic.play().then(() => {
        console.log("Music started! 🎶");
      }).catch((error) => {
        console.log("Music play failed:", error);
      });
      startTypewriter();
      startHearts();
    });

    setInterval(moveGiftRandomly, 2000);

    const paragraphs = [
      "Kont mrid frasi kont mkn3rfx ntsrf kont anani kont insan mytklx 3lih ana am srry ana ndmt 3la hdchi kaml ana ghlt o jit bx nsl7 ghlti db.",
      "Bghit n9olik sorry 3la kolchi ana 3nitha bs7 makntmnax ntfar9 m3ak --- kan bzaf 3lya w 7sit eni t9il m3jbnix l7al wa5a 5litk fei lwa9t li kont m7tajk fih rah nti kolchi o ana bs7 kn3tdr.",
      "L9it rasi dayr m3ak ma bghitkch tfhmna b7al ma kanch 3ndna 9w8t mn awal --- Daba m3ak bghit rj3 l3la9a li beynatna 7sn mn lawl sffff ana 4lt o ana 3arf.",
      "Wlakin ana kn7md rbi 3la had lmaw9f 3rft bli nti konti insana 79i9ya m3aya 3rft bli kolchi kan s7 binatna o nti kan m3ak l79 kaml mlol hdxi ana ghaytmni forever.",
      "Sf 3rft rasi m3 x5s al s7 o 3rft bli nti konti hya alhdya li rbi 3tani liha nti hya mlja2 dyali.",
      "Ana takd bli nti hya li 5asni ntay9 fiha li 5asni 💍.",
      "Ana knbghik bzf o yarbi kolchi yrj3 b7al lawl tani o 7sn💝."
    ];

    let messageIndex = 0;
    let charIndex = 0;
    let word = '';

    function startTypewriter() {
      word = paragraphs[messageIndex];
      typeChar();
    }

    function typeChar() {
      if (charIndex < word.length) {
        letterContent.innerHTML += word.charAt(charIndex);
        charIndex++;
        setTimeout(typeChar, 20);
      } else {
        messageIndex++;
        if (messageIndex < paragraphs.length) {
          letterContent.innerHTML += "<br><br>";
          charIndex = 0;
          word = paragraphs[messageIndex];
          setTimeout(typeChar, 500);
        }
      }
    }

    function toggleTheme() {
      isDarkMode = !isDarkMode;
      document.body.style.background = isDarkMode
        ? 'linear-gradient(135deg, #1a1a2e, #16213e)'
        : 'linear-gradient(135deg, #f8f9fa, #e0e0e0)';
      document.body.style.color = isDarkMode ? '#ffffff' : '#000000';
    }

    function getRandomHeartColor() {
      if (isDarkMode) {
        const darkColors = ['#4fc3f7', '#9c27b0', '#ff4081'];
        return darkColors[Math.floor(Math.random() * darkColors.length)];
      } else {
        const lightColors = ['#ff8a80', '#ff80ab', '#ffb74d'];
        return lightColors[Math.floor(Math.random() * lightColors.length)];
      }
    }

    function createHeart() {
      const heart = document.createElement('div');
      heart.className = 'heart';
      heart.style.left = Math.random() * 100 + 'vw';
      heart.style.background = getRandomHeartColor();
      document.body.appendChild(heart);
      setTimeout(() => {
        heart.remove();
      }, 5000);
    }

    function startHearts() {
      setInterval(createHeart, 300);
    }
  </script>
</body>
</html>
