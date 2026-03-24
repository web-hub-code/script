<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Enterprise Infrastructure</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #030303; --card: rgba(255,255,255,0.05); --border: rgba(255,255,255,0.1); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1); font-family: 'Plus Jakarta Sans', sans-serif; outline: none; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }

  /* AUTH MODAL */
  #authOverlay { position: fixed; inset: 0; background: var(--bg); z-index: 100000; display: flex; align-items: center; justify-content: center; padding: 20px; }
  .auth-card { width: 100%; max-width: 400px; background: var(--card); border: 1px solid var(--border); border-radius: 40px; padding: 40px; backdrop-filter: blur(25px); text-align: center; box-shadow: 0 30px 60px rgba(0,0,0,0.8); }

  /* HEADER */
  header { display: flex; align-items: center; padding: 65px 20px 15px; position: relative; justify-content: center; border-bottom: 1px solid var(--border); }
  .logo-text { font-size: 24px; font-weight: 800; letter-spacing: 8px; text-shadow: 0 0 15px var(--neon); cursor: pointer; }
  .menu-btn { position: absolute; left: 20px; font-size: 24px; cursor: pointer; color: var(--neon); top: 68px; }

  /* NAVIGATION DRAWER */
  .drawer { position: fixed; top: 0; left: -100%; width: 280px; height: 100%; background: rgba(10,10,10,0.98); backdrop-filter: blur(30px); z-index: 50000; border-right: 1px solid var(--border); padding: 40px 20px; }
  .drawer.open { left: 0; }
  .drawer-item { padding: 18px; border-radius: 15px; margin-bottom: 10px; background: var(--card); font-size: 11px; font-weight: 700; cursor: pointer; text-transform: uppercase; letter-spacing: 1px; display: flex; align-items: center; gap: 15px; }

  /* PAGES */
  .page { max-width: 450px; margin: 0 auto; padding: 20px 20px 140px; display: none; }
  .active { display: block !important; animation: fadeIn 0.4s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

  /* UI ELEMENTS */
  .wallet-box { background: linear-gradient(135deg, #0a0a0a, #000); border: 1px solid var(--neon); padding: 35px; border-radius: 40px; text-align: center; margin-bottom: 25px; box-shadow: 0 10px 30px rgba(0,247,255,0.1); }
  .node-card { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 25px; margin-bottom: 15px; border-left: 4px solid var(--neon); position: relative; }
  
  /* PROGRESS & TIMER */
  .progress-container { background: rgba(255,255,255,0.05); height: 6px; border-radius: 10px; margin-top: 15px; overflow: hidden; }
  .progress-fill { height: 100%; background: var(--success); width: 0%; box-shadow: 0 0 10px var(--success); }

  /* INPUTS & BUTTONS */
  input, select { width: 100%; padding: 16px; margin-top: 10px; border-radius: 18px; border: 1px solid var(--border); background: rgba(255,255,255,0.02); color: #fff; font-size: 13px; }
  .btn-action { width: 100%; padding: 18px; border-radius: 20px; border: none; font-weight: 800; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; margin-top: 15px; text-transform: uppercase; letter-spacing: 1px; }
  .btn-action:disabled { background: #222; opacity: 0.4; cursor: not-allowed; }

  /* NAV BAR */
  .nav { position: fixed; bottom: 25px; left: 15px; right: 15px; background: rgba(10,10,10,0.95); backdrop-filter: blur(20px); display: flex; justify-content: space-around; padding: 22px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 9px; opacity: 0.5; cursor: pointer; font-weight: 800; text-transform: uppercase; color: #fff; }
  .nav-item.active { opacity: 1; color: var(--neon); }
</style>
</head>
<body>

<div id="authOverlay">
    <div class="auth-card">
        <div class="logo-text" style="font-size:18px; margin-bottom:25px;">VERBOSE ACCESS</div>
        <input id="authPhone" type="number" placeholder="Mobile Number">
        <input id="authPass" type="password" placeholder="Cloud Security PIN">
        <button class="btn-action" onclick="handleAuth()">SECURE LOGIN</button>
        <p style="font-size:9px; opacity:0.4; margin-top:15px; letter-spacing:1px;">AUTO-REGISTRATION ENABLED FOR NEW USERS</p>
    </div>
</div>

<header>
    <div class="menu-btn" onclick="toggleMenu()">☰</div>
    <div class="logo-text" id="adminTrigger">VERBOSE</div>
</header>

<div class="drawer" id="drawer">
    <div class="logo-text" style="font-size:16px; margin-bottom:40px; text-align:center;">MENU</div>
    <div class="drawer-item" onclick="tab('dash'); toggleMenu()">Dashboard</div>
    <div class="drawer-item" onclick="tab('finance'); toggleMenu()">Deposit Assets</div>
    <div class="drawer-item" onclick="tab('withdrawPage'); toggleMenu()">Payout Center</div>
    <div class="drawer-item" onclick="tab('promoPage'); toggleMenu()">Redeem Code</div>
    <div class="drawer-item" style="margin-top:50px; color:var(--error);" onclick="logout()">Terminate Session</div>
</div>

<div id="dash" class="page active">
    <div class="wallet-box">
        <span id="uIDDisplay" style="font-size:10px; opacity:0.6; letter-spacing:2px;">IDENTITY: ---</span>
        <div style="font-size:38px; font-weight:800; margin-top:10px;">PKR <span id="uBal">0.00</span></div>
    </div>

    <div id="activeBox" style="background:rgba(0,255,136,0.05); border:1px solid var(--success); padding:25px; border-radius:30px; display:none;">
        <div style="display:flex; justify-content:space-between; align-items:center;">
            <div>
                <small style="color:var(--success); font-weight:800;">ACTIVE NODE</small>
                <div id="actName" style="font-size:18px; font-weight:800;">NONE</div>
            </div>
            <div id="timer" style="font-size:22px; font-weight:800; color:var(--success); font-variant-numeric: tabular-nums;">24:00:00</div>
        </div>
        <div class="progress-container"><div id="pFill" class="progress-fill"></div></div>
    </div>
</div>

<div id="nodesPage" class="page">
    <h3 style="font-size:12px; letter-spacing:2px; margin-bottom:20px;">INVESTMENT INFRASTRUCTURE</h3>
    <div id="nodeGrid"></div>
</div>

<div id="finance" class="page">
    <div class="node-card" style="border-color:var(--success);">
        <h3 style="margin:0 0 10px;">DEPOSIT GATEWAY</h3>
        <p style="font-size:11px; opacity:0.7;">JazzCash/SadaPay: 03705519562<br>EasyPaisa: 03379827882</p>
        <input id="dAmt" type="number" placeholder="Enter Amount">
        <input id="dTID" placeholder="Transaction ID (TID)">
        <button class="btn-action" onclick="submitReq('Deposit')">Submit Assets</button>
    </div>
</div>

<div id="withdrawPage" class="page">
    <div class="node-card" style="border-color:var(--error);">
        <h3 style="margin:0 0 10px;">PAYOUT CENTER</h3>
        <input id="wNum" type="number" placeholder="Account Number">
        <input id="wAmt" type="number" placeholder="Amount (Min 500)">
        <button class="btn-action" style="background:var(--error);" onclick="submitReq('Withdraw')">Request Payout</button>
    </div>
</div>

<div id="promoPage" class="page">
    <div class="node-card" style="border-color:var(--gold);">
        <h3 style="margin:0 0 10px; color:var(--gold);">PROMO CODE</h3>
        <input id="pCode" placeholder="Enter Redeem Code" style="text-align:center;">
        <button class="btn-action" style="background:var(--gold); color:#000;" onclick="submitReq('Promo')">Claim Bonus</button>
    </div>
</div>

<div id="adminPage" class="page">
    <h2 style="color:var(--gold); text-align:center;">GOD MODE HUD</h2>
    <div id="adminLiveReqs"></div>
    <div class="node-card">
        <input id="admT" placeholder="User Phone">
        <input id="admV" type="number" placeholder="Add Amount">
        <button class="btn-action" onclick="godSync()">SYNC DATABASE</button>
    </div>
</div>

<nav class="nav">
    <div class="nav-item active" onclick="tab('dash', this)">Home</div>
    <div class="nav-item" onclick="tab('nodesPage', this)">Nodes</div>
    <div class="nav-item" onclick="tab('finance', this)">Deposit</div>
    <div class="nav-item" onclick="tab('withdrawPage', this)">Payout</div>
</nav>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, update, onValue, get, set, push } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

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

  const plans = [{n:"Starter Core", p:500, d:55}, {n:"Advanced Pulse", p:1000, d:125}, {n:"Enterprise Link", p:2500, d:320}, {n:"Quantum Node", p:5000, d:700}];

  // --- AUTH SYSTEM ---
  window.handleAuth = async () => {
    const p = document.getElementById('authPhone').value, s = document.getElementById('authPass').value;
    if(!p || !s) return alert("Required fields missing");
    const snap = await get(ref(db, `users/${p}`));
    if(snap.exists()) {
        if(snap.val().pass === s) { localStorage.setItem('v_user', p); location.reload(); }
        else alert("Incorrect Access PIN");
    } else {
        await set(ref(db, `users/${p}`), { name:"User", pass:s, balance:0, daily:0, hasActive:false });
        localStorage.setItem('v_user', p); location.reload();
    }
  };

  // --- ENGINE & RENDER ---
  const runEngine = (d) => {
    if(!d.hasActive) return document.getElementById('activeBox').style.display = 'none';
    document.getElementById('activeBox').style.display = 'block';
    document.getElementById('actName').innerText = d.activeName;

    const now = Date.now();
    const last = d.lastProfitTime || d.startTime;
    const next = last + 86400000;
    const diff = next - now;

    if(diff <= 0) {
        update(ref(db, `users/${user}`), { balance: (d.balance || 0) + d.daily, lastProfitTime: now });
    } else {
        let h = Math.floor(diff/3600000).toString().padStart(2,'0');
        let m = Math.floor((diff%3600000)/60000).toString().padStart(2,'0');
        let s = Math.floor((diff%60000)/1000).toString().padStart(2,'0');
        document.getElementById('timer').innerText = `${h}:${m}:${s}`;
        document.getElementById('pFill').style.width = `${((86400000 - diff)/86400000)*100}%`;
    }
  };

  const renderNodes = (hasActive) => {
    const grid = document.getElementById('nodeGrid'); grid.innerHTML = "";
    plans.forEach(x => {
        grid.innerHTML += `<div class="node-card"><b>${x.n}</b><br><small>Profit: PKR ${x.d}/day</small><br>
            <button class="btn-action" ${hasActive ? 'disabled' : ''} onclick="buyNode(${x.p}, ${x.d}, '${x.n}')">
                ${hasActive ? 'LIMIT REACHED' : 'ACTIVATE PKR ' + x.p}
            </button></div>`;
    });
  };

  window.buyNode = async (price, daily, name) => {
    const s = await get(ref(db, `users/${user}`));
    if(s.val().balance < price) return alert("Insufficient Balance");
    const t = Date.now();
    await update(ref(db, `users/${user}`), { balance: s.val().balance - price, daily, hasActive:true, activeName:name, startTime:t, lastProfitTime:t });
    alert("Node Initialized.");
  };

  // --- REQUESTS ---
  window.submitReq = (type) => {
    const amt = type === 'Promo' ? 0 : (document.getElementById(type === 'Deposit' ? 'dAmt' : 'wAmt').value);
    const detail = type === 'Deposit' ? document.getElementById('dTID').value : (type === 'Withdraw' ? document.getElementById('wNum').value : document.getElementById('pCode').value);
    push(ref(db, `admin/requests`), { user, type, amt, detail, status:"Pending", time: new Date().toLocaleString() });
    alert("Request Synchronized with Cloud.");
  };

  // --- ADMIN GOD MODE ---
  let c = 0;
  document.getElementById('adminTrigger').onclick = () => { if(++c >= 7) { if(prompt("God Key?")==="nazim786") { tab('adminPage'); loadAdminRequests(); } c=0; } };
  const loadAdminRequests = () => {
    onValue(ref(db, `admin/requests`), s => {
        const h = document.getElementById('adminLiveReqs'); h.innerHTML = "";
        if(s.exists()) Object.entries(s.val()).reverse().forEach(([k,v]) => {
            h.innerHTML += `<div class="node-card" style="font-size:10px; border-color:var(--gold);">
                <b>${v.type}</b> | ID: ${v.user}<br>AMT: ${v.amt} | VAL: ${v.detail}</div>`;
        });
    });
  };
  window.godSync = async () => {
    const t = document.getElementById('admT').value, v = Number(document.getElementById('admV').value);
    const s = await get(ref(db, `users/${t}`));
    if(s.exists()) await update(ref(db, `users/${t}`), { balance: (s.val().balance || 0) + v });
    alert("Database Updated.");
  };

  window.toggleMenu = () => document.getElementById('drawer').classList.toggle('open');
  window.tab = (id, el) => { document.querySelectorAll('.page').forEach(p => p.classList.remove('active')); document.getElementById(id).classList.add('active'); };
  window.logout = () => { localStorage.clear(); location.reload(); };

  if(user) {
    document.getElementById('authOverlay').style.display = 'none';
    onValue(ref(db, `users/${user}`), s => {
        const d = s.val();
        document.getElementById('uBal').innerText = (d.balance || 0).toLocaleString();
        document.getElementById('uIDDisplay').innerText = "IDENTITY: " + user;
        renderNodes(d.hasActive); runEngine(d);
    });
    setInterval(() => { get(ref(db, `users/${user}`)).then(s => runEngine(s.val())); }, 1000);
  }
</script>
</body>
</html>
