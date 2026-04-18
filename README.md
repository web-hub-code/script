<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime Solutions | Elite Windows Script</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&family=JetBrains+Mono:wght@500&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #6366f1;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #f43f5e;
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
            min-height: 100vh;
            padding: 20px;
        }

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
            font-size: clamp(30px, 5vw, 50px);
            font-weight: 800; letter-spacing: 8px;
            background: linear-gradient(to right, #fff, var(--primary), #a855f7);
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
            text-transform: uppercase;
        }

        .status-pill {
            display: inline-flex; align-items: center; gap: 8px;
            background: rgba(16, 185, 129, 0.1); color: var(--success);
            padding: 8px 25px; border-radius: 50px; font-size: 12px;
            font-weight: 700; border: 1px solid var(--success);
            margin-bottom: 20px;
        }

        /* Live Input Hub */
        .input-hub {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 20px;
            margin-bottom: 30px; max-width: 1400px; margin-inline: auto;
        }

        .input-hub input {
            background: #020617; border: 1px solid var(--border);
            padding: 18px; color: white; border-radius: 15px;
            font-family: 'JetBrains Mono', monospace; outline: none;
        }

        .input-hub input:focus { border-color: var(--primary); box-shadow: 0 0 15px rgba(99, 102, 241, 0.2); }

        /* Workspace Grid */
        .workspace {
            display: grid; grid-template-columns: 1.8fr 1fr; gap: 30px;
            max-width: 1600px; margin: 0 auto;
        }

        @media (max-width: 1024px) { .workspace { grid-template-columns: 1fr; } }

        .script-panel {
            background: var(--card); border-radius: 40px;
            border: 1px solid var(--border); padding: clamp(20px, 5vw, 50px);
        }

        /* Step Logic */
        .step-block {
            margin-bottom: 50px; padding-left: 30px;
            border-left: 5px solid var(--primary);
            position: relative;
        }

        .step-tag {
            background: var(--primary); color: white;
            padding: 6px 16px; border-radius: 8px;
            font-size: 11px; font-weight: 800; text-transform: uppercase;
            margin-bottom: 20px; display: inline-block;
        }

        .dialogue { font-size: clamp(18px, 3vw, 24px); line-height: 1.8; color: #cbd5e1; }
        .hl { color: var(--warning); font-weight: 800; border-bottom: 2px solid var(--warning); }
        .hook { color: var(--success); font-weight: 600; display: block; margin-top: 15px; font-size: 16px; }

        /* Rebuttals & Sidebar */
        .tool-card {
            background: var(--glass); border: 1px solid var(--border);
            border-radius: 30px; padding: 30px; margin-bottom: 25px;
        }

        .rebuttal-box {
            background: #020617; border-radius: 15px; padding: 20px;
            margin-bottom: 15px; border-left: 4px solid var(--danger);
            cursor: help;
        }

        .rebuttal-box strong { color: #f87171; font-size: 13px; display: block; margin-bottom: 5px; text-transform: uppercase; }
        .rebuttal-box p { font-size: 14px; color: #94a3b8; }

        .timeline-box { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 20px; }
        .time-btn {
            background: rgba(255,255,255,0.05); border: 1px solid var(--border);
            color: #fff; padding: 12px; border-radius: 12px; font-size: 11px;
            cursor: pointer; text-align: center; font-weight: 700;
        }
        .time-btn:hover { background: var(--primary); }

        .final-action {
            background: linear-gradient(135deg, var(--success), #059669);
            color: white; border: none; width: 100%;
            padding: 25px; border-radius: 20px; font-weight: 900;
            font-size: 20px; text-transform: uppercase; cursor: pointer;
            box-shadow: 0 15px 40px rgba(16, 185, 129, 0.3);
        }

        footer { text-align: center; padding: 60px; opacity: 0.4; font-size: 12px; }
    </style>
</head>
<body>

<div class="container">
    <header>
        <div class="status-pill">● WINDOWS FUTURE-PROOF PROGRAM ACTIVE</div>
        <h1>PRIME SOLUTIONS</h1>
        <p style="margin-top: 15px; opacity: 0.8; letter-spacing: 2px; font-weight: 600;">ELITE RESIDENTIAL WINDOWS NETWORK</p>
    </header>

    <div class="input-hub">
        <input type="text" id="agN" placeholder="Agent Name..." onkeyup="sync()">
        <input type="text" id="cuN" placeholder="Customer Name..." onkeyup="sync()">
        <input type="text" id="ciN" placeholder="City/Location..." onkeyup="sync()">
    </div>

    <div class="workspace">
        <div class="script-panel">
            
            <div class="step-block">
                <span class="step-tag">Step 1-3: Introduction & Trust</span>
                <div class="dialogue">
                    "Hi, this is <span class="hl ag">Agent</span> from <strong>Prime Solutions</strong>. We're reaching out to homeowners in <span class="hl ci">City</span>—not for a sales call, but to offer <strong>Free Informational Estimates</strong> for your <span class="hl">future windows improvement</span>. <br><br>
                    Our company provides the <strong>best prices and market discounts</strong>. We just want to give you the data so you have it on file for whenever you're ready. Are you the <strong>homeowner</strong>?"
                </div>
                <span class="hook">💡 CX Grab: Informational only—no pressure, no sign-up today.</span>
            </div>

            <div class="step-block" style="border-left-color: var(--warning);">
                <span class="step-tag">Step 4-8: The "Future" Qualification</span>
                <div class="dialogue">
                    "Great! Are we looking at <strong>5 to 10 windows</strong> or more? And do you prefer <strong>Sliding or Double-Hung</strong> style? <br><br>
                    We understand you might not be ready right now. Just so I can lock in the right <strong>seasonal discount</strong> for you—<strong>how soon do you think you'll be ready for new windows?</strong> <br><br>
                    A <span class="hl">couple of months</span>, <strong>3 to 6 months</strong>, or maybe <strong>a year</strong> from now?"
                </div>
                <div class="timeline-box">
                    <div class="time-btn">ASAP (Immediate)</div>
                    <div class="time-btn">2-3 Months (Planning)</div>
                    <div class="time-btn">6 Months (Future)</div>
                    <div class="time-btn">8-12 Months (Long Term)</div>
                </div>
            </div>

            <div class="step-block" style="border-left-color: var(--success);">
                <span class="step-tag">Step 9-12: Securing the Quote</span>
                <div class="dialogue">
                    "Perfect, <span class="hl cu">Customer</span>. To ensure your report has the <strong>best market-beating price</strong>, may I verify your <strong>ZIP code</strong> and <strong>DOB</strong>? <br><br>
                    This applies any <span class="hl">Senior, Veteran, or Federal incentives</span> to your quote. Our field specialist will simply drop off a <strong>Zero-Cost Price-Locked Guide</strong>. <br><br>
                    Would a morning or afternoon work for a quick drop-off?"
                </div>
                <span class="hook">💡 CX Grab: Lock the best price today; think about it later.</span>
            </div>

        </div>

        <div class="sidebar">
            <div class="tool-card">
                <h4 style="color: var(--success); margin-bottom: 20px; font-size: 14px;">🎯 WINDOWS CX REBUTTALS</h4>
                
                <div class="rebuttal-box">
                    <strong>"I can't afford windows now."</strong>
                    <p>"That's exactly why we're calling! We provide the <strong>free info today</strong> so you can plan for the future with the <strong>highest discounts</strong> already locked in."</p>
                </div>

                <div class="rebuttal-box">
                    <strong>"Is this a sales pitch?"</strong>
                    <p>"Not at all. This is a <strong>free informational service</strong>. We give you the price guarantee, and you decide when it's right for your budget."</p>
                </div>

                <div class="rebuttal-box">
                    <strong>"Why do you need my DOB?"</strong>
                    <p>"Windows rebates are often <strong>age-based</strong> (Senior/Veteran). We want to make sure you get every single dollar of discount available."</p>
                </div>
            </div>

            <button class="final-action" onclick="alert('Windows Future-Lead Logged!')">Lock Future Estimate</button>
        </div>
    </div>

    <footer>
        <strong>PRIME SOLUTIONS AGENCY</strong> | Residential Windows Division © 2026<br>
        Premium Future-Planning OS | V15.0 FINAL
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
