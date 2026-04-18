<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime Solutions | Elite Lead OS</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #6366f1;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #f43f5e;
            --bg: #030712;
            --glass: rgba(255, 255, 255, 0.05);
        }

        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background: radial-gradient(circle at top right, #1e1b4b, #030712);
            color: #f8fafc;
            margin: 0;
            padding: 20px;
            min-height: 100vh;
        }

        /* Animated Header */
        header {
            background: var(--glass);
            backdrop-filter: blur(15px);
            border: 1px solid rgba(255,255,255,0.1);
            border-radius: 30px;
            padding: 40px;
            text-align: center;
            margin-bottom: 30px;
            border-bottom: 4px solid var(--warning);
        }

        header h1 { 
            font-size: 40px; font-weight: 800; letter-spacing: 5px; 
            background: linear-gradient(to right, #fff, var(--primary));
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
        }

        /* Live Status Badge */
        .live-badge {
            display: inline-block;
            background: rgba(16, 185, 129, 0.1);
            color: var(--success);
            padding: 5px 15px;
            border-radius: 50px;
            font-size: 12px;
            font-weight: 700;
            border: 1px solid var(--success);
            margin-bottom: 15px;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { opacity: 1; }
            50% { opacity: 0.5; }
            100% { opacity: 1; }
        }

        .main-dashboard {
            display: grid;
            grid-template-columns: 1.8fr 1fr;
            gap: 25px;
            max-width: 1500px;
            margin: 0 auto;
        }

        .script-card {
            background: rgba(15, 23, 42, 0.6);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255,255,255,0.05);
            border-radius: 35px;
            padding: 45px;
        }

        .step-box {
            margin-bottom: 50px;
            border-left: 5px solid var(--primary);
            padding-left: 25px;
            transition: 0.3s;
        }

        .step-box:hover { border-left-width: 10px; background: rgba(99, 102, 241, 0.05); border-radius: 0 20px 20px 0; }

        .step-num { font-size: 11px; font-weight: 800; text-transform: uppercase; color: var(--primary); display: block; margin-bottom: 10px; }
        .dialogue { font-size: 22px; line-height: 1.8; color: #e2e8f0; }
        .hl { color: var(--warning); font-weight: 800; }

        /* Modern Sidebar */
        .sidebar { display: flex; flex-direction: column; gap: 20px; }
        
        .tool-widget {
            background: var(--glass);
            border: 1px solid rgba(255,255,255,0.1);
            padding: 30px;
            border-radius: 25px;
        }

        .rebuttal-btn {
            background: #0f172a;
            border: 1px solid var(--danger);
            color: var(--danger);
            width: 100%;
            padding: 15px;
            border-radius: 12px;
            margin-bottom: 10px;
            cursor: pointer;
            text-align: left;
            font-weight: 600;
            transition: 0.3s;
        }

        .rebuttal-btn:hover { background: var(--danger); color: white; transform: translateX(10px); }

        .submit-lead {
            background: linear-gradient(135deg, var(--success), #059669);
            color: white;
            padding: 25px;
            border: none;
            border-radius: 20px;
            font-weight: 900;
            font-size: 20px;
            cursor: pointer;
            box-shadow: 0 10px 30px rgba(16, 185, 129, 0.3);
            text-transform: uppercase;
        }

        /* Floating Input Area */
        .inputs-area {
            display: flex; gap: 15px; margin-bottom: 25px;
        }
        .inputs-area input {
            background: #020617; border: 1px solid #1e293b; color: white;
            padding: 12px; border-radius: 10px; flex: 1; outline: none;
        }
        .inputs-area input:focus { border-color: var(--primary); }

        footer { text-align: center; padding: 40px; opacity: 0.5; font-size: 13px; }
    </style>
</head>
<body>

<div class="master-container">
    <header>
        <div class="live-badge">● LIVE SYSTEM ACTIVE: 2026 REBATE PROGRAM</div>
        <h1>PRIME SOLUTIONS</h1>
        <p style="opacity: 0.7; font-weight: 600;">USA Home Efficiency Script Engine</p>
    </header>

    <div class="inputs-area">
        <input type="text" id="agentN" placeholder="Agent Name..." onkeyup="sync()">
        <input type="text" id="custN" placeholder="Customer Name..." onkeyup="sync()">
        <input type="text" id="cityN" placeholder="City Name..." onkeyup="sync()">
    </div>

    <div class="main-dashboard">
        <div class="script-card">
            <div class="step-box">
                <span class="step-num">Phases 1-3: The Hook</span>
                <div class="dialogue" id="d1">
                    "Hi, this is <span class="hl ag">Agent</span> from <strong>Prime Solutions</strong>. How's it going in <span class="hl ci">City</span>? <br><br>
                    We're verifying local homeowners for the <span class="hl">2026 Energy Rebates</span>. Are you the <strong>homeowner</strong>? <br><br>
                    Great! Are we looking at <strong>5 to 10 windows</strong> or more?"
                </div>
            </div>

            <div class="step-box" style="border-left-color: var(--warning);">
                <span class="step-num">Phases 4-6: Rebate Data</span>
                <div class="dialogue" id="d2">
                    "To check the tax credits for your area, what is your <strong>ZIP code</strong>? <br><br>
                    And for the record, what is your <strong>Date of Birth</strong>? This ensures you get the <span class="hl">Senior or Military discounts</span> we have on file."
                </div>
            </div>

            <div class="step-box" style="border-left-color: var(--success);">
                <span class="step-num">Phases 7-12: The Closing</span>
                <div class="dialogue" id="d3">
                    "For our <strong>0% interest plans</strong>, what range is your credit score? <br><br>
                    I'll have the specialist visit for a <span class="hl">Free 12-Month Price-Locked Estimate</span>. Do mornings or evenings work best for you and your spouse, <span class="hl cu">Customer</span>?"
                </div>
            </div>
        </div>

        <div class="sidebar">
            <div class="tool-widget">
                <h4 style="margin:0 0 20px 0; color: var(--success); font-size: 14px;">INSTANT REBUTTALS</h4>
                <button class="rebuttal-btn" onclick="alert('Jawab: Credits vary by county, ZIP ensures we find the exact ones for your street.')">"Why do you need my ZIP?"</button>
                <button class="rebuttal-btn" onclick="alert('Jawab: The 1-year price lock is a legal document, we need both owners to receive it.')">"Why both spouses?"</button>
                <button class="rebuttal-btn" onclick="alert('Jawab: We offer 0% interest with no-out-of-pocket costs today.')">"I can't afford it now."</button>
            </div>

            <div class="tool-widget" style="background: rgba(99, 102, 241, 0.05);">
                <h4 style="color: var(--primary); font-size: 12px;">AGENT PERFORMANCE</h4>
                <p style="font-size: 13px; color: #94a3b8;">Current Rebate: <span style="color:white;">$1,500 - $4,000</span></p>
                <p style="font-size: 13px; color: #94a3b8;">Program: <span style="color:white;">2026 Federal Efficiency</span></p>
            </div>

            <button class="submit-lead" onclick="alert('Lead Locked Successfully!')">Lock Final Lead</button>
        </div>
    </div>

    <footer>
        PRIME SOLUTIONS AGENCY | PREMIUM BRANDING & SCRIPT SYSTEMS © 2026<br>
        <a href="https://web-hub-code.github.io/PRIMESOLUTIONS/" style="color:var(--primary); text-decoration:none;">Agency Portfolio</a>
    </footer>
</div>

<script>
    function sync() {
        let ag = document.getElementById('agentN').value || "Agent";
        let cu = document.getElementById('custN').value || "Customer";
        let ci = document.getElementById('cityN').value || "City";

        document.querySelectorAll('.ag').forEach(e => e.innerText = ag);
        document.querySelectorAll('.cu').forEach(e => e.innerText = cu);
        document.querySelectorAll('.ci').forEach(e => e.innerText = ci);
    }
</script>

</body>
</html>
