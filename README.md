<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>VERBOSE — Trusted Assets</title>
<style>
  :root{ --neon:#00f7ff; --accent:#ff5cff; --dark:#070707; --glass:rgba(255,255,255,0.03); }
  *{box-sizing:border-box; transition: 0.3s; -webkit-tap-highlight-color: transparent;}
  body { margin:0; font-family:'Segoe UI', Roboto, sans-serif; background:var(--dark); color:#fff; overflow-x:hidden; }
  
  /* Modern Header */
  header { text-align:center; padding:35px 20px; font-size:35px; font-weight:900; background:linear-gradient(90deg,var(--neon),var(--accent)); -webkit-background-clip:text; -webkit-text-fill-color:transparent; cursor:pointer; text-transform:uppercase; letter-spacing:5px; filter: drop-shadow(0 0 10px rgba(0,247,255,0.3)); }

  /* Glassmorphism Containers */
  .page { max-width:420px; margin:15px auto 100px; background:var(--glass); padding:25px; border-radius:20px; border:1px solid rgba(0,255,240,0.1); backdrop-filter: blur(15px); }
  .user-card { background:linear-gradient(135deg, rgba(0,247,255,0.1), rgba(255,92,255,0.05)); padding:20px; border-radius:18px; margin-bottom:15px; border-left:5px solid var(--neon); box-shadow: 0 10px 20px rgba(0,0,0,0.3); }
  
  /* Form Elements */
  input, select { width:100%; padding:15px; margin-top:12px; border-radius:12px; border:1px solid rgba(255,255,255,0.08); background:rgba(0,0,0,0.4); color:#fff; font-size:15px; }
  button { width:100%; padding:15px; margin-top:18px; border-radius:12px; border:none; background:linear-gradient(90deg,var(--neon),var(--accent)); color:#000; font-weight:800; cursor:pointer; font-size:16px; box-shadow: 0 4px 15px rgba(0,247,255,0.2); }
  button:active { transform: scale(0.96); }

  /* Navigation Bar */
  .nav { position:fixed; bottom:0; left:0; right:0; background:rgba(10,10,12,0.98); display:flex; justify-content:space-around; padding:18px; border-top:1px solid rgba(0,255,240,0.15); backdrop-filter: blur(20px); z-index:1000; }
  .nav-item { text-align:center; font-size:11px; cursor:pointer; opacity:0.6; color:#fff; text-decoration:none; flex:1; }
  .nav-item.active { opacity:1; color:var(--neon); font-weight:bold; }
  
  /* Status Badges */
  .status { font-size:10px; padding:3px 8px; border-radius:20px; text-transform:uppercase; font-weight:bold; }
  .status-pending { background:#ffaa00; color:#000; }
  .status-success { background:#00ff88; color:#000; }
  
  .hidden { display:none; }
  .plan-card { background:rgba(255,255,255,0.02); padding:15px; border-radius:15px; margin:10px 0; display:flex; justify-content:space-between; align-items:center; border:1px solid rgba(255,255,255,0.05); }
</style>
</head>
<body>

<header id="mainHeader">VERBOSE</header>

<div id="loginPage" class="page">
  <h2 style="text-align:center; margin-bottom:5px;">Welcome</h2>
  <p style="text-align:center; font-size:12px; color:rgba(255,255,255,0.5); margin-bottom:20px;">Prime Solutions Secured Network</p>
  <input id="u_name" type="text" placeholder="Username" autocomplete="off">
  <input id="u_pass" type="password" placeholder="Password">
  <button id="entryBtn">SIGN IN / JOIN NOW</button>
</div>

<div id="dashboard" class="page hidden">
  <div class="user-card">
    <div id="welcomeMsg" style="font-size:16px; opacity:0.8;">Hello, User</div>
    <div style="margin-top:12px; font-size:32px; font-weight:900;">Rs <span id="mainBal">0.00</span></div>
    <div style="font-size:12px; color:var(--neon); letter-spacing:1px;">TOTAL AVAILABLE BALANCE</div>
  </div>

  <div style="display:grid; grid-template-columns: 1fr 1fr; gap:10px; margin-bottom:15px;">
    <div class="user-card" style="margin:0; padding:15px; border-left:3px solid var(--accent);">
      <div style="font-size:10px; opacity:0.7;">Daily Profit</div>
      <div style="font-size:18px; font-weight:bold;">Rs <span id="dailyEarn">0.00</span></div>
    </div>
    <div class="user-card" style="margin:0; padding:15px; border-left:3px solid #fff;">
      <div style="font-size:10px; opacity:0.7;">Active Plans</div>
      <div id="activePlansCount" style="font-size:18px; font-weight:bold;">0</div>
    </div>
  </div>

  <div class="user-card" style="background:rgba(0,0,0,0.3); border:none;">
    <p style="font-size:11px; margin:0 0 8px 0;">Referral Link (10% Bonus):</p>
    <div style="display:flex; gap:5px;">
      <input id="refUrl" readonly style="margin:0; padding:10px; font-size:10px; flex:3;">
      <button onclick="copyLink()" style="margin:0; padding:10px; flex:1; font-size:10px;">COPY</button>
    </div>
  </div>
</div>

<div id="plansPage" class="page hidden">
  <h3 style="color:var(--neon); margin-top:0;">Premium Assets</h3>
  <div id="plansContainer"></div>
</div>

<div id="walletPage" class="page hidden">
  <h3>Financial Center</h3>
  <div class="user-card" style="background:rgba(0,255,240,0.05);">
    <p style="font-size:12px; margin-bottom:10px;"><b>Deposit via JazzCash/EasyPaisa:</b><br>Number: 03705519562<br>Name: Muhammad Nazim</p>
    <input id="d_amount" type="number" placeholder="Deposit Amount">
    <input id="d_tid" placeholder="Transaction ID (TID)">
    <button onclick="handleFinance('Deposit')" style="background:var(--neon)">SUBMIT DEPOSIT</button>
  </div>
  
  <div class="user-card" style="margin-top:20px;">
    <p style="font-size:12px;"><b>Withdraw Profit:</b></p>
    <select id="w_method"><option>JazzCash</option><option>EasyPaisa</option></select>
    <input id="w_amount" type="number" placeholder="Withdraw Amount">
    <input id="w_phone" placeholder="Phone Number">
    <button onclick="handleFinance('Withdraw')" style="background:var(--accent)">REQUEST WITHDRAW</button>
  </div>
</div>

<div id="adminPage" class="page hidden" style="border: 2px dashed var(--accent);">
  <h2 style="text-align:center; color:var(--accent);">⚡ GOD MODE ⚡</h2>
  <input id="searchUser" placeholder="Username">
  <button id="findBtn">Search User</button>
  <div id="editBox" class="hidden">
    <input id="setBal" type="number" placeholder="Set Balance">
    <button id="saveBtn">Update</button>
  </div>
  <div id="adminLogs" style="margin-top:20px; max-height:300px; overflow-y:auto;"></div>
</div>

<div id="bottomNav" class="nav hidden">
  <div class="nav-item active" onclick="tab('dashboard', this)">🏠<br>Home</div>
  <div class="nav-item" onclick="tab('plansPage', this)">📦<br>Plans</div>
  <div class="nav-item" onclick="tab('walletPage', this)">💰<br>Wallet</div>
  <div class="nav-item" onclick="doLogout()">🚪<br>Logout</div>
  <div id="adminNav" class="nav-item hidden" onclick="tab('adminPage', this)">⚡<br>God</div>
</div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, set, get, update, onValue } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

  const firebaseConfig = {
    apiKey: "AIzaSyBe5Q5jXpx3UvrHC9WOky9UWeDnP9SPfZI",
    authDomain: "verbose-6c008.firebaseapp.com",
    projectId: "verbose-6c008",
    databaseURL: "https://verbose-6c008-default-rtdb.firebaseio.com",
    appId: "1:867100945312:web:315dfb48fb34496cee12c5"
  };

  const app = initializeApp(firebaseConfig);
  const db = getDatabase(app);

  // --- LOGIN LOGIC ---
  document.getElementById('entryBtn').onclick = async () => {
    const user = document.getElementById('u_name').value.trim().toLowerCase();
    const pass = document.getElementById('u_pass').value.trim();
    if(!user || !pass) return alert("Puri details daalein!");

    const userRef = ref(db, 'users/' + user);
    const snap = await get(userRef);

    if(snap.exists()) {
      if(snap.val().password === pass) setupUser(user, snap.val());
      else alert("Wrong password!");
    } else {
      const data = { username:user, password:pass, balance:0, dailyProfit:0, plans:0, refCode: Math.random().toString(36).substring(7) };
      await set(userRef, data);
      setupUser(user, data);
    }
  };

  function setupUser(u, data) {
    localStorage.setItem('v_user', u);
    document.getElementById('welcomeMsg').innerText = "Hello, " + u;
    document.getElementById('mainBal').innerText = parseFloat(data.balance).toFixed(2);
    document.getElementById('dailyEarn').innerText = parseFloat(data.dailyProfit || 0).toFixed(2);
    document.getElementById('activePlansCount').innerText = data.plans || 0;
    document.getElementById('refUrl').value = window.location.origin + window.location.pathname + "?ref=" + data.refCode;
    
    document.getElementById('loginPage').classList.add('hidden');
    document.getElementById('dashboard').classList.remove('hidden');
    document.getElementById('bottomNav').classList.remove('hidden');
    renderPlans();
    syncData(u);
  }

  function syncData(u) {
    onValue(ref(db, 'users/' + u), (snap) => {
      const d = snap.val();
      document.getElementById('mainBal').innerText = parseFloat(d.balance).toFixed(2);
    });
  }

  function renderPlans() {
    const cont = document.getElementById('plansContainer');
    cont.innerHTML = "";
    for(let i=1; i<=25; i++) {
      const cost = Math.round(200 + (i-1)*(30000-200)/24);
      cont.innerHTML += `<div class="plan-card">
        <div><b>Plan ${i}</b><br><small>Invest: Rs ${cost}</small></div>
        <button style="width:70px; margin:0; font-size:10px;" onclick="tab('walletPage')">BUY</button>
      </div>`;
    }
  }

  // --- FINANCE ---
  window.handleFinance = (type) => {
    const u = localStorage.getItem('v_user');
    const amt = (type === 'Deposit') ? document.getElementById('d_amount').value : document.getElementById('w_amount').value;
    const info = (type === 'Deposit') ? document.getElementById('d_tid').value : document.getElementById('w_phone').value;
    
    if(!amt || !info) return alert("Details incomplete!");
    
    const key = Date.now();
    set(ref(db, 'transactions/' + key), {
      user: u, amount: amt, info: info, type: type, status: 'pending', time: new Date().toLocaleString()
    });
    alert(type + " request sent! Admin verify karega.");
  };

  // --- ADMIN GOD MODE ---
  let tap = 0;
  document.getElementById('mainHeader').onclick = () => {
    tap++; if(tap === 7) {
      if(prompt("Admin Secret:") === "prime786") {
        document.getElementById('adminNav').classList.remove('hidden');
        tab('adminPage');
      }
      tap = 0;
    }
  };

  document.getElementById('findBtn').onclick = async () => {
    const u = document.getElementById('searchUser').value.trim().toLowerCase();
    const s = await get(ref(db, 'users/' + u));
    if(s.exists()) {
      document.getElementById('setBal').value = s.val().balance;
      document.getElementById('editBox').classList.remove('hidden');
    }
  };

  document.getElementById('saveBtn').onclick = async () => {
    const u = document.getElementById('searchUser').value.trim().toLowerCase();
    const nb = parseFloat(document.getElementById('setBal').value);
    await update(ref(db, 'users/' + u), { balance: nb });
    alert("Updated!");
  };

  onValue(ref(db, 'transactions'), (snap) => {
    const logs = document.getElementById('adminLogs');
    logs.innerHTML = "<h4>Live Transactions</h4>";
    const data = snap.val();
    for(let id in data) {
      if(data[id].status === 'pending') {
        logs.innerHTML += `<div class="plan-card" style="font-size:11px;">
          <div>${data[id].user}<br>${data[id].type}: Rs ${data[id].amount}</div>
          <button style="width:60px; font-size:9px;" onclick="alert('Open Firebase to Approve')">Review</button>
        </div>`;
      }
    }
  });

  // --- HELPERS ---
  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.add('hidden'));
    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
    document.getElementById(id).classList.remove('hidden');
    if(el) el.classList.add('active');
  };
  window.doLogout = () => { localStorage.clear(); location.reload(); };
  window.copyLink = () => { document.getElementById('refUrl').select(); document.execCommand('copy'); alert("Copied!"); };
</script>
</body>
</html>
