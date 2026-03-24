<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>VERBOSE — Prime Solutions Pro</title>
<style>
  :root{ --neon:#00f7ff; --accent:#ff5cff; --dark:#050505; --glass:rgba(255,255,255,0.05); }
  *{box-sizing:border-box; transition: 0.3s; -webkit-tap-highlight-color: transparent;}
  body { margin:0; font-family:'Poppins', sans-serif; background:var(--dark); color:#fff; overflow-x:hidden; }
  header { text-align:center; padding:35px 20px; font-size:35px; font-weight:900; background:linear-gradient(90deg,var(--neon),var(--accent)); -webkit-background-clip:text; -webkit-text-fill-color:transparent; cursor:pointer; text-transform:uppercase; letter-spacing:5px; }
  
  .page { max-width:420px; margin:15px auto 100px; background:var(--glass); padding:25px; border-radius:30px; border:1px solid rgba(0,255,240,0.1); backdrop-filter: blur(20px); }
  .user-card { background:linear-gradient(135deg, rgba(0,247,255,0.12), rgba(255,92,255,0.06)); padding:20px; border-radius:22px; margin-bottom:15px; border-left:5px solid var(--neon); }
  
  /* WhatsApp Floating Button */
  .whatsapp-btn { position: fixed; bottom: 90px; right: 20px; width: 60px; height: 60px; background: #25d366; border-radius: 50%; display: flex; justify-content: center; align-items: center; box-shadow: 0 4px 15px rgba(0,0,0,0.4); z-index: 9999; cursor: pointer; text-decoration: none; }
  .whatsapp-btn svg { width: 35px; fill: white; }

  /* Payout Notification Pop-up */
  #payoutNotice { position: fixed; top: 20px; left: 50%; transform: translateX(-50%); background: rgba(0,0,0,0.9); border: 1px solid var(--neon); padding: 10px 20px; border-radius: 50px; font-size: 11px; z-index: 10000; display: none; white-space: nowrap; animation: slideDown 0.5s ease; }
  @keyframes slideDown { from { top: -50px; } to { top: 20px; } }

  input, select { width:100%; padding:15px; margin-top:12px; border-radius:15px; border:1px solid rgba(255,255,255,0.1); background:rgba(0,0,0,0.6); color:#fff; font-size:14px; outline:none; }
  button { width:100%; padding:16px; margin-top:18px; border-radius:15px; border:none; background:linear-gradient(90deg,var(--neon),var(--accent)); color:#000; font-weight:800; cursor:pointer; }
  
  .nav { position:fixed; bottom:0; left:0; right:0; background:rgba(5,5,5,0.95); display:flex; justify-content:space-around; padding:20px; z-index:1000; }
  .nav-item { text-align:center; font-size:10px; cursor:pointer; opacity:0.5; color:#fff; flex:1; }
  .nav-item.active { opacity:1; color:var(--neon); }
  .status-tag { font-size:10px; padding:3px 10px; border-radius:20px; float:right; font-weight:bold; }
  .pending { background: #ffa500; color: #000; } .approved { background: #00ff88; color: #000; }
  .hidden { display:none; }
</style>
</head>
<body>

<div id="payoutNotice">User <b>Asad</b> just withdrew <b>Rs 4,500</b></div>

<header id="mainHeader">VERBOSE</header>

<a href="https://chat.whatsapp.com/EbfTbr66JQLFEmjnxrReE3" target="_blank" class="whatsapp-btn">
  <svg viewBox="0 0 448 512"><path d="M380.9 97.1C339 55.1 283.2 32 223.9 32c-122.4 0-222 99.6-222 222 0 39.1 10.2 77.3 29.6 111L0 480l117.7-30.9c32.4 17.7 68.9 27 106.1 27h.1c122.3 0 224.1-99.6 224.1-222 0-59.3-25.2-115-67.1-157zm-157 341.6c-33.2 0-65.7-8.9-94-25.7l-6.7-4-69.8 18.3L72 359.2l-4.4-7c-18.5-29.4-28.2-63.3-28.2-98.2 0-101.7 82.8-184.5 184.6-184.5 49.3 0 95.6 19.2 130.4 54.1 34.8 34.9 56.2 81.2 56.1 130.5 0 101.8-84.9 184.6-186.6 184.6zm101.2-138.2c-5.5-2.8-32.8-16.2-37.9-18-5.1-1.9-8.8-2.8-12.5 2.8-3.7 5.6-14.3 18-17.6 21.8-3.2 3.7-6.5 4.2-12 1.4-5.5-2.8-23.2-8.5-44.2-27.2-16.4-14.6-27.4-32.7-30.7-38.2-3.2-5.5-.4-8.5 2.4-11.2 2.5-2.6 5.5-6.5 8.3-9.8 2.8-3.2 3.7-5.5 5.5-9.3 1.9-3.7.9-6.9-.5-9.7-1.4-2.8-12.5-30.1-17.1-41.2-4.5-10.8-9.1-9.3-12.5-9.5-3.2-.2-6.9-.2-10.6-.2-3.7 0-9.7 1.4-14.8 6.9-5.1 5.6-19.4 19-19.4 46.3 0 27.3 19.9 53.7 22.6 57.4 2.8 3.7 39.1 59.7 94.8 83.8 13.2 5.8 23.5 9.2 31.5 11.8 13.3 4.2 25.4 3.6 35 2.2 10.7-1.5 32.8-13.4 37.4-26.4 4.6-13 4.6-24.1 3.2-26.4-1.3-2.5-5-3.9-10.5-6.6z"/></svg>
</a>

<div id="loginPage" class="page">
  <h2 style="text-align:center;">Elite Access</h2>
  <input id="u_name" type="text" placeholder="Username">
  <input id="u_pass" type="password" placeholder="Password">
  <button id="entryBtn">SIGN IN / JOIN</button>
</div>

<div id="dashboard" class="page hidden">
  <div class="user-card">
    <div id="welcomeMsg" style="font-size:14px; opacity:0.7;">Welcome</div>
    <div style="font-size:35px; font-weight:900; margin:10px 0;">Rs <span id="mainBal">0.00</span></div>
    <div style="font-size:11px; color:var(--neon); font-weight:bold;">WALLET BALANCE</div>
  </div>

  <div class="user-card" style="border-left-color: var(--accent); background:rgba(255,92,255,0.05);">
    <div style="font-size:12px;"><b>3-Tier Referral System</b></div>
    <div style="font-size:10px; opacity:0.7;">L1: 10% | L2: 5% | L3: 2% commission.</div>
  </div>

  <div class="user-card" style="border-left-color:#fff;">
    <p style="font-size:11px; margin-bottom:5px;">Redeem Code:</p>
    <div style="display:flex; gap:8px;">
      <input id="promoInput" placeholder="Enter Code" style="margin:0; flex:2;">
      <button onclick="applyPromo()" style="margin:0; flex:1; padding:12px; font-size:11px;">APPLY</button>
    </div>
  </div>
  <h3 style="font-size:16px; margin:25px 0 12px 0;">History</h3>
  <div id="historyList"></div>
</div>

<div id="walletPage" class="page hidden">
  <div class="user-card" style="font-size:13px; background:rgba(0,0,0,0.5);">
    <b>JazzCash/SadaPay:</b> <span style="color:var(--neon)">03705519562</span><br>
    <b>EasyPaisa:</b> <span style="color:var(--neon)">03379827882</span><br>
    <small>Beneficiary: Muhammad Nazim</small>
  </div>
  <input id="d_amount" type="number" placeholder="Deposit Amount">
  <input id="d_tid" placeholder="TID Number">
  <input id="d_proof" placeholder="Proof (TID screenshot link)">
  <button onclick="submitReq('Deposit')">CONFIRM DEPOSIT</button>
  <hr style="opacity:0.1; margin:30px 0;">
  <input id="w_amount" type="number" placeholder="Withdraw Amount">
  <input id="w_phone" placeholder="Account Number">
  <button onclick="submitReq('Withdraw')" style="background:var(--accent)">REQUEST PAYOUT</button>
</div>

<div id="bottomNav" class="nav hidden">
  <div class="nav-item active" onclick="tab('dashboard', this)">🏠<br>Home</div>
  <div class="nav-item" onclick="tab('walletPage', this)">💰<br>Wallet</div>
  <div class="nav-item" onclick="doLogout()">🚪<br>Logout</div>
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

  // AUTH
  document.getElementById('entryBtn').onclick = async () => {
    const u = document.getElementById('u_name').value.trim().toLowerCase();
    const p = document.getElementById('u_pass').value.trim();
    if(!u || !p) return alert("Fill all!");
    const userRef = ref(db, 'users/' + u);
    const snap = await get(userRef);
    if(snap.exists()) {
      if(snap.val().password === p) start(u); else alert("Wrong!");
    } else {
      await set(userRef, { username:u, password:p, balance:0 });
      start(u);
    }
  };

  function start(u) {
    localStorage.setItem('v_user', u);
    document.getElementById('welcomeMsg').innerText = "Hello, " + u;
    document.getElementById('loginPage').classList.add('hidden');
    document.getElementById('dashboard').classList.remove('hidden');
    document.getElementById('bottomNav').classList.remove('hidden');
    onValue(ref(db, 'users/' + u), s => {
      document.getElementById('mainBal').innerText = parseFloat(s.val().balance).toFixed(2);
    });
    loadHistory(u);
    showLivePayouts();
  }

  // LIVE PAYOUTS MOCK
  function showLivePayouts() {
    const names = ["Zeeshan", "Mehak", "Hamza", "Ayesha", "Usman", "Rida"];
    setInterval(() => {
      const name = names[Math.floor(Math.random()*names.length)];
      const amt = Math.floor(Math.random()*10000) + 1000;
      const el = document.getElementById('payoutNotice');
      el.innerHTML = `User <b>${name}</b> just withdrew <b>Rs ${amt.toLocaleString()}</b>`;
      el.style.display = 'block';
      setTimeout(() => el.style.display = 'none', 4000);
    }, 15000);
  }

  // HISTORY & FINANCE
  function loadHistory(u) {
    onValue(ref(db, 'history/' + u), s => {
      const cont = document.getElementById('historyList');
      cont.innerHTML = "";
      const data = s.val();
      for(let id in data) {
        cont.innerHTML += `<div class="user-card" style="font-size:12px;">
          <span class="status-tag ${data[id].status}">${data[id].status}</span>
          <b>${data[id].type}</b>: Rs ${data[id].amount}
        </div>`;
      }
    });
  }

  window.submitReq = (type) => {
    const u = localStorage.getItem('v_user');
    const amt = (type=='Deposit')? document.getElementById('d_amount').value : document.getElementById('w_amount').value;
    if(!amt) return alert("Enter amount!");
    const key = Date.now();
    const r = { user:u, amount:amt, type:type, status:'pending', time:new Date().toLocaleString() };
    set(ref(db, 'requests/' + key), r);
    set(ref(db, 'history/' + u + '/' + key), r);
    alert("Sent!");
  };

  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.add('hidden'));
    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
    document.getElementById(id).classList.remove('hidden');
    if(el) el.classList.add('active');
  };
  window.doLogout = () => { localStorage.clear(); location.reload(); };
</script>
</body>
</html>
