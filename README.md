<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Master Script | Prime Solutions USA</title>
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;800&family=JetBrains+Mono&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #3b82f6;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
            --dark-navy: #020617;
            --card-bg: #0f172a;
            --text-silver: #cbd5e1;
        }

        body {
            font-family: 'Outfit', sans-serif;
            background-color: var(--dark-navy);
            color: #f8fafc;
            margin: 0;
            padding: 20px;
        }

        .master-wrapper {
            max-width: 1300px;
            margin: 0 auto;
            background: var(--card-bg);
            border: 1px solid #1e293b;
            border-radius: 30px;
            overflow: hidden;
            box-shadow: 0 50px 100px -20px rgba(0,0,0,0.8);
        }

        header {
            background: linear-gradient(135deg, #1e3a8a 0%, #3b82f6 100%);
            padding: 50px 30px;
            text-align: center;
            border-bottom: 5px solid var(--warning);
        }

        header h1 { margin: 0; font-size: 35px; font-weight: 800; letter-spacing: 2px; }
        header p { color: var(--warning); font-size: 18px; font-weight: 600; margin-top: 10px; }

        .main-grid {
            display: grid;
            grid-template-columns: 1.8fr 1fr;
            gap: 2px;
            background: #1e293b;
        }

        .panel { background: var(--card-bg); padding: 45px; }

        /* Step Styling */
        .step-container {
            margin-bottom: 50px;
            padding-left: 25px;
            border-left: 6px solid var(--primary);
            position: relative;
        }

        .step-tag {
            background: var(--primary);
            color: white;
            font-size: 12px;
            font-weight: 900;
            padding: 5px 15px;
            border-radius: 8px;
            display: inline-block;
            margin-bottom: 15px;
            text-transform: uppercase;
        }

        .dialogue-text {
            font-size: 21px;
            line-height: 1.7;
            color: #f1f5f9;
        }

        .highlight { color: var(--warning); font-weight: 800; text-decoration: underline; }

        /* Right Sidebar Features */
        .feature-card {
            background: #1e293b;
            border: 1px solid #334155;
            padding: 25px;
            border-radius: 20px;
            margin-bottom: 25px;
        }

        .feature-card h4 { color: var(--success); margin: 0 0 15px 0; text-transform: uppercase; font-size: 15px; }

        .logic-hint {
            font-family: 'JetBrains Mono', monospace;
            font-size: 13px;
            color: #60a5fa;
            background: rgba(96, 165, 250, 0.1);
            padding: 10px;
            border-radius: 8px;
            margin-top: 10px;
            display: block;
        }

        .cta-button {
            background: var(--success);
            color: white;
            width: 100%;
            padding: 20px;
            border-radius: 15px;
            font-weight: 900;
            font-size: 18px;
            border: none;
            cursor: pointer;
            text-transform: uppercase;
            transition: 0.3s;
        }

        .cta-button:hover { background: #059669; box-shadow: 0 0 20px var(--success); }

        .disclaimer-footer {
            background: #020617;
            padding: 25px;
            font-size: 13px;
            color: #64748b;
            border-top: 1px solid #1e293b;
            font-style: italic;
        }
    </style>
</head>
<body>

<div class="master-wrapper">
    <header>
        <h1>ULTIMATE WINDOW CONVERSION SYSTEM</h1>
        <p>COMPLETE 12-STEP PROFESSIONAL SCRIPT | PRIME SOLUTIONS USA</p>
    </header>

    <div class="main-grid">
        <div class="panel">
            
            <div class="step-container">
                <span class="step-tag">Step 1-3: Verification & Interest</span>
                <div class="dialogue-text">
                    "Hi, this is [Your Name] from the <strong>Project Assessment Center</strong>. How are you today? <br><br>
                    We’re helping homeowners in your area secure <span class="highlight">2026 Home Improvement Rebates</span>. Are you the <strong>homeowner</strong> of the property? <br><br>
                    Great! Roughly how many windows are you looking to estimate—around <strong>5 to 10</strong>, or more? And do you prefer <strong>Sliding, Casement, or Modern Aluminum</strong>?"
                </div>
                <span class="logic-hint">// Strategy: Use "Project Assessment Center" to sound official and non-salesy.</span>
            </div>

            <div class="step-container" style="border-left-color: var(--warning);">
                <span class="step-tag">Step 4-6: Rebate Qualification</span>
                <div class="dialogue-text">
                    "To check the <strong>tax incentives</strong> in your area, may I have your <strong>ZIP code</strong>? <br><br>
                    And for the state record, may I ask for your <strong>Date of Birth</strong>? This is purely to see which <span class="highlight">Senior or First-Time Buyer Rebates</span> you qualify for."
                </div>
            </div>

            <div class="step-container" style="border-left-color: var(--success);">
                <span class="step-tag">Step 7-10: Financing & Credit Lock</span>
                <div class="dialogue-text">
                    "Excellent. Are you planning this for <strong>this month</strong> or just budgeting for the next 90 days? Have you seen other quotes yet? <br><br>
                    To secure the <span class="highlight">0% Interest Financing</span>, roughly where does your credit score sit? Most homeowners check their banking app—I’ll hold for a second while you grab that range. <br><br>
                    Lastly, any <strong>mortgage modifications</strong> in the past 2 years?"
                </div>
                <span class="logic-hint">// Strategy: "Banking App" check is the ultimate CX grab—it stops the customer from hanging up.</span>
            </div>

            <div class="step-container" style="border-left-color: var(--danger);">
                <span class="step-tag">Step 11-12: Property & Commitment</span>
                <div class="dialogue-text">
                    "Perfect. Can I get your <strong>Full Name and Full Address</strong> for the files? <br><br>
                    You’re all set! Our specialist will bring your <span class="highlight">12-Month Price-Locked Estimate</span>. This is a 100% free technical report for your records. Do <strong>mornings or evenings</strong> work best for you and your spouse?"
                </div>
            </div>

        </div>

        <div class="panel" style="border-left: 1px solid #1e293b;">
            
            <div class="feature-card">
                <h4>💎 Why This Works (CX GRAB)</h4>
                <p style="font-size: 14px; color: var(--text-silver); line-height: 1.6;">
                    • <strong>The "Price Lock" Hook:</strong> Customers hate inflation. Telling them the price is locked for 1 year makes them feel safe.<br><br>
                    • <strong>The "Spouse" Importance:</strong> Never book without both! It avoids cancellations.<br><br>
                    • <strong>Energy Audit Tone:</strong> Speak like a technician, not a salesman.
                </p>
            </div>

            <div class="feature-card" style="border-color: var(--primary);">
                <h4>📝 Objection Handling</h4>
                <p style="font-size: 14px; color: var(--text-silver);">
                    <strong>"I'm not interested"</strong><br>
                    <em>"I understand! Most people aren't ready today, which is why we provide a 12-month quote. It's a free asset for your home's future value."</em>
                </p>
            </div>

            <div class="feature-card" style="background: rgba(16, 185, 129, 0.05); border-color: var(--success);">
                <h4>🔒 Legal Disclaimer</h4>
                <p style="font-size: 12px; line-height: 1.4; color: #94a3b8;">
                    "Today's date is [Date]. By confirming, you agree to a callback from our specialist, even if you are on the <strong>Do Not Call List</strong>. This is for your requested future estimate."
                </p>
            </div>

            <button class="cta-button">Confirm & Submit Lead</button>
        </div>
    </div>

    <div class="disclaimer-footer">
        PROPERTY OF PRIME SOLUTIONS USA | 2026 INTERNAL TRAINING DOCUMENT | CONFIDENTIAL
    </div>
</div>

</body>
</html>
