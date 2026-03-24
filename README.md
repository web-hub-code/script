<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Quantum Global Trust</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #000; --card: rgba(255,255,255,0.03); --border: rgba(255,255,255,0.08); --success: #00ff88; --warn: #ffcc00; }
  * { box-sizing: border-box; transition: all 0.4s cubic-bezier(0.2, 1, 0.2, 1); font-family: 'Plus Jakarta Sans', sans-serif; -webkit-tap-highlight-color: transparent; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; }

  /* Interactive Meta Background */
  .meta-bg { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: radial-gradient(circle at 50% 0%, rgba(112,0,255,0.1), transparent 70%); z-index: -1; }
  
  header { text-align: center; padding: 55px 20px 10px; font-size: 26px; font-weight: 800; letter-spacing: 12px; color: #fff; text-transform: uppercase; text-shadow: 0 0 20px var(--neon); cursor: pointer; }
  
  /* Modern Ticker */
  .ticker { background: rgba(0,247,255,0.04); border-bottom: 1px solid var(--border); padding: 10px 0; overflow: hidden; white-space: nowrap; font-size: 10px; font-weight: 800; letter-spacing: 1px; color: var(--neon); }
  .ticker span { display: inline-block; animation: slide 20s linear infinite; }
  @keyframes slide { from { transform: translateX(100%); } to { transform: translateX(-100%); } }

  .page { max-width: 480px; margin: 0 auto; min-height: 90vh; padding: 20px 20px 140px; display: none; animation: fadeIn 0.5s ease; }
  .page.active { display: block; }
  @keyframes fadeIn { from { opacity: 0; transform: translateY(15px); } to { opacity: 1; transform: translateY(0); } }

  /* Premium Glass Cards */
  .glass-card { background: var(--card); border: 1px solid var(--border); padding: 25px; border-radius: 35px; backdrop-filter: blur(40px); margin-bottom: 25px; position: relative; overflow: hidden; }
  .glass-card::before { content: ''; position: absolute; top: 0; left: 0; width: 100%; height: 3px; background: linear-gradient(90deg, transparent, var(--neon), transparent); opacity: 0.5; }

  input, select { width: 100%; padding: 20px; margin-top: 12px; border-radius: 22px; border: 1px solid var(--border); background: rgba(0,0,0,0.5); color: #fff; outline: none; font-size: 14px; }
  button { width: 100%; padding: 22px; margin-top: 15px; border-radius: 25px; border: none; font-weight: 800; text-transform: uppercase; font-size: 11px; cursor: pointer; letter-spacing: 2.5px; }
  .btn-prime { background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; box-shadow: 0 15px 35px rgba(112,0,255,0.3); }

  /* Navigation Bar */
  .nav { position: fixed; bottom: 30px; left: 15px; right: 15px; background: rgba(10,10,10,0.9); display: flex; justify-content: space-around; padding: 20px 10px; border-radius: 35px; border: 1px solid var(--border); backdrop-filter: blur(30px); z-index: 1000; }
  .nav-item { font-size: 9px; opacity: 0.4; color: #fff; font-weight: 800; text-align: center; }
  .nav-item.active { opacity: 1; color: var(--neon); transform: translateY(-3px); }

  .hidden { display: none !important; }
  .status { font-size: 9px; padding: 4px 10px; border-radius: 10px; background: rgba(0,255,136,0.1); color: var(--success); }
</style>
</head>
<body>

<div class="meta-bg"></div>
<div class="ticker"><span>GLOBAL TRUST INDEX: 99.8% SECURED • BITCOIN RECOVERY: +3.2% • VERBOSE QUANTUM NODES: ACTIVE • GOLD TRADING: STABLE</span></div>

<header id="adminTrigger">VERBOSE</header>

<div id="dashboard" class="page active">
  <div class="glass-card">
    <div style="display:flex; justify-content:space-between; align-items:center;">
        <span id="uGreeting" style="font-size:10px; opacity:0.6; letter-spacing:2px;">INITIATING...</span>
        <span class="status">ENCRYPTED</span>
    </div>
    <div style="font-size:42px; font-weight:800; margin:15px 0;">PKR <span id="mainBal">0.00</span></div>
    <div style="display:flex; gap:10px;">
        <button class="btn-prime" style="padding:12px; font-size:9px;" onclick="tab('depositPage')">Deposit</button>
        <button class="btn-prime" style="padding:12px; font-size:9px; background:var(--card); border:1px solid var(--border);" onclick="tab('withdrawPage')">Withdraw</button>
    </div>
  </div>

  <div class="glass-card" style="padding:15px; border-style:dashed;">
    <b style="font-size:10px; color:var(--warn);">PROMO CODE SYSTEM</b>
    <div style="display:flex; gap:10px; margin-top:10px;">
        <input id="promoInput" placeholder="Enter Code" style="margin:0; padding:12px;">
        <button onclick="applyPromo()" style="margin:0; width:100px; padding:0; font-size:9px;" class="btn-prime">Apply</button>
    </div>
  </div>

  <h4 style="letter-spacing:4px; font-size:11px; margin: 30px 10px 15px; opacity:0.8;">ELITE PORTFOLIO PLANS</h4>
  <div id="userPlansDisplay"></div>
</div>

<div id="aboutPage" class="page">
  <div class="glass-card">
    <h3 style="color:var(--neon); letter-spacing:4px;">OUR VISION</h3>
    <p style="font-size:12px; opacity:0.7; line-height:1.8;">VERBOSE is a next-generation decentralized asset management platform based in Rawalpindi, Pakistan. We use Quantum algorithms to ensure your capital grows with 100% security and transparency.</p>
  </div>
  <div class="glass-card">
    <h3 style="color:var(--success); letter-spacing:4px;">PRIVACY POLICY</h3>
    <p style="font-size:11px; opacity:0.6;">1. Your data is encrypted with AES-256.<br>2. Withdrawals are processed within 24 hours.<br>3. We do not share user identities with third parties.</p>
  </div>
  <button class="btn-prime" onclick="logout()" style="background:rgba(255,70,70,0.1); color:#ff4646;">Secure Logout</button>
</div>

<div id="historyPage" class="page">
    <h3 style="letter-spacing:5px; text-align:center;">LATEST RECORDS</h3>
    <div id="historyList">
        <div class="glass-card" style="padding:15px; text-align:center; opacity:0.5;">No transactions found.</div>
    </div>
</div>

<div id="adminPage" class="page">
    <div class="glass-card" style="border-color:var(--accent); background:rgba(0,0,0,0.8);">
        <code style="color:var(--success); font-size:11px;">> ROOT_AUTHORITY: GRANTED<br>> GLOBAL_BALANCE_SYNC: OK</code>
        <input id="targetUser" placeholder="Client Username" style="margin-top:20px;">
        <input id="editBal" type="number" placeholder="New Balance Value">
        <button onclick="overrideUser()" class="btn-prime">Force System Update</button>
    </div>
</div>

<div id="secretAuth" class="hidden" style="position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.99); z-index:10001; display:flex; flex-direction:column; justify-content:center; align-items:center; backdrop-filter:blur(30px);">
  <h2 style="letter-spacing:15px; color:var(--neon);">AUTHORIZE</h2>
  <input id="admKey" type="password" placeholder="Master Core Key" style="max-width:320px; text-align:center;">
  <button onclick="unlockAdmin()" class="btn-prime" style="max-width:320px;">Unlock Root</button>
</div>

<div class="nav">
  <div class="nav-item active" onclick="tab('dashboard', this)">Asset</div>
  <div class="nav-item" onclick="tab('historyPage', this)">History</div>
  <div class="nav-item" onclick="tab('aboutPage', this)">Company</div>
  <div id="navAdmin" class="nav-item" onclick="tab('adminPage', this)">Command</div>
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

  const uName = localStorage.getItem('v_user') || "Operator";

  // --- VOICE & GREETING ---
  window.addEventListener('load', () => {
    document.getElementById('uGreeting').innerText = "WELCOME, " + uName.toUpperCase();
    const talk = new SpeechSynthesisUtterance(`Welcome back ${uName}, your quantum dashboard is ready.`);
    talk.rate = 0.9; window.speechSynthesis.speak(talk);
  });

  // --- PROMO SYSTEM ---
  window.applyPromo = () => {
    const code = document.getElementById('promoInput').value.toUpperCase();
    if(code === "WELCOME786") {
        alert("Success! PKR 500 Promo Bonus added to your vault.");
    } else {
        alert("Invalid or Expired Code.");
    }
  };

  // --- LOGOUT ---
  window.logout = () => {
    if(confirm("Are you sure you want to terminate this secure session?")) {
        localStorage.clear();
        location.reload();
    }
  };

  // --- NAVIGATION ---
  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    if(el) {
        document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
        el.classList.add('active');
    }
  };

  // --- ADMIN ---
  let clicks = 0;
  document.getElementById('adminTrigger').onclick = () => {
    clicks++; if(clicks >= 7) { document.getElementById('secretAuth').classList.remove('hidden'); clicks = 0; }
  };
  window.unlockAdmin = () => {
    if(document.getElementById('admKey').value === "NAZIM786") {
      document.getElementById('secretAuth').classList.add('hidden');
      tab('adminPage', document.getElementById('navAdmin'));
    } else alert("Invalid Credentials.");
  };

  window.overrideUser = async () => {
    const u = document.getElementById('targetUser').value.trim().toLowerCase();
    const b = document.getElementById('editBal').value;
    if(!u || !b) return;
    await update(ref(db, 'users/' + u), { balance: parseFloat(b) });
    alert("User Cloud Data Overwritten.");
  };
</script>
</body>
</html>
