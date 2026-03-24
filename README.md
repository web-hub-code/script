<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Quantum Final</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #030303; --card: rgba(255,255,255,0.04); --border: rgba(255,255,255,0.08); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.3s; font-family: 'Plus Jakarta Sans', sans-serif; outline: none; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }

  /* TICKER & HEADER */
  .ticker-wrap { background: rgba(0,247,255,0.05); border-bottom: 1px solid var(--border); padding: 8px 0; overflow: hidden; white-space: nowrap; position: fixed; top: 0; width: 100%; z-index: 10000; }
  .ticker { display: inline-block; animation: scroll 25s linear infinite; font-size: 10px; font-weight: 800; color: var(--neon); letter-spacing: 1px; }
  @keyframes scroll { from { transform: translateX(100%); } to { transform: translateX(-100%); } }

  header { text-align: center; padding: 75px 20px 10px; cursor: pointer; }
  .logo-text { font-size: 28px; font-weight: 800; letter-spacing: 10px; text-shadow: 0 0 20px var(--neon); }
  
  .page { max-width: 450px; margin: 0 auto; padding: 10px 20px 140px; display: none; }
  .active { display: block !important; animation: fadeIn 0.4s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

  /* DASHBOARD BOXES */
  .wallet-box { background: linear-gradient(135deg, #0a0a0a, #000); border: 1px solid var(--neon); padding: 30px; border-radius: 35px; margin-bottom: 20px; text-align: center; }
  .timer-box { background: rgba(112,0,255,0.1); border: 1px dashed var(--accent); padding: 15px; border-radius: 20px; margin-bottom: 25px; text-align: center; }
  .timer-val { font-size: 24px; font-weight: 800; color: var(--accent); font-variant-numeric: tabular-nums; }

  /* HISTORY LIST */
  .hist-item { background: var(--card); border: 1px solid var(--border); padding: 15px; border-radius: 20px; margin-bottom: 10px; display: flex; justify-content: space-between; align-items: center; }
  .hist-info { font-size: 11px; }
  .hist-amt { font-weight: 800; font-size: 12px; }

  /* NODES & NAV */
  .node-item { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 18px; display: flex; align-items: center; gap: 15px; margin-bottom: 12px; border-left: 4px solid var(--accent); }
  .btn-action { width: 100%; padding: 18px; border-radius: 20px; border: none; font-weight: 800; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; margin-top: 15px; }
  input { width: 100%; padding: 16px; margin-top: 10px; border-radius: 18px; border: 1px solid var(--border); background: rgba(255,255,255,0.02); color: #fff; }

  .nav { position: fixed; bottom: 25px; left: 15px; right: 15px; background: rgba(10,10,10,0.95); backdrop-filter: blur(25px); display: none; justify-content: space-around; padding: 22px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 8px; opacity: 0.4; font-weight: 800; cursor: pointer; color: #fff; text-transform: uppercase; }
  .nav-item.active { opacity: 1; color: var(--neon); }
</style>
</head>
<body>

<div class="ticker-wrap"><div class="ticker">💎 VERBOSE v22.0 LIVE... 🚀 MINING SERVERS OPTIMIZED... ✅ INSTANT WITHDRAWALS ENABLED...</div></div>

<div id="authPage" style="position:fixed; inset:0; background:var(--bg); z-index:30000; padding:20px; display:flex; flex-direction:column; justify-content:center; align-items:center;">
    <div style="width:100%; max-width:400px; background:var(--card); padding:40px; border-radius:40px; border:1px solid var(--border); text-align:center;">
        <div class="logo-text" style="font-size:24px;">VERBOSE</div>
        <input id="authName" placeholder="Full Name">
        <input id="authPhone" type="number" placeholder="Mobile Node ID">
        <input id="authPass" type="password" placeholder="Cloud Key">
        <button class="btn-action" onclick="handleAuth()">LOGIN SYSTEM</button>
    </div>
</div>

<header id="adminTrigger"><div class="logo-text">VERBOSE</div></header>

<div id="dash" class="page">
    <div class="wallet-box">
        <span style="font-size:10px; color:var(--neon); letter-spacing:2px;" id="dispUser">OPERATOR</span>
        <div style="font-size:38px; font-weight:800; margin-top:10px;">PKR <span id="uBal">0.00</span></div>
    </div>
    <div class="timer-box">
        <small style="font-size:9px; opacity:0.6; text-transform:uppercase;">Next Profit Distribution</small>
        <div class="timer-val" id="miningTimer">23:59:59</div>
    </div>
    <div style="display:grid; grid-template-columns:1fr 1fr; gap:10px;">
        <div class="wallet-box" style="padding:15px;"><small>Daily Yield</small><div id="uDaily">0.00</div></div>
        <div class="wallet-box" style="padding:15px;"><small>Total Profit</small><div id="uTotal">0.00</div></div>
    </div>
</div>

<div id="nodesPage" class="page">
    <h3 style="font-size:12px; letter-spacing:2px; margin-bottom:20px;">MINING SERVERS</h3>
    <div id="nodeGrid"></div>
</div>

<div id="historyPage" class="page">
    <h3 style="font-size:12px; letter-spacing:2px; margin-bottom:20px;">ACTIVITY LOGS</h3>
    <div id="histGrid">
        <div class="hist-item">
            <div class="hist-info"><b>System Init</b><br><small>2026-03-24</small></div>
            <div class="hist-amt" style="color:var(--success);">Active</div>
        </div>
    </div>
</div>

<div id="adminPage" class="page">
    <h2 style="color:var(--gold);">GOD MODE HUD</h2>
    <div class="wallet-box" style="border-color:var(--gold);">
        <input id="tUser" placeholder="User ID">
        <input id="nBal" type="number" placeholder="New Balance">
        <button class="btn-action" style="background:var(--gold); color:#000;" onclick="godSync()">OVERWRITE DATA</button>
    </div>
</div>

<nav class="nav" id="mainNav">
    <div class="nav-item active" onclick="tab('dash', this)">Home</div>
    <div class="nav-item" onclick="tab('nodesPage', this)">Nodes</div>
    <div class="nav-item" onclick="tab('historyPage', this)">History</div>
    <div class="nav-item" onclick="logout()" style="color:var(--error);">Exit</div>
</nav>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, set, update, onValue, get, push } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

  const firebaseConfig = {
    apiKey: "AIzaSyBe5Q5jXpx3UvrHC9WOky9UWeDnP9SPfZI",
    authDomain: "verbose-6c008.firebaseapp.com",
    projectId: "verbose-6c008",
    databaseURL: "https://verbose-6c008-default-rtdb.firebaseio.com",
    appId: "1:867100945312:web:315dfb48fb34496cee12c5"
  };

  const app = initializeApp(firebaseConfig);
  const db = getDatabase(app);
  let user = localStorage.getItem('v_user');

  // --- TIMER LOGIC ---
  function startTimer() {
    setInterval(() => {
        let now = new Date();
        let night = new Date(now.getFullYear(), now.getMonth(), now.getDate() + 1, 0, 0, 0);
        let diff = night - now;
        let h = Math.floor(diff / 3600000).toString().padStart(2, '0');
        let m = Math.floor((diff % 3600000) / 60000).toString().padStart(2, '0');
        let s = Math.floor((diff % 60000) / 1000).toString().padStart(2, '0');
        document.getElementById('miningTimer').innerText = `${h}:${m}:${s}`;
    }, 1000);
  }

  // --- RENDER NODES ---
  const grid = document.getElementById('nodeGrid');
  for(let i=1; i<=25; i++) {
    grid.innerHTML += `<div class="node-item"><div><h4>Server v.${i}</h4><small>Yield ${50*i}/D</small></div><button class="btn-action" style="width:70px; margin:0; font-size:10px;" onclick="addHistory('Buy Node', ${500*i})">BUY</button></div>`;
  }

  window.addHistory = (type, amt) => {
    if(!user) return;
    push(ref(db, `users/${user}/history`), { type, amt, date: new Date().toLocaleDateString() });
    alert("Request Sent, Sweetie!");
  };

  // --- AUTH ---
  window.handleAuth = async () => {
    const p = document.getElementById('authPhone').value, s = document.getElementById('authPass').value, n = document.getElementById('authName').value;
    if(!p || !s) return alert("Missing data!");
    const r = ref(db, `users/${p}`);
    const snap = await get(r);
    if(snap.exists()) {
        if(snap.val().pass === s) { localStorage.setItem('v_user', p); location.reload(); }
        else alert("Wrong Key!");
    } else {
        await set(r, { name: n, pass: s, balance: 0, daily: 0, total: 0 });
        localStorage.setItem('v_user', p); location.reload();
    }
  };

  // --- ADMIN ---
  let clicks = 0;
  document.getElementById('adminTrigger').onclick = () => { if(++clicks >= 7) { let k = prompt("Master Key?"); if(k==="nazim786") tab('adminPage', null); clicks=0; } };
  window.godSync = () => {
    update(ref(db, `users/${document.getElementById('tUser').value}`), { balance: Number(document.getElementById('nBal').value) });
    alert("God-Mode Sync Complete!");
  };

  // --- UI ---
  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    if(el) { document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active')); el.classList.add('active'); }
  };
  window.logout = () => { localStorage.clear(); location.reload(); };

  if(user) {
    document.getElementById('authPage').style.display = 'none';
    document.getElementById('mainNav').style.display = 'flex';
    document.getElementById('dash').classList.add('active');
    startTimer();
    onValue(ref(db, `users/${user}`), s => {
        const d = s.val();
        document.getElementById('uBal').innerText = d.balance.toLocaleString();
        document.getElementById('uDaily').innerText = d.daily.toLocaleString();
        document.getElementById('uTotal').innerText = d.total.toLocaleString();
        document.getElementById('dispUser').innerText = "OPERATOR: " + d.name.toUpperCase();
        
        const hGrid = document.getElementById('histGrid');
        hGrid.innerHTML = '';
        if(d.history) {
            Object.values(d.history).reverse().forEach(h => {
                hGrid.innerHTML += `<div class="hist-item"><div class="hist-info"><b>${h.type}</b><br><small>${h.date}</small></div><div class="hist-amt">PKR ${h.amt}</div></div>`;
            });
        }
    });
  }
</script>
</body>
</html>
