<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime Solutions | Official Windows Script Hub</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&family=JetBrains+Mono:wght@500&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #6366f1;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #f87171;
            --bg: #030712;
            --glass: rgba(255, 255, 255, 0.03);
            --border: rgba(255, 255, 255, 0.1);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1); }
        
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background: radial-gradient(circle at 0% 0%, #1e1b4b 0%, #030712 100%);
            color: #f1f5f9;
            min-height: 100vh;
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
            box-shadow: 0 25px 50px rgba(0,0,0,0.5);
        }

        header h1 {
            font-size: clamp(25px, 5vw, 45px);
            font-weight: 800; letter-spacing: 6px;
            background: linear-gradient(to right, #fff, var(--primary), #a855f7);
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
            text-transform: uppercase;
        }

        .status-badge {
            display: inline-flex; align-items: center; gap: 8px;
            background: rgba(16, 185, 129, 0.1); color: var(--success);
            padding: 8px 25px; border-radius: 50px; font-size: 11px;
            font-weight: 700; border: 1px solid var(--success);
            margin-bottom: 15px;
        }

        /* Live Control Center */
        .control-hub {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 15px;
            margin-bottom: 30px; max-width: 1400px; margin-inline: auto;
        }

        .control-hub input {
            background: #020617; border: 1px solid var(--border);
            padding: 18px; color: white; border-radius: 15px;
            font-family: 'JetBrains Mono', monospace; outline: none;
        }

        .control-hub input:focus { border-color: var(--primary); box-shadow: 0 0 15px rgba(99, 102, 241, 0.3); }

        /* Workspace Grid */
        .workspace {
            display: grid; grid-template-columns: 1.8fr 1fr; gap: 30px;
            max-width: 1600px; margin: 0 auto;
        }

        @media (max-width: 1100px) { .workspace { grid-template-columns: 1fr; } }

        .script-panel {
            background: rgba(15, 23, 42, 0.8);
            border-radius: 40px; border: 1px solid var(--border);
            padding: clamp(20px, 5vw, 50px);
        }

        /* Natural Dialogue Blocks */
        .step-card {
            margin-bottom: 50px; padding: 30px;
            background: var(--glass); border-radius: 30px;
            border-left: 6px solid var(--primary);
            position: relative;
        }

        .step-label {
            background: var(--primary); color: white;
            padding: 5px 15px; border-radius: 8px;
            font-size: 10px; font-weight: 800; text-transform: uppercase;
            margin-bottom: 20px; display: inline-block;
        }

        .dialogue { font-size: clamp(18px, 2.5vw, 24px); line-height: 1.8; color: #cbd5e1; }
        .hl { color: var(--warning); font-weight: 800; border-bottom: 2px dashed var(--warning); }
        .natural-tip { 
            color: var(--success); font-weight: 600; display: block; 
            margin-top: 20px; font-size: 14px; font-style: italic;
            border-top: 1px solid var(--border); padding-top: 15px;
        }

        /* Sidebar Tools */
        .sidebar { display: flex; flex-direction: column; gap: 25px; }

        .tool-card {
            background: var(--glass); border: 1px solid var(--border);
            border-radius: 30px; padding: 30px;
        }

        .rebuttal-pill {
            background: #020617; border-radius: 18px; padding: 20px;
            margin-bottom: 15px; border-left: 4px solid var(--danger);
            cursor: pointer;
        }

        .rebuttal-pill:hover { transform: translateX(10px); background: #1e1b4b; }
        .rebuttal-pill strong { color: var(--danger); font-size: 12px; display: block; margin-bottom: 8px; text-transform: uppercase; }
        .rebuttal-pill p { font-size: 14px; color: #94a3b8; line-height: 1.6; }

        .timeline-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 15px; }
        .time-pill {
            background: rgba(255,255,255,0.05); border: 1px solid var(--border);
            color: white; padding: 10px; border-radius: 12px; font-size: 11px;
            text-align: center; cursor: pointer; font-weight: 700;
        }
        .time-pill:hover { background: var(--primary); }

        .action-btn {
            background: linear-gradient(135deg, #10b981, #059669);
            color: white; border: none; width: 100%;
            padding: 25px; border-radius: 20px; font-weight: 900;
            font-size: 20px; text-transform: uppercase; cursor: pointer;
            box-shadow: 0 15px 40px rgba(16, 185, 129, 0.3);
        }

        .action-btn:hover { transform: translateY(-5px); box-shadow: 0 25px 50px rgba(16, 185, 129, 0.4); }

        footer { text-align: center; padding: 60px; opacity: 0.4; font-size: 12px; letter-spacing: 2px; }
    </style>
</head>
<body>

<div class="container">
    <header>
        <div class="status-badge">● ELITE MODE: NATURAL CONVERSATION ACTIVE</div>
        <h1>PRIME SOLUTIONS</h1>
        <p style="margin-top: 15px; opacity: 0.7; font-size: 13px; letter-spacing: 4px; font-weight: 600;">RESIDENTIAL WINDOWS NETWORK</p>
    </header>

    <div class="control-hub">
        <input type="text" id="agN" placeholder="Agent Name..." onkeyup="sync()">
        <input type="text" id="cuN" placeholder="Customer Name..." onkeyup="sync()">
        <input type="text" id="ciN" placeholder="City Name..." onkeyup="sync()">
    </div>

    <div class="workspace">
        <div class="script-panel">
            
            <div class="step-card">
                <span class="step-label">Phase 1: Friendly Introduction</span>
                <div class="dialogue">
                    "Hey <span class="hl cu">Customer</span>! How’s your afternoon going over in <span class="hl ci">City</span>? <br><br>
                    Look, I’m <span class="hl ag">Agent</span> from <strong>Prime Solutions</strong>. I’m not calling to sell or sign you up for anything today. <br><br>
                    Honestly, we’re just reaching out to offer <strong>free informational estimates</strong> for <span class="hl">future</span> window upgrades. Just checking—are you the <strong>homeowner</strong> there?"
                </div>
                <span class="natural-tip">🗣️ Style: Bilkul relax hokar baat karein, jaise kisi dost se ghap-shup kar rahe hon.</span>
            </div>

            <div class="step-card" style="border-left-color: var(--warning);">
                <span class="step-label">Phase 2: The "Future" Logic</span>
                <div class="dialogue">
                    "Nice! You know, most people aren't ready to change windows *right now*, and that's totally cool. <br><br>
                    Whenever you *do* decide to fix 'em up—maybe in <strong>3 months, 6 months</strong>, or even <strong>next year</strong>—it’s better to have the <strong>best market price</strong> already locked in. <br><br>
                    Just for my notes, are we talking about <strong>5 to 10 windows</strong> or a bigger project?"
                </div>
                <div class="timeline-grid">
                    <div class="time-pill">ASAP</div>
                    <div class="time-pill">2-3 Months</div>
                    <div class="time-pill">6 Months</div>
                    <div class="time-pill">1 Year+</div>
                </div>
                <span class="natural-tip">🗣️ Style: "Next year" bolne se customer ka pressure khatam ho jata hai.</span>
            </div>

            <div class="step-card" style="border-left-color: var(--success);">
                <span class="step-label">Phase 3: Locking The Discount</span>
                <div class="dialogue">
                    "Perfect! To make sure you get our <strong>highest market discounts</strong> (especially if you qualify for <span class="hl">Senior or Veteran incentives</span>), let me just verify your <strong>ZIP and DOB</strong>. <br><br>
                    This is strictly for your informational guide. My specialist will just drop off a <strong>Free Price-Locked Report</strong>—you can keep it in a drawer and use it when YOU are ready. <br><br>
                    Do <strong>mornings</strong> work for a 2-minute drop-off?"
                </div>
                <span class="natural-tip">🗣️ Style: "Keep it in a drawer" ka matlab hai ke koi jaldi nahi hai.</span>
            </div>

        </div>

        <div class="sidebar">
            <div class="tool-card">
                <h4 style="color: var(--success); margin-bottom: 25px; font-size: 14px; letter-spacing: 1px;">NATURAL REBUTTALS</h4>
                
                <div class="rebuttal-pill">
                    <strong>"I'm not interested right now."</strong>
                    <p>"Haha, I figured! That's exactly why I'm calling—not for today, but for your <strong>future</strong> needs. It's just free info for your records."</p>
                </div>

                <div class="rebuttal-pill">
                    <strong>"Is this a sales call?"</strong>
                    <p>"Honestly? No. It’s a <strong>free informational call</strong>. We give you the market guide, and you decide if or when to use it."</p>
                </div>

                <div class="rebuttal-pill">
                    <strong>"Why do you need my DOB?"</strong>
                    <p>"State and federal incentives are often <strong>age-based</strong>. I just want to make sure you get the maximum discount possible!"</p>
                </div>
            </div>

            <div class="tool-card" style="background: rgba(99, 102, 241, 0.05);">
                <h4 style="color: var(--primary); font-size: 12px; margin-bottom: 10px;">PRO AGENT TIP</h4>
                <p style="font-size: 13px; color: #94a3b8; line-height: 1.8;">
                    Robot mat banna. Customer ke sath normal ghap-shup karein. Agar wo hansi mazaq karein, toh aap bhi karein. Sale details khud ba khud mil jayengi!
                </p>
            </div>

            <button class="action-btn" onclick="alert('Natural Lead Successfully Saved!')">Submit Future Lead</button>
        </div>
    </div>

    <footer>
        <strong>PRIME SOLUTIONS AGENCY</strong> | The Art of Natural Sales © 2026<br>
        Everything Modern, Premium & Animated
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
