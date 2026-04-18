<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prime Solutions | Casual Friendly OS</title>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&family=JetBrains+Mono:wght@500&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary: #8b5cf6;
            --success: #10b981;
            --warning: #f59e0b;
            --bg: #020617;
            --glass: rgba(255, 255, 255, 0.04);
            --border: rgba(255, 255, 255, 0.1);
        }

        * { margin: 0; padding: 0; box-sizing: border-box; transition: 0.3s ease; }
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background: radial-gradient(circle at top right, #1e1b4b, #020617);
            color: #f1f5f9;
            padding: 20px;
            min-height: 100vh;
        }

        /* Modern Glass Header */
        header {
            background: var(--glass);
            backdrop-filter: blur(25px);
            border: 1px solid var(--border);
            border-radius: 35px;
            padding: 40px;
            text-align: center;
            margin-bottom: 30px;
        }

        header h1 {
            font-size: clamp(28px, 4vw, 48px);
            font-weight: 800; letter-spacing: 5px;
            background: linear-gradient(to right, #fff, #a78bfa);
            -webkit-background-clip: text; -webkit-text-fill-color: transparent;
        }

        /* Live Control Panel */
        .controls {
            display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 15px;
            margin-bottom: 30px; max-width: 1200px; margin-inline: auto;
        }
        .controls input {
            background: rgba(15, 23, 42, 0.8); border: 1px solid var(--border);
            padding: 15px; color: white; border-radius: 12px; outline: none;
        }
        .controls input:focus { border-color: var(--primary); }

        /* Chat Workspace */
        .workspace {
            display: grid; grid-template-columns: 2fr 1fr; gap: 25px;
            max-width: 1500px; margin: 0 auto;
        }

        @media (max-width: 1000px) { .workspace { grid-template-columns: 1fr; } }

        .chat-panel {
            background: rgba(15, 23, 42, 0.6);
            border-radius: 40px; border: 1px solid var(--border);
            padding: clamp(20px, 4vw, 45px);
        }

        /* Dialogue Box Styling */
        .chat-bubble {
            margin-bottom: 40px; padding: 25px;
            background: var(--glass); border-radius: 25px;
            border-left: 6px solid var(--primary);
            position: relative;
        }

        .chat-label {
            position: absolute; top: -12px; left: 30px;
            background: var(--primary); padding: 4px 12px;
            border-radius: 8px; font-size: 10px; font-weight: 800;
        }

        .text { font-size: clamp(18px, 2.5vw, 22px); line-height: 1.7; color: #cbd5e1; }
        .hl { color: var(--warning); font-weight: 800; }
        .tip { color: var(--success); font-weight: 600; font-size: 14px; margin-top: 15px; display: block; border-top: 1px solid var(--border); padding-top: 10px; }

        /* Side Tools */
        .sidebar { display: flex; flex-direction: column; gap: 20px; }
        .card { background: var(--glass); border: 1px solid var(--border); border-radius: 25px; padding: 25px; }

        .rebuttal {
            background: #020617; padding: 15px; border-radius: 15px;
            margin-bottom: 12px; border-left: 3px solid #f87171;
        }
        .rebuttal strong { font-size: 12px; color: #f87171; display: block; margin-bottom: 5px; }
        .rebuttal p { font-size: 14px; color: #94a3b8; }

        .btn {
            background: linear-gradient(135deg, var(--success), #059669);
            color: white; border: none; width: 100%;
            padding: 22px; border-radius: 18px; font-weight: 800;
            cursor: pointer; text-transform: uppercase; margin-top: 10px;
        }

        footer { text-align: center; padding: 40px; opacity: 0.3; font-size: 11px; }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1>PRIME SOLUTIONS</h1>
        <p style="opacity: 0.7; font-size: 12px; letter-spacing: 3px; margin-top: 10px;">NATURAL CONVERSATION ENGINE</p>
    </header>

    <div class="controls">
        <input type="text" id="ag" placeholder="Your Name..." onkeyup="sync()">
        <input type="text" id="cu" placeholder="Customer Name..." onkeyup="sync()">
        <input type="text" id="ci" placeholder="City..." onkeyup="sync()">
    </div>

    <div class="workspace">
        <div class="chat-panel">
            
            <div class="chat-bubble">
                <span class="chat-label">PHASE 1: THE VIBE CHECK</span>
                <div class="text">
                    "Hey <span class="hl cu">Customer</span>! How’s it going over in <span class="hl ci">City</span> today? <br><br>
                    Look, I won’t take much of your time. This isn’t one of those annoying sales calls—honestly, I'm just reaching out from <strong>Prime Solutions</strong> to let homeowners know about some <strong>crazy discounts</strong> we have for <span class="hl">future</span> window upgrades. <br><br>
                    Just checking in—are you the <strong>homeowner</strong> there?"
                </div>
                <span class="tip">💡 Pro Tip: Speak slowly, like you're just chillin'. No rush!</span>
            </div>

            <div class="chat-bubble" style="border-left-color: var(--warning);">
                <span class="chat-label">PHASE 2: TALKING WINDOWS</span>
                <div class="text">
                    "Nice! You know, we’re just offering <strong>free estimates</strong> that you can keep in your back pocket for later. <br><br>
                    Whenever you *do* decide to fix up those windows—maybe in a <strong>few months</strong> or even <strong>next year</strong>—you’ll already have the <strong>best market price</strong> locked in. <br><br>
                    Are we talking about <strong>5 to 10 windows</strong>, or is it a bigger project?"
                </div>
                <span class="tip">💡 Pro Tip: If they say 'not now', laugh and say 'Exactly! That's why I'm calling early!'</span>
            </div>

            <div class="chat-bubble" style="border-left-color: var(--success);">
                <span class="chat-label">PHASE 3: LOCKING THE DEAL</span>
                <div class="text">
                    "Totally get it. To make sure I get you the <strong>max discount</strong> (we have special ones for <span class="hl">Seniors and Veterans</span>), I just need to verify your <strong>ZIP and DOB</strong> real quick. <br><br>
                    This way, my specialist can just drop off a <strong>quick info-guide</strong> with the price locked for 12 months. <br><br>
                    Do you usually have a <strong>free moment in the mornings</strong>, or are afternoons better for a 2-minute drop off?"
                </div>
                <span class="tip">💡 Pro Tip: Keep it light. It's just a 'quick info-guide', not a 'meeting'.</span>
            </div>

        </div>

        <div class="sidebar">
            <div class="card">
                <h4 style="color: var(--success); margin-bottom: 20px; font-size: 14px;">FRIENDLY COMEBACKS</h4>
                
                <div class="rebuttal">
                    <strong>"I'm not interested."</strong>
                    <p>"Haha, I figured! Most people aren't ready *today*. That's why I'm just giving you the <strong>free info</strong> for the future. No pressure at all."</p>
                </div>

                <div class="rebuttal">
                    <strong>"I don't give my DOB."</strong>
                    <p>"Oh, no worries! It’s just because the state gives <strong>better rates</strong> to certain age groups. I just want to make sure you're not overpaying later!"</p>
                </div>

                <div class="rebuttal">
                    <strong>"Just mail it to me."</strong>
                    <p>"I wish I could, but these discounts are <strong>location-specific</strong>. My guy will just drop it off—takes 2 minutes, and then you can toss it in a drawer until you're ready!"</p>
                </div>
            </div>

            <div class="card" style="background: rgba(139, 92, 246, 0.1);">
                <p style="font-size: 13px; color: #a78bfa; line-height: 1.6;">
                    <strong>Remember Sweetie:</strong><br>
                    Don't sound like a robot. Use words like "Look," "Honestly," and "No biggie." Customer ko apna dost samjho!
                </p>
            </div>

            <button class="btn" onclick="alert('Friendly Lead Saved!')">Finish The Chat</button>
        </div>
    </div>

    <footer>
        PRIME SOLUTIONS | THE ART OF CONVERSATION © 2026
    </footer>
</div>

<script>
    function sync() {
        let ag = document.getElementById('ag').value || "Agent";
        let cu = document.getElementById('cu').value || "Customer";
        let ci = document.getElementById('ci').value || "City";

        document.querySelectorAll('.ag').forEach(e => e.innerText = ag);
        document.querySelectorAll('.cu').forEach(e => e.innerText = cu);
        document.querySelectorAll('.ci').forEach(e => e.innerText = ci);
    }
</script>

</body>
</html>
