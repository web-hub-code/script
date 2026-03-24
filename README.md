<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Enterprise Asset Management</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --dark: #020202; --glass: rgba(255,255,255,0.03); --border: rgba(255,255,255,0.08); }
  * { box-sizing: border-box; transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1); font-family: 'Inter', sans-serif; }
  body { margin:0; background: var(--dark); color: #fff; overflow-x: hidden; }
  
  header { text-align: center; padding: 40px 20px 10px; font-size: 22px; font-weight: 800; letter-spacing: 8px; color: #fff; text-transform: uppercase; text-shadow: 0 0 15px var(--neon); }
  .page { max-width: 450px; margin: 0 auto 100px; padding: 20px; min-height: 80vh; }
  
  .user-card { background: var(--glass); border: 1px solid var(--border); padding: 22px; border-radius: 28px; margin-bottom: 20px; backdrop-filter: blur(25px); border-left: 4px solid var(--neon); position: relative; }
  input, select { width: 100%; padding: 16px; margin-top: 12px; border-radius: 14px; border: 1px solid var(--border); background: rgba(0,0,0,0.7); color: #fff; font-size: 14px; outline: none; }
  button { width: 100%; padding: 16px; margin-top: 18px; border-radius: 16px; border: none; background: #fff; color: #000; font-weight: 800; cursor: pointer; text-transform: uppercase; font-size: 11px; letter-spacing: 1.5px; }
  .btn-neon { background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; }
  .btn-logout { background: rgba(255,70,70,0.1); color: #ff4646; border: 1px solid rgba(255,70,70,0.2); }

  .nav { position: fixed; bottom: 0; left: 0; right: 0; background: rgba(0,0,0,0.95); display: flex; justify-content: space-around; padding: 15px 5px 30px; z-index: 1000; border-top: 1px solid var(--border); backdrop-filter: blur(15px); }
  .nav-item { text-align: center; font-size: 9px; cursor: pointer; opacity: 0.4; color: #fff; font-weight: 700; text-transform: uppercase; flex: 1; }
  .nav-item.active { opacity: 1; color: var(--neon); }

  .hidden { display: none !important; }
  .alert-box { background: rgba(255,70,70,0.05); border: 1px solid rgba(255,70,70,0.2); padding: 15px; border-radius: 18px; margin-bottom: 20px; border-left: 4px solid #ff4646; font-size: 10px; line-height: 1.5; }

  #maintenanceScreen { position:fixed; top:0; left:0; width:100%; height:100%; background:var(--dark); z-index:9999; display:flex; flex-direction:column; justify-content:center; align-items:center; text-align:center; padding:30px; }
  #secretAuth { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.98); z-index: 10001; display: flex; flex-direction: column; justify-content: center; align-items: center; padding: 30px; }
</style>
</head>
<body>

<div id="maintenanceScreen" class="hidden">
  <h2 style="letter-spacing:4px; color:var(--neon);">SYSTEM OPTIMIZATION</h2>
  <p style="font-size:11px; opacity:0.6;">We are currently upgrading our security protocols. Please check back later.</p>
</div>

<header>VERBOSE</header>

<div id="loginPage" class="page">
  <div style="text-align:center; margin-bottom:40px;">
    <h3 id="adminTrigger" style="margin:0; font-weight:800; user-select:none;">Secure Portal Access</h3>
    <p style="font-size:10px; opacity:0.4; letter-spacing:1px; margin-top:5px;">ENTERPRISE ENCRYPTION ACTIVE</p>
  </div>
  <input id="u_name" placeholder="Username">
  <input id="u_pass" type="password" placeholder="Password">
  <button id="entryBtn" class="btn-neon">Authenticate Access</button>
</div>

<div id="secretAuth" class="hidden">
  <h3 style="color:var(--neon); letter-spacing:3px;">SYSTEM OVERRIDE</h3>
  <input id="adminKey" type="password" placeholder="Enter Master Key" style="max-width:300px;">
  <button onclick="verifyAdmin()" class="btn-neon" style="max-width:300px;">Unlock Console</button>
  <button onclick="document.getElementById('secretAuth').classList.add('hidden')" style="background:transparent; color:#fff; font-size:10px; margin-top:10px;">Exit Shell</button>
</div>

<div id="dashboard" class="page hidden">
  <div class="alert-box">
    <b style="color:#ff4646;">SECURITY ADVISORY:</b><br>
    Do not share personal verification data. Official administration never requests passwords.
  </div>
  <div class="user-card">
    <div style="font-size:10px; opacity:0.5; text-transform:uppercase;">Account Balance</div>
    <div style="font-size:36px; font-weight:800; margin:10px 0;">PKR <span id="mainBal">0.00</span></div>
    <div style="font-size:9px; color:var(--neon); font-weight:800;">VERIFIED & ACTIVE</div>
  </div>
  <button onclick="tab('plansPage')" class="btn-neon">Investment Portfolios</button>
  <button onclick="userLogout()" class="btn-logout">Terminate Session</button>
</div>

<div id="walletPage" class="page hidden">
  <h4 style="text-transform:uppercase; letter-spacing:1px;">Funding & Liquidation</h4>
  <div class="user-card" style="font-size:12px; border-left-color:var(--accent);">
    <b>Payment Hubs:</b><br>
    JazzCash: 03705519562<br>
    EasyPaisa: 03379827882
  </div>
  <input id="d_amount" type="number" placeholder="Deposit Amount">
  <input id="d_tid" placeholder="Transaction ID (TID)">
  <label style="font-size:10px; display:block; margin:15px 0 5px 5px; opacity:0.6;">Proof Screenshot:</label>
  <input type="file" id="proofFile" accept="image/*" style="font-size:10px; border:1px dashed var(--border); padding:10px;">
  <button onclick="handleDeposit()" class="btn-neon">Submit Audit</button>

  <hr style="opacity:0.1; margin:30px 0;">
  <p style="font-size:10px; opacity:0.5;">Min Withdrawal: 200 PKR</p>
  <input id="w_amount" type="number" placeholder="Withdrawal Amount">
  <button id="withdrawBtn" onclick="submitWithdraw()">Request Payout</button>
</div>

<div id="partnershipPage" class="page hidden">
  <h4 style="text-transform:uppercase;">Partnership Network</h4>
  <div class="user-card">
    <div style="font-size:10px; opacity:0.5;">INVITATION LINK</div>
    <button onclick="copyRefLink()" style="font-size:10px; padding:10px;">Copy Professional Link</button>
  </div>
  <div id="referralList"></div>
</div>

<div id="adminPage" class="page hidden" style="border: 2px solid var(--accent);">
  <h3 style="text-align:center; color:var(--neon);">EXECUTIVE CONSOLE</h3>
  <button onclick="toggleMaintenance()" id="maintBtn" style="background:orange;">Maintenance: ON/OFF</button>
  <button onclick="distributeGlobalProfit()" class="btn-neon">Distribute Daily Profits</button>
  
  <h5 style="margin-top:20px;">User Audit:</h5>
  <input id="modUser" placeholder="Username">
  <button onclick="inspectUser()" style="padding:10px; font-size:10px;">Inspect Account</button>
  <div id="modPanel" class="hidden user-card" style="margin-top:10px;">
    <input id="modNewBal" type="number" placeholder="New Balance">
    <button onclick="applyMod()" style="padding:10px;">Update Balance</button>
    <button onclick="toggleBan()" class="btn-logout" style="margin-top:5px;">Ban/Unban User</button>
  </div>

  <h5 style="margin-top:20px;">Financial Audit Queue:</h5>
  <div id="adminRequests"></div>
</div>

<div id="bottomNav" class="nav hidden">
  <div class="nav-item active" onclick="tab('dashboard', this)">Home</div>
  <div class="nav-item" onclick="tab('plansPage', this)">Plans</div>
  <div class="nav-item" onclick="tab('partnershipPage', this)">Partners</div>
  <div class="nav-item" onclick="tab('walletPage', this)">Wallet</div>
</div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, set, get, update, onValue, remove } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

  const firebaseConfig = {
    apiKey: "AIzaSyBe5Q5jXpx3UvrHC9WOky9UWeDnP9SPfZI",
    authDomain: "verbose-6c008.firebaseapp.com",
    projectId: "verbose-6c008",
    databaseURL: "https://verbose-6c008-default-rtdb.firebaseio.com",
    appId: "1:867100945312:web:315dfb48fb34496cee12c5"
  };
  const app = initializeApp(firebaseConfig);
  const db = getDatabase(app);
  const MASTER_KEY = "NAZIM786";

  // --- SESSION & MAINTENANCE ---
  window.onload = () => {
    const user = localStorage.getItem('v_user');
    if(user) sessionStart(user);
    checkMaintenance();
  };

  function sessionStart(u) {
    localStorage.setItem('v_user', u);
    document.getElementById('loginPage').classList.add('hidden');
    document.getElementById('dashboard').classList.remove('hidden');
    document.getElementById('bottomNav').classList.remove('hidden');
    onValue(ref(db, 'users/'+u), s => {
      if(s.exists()){
        const bal = parseFloat(s.val().balance);
        document.getElementById('mainBal').innerText = bal.toLocaleString();
        const wBtn = document.getElementById('withdrawBtn');
        wBtn.disabled = bal < 200;
        wBtn.style.opacity = bal < 200 ? 0.3 : 1;
      }
    });
  }

  window.userLogout = () => { if(confirm("Terminate session?")){ localStorage.clear(); location.reload(); } };

  // --- SECRET ADMIN TRIGGER ---
  let clicks = 0;
  document.getElementById('adminTrigger').onclick = () => {
    clicks++;
    if(clicks >= 7) { document.getElementById('secretAuth').classList.remove('hidden'); clicks = 0; }
    setTimeout(() => clicks = 0, 3000);
  };

  window.verifyAdmin = () => {
    if(document.getElementById('adminKey').value === MASTER_KEY) {
      document.getElementById('secretAuth').classList.add('hidden');
      tab('adminPage');
      loadAdminRequests();
    } else alert("Denied.");
  };

  // --- CORE SYSTEMS ---
  window.handleDeposit = async () => {
    const u = localStorage.getItem('v_user'), amt = document.getElementById('d_amount').value, tid = document.getElementById('d_tid').value, file = document.getElementById('proofFile').files[0];
    if(!amt || !tid || !file) return alert("Audit data incomplete.");
    const reader = new FileReader(); reader.readAsDataURL(file);
    reader.onload = async () => {
      await set(ref(db, 'requests/'+Date.now()), { user:u, amount:amt, tid:tid, proof:reader.result, type:'Deposit', status:'pending', time:new Date().toLocaleString() });
      alert("Sent for manual audit.");
    };
  };

  window.submitWithdraw = async () => {
    const u = localStorage.getItem('v_user'), amt = parseFloat(document.getElementById('w_amount').value);
    if(amt < 200) return alert("Min 200 PKR.");
    await set(ref(db, 'requests/'+Date.now()), { user:u, amount:amt, type:'Withdraw', status:'pending', time:new Date().toLocaleString() });
    alert("Withdrawal requested.");
  };

  // --- ADMIN FUNCTIONS ---
  function loadAdminRequests() {
    onValue(ref(db, 'requests'), snap => {
      const cont = document.getElementById('adminRequests'); cont.innerHTML = "";
      if(!snap.exists()) return cont.innerHTML = "Queue Empty.";
      Object.keys(snap.val()).forEach(id => {
        const r = snap.val()[id];
        cont.innerHTML += `<div class="user-card" style="font-size:10px;"><b>${r.user} | ${r.amount}</b><br><img src="${r.proof}" style="width:100%; border-radius:10px;"><br><button onclick="approveAudit('${id}','${r.user}',${r.amount},'${r.type}')" style="background:#00ff88;">Approve</button></div>`;
      });
    });
  }

  window.approveAudit = async (id, u, amt, type) => {
    const s = await get(ref(db, 'users/'+u));
    let nb = type === 'Deposit' ? parseFloat(s.val().balance) + amt : parseFloat(s.val().balance) - amt;
    await update(ref(db, 'users/'+u), { balance: nb });
    await remove(ref(db, 'requests/'+id));
    alert("Done.");
  };

  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.add('hidden'));
    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
    document.getElementById(id).classList.remove('hidden');
    if(el) el.classList.add('active');
  };

  function checkMaintenance() {
    onValue(ref(db, 'system_config/maintenance'), s => {
      if(s.val() && localStorage.getItem('v_user') !== 'admin') document.getElementById('maintenanceScreen').classList.remove('hidden');
      else document.getElementById('maintenanceScreen').classList.add('hidden');
    });
  }

  window.copyRefLink = () => {
    const link = `${window.location.origin}${window.location.pathname}?ref=${localStorage.getItem('v_user')}`;
    navigator.clipboard.writeText(link); alert("Link Copied.");
  };
</script>
</body>
</html>
