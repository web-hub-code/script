<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>VERBOSE — Professional</title>
<style>
  /* BASE STYLES (Same as your original file) */
  :root{ --neon:#00f7ff; --accent:#ff5cff; --dark:#070707; --panel:#0f1114; }
  *{box-sizing:border-box}
  body { margin:0; font-family:Inter, Arial, sans-serif; background:var(--dark); color:#fff; overflow-x:hidden; -webkit-font-smoothing:antialiased; }
  header { text-align:center; padding:24px 12px; font-size:28px; font-weight:800; letter-spacing:2px; background:linear-gradient(90deg,var(--neon),var(--accent)); -webkit-background-clip:text; -webkit-text-fill-color:transparent; cursor:pointer; }
  
  /* Cards / Panels */
  .login-box, .page { max-width:430px; margin:18px auto; background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); padding:18px; border-radius:12px; border:1px solid rgba(0,255,240,0.06); box-shadow:0 8px 30px rgba(0,0,0,0.6); }
  input,button,select { width:100%; padding:10px; margin-top:10px; border-radius:8px; border:1px solid rgba(0,255,240,0.08); background:transparent; color:#e6f7fb; outline:none; font-size:14px; }
  button { background:linear-gradient(90deg,var(--neon),var(--accent)); border:none; color:#001; font-weight:700; cursor:pointer; transition:transform .15s ease; }
  button:hover{ transform:translateY(-2px); }

  /* Navigation */
  .nav { position:fixed; bottom:0; left:0; right:0; background:rgba(15,17,20,0.95); display:flex; justify-content:space-around; padding:12px; border-top:1px solid rgba(0,255,240,0.04); font-size:11px; z-index:1000; }
  .nav div{text-align:center;cursor:pointer; width:60px;}
  .hidden{display:none;}

  /* User & Plan Boxes (Your original CSS) */
  .user-box { background:linear-gradient(90deg, rgba(0,255,240,0.06), rgba(255,92,255,0.02)); padding:14px; border-radius:12px; margin-bottom:12px; border:1px solid rgba(0,255,240,0.06); }
  .plan-box { border:1px solid rgba(0,255,240,0.06); padding:12px; margin:10px 0; border-radius:10px; background:rgba(255,255,255,0.01); display:flex; justify-content:space-between; align-items:center; }
  .alert-box { background:rgba(255,92,255,0.05); padding:12px; border-radius:10px; margin-bottom:12px; border:1px solid rgba(255,92,255,0.2); color:var(--accent); font-size:12px; }
  .small {font-size:12px; color:rgba(230,247,251,0.6);}
</style>
</head>
<body>

<header id="mainHeader">VERBOSE</header>

<div id="loginPage" class="login-box">
  <h2 style="margin:0">Access Portal</h2>
  <p class="small">Powered by Prime Solutions</p>
  <input id="user" placeholder="Username" />
  <input id="pass" placeholder="Password" type="password" />
  <button onclick="handleAuth()">Login / Signup</button>
  <p class="small" style="margin-top:15px; text-align:center;">Tip: Use same username for all your assets.</p>
</div>

<div id="dashboard" class="page hidden">
  <div class="alert-box">Warning: Only use official VERBOSE channels for deposits (JazzCash: 03705519562).</div>
  <div class="user-box">
    <div id="dashUser" style="font-size:18px; font-weight:800;">Welcome</div>
    <div style="margin-top:5px;">Balance: Rs <span id="dashBalance">0</span></div>
    <div class="small" style="color:var(--neon)">Daily Profit: Rs <span id="dashDaily">0</span></div>
  </div>
  
  <div class="user-box" style="background:transparent;">
    <p class="small">Referral Link:</p>
    <input id="refLink" readonly style="font-size:10px; border-style:dashed;">
    <button onclick="copyRef()" style="margin-top:5px; padding:5px;">Copy Link</button>
  </div>
</div>

<div id="plans" class="page hidden">
  <h2 style="color:var(--neon)">Investment Plans</h2>
  <div id="plansList"></div>
</div>

<div id="history" class="page hidden">
  <h3>Transaction History</h3>
  <div id="historyList" class="small">No history found.</div>
</div>

<div id="about" class="page hidden">
  <div class="user-box">
    <h3>About VERBOSE</h3>
    <p class="small">A professional asset management platform by Prime Solutions. Secure, Transparent, and Professional.</p>
    <p class="small"><b>WhatsApp Support:</b> 03705519562</p>
    <p class="small"><b>Email:</b> rock.earn92@gmail.com</p>
  </div>
  <h3>Privacy Policy</h3>
  <p class="small">We use Firebase cloud encryption to protect your data. Each withdrawal is manually verified by Muhammad Nazim.</p>
</div>

<div id="godMode" class="page hidden" style="border: 2px dashed var(--neon);">
  <h2 style="color:var(--neon); text-align:center;">⚡ GOD MODE ⚡</h2>
  <div class="user-box">
    <input id="adminSearchUser" placeholder="Target Username">
    <button onclick="fetchUserAdmin()">Fetch User</button>
    <div id="adminEditor" class="hidden">
      <input id="editBalance" type="number" placeholder="New Balance">
      <input id="editDaily" type="number" placeholder="New Daily">
      <button onclick="saveAdminChanges()">Update Account</button>
    </div>
  </div>
  <div class="user-box">
    <h3>Pending Deposits</h3>
    <div id="pendingList" class="small"></div>
  </div>
  <button onclick="showPage('dashboard')">Close Admin</button>
</div>

<div id="bottomNav" class="nav hidden">
  <div onclick="showPage('dashboard')">🏠<br>Home</div>
  <div onclick="showPage('plans')">📦<br>Plans</div>
  <div onclick="showPage('history')">📜<br>History</div>
  <div onclick="showPage('about')">ℹ️<br>About</div>
  <div onclick="logout()">🚪<br>Logout</div>
  <div onclick="showPage('godMode')" id="adminBtn" class="hidden">⚡<br>Admin</div>
</div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, set, get, update, onValue } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

  // Configuration from your Firebase setup
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

  // --- AUTH SYSTEM (Sign up / Login same flow) ---
  window.handleAuth = async () => {
    const u = document.getElementById('user').value.trim();
    const p = document.getElementById('pass').value.trim();
    if(!u || !p) return alert("Please fill details!");

    const userRef = ref(db, 'users/' + u);
    const snap = await get(userRef);

    if(snap.exists()){
      if(snap.val().password === p) loginSuccess(u, snap.val());
      else alert("Wrong password, sweetie!");
    } else {
      const newUser = { 
        username: u, 
        password: p, 
        balance: 0, 
        dailyProfit: 0, 
        refCode: Math.random().toString(36).substring(7) 
      };
      await set(userRef, newUser);
      loginSuccess(u, newUser);
    }
  };

  function loginSuccess(u, data) {
    localStorage.setItem('v_user', u);
    document.getElementById('dashUser').innerText = u;
    document.getElementById('dashBalance').innerText = data.balance;
    document.getElementById('dashDaily').innerText = data.dailyProfit;
    document.getElementById('refLink').value = "https://gtv140.github.io/verbose/?ref=" + data.refCode;
    
    showPage('dashboard');
    document.getElementById('loginPage').classList.add('hidden');
    document.getElementById('bottomNav').classList.remove('hidden');
    
    renderPlans();
    loadHistory(u);
    listenForAdmin();
  }

  // --- RENDERING PLANS (25 Plans from your logic) ---
  function renderPlans() {
    const list = document.getElementById('plansList');
    list.innerHTML = "";
    for(let i=1; i<=25; i++) {
      const invest = Math.round(200 + (i-1)*(30000-200)/24);
      const daily = Math.round((invest * 2.3) / 25);
      list.innerHTML += `
        <div class="plan-box">
          <div><b>Plan ${i}</b><span class="small">Invest: Rs ${invest}<br>Daily: Rs ${daily}</span></div>
          <button onclick="buyPlan(${invest})" style="width:80px; font-size:10px;">Buy Now</button>
        </div>`;
    }
  }

  window.buyPlan = (amt) => {
    const u = localStorage.getItem('v_user');
    alert("Send Rs " + amt + " to JazzCash: 03705519562. Then contact admin.");
    const dId = Date.now();
    set(ref(db, 'deposits/' + dId), { user:u, amount:amt, status:'pending' });
  };

  // --- GOD MODE (7 Clicks on Header) ---
  let clicks = 0;
  document.getElementById('mainHeader').onclick = () => {
    clicks++;
    if(clicks === 7) {
      if(prompt("Admin Key:") === "prime786") {
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
    alert("Data updated, Boss!");
  };

  function listenForAdmin() {
    onValue(ref(db, 'deposits'), (snap) => {
      const pList = document.getElementById('pendingList');
      pList.innerHTML = "";
      const data = snap.val();
      for(let id in data) {
        if(data[id].status === 'pending') {
          pList.innerHTML += `<div style="margin-bottom:5px;">${data[id].user}: Rs ${data[id].amount} 
          <button onclick="approveDep('${id}','${data[id].user}',${data[id].amount})" style="padding:2px; width:60px;">OK</button></div>`;
        }
      }
    });
  }

  window.approveDep = async (id, u, amt) => {
    const uSnap = await get(ref(db, 'users/' + u));
    const newB = (uSnap.val().balance || 0) + amt;
    await update(ref(db, 'users/' + u), { balance: newB });
    await update(ref(db, 'deposits/' + id), { status: 'success' });
    alert("Approved!");
  };

  // --- UTILS ---
  window.showPage = (id) => {
    document.querySelectorAll('.page').forEach(p => p.classList.add('hidden'));
    document.getElementById(id).classList.remove('hidden');
  };
  window.copyRef = () => {
    document.getElementById('refLink').select();
    document.execCommand('copy');
    alert("Link Copied!");
  };
  window.logout = () => { localStorage.clear(); location.reload(); };

</script>
</body>
</html>
