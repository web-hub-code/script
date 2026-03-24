<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Enterprise Solutions</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --dark: #020202; --glass: rgba(255,255,255,0.03); --card-border: rgba(255,255,255,0.08); }
  * { box-sizing: border-box; transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1); font-family: 'Inter', sans-serif; }
  body { margin:0; background: var(--dark); color: #fff; overflow-x: hidden; }
  
  header { text-align: center; padding: 40px 20px; font-size: 24px; font-weight: 800; letter-spacing: 10px; color: #fff; text-transform: uppercase; text-shadow: 0 0 20px rgba(0,247,255,0.3); }
  
  .page { max-width: 450px; margin: 0 auto 100px; padding: 20px; min-height: 80vh; }
  
  /* Modern Glass Cards */
  .user-card { background: var(--glass); border: 1px solid var(--card-border); padding: 22px; border-radius: 28px; margin-bottom: 20px; backdrop-filter: blur(25px); position: relative; overflow: hidden; }
  .user-card::before { content: ""; position: absolute; top: 0; left: 0; width: 4px; height: 100%; background: linear-gradient(to bottom, var(--neon), var(--accent)); }
  
  input { width: 100%; padding: 16px; margin-top: 12px; border-radius: 14px; border: 1px solid var(--card-border); background: rgba(0,0,0,0.7); color: #fff; font-size: 14px; outline: none; }
  input:focus { border-color: var(--neon); }
  
  button { width: 100%; padding: 16px; margin-top: 20px; border-radius: 16px; border: none; background: #fff; color: #000; font-weight: 800; cursor: pointer; text-transform: uppercase; font-size: 11px; letter-spacing: 1.5px; }
  .btn-neon { background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; box-shadow: 0 10px 20px rgba(0,0,0,0.3); }
  
  /* Navigation Bar - Clean & Modern */
  .nav { position: fixed; bottom: 0; left: 0; right: 0; background: rgba(0,0,0,0.9); display: flex; justify-content: space-around; padding: 15px 5px 30px; z-index: 1000; border-top: 1px solid var(--card-border); backdrop-filter: blur(15px); }
  .nav-item { text-align: center; font-size: 9px; cursor: pointer; opacity: 0.4; color: #fff; font-weight: 700; text-transform: uppercase; letter-spacing: 1px; }
  .nav-item.active { opacity: 1; color: var(--neon); text-shadow: 0 0 10px var(--neon); }

  .hidden { display: none !important; }
  
  /* Secret Admin Styles */
  #adminPortal { position: fixed; top: 50%; left: 50%; transform: translate(-50%, -50%); width: 90%; max-width: 380px; z-index: 10001; background: #080808; border: 1px solid var(--accent); padding: 30px; border-radius: 24px; box-shadow: 0 0 50px rgba(0,0,0,1); }
</style>
</head>
<body>

<header id="mainHeader">VERBOSE</header>

<div id="loginPage" class="page">
  <div style="text-align:center; margin-bottom:40px;">
    <h3 id="adminTrigger" style="margin:0; font-weight:800; cursor:default; user-select:none;">Secure Portal</h3>
    <p style="font-size:11px; opacity:0.4; letter-spacing:1px;">Multi-Factor Authentication Active</p>
  </div>
  
  <input id="u_name" placeholder="Username">
  <input id="u_pass" type="password" placeholder="Password">
  
  <div style="margin-top:20px; font-size:10px; display:flex; gap:10px; opacity:0.6;">
    <input type="checkbox" id="termsCheck" style="width:18px; margin:0;">
    <label for="termsCheck">I agree to the Professional Service Agreement and Risk Policy.</label>
  </div>
  <button id="entryBtn" class="btn-neon">Authorize & Login</button>
</div>

<div id="adminPortal" class="hidden">
  <h4 style="text-align:center; color:var(--neon); margin-top:0;">SYSTEM OVERRIDE</h4>
  <p style="font-size:10px; text-align:center; opacity:0.6;">Enter Secret Authorization Key</p>
  <input id="adminKey" type="password" placeholder="Key ID">
  <button onclick="accessAdmin()" class="btn-neon">Access Console</button>
  <button onclick="closeSecretPortal()" style="background:transparent; color:#fff; border:1px solid #333; margin-top:10px;">Cancel</button>
</div>

<div id="dashboard" class="page hidden">
  <div class="user-card" style="background: linear-gradient(135deg, rgba(0,247,255,0.05), rgba(112,0,255,0.05));">
    <div style="font-size:10px; opacity:0.5; text-transform:uppercase;">Current Liquidity</div>
    <div style="font-size:38px; font-weight:800; margin:10px 0;">PKR <span id="mainBal">0.00</span></div>
    <div style="font-size:9px; color:var(--neon); font-weight:800; letter-spacing:1px;">ACCOUNT STATUS: VERIFIED</div>
  </div>
  
  <div class="user-card" style="border-left-color: #ff4646; background: rgba(255,70,70,0.05);">
    <b style="font-size:11px; color:#ff4646;">SECURITY NOTICE:</b>
    <p style="font-size:10px; margin-top:5px; opacity:0.7; line-height:1.6;">Never share your recovery key. Official support communicates only via encrypted channels.</p>
  </div>
  
  <button onclick="tab('plansPage')" class="btn-neon">Investment Marketplace</button>
</div>

<div id="bottomNav" class="nav hidden">
  <div class="nav-item active" onclick="tab('dashboard', this)">Home</div>
  <div class="nav-item" onclick="tab('plansPage', this)">Plans</div>
  <div class="nav-item" onclick="tab('partnershipPage', this)">Network</div>
  <div class="nav-item" onclick="tab('walletPage', this)">Wallet</div>
  </div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, set, get, update, onValue } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

  // Firebase Config setup here
  const app = initializeApp(firebaseConfig);
  const db = getDatabase(app);

  const MASTER_KEY = "NAZIM786";

  // --- SECRET ADMIN TRIGGER LOGIC ---
  let secretClicks = 0;
  document.getElementById('adminTrigger').onclick = () => {
    secretClicks++;
    if(secretClicks >= 7) {
      document.getElementById('adminPortal').classList.remove('hidden');
      secretClicks = 0;
    }
    // Reset clicks after 3 seconds of inactivity
    setTimeout(() => { secretClicks = 0; }, 3000);
  };

  window.closeSecretPortal = () => {
    document.getElementById('adminPortal').classList.add('hidden');
  };

  window.accessAdmin = () => {
    const key = document.getElementById('adminKey').value;
    if(key === MASTER_KEY) {
      alert("System Authorized.");
      document.getElementById('adminPortal').classList.add('hidden');
      tab('adminPage'); // Now you can enter the admin page
    } else {
      alert("Access Denied.");
    }
  };

  // --- SESSION MANAGEMENT ---
  window.onload = () => {
    const user = localStorage.getItem('v_user');
    if(user) sessionStart(user);
  };

  function sessionStart(u) {
    localStorage.setItem('v_user', u);
    document.getElementById('loginPage').classList.add('hidden');
    document.getElementById('dashboard').classList.remove('hidden');
    document.getElementById('bottomNav').classList.remove('hidden');
    
    onValue(ref(db, 'users/' + u), snap => {
      if(snap.exists()) {
        document.getElementById('mainBal').innerText = parseFloat(snap.val().balance).toLocaleString();
      }
    });
  }

  // Login handler
  document.getElementById('entryBtn').onclick = async () => {
    const u = document.getElementById('u_name').value.trim().toLowerCase();
    const p = document.getElementById('u_pass').value.trim();
    if(!u || !p || !document.getElementById('termsCheck').checked) return alert("Fill all requirements.");
    
    const snap = await get(ref(db, 'users/' + u));
    if(snap.exists()){
      if(snap.val().password === p) sessionStart(u); else alert("Invalid Login.");
    } else {
      await set(ref(db, 'users/' + u), { username:u, password:p, balance:0 });
      sessionStart(u);
    }
  };

  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.add('hidden'));
    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
    document.getElementById(id).classList.remove('hidden');
    if(el) el.classList.add('active');
  };
</script>
</body>
</html>
