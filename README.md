<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Birthday Surprise 💗</title>

<style>
*{
  box-sizing:border-box;
}

body{
  margin:0;
  min-height:100vh;
  overflow:hidden;
  display:flex;
  justify-content:center;
  align-items:center;
  font-family:Arial,sans-serif;
  color:white;
  background:
    radial-gradient(circle at 15% 10%,#702c72,transparent 30%),
    radial-gradient(circle at 90% 90%,#382064,transparent 30%),
    linear-gradient(135deg,#08040d,#210b29,#0b0610);
}

.card{
  width:92%;
  max-width:540px;
  max-height:92vh;
  overflow:auto;
  padding:35px 25px;
  text-align:center;
  border-radius:30px;
  background:rgba(255,255,255,.08);
  border:1px solid rgba(255,255,255,.2);
  backdrop-filter:blur(18px);
  box-shadow:0 25px 80px rgba(0,0,0,.5);
}

h1{
  font-size:clamp(30px,8vw,48px);
  line-height:1.2;
}

.sparkle,.heart{
  animation:pulse 1.5s infinite;
}

.sparkle{
  font-size:50px;
}

.heart{
  font-size:65px;
}

.subtitle{
  line-height:1.7;
  opacity:.85;
}

input{
  width:100%;
  padding:16px;
  margin:20px 0 15px;
  border-radius:15px;
  border:1px solid #ff69b4;
  outline:none;
  background:rgba(0,0,0,.25);
  color:white;
  text-align:center;
  font-size:16px;
}

input::placeholder{
  color:#cbbccc;
}

button{
  padding:14px 24px;
  margin:6px;
  border:none;
  border-radius:50px;
  color:white;
  font-size:15px;
  font-weight:bold;
  cursor:pointer;
  background:linear-gradient(135deg,#ff4f9a,#9d6cff);
  box-shadow:0 8px 28px rgba(255,79,154,.3);
  transition:.25s;
}

button:hover{
  transform:translateY(-2px) scale(1.03);
}

#wish,
#ending{
  display:none;
}

.shayari{
  margin:22px 0;
  padding:20px;
  border-radius:22px;
  background:rgba(255,105,180,.08);
  border:1px solid rgba(255,105,180,.25);
}

.shayari p{
  font-size:17px;
  line-height:1.9;
  font-style:italic;
}

.message{
  font-size:18px;
  line-height:1.8;
}

.small{
  font-size:13px;
  opacity:.6;
}

.typing{
  min-height:55px;
  font-size:18px;
  line-height:1.7;
}

.float{
  position:fixed;
  bottom:-50px;
  pointer-events:none;
  animation:floatUp 5s linear forwards;
  z-index:10;
}

@keyframes pulse{
  50%{
    transform:scale(1.1);
  }
}

@keyframes floatUp{
  to{
    transform:translateY(-110vh) rotate(360deg);
    opacity:0;
  }
}
</style>
</head>

<body>

<!-- FIRST SCREEN -->

<div class="card" id="start">

  <div class="sparkle">✨</div>

  <h1>
    A Little Surprise For You 💗
  </h1>

  <p class="subtitle">
    Pehle apna naam likho...<br>
    phir tumhare liye ek chhota sa surprise hai 💌
  </p>

  <input
    id="name"
    maxlength="30"
    placeholder="Your beautiful name..."
  >

  <button onclick="showWish()">
    Open My Surprise 💌
  </button>

  <p class="small">
    Made with good wishes & a little courage ✨
  </p>

</div>


<!-- BIRTHDAY SCREEN -->

<div class="card" id="wish">

  <div class="heart">
    💖
  </div>

  <h1>
    Happy Birthday,<br>
    <span id="person"></span>! 🎂
  </h1>

  <p class="typing" id="typing"></p>


  <!-- SHAYARI -->

  <div class="shayari">

    <div style="font-size:30px;">
      🌸
    </div>

    <p>

      Chand bhi aaj thoda sa sharma raha hoga,<br>

      kyunki aaj usse bhi koi zyada pyaara
      nazar aa raha hoga. ✨

      <br>

      Dua hai tumhari har khushi
      tum tak khud chal kar aaye,

      <br>

      aur tumhari har subah
      ek khoobsurat muskaan laaye. 🌷

      <br><br>

      Bas aaj itna kehna hai...

      <br>

      <b>
        tumhari smile hamesha
        aise hi beautiful rahe. 💗
      </b>

    </p>

  </div>


  <button onclick="playShayari()">
    🔊 Shayari Suno
  </button>

  <button onclick="toggleMusic()" id="musicBtn">
    🎵 Play Soft Music
  </button>

  <br>

  <button onclick="showEnding()">
    One More Thing... 💝
  </button>

</div>


<!-- FINAL SCREEN -->

<div class="card" id="ending">

  <div class="heart">
    🫶
  </div>

  <h1>
    One Last Little Thing... 💌
  </h1>

  <p class="message">

    Some people make ordinary days
    feel a little more special
    just by being around. 🌸

    <br><br>

    So today, I just wanted to wish you
    a year full of happiness, laughter,
    beautiful memories and dreams
    coming true. ✨

  </p>

  <button onclick="finalReveal()">
    Read The Last Line 💗
  </button>

  <p
    id="lastLine"
    class="message">
  </p>

</div>


<script>

let audioCtx = null;
let musicTimer = null;
let musicOn = false;


/* OPEN SURPRISE */

function showWish(){

  const nameInput =
    document.getElementById("name");

  const name =
    nameInput.value.trim();

  if(!name){

    nameInput.focus();

    nameInput.placeholder =
      "Pehle apna naam toh likho 😄💗";

    return;
  }

  document.getElementById("person")
    .textContent = name;

  document.getElementById("start")
    .style.display = "none";

  document.getElementById("wish")
    .style.display = "block";

  createHearts();

  typeIntro();

  setTimeout(playShayari,500);

  setTimeout(() => {
    toggleMusic();
  },900);
}


/* TYPING EFFECT */

function typeIntro(){

  const text =
    "Wishing you a day as lovely, bright and wonderful as your smile. ✨";

  const box =
    document.getElementById("typing");

  box.textContent = "";

  let i = 0;

  function type(){

    if(i < text.length){

      box.textContent += text[i];

      i++;

      setTimeout(type,35);
    }
  }

  type();
}


/* VOICE SHAYARI */

function playShayari(){

  if(!("speechSynthesis" in window)){

    alert(
      "Is browser mein voice feature supported nahi hai 💗"
    );

    return;
  }

  speechSynthesis.cancel();

  const text =
    "Chand bhi aaj thoda sa sharma raha hoga. " +
    "Kyunki aaj usse bhi koi zyada pyaara nazar aa raha hoga. " +
    "Dua hai humhari har khushi tum tak khud chal kar aaye. " +
    "Aur tumhari har subah ek khoobsurat muskaan laaye. " +
    "Bas aaj itna kehna hai... " +
    "tumhari smile hamesha aise hi beautiful rahe.";

  const voice =
    new SpeechSynthesisUtterance(text);

  voice.rate = .82;
  voice.pitch = 1.12;
  voice.volume = 50;

  speechSynthesis.speak(voice);

  createHearts();
}


/* SOFT MUSIC */

function toggleMusic(){

  const btn =
    document.getElementById("musicBtn");

  if(musicOn){

    clearInterval(musicTimer);

    musicOn = false;

    btn.textContent =
      "🎵 Play Soft Music";

    return;
  }

  audioCtx =
    audioCtx ||
    new (
      window.AudioContext ||
      window.webkitAudioContext
    )();

  if(audioCtx.state === "suspended"){
    audioCtx.resume();
  }

  musicOn = true;

  btn.textContent =
    "⏸️ Pause Music";

  const notes = [
    261.63,
    329.63,
    392.00,
    329.63,
    293.66,
    349.23,
    440.00,
    349.23
  ];

  let index = 0;

  function playNote(){

    if(!musicOn) return;

    const osc =
      audioCtx.createOscillator();

    const gain =
      audioCtx.createGain();

    osc.type = "sine";

    osc.frequency.value =
      notes[index % notes.length];

    gain.gain.setValueAtTime(
      .0001,
      audioCtx.currentTime
    );

    gain.gain.exponentialRampToValueAtTime(
      .04,
      audioCtx.currentTime + .08
    );

    gain.gain.exponentialRampToValueAtTime(
      .0001,
      audioCtx.currentTime + .75
    );

    osc.connect(gain);

    gain.connect(
      audioCtx.destination
    );

    osc.start();

    osc.stop(
      audioCtx.currentTime + .8
    );

    index++;
  }

  playNote();

  musicTimer =
    setInterval(playNote,900);
}


/* FINAL SCREEN */

function showEnding(){

  document.getElementById("wish")
    .style.display = "none";

  document.getElementById("ending")
    .style.display = "block";

  createHearts();
}


/* LAST MESSAGE */

function finalReveal(){

  const name =
    document.getElementById("person")
      .textContent;

  document.getElementById("lastLine")
    .innerHTML =
    "And " + name +
    ", I hope you always keep that beautiful smile. 💗" +
    "<br><br>" +
    "Happy Birthday once again! 🎂✨";

  createHearts();
}


/* FLOATING HEARTS */

function createHearts(){

  const emojis = [
    "💗",
    "💖",
    "💕",
    "✨",
    "🌸",
    "🎈",
    "💝",
    "⭐"
  ];

  for(let i=0;i<28;i++){

    const heart =
      document.createElement("div");

    heart.className = "float";

    heart.textContent =
      emojis[
        Math.floor(
          Math.random() *
          emojis.length
        )
      ];

    heart.style.left =
      Math.random() * 100 + "vw";

    heart.style.fontSize =
      (15 + Math.random()*25) + "px";

    heart.style.animationDuration =
      (3 + Math.random()*4) + "s";

    document.body.appendChild(heart);

    setTimeout(() => {
      heart.remove();
    },7000);
  }
}


/* ENTER KEY */

document
  .getElementById("name")
  .addEventListener("keydown",function(e){

    if(e.key === "Enter"){
      showWish();
    }

  });

</script>

</body>
</html>