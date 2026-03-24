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
  header { display: flex; align-items: center; padding: 65px 20px 15px; position: relative; justify-content: center; border-bottom: 1px solid var(--border); }
  .menu-btn { position: absolute; left: 20px; font-size: 24px; cursor: pointer; color: var(--neon); top: 68px; }
  .logo-text { font-size: 24px; font-weight: 800; letter-spacing: 8px; text-shadow: 0 0 15px var(--neon); cursor: pointer; }

  .drawer { position: fixed; top: 0; left: -100%; width: 280px; height: 100%; background: rgba(10,10,10,0.98); backdrop-filter: blur(25px); z-index: 50000; border-right: 1px solid var(--border); padding: 40px 20px; transition: 0.5s cubic-bezier(0.4, 0, 0.2, 1); }
  .drawer.open { left: 0; }
  .drawer-overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.7); z-index: 45000; display: none; }
  .drawer-item { padding: 18px; border-radius: 15px; margin-bottom: 10px; background: var(--card); font-size: 11px; font-weight: 700; cursor: pointer; display: flex; align-items: center; gap: 15px; text-transform: uppercase; letter-spacing: 1px; }

  /* PAGES */
  .page { max-width: 450px; margin: 0 auto; padding: 20px 20px 140px; display: none; }
  .active { display: block !important; animation: fadeIn 0.4s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

  /* UI CARDS */
  .wallet-box { background: linear-gradient(135deg, #0a0a0a, #000); border: 1px solid var(--neon); padding: 35px; border-radius: 40px; text-align: center; margin-bottom: 25px; box-shadow: 0 15px 35px rgba(0,247,255,0.1); }
  .node-card { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 25px; margin-bottom: 18px; border-left: 4px solid var(--neon); position: relative; }
  
  /* INPUTS & BUTTONS */
  input, select { width: 100%; padding: 16px; margin-top: 10px; border-radius: 18px; border: 1px solid var(--border); background: rgba(255,255,255,0.02); color: #fff; font-size: 13px; }
  .btn-action { width: 100%; padding: 18px; border-radius: 20px; border: none; font-weight: 800; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; margin-top: 15px; text-transform: uppercase; letter-spacing: 1px; }
  .btn-action:disabled { opacity: 0.5; cursor: not-allowed; }

  /* TICKER */
  .ticker-wrap { background: rgba(0,247,255,0.05); padding: 10px 0; overflow: hidden; white-space: nowrap; position: fixed; top: 0; width: 100%; z-index: 10000; border-bottom: 1px solid var(--border); }
  .ticker { display: inline-block; animation: scroll 35s linear infinite; font-size: 10px; color: var(--neon); font-weight: 800; letter-spacing: 1px; }
  @keyframes scroll { from { transform: translateX(100%); } to { transform: translateX(-100%); } }

  /* NAVIGATION BAR */
  .nav { position: fixed; bottom: 25px; left: 15px; right: 15px; background: rgba(10,10,10,0.95); backdrop-filter: blur(20px); display: flex; justify-content: space-around; padding: 22px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 9px; opacity: 0.5; cursor: pointer; font-weight: 800; text-transform: uppercase; color: #fff; }
  .nav-item.active { opacity: 1; color: var(--neon); }
</style>
</head>
<body>

<div class="ticker-wrap">
    <div class="ticker">NETWORK STATUS: SECURE | WITHDRAWAL PROCESSING TIME: 1-3 HOURS | REFERRAL BONUS: 10% DIRECT | CLOUD NODES OPERATIONAL</div>
</div>

<div class="drawer-overlay" id="overlay" onclick="toggleMenu()"></div>
<div class="drawer" id="drawer">
    <div class="logo-text" style="font-size:16px; margin-bottom:40px; text-align:center;">MENU SYSTEM</div>
    <div class="drawer-item" onclick="tab('dash'); toggleMenu()">Dashboard</div>
    <div class="drawer-item" onclick="tab('teamPage'); toggleMenu()">Network Team</div>
    <div class="drawer-item" onclick="tab('promoPage'); toggleMenu()">Promo Code</div>
    <div class="drawer-item" onclick="tab('historyPage'); toggleMenu()">Activity Logs</div>
    <div class="drawer-item" style="margin-top:50px; color:var(--error);" onclick="logout()">Logout Session</div>
</div>

<header>
    <div class="menu-btn" onclick="toggleMenu()">☰</div>
    <div class="logo-text" id="adminTrigger">VERBOSE</div>
</header>

<div id="dash" class="page active">
    <div class="wallet-box">
        <span id="dispUser" style="font-size:10px; letter-spacing:2px; opacity:0.6;">INITIALIZING...</span>
        <div style="font-size:38px; font-weight:800; margin-top:10px;">PKR <span id="uBal">0.00</span></div>
    </div>
    <div style="background:rgba(112,0,255,0.08); border:1px dashed var(--accent); padding:20px; border-radius:25px; text-align:center;">
        <small style="font-size:9px; opacity:0.6; letter-spacing:1px;">PROFIT DISTRIBUTION TIMER</small>
        <div id="timer" style="font-size:26px; font-weight:800; color:var(--accent); font-variant-numeric: tabular-nums;">23:59:59</div>
    </div>
    <div style="display:grid; grid-template-columns: 1fr 1fr; gap:12px; margin-top:20px;">
        <div class="node-card" style="margin:0; text-align:center;"><small>Daily Yield</small><br><b id="uDaily">0.00</b></div>
        <div class="node-card" style="margin:0; text-align:center;"><small>Total Return</small><br><b id="uTotal">0.00</b></div>
    </div>
</div>

<div id="nodesPage" class="page">
    <h3 style="font-size:12px; letter-spacing:2px; margin-bottom:25px;">CLOUD MINING NODES</h3>
    <div id="nodeGrid"></div>
</div>

<div id="finance" class="page">
    <div class="node-card" style="border-color:var(--success);">
        <h3 style="margin-top:0;">DEPOSIT GATEWAY</h3>
        <p style="font-size:11px; line-height:1.6; opacity:0.8;">
            JazzCash / SadaPay: <b>03705519562</b><br>
            EasyPaisa: <b>03379827882</b>
        </p>
        <select id="dMethod">
            <option>JazzCash</option><option>EasyPaisa</option><option>SadaPay</option>
        </select>
        <input id="dAmt" type="number" placeholder="Enter Deposit Amount">
        <input id="dTID" placeholder="Transaction ID (TID)">
        <button class="btn-action" onclick="submitDeposit()">Submit Deposit Request</button>
    </div>
</div>

<div id="withdrawPage" class="page">
    <div class="node-card" style="border-color:var(--error);">
        <h3 style="margin-top:0;">PAYOUT REQUEST</h3>
        <input id="wName" readonly style="opacity:0.5; background:rgba(255,255,255,0.05);">
        <select id="wMethod">
            <option>JazzCash</option><option>EasyPaisa</option><option>SadaPay</option>
        </select>
        <input id="wNum" type="number" placeholder="Account Number">
        <input id="wAmt" type="number" placeholder="Amount (Minimum 500)">
        <button class="btn-action" style="background:var(--error);" onclick="submitWithdraw()">Process Payout</button>
    </div>
</div>

<div id="teamPage" class="page">
    <h3 style="font-size:12px; letter-spacing:2px;">NETWORK TEAM</h3>
    <div style="display:grid; grid-template-columns:1fr 1fr; gap:12px;">
        <div class="node-card">Direct Team<br><b id="tCount">0</b></div>
        <div class="node-card">Network Bonus<br><b id="tBonus">0.00</b></div>
    </div>
    <div class="node-card" id="refLink" onclick="copyRef()" style="font-size:10px; cursor:pointer; text-align:center; border-style:dashed; border-color:var(--accent);">
        Click to Copy Referral Link
    </div>
</div>

<div id="promoPage" class="page">
    <div class="node-card" style="border-color:var(--gold); text-align:center;">
        <h3 style="color:var(--gold); margin-top:0;">REDEEM PROMO CODE</h3>
        <input id="pCode" placeholder="Enter Promotional Code" style="text-align:center; border-color:var(--gold);">
        <button class="btn-action" style="background:var(--gold); color:#000;" onclick="submitPromo()">Apply Code</button>
    </div>
</div>

<div id="historyPage" class="page">
    <h3 style="font-size:12px; letter-spacing:2px;">ACTIVITY HISTORY</h3>
    <div id="histGrid"></div>
</div>

<div id="adminPage" class="page">
    <h2 style="color:var(--gold); text-align:center; letter-spacing:3px;">ROOT ACCESS PANEL</h2>
    <div class="node-card" style="border-color:var(--gold);">
        <small style="color:var(--gold);">DATABASE OVERWRITE</small>
        <input id="tUser" placeholder="User ID (Phone)">
        <input id="nBal" type="number" placeholder="Add/Sub Balance">
        <button class="btn-action" style="background:var(--gold); color:#000;" onclick="godUpdate()">Update User Data</button>
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

  // --- NODE INITIALIZATION ---
  const nodes = [
    { name: "Alpha Node", price: 500, daily: 55, days: 30 },
    { name: "Beta Pulse", price: 1000, daily: 120, days: 30 },
    { name: "Gamma Core", price: 2500, daily: 310, days: 30 },
    { name: "Delta Link", price: 5000, daily: 650, days: 30 },
    { name: "Omega Prime", price: 10000, daily: 1400, days: 30 }
  ];
  const grid = document.getElementById('nodeGrid');
  nodes.forEach(n => {
    grid.innerHTML += `<div class="node-card">
        <div style="display:flex; justify-content:space-between;"><b>${n.name}</b> <span>PKR ${n.price}</span></div>
        <div style="display:grid; grid-template-columns: 1fr 1fr; gap:10px; margin:15px 0; font-size:11px; opacity:0.7;">
            <div>Daily: PKR ${n.daily}</div><div>Period: ${n.days} Days</div>
        </div>
        <button class="btn-action" style="padding:12px; margin-top:5px; font-size:11px;" onclick="buyNode(${n.price}, ${n.daily}, '${n.name}')">Activate Node</button>
    </div>`;
  });

  // --- CORE LOGIC ---
  window.buyNode = async (p, d, name) => {
    if(currentBalance < p) return alert("Insufficient balance for this node.");
    const userRef = ref(db, `users/${user}`);
    await update(userRef, { balance: currentBalance - p, daily: d });
    push(ref(db, `users/${user}/history`), { type: "Node Purchase: " + name, amt: "-" + p, date: new Date().toLocaleDateString() });
    alert("Node activation successful.");
  };

  window.submitDeposit = () => {
    const tid = document.getElementById('dTID').value;
    const amt = document.getElementById('dAmt').value;
    if(!tid || !amt) return alert("All fields required.");
    push(ref(db, `admin/deposits`), { user, tid, amount: amt, method: document.getElementById('dMethod').value, status: "Pending", date: new Date().toLocaleString() });
    alert("Deposit request submitted.");
  };

  window.submitWithdraw = () => {
    const amt = document.getElementById('wAmt').value;
    if(amt < 500) return alert("Minimum withdrawal is PKR 500.");
    push(ref(db, `admin/withdrawals`), { user, amount: amt, account: document.getElementById('wNum').value, method: document.getElementById('wMethod').value, status: "Pending" });
    alert("Withdrawal request sent.");
  };

  window.submitPromo = () => {
    const code = document.getElementById('pCode').value;
    if(!code) return alert("Code required.");
    push(ref(db, `admin/promo_requests`), { user, code, status: "Pending" });
    alert("Promo request sent for verification.");
  };

  // --- TIMER ---
  setInterval(() => {
    let diff = new Date(new Date().setHours(24,0,0,0)) - new Date();
    let h = Math.floor(diff/3600000).toString().padStart(2,'0');
    let m = Math.floor((diff%3600000)/60000).toString().padStart(2,'0');
    let s = Math.floor((diff%60000)/1000).toString().padStart(2,'0');
    document.getElementById('timer').innerText = `${h}:${m}:${s}`;
  }, 1000);

  // --- ADMIN SYSTEM ---
  let cCount = 0;
  document.getElementById('adminTrigger').onclick = () => { if(++cCount >= 7) { if(prompt("Security Key?")==="nazim786") tab('adminPage'); cCount=0; } };
  window.godUpdate = async () => {
    const t = document.getElementById('tUser').value;
    const v = Number(document.getElementById('nBal').value);
    const snap = await get(ref(db, `users/${t}`));
    if(snap.exists()) await update(ref(db, `users/${t}`), { balance: (snap.val().balance || 0) + v });
    alert("Database updated.");
  };

  // --- UI CORE ---
  window.toggleMenu = () => {
    document.getElementById('drawer').classList.toggle('open');
    document.getElementById('overlay').style.display = document.getElementById('drawer').classList.contains('open') ? 'block' : 'none';
  };
  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    if(el) { document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active')); el.classList.add('active'); }
  };
  window.copyRef = () => { navigator.clipboard.writeText(`https://gtv140.github.io/?ref=${user}`); alert("Referral link copied."); };
  window.logout = () => { localStorage.clear(); location.reload(); };

  if(user) {
    onValue(ref(db, `users/${user}`), s => {
        const d = s.val();
        if(d) {
            currentBalance = d.balance || 0;
            document.getElementById('uBal').innerText = currentBalance.toLocaleString();
            document.getElementById('uDaily').innerText = (d.daily || 0).toLocaleString();
            document.getElementById('uTotal').innerText = (d.total || 0).toLocaleString();
            document.getElementById('dispUser').innerText = "ID: " + user + " | " + d.name.toUpperCase();
            document.getElementById('wName').value = "ACCOUNT: " + d.name.toUpperCase();
            document.getElementById('tCount').innerText = d.teamCount || 0;
            document.getElementById('tBonus').innerText = (d.teamBonus || 0).toLocaleString();
            
            const hGrid = document.getElementById('histGrid');
            hGrid.innerHTML = '';
            if(d.history) Object.values(d.history).reverse().forEach(h => {
                hGrid.innerHTML += `<div class="node-card" style="font-size:11px; padding:15px; border-left-color:var(--accent);">
                    <div style="display:flex; justify-content:space-between;"><b>${h.type}</b> <span>${h.amt}</span></div>
                    <small style="opacity:0.5;">${h.date}</small></div>`;
            });
        }
    });
  } else {
      let p = prompt("Enter Phone Number:");
      let n = prompt("Enter Name:");
      if(p && n) { set(ref(db, `users/${p}`), { name: n, balance: 0, daily: 0, total: 0, pass: "123" }); localStorage.setItem('v_user', p); location.reload(); }
  }
</script>
</body>
</html>
