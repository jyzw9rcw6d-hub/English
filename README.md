<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8" />
<meta name="viewport"
content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>

<title>ENGLISH ENGINE Ultimate</title>

<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@700;800&family=Noto+Sans+JP:wght@300;400;500&display=swap" rel="stylesheet">

<style>

:root{
  --bg:#080A0F;
  --card:#0E1219;
  --border:rgba(255,255,255,0.08);
  --border-bright:rgba(255,255,255,0.16);

  --text:#D5DBE7;
  --text-dim:rgba(255,255,255,0.38);

  --accent:#00D4FF;
  --accent-glow:rgba(0,212,255,0.25);

  --green:#00FF8C;
  --green-bg:rgba(0,255,140,0.08);
  --green-border:rgba(0,255,140,0.35);

  --red:#FF4D4D;
  --red-bg:rgba(255,77,77,0.08);
  --red-border:rgba(255,77,77,0.35);

  --yellow:#FFB800;
  --purple:#B95CFF;

  --mono:'Space Mono', monospace;
  --display:'Syne', sans-serif;
  --jp:'Noto Sans JP', sans-serif;
}

*{
  margin:0;
  padding:0;
  box-sizing:border-box;
}

html{
  scroll-behavior:smooth;
}

body{
  background:var(--bg);
  color:var(--text);
  font-family:var(--jp);
  min-height:100vh;
  overflow-x:hidden;
}

button{
  touch-action:manipulation;
}

body::before{
  content:'';
  position:fixed;
  inset:0;

  background-image:
    linear-gradient(rgba(255,255,255,0.025) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.025) 1px, transparent 1px);

  background-size:44px 44px;
  pointer-events:none;
}

body::after{
  content:'';
  position:fixed;
  inset:0;

  background:
    radial-gradient(circle at 10% 0%, rgba(0,212,255,0.08), transparent 30%),
    radial-gradient(circle at 90% 100%, rgba(185,92,255,0.08), transparent 35%);

  pointer-events:none;
}

.wrap{
  position:relative;
  z-index:1;
  max-width:700px;
  margin:auto;
  padding:2rem 1rem 4rem;
}

/* HEADER */

.header{
  margin-bottom:2rem;
}

.header-eye{
  font-family:var(--mono);
  font-size:10px;
  letter-spacing:.28em;
  color:var(--accent);
  opacity:.7;
  margin-bottom:.6rem;
}

.header-title{
  font-family:var(--display);
  font-size:clamp(42px, 10vw, 74px);
  font-weight:800;
  line-height:.92;
  color:white;
}

.header-title span{
  display:block;

  background:linear-gradient(90deg, var(--accent), var(--purple));

  -webkit-background-clip:text;
  -webkit-text-fill-color:transparent;
}

.header-rule{
  margin-top:1rem;
  width:60px;
  height:1px;
  background:linear-gradient(90deg,var(--accent),transparent);
}

/* CARD */

.card{
  background:rgba(255,255,255,0.03);
  border:1px solid var(--border);
  border-radius:14px;
  padding:1.5rem;
  overflow:hidden;
  position:relative;
}

.card::before{
  content:'';
  position:absolute;
  left:0;
  top:0;
  width:100%;
  height:1px;

  background:
    linear-gradient(
      90deg,
      transparent,
      var(--accent),
      transparent
    );
}

/* META */

.meta{
  display:flex;
  justify-content:space-between;
  align-items:center;
  gap:1rem;
  margin-bottom:1.5rem;
}

.badges{
  display:flex;
  flex-wrap:wrap;
  gap:8px;
}

.badge{
  font-family:var(--mono);
  font-size:10px;
  letter-spacing:.16em;
  padding:4px 10px;
  border-radius:4px;
  border:1px solid;
}

.badge-field{
  color:var(--accent);
  border-color:rgba(0,212,255,.3);
  background:rgba(0,212,255,.08);
}

.badge-easy{
  color:var(--green);
  border-color:rgba(0,255,140,.35);
  background:rgba(0,255,140,.08);
}

.badge-mid{
  color:var(--yellow);
  border-color:rgba(255,184,0,.35);
  background:rgba(255,184,0,.08);
}

