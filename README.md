<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime Solutions | Elite Master Lead OS</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&family=JetBrains+Mono:wght@500&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #6366f1;
            --success: #10b981;
            --warning: #f59e0b;
            --bg: #030712;
            --card: #0f172a;
            --glass: rgba(255, 255, 255, 0.03);
            --border: rgba(255, 255, 255, 0.1);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; transition: 0.3s ease; }
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background: radial-gradient(circle at 0% 0%, #1e1b4b 0%, #030712 100%);
            color: #f1f5f9;
            padding: 20px;
        }

        /* Animated Header */
        header {
            background: var(--glass);
            backdrop-filter: blur(25px);
            border: 1px solid var(--border);
            border-radius: 40px;
            padding: 50px 20px;
            text-align: center;
            margin-bottom: 30px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.5);
        }

        header h1 {
            font-size: 50px; font-weight: 800; letter-spacing: 8px;
            background: linear-gradient(to right, #fff, var(--primary), #a855f7);
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
            text-transform: uppercase;
        }

        .portal-badge {
            display: inline-flex; align-items: center; gap: 8px;
            background: rgba(16, 185, 129, 0.1); color: var(--success);
            padding: 8px 25px; border-radius: 50px; font-size: 12px;
            font-weight: 700; border: 1px solid var(--success);
            margin-bottom: 20px;
        }

        /* Live Sync Controls */
        .control-hub {
            display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px;
            margin-bottom: 30px; max-width: 1400px; margin-inline: auto;
        }

        .control-hub input {
            background: #020617; border: 1px solid var(--border);
            padding: 18px; color: white; border-radius: 15px;
            font-family: 'JetBrains Mono', monospace; outline: none;
        }

        .control-hub input:focus { border-color: var(--primary); box-shadow: 0 0 15px rgba(99, 102, 241, 0.2); }

        /* Main Grid */
        .workspace {
            display: grid; grid-template-columns: 1.8fr 1fr; gap: 30px;
            max-width: 1550px; margin: 0 auto;
        }

        .script-panel {
            background: var(--card); border-radius: 40px;
            border: 1px solid var(--border); padding: 50px;
        }

        /* Step Styling */
        .step-block {
            margin-bottom: 50px; padding-left: 30px;
            border-left: 5px solid var(--primary);
            animation: fadeIn 0.6s ease-out;
        }

        .step-tag {
            background: var(--primary); color: white;
            padding: 5px 15px; border-radius: 8px;
            font-size: 11px; font-weight: 800; text-transform: uppercase;
            margin-bottom: 15px; display: inline-block;
        }

        .dialogue { font-size: 24px; line-height: 1.8; color: #e2e8f0; }
        .hl { color: var(--warning); font-weight: 800; border-bottom: 2px solid var(--warning); }
        .trust-line { color: var(--success); font-weight: 600; display: block; margin-top: 15px; font-size: 16px; }

        /* Sidebar & Rebuttals */
        .sidebar { display: flex; flex-direction: column; gap: 25px; }

        .tool-card {
            background: var(--glass); border: 1px solid var(--border);
            border-radius: 30px; padding: 30px;
        }

        .rebuttal-box {
            background: #020617; border-radius: 15px; padding: 20px;
            margin-bottom: 15px; border-left: 4px solid var(--danger);
            cursor: pointer;
        }

        .rebuttal-box:hover { transform: translateX(10px); background: #1e1b4b; }
        .rebuttal-box strong { color: #f87171; font-size: 13px; display: block; margin-bottom: 5px; }

        .time-pill {
            display: inline-block; background: rgba(255,255,255,0.05);
            padding: 10px 15px; border-radius: 10px; margin: 5px;
            font-size: 12px; cursor: pointer; border: 1px solid var(--border);
        }
        .time-pill:hover { background: var(--primary); color: white; }

        .submit-btn {
            background: linear-gradient(135deg, var(--success), #059669);
            color: white; border: none; width: 100%;
            padding: 25px; border-radius: 20px; font-weight: 900;
            font-size: 20px; text-transform: uppercase; cursor: pointer;
            box-shadow: 0 15px 40px rgba(16, 185, 129, 0.3);
        }

        @keyframes fadeIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }

        footer { text-align: center; padding: 60px; opacity: 0.4; font-size: 12px; }
    </style>
</head>
<body>

<div class="container">
    <header>
        <div class="portal-badge">● TRUSTED NETWORK | FUTURE IMPROVEMENT PROGRAM</div>
        <h1>PRIME SOLUTIONS</h1>
    </header>

    <div class="control-hub">
        <input type="text" id="agN" placeholder="Agent Name..." onkeyup="sync()">
        <input type="text" id="cuN" placeholder="Customer Name..." onkeyup="sync()">
        <input type="text" id="ciN" placeholder="City Name..." onkeyup="sync()">
    </div>

    <div class="workspace">
        <div class="script-panel">
            
            <div class="step-block">
                <span class="step-tag">Step 1-3: Non-Sales Introduction</span>
                <div class="dialogue">
                    "Hi, this is <span class="hl ag">Agent</span> from <strong>Prime Solutions</strong>. We're reaching out to homeowners in <span class="hl ci">City</span>—not for a sales call, but to offer <strong>Free Estimates</strong> for your <span class="hl">future home improvements</span>. <br><br>
                    Hamari company market se behtar <strong>prices aur discounts</strong> offer karti hai, toh hum chahte hain ke aapke paas ye info ho jab bhi aap ready hon. Are you the <strong>homeowner</strong>?"
                </div>
                <span class="trust-line">✅ Trust Point: Ye sirf ek informational call hai, koi sign-up nahi.</span>
            </div>

            <div class="step-block" style="border-left-color: var(--warning);">
                <span class="step-tag">Step 4-6: Future Planning</span>
                <div class="dialogue">
                    "Hum samajhte hain ke aap abhi ready nahi honge. Just for our records—<strong>aap windows ya improvement kab tak plan kar rahe hain?</strong> <br><br>
                    Maybe in <span class="hl">2 months</span>, <strong>6 months</strong>, ya shayad <strong>1 saal</strong> ke baad?"
                </div>
                <div style="margin-top:15px;">
                    <span class="time-pill">ASAP</span>
                    <span class="time-pill">2-3 Months</span>
                    <span class="time-pill">6 Months</span>
                    <span class="time-pill">1 Year+</span>
                </div>
            </div>

            <div class="step-block" style="border-left-color: var(--success);">
                <span class="step-tag">Step 7-12: Value Lock</span>
                <div class="dialogue">
                    "Perfect, <span class="hl cu">Customer</span>. To lock your <strong>Market Discount</strong>, may I verify your <strong>ZIP code</strong> and <strong>DOB</strong>? <br><br>
                    Ye sirf isliye hai taaki hum aapke area ke <span class="hl">Senior ya Veteran discounts</span> apply kar saken. <br><br>
                    Specialist kab aakar aapko ye <strong>Price-Locked Guide</strong> drop kar de?"
                </div>
                <span class="trust-line">✅ Trust Point: Estimate 12 mahine tak valid rahega.</span>
            </div>

        </div>

        <div class="sidebar">
            <div class="tool-card">
                <h4 style="color: var(--success); margin-bottom: 20px; font-size: 14px;">CX GRAB REBUTTALS</h4>
                
                <div class="rebuttal-box">
                    <strong>"I am busy right now."</strong>
                    <p>"I understand! Isliye main sirf 60 seconds lungi taaki aapka **Future Discount** lock ho jaye aur hum aapko guide drop kar saken."</p>
                </div>

                <div class="rebuttal-box">
                    <strong>"Why do you need my DOB?"</strong>
                    <p>"Hamare discounts age-based hote hain. DOB se hum aapko **Maximum Saving** dila sakte hain jo market mein koi nahi dega."</p>
                </div>

                <div class="rebuttal-box">
                    <strong>"Is this a sales call?"</strong>
                    <p>"Bilkul nahi! Ye sirf **Future Planning** ke liye free informational call hai. Aap decision tabhi lein jab aap ready hon."</p>
                </div>
            </div>

            <button class="submit-btn" onclick="alert('Lead Locked for Prime Solutions!')">Submit Future Lead</button>
        </div>
    </div>

    <footer>
        <strong>PRIME SOLUTIONS AGENCY</strong> | Premium Branding Systems © 2026<br>
        Designed for Elite Performance
    </footer>
</div>

<script>
    function sync() {
        let ag = document.getElementById('agN').value || "Agent";
        let cu = document.getElementById('cuN').value || "Customer";
        let ci = document.getElementById('ciN').value || "City";

        document.querySelectorAll('.ag').forEach(e => e.innerText = ag);
        document.querySelectorAll('.cu').forEach(e => e.innerText = cu);
        document.querySelectorAll('.ci').forEach(e => e.innerText = ci);
    }
</script>

</body>
</html>
