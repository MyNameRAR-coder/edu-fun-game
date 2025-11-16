<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Edu-Fun — Game Browser</title>
<style>
:root{
  --bg:#0f1724;
  --card:#0b1220;
  --accent:#4f46e5;
  --muted:#94a3b8;
  --glass:rgba(255,255,255,0.03)
}
*{box-sizing:border-box;margin:0;padding:0}
body{
  font-family:Inter,ui-sans-serif,system-ui,-apple-system,'Segoe UI',Roboto,'Helvetica Neue',Arial;
  background:linear-gradient(180deg,#071029 0%,#0f1724 100%);
  color:#e6eef8;
}
header{
  display:flex;align-items:center;justify-content:space-between;
  padding:18px 28px;background:linear-gradient(90deg,rgba(255,255,255,0.03),transparent);
  backdrop-filter: blur(4px)
}
.brand{display:flex;gap:12px;align-items:center}
.logo{width:44px;height:44px;border-radius:8px;
  background:linear-gradient(135deg,var(--accent),#06b6d4);
  display:flex;align-items:center;justify-content:center;font-weight:700
}
h1{font-size:18px;margin:0}
.controls{display:flex;gap:12px;align-items:center}
.btn{background:var(--accent);border:none;padding:10px 14px;border-radius:10px;color:white;cursor:pointer;font-weight:600}
.container{max-width:1100px;margin:26px auto;padding:18px}
.grid{display:grid;grid-template-columns:320px 1fr;gap:18px}
.card{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));border-radius:12px;padding:16px;box-shadow:0 6px 18px rgba(2,6,23,0.6)}
.modes{display:flex;flex-direction:column;gap:10px}
.mode-btn{display:flex;align-items:center;gap:12px;padding:12px;border-radius:10px;background:var(--glass);cursor:pointer}
.mode-btn:hover{transform:translateY(-4px);transition:all .18s}
.small{font-size:13px;color:var(--muted)}
.game-top{display:flex;justify-content:space-between;align-items:center;margin-bottom:12px}
.timer{font-weight:700;font-size:20px}
.question-card{
  padding:18px;border-radius:10px;background:linear-gradient(90deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
  margin-bottom:12px;overflow:hidden;position:relative
}
.q-text{font-size:22px;font-weight:700;min-height:60px}
.options{display:grid;grid-template-columns:repeat(2,1fr);gap:10px;margin-top:12px}
.opt{padding:12px;border-radius:10px;background:#071627;cursor:pointer;border:1px solid rgba(255,255,255,0.03);transition:transform .3s}
.opt.correct{outline:3px solid rgba(34,197,94,0.18)}
.opt.wrong{outline:3px solid rgba(239,68,68,0.18)}
.footer-controls{display:flex;gap:10px;align-items:center;justify-content:flex-end;margin-top:10px}
.leaderboard{margin-top:12px}
.list{max-height:220px;overflow:auto}
.li{display:flex;justify-content:space-between;padding:8px;border-bottom:1px solid rgba(255,255,255,0.02)}
.hidden{display:none}
@media (max-width:900px){.grid{grid-template-columns:1fr}}
.slide-enter{transform:translateX(100%);opacity:0}
.slide-enter-active{transform:translateX(0);opacity:1;transition:all .4s}
.slide-exit{transform:translateX(0);opacity:1}
.slide-exit-active{transform:translateX(-100%);opacity:0;transition:all .4s}
</style>
</head>
<body>
<header>
<div class="brand"><div class="logo">ED</div><div><h1>Edu-Fun</h1><div class="small">Game Browser</div></div></div>
<div class="controls">
<button class="audio-toggle" id="muteBtn">🔊 Music On</button>
<button class="btn" id="profileBtn">Profile</button>
</div>
</header>

<main class="container">
<div class="grid">
<aside class="card">
  <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:12px">
    <div>
      <div class="small">XP</div>
      <div style="font-weight:800;font-size:18px">Level 3 — 680 XP</div>
    </div>
    <div style="text-align:right">
      <div class="small">Best</div>
      <div style="font-weight:800">123 pts</div>
    </div>
  </div>

  <div class="modes">
    <div class="mode-btn" data-mode="timer"><div style="font-weight:800">Time Rush</div><div class="small">Jawab sebanyak mungkin dalam 60 detik</div></div>
    <div class="mode-btn" data-mode="map"><div style="font-weight:800">World Map Quiz</div><div class="small">Tebak bendera & letak negara</div></div>
    <div class="mode-btn" data-mode="general"><div style="font-weight:800">General Knowledge</div><div class="small">Trivia global & Indonesia</div></div>
    <div class="mode-btn" data-mode="math"><div style="font-weight:800">Math Mode</div><div class="small">Latihan matematika dasar</div></div>
    <div class="mode-btn" data-mode="survival"><div style="font-weight:800">Survival Mode</div><div class="small">Bertahan dengan kesulitan meningkat</div></div>
  </div>

  <div class="leaderboard card" style="margin-top:14px">
    <div style="font-weight:800;margin-bottom:8px">Leaderboard (Local)</div>
    <div class="list" id="leaderList"></div>
  </div>
</aside>

<section class="card" id="mainArea">
<div id="intro">
<h2>Selamat datang!</h2>
<p class="small">Pilih mode dan tingkat kesulitan, fokus, dan bersenang-senang!</p>
</div>

<div id="gameArea" class="hidden">
<div class="game-top">
<div class="timer">⏱ <span id="timerDisplay">--</span></div>
<div>
<label class="small">Kesulitan:
<select id="difficulty">
<option value="mudah">Mudah</option>
<option value="sedang">Sedang</option>
<option value="sulit">Sulit</option>
</select></label>
</div>
</div>

<div id="singleArea">
<div class="question-card" id="questionCard">
<div class="q-text" id="qSingle">–</div>
<div class="options" id="optsSingle"></div>
</div>
<div class="footer-controls">
<div class="small" id="explainSingle"></div>
<div><button class="btn" id="stopBtn">Stop</button></div>
</div>
</div>
</div>
</section>
</div>
</main>

<audio id="bgMusic" loop src="music/theme.mp3"></audio>
<audio id="sfxCorrect" src="music/correct.mp3"></audio>
<audio id="sfxWrong" src="music/wrong.mp3"></audio>
<audio id="sfxClick" src="music/click.mp3"></audio>

<script>
// ==== BANK SOAL (singkat contoh, lengkapkan 240+) ====
const questions={
general:{mudah:[{q:'Ibukota Indonesia?',opts:['Jakarta','Bandung','Surabaya','Medan'],a:'Jakarta',ex:'Ibukota Indonesia adalah Jakarta'}],
sedang:[{q:'Presiden Indonesia ke-3?',opts:['Sukarno','Soeharto','BJ Habibie','Megawati'],a:'BJ Habibie',ex:'BJ Habibie Presiden ke-3'}],
sulit:[{q:'Negara terbesar di dunia?',opts:['USA','China','Rusia','Kanada'],a:'Rusia',ex:'Rusia negara terbesar'}]},
math:{mudah:[{q:'5 + 7 = ?',opts:[11,12,13,14],a:12,ex:'5 + 7 = 12'}],
sedang:[{q:'15 ÷ 3 = ?',opts:[4,5,6,7],a:5,ex:'15 ÷ 3 = 5'}],
sulit:[{q:'72 ÷ 8 + 5 = ?',opts:[13,14,15,16],a:14,ex:'72 ÷ 8 + 5 = 14'}]},
map:{mudah:[{q:'🇮🇩 Negara ini?',opts:['Indonesia','Malaysia','Philippines','Brunei'],a:'Indonesia',ex:'Bendera merah putih'}],
sedang:[{q:'🇮🇳 Negara ini?',opts:['Pakistan','India','Bangladesh','Nepal'],a:'India',ex:'Bendera India'}],
sulit:[{q:'🇧🇩 Negara ini?',opts:['Bangladesh','Pakistan','India','Nepal'],a:'Bangladesh',ex:'Bendera hijau merah'}]}
};

// ==== GAME LOGIC ====
let mode=null, timerInterval=null, timeLeft=0, sessionActive=false, currentQSet=[], qIndex=0, score=0;

const bg=document.getElementById('bgMusic');
const sfxCorrect=document.getElementById('sfxCorrect');
const sfxWrong=document.getElementById('sfxWrong');
const sfxClick=document.getElementById('sfxClick');
const muteBtn=document.getElementById('muteBtn');
const difficultySelect=document.getElementById('difficulty');
const questionCard=document.getElementById('questionCard');

function playSfxSafe(el){try{if(el){el.currentTime=0;el.play().catch(()=>{});}}catch(e){}}
function playSfxCorrect(){playSfxSafe(sfxCorrect);}
function playSfxWrong(){playSfxSafe(sfxWrong);}
function playSfxClick(){playSfxSafe(sfxClick);}

muteBtn.addEventListener('click',()=>{
  sessionActive=!sessionActive;
  if(sessionActive){ bg.play().catch(()=>{}); muteBtn.innerText='🔈 Music On';}
  else{ bg.pause(); muteBtn.innerText='🔇 Music Off';}
});

function loadLeaderboard(){ const raw=localStorage.getItem('edu_leader'); return raw? JSON.parse(raw):[] }
function saveLeaderboard(list){ localStorage.setItem('edu_leader',JSON.stringify(list)); renderLeaderboard(); }
function addLeaderboard(name,score){ let l=loadLeaderboard(); l.push({name,score,date:Date.now()}); l.sort((a,b)=>b.score-b.score); while(l.length>10) l.pop(); saveLeaderboard(l); }
function renderLeaderboard(){ const list=loadLeaderboard(); const el=document.getElementById('leaderList'); el.innerHTML=''; list.forEach(i=>{ const d=document.createElement('div'); d.className='li'; d.innerHTML=`<div>${i.name}</div><div>${i.score}</div>`; el.appendChild(d); }); }
renderLeaderboard();

document.querySelectorAll('.mode-btn').forEach(b=>b.addEventListener('click',()=>{
  playSfxClick(); const m=b.getAttribute('data-mode'); if(m) start(m);
}));
document.getElementById('stopBtn').addEventListener('click',()=>{ playSfxClick(); endSession(); });

function shuffle(a){return a.slice().sort(()=>Math.random()-0.5);}

function start(which){
  mode=which; document.getElementById('intro').classList.add('hidden'); document.getElementById('gameArea').classList.remove('hidden'); sessionActive=true;
  score=0; qIndex=0;
  if(which==='timer') startTimerMode(60);
  else if(which==='survival') startSurvivalMode();
  else startSingleMode(which);
}

function endSession(){sessionActive=false; clearInterval(timerInterval); document.getElementById('gameArea').classList.add('hidden'); document.getElementById('intro').classList.remove('hidden');}

function startSingleMode(type){
  const diff=difficultySelect.value;
  if(type==='map') currentQSet=shuffle(questions.map[diff]);
  else if(type==='general') currentQSet=shuffle(questions.general[diff]);
  else if(type==='math') currentQSet=shuffle(questions.math[diff]);
  qIndex=0; score=0; loadQuestion();
}

function loadQuestion(){
  if(qIndex>=currentQSet.length){ addLeaderboard('You',score); endSession(); return; }
  const q=currentQSet[qIndex];
  questionCard.classList.add('slide-enter'); setTimeout(()=>questionCard.classList.remove('slide-enter'),10);
  document.getElementById('qSingle').innerText=q.q;
  const opts=document.getElementById('optsSingle'); opts.innerHTML='';
  shuffle(q.opts).forEach(o=>{
    const d=document.createElement('div'); d.className='opt'; d.innerText=o;
    d.onclick=()=>handleAnswer(o,q);
    opts.appendChild(d);
  });
}

function handleAnswer(o,q){
  if(o===q.a){ playSfxCorrect(); score++; document.getElementById('explainSingle').innerText=q.ex; }
  else { playSfxWrong(); document.getElementById('explainSingle').innerText='Salah. '+q.ex; }
  qIndex++; setTimeout(loadQuestion,400);
}

function startTimerMode(sec){
  timeLeft=sec; score=0; document.getElementById('timerDisplay').innerText=timeLeft;
  const diff=difficultySelect.value; currentQSet=shuffle([...questions.general[diff],...questions.math[diff],...questions.map[diff]]); qIndex=0;
  timerInterval=setInterval(()=>{
    timeLeft--; document.getElementById('timerDisplay').innerText=timeLeft;
    if(timeLeft<=0){clearInterval(timerInterval); addLeaderboard('You',score); endSession();}
  },1000);
  loadQuestion();
}

function startSurvivalMode(){
  score=0; qIndex=0; timeLeft=10;
  const diff=difficultySelect.value; currentQSet=shuffle([...questions.general[diff],...questions.math[diff],...questions.map[diff]]);
  document.getElementById('timerDisplay').innerText=timeLeft;
  loadQuestion();
  timerInterval=setInterval(()=>{
    timeLeft--; document.getElementById('timerDisplay').innerText=timeLeft;
    if(timeLeft<=0){clearInterval(timerInterval); addLeaderboard('You',score); endSession();}
  },1000);
}
</script>
</body>
</html>
