<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime Solutions | Official Agent Portal</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #6366f1;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #f43f5e;
            --bg: #020617;
            --card: #0f172a;
        }

        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: var(--bg);
            color: #f1f5f9;
            margin: 0;
            padding: 20px;
        }

        .master-container {
            max-width: 1400px;
            margin: 0 auto;
            background: var(--card);
            border-radius: 40px;
            border: 1px solid rgba(255,255,255,0.1);
            overflow: hidden;
            box-shadow: 0 50px 100px -20px rgba(0,0,0,0.9);
        }

        /* Agency Header */
        header {
            background: linear-gradient(135deg, #1e1b4b 0%, #4338ca 100%);
            padding: 45px;
            text-align: center;
            border-bottom: 5px solid var(--warning);
        }

        header h1 { margin: 0; font-size: 40px; font-weight: 800; letter-spacing: 4px; }
        .branding-sub { color: var(--warning); font-size: 14px; font-weight: 600; margin-top: 10px; display: block; }

        /* Real-time Inputs */
        .input-hub {
            background: rgba(99, 102, 241, 0.1);
            padding: 25px 40px;
            display: flex;
            gap: 20px;
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }

        .input-hub input {
            background: #020617;
            border: 1px solid #334155;
            padding: 14px;
            color: white;
            border-radius: 12px;
            flex: 1;
            font-size: 14px;
            outline: none;
            transition: 0.3s;
        }

        .input-hub input:focus { border-color: var(--primary); box-shadow: 0 0 10px rgba(99, 102, 241, 0.3); }

        .content-grid {
            display: grid;
            grid-template-columns: 1.8fr 1fr;
            gap: 2px;
            background: rgba(255,255,255,0.1);
        }

        .panel { background: var(--card); padding: 45px; }

        /* Script Content */
        .step-box {
            margin-bottom: 50px;
            border-left: 6px solid var(--primary);
            padding-left: 25px;
            position: relative;
        }

        .phase-tag {
            background: var(--primary);
            color: white;
            padding: 6px 15px;
            border-radius: 8px;
            font-size: 11px;
            font-weight: 800;
            text-transform: uppercase;
            margin-bottom: 20px;
            display: inline-block;
        }

        .dialogue { font-size: 22px; line-height: 1.8; color: #e2e8f0; }
        .hl { color: var(--warning); font-weight: 800; text-decoration: underline; }

        .copy-btn {
            margin-top: 20px;
            background: rgba(255,255,255,0.05);
            border: 1px solid var(--primary);
            color: var(--primary);
            padding: 10px 20px;
            border-radius: 10px;
            cursor: pointer;
            font-weight: 700;
            transition: 0.3s;
        }

        .copy-btn:hover { background: var(--primary); color: white; }

        /* Sidebar Tools */
        .rebuttal-pill {
            background: #020617;
            padding: 20px;
            border-radius: 18px;
            margin-bottom: 15px;
            border-left: 4px solid var(--danger);
        }

        .rebuttal-pill strong { color: var(--danger); display: block; margin-bottom: 8px; font-size: 13px; }
        .rebuttal-pill p { font-size: 15px; color: #94a3b8; margin: 0; line-height: 1.6; }

        .lock-btn {
            background: var(--success);
            color: white;
            width: 100%;
            padding: 25px;
            border: none;
            border-radius: 20px;
            font-weight: 900;
            font-size: 20px;
            cursor: pointer;
            text-transform: uppercase;
            box-shadow: 0 15px 30px rgba(16, 185, 129, 0.3);
            margin-top: 20px;
        }

        footer { text-align: center; padding: 40px; background: #020617; color: #475569; font-size: 13px; }
    </style>
</head>
<body>

<div class="master-container">
    <header>
        <h1>PRIME SOLUTIONS</h1>
        <span class="branding-sub">OFFICIAL AGENT COMMAND CENTER & LEAD OS</span>
    </header>

    <div class="input-hub">
        <input type="text" id="agentInput" placeholder="Agent Name..." onkeyup="sync()">
        <input type="text" id="custInput" placeholder="Customer Name..." onkeyup="sync()">
        <input type="text" id="cityInput" placeholder="City Name..." onkeyup="sync()">
    </div>

    <div class="content-grid">
        <div class="panel">
            
            <div class="step-box">
                <span class="phase-tag">Phase 1: Verification</span>
                <div class="dialogue" id="d1">
                    "Hi, this is <span class="hl agent">Agent</span> from <strong>Prime Solutions</strong>. How are you today? <br><br>
                    We’re verifying homeowners in <span class="hl city">City</span> for the <span class="hl">2026 Home Efficiency Credits</span>. Are you the <strong>homeowner</strong>? <br><br>
                    Great! Are we looking at <strong>5 to 10 windows</strong> or more? And do you prefer <strong>Sliding or Casement</strong>?"
                </div>
                <button class="copy-btn" onclick="copyIt('d1')">COPY DIALOGUE</button>
            </div>

            <div class="step-box" style="border-left-color: var(--warning);">
                <span class="phase-tag">Phase 2: Qualification</span>
                <div class="dialogue" id="d2">
                    "To check the specific rebate for your county, what is your <strong>ZIP code</strong>? <br><br>
                    And for the state record, what is your <strong>Date of Birth</strong>? This helps us apply the <span class="hl">Senior or Veteran discounts</span> properly."
                </div>
                <button class="copy-btn" onclick="copyIt('d2')">COPY DIALOGUE</button>
            </div>

            <div class="step-box" style="border-left-color: var(--success);">
                <span class="phase-tag">Phase 3: Financials & Closing</span>
                <div class="dialogue" id="d3">
                    "Perfect, <span class="hl cust">Customer</span>. To qualify for <strong>0% interest</strong>, what is your credit range? <br><br>
                    Lastly, our specialist will visit for a <span class="hl">Free 12-Month Price-Locked Estimate</span>. Do mornings or evenings work best for you and your spouse?"
                </div>
                <button class="copy-btn" onclick="copyIt('d3')">COPY DIALOGUE</button>
            </div>

        </div>

        <div class="panel" style="border-left: 1px solid rgba(255,255,255,0.1);">
            <h4 style="color: var(--success); margin-top: 0; letter-spacing: 1px;">OBJECTION HANDLER</h4>
            
            <div class="rebuttal-pill">
                <strong>"Why do you need my ZIP?"</strong>
                <p>"Rebates are location-based. Your ZIP ensures Prime Solutions finds the exact credits for your specific street."</p>
            </div>

            <div class="rebuttal-pill">
                <strong>"Why both spouses?"</strong>
                <p>"The quote is a legal 12-month price guarantee. We need both owners to receive the data together."</p>
            </div>

            <div class="rebuttal-pill">
                <strong>"Not interested right now."</strong>
                <p>"I understand! That's why we give a 12-month price lock—so you can use the discount whenever you're ready within a year."</p>
            </div>

            <button class="lock-btn">Submit Prime Lead</button>
        </div>
    </div>

    <footer>
        PRIME SOLUTIONS AGENCY © 2026 | PREMIUM WEB & SCRIPT SYSTEMS<br>
        <a href="https://web-hub-code.github.io/PRIMESOLUTIONS/" style="color:var(--primary); text-decoration:none;">Visit Main Portfolio</a>
    </footer>
</div>

<script>
    function sync() {
        let agent = document.getElementById('agentInput').value || "Agent";
        let cust = document.getElementById('custInput').value || "Customer";
        let city = document.getElementById('cityInput').value || "City";

        document.querySelectorAll('.agent').forEach(e => e.innerText = agent);
        document.querySelectorAll('.cust').forEach(e => e.innerText = cust);
        document.querySelectorAll('.city').forEach(e => e.innerText = city);
    }

    function copyIt(id) {
        let text = document.getElementById(id).innerText;
        navigator.clipboard.writeText(text);
        alert("Copied to clipboard!");
    }
</script>

</body>
</html>
