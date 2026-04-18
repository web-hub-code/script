<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime Solutions | Elite Lead System</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #4f46e5;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
            --dark-navy: #020617;
            --card-bg: #0f172a;
            --text-main: #f8fafc;
        }

        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: var(--dark-navy);
            color: var(--text-main);
            margin: 0;
            padding: 20px;
        }

        .master-container {
            max-width: 1400px;
            margin: 0 auto;
            background: var(--card-bg);
            border-radius: 30px;
            border: 1px solid #1e293b;
            overflow: hidden;
            box-shadow: 0 50px 100px -20px rgba(0,0,0,0.8);
        }

        /* Branding Header */
        header {
            background: linear-gradient(135deg, #1e1b4b 0%, #4f46e5 100%);
            padding: 40px;
            text-align: center;
            border-bottom: 5px solid var(--warning);
        }

        header h1 { margin: 0; font-size: 36px; font-weight: 800; letter-spacing: 3px; }
        header .brand-url { font-family: monospace; color: var(--warning); font-size: 14px; margin-top: 5px; display: block; text-decoration: none; opacity: 0.8; }
        header .tagline { margin-top: 10px; font-weight: 600; font-size: 16px; color: #94a3b8; }

        .dashboard-grid {
            display: grid;
            grid-template-columns: 1.8fr 1fr;
            gap: 2px;
            background: #1e293b;
        }

        .panel { background: var(--card-bg); padding: 40px; }

        /* Step Logic */
        .step-block {
            margin-bottom: 40px;
            padding-left: 20px;
            border-left: 5px solid var(--primary);
        }

        .step-label {
            background: var(--primary);
            color: white;
            padding: 4px 12px;
            border-radius: 6px;
            font-size: 11px;
            font-weight: 800;
            text-transform: uppercase;
            margin-bottom: 12px;
            display: inline-block;
        }

        .dialogue { font-size: 20px; line-height: 1.7; color: #e2e8f0; }
        .highlight { color: var(--warning); font-weight: 700; }

        /* Sidebar Tools */
        .tool-card {
            background: rgba(2, 6, 23, 0.5);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 1px solid #334155;
        }

        .tool-card h4 { margin: 0 0 15px 0; color: var(--success); text-transform: uppercase; font-size: 14px; }

        .rebuttal-box {
            background: #0f172a;
            border-radius: 10px;
            padding: 12px;
            margin-top: 10px;
            border-left: 3px solid var(--danger);
        }

        .rebuttal-q { color: var(--danger); font-weight: 800; font-size: 12px; display: block; }
        .rebuttal-a { color: #94a3b8; font-size: 14px; display: block; margin-top: 5px; }

        /* Footer / Company Info */
        footer {
            background: #020617;
            padding: 30px;
            border-top: 1px solid #1e293b;
            text-align: center;
        }

        .company-details { font-size: 13px; color: #64748b; line-height: 2; }
        .company-details a { color: var(--primary); text-decoration: none; font-weight: 600; }
        
        .cta-button {
            background: var(--success);
            color: white;
            width: 100%;
            border: none;
            padding: 20px;
            border-radius: 15px;
            font-weight: 900;
            font-size: 18px;
            cursor: pointer;
            text-transform: uppercase;
            box-shadow: 0 10px 20px rgba(16, 185, 129, 0.2);
        }
    </style>
</head>
<body>

<div class="master-container">
    <header>
        <h1>PRIME SOLUTIONS</h1>
        <a href="https://web-hub-code.github.io/PRIMESOLUTIONS/" target="_blank" class="brand-url">web-hub-code.github.io/PRIMESOLUTIONS/</a>
        <p class="tagline">USA Home Improvement & Lead Generation Excellence</p>
    </header>

    <div class="dashboard-grid">
        <div class="panel">
            <div class="step-block">
                <span class="step-label">Step 1-3: Introduction & Hook</span>
                <div class="dialogue">
                    "Hi, this is [Name] calling from <strong>Prime Solutions</strong>. How are you today? <br><br>
                    We’re helping homeowners secure <span class="highlight">2026 Window Rebates</span>. Are you the <strong>homeowner</strong>? <br><br>
                    Great! Are we looking at <strong>5 to 10 windows</strong> or more? And do you prefer <strong>Sliding or Casement</strong> styles?"
                </div>
            </div>

            <div class="step-block" style="border-left-color: var(--warning);">
                <span class="step-label">Step 4-6: Location & Data</span>
                <div class="dialogue">
                    "To check local tax credits, what is your <strong>ZIP code</strong>? <br><br>
                    And for the record, what is your <strong>Date of Birth</strong>? This ensures you receive the <span class="highlight">proper senior or state discounts</span>."
                </div>
            </div>

            <div class="step-block" style="border-left-color: var(--success);">
                <span class="step-label">Step 7-10: Financing & History</span>
                <div class="dialogue">
                    "Are you planning this <strong>this month</strong>? To qualify for <strong>0% Interest</strong>, what is your credit score range? I’ll hold while you check your banking app real quick. <br><br>
                    Lastly, any <strong>mortgage modifications</strong> in the last 2 years?"
                </div>
            </div>

            <div class="step-block" style="border-left-color: var(--danger);">
                <span class="step-label">Step 11-12: The Professional Close</span>
                <div class="dialogue">
                    "Perfect. Can I get your <strong>Full Name and Address</strong>? <br><br>
                    Our specialist will visit for a <span class="highlight">Free 12-Month Price-Locked Estimate</span>. Do mornings or evenings work best for you and your spouse?"
                </div>
            </div>
        </div>

        <div class="panel" style="border-left: 1px solid #1e293b;">
            <div class="tool-card">
                <h4>🎯 Rebuttals (The Why)</h4>
                <div class="rebuttal-box">
                    <span class="rebuttal-q">"Why ZIP code?"</span>
                    <span class="rebuttal-a">"To match county-specific rebates for Prime Solutions clients."</span>
                </div>
                <div class="rebuttal-box">
                    <span class="rebuttal-q">"Why Credit Score?"</span>
                    <span class="rebuttal-a">"To secure 0% down-payment financing options."</span>
                </div>
            </div>

            <div class="tool-card" style="border-color: var(--primary);">
                <h4>💎 Agent Pro-Tips</h4>
                <p style="font-size: 13px; color: #94a3b8; line-height: 1.6;">
                    • Mention <strong>Prime Solutions</strong> early to build trust.<br>
                    • Keep the tone helpful (Advisor), not pushy (Salesman).<br>
                    • Use the 12-month price lock as the final hook.
                </p>
            </div>

            <button class="cta-button">Submit Prime Lead</button>
        </div>
    </div>

    <footer>
        <div class="company-details">
            <strong>OFFICIAL PROPERTY OF PRIME SOLUTIONS</strong><br>
            Visit us: <a href="https://web-hub-code.github.io/PRIMESOLUTIONS/" target="_blank">web-hub-code.github.io/PRIMESOLUTIONS/</a><br>
            <span style="font-style: italic; opacity: 0.6;">DNC Disclaimer: By confirming, the homeowner agrees to a callback from our specialist for a free estimate.</span>
        </div>
    </footer>
</div>

</body>
</html>