.badge-hard{
  color:var(--red);
  border-color:rgba(255,77,77,.35);
  background:rgba(255,77,77,.08);
}

.counter{
  font-family:var(--mono);
  font-size:11px;
  letter-spacing:.15em;
  color:var(--text-dim);
}

/* SECTION */

.sec-label{
  font-family:var(--mono);
  font-size:9px;
  letter-spacing:.3em;
  color:var(--text-dim);
  margin-bottom:12px;
}

/* QUESTION */

.q-sentence{
  font-size:1.08rem;
  line-height:1.95;
  color:white;
  font-weight:300;
  word-break:break-word;
  margin-bottom:.6rem;
}

.q-blank{
  display:inline-block;
  min-width:90px;
  text-align:center;
  border-bottom:2px solid var(--accent);
  color:var(--accent);
  font-family:var(--mono);
  font-weight:700;
  letter-spacing:.12em;
}

.q-inst{
  font-family:var(--mono);
  font-size:10px;
  color:var(--text-dim);
  letter-spacing:.16em;
  margin-bottom:1.4rem;
}

/* CHOICES */

.choices{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:10px;
}

.choice{
  background:transparent;
  border:1px solid var(--border-bright);
  border-radius:8px;

  padding:14px;

  display:flex;
  gap:10px;
  align-items:flex-start;

  color:var(--text);
  cursor:pointer;

  transition:.15s;
}

.choice:hover:not(:disabled){
  border-color:var(--accent);
  background:rgba(255,255,255,0.04);
  color:white;
}

.choice:disabled{
  cursor:not-allowed;
}

.choice-label{
  font-family:var(--mono);
  font-size:10px;
  color:var(--text-dim);
  min-width:16px;
}

.choice.correct{
  background:var(--green-bg);
  border-color:var(--green-border);
  color:var(--green);
}

.choice.correct .choice-label{
  color:var(--green);
}

.choice.wrong{
  background:var(--red-bg);
  border-color:var(--red-border);
  color:var(--red);
}

.choice.wrong .choice-label{
  color:var(--red);
}

.choice.reveal{
  background:var(--green-bg);
  border-color:var(--green-border);
  color:var(--green);
  opacity:.55;
}

/* RESULT */

.result{
  display:none;
  margin-top:1rem;
  border-radius:8px;
  padding:15px;
  animation:fade .25s ease;
}

.result.correct-res{
  background:var(--green-bg);
  border:1px solid var(--green-border);
}

.result.wrong-res{
  background:var(--red-bg);
  border:1px solid var(--red-border);
}

.result-title{
  font-family:var(--mono);
  font-size:10px;
  letter-spacing:.25em;
  margin-bottom:8px;
}

.result-exp{
  margin-top:10px;
  padding-top:10px;
  border-top:1px solid var(--border);
  line-height:1.8;
  color:var(--text);
  font-size:14px;
}

/* BUTTON */

.btn-row{
  margin-top:1.5rem;
}

.btn-main{
  width:100%;
  border:none;
  border-radius:8px;
  padding:15px;

  background:var(--accent);
  color:#081018;

  font-family:var(--mono);
  font-size:11px;
  font-weight:700;
  letter-spacing:.2em;

  cursor:pointer;
  transition:.18s;
}

.btn-main:hover{
  transform:translateY(-1px);
  box-shadow:0 0 24px var(--accent-glow);
}

/* STATS */

.stats{
  margin-top:10px;

  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:10px;
}

.stat{
  background:rgba(255,255,255,0.03);
  border:1px solid var(--border);
  border-radius:12px;
  padding:16px;
  text-align:center;
}

.stat-val{
  font-family:var(--mono);
  font-size:28px;
  font-weight:700;
  margin-bottom:6px;
}

.stat-lbl{
  font-family:var(--mono);
  font-size:9px;
  letter-spacing:.24em;
  color:var(--text-dim);
}

/* LOADER */

.loader{
  display:none;
  align-items:flex-end;
  gap:5px;
  height:34px;
  margin-bottom:1rem;
}

.loader.active{
  display:flex;
}

