<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>A Secret Kept For You</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,500;0,600;1,500;1,600&family=Poppins:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --wine:#2b0a1f;
    --plum:#4a1236;
    --rose:#e8b4b8;
    --gold:#c9a15a;
    --champagne:#f6ebe4;
    --ink:#fdf6f0;
    --glass: rgba(255,255,255,0.06);
    --glass-border: rgba(201,161,90,0.35);
  }

  *{box-sizing:border-box; -webkit-tap-highlight-color:transparent;}

  html,body{
    margin:0; padding:0; width:100%; min-height:100%;
    font-family:'Poppins', sans-serif;
    color:var(--ink);
    background:linear-gradient(135deg, var(--wine), var(--plum) 45%, #6e2142 75%, #8a3a52 100%);
    background-size:300% 300%;
    animation:gradientShift 18s ease infinite;
    overflow-x:hidden;
  }

  @keyframes gradientShift{
    0%{background-position:0% 50%;}
    50%{background-position:100% 50%;}
    100%{background-position:0% 50%;}
  }

  h1,h2,h3{
    font-family:'Playfair Display', serif;
    font-weight:600;
    margin:0 0 14px 0;
    letter-spacing:0.3px;
  }

  p{
    font-weight:300;
    line-height:1.75;
    font-size:16px;
    color:var(--champagne);
    margin:0;
  }

  #heart-field{
    position:fixed; inset:0; pointer-events:none; z-index:1; overflow:hidden;
  }

  .drift-heart{
    position:absolute;
    bottom:-40px;
    opacity:0.55;
    color:var(--gold);
    filter: drop-shadow(0 0 6px rgba(201,161,90,0.35));
    animation-name: floatUp;
    animation-timing-function: ease-in;
    animation-iteration-count: 1;
    will-change: transform, opacity;
  }

  @keyframes floatUp{
    0%{ transform:translate(0,0) rotate(0deg) scale(var(--s,1)); opacity:0; }
    10%{ opacity:0.6; }
    100%{ transform:translate(var(--dx,20px), -115vh) rotate(var(--r,25deg)) scale(var(--s,1)); opacity:0; }
  }

  .screen{
    position:relative; z-index:2;
    min-height:100vh; width:100%;
    display:none;
    align-items:center; justify-content:center;
    padding:32px 18px 56px;
  }

  .screen.active{
    display:flex;
  }

  .card{
    width:100%; max-width:440px;
    background:var(--glass);
    border:1px solid var(--glass-border);
    backdrop-filter: blur(14px);
    -webkit-backdrop-filter: blur(14px);
    border-radius:26px;
    padding:38px 28px;
    text-align:center;
    box-shadow: 0 20px 60px rgba(0,0,0,0.35);
    animation: revealCard 0.7s cubic-bezier(.22,.9,.32,1);
  }

  @keyframes revealCard{
    0%{ opacity:0; transform:translateY(24px) scale(0.97); }
    100%{ opacity:1; transform:translateY(0) scale(1); }
  }

  .eyebrow{
    font-size:11px;
    letter-spacing:3px;
    text-transform:uppercase;
    color:var(--gold);
    margin-bottom:10px;
    font-weight:500;
  }

  .seal{
    width:64px; height:64px;
    margin:0 auto 20px;
    border-radius:50%;
    background:radial-gradient(circle at 35% 30%, #e6c98a, var(--gold) 60%, #8a6a2e 100%);
    display:flex; align-items:center; justify-content:center;
    box-shadow:0 8px 24px rgba(201,161,90,0.4), inset 0 0 8px rgba(255,255,255,0.4);
  }

  .seal svg{ width:28px; height:28px; }

  input[type="tel"]{
    width:100%;
    text-align:center;
    letter-spacing:10px;
    font-size:22px;
    font-family:'Playfair Display', serif;
    padding:14px 10px;
    margin:18px 0 6px;
    border-radius:14px;
    border:1px solid var(--glass-border);
    background:rgba(255,255,255,0.08);
    color:var(--ink);
    outline:none;
  }

  input[type="tel"]:focus{
    border-color:var(--gold);
    box-shadow:0 0 0 3px rgba(201,161,90,0.2);
  }

  .hint{
    font-size:12.5px;
    color:var(--rose);
    opacity:0.85;
    margin-top:2px;
    font-style:italic;
  }

  .error-msg{
    min-height:20px;
    font-size:13px;
    color:#f3c6c6;
    margin-top:10px;
    font-weight:400;
  }

  .shake{ animation: shakeIt 0.45s; }
  @keyframes shakeIt{
    0%,100%{ transform:translateX(0); }
    20%{ transform:translateX(-10px); }
    40%{ transform:translateX(9px); }
    60%{ transform:translateX(-6px); }
    80%{ transform:translateX(5px); }
  }

  button{
    font-family:'Poppins', sans-serif;
    font-weight:500;
    font-size:15px;
    letter-spacing:0.4px;
    color:var(--wine);
    background:linear-gradient(135deg, #f3dfa8, var(--gold) 55%, #b98a45);
    border:none;
    padding:15px 30px;
    border-radius:40px;
    cursor:pointer;
    margin-top:20px;
    box-shadow:0 10px 26px rgba(201,161,90,0.35);
    transition:transform 0.25s ease, box-shadow 0.25s ease;
  }

  button:hover{ transform:translateY(-2px); box-shadow:0 14px 30px rgba(201,161,90,0.5); }
  button:active{ transform:translateY(0) scale(0.98); }

  .btn-ghost{
    background:transparent;
    color:var(--champagne);
    border:1px solid var(--glass-border);
    box-shadow:none;
  }

  .btn-ghost:hover{ border-color:var(--gold); box-shadow:0 8px 20px rgba(0,0,0,0.2); }

  .spotify-btn{
    display:inline-flex; align-items:center; gap:10px;
    background:linear-gradient(135deg,#1DB954,#169c46);
    color:#fff;
  }

  .progress{
    font-size:11px;
    letter-spacing:2px;
    text-transform:uppercase;
    color:var(--rose);
    margin-bottom:16px;
    opacity:0.8;
  }

  .level-text{
    margin:16px 0 4px;
  }

  .pic-wrap{
    margin:18px auto 6px;
    width:100%;
    max-width:320px;
    border-radius:20px;
    overflow:hidden;
    box-shadow:0 16px 34px rgba(0,0,0,0.4);
    border:1px solid var(--glass-border);
  }

  .pic-wrap img{
    width:100%; height:280px; object-fit:cover; display:block;
  }

  .pic-fallback{
    width:100%; height:280px;
    display:flex; flex-direction:column; align-items:center; justify-content:center;
    background:linear-gradient(135deg, rgba(201,161,90,0.25), rgba(74,18,54,0.6));
    gap:10px;
  }

  .pic-fallback svg{ width:40px; height:40px; opacity:0.8; }
  .pic-fallback span{ font-size:12px; color:var(--rose); letter-spacing:1px; }

  .final-title{
    font-size:28px;
    margin-bottom:6px;
  }

  .final-text{
    text-align:left;
    font-size:15.5px;
    line-height:1.9;
    max-height:52vh;
    overflow-y:auto;
    padding-right:6px;
    margin-top:14px;
  }

  .final-text::-webkit-scrollbar{ width:4px; }
  .final-text::-webkit-scrollbar-thumb{ background:var(--gold); border-radius:4px; }

  .love-sign{
    margin-top:22px;
    font-family:'Playfair Display', serif;
    font-style:italic;
    font-size:22px;
    color:var(--gold);
  }

  .small-note{
    font-size:12px;
    color:var(--rose);
    margin-top:24px;
    opacity:0.8;
  }

  @media (max-width:360px){
    .card{ padding:30px 20px; }
    input[type="tel"]{ letter-spacing:8px; font-size:19px; }
  }

  @media (prefers-reduced-motion: reduce){
    html,body{ animation:none; }
    .drift-heart{ display:none; }
    .card{ animation:none; }
  }
</style>
</head>
<body>

<div id="heart-field"></div>

<!-- LOCK SCREEN -->
<div class="screen active" id="lock-screen">
  <div class="card">
    <div class="eyebrow">A Private Little World</div>
    <div class="seal">
      <svg viewBox="0 0 24 24" fill="none"><path d="M12 21s-7.2-4.6-9.8-9.1C.6 8.6 2 5 5.4 4.2c2-.5 3.9.4 5 2 .1.1.2.1.3 0 1.1-1.6 3-2.5 5-2 3.4.8 4.8 4.4 3.2 7.7C19.2 16.4 12 21 12 21z" fill="#2b0a1f"/></svg>
    </div>
    <h1>This Door Only Opens For You</h1>
    <p>Somewhere in your memory, a number is waiting. Enter it, and my heart unlocks.</p>
    <input type="tel" id="pin-input" maxlength="4" placeholder="• • • •" inputmode="numeric">
    <div class="hint">psst... think of the year our story turns a page 🎆</div>
    <div class="error-msg" id="error-msg"></div>
    <button onclick="checkPin()">Unlock My Heart</button>
  </div>
</div>

<!-- WELCOME SCREEN -->
<div class="screen" id="welcome-screen">
  <div class="card">
    <div class="eyebrow">Access Granted</div>
    <h1>Hi, My Love.</h1>
    <p>You found the key. Before we go any further, put this on — it's the song that sounds like us. Then, when you're ready, step inside.</p>
    <a href="https://open.spotify.com/track/2c5JKO8gPaOFVxQ0elwXEG?si=IRjB_ApESGyMgiJxzMM6ig&utm_source=copy-link" target="_blank" rel="noopener">
      <button class="spotify-btn">♪ Play Our Song</button>
    </a>
    <br>
    <button onclick="goTo('level-screen'); renderLevel();">Begin Our Journey</button>
  </div>
</div>

<!-- LEVEL / STORY SCREEN -->
<div class="screen" id="level-screen">
  <div class="card">
    <div class="progress" id="level-progress">Chapter 1 of 20</div>
    <h2 id="level-title"></h2>
    <p class="level-text" id="level-text"></p>
    <div id="level-extra"></div>
    <button id="level-btn" onclick="nextLevel()"></button>
  </div>
</div>

<!-- FINAL SCREEN -->
<div class="screen" id="final-screen">
  <div class="card">
    <div class="eyebrow">The Last Door</div>
    <h2 class="final-title">To You, Always</h2>
    <div class="final-text">
      <p id="final-message"></p>
    </div>
    <div class="love-sign">I love you ❤️</div>
    <div class="small-note">— every version of me, every day, always choosing you.</div>
  </div>
</div>

<script>
  /* ---------- Floating hearts background ---------- */
  const field = document.getElementById('heart-field');
  function spawnHeart(){
    const h = document.createElement('div');
    h.className = 'drift-heart';
    h.innerHTML = `<svg width="${16+Math.random()*14}" height="${16+Math.random()*14}" viewBox="0 0 24 24" fill="currentColor"><path d="M12 21s-7.2-4.6-9.8-9.1C.6 8.6 2 5 5.4 4.2c2-.5 3.9.4 5 2 .1.1.2.1.3 0 1.1-1.6 3-2.5 5-2 3.4.8 4.8 4.4 3.2 7.7C19.2 16.4 12 21 12 21z"/></svg>`;
    const left = Math.random()*94 + 2;
    const dur = 7 + Math.random()*8;
    const dx = (Math.random()*80 - 40) + 'px';
    const rot = (Math.random()*60 - 30) + 'deg';
    const scale = (0.6 + Math.random()*0.9).toFixed(2);
    h.style.left = left + 'vw';
    h.style.setProperty('--dx', dx);
    h.style.setProperty('--r', rot);
    h.style.setProperty('--s', scale);
    h.style.animationDuration = dur + 's';
    field.appendChild(h);
    setTimeout(()=> h.remove(), dur*1000 + 200);
  }
  setInterval(spawnHeart, 650);
  for(let i=0;i<6;i++){ setTimeout(spawnHeart, i*300); }

  /* ---------- Screen navigation ---------- */
  function goTo(id){
    document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    window.scrollTo(0,0);
  }

  /* ---------- PIN lock ---------- */
  const correctPin = "2026";
  const wrongMessages = [
    "Nice try, but that's not our year. My heart stays locked a little longer 😏",
    "Wrong number, right person. Guess again, love.",
    "Access denied — but my love for you? Fully approved. Try once more.",
    "Hmm, not quite. Even my WiFi password is easier to guess than my heart.",
    "That pin doesn't open me... but you already have the other key. Try again."
  ];

  function checkPin(){
    const val = document.getElementById('pin-input').value.trim();
    const card = document.querySelector('#lock-screen .card');
    const errorBox = document.getElementById('error-msg');
    if(val === correctPin){
      errorBox.textContent = '';
      goTo('welcome-screen');
    } else {
      const msg = wrongMessages[Math.floor(Math.random()*wrongMessages.length)];
      errorBox.textContent = msg;
      card.classList.remove('shake');
      void card.offsetWidth;
      card.classList.add('shake');
    }
  }

  document.getElementById('pin-input').addEventListener('keydown', function(e){
    if(e.key === 'Enter'){ checkPin(); }
  });

  /* ---------- Levels ---------- */
  const levels = [
    { title:"Where It Began", text:"Somewhere between a normal day and a quiet coincidence, you walked into my life — and nothing has felt ordinary since.", btn:"Unlock Memory" },
    { title:"The First Spark", text:"I remember the exact feeling of talking to you for the first time — like finding a song I didn't know I'd been missing.", btn:"Continue Our Story" },
    { title:"Her Smile", text:"Your smile has this quiet power. It can end a bad day, calm a racing mind, and somehow always feels like home.", btn:"Open The Next Chapter" },
    { title:"Late Night Talks", text:"Some of my favorite memories aren't big moments at all — just us, talking until far too late, not wanting the conversation to end.", btn:"Turn The Page" },
    { title:"The Sound of Her Laugh", text:"If I could bottle one sound to keep forever, it would be your laugh. It's the most honest kind of happiness I know.", btn:"Step Closer To My Heart" },
    { title:"Comfort in Chaos", text:"On the days everything felt like too much, you were the one steady thing. You didn't fix it — you just stayed. That mattered more.", btn:"Reveal The Next Moment" },
    { title:"Small Moments, Big Feelings", text:"A text in the middle of the day. A random 'thinking of you.' The smallest things you do somehow mean the most to me.", btn:"Walk With Me" },
    { title:"Holding Hands", text:"There's a whole conversation in the way you hold my hand — steady, sure, like you're not going anywhere. I hope you never do.", btn:"Keep Reading My Heart" },
    { title:"Through the Storms", text:"We've had hard days, misunderstandings, moments neither of us handled perfectly. But we stayed. That's what love actually looks like.", btn:"Unfold The Story" },
    { title:"A Memory Worth Keeping", text:"Some moments deserve more than words. This one is for you.", btn:"Discover More", extra:"picture" },
    { title:"Inside Jokes Only We Understand", text:"There are things I only laugh about with you — little words and moments that mean nothing to the world and everything to us.", btn:"Open This Memory" },
    { title:"The Words 'I Love You'", text:"The first time I said it, I meant every letter. Every time since, it's only gotten more true, not less.", btn:"Hear My Heart" },
    { title:"Dreaming of Forever", text:"I catch myself imagining years from now — still choosing you, still building something real, still glad I found you.", btn:"Dream With Me" },
    { title:"Songs That Sound Like Her", text:"Certain songs just remind me of you now. They didn't used to. You've quietly rewritten what things mean to me.", btn:"Play The Next Track" },
    { title:"Missing Her", text:"Even on days we talk for hours, there's a part of me that still misses you the moment we're apart. That's just what you do to me.", btn:"Find Me Here" },
    { title:"Her Quiet Strength", text:"You carry more than people realize, and you still show up soft and warm for the people you love. I notice. I admire that deeply.", btn:"See Her Strength" },
    { title:"Every Little Adventure", text:"Whether it's something big or just an ordinary afternoon, everything feels like an adventure when you're the one beside me.", btn:"Continue The Adventure" },
    { title:"Growing, Not Perfect", text:"We're not perfect — neither of us. But I'd rather grow through the hard parts with you than have it easy with anyone else.", btn:"Grow With Me" },
    { title:"Choosing Her, Again and Again", text:"Love isn't just a feeling from the beginning. It's a choice I keep making — today, tomorrow, and every ordinary day after that.", btn:"Choose Us Again" },
    { title:"One Last Door", text:"There's one more thing I need you to read. Take a breath before you open it.", btn:"Open The Final Door" }
  ];

  let currentLevel = 0;

  function renderLevel(){
    const l = levels[currentLevel];
    document.getElementById('level-progress').textContent = `Chapter ${currentLevel+1} of ${levels.length}`;
    document.getElementById('level-title').textContent = l.title;
    document.getElementById('level-text').textContent = l.text;
    document.getElementById('level-btn').textContent = l.btn;

    const extraBox = document.getElementById('level-extra');
    extraBox.innerHTML = '';
    if(l.extra === 'picture'){
      const wrap = document.createElement('div');
      wrap.className = 'pic-wrap';
      wrap.innerHTML = `
        <img src="data:image/jpeg;base64,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" alt="our memory">`;
      extraBox.appendChild(wrap);
    }

    const card = document.querySelector('#level-screen .card');
    card.style.animation = 'none';
    void card.offsetWidth;
    card.style.animation = 'revealCard 0.6s cubic-bezier(.22,.9,.32,1)';
  }

  function nextLevel(){
    currentLevel++;
    if(currentLevel >= levels.length){
      renderFinal();
      goTo('final-screen');
    } else {
      renderLevel();
    }
  }

  /* ---------- Final message ---------- */
  function renderFinal(){
    const msg = `Before you, I didn't know a person could feel like both home and adventure at once. I am endlessly thankful you walked into my life — not because things became easy, but because they became worth it.

I see how much love and effort you put into us, even on the days it isn't easy, even when no one else notices. I notice. I am grateful for every quiet sacrifice, every patient moment, every time you chose to stay and try instead of walking away.

We are not perfect, and I stopped needing us to be. What I want instead is real — two people who mess up sometimes, who talk it through, who keep choosing to grow side by side instead of giving up when it gets hard. I would rather build something true with you than something flawless with anyone else.

So here is my promise, said plainly: I choose you. Not just today, in this moment of soft lights and quiet words, but tomorrow, and the ordinary Tuesday after that, and all the days that don't feel like anything special except that you're in them.

I want more mornings that start with your name in my head. More inside jokes no one else will ever understand. More hard days we get through together and more small, ordinary moments that somehow become the ones I remember most. I want a whole life stacked with memories that have your laugh somewhere in the background.

Thank you for being patient with me, for loving me even when I'm still learning how to love well. Thank you for being exactly, uniquely you. Whatever comes next, I want to face it standing next to you.

I love you ❤️`;
    document.getElementById('final-message').textContent = msg;
  }
</script>
</body>
</html>
