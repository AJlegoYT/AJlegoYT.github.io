<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>LEGO Clone Trooper Clicker</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            user-select: none;
            -webkit-user-select: none;
            -moz-user-select: none;
            -ms-user-select: none;
            -webkit-tap-highlight-color: transparent;
        }
        
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            color: white;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            overflow-y: auto;
        }
        
        .credit {
            position: absolute;
            top: 10px;
            right: 10px;
            font-size: 0.7em;
            font-weight: bold;
            color: rgba(255,255,255,0.8);
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            letter-spacing: 1px;
            z-index: 100;
        }
        
        h1 {
            text-align: center;
            padding: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            font-size: clamp(1.2em, 5vw, 2em);
        }
        
        .container {
            display: flex;
            flex: 1;
            overflow: hidden;
            gap: 10px;
            padding: 10px;
        }
        
        .middle-display {
            flex: 2;
            background: rgba(255,255,255,0.15);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 20px;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(60px, 1fr));
            align-content: start;
            gap: 10px;
            overflow-y: auto;
            box-shadow: 0 8px 32px rgba(0,0,0,0.3);
            min-height: 200px;
        }
        
        .support-icon-display {
            position: static;
            width: 60px;
            height: 60px;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto;
        }
        
        .support-icon-display .icon {
            width: 100%;
            height: auto;
        }
        
        .support-icon-display .emoji-fallback {
            font-size: 2em;
        }
        
        .empty-message {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: rgba(255,255,255,0.5);
            font-size: 1.2em;
            text-align: center;
            width: 80%;
        }
        
        .more-troopers {
            position: absolute;
            bottom: 10px;
            left: 50%;
            transform: translateX(-50%);
            color: #ffd700;
            font-size: 1.5em;
            font-weight: bold;
            text-align: center;
            background: rgba(0,0,0,0.7);
            padding: 10px 20px;
            border-radius: 10px;
        }
        
        .support-icon-display .count {
            font-size: 1.5em;
            font-weight: bold;
            color: #ffd700;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
        }
        
        .clicker-section {
            background: rgba(255,255,255,0.1);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 15px;
            text-align: center;
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: space-around;
            box-shadow: 0 8px 32px rgba(0,0,0,0.3);
        }
        
        .counter {
            font-size: clamp(2em, 8vw, 3em);
            font-weight: bold;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
        }
        
        .brick {
            width: clamp(120px, 30vw, 180px);
            height: clamp(120px, 30vw, 180px);
            cursor: pointer;
            position: relative;
            margin: 10px auto;
            transition: transform 0.2s ease, filter 0.2s ease;
            filter: drop-shadow(0 5px 15px rgba(0,0,0,0.6));
            -webkit-user-drag: none;
        }
        
        .brick:hover {
            transform: scale(1.1);
            filter: drop-shadow(0 8px 25px rgba(100,200,255,0.8)) brightness(1.1);
        }
        
        .brick:active {
            transform: scale(0.95);
            filter: drop-shadow(0 3px 10px rgba(255,255,255,0.9)) brightness(1.2);
        }
        
        .helmet {
            width: 100%;
            height: 100%;
            position: relative;
        }

        /* ✅ Ensures helmet clicks always count */
        .helmet, .helmet-image, .helmet-image-fallback {
            width: 100%;
            height: 100%;
            object-fit: contain;
            pointer-events: none;
            -webkit-user-drag: none;
        }
        
        .helmet-image-fallback {
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 4em;
        }
        
        .stats {
            background: rgba(255,255,255,0.1);
            padding: 10px;
            border-radius: 10px;
            font-size: clamp(0.8em, 2.5vw, 1em);
        }
        
        .stat-line {
            margin: 5px 0;
        }
        
        .upgrades-container {
            flex: 1.5;
            display: flex;
            flex-direction: column;
            gap: 10px;
            overflow: hidden;
        }
        
        .upgrades-section {
            background: rgba(255,255,255,0.1);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 15px;
            flex: 1;
            display: flex;
            flex-direction: column;
            box-shadow: 0 8px 32px rgba(0,0,0,0.3);
            overflow: visible;
            position: relative;
        }
        
        .upgrades-section h2 {
            font-size: clamp(1em, 3vw, 1.5em);
            margin-bottom: 10px;
            text-align: center;
        }
        
        .upgrades-list {
            flex: 1;
            overflow-y: auto;
            overflow-x: visible;
            position: relative;
        }
        
        .upgrade {
            background: rgba(255,255,255,0.15);
            border-radius: 8px;
            padding: 10px;
            margin: 8px 0;
            cursor: pointer;
            transition: all 0.2s;
            border: 2px solid transparent;
            font-size: clamp(0.7em, 2vw, 0.9em);
            position: relative;
            display: flex;
            justify-content: space-between;
            align-items: center;
            z-index: 1;
        }
        
        .upgrade:hover {
            z-index: 100;
        }
        
        .upgrade:hover:not(.disabled) {
            background: rgba(255,255,255,0.25);
            border-color: #ffd700;
        }
        
        .upgrade.disabled {
            opacity: 0.5;
        }
        
        .upgrade-title {
            font-weight: bold;
            flex: 1;
        }
        
        .upgrade-details {
            display: none;
            position: absolute;
            top: calc(100% + 5px);
            right: 0;
            width: 220px;
            background: rgba(20,20,20,0.98);
            padding: 12px;
            border-radius: 8px;
            z-index: 1000;
            border: 2px solid #ffd700;
            box-shadow: 0 4px 20px rgba(0,0,0,0.8);
            color: white;
            white-space: normal;
        }
        
        .upgrade:hover .upgrade-details {
            display: block;
        }
        
        .upgrade-desc {
            opacity: 1;
            margin: 5px 0;
            font-size: 0.95em;
            color: #ffffff;
        }
        
        .upgrade-cost {
            color: #ffd700;
            font-weight: bold;
            font-size: 1.2em;
            margin-left: 10px;
        }
        
        .upgrade-owned {
            color: #90EE90;
            margin-top: 5px;
            font-size: 0.95em;
        }
        
        .support-upgrade {
            border-left: 3px solid #ffd700;
        }
        
        .trooper-icon {
            font-size: 2em;
        }
        
        @media (max-width: 768px) {
            .container {
                flex-direction: column;
            }
            
            .clicker-section {
                flex: 0 0 auto;
                max-height: 40vh;
            }
            
            .upgrades-container {
                flex-direction: row;
                flex: 1;
            }
            
            .middle-display {
                order: 3;
            }
            
            .upgrade-details {
                right: auto;
                left: calc(100% + 10px);
            }
        }
    </style>
