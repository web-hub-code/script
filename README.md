<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Quantum Infrastructure</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #030303; --card: rgba(255,255,255,0.04); --border: rgba(255,255,255,0.08); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.3s; font-family: 'Plus Jakarta Sans', sans-serif; outline: none; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; }

  /* HEADER & DRAWER */
  header { display: flex; align-items: center; padding: 60px 20px 10px; position: relative; justify-content: center; border-bottom: 1px solid var(--border); }
  .menu-btn { position: absolute; left: 20px; font-size: 24px; cursor: pointer; color: var(--neon); top: 62px; }
  .logo-text { font-size: 24px; font-weight: 800; letter-spacing: 8px; text-shadow: 0 0 15px var(--neon); cursor: pointer; }

  .drawer { position: fixed; top: 0; left: -100%; width: 280px; height: 100%; background: rgba(10,10,10,0.98); backdrop-filter: blur(20px); z-index: 50000; border-right: 1px solid var(--border); padding: 40px 20px; transition: 0.5s; }
  .drawer.open { left: 0; }
  .drawer-item { padding: 15px; border-radius: 15px; margin-bottom: 8px; background: var(--card); font-size: 11px; font-weight: 700; cursor: pointer; text-transform: uppercase; letter-spacing: 1px; }

  /* PAGES & UI */
  .page { max-width: 450px; margin: 0 auto; padding: 20px 20px 140px; display: none; }
  .active { display: block !important; animation: fadeIn 0.4s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

  .wallet-box { background: linear-gradient(135deg, #0a0a0a, #000); border: 1px solid var(--neon); padding: 30px; border-radius: 35px; text-align: center; margin-bottom: 20px; }
  .node-card { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 20px; margin-bottom: 15px; border-left: 4px solid var(--neon); }
  
  /* INPUTS & BUTTONS */
  input, select { width: 100%; padding: 16px; margin-top: 10px; border-radius: 18px; border: 1px solid var(--border); background: rgba(255,255,255,0.02); color: #fff; font-size: 13px; }
  .btn-action { width: 100%; padding: 18px; border-radius: 20px; border: none; font-weight: 800; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; margin-top: 15px; text-transform: uppercase; }

  /* TICKER */
  .ticker-wrap { background: rgba(0,247,255,0.05); padding: 8px 0; overflow: hidden; white-space: nowrap; position: fixed; top: 0; width: 100%; z-index: 10000; border-bottom: 1px solid var(--border); }
  .ticker { display: inline-block; animation: scroll 30s linear infinite; font-size: 10px; color: var(--neon); font-weight: 800; }
  @keyframes scroll { from { transform: translateX(100%); } to { transform: translateX(-100%); } }

  .nav { position: fixed; bottom: 25px; left: 15px; right: 15px; background: rgba(10,10,10,0.9); backdrop-filter: blur(20px); display: flex; justify-content: space-around; padding: 20px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 9px; opacity: 0.5; cursor: pointer; font-weight: 800; }
  .nav-item.active { opacity: 1; color: var(--neon); }
</style>
</head>
<body>

<div class="ticker-wrap"><div class="ticker">NETWORK STATUS: OPERATIONAL | WITHDRAWAL TIME: 1-2 HOURS | SECURE CLOUD MINING ACTIVE</div></div>

<div class="drawer" id="drawer">
    <div class="logo-text" style="font-size:16px; margin-bottom:40px; text-align:center;">NAVIGATION</div>
    <div class="drawer-item" onclick="tab('dash'); toggleMenu()">Dashboard</div>
    <div class="drawer-item" onclick="tab('teamPage'); toggleMenu()">Network Team</div>
    <div class="drawer-item" onclick="tab('promoPage'); toggleMenu()">Promo Code</div>
    <div class="drawer-item" onclick="tab('historyPage'); toggleMenu()">Activity Logs</div>
    <div class="drawer-item" style="margin-top:50px; color:var(--error);" onclick="logout()">Logout</div>
</div>

<header>
    <div class="menu-btn" onclick="toggleMenu()">☰</div>
    <div class="logo-text" id="adminTrigger">VERBOSE</div>
</header>

<div id="dash" class="page active">
    <div class="wallet-box">
        <span id="dispUser" style="font-size:10px; letter-spacing:2px; opacity:0.6;">IDENTIFYING...</span>
        <div style="font-size:35px; font-weight:800; margin-top:10px;">PKR <span id="uBal">0.00</span></div>
    </div>
    <div id="miningBox" style="background:rgba(112,0,255,0.1); border:1px dashed var(--accent); padding:15px; border-radius:20px; text-align:center;">
        <small style="font-size:9px; opacity:0.6;">NEXT REWARD IN</small>
        <div id="timer" style="font-size:24px; font-weight:800; color:var(--accent);">23:59:59</div>
    </div>
</div>

<div id="nodesPage" class="page">
    <h3 style="font-size:12px; letter-spacing:2px; margin-bottom:20px;">INVESTMENT NODES</h3>
    <div id="nodeGrid"></div>
</div>

<div id="finance" class="page">
    <div class="node-card" style="border-color:var(--success);">
        <h3>DEPOSIT</h3>
        <p style="font-size:11px;">JazzCash/SadaPay: <b>03705519562</b><br>EasyPaisa: <b>03379827882</b></p>
        <select id="dMethod">
            <option>JazzCash</option><option>EasyPaisa</option><option>SadaPay</option>
        </select>
        <input id="dAmt" type="number" placeholder="Amount">
        <input id="dTID" placeholder="Transaction ID (TID)">
        <button class="btn-action" onclick="submitDeposit()">Submit Transaction</button>
    </div>
</div>

<div id="withdrawPage" class="page">
    <div class="node-card" style="border-color:var(--error);">
        <h3>WITHDRAW</h3>
        <input id="wNum" type="number" placeholder="Account Number">
        <input id="wAmt" type="number" placeholder="Amount (Min 500)">
        <button class="btn-action" style="background:var(--error);" onclick="submitWithdraw()">Request Payout</button>
    </div>
</div>

<div id="promoPage" class="page">
    <div class="node-card" style="border-color:var(--gold); text-align:center;">
        <h3 style="color:var(--gold);">PROMO CODE</h3>
        <input id="pCode" placeholder="Enter Code" style="text-align:center;">
        <button class="btn-action" style="background:var(--gold); color:#000;" onclick="submitPromo()">Apply Code</button>
    </div>
</div>

<div id="teamPage" class="page">
    <h3 style="font-size:12px; letter-spacing:2px;">TEAM STRUCTURE</h3>
    <div style="display:grid; grid-template-columns:1fr 1fr; gap:10px; margin-top:20px;">
        <div class="node-card">Members<br><b id="tCount">0</b></div>
        <div class="node-card">Bonus<br><b id="tBonus">0.00</b></div>
    </div>
    <div class="node-card" id="refLink" style="font-size:10px; cursor:pointer; margin-top:20px;">Copy Referral Link</div>
</div>

<div id="adminPage" class="page">
    <h2 style="color:var(--gold); text-align:center;">ROOT CONTROL</h2>
    <div class="node-card" style="border-color:var(--gold);">
        <input id="tUser" placeholder="User ID">
        <input id="nBal" type="number" placeholder="Add Balance">
        <button class="btn-action" style="background:var(--gold); color:#000;" onclick="godUpdate()">Update Database</button>
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
  import { getDatabase, ref, update, onValue, push, get, set } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

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
  let currentBalance = 0;

  // --- NODES RENDER ---
  const nodes = [
    { name: "Server v1", price: 500, daily: 50, days: 30 },
    { name: "Server v2", price: 1000, daily: 110, days: 30 },
    { name: "Server v3", price: 2500, daily: 300, days: 30 },
    { name: "Server v4", price: 5000, daily: 650, days: 30 }
  ];
  const grid = document.getElementById('nodeGrid');
  nodes.forEach(n => {
    grid.innerHTML += `<div class="node-card"><b>${n.name}</b><br><small>Price: ${n.price} | Daily: ${n.daily}</small>
    <button class="btn-action" style="padding:10px; font-size:10px;" onclick="buyNode(${n.price}, ${n.daily})">Activate</button></div>`;
  });

  // --- LOGIC ---
  window.buyNode = async (p, d) => {
    if(currentBalance < p) return alert("Insufficient balance.");
    await update(ref(db, `users/${user}`), { balance: currentBalance - p, daily: d });
    alert("Node Activated.");
  };

  window.submitDeposit = () => push(ref(db, `admin/deposits`), { user, tid: document.getElementById('dTID').value, amount: document.getElementById('dAmt').value, status: "Pending" });
  window.submitWithdraw = () => push(ref(db, `admin/withdrawals`), { user, amount: document.getElementById('wAmt').value, account: document.getElementById('wNum').value, status: "Pending" });
  window.submitPromo = () => push(ref(db, `admin/promo_requests`), { user, code: document.getElementById('pCode').value });

  // --- ADMIN ---
  let clicks = 0;
  document.getElementById('adminTrigger').onclick = () => { if(++clicks >= 7) { if(prompt("Pass?")==="nazim786") tab('adminPage'); clicks=0; } };
  window.godUpdate = async () => {
    const target = document.getElementById('tUser').value;
    const val = Number(document.getElementById('nBal').value);
    const snap = await get(ref(db, `users/${target}`));
    if(snap.exists()) await update(ref(db, `users/${target}`), { balance: (snap.val().balance || 0) + val });
    alert("Database Synced.");
  };

  // --- UI CORE ---
  window.toggleMenu = () => document.getElementById('drawer').classList.toggle('open');
  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    if(el) { document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active')); el.classList.add('active'); }
  };

  if(user) {
    onValue(ref(db, `users/${user}`), s => {
        const d = s.val();
        currentBalance = d.balance || 0;
        document.getElementById('uBal').innerText = currentBalance.toLocaleString();
        document.getElementById('dispUser').innerText = "UID: " + user;
    });
  } else {
      let phone = prompt("Enter Phone Number to Start:");
      if(phone) { localStorage.setItem('v_user', phone); location.reload(); }
  }
</script>
</body>
</html>
