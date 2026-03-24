<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Quantum Infrastructure</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #030303; --card: rgba(255,255,255,0.03); --border: rgba(255,255,255,0.08); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.3s; font-family: 'Plus Jakarta Sans', sans-serif; outline: none; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }

  /* AUTH & ADMIN MODAL */
  .overlay { position: fixed; inset: 0; background: var(--bg); z-index: 20000; padding: 20px; display: flex; flex-direction: column; justify-content: center; align-items: center; }
  .modal-card { width: 100%; max-width: 400px; background: var(--card); border: 1px solid var(--border); padding: 35px; border-radius: 40px; backdrop-filter: blur(30px); text-align: center; }
  
  /* UI COMPONENTS */
  header { text-align: center; padding: 45px 20px 10px; cursor: pointer; }
  .logo-text { font-size: 32px; font-weight: 800; letter-spacing: 12px; text-shadow: 0 0 25px var(--neon); color: #fff; }
  .page { max-width: 450px; margin: 0 auto; padding: 10px 20px 140px; display: none; }
  .active { display: block !important; animation: fadeIn 0.4s ease; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

  .stat-card { background: var(--card); border: 1px solid var(--border); padding: 18px; border-radius: 25px; margin-bottom: 12px; }
  .node-card { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 15px; display: flex; align-items: center; gap: 15px; margin-bottom: 12px; border-left: 4px solid var(--accent); }
  .node-icon { width: 50px; height: 50px; background: rgba(0,247,255,0.05); border: 1px solid var(--neon); border-radius: 15px; display: flex; align-items: center; justify-content: center; font-size: 22px; }

  /* INPUTS & BUTTONS */
  input { width: 100%; padding: 16px; margin-top: 10px; border-radius: 18px; border: 1px solid var(--border); background: rgba(255,255,255,0.02); color: #fff; font-size: 13px; }
  .btn-primary { width: 100%; padding: 16px; border-radius: 18px; border: none; font-weight: 800; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; margin-top: 15px; box-shadow: 0 5px 15px rgba(0,247,255,0.2); }
  
  /* NAVIGATION */
  .nav { position: fixed; bottom: 25px; left: 15px; right: 15px; background: rgba(10,10,10,0.95); backdrop-filter: blur(20px); display: none; justify-content: space-around; padding: 20px; border-radius: 35px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 8px; opacity: 0.4; font-weight: 800; cursor: pointer; color: #fff; text-transform: uppercase; }
  .nav-item.active { opacity: 1; color: var(--neon); }

  /* ADMIN DASHBOARD SPECIFIC */
  #adminPage { background: #000; z-index: 30000; display: none; padding-bottom: 50px; }
  .admin-ctrl { border: 1px solid var(--gold); padding: 15px; border-radius: 20px; margin-bottom: 15px; background: rgba(255,204,0,0.02); }
</style>
</head>
<body>

<div id="authPage" class="overlay">
    <div class="modal-card">
        <div class="logo-text" style="font-size:24px;">VERBOSE</div>
        <input id="authName" placeholder="Full Name">
        <input id="authPhone" type="number" placeholder="Mobile Number">
        <input id="authPass" type="password" placeholder="Password">
        <button class="btn-primary" onclick="handleAuth()">ACCESS CLOUD</button>
        <p style="font-size:10px; margin-top:15px; opacity:0.5;">By joining, you agree to our NYC Privacy Policy.</p>
    </div>
</div>

<div id="adminPanel" class="overlay" style="display:none; z-index:40000;">
    <div class="modal-card" style="border-color:var(--gold);">
        <h2 style="color:var(--gold); font-size:18px;">ROOT ACCESS</h2>
        <input id="adminKey" type="password" placeholder="Enter Admin Password">
        <button class="btn-primary" style="background:var(--gold); color:#000;" onclick="checkAdmin()">VERIFY ROOT</button>
        <button onclick="document.getElementById('adminPanel').style.display='none'" style="background:none; border:none; color:var(--error); margin-top:15px; font-size:10px;">CANCEL</button>
    </div>
</div>

<header id="adminTrigger">
    <div class="logo-text">VERBOSE</div>
</header>

<div id="dash" class="page">
    <div class="stat-card" style="background: linear-gradient(135deg, #0a0a0a, #000); border-color: var(--neon);">
        <small>Total Balance</small>
        <div style="font-size:30px;">PKR <span id="uBal">0.00</span></div>
        <p id="uWelcome" style="font-size:10px; opacity:0.5; margin-top:8px;"></p>
    </div>
    <div style="display:grid; grid-template-columns: 1fr 1fr; gap:10px;">
        <div class="stat-card"><small>Daily Yield</small><div id="uDaily">0.00</div></div>
        <div class="stat-card"><small>Total Mining</small><div id="uTotal">0.00</div></div>
    </div>
    <h3 style="font-size:11px; letter-spacing:2px; margin-top:20px;">ACTIVE CLOUD SERVERS</h3>
    <div id="nodeGrid"></div>
</div>

<div id="finance" class="page">
    <div class="stat-card">
        <h3>WALLET DEPOSIT</h3>
        <p style="font-size:10px; opacity:0.6;">03705519562 (JazzCash/SadaPay)</p>
        <input id="dAmt" type="number" placeholder="Amount">
        <input id="dTID" placeholder="TID Number">
        <button class="btn-primary" onclick="submitDeposit()">SUBMIT DEPOSIT</button>
    </div>
</div>

<div id="adminPage" class="page">
    <h2 style="color:var(--gold);">ADMIN CONTROL HUB</h2>
    <div class="admin-ctrl">
        <h4>User Management</h4>
        <input id="targetUser" placeholder="User Phone Number">
        <input id="newBal" type="number" placeholder="New Balance">
        <button class="btn-primary" style="background:var(--gold); color:#000;" onclick="updateUserBal()">UPDATE BALANCE</button>
    </div>
    <div id="pendingDeposits"></div>
    <button class="btn-primary" style="background:var(--error);" onclick="location.reload()">EXIT ADMIN MODE</button>
</div>

<nav class="nav" id="mainNav">
    <div class="nav-item active" onclick="tab('dash', this)">Home</div>
    <div class="nav-item" onclick="tab('finance', this)">Wallet</div>
    <div class="nav-item" onclick="tab('policy', this)">Policy</div>
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

  // --- NODE RENDERING ---
  const icons = ["📡", "🛰️", "🚀", "🧬", "💎", "⚡", "🌀"];
  const grid = document.getElementById('nodeGrid');
  for(let i=1; i<=25; i++) {
    grid.innerHTML += `
      <div class="node-card">
        <div class="node-icon">${icons[i % icons.length]}</div>
        <div class="node-info"><h4>Node Server v.${i}</h4><p>Cost: PKR ${500*i}</p></div>
        <button class="btn-primary" style="width:70px; font-size:9px; margin:0;" onclick="alert('Sent to Admin!')">BUY</button>
      </div>`;
  }

  // --- AUTH ---
  window.handleAuth = async () => {
    const p = document.getElementById('authPhone').value;
    const s = document.getElementById('authPass').value;
    const n = document.getElementById('authName').value;
    if(!p || !s) return alert("Fill all fields, sweetie!");

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

  // --- ADMIN SYSTEM ---
  let clicks = 0;
  document.getElementById('adminTrigger').onclick = () => {
    if(++clicks >= 7) { document.getElementById('adminPanel').style.display='flex'; clicks=0; }
  };

  window.checkAdmin = () => {
    if(document.getElementById('adminKey').value === "nazim786") {
        document.getElementById('adminPanel').style.display='none';
        tab('adminPage', null);
    } else alert("Access Denied!");
  };

  window.updateUserBal = () => {
    const p = document.getElementById('targetUser').value;
    const b = document.getElementById('newBal').value;
    update(ref(db, `users/${p}`), { balance: Number(b) });
    alert("Balance Synchronized!");
  };

  // --- UI ---
  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    if(el) {
        document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
        el.classList.add('active');
    }
  };

  window.logout = () => { localStorage.clear(); location.reload(); };

  if(user) {
    document.getElementById('authPage').style.display = 'none';
    document.getElementById('mainNav').style.display = 'flex';
    document.getElementById('dash').classList.add('active');
    onValue(ref(db, `users/${user}`), s => {
        const d = s.val();
        document.getElementById('uBal').innerText = d.balance.toLocaleString();
        document.getElementById('uWelcome').innerText = "Operator: " + d.name;
    });
  }
</script>
</body>
</html>
