import os

# Define the HTML content for the Premium Master Website
html_content = """
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime Solutions | Elite Master Lead OS</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&family=JetBrains+Mono:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #6366f1;
            --primary-glow: rgba(99, 102, 241, 0.4);
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #f43f5e;
            --bg: #030712;
            --glass: rgba(255, 255, 255, 0.03);
            --glass-border: rgba(255, 255, 255, 0.08);
            --card-bg: #0f172a;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background: radial-gradient(circle at top right, #1e1b4b, #030712);
            color: #f8fafc;
            min-height: 100vh;
            padding: 20px;
            overflow-x: hidden;
        }

        /* Premium Animations */
        @keyframes fadeIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        @keyframes glow { 0% { box-shadow: 0 0 5px var(--primary-glow); } 50% { box-shadow: 0 0 20px var(--primary-glow); } 100% { box-shadow: 0 0 5px var(--primary-glow); } }

        .master-container {
            max-width: 1550px;
            margin: 0 auto;
            animation: fadeIn 0.8s ease-out;
        }

        /* Glass Header */
        header {
            background: var(--glass);
            backdrop-filter: blur(20px);
            border: 1px solid var(--glass-border);
            border-radius: 30px;
            padding: 40px;
            text-align: center;
            margin-bottom: 25px;
            position: relative;
            overflow: hidden;
        }

        header::after {
            content: '';
            position: absolute;
            top: 0; left: -100%; width: 50%; height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.05), transparent);
            transition: 0.5s;
        }

        header:hover::after { left: 150%; transition: 0.8s; }

        header h1 { 
            font-size: 48px; font-weight: 800; letter-spacing: 6px; 
            background: linear-gradient(to right, #fff, var(--primary));
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
            text-transform: uppercase;
        }

        .agency-badge {
            background: var(--warning); color: #000;
            padding: 5px 15px; border-radius: 50px;
            font-size: 11px; font-weight: 800; letter-spacing: 2px;
            display: inline-block; margin-top: 10px;
        }

        .portal-links { margin-top: 25px; display: flex; justify-content: center; gap: 15px; }
        .portal-links a {
            background: rgba(255,255,255,0.05); color: #fff; text-decoration: none;
            padding: 12px 25px; border-radius: 15px; font-weight: 600; font-size: 13px;
            border: 1px solid var(--glass-border); transition: 0.3s;
        }
        .portal-links a:hover { background: var(--primary); transform: translateY(-3px); }

        /* Control Center Variables */
        .control-bar {
            background: var(--glass);
            backdrop-filter: blur(10px);
            border: 1px solid var(--glass-border);
            padding: 25px 40px;
            border-radius: 25px;
            display: flex;
            gap: 20px;
            margin-bottom: 25px;
        }

        .control-bar input {
            background: #020617; border: 1px solid var(--glass-border);
            padding: 15px; color: #fff; border-radius: 12px; flex: 1;
            outline: none; transition: 0.3s; font-family: 'JetBrains Mono', monospace;
        }

        .control-bar input:focus { border-color: var(--primary); animation: glow 2s infinite; }

        /* Main Workspace */
        .workspace {
            display: grid;
            grid-template-columns: 1fr 400px;
            gap: 25px;
        }

        .script-panel {
            background: var(--card-bg);
            border-radius: 35px;
            border: 1px solid var(--glass-border);
            padding: 50px;
            position: relative;
        }

        .step-section {
            margin-bottom: 60px;
            padding-left: 35px;
            border-left: 4px solid var(--primary);
            position: relative;
        }

        .step-label {
            background: var(--primary); color: #fff;
            padding: 6px 16px; border-radius: 8px;
            font-size: 11px; font-weight: 800; text-transform: uppercase;
            margin-bottom: 20px; display: inline-block;
        }

        .dialogue-text {
            font-size: 22px; line-height: 1.8; color: #cbd5e1;
        }

        .hl { color: var(--warning); font-weight: 800; border-bottom: 2px solid var(--warning); }

        /* Interaction Elements */
        .copy-button {
            margin-top: 25px;
            background: transparent; border: 1px solid var(--primary);
            color: var(--primary); padding: 12px 24px; border-radius: 12px;
            cursor: pointer; font-weight: 700; font-size: 13px;
            transition: 0.3s; display: flex; align-items: center; gap: 10px;
        }

        .copy-button:hover { background: var(--primary); color: #fff; }

        /* Right Sidebar Tools */
        .sidebar { display: flex; flex-direction: column; gap: 25px; }

        .tool-widget {
            background: var(--glass); border: 1px solid var(--glass-border);
            border-radius: 25px; padding: 30px;
        }

        .rebuttal-box {
            background: #020617; border-radius: 15px; padding: 20px;
            margin-bottom: 15px; border-left: 4px solid var(--danger);
            transition: 0.3s; cursor: pointer;
        }

        .rebuttal-box:hover { transform: scale(1.02); background: #0f172a; }
        .rebuttal-box strong { color: var(--danger); font-size: 13px; text-transform: uppercase; display: block; margin-bottom: 8px; }
        .rebuttal-box p { font-size: 14px; color: #94a3b8; line-height: 1.6; }

        .lead-button {
            background: linear-gradient(135deg, var(--success), #059669);
            color: #fff; border: none; width: 100%;
            padding: 25px; border-radius: 20px; font-weight: 900;
            font-size: 20px; text-transform: uppercase; cursor: pointer;
            box-shadow: 0 15px 35px rgba(16, 185, 129, 0.3);
            transition: 0.3s;
        }

        .lead-button:hover { transform: translateY(-5px); box-shadow: 0 20px 45px rgba(16, 185, 129, 0.4); }

        footer {
            margin-top: 50px; text-align: center; padding: 40px;
            opacity: 0.5; font-size: 12px; letter-spacing: 1px;
        }

        /* Scrollbar Styling */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: var(--bg); }
        ::-webkit-scrollbar-thumb { background: var(--primary); border-radius: 10px; }
    </style>
</head>
<body>

<div class="master-container">
    <header>
        <span class="agency-badge">PREMIUM BRAND AGENCY</span>
        <h1>PRIME SOLUTIONS</h1>
        <div class="portal-links">
            <a href="https://web-hub-code.github.io/PRIMESOLUTIONS/">Agency Website</a>
            <a href="https://web-hub-code.github.io/script/">Live Script Hub</a>
        </div>
    </header>

    <div class="control-bar">
        <input type="text" id="agName" placeholder="[Agent Name]" onkeyup="syncData()">
        <input type="text" id="csName" placeholder="[Customer Name]" onkeyup="syncData()">
        <input type="text" id="lcName" placeholder="[City/Location]" onkeyup="syncData()">
    </div>

    <div class="workspace">
        <div class="script-panel">
            <div class="step-section">
                <span class="step-label">Stage 1: The Hook (Steps 1-3)</span>
                <div class="dialogue-text" id="txt1">
                    "Hi, this is <span class="hl dyn-ag">Agent</span> from <strong>Prime Solutions</strong>. How's your day going in <span class="hl dyn-lc">Location</span>? <br><br>
                    We're verifying homeowners for the <span class="hl">2026 Home Efficiency Rebate</span>. Just to check—are you the <strong>homeowner</strong>? <br><br>
                    Excellent! Are we looking at <strong>5 to 10 windows</strong> or a full house today?"
                </div>
                <button class="copy-button" onclick="copyDialog('txt1')">COPY SCRIPT 1</button>
            </div>

            <div class="step-section" style="border-left-color: var(--warning);">
                <span class="step-label">Stage 2: Validation (Steps 4-6)</span>
                <div class="dialogue-text" id="txt2">
                    "To calculate the exact tax credits for your area, may I have your <strong>ZIP code</strong>? <br><br>
                    And for the state record, what is your <strong>Date of Birth</strong>? This helps us apply any <span class="hl">Senior or Military discounts</span> to your final report."
                </div>
                <button class="copy-button" onclick="copyDialog('txt2')">COPY SCRIPT 2</button>
            </div>

            <div class="step-section" style="border-left-color: var(--success);">
                <span class="step-label">Stage 3: Financing & Close (Steps 7-12)</span>
                <div class="dialogue-text" id="txt3">
                    "Perfect, <span class="hl dyn-cs">Customer</span>. To qualify for our <strong>0% interest plans</strong>, what is your credit score range? <br><br>
                    Our specialist will visit for a <span class="hl">Free 12-Month Price-Locked Estimate</span>. Do mornings or evenings work best for you and your spouse?"
                </div>
                <button class="copy-button" onclick="copyDialog('txt3')">COPY SCRIPT 3</button>
            </div>
        </div>

        <div class="sidebar">
            <div class="tool-widget">
                <h4 style="color: var(--success); font-size: 13px; margin-bottom: 20px; letter-spacing: 2px;">OBJECTION HANDLER</h4>
                
                <div class="rebuttal-box">
                    <strong>Why ZIP Code?</strong>
                    <p>"Credits are county-based. Your ZIP ensures we find the exact local funds available for your street."</p>
                </div>

                <div class="rebuttal-box">
                    <strong>Why both spouses?</strong>
                    <p>"The quote is a legal 12-month price lock. Both owners must receive the data to finalize the audit."</p>
                </div>

                <div class="rebuttal-box">
                    <strong>Not interested?</strong>
                    <p>"No problem! We provide the data and lock the price for 1 year. You use it only when you're ready."</p>
                </div>
            </div>

            <div class="tool-widget" style="background: rgba(99, 102, 241, 0.05);">
                <h4 style="color: var(--primary); font-size: 13px; margin-bottom: 15px;">AGENT STATS</h4>
                <div style="font-size: 13px; color: #94a3b8;">
                    <p>Status: <span style="color: var(--success);">● Active</span></p>
                    <p>Price Lock: <span style="color: #fff;">12 Months</span></p>
                    <p>Rebate Year: <span style="color: #fff;">2026</span></p>
                </div>
            </div>

            <button class="lead-button" onclick="alert('Lead Logged to Prime Solutions Database!')">Submit Prime Lead</button>
        </div>
    </div>

    <footer>
        PRIME SOLUTIONS AGENCY & SYSTEMS | PROPRIETARY OS V4.0 FINAL<br>
        DESIGNED FOR ELITE CONVERSIONS © 2026
    </footer>
</div>

<script>
    function syncData() {
        let ag = document.getElementById('agName').value || "Agent";
        let cs = document.getElementById('csName').value || "Customer";
        let lc = document.getElementById('lcName').value || "Location";

        document.querySelectorAll('.dyn-ag').forEach(e => e.innerText = ag);
        document.querySelectorAll('.dyn-cs').forEach(e => e.innerText = cs);
        document.querySelectorAll('.dyn-lc').forEach(e => e.innerText = lc);
    }

    function copyDialog(id) {
        let text = document.getElementById(id).innerText;
        navigator.clipboard.writeText(text);
        let btn = event.target;
        btn.innerText = "COPIED!";
        setTimeout(() => btn.innerText = "COPY SCRIPT", 2000);
    }
</script>

</body>
</html>
"""

# Save the file
with open("PrimeSolutions_Master_OS.html", "w") as f:
    f.write(html_content)
    
