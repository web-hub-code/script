<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Omni-Trust Sentinel</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #000; --card: rgba(255,255,255,0.03); --border: rgba(255,255,255,0.08); --success: #00ff88; }
  * { box-sizing: border-box; transition: all 0.4s cubic-bezier(0.19, 1, 0.22, 1); font-family: 'Plus Jakarta Sans', sans-serif; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; }

  /* Trust Feed Ticker */
  .trust-ticker { background: rgba(0,255,136,0.1); padding: 8px 0; font-size: 9px; font-weight: 800; color: var(--success); overflow: hidden; white-space: nowrap; border-bottom: 1px solid var(--success); }
  .trust-ticker span { display: inline-block; animation: scroll 20s linear infinite; }
  @keyframes scroll { from { transform: translateX(100%); } to { transform: translateX(-100%); } }

  .page { max-width: 480px; margin: 0 auto; padding: 20px 20px 140px; display: none; }
  .page.active { display: block; animation: slideIn 0.5s ease; }
  @keyframes slideIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

  /* Premium Identity Card */
  .id-card { background: linear-gradient(135deg, #1a1a1a, #000); border: 1px solid var(--border); border-radius: 30px; padding: 25px; position: relative; overflow: hidden; margin-bottom: 25px; }
  .id-card::before { content: 'OFFICIAL'; position: absolute; top: 10px; right: -20px; background: var(--neon); color: #000; font-size: 8px; font-weight: 800; padding: 5px 30px; transform: rotate(45deg); }

  /* Chat System */
  #chatToggle { position: fixed; bottom: 110px; right: 25px; width: 65px; height: 65px; background: var(--neon); border-radius: 50%; display: flex; align-items: center; justify-content: center; z-index: 2000; box-shadow: 0 10px 30px rgba(0,247,255,0.5); cursor: pointer; color: #000; font-size: 24px; }
  #supportWindow { position: fixed; bottom: 100px; left: 20px; right: 20px; height: 400px; background: rgba(10,10,10,0.98); border-radius: 35px; border: 1px solid var(--border); display: none; flex-direction: column; z-index: 1999; backdrop-filter: blur(40px); }

  /* Common UI Elements */
  .glass-card { background: var(--card); border: 1px solid var(--border); padding: 20px; border-radius: 30px; margin-bottom: 20px; }
  input { width: 100%; padding: 18px; margin-top: 10px; border-radius: 20px; border: 1px solid var(--border); background: rgba(255,255,255,0.03); color: #fff; outline: none; }
  .btn-sentinel { width: 100%; padding: 20px; margin-top: 15px; border-radius: 22px; border: none; font-weight: 800; text-transform: uppercase; letter-spacing: 2px; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; cursor: pointer; }

  .nav { position: fixed; bottom: 30px; left: 20px; right: 20px; background: rgba(15,15,15,0.9); display: flex; justify-content: space-around; padding: 20px; border-radius: 35px; border: 1px solid var(--border); z-index: 1000; }
  .nav-item { font-size: 9px; opacity: 0.4; font-weight: 800; text-transform: uppercase; color: #fff; }
  .nav-item.active { opacity: 1; color: var(--neon); }
</style>
</head>
<body>

<div class="trust-ticker">
    <span>✓ User_Ali92 withdrew PKR 8,500 via EasyPaisa • ✓ New Node activated by Prince_Khan • ✓ Verbose Global Reserve: $1.2M Secured • ✓ Live Audit: OK</span>
</div>

<header id="adminTrigger" style="text-align:center; padding:40px 0 10px; letter-spacing:10px; font-weight:800;">VERBOSE</header>

<div id="dashboard" class="page active">
  <div class="id-card">
    <div style="font-size:9px; opacity:0.5; letter-spacing:3px;">INVESTOR IDENTITY</div>
    <div id="uNameDisplay" style="font-size:22px; font-weight:800; margin:10px 0; color:var(--neon);">NAZIM_PRIME</div>
    <div style="display:flex; justify-content:space-between; align-items:flex-end;">
        <div>
            <div style="font-size:8px; opacity:0.4;">ACCOUNT BALANCE</div>
            <div style="font-size:24px; font-weight:600;">PKR <span id="mainBal">0.00</span></div>
        </div>
        <div style="text-align:right;">
            <div style="font-size:8px; opacity:0.4;">MEMBER SINCE</div>
            <div style="font-size:10px;">MARCH 2026</div>
        </div>
    </div>
  </div>

  <div id="userPlansDisplay"></div>
</div>

<div id="chatToggle" onclick="toggleChat()">🤖</div>
<div id="supportWindow">
    <div style="padding:20px; border-bottom:1px solid var(--border); display:flex; justify-content:space-between;">
        <b>LIVE SUPPORT</b>
        <span onclick="toggleChat()" style="cursor:pointer;">×</span>
    </div>
    <div id="chatBox" style="flex:1; padding:15px; overflow-y:auto; font-size:13px; display:flex; flex-direction:column; gap:10px;">
        <div style="background:rgba(255,255,255,0.05); padding:10px; border-radius:15px; align-self:flex-start;">Welcome to Verbose Terminal. How can we help?</div>
    </div>
    <div style="padding:15px; display:flex; gap:10px;">
        <input id="chatInp" placeholder="Type here..." style="margin:0; padding:12px;">
        <button onclick="sendMsg()" style="background:var(--neon); border:none; border-radius:15px; padding:0 15px; font-weight:800;">></button>
    </div>
</div>

<div class="nav">
  <div class="nav-item active" onclick="tab('dashboard', this)">Asset</div>
  <div class="nav-item" onclick="alert('Withdraw System Online')">Withdraw</div>
  <div class="nav-item" onclick="alert('Company Details: Based in Rawalpindi')">About</div>
</div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, push, set, update, onValue } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

  const firebaseConfig = {
    apiKey: "AIzaSyBe5Q5jXpx3UvrHC9WOky9UWeDnP9SPfZI",
    authDomain: "verbose-6c008.firebaseapp.com",
    projectId: "verbose-6c008",
    databaseURL: "https://verbose-6c008-default-rtdb.firebaseio.com",
    appId: "1:867100945312:web:315dfb48fb34496cee12c5"
  };
  const app = initializeApp(firebaseConfig);
  const db = getDatabase(app);

  const currentUser = localStorage.getItem('v_user') || "User_New";
  document.getElementById('uNameDisplay').innerText = currentUser.toUpperCase();

  // --- CHAT WITH AUTO-REPLY ---
  window.toggleChat = () => {
    const s = document.getElementById('supportWindow');
    s.style.display = s.style.display === 'flex' ? 'none' : 'flex';
  };

  window.sendMsg = () => {
    const inp = document.getElementById('chatInp');
    if(!inp.value) return;
    
    // User Message
    const box = document.getElementById('chatBox');
    const uDiv = document.createElement('div');
    uDiv.style = "background:var(--accent); padding:10px; border-radius:15px; align-self:flex-end;";
    uDiv.innerText = inp.value;
    box.appendChild(uDiv);

    // Save to Firebase for Admin
    push(ref(db, 'support_chats/' + currentUser), {
        text: inp.value,
        sender: currentUser,
        time: new Date().toLocaleTimeString()
    });

    // Auto AI Reply
    setTimeout(() => {
        const aiDiv = document.createElement('div');
        aiDiv.style = "background:rgba(255,255,255,0.05); padding:10px; border-radius:15px; align-self:flex-start; color:var(--neon);";
        aiDiv.innerText = "System: Message received. Our administration team is reviewing your query.";
        box.appendChild(aiDiv);
        box.scrollTop = box.scrollHeight;
    }, 800);

    inp.value = '';
    box.scrollTop = box.scrollHeight;
  };

  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    if(el) {
        document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
        el.classList.add('active');
    }
  };
</script>
</body>
</html>
