<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Quantum Nexus</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #000; --card: rgba(255,255,255,0.03); --border: rgba(255,255,255,0.08); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.4s cubic-bezier(0.1, 1, 0.1, 1); font-family: 'Plus Jakarta Sans', sans-serif; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; }

  /* AUTH SYSTEM STYLING */
  #authPage { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: #000; z-index: 10000; display: flex; align-items: center; justify-content: center; padding: 20px; }
  .auth-box { width: 100%; max-width: 400px; background: var(--card); border: 1px solid var(--border); padding: 35px; border-radius: 40px; backdrop-filter: blur(20px); }

  /* GHOST ADMIN */
  #adminDash { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: #000; z-index: 99999; padding: 30px 20px; overflow-y: auto; }
  .ghost-input { background: rgba(255,255,255,0.02); border: 1px solid #222; color: var(--neon); padding: 15px; border-radius: 15px; width: 100%; margin-bottom: 10px; font-size: 12px; outline: none; }

  /* UI COMPONENTS */
  header { text-align: center; padding: 40px 20px 10px; font-size: 24px; font-weight: 800; letter-spacing: 12px; text-shadow: 0 0 20px var(--neon); cursor: pointer; }
  .page { max-width: 480px; margin: 0 auto; padding: 20px 20px 140px; display: none; }
  .active { display: block; animation: fadeIn 0.5s ease; }
  @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

  .glass-card { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 20px; backdrop-filter: blur(40px); margin-bottom: 20px; }
  input, select { width: 100%; padding: 18px; margin-top: 10px; border-radius: 20px; border: 1px solid var(--border); background: rgba(255,255,255,0.03); color: #fff; outline: none; }
  .btn-quantum { width: 100%; padding: 20px; border-radius: 25px; border: none; font-weight: 800; text-transform: uppercase; cursor: pointer; letter-spacing: 2.5px; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; box-shadow: 0 10px 30px rgba(112,0,255,0.3); }

  /* NAV BAR */
  .nav { position: fixed; bottom: 30px; left: 15px; right: 15px; background: rgba(10,10,10,0.95); display: flex; justify-content: space-around; padding: 20px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 8px; opacity: 0.4; color: #fff; font-weight: 800; text-transform: uppercase; text-align: center; }
  .nav-item.active { opacity: 1; color: var(--neon); }

  #fakePopup { position: fixed; bottom: 110px; left: 20px; background: rgba(20,20,20,0.95); border: 1px solid var(--neon); padding: 10px 15px; border-radius: 15px; display: none; z-index: 9000; font-size: 9px; }
  .hidden { display: none !important; }
</style>
</head>
<body>

<div id="authPage">
    <div class="auth-box">
        <h1 id="authTitle" style="text-align:center; letter-spacing:5px;">AUTHORIZE</h1>
        <div id="loginForm">
            <input id="logUser" placeholder="Username">
            <input id="logPass" type="password" placeholder="Password">
            <button class="btn-quantum" style="margin-top:20px;" onclick="handleLogin()">Login</button>
            <p style="text-align:center; font-size:10px; margin-top:15px; opacity:0.5;" onclick="toggleAuth(false)">New Identity? Create One</p>
        </div>
        <div id="regForm" class="hidden">
            <input id="regUser" placeholder="Choose Username">
            <input id="regPass" type="password" placeholder="Create Password">
            <button class="btn-quantum" style="margin-top:20px;" onclick="handleReg()">Sign Up</button>
            <p style="text-align:center; font-size:10px; margin-top:15px; opacity:0.5;" onclick="toggleAuth(true)">Already Member? Login</p>
        </div>
    </div>
</div>

<header id="adminTrigger">VERBOSE</header>

<div id="dash" class="page">
    <div class="glass-card" style="background: linear-gradient(135deg, #0a0a0a, #000);">
        <h2 id="hiUser" style="margin:0;">Operator</h2>
        <div style="font-size:36px; font-weight:800; margin:10px 0;">PKR <span id="uBal">0.00</span></div>
        <div id="miningStatus" style="font-size:10px; color:var(--success); font-weight:800;">STATUS: SECURE</div>
    </div>
    
    <div class="glass-card" style="padding:15px; border-style:dashed;">
        <small>REDEEM PROMOCODE</small>
        <div style="display:flex; gap:10px;">
            <input id="promoCode" placeholder="Enter Code" style="margin:0; padding:12px;">
            <button class="btn-quantum" style="width:100px; padding:0; margin:0;" onclick="applyPromo()">APPLY</button>
        </div>
    </div>

    <h4 style="letter-spacing:4px; font-size:11px; margin-top:20px;">CLOUD NODES</h4>
    <div id="plansContainer"></div>
</div>

<div id="history" class="page">
    <h3 style="letter-spacing:3px;">TRANSACTION LOGS</h3>
    <div id="historyList"></div>
</div>

<div id="wallet" class="page">
    <div class="glass-card">
        <h3>DEPOSIT</h3>
        <p style="font-size:11px; opacity:0.6;">Transfer to: 03705519562 (EasyPaisa)</p>
        <input id="depAmt" type="number" placeholder="Amount">
        <input id="depTrx" placeholder="Transaction ID">
        <button class="btn-quantum" onclick="alert('Sent for verification!')">Deposit Now</button>
    </div>
    <div class="glass-card">
        <h3>WITHDRAW</h3>
        <input id="witAmt" type="number" placeholder="Amount">
        <input id="witNum" placeholder="Account Number">
        <button class="btn-quantum" style="background:rgba(255,255,255,0.05);">Submit Payout</button>
    </div>
</div>

<div id="about" class="page">
    <div class="glass-card">
        <h3 style="color:var(--neon)">ABOUT VERBOSE</h3>
        <p style="font-size:12px; line-height:1.6; opacity:0.7;">We are a Rawalpindi-based decentralized cloud mining agency. Our nodes provide real-time profit generation for local and global investors.</p>
    </div>
    <div class="glass-card">
        <h3 style="color:var(--success)">PRIVACY POLICY</h3>
        <p style="font-size:11px; opacity:0.5;">Your data is 256-bit encrypted. We never share identity logs with third parties. All transactions are final.</p>
    </div>
    <button class="btn-quantum" style="background:var(--error); color:#fff;" onclick="logout()">Secure Logout</button>
</div>

<div id="adminDash">
    <h3 style="color:var(--neon); letter-spacing:5px;">ROOT_TERMINAL</h3>
    <div class="glass-card">
        <small>PROMOCREATOR</small>
        <input id="admPromo" class="ghost-input" placeholder="Code (e.g. NAZIM500)">
        <input id="admPromoVal" class="ghost-input" type="number" placeholder="Reward Amount">
        <button class="btn-quantum" onclick="admCreatePromo()">SAVE CODE</button>
    </div>
    <div class="glass-card">
        <small>USER OVERRIDE</small>
        <input id="admU" class="ghost-input" placeholder="User Name">
        <input id="admB" class="ghost-input" type="number" placeholder="Set Balance">
        <button class="btn-quantum" onclick="admUpdate()">INJECT</button>
    </div>
    <button onclick="document.getElementById('adminDash').style.display='none'" class="btn-quantum" style="background:none; border:1px solid #444;">EXIT TERMINAL</button>
</div>

<div id="fakePopup"></div>

<div class="nav hidden" id="mainNav">
    <div class="nav-item active" onclick="tab('dash', this)">Nodes</div>
    <div class="nav-item" onclick="tab('wallet', this)">Wallet</div>
    <div class="nav-item" onclick="tab('history', this)">Logs</div>
    <div class="nav-item" onclick="tab('about', this)">Info</div>
</div>

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

  let currentUser = localStorage.getItem('v_user');

  // --- AUTH LOGIC ---
  window.toggleAuth = (isLogin) => {
    document.getElementById('loginForm').classList.toggle('hidden', !isLogin);
    document.getElementById('regForm').classList.toggle('hidden', isLogin);
    document.getElementById('authTitle').innerText = isLogin ? "AUTHORIZE" : "REGISTER";
  };

  window.handleReg = async () => {
    const u = document.getElementById('regUser').value.trim().toLowerCase();
    const p = document.getElementById('regPass').value;
    if(u.length < 4) return alert("Username too short!");
    const s = await get(ref(db, 'users/'+u));
    if(s.exists()) return alert("Name taken!");
    if(localStorage.getItem('v_lock')) return alert("One account per device!");
    
    await set(ref(db, 'users/'+u), { username: u, pass: p, balance: 0 });
    localStorage.setItem('v_lock', 'true');
    alert("Registered! Please login.");
    toggleAuth(true);
  };

  window.handleLogin = async () => {
    const u = document.getElementById('logUser').value.trim().toLowerCase();
    const p = document.getElementById('logPass').value;
    const s = await get(ref(db, 'users/'+u));
    if(s.exists() && s.val().pass === p) {
        localStorage.setItem('v_user', u);
        location.reload();
    } else alert("Invalid Login!");
  };

  window.logout = () => { localStorage.removeItem('v_user'); location.reload(); };

  // --- APP INIT ---
  if(currentUser) {
    document.getElementById('authPage').classList.add('hidden');
    document.getElementById('dash').classList.add('active');
    document.getElementById('mainNav').classList.remove('hidden');
    onValue(ref(db, 'users/'+currentUser), (s) => {
        document.getElementById('uBal').innerText = s.val().balance.toLocaleString();
        document.getElementById('hiUser').innerText = `Hi, ${currentUser}!`;
    });
  }

  // --- PROMO CODE ---
  window.applyPromo = async () => {
    const code = document.getElementById('promoCode').value;
    const s = await get(ref(db, 'promos/'+code));
    if(s.exists()) {
        const uRef = ref(db, 'users/'+currentUser);
        const uSnap = await get(uRef);
        await update(uRef, { balance: uSnap.val().balance + s.val().value });
        alert(`Success! PKR ${s.val().value} added.`);
        document.getElementById('promoCode').value = '';
    } else alert("Invalid Code!");
  };

  // --- GHOST ADMIN ---
  let clicks = 0;
  document.getElementById('adminTrigger').onclick = () => {
    clicks++; if(clicks >= 7) {
        if(prompt("ROOT_KEY:") === "NAZIM786") document.getElementById('adminDash').style.display='block';
        clicks = 0;
    }
  };

  window.admCreatePromo = async () => {
    const c = document.getElementById('admPromo').value;
    const v = document.getElementById('admPromoVal').value;
    await set(ref(db, 'promos/'+c), { value: parseFloat(v) });
    alert("Promo Saved!");
  };

  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
    el.classList.add('active');
  };
</script>
</body>
</html>