</head>
<body>
    <div class="credit">MADE BY AJ LEGO</div>
    <h1>🧱 LEGO Clone Trooper Clicker 🧱</h1>
    
    <div class="container">
        <div class="clicker-section">
            <div class="trooper-icon">🪖</div>
            <div class="counter" id="trooperCount">0</div>
            <div style="font-size: clamp(0.9em, 2.5vw, 1.2em); margin: 5px 0;">Clone Troopers</div>
            
            <div class="brick" id="brick">
                <div class="helmet">
                    <img src="https://i.imgur.com/PjHMSnO.jpeg" 
                         alt="Clone Trooper Helmet" 
                         class="helmet-image"
                         onerror="this.style.display='none'; this.nextElementSibling.style.display='flex';">
                    <div class="helmet-image-fallback" style="display:none;">🪖</div>
                </div>
            </div>
            
            <div class="stats">
                <div class="stat-line">Per Click: <span id="perClick">1</span></div>
                <div class="stat-line">Per Second: <span id="perSecond">0</span></div>
            </div>
        </div>
        
        <div class="middle-display" id="middleDisplay"></div>
        
        <div class="upgrades-container">
            <div class="upgrades-section">
                <h2>🛠️ Support</h2>
                <div class="upgrades-list" id="supportContainer"></div>
            </div>
            
            <div class="upgrades-section">
                <h2>⬆️ Upgrades</h2>
                <div class="upgrades-list" id="upgradesContainer"></div>
            </div>
        </div>
    </div>

    <script>
    let totalTroopersProduced = 0;
    let troopers = 0;
    let clickPower = 1;
    let troopersPerSecond = 0;

    const brick = document.getElementById('brick');
    const helmet = document.querySelector('.helmet');
    const trooperCount = document.getElementById('trooperCount');
    const perClick = document.getElementById('perClick');
    const perSecond = document.getElementById('perSecond');
    const upgradesContainer = document.getElementById('supportContainer');
    const supportContainer = document.getElementById('upgradesContainer');
    const middleDisplay = document.getElementById('middleDisplay');

    // ✅ Function to add troopers when helmet/brick clicked
    function addTroopers() {
        troopers += clickPower;
        totalTroopersProduced += clickPower;
        updateDisplay();
        updateMiddleDisplayIfNeeded();
        updateUpgrades();
    }

    // ✅ Ensure clicks on either brick or helmet add troopers
    brick.addEventListener('click', addTroopers);
    helmet.addEventListener('click', addTroopers);

    // ... (your existing upgrade arrays and logic remain unchanged) ...
    // ⚠️ All your existing JS logic stays the same below this comment
    </script>
</body>
</html>
