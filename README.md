<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Master Script Dashboard | Prime Solutions USA</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #4f46e5;
            --success: #10b981;
            --accent: #f59e0b;
            --dark: #0f172a;
            --card: #1e293b;
        }

        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: var(--dark);
            color: #f8fafc;
            margin: 0;
            padding: 20px;
        }

        .dashboard {
            max-width: 1100px;
            margin: 0 auto;
            background: var(--card);
            border-radius: 24px;
            overflow: hidden;
            border: 1px solid #334155;
            box-shadow: 0 50px 100px -20px rgba(0,0,0,0.5);
        }

        header {
            background: linear-gradient(135deg, #312e81 0%, #4f46e5 100%);
            padding: 30px;
            text-align: center;
            border-bottom: 4px solid var(--accent);
        }

        header h1 { margin: 0; font-size: 24px; text-transform: uppercase; letter-spacing: 2px; }
        header p { color: var(--accent); margin-top: 5px; font-weight: 600; font-size: 14px; }

        .main-layout {
            display: grid;
            grid-template-columns: 1.6fr 1fr;
            gap: 2px;
            background: #334155;
        }

        .script-panel, .tools-panel { background: var(--card); padding: 30px; }

        .step-box {
            margin-bottom: 30px;
            padding-left: 20px;
            border-left: 4px solid var(--primary);
            position: relative;
        }

        .step-label {
            background: var(--primary);
            color: white;
            padding: 3px 10px;
            border-radius: 4px;
            font-size: 10px;
            font-weight: 800;
            text-transform: uppercase;
            margin-bottom: 10px;
            display: inline-block;
        }

        .dialogue {
            font-size: 17px;
            line-height: 1.6;
            color: #e2e8f0;
        }

        .highlight { color: var(--accent); font-weight: 700; }

        /* Sidebar Tools */
        .tool-card {
            background: rgba(15, 23, 42, 0.5);
            padding: 15px;
            border-radius: 12px;
            margin-bottom: 15px;
            border: 1px solid #334155;
        }

        .tool-card h4 { color: var(--success); margin: 0 0 10px 0; font-size: 13px; text-transform: uppercase; }

        .btn-status {
            background: var(--success);
            color: white;
            width: 100%;
            border: none;
            padding: 15px;
            border-radius: 10px;
            font-weight: 800;
            margin-top: 10px;
        }

        .disclaimer-text {
            font-size: 11px;
            color: #94a3b8;
            font-style: italic;
            line-height: 1.4;
            margin-top: 20px;
            padding: 15px;
            background: rgba(0,0,0,0.2);
            border-radius: 8px;
        }

        .grab-point { color: #38bdf8; font-weight: 600; }
    </style>
</head>
<body>

<div class="dashboard">
    <header>
        <h1>USA Window Solutions Master Script</h1>
        <p>12-Step Complete Customer Qualification & Closing System</p>
    </header>

    <div class="main-layout">
        <div class="script-panel">
            
            <div class="step-box">
                <span class="step-label">Step 1 & 2: Opening & Interest</span>
                <div class="dialogue">
                    "Hi, this is [Your Name] calling regarding home improvement services. How are you today? <br><br>
                    We’re offering <span class="highlight">free window estimates</span> in your area for homeowners looking to upgrade or replace their windows. Just wanted to see if you might be interested in a zero-cost quote?"
                </div>
            </div>

            <div class="step-box" style="border-left-color: var(--accent);">
                <span class="step-label">Step 3 - 5: Requirement & Qualification</span>
                <div class="dialogue">
                    "Perfect! To make sure we match the right specialist—are you the <strong>homeowner</strong>? <br><br>
                    Roughly <strong>how many windows</strong> are you looking to get done—around 5 to 10, or more? And do you prefer <span class="highlight">Sliding, Casement, or Aluminum</span> windows? <br><br>
                    Excellent. May I have your <strong>ZIP code</strong> to check the local 2026 rebate rates?"
                </div>
            </div>

            <div class="step-box" style="border-left-color: var(--success);">
                <span class="step-label">Step 6 - 9: Financing & Urgency</span>
                <div class="dialogue">
                    "To match you with the best <span class="highlight">0% down financing</span>, what is your Date of Birth? <br><br>
                    Are you looking to start this project <span class="highlight">this month, next month</span>, or just building a budget? Have you received any other estimates yet? <br><br>
                    For the best rates, what range does your credit score sit in? Most people check their banking app—I can wait a second while you grab that range."
                </div>
            </div>

            <div class="step-box" style="border-left-color: #f43f5e;">
                <span class="step-label">Step 10 - 12: Final Lock & Booking</span>
                <div class="dialogue">
                    "Any mortgage modifications recently? No? Great. <br><br>
                    Let's get your <strong>Full Name and Property Address</strong>. You're all set! Our specialist will provide a <span class="highlight">12-Month Price-Locked Estimate</span>. Do mornings or evenings work best for you and your spouse?"
                </div>
            </div>

        </div>

        <div class="tools-panel">
            <div class="tool-card">
                <h4>🎯 Why They Will Say YES</h4>
                <p style="font-size: 13px; line-height: 1.5;">
                    • <span class="grab-point">Free Information:</span> It's a "No-Cost" future roadmap.<br>
                    • <span class="grab-point">Price Lock:</span> Quote is valid for 1 year, protecting them from inflation.<br>
                    • <span class="grab-point">Consultative:</span> We sound like advisors, not salesmen.
                </p>
            </div>

            <div class="tool-card">
                <h4>⚠️ Legal Disclaimer</h4>
                <div class="disclaimer-text">
                    "Today’s date is [Date]. One of our window specialists will give you a quick callback shortly to finalize the time. By confirming, you agree to receive this call even if your number is on a <strong>Do Not Call List</strong>."
                </div>
            </div>

            <div class="tool-card" style="border-color: var(--primary);">
                <h4>📋 Quality Control</h4>
                <ul style="padding-left: 15px; font-size: 12px; margin: 0;">
                    <li>Confirm BOTH Spouses present</li>
                    <li>Set 20-minute expectation</li>
                    <li>Must be 21+ for financing</li>
                </ul>
            </div>

            <button class="btn-status">SUBMIT LEAD NOW</button>
        </div>
    </div>
</div>

</body>
</html>
