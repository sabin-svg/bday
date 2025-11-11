<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Happy Birthday — Surprise</title>
  <meta name="color-scheme" content="dark light">
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@300;600;800&family=Pacifico&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg1: #0f172a;
      --bg2: #1e293b;
      --accent: #ff6b81;
      --accent2: #ffd166;
      --glass: rgba(255,255,255,0.06);
      --card-bg: linear-gradient(180deg, rgba(255,255,255,0.03), rgba(255,255,255,0.02));
    }
    *{box-sizing:border-box}
    html,body{height:100%;margin:0;font-family:Montserrat,system-ui,Arial;background:radial-gradient(1000px 600px at 10% 10%, rgba(255,99,130,0.06), transparent), linear-gradient(160deg,var(--bg1),var(--bg2));color:#fff; -webkit-font-smoothing:antialiased;}

    /* page layout */
    .container{min-height:100vh;display:flex;align-items:center;justify-content:center;padding:36px}
    .stage{width:100%;max-width:1100px;border-radius:18px;padding:28px;background:var(--card-bg);backdrop-filter: blur(6px);box-shadow: 0 30px 80px rgba(2,6,23,0.6);position:relative;overflow:hidden;display:grid;grid-template-columns:1fr 480px;gap:26px;align-items:center}
    .hero {padding:8px 0}
    h1{font-family:Pacifico, cursive;font-size:48px;margin:0 0 6px;color: #fff;text-shadow:0 6px 28px rgba(0,0,0,0.45)}

    .subtitle{color:rgba(255,255,255,0.75);margin-bottom:16px}

    /* input panel */
    .panel{background:rgba(255,255,255,0.02);padding:18px;border-radius:12px;border:1px solid rgba(255,255,255,0.04)}
    label{display:block;font-size:13px;color:rgba(255,255,255,0.8);margin-bottom:8px}
    input[type="text"]{width:100%;padding:12px;border-radius:10px;border:1px solid rgba(255,255,255,0.06);background:transparent;color:#fff;font-size:16px}
    .small{font-size:13px;color:rgba(255,255,255,0.65);margin-top:8px}
    .row{display:flex;gap:10px;margin-top:14px;flex-wrap:wrap}
    button.btn{background:linear-gradient(90deg,var(--accent),#ff9bb3);padding:10px 14px;border-radius:10px;border:none;cursor:pointer;font-weight:700;color:#102;box-shadow:0 10px 30px rgba(255,107,129,0.12);}

    /* cake preview (3D-ish) */
    .scene{display:flex;align-items:center;justify-content:center;height:420px;perspective:1200px}
    .cake-3d{width:320px;transform-style:preserve-3d;transition:transform .8s cubic-bezier(.2,.9,.2,.95);position:relative}
    .cake-layer{
      width:280px;height:78px;background:linear-gradient(180deg,#fff,#f7e8ff);border-radius:16px;border:6px solid #ffe7f5;box-shadow: 0 12px 30px rgba(0,0,0,0.35);position:absolute;left:50%;transform:translateX(-50%);display:flex;align-items:center;justify-content:center;
    }
    .layer-1{bottom:0;z-index:3}
    .layer-2{bottom:68px;z-index:4;transform:translateX(-50%) scale(.98)}
    .layer-3{bottom:132px;z-index:5;transform:translateX(-50%) scale(.96)}
    .candle{position:absolute;left:50%;top:40px;transform:translateX(-50%);display:flex;gap:8px;align-items:flex-end}
    .candle .stick{width:8px;height:40px;background:#ffd166;border-radius:3px}
    .flame{width:14px;height:22px;border-radius:50% 50% 40% 40%;background:linear-gradient(180deg,#ffd166,#ff6b6b);filter:drop-shadow(0 8px 12px rgba(255,107,129,0.12));animation:flame 900ms infinite}
    @keyframes flame{0%{transform:translateY(0)}50%{transform:translateY(-4px)}100%{transform:translateY(0)}}

    /* cake slice (hidden until cut) */
    .slice{position:absolute;left:50%;bottom:8px;transform-origin:bottom center;transform:translateX(20%) rotateZ(6deg) scale(0);width:120px;height:140px;background:linear-gradient(180deg,#fff,#f6e6ff);border-radius:10px;border:6px solid #ffe7f5;box-shadow:0 20px 40px rgba(0,0,0,0.45);z-index:10;transition:transform .9s cubic-bezier(.2,.9,.2,.9),opacity .6s}
    .slice.visible{transform:translateX(200%) rotateZ(10deg) translateY(-60px) scale(1);opacity:1}

    /* overlay controls */
    .controls{display:flex;flex-direction:column;gap:12px;margin-top:14px}
    .btn.ghost{background:transparent;border:1px solid rgba(255,255,255,0.06);color:#fff}
    .share{display:flex;gap:10px}

    /* memories gallery */
    .gallery{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-top:14px}
    .gallery img{width:100%;height:86px;object-fit:cover;border-radius:10px;cursor:pointer;transition:transform .28s}
    .gallery img:hover{transform:translateY(-6px)}

    /* modal */
    .modal{position:fixed;left:0;top:0;width:100%;height:100%;display:none;align-items:center;justify-content:center;background:linear-gradient(180deg, rgba(2,6,23,0.6), rgba(2,6,23,0.85));z-index:9999;backdrop-filter: blur(4px)}
    .modal.show{display:flex}
    .modal .card{max-width:880px;padding:20px}
    .modal img{max-width:100%;height:auto;border-radius:12px;display:block}

    /* confetti canvas */
    canvas.conf{position:fixed;left:0;top:0;width:100%;height:100%;pointer-events:none;z-index:500}

    /* footer text */
    .footer {font-size:13px;color:rgba(255,255,255,0.7);margin-top:10px}

    /* responsive */
    @media (max-width:980px){
      .stage{grid-template-columns:1fr; padding:18px}
      .scene{height:300px}
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="stage" id="stage">
      <div class="hero">
        <h1 id="greeting">Happy Birthday</h1>
        <div class="subtitle" id="sub">Make it special — start by entering her name</div>

        <div class="panel">
          <label for="nameInput">Enter her name</label>
          <input id="nameInput" type="text" placeholder="Her name (e.g., Priya)" maxlength="24" />
          <div class="row">
            <button class="btn" id="saveName">Set Name & Start</button>
            <button class="btn ghost" id="resetName">Reset</button>
            <div style="flex:1" class="small">Name is saved locally on your browser (no server). You can edit anytime.</div>
          </div>

          <div class="controls">
            <div style="display:flex;gap:8px;align-items:center;margin-top:8px">
              <button class="btn" id="openCakeBtn">Open / Cut Cake 🎂</button>
              <button class="btn ghost" id="playMusic">Play Music ▶</button>
              <button class="btn ghost" id="toggleConfetti">Confetti On/Off</button>
            </div>

            <div style="margin-top:12px">
              <div style="font-weight:700;margin-bottom:6px">Memories</div>
              <div class="gallery" id="gallery">
                <img src="images/hand-holding-in-love.jpg" alt="memory1" data-caption="Our walk hand in hand">
                <img src="images/pexels-.jpg" alt="memory2" data-caption="Sunset by the sea">
                <img src="images/photo3.jpg" alt="memory3" data-caption="Add your photo3.jpg in images/">
              </div>
            </div>
          </div>

          <div class="footer">Tip: click any memory to enlarge. Open the cake to cut it — nice animation included.</div>
        </div>
      </div>

      <!-- right: 3D cake preview -->
      <div>
        <div class="scene" id="scene">
          <div class="cake-3d" id="cake3d">
            <div class="layer-3 cake-layer"></div>
            <div class="layer-2 cake-layer"></div>
            <div class="layer-1 cake-layer"></div>
            <div class="candle">
              <div class="stick"></div>
              <div class="flame"></div>
            </div>
            <div class="slice" id="slice">🍰</div>
          </div>
        </div>

        <div style="display:flex;justify-content:center;margin-top:12px;gap:10px">
          <button class="btn" id="downloadBtn">Download Card</button>
          <button class="btn ghost" id="restartBtn">Replay 🎉</button>
        </div>
      </div>

      <canvas class="conf" id="confettiCanvas"></canvas>
    </div>
  </div>

  <!-- modal for gallery -->
  <div class="modal" id="modal">
    <div class="panel card">
      <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:10px">
        <strong id="modalCaption">Memory</strong>
        <button class="btn ghost" id="closeModal">Close</button>
      </div>
      <img id="modalImg" src="" alt="preview">
    </div>
  </div>

  <audio id="bgMusic" preload="auto" loop>
    <!-- To enable music: place music.mp3 in root and uncomment next line -->
    <!-- <source src="music.mp3" type="audio/mpeg"> -->
  </audio>

  <script>
    // --- basics: elements
    const nameInput = document.getElementById('nameInput');
    const saveName = document.getElementById('saveName');
    const resetName = document.getElementById('resetName');
    const greeting = document.getElementById('greeting');
    const sub = document.getElementById('sub');
    const cake3d = document.getElementById('cake3d');
    const slice = document.getElementById('slice');
    const openCakeBtn = document.getElementById('openCakeBtn');
    const playMusic = document.getElementById('playMusic');
    const bgMusic = document.getElementById('bgMusic');
    const toggleConfetti = document.getElementById('toggleConfetti');
    const confettiCanvas = document.getElementById('confettiCanvas');
    const downloadBtn = document.getElementById('downloadBtn');
    const restartBtn = document.getElementById('restartBtn');

    // gallery modal
    const gallery = document.getElementById('gallery');
    const modal = document.getElementById('modal');
    const modalImg = document.getElementById('modalImg');
    const modalCaption = document.getElementById('modalCaption');
    const closeModal = document.getElementById('closeModal');

    // --- localStorage name handling
    function setName(n){
      if(!n) return;
      localStorage.setItem('hb_name', n);
      applyName();
    }
    function applyName(){
      const n = localStorage.getItem('hb_name') || '';
      if(n.trim()){
        greeting.textContent = `Happy Birthday, ${n}!`;
        sub.textContent = `A little surprise for ${n} — tap the cake to cut it`;
      } else {
        greeting.textContent = 'Happy Birthday';
        sub.textContent = 'Make it special — start by entering her name';
      }
      nameInput.value = n || '';
    }
    saveName.addEventListener('click', ()=>{ setName(nameInput.value.trim()); })
    resetName.addEventListener('click', ()=>{ localStorage.removeItem('hb_name'); applyName(); })

    applyName();

    // --- simple 3D tilt on pointer
    document.getElementById('scene').addEventListener('mousemove', (e)=>{
      const rect = e.currentTarget.getBoundingClientRect();
      const cx = rect.left + rect.width/2;
      const cy = rect.top + rect.height/2;
      const dx = (e.clientX - cx)/rect.width;
      const dy = (e.clientY - cy)/rect.height;
      cake3d.style.transform = `rotateX(${(-dy*8).toFixed(2)}deg) rotateY(${(dx*12).toFixed(2)}deg) translateZ(0)`;
    });
    document.getElementById('scene').addEventListener('mouseleave', ()=>{ cake3d.style.transform = 'rotateX(0) rotateY(0)'; });

    // --- cake cutting animation
    let cut = false;
    function cutCake(){
      if(cut) return;
      cut = true;
      // push layers apart and pop slice
      const layers = cake3d.querySelectorAll('.cake-layer');
      layers.forEach((el,i)=>{
        const up = -12 - i*16;
        el.animate([{transform:`translateX(-50%) scale(${1 - i*0.02})`},{transform:`translateX(-50%) translateY(${up}px) scale(${1 - i*0.02})`}], {duration:700, easing:'cubic-bezier(.2,.8,.2,1)', fill:'forwards'});
      });
      // show slice
      slice.classList.add('visible');
      // small wobble
      cake3d.animate([{transform:'translateY(0)'},{transform:'translateY(-8px)'},{transform:'translateY(0)'}],{duration:900,iterations:1});
      // confetti burst
      spawnConfetti(200);
      // optional: play music
      playAudioIfAvailable();
    }

    openCakeBtn.addEventListener('click', cutCake);
    cake3d.addEventListener('click', cutCake);

    // --- confetti (simple canvas)
    const ctx = confettiCanvas.getContext('2d');
    let W,H;
    function resize(){ W = confettiCanvas.width = confettiCanvas.clientWidth; H = confettiCanvas.height = confettiCanvas.clientHeight; }
    window.addEventListener('resize', resize); resize();
    const colors = ['#ff6b81','#ffd166','#8be9fd','#6a5cff','#7efc82'];
    let pieces = [];
    function random(min,max){return Math.random()*(max-min)+min}
    function spawnConfetti(n=80){
      for(let i=0;i<n;i++){
        pieces.push({
          x: random(0,W), y: random(-H,0),
          w: random(6,16), h: random(8,18),
          vx: random(-2,2), vy: random(2,7),
          r: random(0,360), color: colors[Math.floor(Math.random()*colors.length)]
        });
      }
    }
    function update(){
      ctx.clearRect(0,0,W,H);
      for(const p of pieces){
        p.x += p.vx; p.y += p.vy; p.r += p.vx*3;
        ctx.save(); ctx.translate(p.x,p.y); ctx.rotate(p.r*Math.PI/180);
        ctx.fillStyle = p.color; ctx.fillRect(-p.w/2,-p.h/2, p.w, p.h);
        ctx.restore();
      }
      pieces = pieces.filter(p => p.y < H + 40);
      requestAnimationFrame(update);
    }
    update();

    // toggle confetti
    let confOn = true;
    toggleConfetti.addEventListener('click', ()=>{
      confOn = !confOn;
      confettiCanvas.style.display = confOn ? 'block' : 'none';
    });

    // convenience: spawn small burst once on load if name present
    if(localStorage.getItem('hb_name')) setTimeout(()=>spawnConfetti(40),600);

    // --- music handling
    function playAudioIfAvailable(){
      if(bgMusic.querySelector('source')){
        bgMusic.play().catch(()=>{ console.log('autoplay blocked'); });
        playMusic.textContent = 'Pause ⏸';
      }
    }
    playMusic.addEventListener('click', ()=>{
      if(bgMusic.paused){ bgMusic.play().catch(()=>alert('Browser blocked autoplay. Add music.mp3 to root and allow play.')); playMusic.textContent='Pause ⏸'; }
      else { bgMusic.pause(); playMusic.textContent='Play Music ▶'; }
    });

    // --- gallery modal
    gallery.addEventListener('click', (e)=>{
      const img = e.target.closest('img');
      if(!img) return;
      modalImg.src = img.src;
      modalCaption.textContent = img.dataset.caption || 'Memory';
      modal.classList.add('show');
    });
    closeModal.addEventListener('click', ()=>{ modal.classList.remove('show'); });

    // close on backdrop click
    modal.addEventListener('click', (e)=>{ if(e.target === modal) modal.classList.remove('show'); });

    // --- download image (simple screenshot via SVG foreignObject)
    downloadBtn.addEventListener('click', async ()=>{
      const stage = document.getElementById('stage');
      const svg = `<svg xmlns='http://www.w3.org/2000/svg' width='1200' height='630'><foreignObject width='100%' height='100%'>${new XMLSerializer().serializeToString(stage)}</foreignObject></svg>`;
      const blob = new Blob([svg],{type:'image/svg+xml;charset=utf-8'});
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a'); a.href = url; a.download = 'birthday-card.svg'; a.click(); URL.revokeObjectURL(url);
    });

    // restart animation (reset)
    restartBtn.addEventListener('click', ()=>{
      cut = false;
      slice.classList.remove('visible');
      const layers = cake3d.querySelectorAll('.cake-layer');
      layers.forEach((el)=> el.style.transform = '');
      spawnConfetti(60);
    });

    // keyboard shortcut
    window.addEventListener('keydown', (e)=>{ if(e.key.toLowerCase()==='w'){ cutCake(); } });

    // set default images exist check: if missing, show placeholder text
    document.querySelectorAll('.gallery img').forEach(img=>{
      img.onerror = ()=>{ img.style.opacity = .35; img.style.objectFit='contain'; img.src = 'data:image/svg+xml;utf8,' + encodeURIComponent(`<svg xmlns="http://www.w3.org/2000/svg" width="400" height="250"><rect width="100%" height="100%" fill="#0f172a"/><text x="50%" y="50%" fill="#fff" font-family="Arial" font-size="18" text-anchor="middle" dy=".3em">Place ${img.getAttribute('alt')} in images/</text></svg>`); }
    });

  </script>
</body>
</html>
