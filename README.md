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

        /* Branding Header */
        header {
            background: linear-gradient(135deg, #1e1b4b 0%, #4338ca 100%);
            padding: 50px 40px;
            text-align: center;
            border-bottom: 4px solid var(--warning);
        }

        header h1 { margin: 0; font-size: 45px; font-weight: 800; letter-spacing: 4px; text-transform: uppercase; }
        .links { margin-top: 20px; display: flex; justify-content: center; gap: 15px; }
        .links a { 
            background: var(--glass); color: var(--warning); padding: 8px 20px; 
            border-radius: 50px; text-decoration: none; font-size: 13px; font-weight: 600;
            border: 1px solid rgba(245, 158, 11, 0.3); transition: 0.3s;
        }
        .links a:hover { background: var(--warning); color: #000; }

        .dashboard {
            display: grid;
            grid-template-columns: 1.8fr 1fr;
            gap: 2px;
            background: #1e293b;
        }

        .panel { background: var(--panel); padding: 50px; }

        /* Step Logic */
        .step-card {
            margin-bottom: 40px;
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

        /* Tools & Rebuttals */
        .tool-card {
            background: rgba(2, 6, 23, 0.5);
            border: 1px solid #334155;
            padding: 25px;
            border-radius: 20px;
            margin-bottom: 25px;
        }

        .tool-card h4 { color: var(--success); margin: 0 0 15px 0; text-transform: uppercase; font-size: 14px; }

        .rebuttal-box {
            background: #020617;
            padding: 15px;
            border-radius: 12px;
            margin-bottom: 12px;
            border-left: 4px solid var(--danger);
        }

        .rebuttal-box strong { color: var(--danger); font-size: 12px; display: block; margin-bottom: 5px; }
        .rebuttal-box p { font-size: 14px; color: #94a3b8; margin: 0; line-height: 1.5; }

        .cta-btn {
            background: var(--success);
            color: white;
            width: 100%;
            border: none;
            padding: 22px;
            border-radius: 18px;
            font-weight: 900;
            font-size: 20px;
            cursor: pointer;
            text-transform: uppercase;
            box-shadow: 0 10px 30px rgba(16, 185, 129, 0.3);
            transition: 0.3s;
        }
        .cta-btn:hover { transform: translateY(-5px); }

        footer {
            background: #020617;
            padding: 40px;
            text-align: center;
            border-top: 1px solid #1e293b;
        }

        .footer-text { font-size: 14px; color: #64748b; line-height: 2; }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1>PRIME SOLUTIONS</h1>
        <div class="links">
            <a href="https://web-hub-code.github.io/PRIMESOLUTIONS/" target="_blank">Home Website</a>
            <a href="https://web-hub-code.github.io/script/" target="_blank">Agent Script Portal</a>
        </div>
        <p style="margin-top: 20px; opacity: 0.8;">USA Energy Performance & Lead Management System</p>
    </header>

    <div class="dashboard">
        <div class="panel">
            
            <div class="step-card">
                <span class="step-label">Phase 1: Ownership (Steps 1-3)</span>
                <div class="dialogue">
                    "Hi, this is [Name] calling from <strong>Prime Solutions</strong>. How are you today? <br><br>
                    We're currently assisting homeowners with the <span class="hl">2026 Energy Rebate Verification</span>. Just to confirm—are you the <strong>homeowner</strong>? <br><br>
                    Great! Are we looking at <strong>5 to 10 windows</strong> or more? And do you prefer <strong>Sliding or Casement</strong>?"
                </div>
            </div>

            <div class="step-card" style="border-left-color: var(--warning);">
                <span class="step-label">Phase 2: Qualification (Steps 4-6)</span>
                <div class="dialogue">
                    "To check local tax incentives for your county, may I have your <strong>ZIP code</strong>? <br><br>
                    And for the record, what is your <strong>Date of Birth</strong>? This helps us apply the <span class="hl">Senior, Veteran, or Homeowner discounts</span> correctly."
                </div>
            </div>

            <div class="step-card" style="border-left-color: var(--success);">
                <span class="step-label">Phase 3: Financials (Steps 7-10)</span>
                <div class="dialogue">
                    "Are you planning this <strong>this month</strong>? To qualify for <strong>0% interest</strong>, what's your credit score range? I'll hold while you check your banking app real quick. <br><br>
                    Lastly, any <strong>mortgage modifications</strong> in the last 2 years?"
                </div>
            </div>

            <div class="step-card" style="border-left-color: var(--danger);">
                <span class="step-label">Phase 4: Final Closing (Steps 11-12)</span>
                <div class="dialogue">
                    "Perfect. Can I get your <strong>Full Name and Full Address</strong>? <br><br>
                    Our specialist will visit to drop off your <strong>Free 12-Month Price-Locked Report</strong>. Do <span class="hl">mornings or evenings</span> work best for you and your spouse?"
                </div>
            </div>

        </div>

        <div class="panel" style="border-left: 1px solid #1e293b;">
            
            <div class="tool-card">
                <h4>🎯 Advanced Rebuttals</h4>
                <div class="rebuttal-box">
                    <strong>"Why do you need my ZIP?"</strong>
                    <p>"Utility rebates vary by county. Your ZIP tells Prime Solutions exactly which credits are available for your street."</p>
                </div>
                <div class="rebuttal-box">
                    <strong>"Why both spouses?"</strong>
                    <p>"The estimate is a legal 1-year price lock. We need both owners present to finalize the report data together."</p>
                </div>
                <div class="rebuttal-box">
                    <strong>"Why Credit Score?"</strong>
                    <p>"To match you with 0% interest programs so you don't pay anything out of pocket today."</p>
                </div>
            </div>

            <div class="tool-card" style="border-color: var(--primary);">
                <h4>🚀 Success Strategy</h4>
                <ul style="font-size: 13px; color: #94a3b8; line-height: 2; padding-left: 20px;">
                    <li>Keep the tone <strong>Consultative</strong>.</li>
                    <li>Refer to the visit as a <strong>"Technical Report."</strong></li>
                    <li>Always use the <strong>"12-Month Price Lock."</strong></li>
                </ul>
            </div>

            <button class="cta-btn">Submit Prime Lead</button>
        </div>
    </div>

    <footer>
        <div class="footer-text">
            PROPRIETARY PROPERTY OF <strong>PRIME SOLUTIONS</strong> © 2026<br>
            Branding & Script Hub: <a href="https://web-hub-code.github.io/script/" style="color:var(--primary); text-decoration:none;">web-hub-code.github.io/script/</a>
        </div>
        <p style="font-size: 11px; color: #475569; margin-top: 20px; font-style: italic;">
            DNC Disclaimer: Homeowner agrees to a callback from Prime Solutions even if on the DNC list for this free estimate.
        </p>
    </footer>
</div>

</body>
</html>
