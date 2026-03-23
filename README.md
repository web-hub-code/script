<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <title>VERBOSE - God Mode</title>
    <style>
        :root { --neon:#00f7ff; --accent:#ff5cff; --dark:#070707; }
        body { margin:0; font-family:Inter, sans-serif; background:var(--dark); color:#fff; overflow-x:hidden; }
        header { text-align:center; padding:24px; font-size:28px; font-weight:800; background:linear-gradient(90deg,var(--neon),var(--accent)); -webkit-background-clip:text; -webkit-text-fill-color:transparent; cursor:pointer; }
        .login-box, .page { max-width:430px; margin:18px auto; background:rgba(255,255,255,0.02); padding:18px; border-radius:12px; border:1px solid rgba(0,255,240,0.1); }
        input, button, select { width:100%; padding:10px; margin-top:10px; border-radius:8px; border:1px solid rgba(0,255,240,0.2); background:transparent; color:#fff; }
        button { background:linear-gradient(90deg,var(--neon),var(--accent)); color:#000; font-weight:700; cursor:pointer; border:none; }
        .hidden { display:none; }
        .nav { position:fixed; bottom:0; left:0; right:0; background:rgba(15,17,20,0.95); display:flex; justify-content:space-around; padding:12px; border-top:1px solid rgba(0,255,240,0.1); }
        .nav div { text-align:center; cursor:pointer; font-size:12px; }
        .user-box { background:rgba(0,255,240,0.05); padding:14px; border-radius:12px; margin-bottom:12px; border:1px solid rgba(0,255,240,0.1); }
        .alert-box { background:rgba(255,92,255,0.05); padding:12px; border-radius:10px; margin-bottom:12px; border:1px solid rgba(255,92,255,0.2); color:var(--accent); }
    </style>
</head>
<body>

<header id="mainHeader">VERBOSE</header>

<div id="loginPage" class="login-box">
    <h2>Login / Signup</h2>
    <input id="user" placeholder="Username" />
    <input id="pass" placeholder="Password" type="password" />
    <button onclick="handleAuth()">Access Portal</button>
    <p style="font-size:11px; margin-top:10px; opacity:0.6;">Tip: Sirf apna username yaad rakhein, hum baki sambhal len gay.</p>
</div>

<div id="dashboard" class="page hidden">
    <div class="user-box">
        <div id="dashUser" style="font-weight:800; font-size:18px;">---</div>
        <div style="font-size:14px; margin-top:5px;">Balance: Rs <span id="dashBalance">0</span></div>
        <div style="font-size:12px; color:var(--neon);">Daily Profit: Rs <span id="dashDaily">0</span></div>
    </div>
    <button onclick="logout()">Logout</button>
</div>

<div id="godMode" class="page hidden" style="border: 2px dashed var(--neon);">
    <h2 style="color:var(--neon); text-align:center;">⚡ GOD MODE ⚡</h2>
    <div class="user-box">
        <input id="adminSearchUser" placeholder="Search Username">
        <button onclick="fetchUserForAdmin()">Fetch User</button>
        <div id="userDataEditor" class="hidden">
            <input id="editBalance" type="number" placeholder="New Balance">
            <input id="editDaily" type="number" placeholder="New Daily">
            <button onclick="saveUserChanges()" style="background:var(--accent);">Update User</button>
        </div>
    </div>
    <div class="alert-box">
        <h3>Pending Deposits</h3>
        <div id="pendingList" style="font-size:12px;">Checking for requests...</div>
    </div>
    <button onclick="showPage('dashboard')">Exit God Mode</button>
</div>

<div id="bottomNav" class="nav hidden">
    <div onclick="showPage('dashboard')">🏠<br>Home</div>
    <div onclick="alert('Plans working in background...')">📦<br>Plans</div>
    <div onclick="showPage('godMode')" id="adminBtn" class="hidden">⚡<br>Admin</div>
</div>

<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
    import { getDatabase, ref, set, get, update, onValue } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-database.js";

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

    // --- AUTH LOGIC ---
    window.handleAuth = async () => {
        const u = document.getElementById('user').value.trim();
        const p = document.getElementById('pass').value.trim();
        if(!u || !p) return alert("Fill details!");

        const userRef = ref(db, 'users/' + u);
        const snap = await get(userRef);

        if(snap.exists()) {
            if(snap.val().password === p) loginSuccess(u, snap.val());
            else alert("Wrong password!");
        } else {
            const newData = { username:u, password:p, balance:0, dailyProfit:0 };
            await set(userRef, newData);
            loginSuccess(u, newData);
        }
    };

    function loginSuccess(u, data) {
        localStorage.setItem('v_user', u);
        document.getElementById('dashUser').innerText = u;
        document.getElementById('dashBalance').innerText = data.balance;
        document.getElementById('dashDaily').innerText = data.dailyProfit;
        showPage('dashboard');
        document.getElementById('loginPage').classList.add('hidden');
        document.getElementById('bottomNav').classList.remove('hidden');
        listenForDeposits();
    }

    // --- GOD MODE CORE ---
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

    window.fetchUserForAdmin = async () => {
        const u = document.getElementById('adminSearchUser').value;
        const snap = await get(ref(db, 'users/' + u));
        if(snap.exists()) {
            document.getElementById('editBalance').value = snap.val().balance;
            document.getElementById('editDaily').value = snap.val().dailyProfit;
            document.getElementById('userDataEditor').classList.remove('hidden');
        }
    };

    window.saveUserChanges = async () => {
        const u = document.getElementById('adminSearchUser').value;
        await update(ref(db, 'users/' + u), {
            balance: parseFloat(document.getElementById('editBalance').value),
            dailyProfit: parseFloat(document.getElementById('editDaily').value)
        });
        alert("Updated!");
    };

    function listenForDeposits() {
        onValue(ref(db, 'deposits'), (snap) => {
            const list = document.getElementById('pendingList');
            list.innerHTML = "";
            const data = snap.val();
            for(let id in data) {
                if(data[id].status === "pending") {
                    list.innerHTML += `<div>${data[id].user}: Rs ${data[id].amount} 
                    <button onclick="approve('${id}','${data[id].user}',${data[id].amount})">Approve</button></div>`;
                }
            }
        });
    }

    window.showPage = (id) => {
        document.querySelectorAll('.page').forEach(p => p.classList.add('hidden'));
        document.getElementById(id).classList.remove('hidden');
    };

    window.logout = () => { localStorage.clear(); location.reload(); };

</script>
</body>
</html>
