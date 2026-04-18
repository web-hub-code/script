<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime Solutions | Elite Script OS</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #6366f1;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #f43f5e;
            --bg-dark: #020617;
            --panel: #0f172a;
            --glass: rgba(255, 255, 255, 0.05);
        }

        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: var(--bg-dark);
            color: #f1f5f9;
            margin: 0;
            padding: 20px;
        }

        .container {
            max-width: 1450px;
            margin: 0 auto;
            background: var(--panel);
            border: 1px solid #1e293b;
            border-radius: 40px;
            overflow: hidden;
            box-shadow: 0 50px 100px -20px rgba(0,0,0,0.8);
        }

        /* Agency Branding Header */
        header {
            background: linear-gradient(135deg, #1e1b4b 0%, #4338ca 100%);
            padding: 60px 40px;
            text-align: center;
            border-bottom: 4px solid var(--warning);
        }

        header h1 { margin: 0; font-size: 45px; font-weight: 800; letter-spacing: 4px; text-transform: uppercase; }
        .agency-tag { color: var(--warning); font-weight: 600; font-size: 14px; letter-spacing: 2px; display: block; margin-top: 5px; }
        
        .nav-links { margin-top: 25px; display: flex; justify-content: center; gap: 15px; }
        .nav-links a { 
            background: var(--glass); color: white; padding: 10px 25px; 
            border-radius: 50px; text-decoration: none; font-size: 13px; font-weight: 600;
            border: 1px solid rgba(255, 255, 255, 0.1); transition: 0.3s;
        }
        .nav-links a:hover { background: white; color: black; }

        .dashboard {
            display: grid;
            grid-template-columns: 1.8fr 1fr;
            gap: 2px;
            background: #1e293b;
        }

        .panel { background: var(--panel); padding: 50px; }

        /* The 12-Step Script Flow */
        .step-card {
            margin-bottom: 45px;
            padding-left: 30px;
            border-left: 6px solid var(--primary);
        }

        .step-label {
            background: var(--primary);
            color: white;
            padding: 5px 15px;
            border-radius: 8px;
            font-size: 11px;
            font-weight: 800;
            text-transform: uppercase;
            margin-bottom: 15px;
            display: inline-block;
        }

        .dialogue { font-size: 21px; line-height: 1.8; color: #e2e8f0; }
        .hl { color: var(--warning); font-weight: 800; text-decoration: underline; }

        /* Rebuttals & Tools */
        .card {
            background: rgba(2, 6, 23, 0.5);
            border: 1px solid #334155;
            padding: 30px;
            border-radius: 25px;
            margin-bottom: 30px;
        }

        .card h4 { color: var(--success); margin: 0 0 20px 0; text-transform: uppercase; font-size: 14px; }

        .rebuttal-box {
            background: #020617;
            padding: 18px;
            border-radius: 15px;
            margin-bottom: 15px;
            border-left: 4px solid var(--danger);
        }

        .rebuttal-box strong { color: var(--danger); font-size: 13px; display: block; margin-bottom: 8px; }
        .rebuttal-box p { font-size: 15px; color: #94a3b8; margin: 0; line-height: 1.5; }

        .action-btn {
            background: var(--success);
            color: white;
            width: 100%;
            border: none;
            padding: 25px;
            border-radius: 20px;
            font-weight: 900;
            font-size: 18px;
            cursor: pointer;
            text-transform: uppercase;
            box-shadow: 0 15px 30px rgba(16, 185, 129, 0.2);
            transition: 0.3s;
        }

        footer {
            background: #020617;
            padding: 40px;
            text-align: center;
            border-top: 1px solid #1e293b;
        }

        .footer-brand { font-size: 13px; color: #64748b; line-height: 2; }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1>PRIME SOLUTIONS</h1>
        <span class="agency-tag">PREMIUM WEB & BRANDING AGENCY</span>
        <div class="nav-links">
            <a href="https://web-hub-code.github.io/PRIMESOLUTIONS/" target="_blank">Agency Portfolio</a>
            <a href="https://web-hub-code.github.io/script/" target="_blank">Live Script Portal</a>
        </div>
    </header>

    <div class="dashboard">
        <div class="panel">
            
            <div class="step-card">
                <span class="step-label">Step 1-3: The Introduction</span>
                <div class="dialogue">
                    "Hi, I'm [Name] from <strong>Prime Solutions</strong>. How are you? <br><br>
                    We’re helping homeowners verify their <span class="hl">2026 Energy Rebates</span>. Are you the <strong>homeowner</strong>? <br><br>
                    Perfect! About how many windows—<strong>5 to 10</strong> or more? And do you like <strong>Sliding or Casement</strong>?"
                </div>
            </div>

            <div class="step-card" style="border-left-color: var(--warning);">
                <span class="step-label">Step 4-6: Qualification</span>
                <div class="dialogue">
                    "To check local county credits, what is your <strong>ZIP code</strong>? <br><br>
                    And for state eligibility, may I have your <strong>Date of Birth</strong>? This ensures you get the <span class="hl">Senior or Veteran discounts</span> available."
                </div>
            </div>

            <div class="step-card" style="border-left-color: var(--success);">
                <span class="step-label">Step 7-10: Financing Hook</span>
                <div class="dialogue">
                    "Planning for this month? For our <span class="hl">0% Interest & No-Down-Payment</span> plans, what's your credit range? Check your banking app—I'll hold. <br><br>
                    Lastly, any <strong>mortgage modifications</strong> recently?"
                </div>
            </div>

            <div class="step-card" style="border-left-color: var(--danger);">
                <span class="step-label">Step 11-12: The Close</span>
                <div class="dialogue">
                    "Great! Confirm your <strong>Full Name and Address</strong>. <br><br>
                    Our specialist will visit for a <span class="hl">Free 12-Month Price-Locked Estimate</span>. Do <strong>mornings or evenings</strong> work for you and your spouse?"
                </div>
            </div>

        </div>

        <div class="panel" style="border-left: 1px solid #1e293b;">
            <div class="card">
                <h4>🎯 Live Rebuttals</h4>
                <div class="rebuttal-box">
                    <strong>"Why do you need my ZIP?"</strong>
                    <p>"Rebates are location-specific. Your ZIP ensures Prime Solutions calculates the exact credits for your street."</p>
                </div>
                <div class="rebuttal-box">
                    <strong>"Why both spouses?"</strong>
                    <p>"The quote is a legal 12-month price guarantee. We need both owners present to finalize the data together."</p>
                </div>
                <div class="rebuttal-box">
                    <strong>"Is this a sales call?"</strong>
                    <p>"This is a technical assessment. We provide the data and price-lock; you decide when you're ready."</p>
                </div>
            </div>

            <div class="card" style="border-color: var(--primary);">
                <h4>🚀 Agency Success Tips</h4>
                <p style="font-size: 13px; color: #94a3b8; line-height: 1.8;">
                    • Build trust using the <strong>Prime Solutions</strong> brand name.<br>
                    • Use the <strong>"12-Month Price Lock"</strong> as your strongest hook.<br>
                    • Treat every lead as a <strong>"Technical Audit."</strong>
                </p>
            </div>

            <button class="action-btn">Lock Final Appointment</button>
        </div>
    </div>

    <footer>
        <div class="footer-brand">
            <strong>PRIME SOLUTIONS AGENCY</strong> | Premium Web Development & Lead Generation<br>
            <a href="https://web-hub-code.github.io/PRIMESOLUTIONS/" style="color:var(--primary); text-decoration:none;">Visit Portfolio</a> • 
            <a href="https://web-hub-code.github.io/script/" style="color:var(--primary); text-decoration:none;">User Script Hub</a>
        </div>
    </footer>
</div>

</body>
</html>