.loader div{
  width:4px;
  border-radius:999px;
  background:var(--accent);
  animation:loader 1s infinite ease-in-out;
}

.loader div:nth-child(1){height:40%; animation-delay:0s;}
.loader div:nth-child(2){height:100%; animation-delay:.1s;}
.loader div:nth-child(3){height:60%; animation-delay:.2s;}
.loader div:nth-child(4){height:80%; animation-delay:.3s;}
.loader div:nth-child(5){height:35%; animation-delay:.4s;}

@keyframes loader{
  0%,100%{
    opacity:.25;
    transform:scaleY(.7);
  }
  50%{
    opacity:1;
    transform:scaleY(1);
  }
}

@keyframes fade{
  from{
    opacity:0;
    transform:translateY(6px);
  }
  to{
    opacity:1;
    transform:none;
  }
}

@media(max-width:640px){

  .choices{
    grid-template-columns:1fr;
  }

}

</style>
</head>
<body>

<div class="wrap">

<header class="header">
  <div class="header-eye">// Grammar · Vocabulary · Medical Level</div>

  <h1 class="header-title">
    ENGLISH
    <span>ENGINE</span>
  </h1>

  <div class="header-rule"></div>
</header>

<div class="card">

  <div class="meta">
    <div class="badges" id="tags"></div>
    <div class="counter" id="counter">Q — 000</div>
  </div>

  <div class="loader" id="loader">
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
  </div>

  <div id="q-wrap">

    <div class="sec-label">QUESTION</div>

    <div class="q-sentence" id="q-sentence"></div>

    <div class="q-inst">
      ↑ 空欄に入る最も適切なものを選べ
    </div>

    <div class="sec-label">CHOICES</div>

    <div class="choices" id="choices"></div>

    <div class="result" id="result">

      <div class="result-title" id="result-title"></div>

      <div id="result-answer"></div>

      <div class="result-exp" id="result-exp"></div>

    </div>

  </div>

  <div class="btn-row">
    <button class="btn-main" onclick="generateQuestion()">
      GENERATE →
    </button>
  </div>

</div>

<div class="stats">

  <div class="stat">
    <div class="stat-val" id="stat-total" style="color:var(--accent)">
      0
    </div>
    <div class="stat-lbl">TOTAL</div>
  </div>

  <div class="stat">
    <div class="stat-val" id="stat-correct" style="color:var(--green)">
      0
    </div>
    <div class="stat-lbl">CORRECT</div>
  </div>

  <div class="stat">
    <div class="stat-val" id="stat-rate">
      —
    </div>
    <div class="stat-lbl">RATE</div>
  </div>

</div>

</div>

<script>

/* =========================
   UTIL
========================= */

function pick(arr){
  return arr[Math.floor(Math.random() * arr.length)];
}

function shuffle(arr){

  const a = arr.slice();

  for(let i = a.length - 1; i > 0; i--){

    const j = Math.floor(Math.random() * (i + 1));

    [a[i], a[j]] = [a[j], a[i]];
  }

  return a;
}

function createQuestion({
  cat,
  lv,
  q,
  ans,
  wrong,
  exp
}){

  return {
    cat,
    lv,
    q,
    ans,
    choices: shuffle([ans, ...wrong]),
    exp
  };
}

/* =========================
   DATA
========================= */

/* =========================
   医学部問題
========================= */

const medicalQuestions = [

  createQuestion({
    cat:"医学部単語",
    lv:"医学部",
    q:"The vaccine was proven highly ___.",
    ans:"effective",
    wrong:["harmful","fragile","ordinary"],
    exp:"effective = 効果的な。"
  })

];

/* =========================
   全問題をまとめる
========================= */

const questions = [
  ...medicalQuestions
];

/* =========================
   CONFIG
========================= */

const LABELS = ['A','B','C','D'];

const levelConfig = {

  "基礎":{
    cls:"badge-easy",
    label:"BASIC"
  },

  "標準":{
    cls:"badge-mid",
    label:"STANDARD"
  },

  "難関大":{
    cls:"badge-hard",
    label:"ADVANCED"
  },

  "医学部":{
    cls:"badge-hard",
    label:"MEDICAL"
  }

};

