<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>VERBOSE — Prime Solutions</title>
<style>
  /* Base Styles from your original file */
  :root{ --neon:#00f7ff; --accent:#ff5cff; --dark:#070707; }
  *{box-sizing:border-box}
  body { margin:0; font-family:Inter, sans-serif; background:var(--dark); color:#fff; }
  header { text-align:center; padding:24px; font-size:28px; font-weight:800; background:linear-gradient(90deg,var(--neon),var(--accent)); -webkit-background-clip:text; -webkit-text-fill-color:transparent; cursor:pointer; }
  .page { max-width:430px; margin:18px auto; background:rgba(255,255,255,0.02); padding:18px; border-radius:12px; border:1px solid rgba(0,255,240,0.1); }
  input, button { width:100%; padding:12px; margin-top:10px; border-radius:8px; border:1px solid rgba(0,255,240,0.1); background:transparent; color:#fff; }
  button { background:linear-gradient(90deg,var(--neon),var(--accent)); border:none; color:#000; font-weight:700; cursor:pointer; }
  .nav { position:fixed; bottom:0; left:0; right:0; background:#0f1114; display:flex; justify-content:space-around; padding:12px; border-top:1px solid rgba(0,255,240,0.1); font-size:12px; }
  .hidden { display:none; }
  .user-box { background:rgba(0,255,240,0.05); padding:15px; border-radius:12px; margin-bottom:10px; }
  .plan-box { border:1px solid rgba(0,255,240,0.1); padding:12px; margin:10px 0; border-radius:10px; display:flex; justify-content:space-between; align-items:center; }
</style>
</head>
<body>

<header id="mainHeader">VERBOSE</header>

<div id="loginPage" class="page">
  <h2 style="text-align:center">Login / Signup</h2>
  <input id="user" placeholder="Username" />
  <input id="pass" placeholder="Password" type="password" />
  <button id="loginBtn">Access Portal</button>
</div>

<div id="dashboard" class="page hidden">
  <div class="user-box">
    <div id="dashUser" style="font-size:18px; font-weight:800;">Welcome</div>
    <div style="margin-top:5px;">Balance: Rs <span id="dashBalance">0</span></div>
  </div>
  <div class="user-box">
    <input id="refLink" readonly style="font-size:10px;">
    <button onclick="copyRef()">Copy Referral</button>
  </div>
</div>

<div id="plans" class="page hidden">
  <h3>Investment Plans</h3>
  <div id="plansList"></div>
</div>

<div id="godMode" class="page hidden" style="border: 2px dashed var(--neon);">
  <h2 style="text-align:center">⚡ GOD MODE ⚡</h2>
  <input id="adminSearch" placeholder="Username">
  <button id="fetchUser">Fetch User</button>
  <div id="adminEditor" class="hidden">
    <input id="newBal" type="number" placeholder="New Balance">
    <button id="updateUser">Update Balance</button>
  </div>
</div>

<div id="bottomNav" class="nav hidden">
  <div onclick="showPage('dashboard')">🏠 Home</div>
  <div onclick="showPage('plans')">📦 Plans</div>
  <div onclick="logout()">🚪 Logout</div>
</div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, set, get, update } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

  const firebaseConfig = {
    apiKey: "AIzaSyCMG6KG_oD8cjEk4YpbxXik-C5q8K5MDHk",
    authDomain: "dark-web-9.firebaseapp.com",
    projectId: "dark-web-9",
    databaseURL: "https://dark-web-9-default-rtdb.firebaseio.com", // Fixed URL
    storageBucket: "dark-web-9.appspot.com",
    appId: "1:564328425161:web:eb109ab77356dafe7f4f18"
  };

  const app = initializeApp(firebaseConfig);
  const db = getDatabase(app);

  // LOGIN LOGIC
  document.getElementById('loginBtn').onclick = async () => {
    const u = document.getElementById('user').value.trim();
    const p = document.getElementById('pass').value.trim();
    if(!u || !p) return alert("Fill fields!");

    const userRef = ref(db, 'users/' + u);
    const snap = await get(userRef);

    if(snap.exists()){
      if(snap.val().password === p) startApp(u, snap.val());
      else alert("Wrong password!");
    } else {
      const data = { username:u, password:p, balance:0, ref: Math.random().toString(36).substring(7) };
      await set(userRef, data);
      startApp(u, data);
    }
  };

  function startApp(u, data) {
    localStorage.setItem('v_user', u);
    document.getElementById('dashUser').innerText = u;
    document.getElementById('dashBalance').innerText = data.balance;
    document.getElementById('refLink').value = "https://gtv140.github.io/verbose/?ref=" + data.ref;
    
    document.getElementById('loginPage').classList.add('hidden');
    document.getElementById('dashboard').classList.remove('hidden');
    document.getElementById('bottomNav').classList.remove('hidden');
    renderPlans();
  }

  function renderPlans() {
    const list = document.getElementById('plansList');
    list.innerHTML = "";
    for(let i=1; i<=25; i++) {
      const invest = Math.round(200 + (i-1)*(30000-200)/24);
      list.innerHTML += `<div class="plan-box">
        <div>Plan ${i}<br><small>Invest: Rs ${invest}</small></div>
        <button style="width:70px" onclick="alert('Contact Admin')">Buy</button>
      </div>`;
    }
  }

  // GOD MODE TRIGGER (7 Clicks on Header)
  let c = 0;
  document.getElementById('mainHeader').onclick = () => {
    c++; if(c === 7) {
      if(prompt("Key:") === "prime786") showPage('godMode');
      c = 0;
    }
  };

  window.showPage = (id) => {
    document.querySelectorAll('.page').forEach(p => p.classList.add('hidden'));
    document.getElementById(id).classList.remove('hidden');
  };

  window.logout = () => { localStorage.clear(); location.reload(); };
</script>
</body>
</html>
