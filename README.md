<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>VERBOSE - Professional Portal</title>
<style>
  :root{ --neon:#00f7ff; --accent:#ff5cff; --dark:#070707; --panel:#0f1114; }
  *{box-sizing:border-box}
  body { margin:0; font-family:Inter, Arial, sans-serif; background:var(--dark); color:#fff; overflow-x:hidden; -webkit-font-smoothing:antialiased; }
  header { text-align:center; padding:24px 12px; font-size:28px; font-weight:800; letter-spacing:2px; background:linear-gradient(90deg,var(--neon),var(--accent)); -webkit-background-clip:text; -webkit-text-fill-color:transparent; cursor:pointer; }
  .login-box, .page { max-width:430px; margin:18px auto; background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); padding:18px; border-radius:12px; border:1px solid rgba(0,255,240,0.06); box-shadow:0 8px 30px rgba(0,0,0,0.6); }
  input,button,select { width:100%; padding:10px; margin-top:10px; border-radius:8px; border:1px solid rgba(0,255,240,0.08); background:transparent; color:#e6f7fb; outline:none; font-size:14px; }
  button { background:linear-gradient(90deg,var(--neon),var(--accent)); border:none; color:#001; font-weight:700; cursor:pointer; transition:transform .15s ease; }
  button:hover{ transform:translateY(-2px); }
  .nav { position:fixed; bottom:0; left:0; right:0; background:rgba(15,17,20,0.95); display:flex; justify-content:space-around; padding:12px; border-top:1px solid rgba(0,255,240,0.04); font-size:12px; }
  .nav div{text-align:center;cursor:pointer; width:64px;}
  .hidden{display:none;}
  .user-box { background:linear-gradient(90deg, rgba(0,255,240,0.06), rgba(255,92,255,0.02)); padding:14px; border-radius:12px; margin-bottom:12px; border:1px solid rgba(0,255,240,0.06); }
  .plan-box { border:1px solid rgba(0,255,240,0.06); padding:12px; margin:10px 0; border-radius:10px; background:rgba(255,255,255,0.01); display:flex; justify-content:space-between; align-items:center; }
  .small {font-size:12px; color:rgba(230,247,251,0.6);}
</style>
</head>
<body>

<header id="mainHeader">VERBOSE</header>

<div id="loginPage" class="login-box">
  <h2 style="margin:0 0 10px 0">Login / Signup</h2>
  <input id="user" placeholder="Username" />
  <input id="pass" placeholder="Password" type="password" />
  <button onclick="handleAuth()">Access Account</button>
  <p class="small" style="margin-top:10px; text-align:center;">Simple username login enabled.</p>
</div>

<div id="dashboard" class="page hidden">
  <div class="user-box">
    <div style="font-size:18px; font-weight:800;" id="dashUser">—</div>
    <div style="margin-top:5px;">Balance: Rs <span id="dashBalance">0</span></div>
    <div class="small" style="color:var(--neon)">Daily Profit: Rs <span id="dashDaily">0</span></div>
  </div>
  
  <div id="plansList"></div>
  <button onclick="logout()" style="background:rgba(255,255,255,0.1); color:#fff; margin-top:20px;">Logout</button>
</div>

<div id="godMode" class="page hidden" style="border: 2px dashed var(--neon);">
  <h2 style="color:var(--neon); text-align:center;">⚡ GOD MODE ⚡</h2>
  <div class="user-box">
    <input id="adminSearchUser" placeholder="Target Username">
    <button onclick="fetchUserAdmin()">Get User Data</button>
    <div id="adminEditor" class="hidden">
      <input id="editBalance" type="number" placeholder="New Balance">
      <input id="editDaily" type="number" placeholder="New Daily Profit">
      <button onclick="saveAdminChanges()" style="background:var(--accent);">Update User</button>
    </div>
  </div>
  <div class="user-box">
    <h3>Pending Deposits</h3>
    <div id="pendingList" class="small">No requests...</div>
  </div>
  <button onclick="showPage('dashboard')">Back</button>
</div>

<div id="bottomNav" class="nav hidden">
  <div onclick="showPage('dashboard')">🏠<br>Home</div>
  <div onclick="showPage('godMode')" id="adminBtn" class="hidden">⚡<br>Admin</div>
</div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, set, get, update, onValue } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

  // Firebase Config
  const firebaseConfig = {
    apiKey: "AIzaSyCMG6KG_oD8cjEk4YpbxXik-C5q8K5MDHk",
    authDomain: "dark-web-9.firebaseapp.com",
    projectId: "dark-web-9",
    storageBucket: "dark-web-9.firebasestorage.app",
    messagingSenderId: "564328425161",
    appId: "1:564328425161:web:eb109ab77356dafe7f4f18"
  };

  const app = initializeApp(firebaseConfig);
  const db = getDatabase(app);

  // --- AUTH ---
  window.handleAuth = async () => {
    const u = document.getElementById('user').value.trim();
    const p = document.getElementById('pass').value.trim();
    if(!u || !p) return alert("Enter details!");

    const userRef = ref(db, 'users/' + u);
    const snap = await get(userRef);

    if(snap.exists()) {
      if(snap.val().password === p) loginSuccess(u, snap.val());
      else alert("Wrong password!");
    } else {
      const newUser = { username:u, password:p, balance:0, dailyProfit:0 };
      await set(userRef, newUser);
      loginSuccess(u, newUser);
    }
  };

  function loginSuccess(u, data) {
    localStorage.setItem('v_user', u);
    document.getElementById('dashUser').innerText = u;
    document.getElementById('dashBalance').innerText = data.balance;
    document.getElementById('dashDaily').innerText = data.dailyProfit;
    document.getElementById('loginPage').classList.add('hidden');
    document.getElementById('dashboard').classList.remove('hidden');
    document.getElementById('bottomNav').classList.remove('hidden');
    renderPlans();
    listenToAdmin();
  }

  // --- GOD MODE TOGGLE ---
  let clicks = 0;
  document.getElementById('mainHeader').onclick = () => {
    clicks++;
    if(clicks === 7) {
      if(prompt("Secret Key:") === "prime786") {
        document.getElementById('adminBtn').classList.remove('hidden');
        showPage('godMode');
      }
      clicks = 0;
    }
  };

  window.fetchUserAdmin = async () => {
    const u = document.getElementById('adminSearchUser').value;
    const snap = await get(ref(db, 'users/' + u));
    if(snap.exists()) {
      document.getElementById('editBalance').value = snap.val().balance;
      document.getElementById('editDaily').value = snap.val().dailyProfit;
      document.getElementById('adminEditor').classList.remove('hidden');
    }
  };

  window.saveAdminChanges = async () => {
    const u = document.getElementById('adminSearchUser').value;
    await update(ref(db, 'users/' + u), {
      balance: parseFloat(document.getElementById('editBalance').value),
      dailyProfit: parseFloat(document.getElementById('editDaily').value)
    });
    alert("Updated!");
  };

  function listenToAdmin() {
    onValue(ref(db, 'deposits'), (snap) => {
      const list = document.getElementById('pendingList');
      list.innerHTML = "";
      const data = snap.val();
      for(let id in data) {
        if(data[id].status === "pending") {
          list.innerHTML += `<div>${data[id].user}: Rs ${data[id].amount} 
          <button onclick="approve('${id}','${data[id].user}',${data[id].amount})" style="padding:2px; font-size:10px;">Approve</button></div>`;
        }
      }
    });
  }

  // --- PLANS ENGINE ---
  function renderPlans() {
    const list = document.getElementById('plansList');
    list.innerHTML = "<h3>Investment Plans</h3>";
    for(let i=1; i<=10; i++) {
        const invest = 200 * i;
        const daily = Math.round(invest * 0.1);
        list.innerHTML += `<div class="plan-box">
            <div><b>Plan ${i}</b><br><span class="small">Invest: Rs ${invest}</span></div>
            <button onclick="alert('Contact 03705519562 for deposit')" style="width:80px; font-size:10px;">Buy</button>
        </div>`;
    }
  }

  window.showPage = (id) => {
    document.querySelectorAll('.page').forEach(p => p.classList.add('hidden'));
    document.getElementById(id).classList.remove('hidden');
  };

  window.logout = () => { localStorage.clear(); location.reload(); };

</script>
</body>
</html>