/* =========================
   STATE
========================= */

let total = 0;
let correct = 0;

let answered = false;
let currentQuestion = null;
let lastQuestion = null;

/* =========================
   STORAGE
========================= */

function saveStats(){

  localStorage.setItem(
    'english_engine_stats',

    JSON.stringify({
      total,
      correct
    })
  );
}

function loadStats(){

  const saved =
    JSON.parse(
      localStorage.getItem('english_engine_stats')
    );

  if(saved){

    total = saved.total || 0;
    correct = saved.correct || 0;

    updateStats();
  }
}

/* =========================
   GENERATE
========================= */

function generateQuestion(){

  answered = false;

  const loader = document.getElementById('loader');
  const qWrap = document.getElementById('q-wrap');
  const result = document.getElementById('result');

  loader.classList.add('active');

  qWrap.style.opacity = '0';

  result.style.display = 'none';

  setTimeout(() => {

    let q;

    do{
      q = pick(questions);
    }
    while(q === lastQuestion && questions.length > 1);

    lastQuestion = q;

    currentQuestion = q;

    renderQuestion(q);

    loader.classList.remove('active');

    qWrap.style.transition = '.25s';
    qWrap.style.opacity = '1';

  }, 180);

}

/* =========================
   RENDER
========================= */

function renderQuestion(q){

  const level = levelConfig[q.lv];

  document.getElementById('tags').innerHTML = `
    <span class="badge badge-field">${q.cat}</span>
    <span class="badge ${level.cls}">
      ${level.label}
    </span>
  `;

  document.getElementById('counter').textContent =
    'Q — ' + String(total + 1).padStart(3, '0');

  const sentence =
    q.q.replace(
      /___/g,
      '<span class="q-blank">___</span>'
    );

  document.getElementById('q-sentence').innerHTML =
    sentence;

  const choicesEl =
    document.getElementById('choices');

  choicesEl.innerHTML = '';

  q.choices.forEach((choice, index) => {

    const btn = document.createElement('button');

    btn.className = 'choice';

    btn.dataset.answer = choice;

    btn.innerHTML = `
      <span class="choice-label">${LABELS[index]}</span>
      <span>${choice}</span>
    `;

    btn.onclick = () => checkAnswer(choice, q.ans);

    choicesEl.appendChild(btn);

  });

}

/* =========================
   CHECK
========================= */

function checkAnswer(selected, correct){

  if(answered) return;

  answered = true;

  const isCorrect = selected === correct;

  const choices = document.querySelectorAll('.choice');

  choices.forEach(btn => {

    btn.disabled = true;

    if(btn.dataset.answer === correct){
      btn.classList.add('correct');
    }
    else if(btn.dataset.answer === selected && !isCorrect){
      btn.classList.add('wrong');
    }
    else{
      btn.classList.add('reveal');
    }

  });

  total++;
  if(isCorrect) correct++;

  updateStats();

  const result = document.getElementById('result');
  result.style.display = 'block';

  const resultTitle = document.getElementById('result-title');
  const resultAnswer = document.getElementById('result-answer');
  const resultExp = document.getElementById('result-exp');

  if(isCorrect){
    result.className = 'result correct-res';
    resultTitle.textContent = '✓ CORRECT';
  }
  else{
    result.className = 'result wrong-res';
    resultTitle.textContent = '✗ WRONG';
  }

  resultAnswer.innerHTML = `<strong>Answer: ${correct}</strong>`;
  resultExp.textContent = currentQuestion.exp;

}

/* =========================
   UPDATE STATS
========================= */

function updateStats(){

  document.getElementById('stat-total').textContent = total;
  document.getElementById('stat-correct').textContent = correct;

  const rate = total === 0 ? '—' : (correct / total * 100).toFixed(1) + '%';
  document.getElementById('stat-rate').textContent = rate;

  saveStats();

}

/* =========================
   INIT
========================= */

window.addEventListener('load', () => {

  loadStats();

  if(questions.length === 0){
    document.getElementById('q-sentence').innerHTML = 'No questions available';
  }
  else{
    generateQuestion();
  }

});

</script>

</body>
</html>
