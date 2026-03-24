<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>VERBOSE — Prime Solutions</title>
<style>
  :root{ --neon:#00f7ff; --accent:#ff5cff; --dark:#070707; }
  *{box-sizing:border-box; transition: 0.3s;}
  body { margin:0; font-family:'Segoe UI', sans-serif; background:var(--dark); color:#fff; overflow-x:hidden; }
  header { text-align:center; padding:30px; font-size:32px; font-weight:900; background:linear-gradient(90deg,var(--neon),var(--accent)); -webkit-background-clip:text; -webkit-text-fill-color:transparent; cursor:pointer; text-transform:uppercase; letter-spacing:3px; }
  
  .page { max-width:420px; margin:20px auto; background:rgba(255,255,255,0.03); padding:25px; border-radius:15px; border:1px solid rgba(0,255,240,0.1); box-shadow: 0 10px 30px rgba(0,0,0,0.5); }
  input, select { width:100%; padding:14px; margin-top:12px; border-radius:10px; border:1px solid rgba(255,255,255,0.1); background:rgba(0,0,0,0.2); color:#fff; outline:none; }
  button { width:100%; padding:14px; margin-top:15px; border-radius:10px; border:none; background:linear-gradient(90deg,var(--neon),var(--accent)); color:#000; font-weight:800; cursor:pointer; font-size:16px; }
  
  .nav { position:fixed; bottom:0; left:0; right:0; background:rgba(15,17,20,0.95); display:flex; justify-content:space-around; padding:15px; border-top:1px solid rgba(0,255,240,0.1); backdrop-filter: blur(10px); z-index:1000; }
  .nav-item { text-align:center; font-size:12px; cursor:pointer; opacity:0.7; }
  .hidden { display:none; }
  
  .user-card { background:linear-gradient(135deg, rgba(0,247,255,0.1), rgba(255,92,255,0.05)); padding:20px; border-radius:15px; margin-bottom:15px; border-left:4px solid var(--neon); }
  .plan-card { background:rgba(255,255,255,0.02); padding:15px; border-radius:12px; margin:10px 0; display:flex; justify-content:space-between; align-items:center; border:1px solid rgba(255,255,255,0.05); }
</style>
</head>
<body>

<header id="mainHeader">VERBOSE</header>

<div id="loginPage" class="page">
  <h2 style="text-align:center;">Member Access</h2>
  <input id="u_name" type="text" placeholder="Username">
  <input id="u_pass" type="password" placeholder="Password">
  <button id="entryBtn">LOGIN / REGISTER</button>
</div>

<div id="dashboard" class="page hidden">
  <div class="user-card">
    <div id="welcomeMsg" style="font-size:18px; font-weight:bold;">Welcome!</div>
    <div style="margin-top:10px; font-size:28px; font-weight:900;">Rs <span id="mainBal">0.00</span></div>
    <div style="font-size:11px; color:var(--neon);">TOTAL BALANCE</div>
  </div>
  <div class="user-card" style="background:rgba(0,0,0,0.2); border:none;">
    <p style="font-size:11px; margin:0 0 5px 0;">Referral Link:</p>
    <input id="refUrl" readonly style="font-size:10px; padding:8px; background:#000;">
    <button onclick="copyLink()" style="padding:5px; font-size:12px; margin-top:8px;">Copy Link</button>
  </div>
</div>

<div id="plansPage" class="page hidden">
  <h3 style="color:var(--neon)">Investment Plans</h3>
  <div id="plansContainer"></div>
</div>

<div id="withdrawPage" class="page hidden">
  <h3>Withdrawal</h3>
  <div class="user-card">
    <select id="w_method">
      <option value="JazzCash">JazzCash</option>
      <option value="EasyPaisa">EasyPaisa</option>
    </select>
    <input id="w_amount" type="number" placeholder="Enter Amount">
    <input id="w_phone" type="text" placeholder="Phone Number">
    <button onclick="sendRequest('Withdraw')">Request Withdrawal</button>
  </div>
</div>

<div id="adminPage" class="page hidden" style="border: 2px dashed var(--accent);">
  <h2 style="text-align:center;">⚡ GOD MODE ⚡</h2>
  <input id="searchUser" placeholder="Username to Edit">
  <button id="findBtn">Search</button>
  <div id="editBox" class="hidden">
    <input id="setBal" type="number" placeholder="New Balance">
    <button id="saveBtn">Update Account</button>
  </div>
  <div id="requestsList" style="margin-top:20px; font-size:11px;"></div>
</div>

<div id="bottomNav" class="nav hidden">
  <div class="nav-item" onclick="changeTab('dashboard')">🏠<br>Home</div>
  <div class="nav-item" onclick="changeTab('plansPage')">📦<br>Plans</div>
  <div class="nav-item" onclick="changeTab('withdrawPage')">💰<br>Cashout</div>
  <div class="nav-item" onclick="doLogout()">🚪<br>Exit</div>
  <div id="adminNav" class="nav-item hidden" onclick="changeTab('adminPage')">⚡<br>God</div>
</div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, set, get, update, onValue } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

  const firebaseConfig = {
    apiKey: "AIzaSyCMG6KG_oD8cjEk4YpbxXik-C5q8K5MDHk",
    authDomain: "dark-web-9.firebaseapp.com",
    projectId: "dark-web-9",
    databaseURL: "https://dark-web-9-default-rtdb.firebaseio.com",
    appId: "1:564328425161:web:eb109ab77356dafe7f4f18"
  };

  const app = initializeApp(firebaseConfig);
  const db = getDatabase(app);

  // AUTH SYSTEM
  document.getElementById('entryBtn').onclick = async () => {
    const user = document.getElementById('u_name').value.trim().toLowerCase();
    const pass = document.getElementById('u_pass').value.trim();
    if(!user || !pass) return alert("Fill details!");

    const userRef = ref(db, 'users/' + user);
    const snap = await get(userRef);

    if(snap.exists()) {
      if(snap.val().password === pass) login(user, snap.val());
      else alert("Wrong password!");
    } else {
      const newData = { username:user, password:pass, balance:0, refCode: Math.random().toString(36).substring(7) };
      await set(userRef, newData);
      login(user, newData);
    }
  };

  function login(u, data) {
    localStorage.setItem('v_user', u);
    document.getElementById('welcomeMsg').innerText = "Hello, " + u;
    document.getElementById('mainBal').innerText = parseFloat(data.balance).toFixed(2);
    document.getElementById('refUrl').value = window.location.origin + window.location.pathname + "?ref=" + data.refCode;
    
    changeTab('dashboard');
    document.getElementById('loginPage').classList.add('hidden');
    document.getElementById('bottomNav').classList.remove('hidden');
    genPlans();
    listenAdmin();
  }

  function genPlans() {
    const cont = document.getElementById('plansContainer');
    cont.innerHTML = "";
    for(let i=1; i<=25; i++) {
      const cost = Math.round(200 + (i-1)*(30000-200)/24);
      cont.innerHTML += `<div class="plan-card">
        <div><b>Plan ${i}</b><br><small>Rs ${cost}</small></div>
        <button style="width:70px; margin:0; font-size:10px;" onclick="alert('Send Rs ${cost} to JazzCash: 03705519562')">BUY</button>
      </div>`;
    }
  }

  // ADMIN SYSTEM
  let taps = 0;
  document.getElementById('mainHeader').onclick = () => {
    taps++; if(taps === 7) {
      if(prompt("Admin Key:") === "prime786") {
        document.getElementById('adminNav').classList.remove('hidden');
        changeTab('adminPage');
      }
      taps = 0;
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
    await update(ref(db, 'users/' + u), { balance: parseFloat(document.getElementById('setBal').value) });
    alert("Updated!");
  };

  function listenAdmin() {
    onValue(ref(db, 'requests'), (snap) => {
      const list = document.getElementById('requestsList');
      list.innerHTML = "<h4>Withdrawal Requests</h4>";
      const data = snap.val();
      for(let id in data) {
        if(data[id].status === 'pending') {
          list.innerHTML += `<div>${data[id].user}: Rs ${data[id].amount} (${data[id].method}) <button onclick="appr('${id}')">OK</button></div>`;
        }
      }
    });
  }

  // UTILS
  window.changeTab = (id) => {
    document.querySelectorAll('.page').forEach(p => p.classList.add('hidden'));
    document.getElementById(id).classList.remove('hidden');
  };
  window.doLogout = () => { localStorage.clear(); location.reload(); };
  window.copyLink = () => { document.getElementById('refUrl').select(); document.execCommand('copy'); alert("Copied!"); };
  window.sendRequest = (type) => {
    const u = localStorage.getItem('v_user');
    const amt = document.getElementById('w_amount').value;
    const method = document.getElementById('w_method').value;
    set(ref(db, 'requests/' + Date.now()), { user:u, amount:amt, method:method, status:'pending' });
    alert("Request Sent!");
  };
</script>
</body>
</html>
