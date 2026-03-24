<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Quantum Ecosystem</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #000; --card: rgba(255,255,255,0.03); --border: rgba(255,255,255,0.08); --success: #00ff88; --error: #ff4646; --gold: #ffcc00; }
  * { box-sizing: border-box; transition: 0.4s cubic-bezier(0.1, 1, 0.1, 1); font-family: 'Plus Jakarta Sans', sans-serif; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; }

  /* GHOST ADMIN LAYER */
  #adminDash { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: #000; z-index: 99999; padding: 30px 20px; overflow-y: auto; }
  .ghost-input { background: rgba(255,255,255,0.02); border: 1px solid #222; color: var(--neon); padding: 15px; border-radius: 15px; width: 100%; margin-bottom: 10px; font-size: 12px; outline: none; }
  
  /* UI COMPONENTS */
  header { text-align: center; padding: 45px 20px 10px; font-size: 24px; font-weight: 800; letter-spacing: 12px; text-shadow: 0 0 20px var(--neon); cursor: pointer; }
  .page { max-width: 480px; margin: 0 auto; padding: 20px 20px 140px; display: none; }
  .active { display: block; animation: slideUp 0.5s ease; }
  @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

  .glass-card { background: var(--card); border: 1px solid var(--border); border-radius: 30px; padding: 25px; backdrop-filter: blur(40px); margin-bottom: 20px; position: relative; }
  .node-card { background: var(--card); border: 1px solid var(--border); border-radius: 35px; overflow: hidden; margin-bottom: 25px; position: relative; }
  .node-img { width: 100%; height: 180px; object-fit: cover; }
  .offer-tag { position: absolute; top: 15px; left: 15px; background: var(--gold); color: #000; font-size: 9px; font-weight: 800; padding: 5px 12px; border-radius: 20px; z-index: 10; }

  /* BUTTONS */
  .btn-quantum { width: 100%; padding: 20px; border-radius: 25px; border: none; font-weight: 800; text-transform: uppercase; cursor: pointer; letter-spacing: 2.5px; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; box-shadow: 0 10px 30px rgba(112,0,255,0.3); }

  /* FAKE POPUP */
  #fakePopup { position: fixed; bottom: 110px; left: 20px; background: rgba(20,20,20,0.95); border: 1px solid var(--neon); padding: 12px 20px; border-radius: 20px; display: none; align-items: center; gap: 12px; z-index: 9000; backdrop-filter: blur(20px); transform: translateY(100px); transition: 0.5s; }

  /* NAVIGATION */
  .nav { position: fixed; bottom: 30px; left: 15px; right: 15px; background: rgba(10,10,10,0.9); display: flex; justify-content: space-around; padding: 22px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 9px; opacity: 0.4; color: #fff; font-weight: 800; text-transform: uppercase; cursor: pointer; }
  .nav-item.active { opacity: 1; color: var(--neon); }
</style>
</head>
<body>

<header id="adminTrigger">VERBOSE</header>

<div id="dash" class="page active">
  <div style="padding: 10px 20px;">
    <h2 id="hiUser" style="margin:0;">Hi, Operator!</h2>
    <p id="timeGreeting" style="font-size:10px; opacity:0.5; letter-spacing:1px;">ACCESS SECURED</p>
  </div>

  <div class="glass-card" style="background: linear-gradient(135deg, #111, #000);">
    <div style="font-size:10px; opacity:0.5; letter-spacing:2px;">WALLET ASSETS</div>
    <div style="font-size:42px; font-weight:800; margin:10px 0;">PKR <span id="uBal">0.00</span></div>
    <div id="activeMining" style="display:none; border-top: 1px solid #222; padding-top:15px; margin-top:15px;">
        <div style="display:flex; justify-content:space-between; font-size:11px; color:var(--success); font-weight:800;">
            <span>MINING ACTIVE</span>
            <span id="timer">24:00:00</span>
        </div>
        <div style="height:3px; background:#222; margin-top:8px; border-radius:10px; overflow:hidden;">
            <div id="progressBar" style="width:0%; height:100%; background:var(--success);"></div>
        </div>
    </div>
  </div>

  <div id="plansContainer"></div>
</div>

<div id="history" class="page">
    <h3 style="letter-spacing:3px; padding-left:10px;">TRANSACTION LEDGER</h3>
    <div id="historyList"></div>
</div>

<div id="adminDash">
    <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:20px;">
        <h3 style="color:var(--neon); letter-spacing:4px;">GHOST_ROOT</h3>
        <button onclick="document.getElementById('adminDash').style.display='none'" style="background:none; border:none; color:var(--error);">[EXIT]</button>
    </div>
    
    <div class="glass-card">
        <small>NODE FACTORY (UPLOAD IMAGE)</small>
        <input type="file" id="fileInp" style="display:none" accept="image/*">
        <div style="border:1px dashed #444; padding:20px; text-align:center; cursor:pointer; margin-top:10px; border-radius:15px;" onclick="document.getElementById('fileInp').click()">SELECT MACHINE IMAGE</div>
        <input id="pName" class="ghost-input" style="margin-top:15px;" placeholder="Node Name">
        <input id="pPrice" class="ghost-input" type="number" placeholder="Cost">
        <input id="pDaily" class="ghost-input" type="number" placeholder="Daily Profit">
        <input id="pDays" class="ghost-input" type="number" placeholder="Duration">
        <button class="btn-quantum" id="deployBtn" onclick="admDeploy()">DEPLOY NODE</button>
    </div>

    <div class="glass-card">
        <small>USER OVERRIDE</small>
        <input id="admU" class="ghost-input" placeholder="Username">
        <input id="admB" class="ghost-input" type="number" placeholder="Set Balance">
        <button class="btn-quantum" style="background:var(--success);" onclick="admUserUpdate()">INJECT DATA</button>
    </div>
</div>

<div id="fakePopup">
    <div style="width:8px; height:8px; background:var(--success); border-radius:50%;"></div>
    <div id="popupText" style="font-size:10px; font-weight:800;"></div>
</div>

<div class="nav">
  <div class="nav-item active" onclick="tab('dash', this)">Nodes</div>
  <div class="nav-item" onclick="tab('history', this)">History</div>
  <div class="nav-item" onclick="logout()">Logout</div>
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

  const user = localStorage.getItem('v_user') || "Guest";

  // --- AUTO LOGOUT (10 MIN) ---
  let idleTime = 0;
  document.onmousemove = () => idleTime = 0;
  setInterval(() => {
    idleTime++;
    if(idleTime > 10) logout(); // 10 minutes
  }, 60000);

  window.logout = () => { localStorage.removeItem('v_user'); location.reload(); };

  // --- ADMIN STEALTH TRIGGER ---
  let clicks = 0;
  document.getElementById('adminTrigger').onclick = () => {
    clicks++; if(clicks >= 7) {
        if(prompt("ROOT_KEY:") === "NAZIM786") document.getElementById('adminDash').style.display='block';
        clicks = 0;
    }
  };

  // --- FAKE SOCIAL PROOF ---
  const names = ["Zeeshan", "Ali", "Sana", "Waqas", "Fatima", "Umer", "Bilal"];
  setInterval(() => {
    const pop = document.getElementById('fakePopup');
    const txt = document.getElementById('popupText');
    const name = names[Math.floor(Math.random()*names.length)];
    const amt = [5000, 15000, 500, 25000][Math.floor(Math.random()*4)];
    txt.innerHTML = `${name} just <span style="color:var(--success)">withdrew</span> PKR ${amt.toLocaleString()}`;
    pop.style.display = 'flex';
    setTimeout(() => pop.style.transform = 'translateY(0)', 100);
    setTimeout(() => { pop.style.transform = 'translateY(100px)'; setTimeout(()=>pop.style.display='none', 500); }, 4000);
  }, 12000);

  // --- MINING & PROFIT LOGIC ---
  function initMining(profit) {
    if(profit <= 0) return;
    document.getElementById('activeMining').style.display = 'block';
    let start = localStorage.getItem('mine_'+user) || Date.now();
    localStorage.setItem('mine_'+user, start);

    setInterval(async () => {
        let elapsed = Math.floor((Date.now() - start) / 1000);
        let remain = (24*3600) - (elapsed % (24*3600));
        
        let h = Math.floor(remain/3600).toString().padStart(2,'0');
        let m = Math.floor((remain%3600)/60).toString().padStart(2,'0');
        let s = (remain%60).toString().padStart(2,'0');
        document.getElementById('timer').innerText = `${h}:${m}:${s}`;
        document.getElementById('progressBar').style.width = (( (24*3600)-remain )/(24*3600)*100) + "%";

        if(remain <= 1) {
            const s = await get(ref(db, 'users/'+user));
            await update(ref(db, 'users/'+user), { balance: (s.val().balance||0) + profit });
            // Add to history
            const hRef = push(ref(db, 'history/'+user));
            set(hRef, { type: 'Mining Profit', amount: profit, date: new Date().toLocaleString() });
        }
    }, 1000);
  }

  // --- LOAD USER DATA ---
  onValue(ref(db, 'users/'+user), (s) => {
    if(s.exists()){
        document.getElementById('uBal').innerText = s.val().balance.toLocaleString();
        document.getElementById('hiUser').innerText = `Hi, ${user}!`;
        if(s.val().dailyProfit) initMining(s.val().dailyProfit);
    }
  });

  // --- ADMIN: DEPLOY NODE ---
  window.admDeploy = async () => {
    const file = document.getElementById('fileInp').files[0];
    const name = document.getElementById('pName').value;
    const price = document.getElementById('pPrice').value;
    if(!file || !name) return alert("Missing Data!");
    
    document.getElementById('deployBtn').innerText = "UPLOADING...";
    const sRefObj = sRef(storage, 'nodes/' + Date.now() + "_" + file.name);
    await uploadBytes(sRefObj, file);
    const url = await getDownloadURL(sRefObj);

    await set(ref(db, 'plans/'+name), {
        name, img: url, cost: parseFloat(price), 
        profit: parseFloat(document.getElementById('pDaily').value),
        days: document.getElementById('pDays').value
    });
    alert("Deployed!"); location.reload();
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
