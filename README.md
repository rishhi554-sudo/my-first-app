<!DOCTYPE html>

<html lang="en">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">

<title>Regimen — Personal Training Journal</title>

<link rel="preconnect" href="https://fonts.googleapis.com">

<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,400;9..144,500;9..144,600&family=Manrope:wght@400;500;600;700;800&display=swap" rel="stylesheet">

<style>

  :root{

    --bg: #F5F3EE;

    --paper: #FBFAF7;

    --card: #FFFFFF;

    --ink: #22261F;

    --ink-soft: #5B6157;

    --navy: #182433;

    --sage: #66735F;

    --gold: #C6A15B;

    --gold-soft: #E7D9BB;

    --line: #E4E0D6;

    --rest: #7C8B72;

    --danger: #B4553F;

    --radius-lg: 22px;

    --radius-md: 14px;

    --radius-sm: 9px;

    --shadow: 0 1px 2px rgba(24,36,51,0.04), 0 8px 24px rgba(24,36,51,0.06);

    box-sizing:border-box;

    padding-top: env(safe-area-inset-top, 0px);

    padding-bottom: env(safe-area-inset-bottom, 0px);

  }

  *{box-sizing:border-box;}

  html{scroll-padding-top: env(safe-area-inset-top, 0px);}

  html,body{height:100%;}

  body{

    margin:0;

    background:var(--bg);

    background-image:

      radial-gradient(circle at 100% 0%, rgba(198,161,91,0.08), transparent 45%),

      radial-gradient(circle at 0% 100%, rgba(102,115,95,0.06), transparent 40%);

    color:var(--ink);

    font-family:'Manrope', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;

    -webkit-font-smoothing:antialiased;

    min-height:100%;

  }

  h1,h2,h3,.serif{

    font-family:'Fraunces', Georgia, serif;

    font-weight:500;

    letter-spacing:-0.01em;

  }

  button{font-family:inherit;}

  ::selection{ background: var(--gold-soft); }

 

  /* ---------- Layout shell ---------- */

  #app{ max-width: 640px; margin: 0 auto; padding: 0 18px 100px; }

  @media (min-width:860px){

    #app{ max-width: 760px; padding: 0 32px 60px; }

  }

 

  /* ---------- Top bar ---------- */

  .topbar{

    display:flex; align-items:center; justify-content:space-between;

    padding: 20px 2px 6px;

  }

  .brand{ display:flex; align-items:center; gap:10px; }

  .brand-mark{

    width:30px; height:30px; border-radius:8px;

    background: linear-gradient(155deg, var(--navy), #263447);

    position:relative; flex:none;

  }

  .brand-mark::after{

    content:""; position:absolute; inset:8px;

    border:1.5px solid var(--gold); border-radius:3px;

  }

  .brand-name{ font-size:15px; letter-spacing:0.04em; color:var(--navy); font-weight:700; }

  nav.desktop-nav{ display:none; gap:4px; background:var(--paper); border:1px solid var(--line); padding:4px; border-radius:999px; }

  nav.desktop-nav button{

    border:none; background:transparent; padding:8px 18px; border-radius:999px;

    font-size:13.5px; font-weight:600; color:var(--ink-soft); cursor:pointer;

    transition: background .25s ease, color .25s ease;

  }

  nav.desktop-nav button.active{ background:var(--navy); color:#fff; }

  @media (min-width:640px){ nav.desktop-nav{ display:flex; } }

 

  /* ---------- Section visibility ---------- */

  .view{ display:none; animation: fadeUp .35s ease both; }

  .view.active{ display:block; }

  @keyframes fadeUp{ from{opacity:0; transform:translateY(6px);} to{opacity:1; transform:none;} }

  @media (prefers-reduced-motion: reduce){ .view{animation:none;} }

 

  /* ---------- Greeting / hero ---------- */

  .hero{ padding: 18px 2px 4px; }

  .day-pill{

    display:inline-flex; align-items:center; gap:8px;

    font-size:12.5px; font-weight:700; letter-spacing:0.14em;

    color:var(--sage); margin-bottom:10px;

  }

  .day-pill .dot{ width:5px; height:5px; border-radius:50%; background:var(--gold); }

  .greeting{ font-size: clamp(26px,6vw,34px); color:var(--navy); margin:0 0 4px; line-height:1.15; }

  .greeting em{ font-style:normal; color:var(--gold); }

  .subline{ color:var(--ink-soft); font-size:15px; margin:0 0 22px; }

 

  /* ---------- Current workout hero card ---------- */

  .workout-hero{

    background: linear-gradient(160deg, var(--navy) 0%, #223448 100%);

    border-radius: var(--radius-lg);

    padding: 26px 24px 22px;

    color:#F4F1E9;

    position:relative;

    overflow:hidden;

    box-shadow: 0 14px 34px rgba(24,36,51,0.22);

  }

  .workout-hero::before{

    content:""; position:absolute; right:-40px; top:-40px; width:180px; height:180px;

    border-radius:50%; background: radial-gradient(circle, rgba(198,161,91,0.28), transparent 70%);

  }

  .wh-top{ display:flex; justify-content:space-between; align-items:flex-start; position:relative; }

  .wh-tag{ font-size:12px; letter-spacing:0.16em; font-weight:700; color:var(--gold); }

  .wh-count{ font-size:12px; color:rgba(244,241,233,0.65); font-weight:600; }

  .wh-title{ font-size: clamp(28px,7vw,38px); margin:10px 0 2px; color:#fff; position:relative; }

  .wh-sub{ font-size:13.5px; color:rgba(244,241,233,0.72); margin:0 0 18px; position:relative; }

  .wh-progress-row{ display:flex; align-items:center; gap:10px; position:relative; margin-bottom:4px;}

  .wh-progress-track{ flex:1; height:6px; border-radius:99px; background:rgba(255,255,255,0.14); overflow:hidden; }

  .wh-progress-fill{ height:100%; border-radius:99px; background: linear-gradient(90deg, var(--gold), #E3C583); transition: width .4s cubic-bezier(.4,0,.2,1); }

  .wh-progress-label{ font-size:12px; color:rgba(244,241,233,0.75); font-weight:600; white-space:nowrap; }

 

  /* ---------- Exercise list ---------- */

  .section-label{

    font-size:12.5px; letter-spacing:0.12em; font-weight:700; color:var(--sage);

    margin: 30px 2px 12px;

  }

  .ex-list{ display:flex; flex-direction:column; gap:10px; }

  .ex-card{

    background:var(--card); border:1px solid var(--line); border-radius: var(--radius-md);

    padding: 15px 15px 15px 18px;

    display:flex; align-items:center; justify-content:space-between; gap:14px;

    transition: border-color .2s ease, background .2s ease;

  }

  .ex-card.checked{ background: #FBF8F1; border-color: var(--gold-soft); }

  .ex-main{ min-width:0; }

  .ex-name{ font-weight:700; font-size:15px; color:var(--ink); margin:0 0 5px; }

  .ex-meta{ display:flex; flex-wrap:wrap; gap:6px; }

  .chip{

    font-size:11px; font-weight:700; letter-spacing:0.04em; padding:3px 9px; border-radius:99px;

    background:#EFEBE1; color:var(--navy);

  }

  .chip.heavy{ background:#FBEAE6; color:var(--danger); }

  .chip.moderate{ background:#EFF1E9; color:var(--sage); }

  .chip.failure{ background:var(--navy); color:#fff; }

  .checkbox{

    flex:none; width:26px; height:26px; border-radius:8px; border:2px solid var(--line);

    background:#fff; cursor:pointer; display:flex; align-items:center; justify-content:center;

    transition: all .18s ease;

  }

  .checkbox svg{ width:14px; height:14px; opacity:0; transform:scale(.5); transition: all .18s ease; }

  .checkbox.on{ background:var(--navy); border-color:var(--navy); }

  .checkbox.on svg{ opacity:1; transform:scale(1); }

 

  /* ---------- Complete button ---------- */

  .complete-bar{ margin-top:26px; }

  .btn-complete{

    width:100%; border:none; cursor:pointer; padding:17px 20px; border-radius: 16px;

    background: linear-gradient(135deg, var(--gold), #B4915A);

    color:#20180B; font-weight:800; font-size:15px; letter-spacing:0.02em;

    box-shadow: 0 10px 22px rgba(198,161,91,0.35);

    transition: transform .15s ease, box-shadow .15s ease;

  }

  .btn-complete:active{ transform: scale(0.985); box-shadow: 0 4px 12px rgba(198,161,91,0.3); }

 

  /* ---------- Rest day ---------- */

  .rest-card{

    background: linear-gradient(165deg, #EFF1E7, #E6E9DB);

    border-radius: var(--radius-lg);

    padding: 40px 26px;

    text-align:center;

    border:1px solid var(--line);

  }

  .rest-leaf{ font-size:34px; margin-bottom:10px; display:block; }

  .rest-title{ font-size:24px; color:var(--navy); margin:0 0 8px; }

  .rest-body{ color:var(--ink-soft); font-size:14.5px; line-height:1.6; max-width:360px; margin:0 auto 22px; }

  .rest-body ul{ text-align:left; display:inline-block; margin:10px 0 0; padding-left:18px; }

  .rest-body li{ margin:4px 0; }

 

  /* ---------- History ---------- */

  .hist-item{

    background:var(--card); border:1px solid var(--line); border-radius: var(--radius-md);

    padding:14px 16px; display:flex; align-items:center; justify-content:space-between; margin-bottom:9px;

  }

  .hist-left{ display:flex; align-items:center; gap:13px; }

  .hist-date{

    width:46px; text-align:center; flex:none;

  }

  .hist-date .num{ font-family:'Fraunces',serif; font-size:19px; color:var(--navy); display:block; line-height:1.1; }

  .hist-date .mon{ font-size:10px; letter-spacing:0.08em; color:var(--ink-soft); font-weight:700; }

  .hist-name{ font-weight:700; font-size:14px; }

  .hist-sub{ font-size:12px; color:var(--ink-soft); margin-top:2px; }

  .status-badge{ font-size:11.5px; font-weight:700; padding:5px 11px; border-radius:99px; white-space:nowrap; }

  .status-badge.done{ background:#E9F1E4; color:#3E6B34; }

  .status-badge.pending{ background:#F5EAE6; color:var(--danger); }

  .empty-state{ text-align:center; padding:50px 20px; color:var(--ink-soft); }

  .empty-state .glyph{ font-size:30px; display:block; margin-bottom:10px; }

 

  /* ---------- Weight tracker ---------- */

  .weight-card{ background:var(--card); border:1px solid var(--line); border-radius: var(--radius-lg); padding:22px; }

  .weight-card h2{ margin:0 0 4px; font-size:20px; color:var(--navy); }

  .weight-card p.desc{ margin:0 0 20px; color:var(--ink-soft); font-size:13.5px; }

  .weight-rows{ display:flex; flex-direction:column; gap:8px; margin-bottom:18px; }

  .weight-row{ display:flex; justify-content:space-between; align-items:baseline; padding:10px 4px; border-bottom:1px dashed var(--line); }

  .weight-row:last-child{ border-bottom:none; }

  .weight-row .wk{ font-size:13px; color:var(--ink-soft); font-weight:600; }

  .weight-row .kg{ font-family:'Fraunces',serif; font-size:18px; color:var(--ink); }

  .weight-row .delta{ font-size:11.5px; font-weight:700; margin-left:8px; }

  .delta.down{ color:#3E6B34; }

  .delta.up{ color:var(--danger); }

  .btn-add-weight{

    width:100%; padding:14px; border-radius:12px; border:1.5px dashed var(--gold);

    background:#FBF6EC; color:#8A6D34; font-weight:700; font-size:14px; cursor:pointer;

  }

  .chart-wrap{ margin-top:22px; }

 

  /* ---------- Modal ---------- */

  .modal-overlay{

    position:fixed; inset:0; background:rgba(20,24,20,0.55); backdrop-filter: blur(3px);

    display:flex; align-items:center; justify-content:center; padding:24px; z-index:50;

    opacity:0; pointer-events:none; transition:opacity .25s ease;

  }

  .modal-overlay.show{ opacity:1; pointer-events:auto; }

  .modal-card{

    background: var(--paper); border-radius:24px; padding:36px 28px; max-width:360px; width:100%;

    text-align:center; transform: translateY(10px) scale(.97); transition: transform .3s cubic-bezier(.2,.8,.2,1);

    box-shadow: 0 30px 60px rgba(0,0,0,0.35);

  }

  .modal-overlay.show .modal-card{ transform:none; }

  .modal-spark{ font-size:36px; margin-bottom:8px; display:block; }

  .modal-card h2{ font-size:24px; color:var(--navy); margin:0 0 10px; }

  .modal-card p{ color:var(--ink-soft); font-size:14.5px; line-height:1.6; margin:0 0 26px; }

  .btn-modal{

    border:none; width:100%; padding:15px; border-radius:14px; cursor:pointer;

    background:var(--navy); color:#fff; font-weight:700; font-size:14.5px;

  }

 

  /* ---------- Onboarding ---------- */

  #onboarding{

    position:fixed; inset:0; background:var(--bg); z-index:60;

    display:flex; align-items:center; justify-content:center; padding:24px;

  }

  .ob-card{ max-width:380px; width:100%; text-align:center; }

  .ob-mark{ width:52px; height:52px; border-radius:14px; margin:0 auto 22px;

    background: linear-gradient(155deg, var(--navy), #263447); position:relative; }

  .ob-mark::after{ content:""; position:absolute; inset:14px; border:2px solid var(--gold); border-radius:4px; }

  .ob-card h1{ font-size:30px; color:var(--navy); margin:0 0 10px; }

  .ob-card p{ color:var(--ink-soft); font-size:14.5px; margin:0 0 28px; }

  .ob-input{

    width:100%; padding:15px 16px; border-radius:14px; border:1.5px solid var(--line);

    background:#fff; font-size:15px; margin-bottom:14px; font-family:inherit; color:var(--ink);

  }

  .ob-input:focus{ outline:none; border-color:var(--gold); }

  .btn-start{

    width:100%; padding:16px; border-radius:14px; border:none; cursor:pointer;

    background: linear-gradient(135deg, var(--gold), #B4915A); color:#20180B;

    font-weight:800; font-size:15px; box-shadow: 0 10px 22px rgba(198,161,91,0.35);

  }

 

  /* ---------- Bottom nav (mobile) ---------- */

  .bottom-nav{

    position:fixed; left:0; right:0; bottom:0; z-index:40;

    background: rgba(251,250,247,0.92); backdrop-filter: blur(10px);

    border-top:1px solid var(--line);

    display:flex; padding: 8px 10px calc(10px + env(safe-area-inset-bottom,0px));

    gap:6px;

  }

  @media (min-width:640px){ .bottom-nav{ display:none; } #app{ padding-bottom:60px; } }

  .bn-btn{

    flex:1; border:none; background:transparent; padding:8px 4px; border-radius:12px;

    display:flex; flex-direction:column; align-items:center; gap:3px; cursor:pointer;

    color:var(--ink-soft); font-size:10.5px; font-weight:700; letter-spacing:0.03em;

  }

  .bn-btn.active{ color:var(--navy); background:#EFECE3; }

  .bn-dot{ width:5px; height:5px; border-radius:50%; background:var(--gold); opacity:0; }

  .bn-btn.active .bn-dot{ opacity:1; }

</style>

</head>

<body>

 

<div id="onboarding" style="display:none;">

  <div class="ob-card">

    <div class="ob-mark"></div>

    <h1>Welcome.</h1>

    <p>Let's get your training journal set up. What should we call you?</p>

    <input id="ob-name-input" class="ob-input" type="text" placeholder="Your name" maxlength="24" autocomplete="off">

    <button class="btn-start" id="ob-start-btn">Start training</button>

  </div>

</div>

 

<div id="app">

  <div class="topbar">

    <div class="brand">

      <div class="brand-mark"></div>

      <span class="brand-name">REGIMEN</span>

    </div>

    <nav class="desktop-nav" id="desktop-nav">

      <button data-view="today" class="active">Today</button>

      <button data-view="history">History</button>

      <button data-view="weight">Weight</button>

    </nav>

  </div>

 

  <!-- TODAY VIEW -->

  <section class="view active" id="view-today">

    <div class="hero">

      <div class="day-pill"><span class="dot"></span><span id="today-label">MONDAY</span></div>

      <h1 class="greeting" id="greeting-text">Good morning, <em>—</em></h1>

      <p class="subline" id="greeting-sub">Ready for today's session?</p>

    </div>

 

    <div class="workout-hero">

      <div class="wh-top">

        <span class="wh-tag" id="wh-tag">DAY 1 / 7</span>

        <span class="wh-count" id="wh-session">SESSION 1</span>

      </div>

      <h2 class="wh-title" id="wh-title">Upper Body</h2>

      <p class="wh-sub" id="wh-sub">7 exercises</p>

      <div class="wh-progress-row">

        <div class="wh-progress-track"><div class="wh-progress-fill" id="wh-fill" style="width:0%"></div></div>

        <span class="wh-progress-label" id="wh-progress-label">0/7</span>

      </div>

    </div>

 

    <div id="workout-body"></div>

  </section>

 

  <!-- HISTORY VIEW -->

  <section class="view" id="view-history">

    <div class="hero" style="padding-top:22px;">

      <h1 class="greeting" style="font-size:26px;">Workout history</h1>

      <p class="subline">Every session, logged.</p>

    </div>

    <div id="history-list"></div>

  </section>

 

  <!-- WEIGHT VIEW -->

  <section class="view" id="view-weight">

    <div class="hero" style="padding-top:22px;">

      <h1 class="greeting" style="font-size:26px;">Weight tracker</h1>

      <p class="subline">One number, once a cycle.</p>

    </div>

    <div class="weight-card">

      <h2>Progression</h2>

      <p class="desc">Log your weight once per completed training cycle.</p>

      <div class="weight-rows" id="weight-rows"></div>

      <button class="btn-add-weight" id="add-weight-btn">+ Add this week's weight</button>

      <div class="chart-wrap" id="weight-chart"></div>

    </div>

  </section>

</div>

 

<nav class="bottom-nav">

  <button class="bn-btn active" data-view="today"><span class="bn-dot"></span>TODAY</button>

  <button class="bn-btn" data-view="history"><span class="bn-dot"></span>HISTORY</button>

  <button class="bn-btn" data-view="weight"><span class="bn-dot"></span>WEIGHT</button>

</nav>

 

<div class="modal-overlay" id="session-modal">

  <div class="modal-card">

    <span class="modal-spark">✨</span>

    <h2>Session finished</h2>

    <p>Another cycle complete. New session, new week, new you. Ready to go again?</p>

    <button class="btn-modal" id="start-new-session-btn">Start new session</button>

  </div>

</div>

 

<script>

(function(){

  "use strict";

 

  /* =====================================================

     DATA — workout plan (exact, per spec)

  ===================================================== */

  var WORKOUTS = {

    1: { name: "Upper Body", rest: false, exercises: [

      { n:"Lat Pulldown", sets:"2 SETS", tags:["HEAVY","FAILURE"] },

      { n:"Chest Supported Row", sets:"2 SETS", tags:["HEAVY","FAILURE"] },

      { n:"Incline Bench Press", sets:"2 SETS", tags:["HEAVY","FAILURE"] },

      { n:"Pec Deck", sets:"2 SETS", tags:["MODERATE","FAILURE"] },

      { n:"Barbell Curls", sets:"2 SETS", tags:["HEAVY","FAILURE"] },

      { n:"Triceps Extensions", sets:"2 SETS", tags:["HEAVY","FAILURE"] },

      { n:"Lateral Raises", sets:"3 SETS", tags:["HEAVY","FAILURE"] }

    ]},

    2: { name: "Legs", rest: false, exercises: [

      { n:"Barbell Squats", sets:"2 SETS", tags:["HEAVY","6–10 REPS"] },

      { n:"Sumo Squat", sets:"2 SETS", tags:["HEAVY","6–10 REPS"] },

      { n:"Romanian Deadlift", sets:"2 SETS", tags:["HEAVY","6–10 REPS"] },

      { n:"Leg Extension", sets:"3 SETS", tags:["MODERATE","10–15 REPS"] },

      { n:"Hamstring Curls", sets:"3 SETS", tags:["MODERATE","10–15 REPS"] },

      { n:"Calf Raises", sets:"3 SETS", tags:["MODERATE","10–15 REPS"] }

    ]},

    3: { name: "Rest", rest: true },

    4: { name: "Push Day", rest: false, exercises: [

      { n:"Incline Dumbbell Press", sets:"2 SETS", tags:["HEAVY","6–10 REPS"] },

      { n:"Bench Press", sets:"2 SETS", tags:["HEAVY","6–10 REPS"] },

      { n:"Pec Deck", sets:"3 SETS", tags:["MODERATE","10–15 REPS"] },

      { n:"Shoulder Press", sets:"2 SETS", tags:["HEAVY","6–10 REPS"] },

      { n:"Lateral Raises", sets:"3 SETS", tags:["MODERATE","10–15 REPS"] },

      { n:"Triceps Pushdown", sets:"3 SETS", tags:["HEAVY","6–10 REPS"] },

      { n:"Skull Crusher", sets:"2 SETS", tags:["HEAVY","6–10 REPS"] },

      { n:"ABS — Hanging Leg Raises / Human Flag", sets:"", tags:["15 REPS EACH"] }

    ]},

    5: { name: "Pull Day", rest: false, exercises: [

      { n:"Pullups", sets:"3 SETS", tags:["FAILURE"] },

      { n:"Lat Pulldown", sets:"2 SETS", tags:["HEAVY","6–10 REPS"] },

      { n:"Chest Supported Rows", sets:"2 SETS", tags:["HEAVY","6–10 REPS"] },

      { n:"Single Arm Lat Pulldown", sets:"3 SETS", tags:["MODERATE","10–15 REPS"] },

      { n:"Incline Dumbbell Curls", sets:"2 SETS", tags:["HEAVY","6–10 REPS"] },

      { n:"Preacher Curls", sets:"1 SET", tags:["MODERATE","15+ REPS","FAILURE","SLOW"] },

      { n:"Rear Delt Fly", sets:"3 SETS", tags:["MODERATE","10–15 REPS"] }

    ]},

    6: { name: "Legs", rest: false, exercises: [

      { n:"Smith Squat", sets:"2 SETS", tags:["HEAVY","6–10 REPS"] },

      { n:"Deadlift", sets:"3 SETS", tags:["MOD–HEAVY","5–8 REPS"] },

      { n:"Hamstring Curls", sets:"3 SETS", tags:["MODERATE","10–15 REPS"] },

      { n:"Bulgarian Split Squats", sets:"3 SETS", tags:["MODERATE","10–15 REPS"] },

      { n:"Calf Raises", sets:"3 SETS", tags:["MODERATE","10–15 REPS"] }

    ]},

    7: { name: "Rest", rest: true }

  };

  var DAY_ORDER = [1,2,3,4,5,6,7];

 

  /* =====================================================

     STORAGE

  ===================================================== */

  var KEYS = {

    name: "wt_userName",

    started: "wt_started",

    currentDay: "wt_currentDay",

    session: "wt_session",

    checks: "wt_checks",         // { exerciseIndex: true }

    history: "wt_history",       // [{date, day, dayName, completed}]

    weights: "wt_weights",       // [{week, weight}]

    lastSeenDate: "wt_lastSeenDate"

  };

 

  function safeGet(key, fallback){

    try{

      var raw = localStorage.getItem(key);

      if(raw === null) return fallback;

      return JSON.parse(raw);

    }catch(e){ return fallback; }

  }

  function safeSet(key, val){

    try{ localStorage.setItem(key, JSON.stringify(val)); }catch(e){ /* storage unavailable */ }

  }

 

  var state = {

    name: safeGet(KEYS.name, null),

    started: safeGet(KEYS.started, false),

    currentDay: safeGet(KEYS.currentDay, 1),

    session: safeGet(KEYS.session, 1),

    checks: safeGet(KEYS.checks, {}),

    history: safeGet(KEYS.history, []),

    weights: safeGet(KEYS.weights, [])

  };

 

  function persist(){

    safeSet(KEYS.name, state.name);

    safeSet(KEYS.started, state.started);

    safeSet(KEYS.currentDay, state.currentDay);

    safeSet(KEYS.session, state.session);

    safeSet(KEYS.checks, state.checks);

    safeSet(KEYS.history, state.history);

    safeSet(KEYS.weights, state.weights);

  }

 

  /* =====================================================

     DATE HELPERS

  ===================================================== */

  var WEEKDAY_NAMES = ["SUNDAY","MONDAY","TUESDAY","WEDNESDAY","THURSDAY","FRIDAY","SATURDAY"];

  var MONTH_SHORT = ["JAN","FEB","MAR","APR","MAY","JUN","JUL","AUG","SEP","OCT","NOV","DEC"];

 

  function todayDate(){ return new Date(); }

  function dateKey(d){

    return d.getFullYear() + "-" + (d.getMonth()+1) + "-" + d.getDate();

  }

  // Monday=Day1 ... Sunday=Day7

  function calendarStartDay(d){

    var dow = d.getDay(); // 0=Sun..6=Sat

    var map = {1:1,2:2,3:3,4:4,5:5,6:6,0:7};

    return map[dow];

  }

 

  /* =====================================================

     WORKOUT LOGIC

  ===================================================== */

  function nextDay(day){

    var idx = DAY_ORDER.indexOf(day);

    var nd = DAY_ORDER[(idx+1) % DAY_ORDER.length];

    return nd;

  }

 

  function upsertHistoryEntry(entry){

    var found = null;

    for(var i=0;i<state.history.length;i++){

      if(state.history[i].date === entry.date){ found = i; break; }

    }

    if(found !== null){ state.history[found] = entry; }

    else { state.history.unshift(entry); }

  }

 

  function ensureTodayLogged(){

    var d = todayDate();

    var dk = dateKey(d);

    var already = state.history.some(function(h){ return h.date === dk; });

    if(!already){

      var w = WORKOUTS[state.currentDay];

      upsertHistoryEntry({

        date: dk,

        day: state.currentDay,

        dayName: w.name,

        completed: false,

        display: d.getDate() + " " + MONTH_SHORT[d.getMonth()]

      });

      persist();

    }

    safeSet(KEYS.lastSeenDate, dk);

  }

 

  function completeCurrentWorkout(){

    var d = todayDate();

    var dk = dateKey(d);

    var w = WORKOUTS[state.currentDay];

    upsertHistoryEntry({

      date: dk,

      day: state.currentDay,

      dayName: w.name,

      completed: true,

      display: d.getDate() + " " + MONTH_SHORT[d.getMonth()]

    });

 

    var wasDay7 = state.currentDay === 7;

    state.currentDay = nextDay(state.currentDay);

    state.checks = {};

 

    if(wasDay7){

      state.session += 1;

      persist();

      renderAll();

      showSessionModal();

      return;

    }

    persist();

    renderAll();

  }

 

  /* =====================================================

     RENDERING

  ===================================================== */

  var $ = function(sel){ return document.querySelector(sel); };

  var $$ = function(sel){ return Array.prototype.slice.call(document.querySelectorAll(sel)); };

 

  function checkSvg(){

    return '<svg viewBox="0 0 24 24" fill="none"><path d="M4 12.5L9.5 18L20 6" stroke="white" stroke-width="2.6" stroke-linecap="round" stroke-linejoin="round"/></svg>';

  }

 

  function renderGreeting(){

    var d = todayDate();

    $("#today-label").textContent = WEEKDAY_NAMES[d.getDay()];

    var hour = d.getHours();

    var salut = hour < 12 ? "Good morning" : (hour < 18 ? "Good afternoon" : "Good evening");

    $("#greeting-text").innerHTML = salut + ", <em>" + escapeHtml(state.name || "there") + "</em>";

    var w = WORKOUTS[state.currentDay];

    $("#greeting-sub").textContent = w.rest ? "Today calls for recovery." : "Ready for today's session?";

  }

 

  function escapeHtml(s){

    return String(s).replace(/[&<>"']/g, function(c){

      return {"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c];

    });

  }

 

  function tagClass(tag){

    var t = tag.toUpperCase();

    if(t.indexOf("HEAVY") !== -1) return "chip heavy";

    if(t.indexOf("MODERATE") !== -1 || t.indexOf("MOD") !== -1) return "chip moderate";

    if(t.indexOf("FAILURE") !== -1) return "chip failure";

    return "chip";

  }

 

  function renderWorkoutHero(){

    var w = WORKOUTS[state.currentDay];

    $("#wh-tag").textContent = "DAY " + state.currentDay + " / 7";

    $("#wh-session").textContent = "SESSION " + state.session;

    $("#wh-title").textContent = w.name;

 

    if(w.rest){

      $("#wh-sub").textContent = "Recovery day";

      $("#wh-progress-row").style.display = "none";

    } else {

      $("#wh-progress-row").style.display = "flex";

      $("#wh-sub").textContent = w.exercises.length + " exercises";

      var total = w.exercises.length;

      var checkedCount = w.exercises.reduce(function(acc, ex, i){

        return acc + (state.checks[i] ? 1 : 0);

      }, 0);

      var pct = total ? Math.round((checkedCount/total)*100) : 0;

      $("#wh-fill").style.width = pct + "%";

      $("#wh-progress-label").textContent = checkedCount + "/" + total;

    }

  }

 

  function renderWorkoutBody(){

    var container = $("#workout-body");

    var w = WORKOUTS[state.currentDay];

    container.innerHTML = "";

 

    if(w.rest){

      var restDiv = document.createElement("div");

      restDiv.innerHTML =

        '<div class="section-label">RECOVERY</div>' +

        '<div class="rest-card">' +

          '<span class="rest-leaf">🌿</span>' +

          '<h2 class="rest-title">Rest day</h2>' +

          '<p class="rest-body">Enjoy your rest day! But don\'t forget:' +

            '<ul><li>Get your steps in</li><li>Stay hydrated</li><li>Recover properly</li></ul>' +

          '</p>' +

          '<button class="btn-complete" id="complete-btn">✓ Complete rest day</button>' +

        '</div>';

      container.appendChild(restDiv);

    } else {

      var label = document.createElement("div");

      label.className = "section-label";

      label.textContent = "EXERCISES";

      container.appendChild(label);

 

      var list = document.createElement("div");

      list.className = "ex-list";

      w.exercises.forEach(function(ex, i){

        var checked = !!state.checks[i];

        var card = document.createElement("div");

        card.className = "ex-card" + (checked ? " checked" : "");

        card.innerHTML =

          '<div class="ex-main">' +

            '<p class="ex-name">' + escapeHtml(ex.n) + '</p>' +

            '<div class="ex-meta">' +

              (ex.sets ? '<span class="chip">' + escapeHtml(ex.sets) + '</span>' : '') +

              ex.tags.map(function(t){ return '<span class="' + tagClass(t) + '">' + escapeHtml(t) + '</span>'; }).join('') +

            '</div>' +

          '</div>' +

          '<button class="checkbox' + (checked ? ' on' : '') + '" data-idx="' + i + '" aria-label="Mark exercise done">' + checkSvg() + '</button>';

        list.appendChild(card);

      });

      container.appendChild(list);

 

      var completeWrap = document.createElement("div");

      completeWrap.className = "complete-bar";

      completeWrap.innerHTML = '<button class="btn-complete" id="complete-btn">Complete workout</button>';

      container.appendChild(completeWrap);

    }

 

    $$(".checkbox").forEach(function(btn){

      btn.addEventListener("click", function(){

        var idx = this.getAttribute("data-idx");

        state.checks[idx] = !state.checks[idx];

        persist();

        renderWorkoutHero();

        renderWorkoutBody();

      });

    });

    var cbtn = $("#complete-btn");

    if(cbtn){ cbtn.addEventListener("click", completeCurrentWorkout); }

  }

 

  function renderHistory(){

    var list = $("#history-list");

    list.innerHTML = "";

    if(state.history.length === 0){

      list.innerHTML = '<div class="empty-state"><span class="glyph">📋</span>No sessions logged yet.</div>';

      return;

    }

    var sorted = state.history.slice().sort(function(a,b){

      return new Date(b.date) - new Date(a.date);

    });

    sorted.forEach(function(h){

      var d = new Date(h.date);

      var item = document.createElement("div");

      item.className = "hist-item";

      item.innerHTML =

        '<div class="hist-left">' +

          '<div class="hist-date"><span class="num">' + d.getDate() + '</span><span class="mon">' + MONTH_SHORT[d.getMonth()] + '</span></div>' +

          '<div>' +

            '<div class="hist-name">Day ' + h.day + ' — ' + escapeHtml(h.dayName) + '</div>' +

          '</div>' +

        '</div>' +

        '<span class="status-badge ' + (h.completed ? 'done' : 'pending') + '">' + (h.completed ? '✓ Completed' : '— Incomplete') + '</span>';

      list.appendChild(item);

    });

  }

 

  function renderWeight(){

    var rows = $("#weight-rows");

    rows.innerHTML = "";

    if(state.weights.length === 0){

      rows.innerHTML = '<div class="empty-state" style="padding:24px 4px;"><span class="glyph">⚖️</span>No entries yet. Log your first weigh-in.</div>';

    } else {

      state.weights.forEach(function(w, i){

        var prev = i > 0 ? state.weights[i-1].weight : null;

        var deltaHtml = "";

        if(prev !== null){

          var d = (w.weight - prev);

          var sign = d > 0 ? "+" : "";

          deltaHtml = '<span class="delta ' + (d <= 0 ? "down" : "up") + '">' + sign + d.toFixed(1) + '</span>';

        }

        var row = document.createElement("div");

        row.className = "weight-row";

        row.innerHTML = '<span class="wk">Week ' + w.week + '</span><span><span class="kg">' + w.weight.toFixed(1) + ' kg</span>' + deltaHtml + '</span>';

        rows.appendChild(row);

      });

    }

    renderWeightChart();

  }

 

  function renderWeightChart(){

    var wrap = $("#weight-chart");

    wrap.innerHTML = "";

    if(state.weights.length < 2){

      if(state.weights.length === 1){

        wrap.innerHTML = '<p style="color:var(--ink-soft); font-size:13px; text-align:center; padding:10px 0;">Add one more entry to see your trend line.</p>';

      }

      return;

    }

    var W = 560, H = 180, pad = 28;

    var vals = state.weights.map(function(w){ return w.weight; });

    var min = Math.min.apply(null, vals), max = Math.max.apply(null, vals);

    if(min === max){ min -= 1; max += 1; }

    var n = vals.length;

    var stepX = (W - pad*2) / (n-1);

 

    function xAt(i){ return pad + i*stepX; }

    function yAt(v){ return H - pad - ((v - min)/(max-min)) * (H - pad*2); }

 

    var pts = vals.map(function(v,i){ return xAt(i) + "," + yAt(v); }).join(" ");

    var areaPts = pts + " " + xAt(n-1) + "," + (H-pad) + " " + xAt(0) + "," + (H-pad);

 

    var circles = vals.map(function(v,i){

      return '<circle cx="' + xAt(i) + '" cy="' + yAt(v) + '" r="4" fill="#C6A15B" stroke="#fff" stroke-width="2"/>';

    }).join("");

 

    var svg =

      '<svg viewBox="0 0 ' + W + ' ' + H + '" width="100%" style="display:block;">' +

        '<defs><linearGradient id="wgrad" x1="0" y1="0" x2="0" y2="1">' +

          '<stop offset="0%" stop-color="#C6A15B" stop-opacity="0.28"/>' +

          '<stop offset="100%" stop-color="#C6A15B" stop-opacity="0"/>' +

        '</linearGradient></defs>' +

        '<polygon points="' + areaPts + '" fill="url(#wgrad)"/>' +

        '<polyline points="' + pts + '" fill="none" stroke="#182433" stroke-width="2.4" stroke-linejoin="round" stroke-linecap="round"/>' +

        circles +

      '</svg>';

    wrap.innerHTML = svg;

  }

 

  function renderAll(){

    renderGreeting();

    renderWorkoutHero();

    renderWorkoutBody();

    renderHistory();

    renderWeight();

  }

 

  /* =====================================================

     NAVIGATION

  ===================================================== */

  function setView(name){

    $$(".view").forEach(function(v){ v.classList.remove("active"); });

    $("#view-" + name).classList.add("active");

    $$(".bn-btn").forEach(function(b){ b.classList.toggle("active", b.getAttribute("data-view") === name); });

    $$("#desktop-nav button").forEach(function(b){ b.classList.toggle("active", b.getAttribute("data-view") === name); });

    window.scrollTo({top:0, behavior:"smooth"});

  }

  $$(".bn-btn, #desktop-nav button").forEach(function(btn){

    btn.addEventListener("click", function(){ setView(this.getAttribute("data-view")); });

  });

 

  /* =====================================================

     MODAL

  ===================================================== */

  function showSessionModal(){

    $("#session-modal").classList.add("show");

  }

  function hideSessionModal(){

    $("#session-modal").classList.remove("show");

  }

  $("#start-new-session-btn").addEventListener("click", hideSessionModal);

 

  /* =====================================================

     WEIGHT ENTRY

  ===================================================== */

  $("#add-weight-btn").addEventListener("click", function(){

    var val = window.prompt("Enter this week's body weight (kg):");

    if(val === null) return;

    var num = parseFloat(val.replace(",", "."));

    if(isNaN(num) || num <= 0 || num > 400){

      window.alert("Please enter a valid weight in kg.");

      return;

    }

    var nextWeek = state.weights.length + 1;

    state.weights.push({ week: nextWeek, weight: num, date: dateKey(todayDate()) });

    persist();

    renderWeight();

  });

 

  /* =====================================================

     ONBOARDING

  ===================================================== */

  function beginOnboarding(){

    $("#onboarding").style.display = "flex";

    var input = $("#ob-name-input");

    var startBtn = $("#ob-start-btn");

    function commit(){

      var val = input.value.trim();

      if(!val){ input.focus(); return; }

      state.name = val.slice(0,24);

      state.started = true;

      state.currentDay = calendarStartDay(todayDate());

      state.session = 1;

      state.checks = {};

      persist();

      $("#onboarding").style.display = "none";

      ensureTodayLogged();

      renderAll();

    }

    startBtn.addEventListener("click", commit);

    input.addEventListener("keydown", function(e){ if(e.key === "Enter") commit(); });

    setTimeout(function(){ input.focus(); }, 200);

  }

 

  /* =====================================================

     BOOT

  ===================================================== */

  function boot(){

    if(!state.name || !state.started){

      beginOnboarding();

      return;

    }

    ensureTodayLogged();

    renderAll();

  }

 

  boot();

})();

</script>

</body>

</html>

 
