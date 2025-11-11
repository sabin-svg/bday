<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Happy Birthday ❤️ — Surprise</title>
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@300;600;800&family=Pacifico&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg1: #0f172a;
      --bg2: #1e293b;
      --accent: #ff6b81;
      --accent2: #ffd166;
      --glass: rgba(255,255,255,0.06);
    }
    *{box-sizing:border-box}
    html,body{height:100%;margin:0;font-family:Montserrat,system-ui,Arial;background:linear-gradient(160deg,var(--bg1),var(--bg2));color:#fff}

    /* center stage */
    .stage{min-height:100vh;display:flex;align-items:center;justify-content:center;padding:40px}
    .card{
      max-width:960px;width:100%;background:linear-gradient(180deg,rgba(255,255,255,0.03), rgba(255,255,255,0.02));border-radius:20px;padding:28px;backdrop-filter: blur(6px);box-shadow: 0 10px 40px rgba(2,6,23,0.6);position:relative;overflow:hidden;
      display:grid;grid-template-columns:1fr 420px;gap:24px;align-items:center
    }

    /* left content */
    .left h1{font-family:Pacifico, cursive;font-size:46px;margin:0 0 6px;letter-spacing:1px}
    .left .subtitle{color:rgba(255,255,255,0.75);margin-bottom:14px}
    .type{font-weight:600;color:var(--accent);font-size:20px}

    /* message box */
    .message{
      background:linear-gradient(135deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));padding:18px;border-radius:12px;border:1px solid rgba(255,255,255,0.04);
      box-shadow: inset 0 1px 0 rgba(255,255,255,0.02)
    }
    .message p{margin:0 0 12px;line-height:1.45}

    /* buttons */
    .controls{display:flex;gap:12px;margin-top:12px}
    .btn{background:linear-gradient(90deg,var(--accent),#ff9bb3);padding:10px 14px;border-radius:10px;border:none;cursor:pointer;font-weight:600;color:#102;box-shadow:0 8px 20px rgba(255,107,129,0.15);transform:translateY(0);transition:transform .16s}
    .btn:active{transform:translateY(2px)}
    .btn.ghost{background:transparent;border:1px solid rgba(255,255,255,0.06);color:#fff}

    /* right preview */
    .preview{display:flex;flex-direction:column;align-items:center;justify-content:center;gap:12px}
    .cake{width:320px;height:230px;display:flex;align-items:flex-end;justify-content:center;position:relative}
    .cake .layer{width:240px;height:60px;background:linear-gradient(180deg,#fff,#f6e6ff);border-radius:10px;border:6px solid #ffe7f5;box-shadow: 0 8px 30px rgba(0,0,0,0.35)}
    .candle{position:absolute;top:30px;left:50%;transform:translateX(-50%);display:flex;gap:8px}
    .flame{width:14px;height:22px;border-radius:50% 50% 40% 40%;background:linear-gradient(180deg,#ffd166,#ff6b6b);filter:drop-shadow(0 6px 8px rgba(255,107,129,0.14));animation:flame 900ms infinite}
    @keyframes flame{0%{transform:translateY(0) scale(1)}50%{transform:translateY(-3px) scale(1.05)}100%{transform:translateY(0) scale(1)}}

    /* floating balloons */
    .balloon{position:absolute;border-radius:60% 60% 60% 60%;width:70px;height:95px;opacity:0.95;display:flex;align-items:center;justify-content:center}
    .balloon::after{content:'';width:2px;height:40px;background:rgba(255,255,255,0.15);position:absolute;bottom:-40px}

    .balloon--1{left:-40px;top:10%;background:radial-gradient(circle at 30% 20%, #ffd166, #ff6b6b);animation:floaty 6s ease-in-out infinite}
    .balloon--2{right:-40px;top:25%;background:radial-gradient(circle at 70% 30%, #8be9fd, #6a5cff);animation:floaty 7s ease-in-out .4s infinite}
    .balloon--3{left:10%;bottom:10%;background:radial-gradient(circle at 20% 20%, #b9f18d, #69f0ae);animation:floaty 8s ease-in-out .8s infinite}
    @keyframes floaty{0%{transform:translateY(0) rotate(-4deg)}50%{transform:translateY(-22px) rotate(3deg)}100%{transform:translateY(0) rotate(-4deg)}}

    /* confetti canvas covers entire card */
    canvas.confetti{position:absolute;left:0;top:0;width:100%;height:100%;pointer-events:none}

    /* small flourish */
    .heart{font-size:26px;color:var(--accent);animation:pop 1.1s infinite ease-in-out}
    @keyframes pop{0%{transform:scale(1)}50%{transform:scale(1.05)}100%{transform:scale(1)}}

    /* responsive */
    @media (max-width:880px){
      .card{grid-template-columns:1fr; padding:18px}
      .cake{width:260px;height:200px}
      .left h1{font-size:36px}
    }

  </style>
</head>
<body>
  <div class="stage">
    <div class="card" id="card">

      <div class="left">
        <div style="display:flex;align-items:center;gap:12px;margin-bottom:10px">
          <div style="width:56px;height:56px;border-radius:14px;background:linear-gradient(135deg,var(--accent),#ff9bb3);display:flex;align-items:center;justify-content:center;font-weight:800;color:#fff;font-size:20px">🎉</div>
          <div>
            <div class="type">Surprise for</div>
            <h1 id="name">Your Love</h1>
            <div class="subtitle">A small page made with ❤️ to celebrate your day</div>
          </div>
        </div>

        <div class="message" id="messageBox">
          <p id="typed">Happy birthday! I hope this day fills your heart with joy and little surprises — because you deserve all the happy moments today and always.</p>
          <div style="display:flex;gap:10px;align-items:center">
            <span class="heart">❤</span>
            <small style="opacity:.7">Open the cake on the right and tap "Make a Wish" ✨</small>
          </div>
        </div>

        <div class="controls">
          <button class="btn" id="wishBtn">Make a Wish ✨</button>
          <button class="btn ghost" id="customizeBtn">Edit message</button>
          <button class="btn ghost" id="confettiToggle">Toggle Confetti</button>
        </div>

        <div style="margin-top:12px;color:rgba(255,255,255,0.6);font-size:13px">Tip: click the cake on the right for a little surprise + allow sound if you want music.</div>
      </div>

      <div class="preview">
        <div style="position:relative;width:100%;display:flex;align-items:center;justify-content:center">
          <div class="cake" id="cake">
            <div class="layer"></div>
            <div class="candle" id="candle">
              <div style="width:8px;height:36px;background:#ffd166;border-radius:4px;margin-top:-6px"></div>
              <div class="flame"></div>
            </div>
          </div>
          <!-- balloons -->
          <div class="balloon balloon--1">🎈</div>
          <div class="balloon balloon--2">🎈</div>
          <div class="balloon balloon--3">🎈</div>
        </div>

        <button class="btn" id="openBtn">Open the Cake 🎂</button>
        <div style="display:flex;gap:12px;margin-top:6px">
          <button class="btn ghost" id="shareBtn">Download Image</button>
          <button class="btn" id="musicBtn">Play Music ▶</button>
        </div>
      </div>

      <canvas class="confetti" id="confettiCanvas"></canvas>
    </div>
  </div>

  <audio id="bgMusic" loop preload="auto">
    <!-- Put your own audio file path here or leave commented. Example: <source src="./happy-bday.mp3" type="audio/mpeg"> -->
  </audio>

  <script>
    // --------- small typed effect ---------
    const nameEl = document.getElementById('name');
    const typedEl = document.getElementById('typed');
    const defaultText = typedEl.textContent;

    // user editable fields
    let recName = 'Your Love';
    nameEl.textContent = recName;

    function typeText(el, text, speed=28){
      el.textContent = '';
      let i=0;const t = setInterval(()=>{el.textContent += text.charAt(i); i++; if(i>=text.length) clearInterval(t)}, speed);
    }

    // initial type
    typeText(typedEl, defaultText, 18);

    // ---------- confetti system ----------
    const canvas = document.getElementById('confettiCanvas');
    const ctx = canvas.getContext('2d');
    let W, H;
    function resize(){ W = canvas.width = canvas.clientWidth; H = canvas.height = canvas.clientHeight }
    window.addEventListener('resize', resize); resize();

    const colors = ['#ff6b81','#ffd166','#8be9fd','#6a5cff','#7efc82'];
    function random(min,max){return Math.random()*(max-min)+min}

    let pieces = [];
    function createConfetti(count=60){
      for(let i=0;i<count;i++){
        pieces.push({x:random(0,W),y:random(-H,0),w:random(6,12),h:random(8,16),vx:random(-1,1),vy:random(2,6),r:random(0,360),color:colors[Math.floor(Math.random()*colors.length)],d:random(0,1)})
      }
    }

    function updateConfetti(){
      ctx.clearRect(0,0,W,H);
      for(let p of pieces){
        p.x += p.vx; p.y += p.vy; p.r += p.vx*3;
        ctx.save(); ctx.translate(p.x,p.y); ctx.rotate(p.r*Math.PI/180);
        ctx.fillStyle = p.color; ctx.fillRect(-p.w/2,-p.h/2,p.w,p.h);
        ctx.restore();
        if(p.y>H+30){ p.x=random(0,W); p.y=random(-H,0); p.vx=random(-1,1); p.vy=random(2,6)}
      }
      requestAnimationFrame(updateConfetti);
    }

    let confettiOn = true; createConfetti(80); updateConfetti();

    // ---------- interactions ----------
    const wishBtn = document.getElementById('wishBtn');
    const openBtn = document.getElementById('openBtn');
    const candle = document.getElementById('candle');
    const bgMusic = document.getElementById('bgMusic');
    const musicBtn = document.getElementById('musicBtn');
    const confettiToggle = document.getElementById('confettiToggle');

    wishBtn.addEventListener('click', ()=>{
      // animate card pulse
      const card = document.getElementById('card');
      card.animate([{transform:'scale(1)'},{transform:'scale(1.02)'},{transform:'scale(1)'}],{duration:450,iterations:1});
      // small personal message change
      typeText(typedEl, 'Wishing you oceans of smiles, surprises, and sweet memories. Make a wish ✨', 18);
      // big confetti burst
      createConfetti(140);
    });

    openBtn.addEventListener('click', ()=>{
      // cake opening surprise: hide candle and show heart burst
      candle.style.transition = 'all .6s ease';
      candle.style.transform = 'translateY(-30px) scale(.8)';
      setTimeout(()=>{ candle.style.opacity = '0'; }, 600);

      // heart float
      const heart = document.createElement('div');
      heart.textContent = '💖';
      heart.style.position='absolute'; heart.style.left='50%'; heart.style.top='30%'; heart.style.transform='translate(-50%,-50%) scale(0)';
      heart.style.fontSize='48px'; heart.style.opacity='0'; heart.style.transition='all .8s cubic-bezier(.2,.8,.2,1)';
      document.getElementById('cake').appendChild(heart);
      requestAnimationFrame(()=>{ heart.style.transform='translate(-50%,-50%) scale(1)'; heart.style.opacity='1'; });

      // confetti + sound trigger
      createConfetti(180);
      // try to play music if user enabled one
      playMusicIfReady();

      setTimeout(()=>{ heart.style.opacity='0'; heart.style.transform='translate(-50%,-10%) scale(.6)'; setTimeout(()=>heart.remove(),900)},2400);
    });

    // --------- music ---------
    function playMusicIfReady(){
      if(bgMusic.querySelector('source')){
        bgMusic.play().catch(()=>{ console.log('autoplay blocked — user interaction required') });
      }
    }

    musicBtn.addEventListener('click', ()=>{
      // toggle play
      if(bgMusic.paused){ bgMusic.play().catch(()=>alert('Browser blocked autoplay. Click allow or add a file to play.')); musicBtn.textContent='Pause ⏸' }
      else { bgMusic.pause(); musicBtn.textContent='Play Music ▶' }
    });

    // -------- download preview image --------
    document.getElementById('shareBtn').addEventListener('click', async ()=>{
      const card = document.getElementById('card');
      // simple html2canvas-like approach using SVG foreignObject
      const svg = `<svg xmlns='http://www.w3.org/2000/svg' width='1200' height='630'><foreignObject width='100%' height='100%'>${new XMLSerializer().serializeToString(card)}</foreignObject></svg>`;
      const blob = new Blob([svg],{type:'image/svg+xml;charset=utf-8'});
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a'); a.href = url; a.download = 'birthday-card.svg'; a.click(); URL.revokeObjectURL(url);
    });

    // confetti toggle
    confettiToggle.addEventListener('click', ()=>{
      confettiOn = !confettiOn; document.getElementById('confettiCanvas').style.display = confettiOn ? 'block' : 'none';
    });

    // small helper to let user edit message
    document.getElementById('customizeBtn').addEventListener('click', ()=>{
      const newMsg = prompt('Write a short message (max 220 chars):', typedEl.textContent);
      if(newMsg!==null){ typedEl.textContent = newMsg.slice(0,220) }
    });

    // ensure canvas adjusts to device pixel ratio for crispness
    function fixDPR(){ const dpr = window.devicePixelRatio || 1; canvas.width = canvas.clientWidth * dpr; canvas.height = canvas.clientHeight * dpr; ctx.setTransform(dpr,0,0,dpr,0,0)}
    window.addEventListener('resize', fixDPR); fixDPR();

    // small accessibility: keyboard shortcut 'w' to make a wish
    window.addEventListener('keydown',(e)=>{ if(e.key.toLowerCase()==='w'){ wishBtn.click() } });

    // initial flourish — gentle confetti pulse
    setTimeout(()=>createConfetti(40),800);
  </script>
</body>
</html>
