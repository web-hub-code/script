<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
<title>VERBOSE — Quantum Nexus Fixed</title>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
<style>
  :root { --neon: #00f7ff; --accent: #7000ff; --bg: #000; --card: rgba(255,255,255,0.03); --border: rgba(255,255,255,0.08); --success: #00ff88; --error: #ff4646; }
  * { box-sizing: border-box; transition: 0.4s; font-family: 'Plus Jakarta Sans', sans-serif; }
  body { margin:0; background: var(--bg); color: #fff; overflow-x: hidden; }

  /* AUTH LAYER */
  #authPage { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: #000; z-index: 10000; display: flex; align-items: center; justify-content: center; padding: 20px; }
  .auth-box { width: 100%; max-width: 400px; background: var(--card); border: 1px solid var(--border); padding: 35px; border-radius: 40px; backdrop-filter: blur(20px); text-align: center; }

  .page { max-width: 480px; margin: 0 auto; padding: 20px 20px 140px; display: none; }
  .active { display: block !important; }

  input { width: 100%; padding: 18px; margin-top: 15px; border-radius: 20px; border: 1px solid var(--border); background: rgba(255,255,255,0.03); color: #fff; outline: none; }
  .btn-quantum { width: 100%; padding: 20px; border-radius: 25px; border: none; font-weight: 800; text-transform: uppercase; cursor: pointer; background: linear-gradient(135deg, var(--neon), var(--accent)); color: #fff; margin-top: 20px; }

  .nav { position: fixed; bottom: 30px; left: 15px; right: 15px; background: rgba(10,10,10,0.95); display: flex; justify-content: space-around; padding: 20px; border-radius: 40px; border: 1px solid var(--border); z-index: 1000; display: none; }
  .nav-item { font-size: 9px; opacity: 0.5; color: #fff; font-weight: 800; text-transform: uppercase; cursor: pointer; }
  .nav-item.active { opacity: 1; color: var(--neon); }
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
            <button class="btn-quantum" onclick="handleLogin()">ENTER TERMINAL</button>
            <p style="font-size:10px; margin-top:15px; opacity:0.5;" onclick="toggleAuth(false)">New Identity? Create One</p>
        </div>
        <div id="regForm" class="hidden">
            <input id="regUser" placeholder="Choose Username">
            <input id="regPass" type="password" placeholder="Create Password">
            <button class="btn-quantum" onclick="handleReg()">GENERATE IDENTITY</button>
            <p style="font-size:10px; margin-top:15px; opacity:0.5;" onclick="toggleAuth(true)">Back to Login</p>
        </div>
    </div>
</div>

<header id="adminTrigger" style="text-align:center; padding:40px; letter-spacing:10px; font-weight:800; text-shadow:0 0 10px var(--neon);">VERBOSE</header>

<div id="dash" class="page">
    <div style="background:var(--card); padding:30px; border-radius:35px; border:1px solid var(--border);">
        <h2 id="hiUser" style="margin:0;">Operator</h2>
        <div style="font-size:42px; font-weight:800; margin:10px 0;">PKR <span id="uBal">0.00</span></div>
        <div style="font-size:10px; color:var(--success);">IDENTITY VERIFIED & SECURE</div>
    </div>
    <div id="plansContainer" style="margin-top:20px;"></div>
</div>

<div class="nav" id="mainNav">
    <div class="nav-item active" onclick="tab('dash', this)">Dashboard</div>
    <div class="nav-item" onclick="logout()">Logout</div>
</div>

<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getDatabase, ref, set, get, onValue } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

  const firebaseConfig = {
    apiKey: "AIzaSyBe5Q5jXpx3UvrHC9WOky9UWeDnP9SPfZI",
    authDomain: "verbose-6c008.firebaseapp.com",
    projectId: "verbose-6c008",
    databaseURL: "https://verbose-6c008-default-rtdb.firebaseio.com",
    appId: "1:867100945312:web:315dfb48fb34496cee12c5"
  };

  const app = initializeApp(firebaseConfig);
  const db = getDatabase(app);

  // --- AUTH FUNCTIONS ---
  window.toggleAuth = (isLogin) => {
    document.getElementById('loginForm').classList.toggle('hidden', !isLogin);
    document.getElementById('regForm').classList.toggle('hidden', isLogin);
    document.getElementById('authTitle').innerText = isLogin ? "AUTHORIZE" : "REGISTER";
  };

  window.handleReg = async () => {
    const u = document.getElementById('regUser').value.trim().toLowerCase();
    const p = document.getElementById('regPass').value;
    if(!u || !p) return alert("Fill all fields!");
    
    const s = await get(ref(db, 'users/'+u));
    if(s.exists()) return alert("Username already taken!");

    await set(ref(db, 'users/'+u), { username: u, pass: p, balance: 0 });
    alert("Registration Successful! Now Login.");
    toggleAuth(true);
  };

  window.handleLogin = async () => {
    const u = document.getElementById('logUser').value.trim().toLowerCase();
    const p = document.getElementById('logPass').value;
    if(!u || !p) return alert("Enter credentials!");

    const s = await get(ref(db, 'users/'+u));
    if(s.exists() && s.val().pass === p) {
        localStorage.setItem('v_user', u);
        checkSession();
    } else {
        alert("Invalid Username or Password!");
    }
  };

  window.logout = () => {
    localStorage.removeItem('v_user');
    location.reload();
  };

  // --- SESSION CHECK ---
  function checkSession() {
    const user = localStorage.getItem('v_user');
    if(user) {
        document.getElementById('authPage').style.display = 'none';
        document.getElementById('mainNav').style.display = 'flex';
        document.getElementById('dash').classList.add('active');
        
        onValue(ref(db, 'users/'+user), (snap) => {
            if(snap.exists()) {
                document.getElementById('uBal').innerText = snap.val().balance.toLocaleString();
                document.getElementById('hiUser').innerText = `Hi, ${snap.val().username}!`;
            }
        });
    }
  }

  // Run on start
  checkSession();

  window.tab = (id, el) => {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
    el.classList.add('active');
  };
</script>
</body>
</html>
