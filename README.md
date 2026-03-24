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

  /* AUTH LAYER */
  #authPage { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: #000; z-index: 10000; display: flex; align-items: center; justify-content: center; padding: 20px; }
  .auth-box { width: 100%; max-width: 400px; background: var(--card); border: 1px solid var(--border); padding: 35px; border-radius: 40px; backdrop-filter: blur(20px); text-align: center; }

  /* GHOST ADMIN */
  #adminDash { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: #000; z-index: 99999; padding: 30px 20px; overflow-y: auto; }
  .ghost-input { background: rgba(255,255,255,0.02); border: 1px solid #222; color: var(--neon); padding: 15px; border-radius: 15px; width: 100%; margin-bottom: 10px; font-size: 12px; outline: none; }

  /* UI COMPONENTS */
  header { text-align: center; padding: 40px 20px 10px; font-size: 24px; font-weight: 800; letter-spacing: 12px; text-shadow: 0 0 20px var(--neon); cursor: pointer; }
  .page { max-width: 480px; margin: 0 auto; padding: 20px 20px 140px; display: none; }
  .active { display: block !important; animation: fadeIn 0.5s ease; }
  @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

  .glass-card { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 20px; backdrop-filter: blur(40px); margin-bottom: 20px; }
  input, select { width: 100%; padding: 18px; margin-top: 10px; border-radius: 20px; border: 1px solid var(--border); background: rgba(255,255,255,0.03); color: #fff; outline: none; }
  .btn-quantum { width: 100%; padding: 20px; border-radius: 25px; border: none; font-weight: 800; text-transform: uppercase; cursor: pointer; letter-spacing: 2.5px; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; box-shadow: 0 10px 30px rgba(112,0,255,0.3); margin-top: 15px; }

  /* NAV BAR */
  .nav { position: fixed; bottom: 30px; left: 15px; right: 15px; background: rgba(10,10,10,0.95); display: none; justify-content: space-around; padding: 20px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 8px; opacity: 0.4; color: #fff; font-weight: 800; text-transform: uppercase; text-align: center; cursor: pointer; }
  .nav-item.active { opacity: 1; color: var(--neon); }

  #fakePopup { position: fixed; bottom: 110px; left: 20px; background: rgba(20,20,20,0.95); border: 1px solid var(--neon); padding: 10px 15px; border-radius: 15px; display: none; z-index: 9000; font-size: 9px; animation: slideIn 0.5s forwards; }
  @keyframes slideIn { from { transform: translateY(100px); } to { transform: translateY(0); } }
  .hidden { display: none !important; }
</style>
</head>
<body>

<div id="authPage">
    <div class="auth-box">
        <h1 id="authTitle" style="letter-spacing:5px;">AUTHORIZE</h1>
        <div id="loginForm">
            <input id="logUser" placeholder="Username">
            <input id="logPass" type="password" placeholder="Password">
            <button class="btn-quantum" onclick="handleLogin()">ACCESS TERMINAL</button>
            <p style="font-size:10px; margin-top:15px; opacity:0.5;" onclick="toggleAuth('reg')">Create New Identity</p>
            <p style="font-size:10px; margin-top:5px; color:var(--neon);" onclick="alert('Please contact Admin on WhatsApp to reset password.')">Forgot Password?</p>
        </div>
        <div id="regForm" class="hidden">
            <input id="regUser" placeholder="Unique Username">
            <input id="regPass" type="password" placeholder="Create Password">
            <button class="btn-quantum" onclick="handleReg()">INITIALIZE SIGNUP</button>
            <p style="font-size:10px; margin-top:15px; opacity:0.5;" onclick="toggleAuth('login')">Back to Authorization</p>
        </div>
    </div>
</div>

<header id="adminTrigger">VERBOSE</header>

<div id="dash" class="page">
    <div class="glass-card" style="background: linear-gradient(135deg, #0a0a0a, #000);">
        <h2 id="hiUser" style="margin:0;">Operator</h2>
        <div style="font-size:42px; font-weight:800; margin:10px 0; color:var(--neon);">PKR <span id="uBal">0.00</span></div>
        <div id="activeMining" style="display:none; border-top:1px solid #222; padding-top:15px; margin-top:10px;">
            <div style="display:flex; justify-content:space-between; font-size:10px; color:var(--success); font-weight:800;">
                <span>CLOUD MINING ACTIVE</span>
                <span id="timer">24:00:00</span>
            </div>
            <div style="height:3px; background:#111; margin-top:8px; border-radius:5px; overflow:hidden;">
                <div id="progressBar" style="width:0%; height:100%; background:var(--success);"></div>
            </div>
        </div>
    </div>
    
    <div class="glass-card" style="padding:15px;">
        <small style="letter-spacing:2px; opacity:0.5;">PROMOCODE REDEMPTION</small>
        <div style="display:flex; gap:10px; margin-top:10px;">
            <input id="promoInp" placeholder="Enter Code" style="margin:0; padding:12px;">
            <button class="btn-quantum" style="width:100px; padding:0; margin:0;" onclick="applyPromo()">REDEEM</button>
        </div>
    </div>

    <div id="plansContainer"></div>
</div>

<div id="history" class="page">
    <h3 style="letter-spacing:3px; padding-left:10px;">TRANSACTION HISTORY</h3>
    <div id="historyList"></div>
</div>

<div id="about" class="page">
    <div class="glass-card">
        <h3 style="color:var(--neon)">ABOUT VERBOSE</h3>
        <p style="font-size:12px; line-height:1.6; opacity:0.7;">We are a decentralized cloud mining agency based in Rawalpindi. We specialize in high-speed asset generation.</p>
    </div>
    <div class="glass-card">
        <h3 style="color:var(--success)">PRIVACY POLICY</h3>
        <p style="font-size:11px; opacity:0.5;">Identity logs are encrypted. All withdrawals are processed within 24 hours. Your security is our priority.</p>
    </div>
    <button class="btn-quantum" style="background:var(--error);" onclick="logout()">SECURE LOGOUT</button>
</div>

<div id="adminDash">
    <h3 style="color:var(--neon); letter-spacing:5px;">ROOT_TERMINAL</h3>
    <div class="glass-card">
        <small>NODE FACTORY</small>
        <input type="file" id="fileInp" style="display:none" accept="image/*">
        <div style="border:1px dashed #444; padding:20px; text-align:center; cursor:pointer; margin-top:10px; border-radius:15px;" onclick="document.getElementById('fileInp').click()">SELECT IMAGE</div>
        <input id="pName" class="ghost-input" style="margin-top:10px;" placeholder="Node Name">
        <input id="pPrice" class="ghost-input" type="number" placeholder="Cost">
        <input id="pDaily" class="ghost-input" type="number" placeholder="Daily Profit">
        <button class="btn-quantum" id="deployBtn" onclick="admDeploy()">DEPLOY NODE</button>
    </div>
    <div class="glass-card">
        <small>USER CONTROL</small>
        <input id="admU" class="ghost-input" placeholder="User Name">
        <input id="admB" class="ghost-input" type="number" placeholder="New Balance">
        <button class="btn-quantum" onclick="admUpdate()">INJECT ASSETS</button>
    </div>
    <button onclick="document.getElementById('adminDash').style.display='none'" class="btn-quantum" style="background:none; border:1px solid #444;">EXIT GHOST MODE</button>
</div>

<div id="fakePopup"></div>

<div class="nav" id="mainNav">
    <div class="nav-item active" onclick="tab('dash', this)">Dashboard</div>
    <div class="nav-item" onclick="tab('history', this)">History</div>
    <div class="nav-item" onclick="tab('about', this)">About</div>
</div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, set, update, onValue, get, push } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";
  import { getStorage, ref as sRef, uploadBytes, getDownloadURL } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-storage.js";

  const firebaseConfig = {
    apiKey: "AIzaSyBe5Q5jXpx3UvrHC9WOky9UWeDnP9SPfZI",
    authDomain: "verbose-6c008.firebaseapp.com",
    projectId: "verbose-6c008",
    storageBucket: "verbose-6c008.appspot.com",
    databaseURL: "https://verbose-6c008-default-rtdb.firebaseio.com",
    appId: "1:867100945312:web:315dfb48fb34496cee12c5"
  };

  const app = initializeApp(firebaseConfig);
  const db = getDatabase(app);
  const storage = getStorage(app);

  let currentUser = localStorage.getItem('v_user');

  // --- WELCOME VOICE ---
  function speak(text) {
    const msg = new SpeechSynthesisUtterance(text);
    msg.rate = 0.9;
    window.speechSynthesis.speak(msg);
  }

  // --- AUTH LOGIC ---
  window.toggleAuth = (type) => {
    document.getElementById('loginForm').classList.toggle('hidden', type === 'reg');
    document.getElementById('regForm').classList.toggle('hidden', type === 'login');
    document.getElementById('authTitle').innerText = type === 'reg' ? "REGISTER" : "AUTHORIZE";
  };

  window.handleReg = async () => {
    const u = document.getElementById('regUser').value.trim().toLowerCase();
    const p = document.getElementById('regPass').value;
    if(!u || !p) return alert("Missing fields!");
    const s = await get(ref(db, 'users/'+u));
    if(s.exists()) return alert("Username taken!");
    if(localStorage.getItem('v_device')) return alert("Single account limit reached!");

    await set(ref(db, 'users/'+u), { username: u, pass: p, balance: 0, dailyProfit: 0 });
    localStorage.setItem('v_device', 'true');
    alert("Identity Created! Please Login.");
    toggleAuth('login');
  };

  window.handleLogin = async () => {
    const u = document.getElementById('logUser').value.trim().toLowerCase();
    const p = document.getElementById('logPass').value;
    const s = await get(ref(db, 'users/'+u));
    if(s.exists() && s.val().pass === p) {
        localStorage.setItem('v_user', u);
        speak(`Welcome back, ${u}. Identity confirmed.`);
        location.reload();
    } else alert("Authorization Failed!");
  };

  window.logout = () => { localStorage.removeItem('v_user'); location.reload(); };

  // --- CORE SYSTEM INIT ---
  if(currentUser) {
    document.getElementById('authPage').style.display = 'none';
    document.getElementById('mainNav').style.display = 'flex';
    document.getElementById('dash').classList.add('active');

    onValue(ref(db, 'users/'+currentUser), (snap) => {
        if(snap.exists()){
            document.getElementById('uBal').innerText = snap.val().balance.toLocaleString();
            document.getElementById('hiUser').innerText = `Hi, ${currentUser}!`;
            if(snap.val().dailyProfit > 0) startMining(snap.val().dailyProfit);
        }
    });
  }

  // --- MINING SYSTEM ---
  function startMining(profit) {
    document.getElementById('activeMining').style.display = 'block';
    let start = localStorage.getItem('mine_start_'+currentUser) || Date.now();
    localStorage.setItem('mine_start_'+currentUser, start);

    setInterval(async () => {
        let elapsed = Math.floor((Date.now() - start) / 1000);
        let remain = (24*3600) - (elapsed % (24*3600));
        
        let h = Math.floor(remain/3600).toString().padStart(2,'0');
        let m = Math.floor((remain%3600)/60).toString().padStart(2,'0');
        let s = (remain%60).toString().padStart(2,'0');
        document.getElementById('timer').innerText = `${h}:${m}:${s}`;
        document.getElementById('progressBar').style.width = (( (24*3600)-remain )/(24*3600)*100) + "%";

        if(remain <= 1) {
            const uRef = ref(db, 'users/'+currentUser);
            const s = await get(uRef);
            await update(uRef, { balance: s.val().balance + profit });
            const hPush = push(ref(db, 'history/'+currentUser));
            set(hPush, { type: 'Profit', amount: profit, date: new Date().toLocaleString() });
        }
    }, 1000);
  }

  // --- FAKE SOCIAL PROOF ---
  const names = ["Zeeshan", "Ali", "Sana", "Waqas", "Fatima", "Umer", "Bilal", "Hamza"];
  setInterval(() => {
    const pop = document.getElementById('fakePopup');
    const name = names[Math.floor(Math.random()*names.length)];
    const amt = [5000, 15000, 3000, 50000][Math.floor(Math.random()*4)];
    pop.innerHTML = `<span style="color:var(--success)">●</span> ${name} from Rawalpindi just withdrew PKR ${amt.toLocaleString()}`;
    pop.style.display = 'block';
    setTimeout(() => { pop.style.display = 'none'; }, 4000);
  }, 10000);

  // --- ADMIN TOOLS ---
  let clicks = 0;
  document.getElementById('adminTrigger').onclick = () => {
    clicks++; if(clicks >= 7) {
        if(prompt("ROOT_KEY:") === "NAZIM786") document.getElementById('adminDash').style.display='block';
        clicks = 0;
    }
  };

  window.admUpdate = async () => {
    const u = document.getElementById('admU').value.toLowerCase();
    const b = document.getElementById('admB').value;
    await update(ref(db, 'users/'+u), { balance: parseFloat(b) });
    alert("Injected!");
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
