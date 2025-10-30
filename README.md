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
            height: 100vh;
            display: flex;
            flex-direction: column;
            overflow: hidden;
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
            position: relative;
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
        
        .fact-popup {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%) translateY(150%);
            background: linear-gradient(135deg, rgba(255,215,0,0.95), rgba(255,165,0,0.95));
            color: #000;
            padding: 15px 25px;
            border-radius: 12px;
            font-size: 0.9em;
            font-weight: bold;
            text-align: center;
            max-width: 400px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.6);
            border: 3px solid #ffd700;
            z-index: 1000;
            animation: slideUp 0.5s ease-out forwards, slideDown 0.5s ease-in 4.5s forwards;
        }
        
        @keyframes slideUp {
            to {
                transform: translateX(-50%) translateY(0);
            }
        }
        
        @keyframes slideDown {
            to {
                transform: translateX(-50%) translateY(150%);
            }
        }
        
        .fact-name {
            font-size: 1.2em;
            margin-bottom: 5px;
            text-shadow: 1px 1px 2px rgba(255,255,255,0.5);
        }
        
        .fact-detail {
            font-size: 0.85em;
            opacity: 0.9;
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
        
        .helmet-image {
            width: 100%;
            height: 100%;
            object-fit: contain;
            filter: contrast(1.1) saturate(1.1);
            pointer-events: none;
            -webkit-user-drag: none;
        }
        
        .helmet-image-fallback {
            width: 100%;
            height: 100%;
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
            
            .fact-popup {
                max-width: 90%;
                font-size: 0.8em;
            }
        }
    </style>
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
        let characters = [];
        let currentFactPopup = null;
        
        // Fallback character data
        const fallbackCharacters = [
            {"name":"Luke Skywalker","gender":"male","hair_color":"blond","height":"172","eye_color":"blue","birth_year":"19BBY"},
            {"name":"Darth Vader","gender":"male","hair_color":"none","height":"202","eye_color":"yellow","birth_year":"41.9BBY"},
            {"name":"Leia Organa","gender":"female","hair_color":"brown","height":"150","eye_color":"brown","birth_year":"19BBY"},
            {"name":"Obi-Wan Kenobi","gender":"male","hair_color":"auburn, white","height":"182","eye_color":"blue-gray","birth_year":"57BBY"},
            {"name":"Yoda","gender":"male","hair_color":"white","height":"66","eye_color":"brown","birth_year":"896BBY"},
            {"name":"Han Solo","gender":"male","hair_color":"brown","height":"180","eye_color":"brown","birth_year":"29BBY"},
            {"name":"Chewbacca","gender":"male","hair_color":"brown","height":"228","eye_color":"blue","birth_year":"200BBY"},
            {"name":"Anakin Skywalker","gender":"male","hair_color":"blond","height":"188","eye_color":"blue","birth_year":"41.9BBY"},
            {"name":"Palpatine","gender":"male","hair_color":"grey","height":"170","eye_color":"yellow","birth_year":"82BBY"},
            {"name":"Padmé Amidala","gender":"female","hair_color":"brown","height":"185","eye_color":"brown","birth_year":"46BBY"},
            {"name":"Mace Windu","gender":"male","hair_color":"none","height":"188","eye_color":"brown","birth_year":"72BBY"},
            {"name":"Qui-Gon Jinn","gender":"male","hair_color":"brown","height":"193","eye_color":"blue","birth_year":"92BBY"},
            {"name":"Boba Fett","gender":"male","hair_color":"black","height":"183","eye_color":"brown","birth_year":"31.5BBY"},
            {"name":"Lando Calrissian","gender":"male","hair_color":"black","height":"177","eye_color":"brown","birth_year":"31BBY"},
            {"name":"C-3PO","gender":"n/a","hair_color":"n/a","height":"167","eye_color":"yellow","birth_year":"112BBY"},
            {"name":"R2-D2","gender":"n/a","hair_color":"n/a","height":"96","eye_color":"red","birth_year":"33BBY"},
            {"name":"Darth Maul","gender":"male","hair_color":"none","height":"175","eye_color":"yellow","birth_year":"54BBY"},
            {"name":"Jango Fett","gender":"male","hair_color":"black","height":"183","eye_color":"brown","birth_year":"66BBY"},
            {"name":"Dooku","gender":"male","hair_color":"white","height":"193","eye_color":"brown","birth_year":"102BBY"},
            {"name":"Rey","gender":"female","hair_color":"brown","height":"170","eye_color":"hazel","birth_year":"15ABY"},
            {"name":"Finn","gender":"male","hair_color":"black","height":"178","eye_color":"brown","birth_year":"unknown"},
            {"name":"Poe Dameron","gender":"male","hair_color":"black","height":"176","eye_color":"brown","birth_year":"2ABY"}
        ];
        
        // Fetch Star Wars characters
        async function loadCharacters() {
            try {
                const response = await fetch('https://swapi.online/api/characters');
                const data = await response.json();
                characters = data;
                console.log('✅ Loaded', characters.length, 'Star Wars characters from API!');
            } catch (error) {
                console.log('⚠️ API fetch failed, using fallback character data');
                characters = fallbackCharacters;
            }
        }
        
        loadCharacters();
        
        // Show random character fact
        function showCharacterFact() {
            if (characters.length === 0) return;
            
            // Remove existing popup if any
            if (currentFactPopup) {
                currentFactPopup.remove();
            }
            
            const randomChar = characters[Math.floor(Math.random() * characters.length)];
            
            const popup = document.createElement('div');
            popup.className = 'fact-popup';
            
            const details = [];
            if (randomChar.birth_year && randomChar.birth_year !== 'unknown') {
                details.push(`Born: ${randomChar.birth_year}`);
            }
            if (randomChar.height && randomChar.height !== 'unknown') {
                details.push(`Height: ${randomChar.height}cm`);
            }
            if (randomChar.gender && randomChar.gender !== 'unknown' && randomChar.gender !== 'n/a') {
                details.push(`Gender: ${randomChar.gender}`);
            }
            if (randomChar.hair_color && randomChar.hair_color !== 'n/a' && randomChar.hair_color !== 'unknown') {
                details.push(`Hair: ${randomChar.hair_color}`);
            }
            if (randomChar.eye_color && randomChar.eye_color !== 'unknown') {
                details.push(`Eyes: ${randomChar.eye_color}`);
            }
            
            popup.innerHTML = `
                <div class="fact-name">⭐ ${randomChar.name} ⭐</div>
                <div class="fact-detail">${details.slice(0, 2).join(' • ')}</div>
            `;
            
            document.body.appendChild(popup);
            currentFactPopup = popup;
            
            // Remove after animation completes
            setTimeout(() => {
                if (popup.parentNode) {
                    popup.remove();
                }
                currentFactPopup = null;
            }, 5000);
        }
        
        const upgrades = [
            {
                id: 'click1',
                name: 'Better Molds',
                desc: '+1 click power',
                baseCost: 10,
                cost: 10,
                owned: 0,
                effect: () => { clickPower += 1; },
                costMultiplier: 1.5
            },
            {
                id: 'auto1',
                name: 'Clone Cadets',
                desc: '+1 trooper/sec',
                baseCost: 25,
                cost: 25,
                owned: 0,
                effect: () => {},
                costMultiplier: 1.3
            },
            {
                id: 'auto2',
                name: 'Training Facility',
                desc: '+5 troopers/sec',
                baseCost: 150,
                cost: 150,
                owned: 0,
                effect: () => {},
                costMultiplier: 1.3
            },
            {
                id: 'click2',
                name: 'Advanced Assembly',
                desc: '+5 click power',
                baseCost: 500,
                cost: 500,
                owned: 0,
                effect: () => { clickPower += 5; },
                costMultiplier: 1.6
            },
            {
                id: 'auto3',
                name: 'Kamino Cloning Vats',
                desc: '+25 troopers/sec',
                baseCost: 1000,
                cost: 1000,
                owned: 0,
                effect: () => {},
                costMultiplier: 1.3
            },
            {
                id: 'click3',
                name: 'Mass Production',
                desc: '+25 click power',
                baseCost: 5000,
                cost: 5000,
                owned: 0,
                effect: () => { clickPower += 25; },
                costMultiplier: 1.8
            },
            {
                id: 'auto4',
                name: 'Clone Army Factory',
                desc: '+100 troopers/sec',
                baseCost: 7500,
                cost: 7500,
                owned: 0,
                effect: () => {},
                costMultiplier: 1.3
            },
            {
                id: 'auto5',
                name: 'Republic Armada',
                desc: '+500 troopers/sec',
                baseCost: 40000,
                cost: 40000,
                owned: 0,
                effect: () => {},
                costMultiplier: 1.3
            }
        ];
        
        const supportUpgrades = [
            {
                id: 'support1',
                name: 'Efficient Training',
                desc: 'Clone Cadets 2x',
                icon: '🎓',
                baseCost: 250,
                cost: 250,
                owned: 0,
                requires: 'auto1',
                revealAt: 100,
                upgradeId: 'auto1',
                effect: () => {},
                costMultiplier: 8
            },
            {
                id: 'support2',
                name: 'Enhanced Facilities',
                desc: 'Training Facilities 2x',
                icon: '🏢',
                baseCost: 1500,
                cost: 1500,
                owned: 0,
                requires: 'auto2',
                revealAt: 500,
                upgradeId: 'auto2',
                effect: () => {},
                costMultiplier: 8
            },
            {
                id: 'support3',
                name: 'Optimized Cloning',
                desc: 'Kamino Vats 2x',
                icon: '🧬',
                baseCost: 10000,
                cost: 10000,
                owned: 0,
                requires: 'auto3',
                revealAt: 2500,
                upgradeId: 'auto3',
                effect: () => {},
                costMultiplier: 8
            },
            {
                id: 'support4',
                name: 'Automated Production',
                desc: 'Clone Factories 2x',
                icon: '🏭',
                baseCost: 75000,
                cost: 75000,
                owned: 0,
                requires: 'auto4',
                revealAt: 25000,
                upgradeId: 'auto4',
                effect: () => {},
                costMultiplier: 8
            },
            {
                id: 'support5',
                name: 'Fleet Coordination',
                desc: 'Republic Armadas 2x',
                icon: '🚀',
                baseCost: 400000,
                cost: 400000,
                owned: 0,
                requires: 'auto5',
                revealAt: 100000,
                upgradeId: 'auto5',
                effect: () => {},
                costMultiplier: 8
            },
            {
                id: 'support6',
                name: 'Master Builder',
                desc: '+10 click power',
                icon: '🔨',
                baseCost: 7500,
                cost: 7500,
                owned: 0,
                requires: 'click2',
                revealAt: 1250,
                effect: () => { 
                    clickPower += 10;
                },
                costMultiplier: 3
            }
        ];
        
        const brick = document.getElementById('brick');
        const trooperCount = document.getElementById('trooperCount');
        const perClick = document.getElementById('perClick');
        const perSecond = document.getElementById('perSecond');
        const upgradesContainer = document.getElementById('supportContainer');
        const supportContainer = document.getElementById('upgradesContainer');
        const middleDisplay = document.getElementById('middleDisplay');
        
        brick.addEventListener('click', () => {
            troopers += clickPower;
            totalTroopersProduced += clickPower;
            updateDisplay();
            updateMiddleDisplayIfNeeded();
            updateUpgrades();
        });
        
        function calculateTroopersPerSecond() {
            let total = 0;
            
            upgrades.forEach(upgrade => {
                if (upgrade.id.startsWith('auto')) {
                    let multiplier = 1;
                    
                    supportUpgrades.forEach(support => {
                        if (support.upgradeId === upgrade.id && support.owned > 0) {
                            multiplier *= Math.pow(2, support.owned);
                        }
                    });
                    
                    if (upgrade.id === 'auto1') total += upgrade.owned * 1 * multiplier;
                    else if (upgrade.id === 'auto2') total += upgrade.owned * 5 * multiplier;
                    else if (upgrade.id === 'auto3') total += upgrade.owned * 25 * multiplier;
                    else if (upgrade.id === 'auto4') total += upgrade.owned * 100 * multiplier;
                    else if (upgrade.id === 'auto5') total += upgrade.owned * 500 * multiplier;
                }
            });
            
            return total;
        }
        
        function buyUpgrade(upgrade) {
            if (troopers >= upgrade.cost) {
                troopers -= upgrade.cost;
                upgrade.owned++;
                upgrade.effect();
                upgrade.cost = Math.floor(upgrade.baseCost * Math.pow(upgrade.costMultiplier, upgrade.owned));
                troopersPerSecond = calculateTroopersPerSecond();
                updateDisplay();
                updateMiddleDisplayIfNeeded();
                updateUpgrades();
                
                // Show character fact on major upgrades
                if (upgrade.owned === 1 || upgrade.owned % 5 === 0) {
                    showCharacterFact();
                }
            }
        }
        
        function buySupportUpgrade(upgrade) {
            if (troopers >= upgrade.cost) {
                troopers -= upgrade.cost;
                upgrade.owned++;
                upgrade.effect();
                upgrade.cost = Math.floor(upgrade.baseCost * Math.pow(upgrade.costMultiplier, upgrade.owned));
                troopersPerSecond = calculateTroopersPerSecond();
                updateDisplay();
                updateMiddleDisplayIfNeeded();
                updateUpgrades();
                
                // Always show character fact on support upgrades
                showCharacterFact();
            }
        }
        
        function renderUpgrades() {
            upgradesContainer.innerHTML = '';
            supportContainer.innerHTML = '';
            
            upgrades.forEach(upgrade => {
                const div = document.createElement('div');
                const canAfford = troopers >= upgrade.cost;
                div.className = 'upgrade' + (canAfford ? '' : ' disabled');
                
                const icon = upgrade.id.includes('click') ? '👆' : '⚙️';
                
                div.innerHTML = `
                    <div class="upgrade-title">${icon} ${upgrade.name}</div>
                    <div class="upgrade-cost">${upgrade.cost.toLocaleString()}</div>
                    <div class="upgrade-details">
                        <div class="upgrade-desc">${upgrade.desc}</div>
                        <div class="upgrade-owned">Owned: ${upgrade.owned}</div>
                    </div>
                `;
                
                div.onclick = () => {
                    if (canAfford) {
                        buyUpgrade(upgrade);
                    }
                };
                
                upgradesContainer.appendChild(div);
            });
            
            supportUpgrades.forEach(upgrade => {
                const requiredUpgrade = upgrades.find(u => u.id === upgrade.requires);
                const requirementMet = requiredUpgrade && requiredUpgrade.owned > 0;
                const trooperThresholdMet = totalTroopersProduced >= upgrade.revealAt;
                
                if (requirementMet && trooperThresholdMet) {
                    const div = document.createElement('div');
                    const canAfford = troopers >= upgrade.cost;
                    div.className = 'upgrade support-upgrade' + (canAfford ? '' : ' disabled');
                    div.innerHTML = `
                        <div class="upgrade-title">${upgrade.icon} ${upgrade.name}</div>
                        <div class="upgrade-cost">${upgrade.cost.toLocaleString()}</div>
                        <div class="upgrade-details">
                            <div class="upgrade-desc">${upgrade.desc}</div>
                            <div class="upgrade-owned">Owned: ${upgrade.owned}</div>
                        </div>
                    `;
                    
                    div.onclick = () => {
                        if (canAfford) {
                            buySupportUpgrade(upgrade);
                        }
                    };
                    
                    supportContainer.appendChild(div);
                }
            });
        }
        
        function renderMiddleDisplay() {
            middleDisplay.innerHTML = '';
            
            let totalGear = 0;
            supportUpgrades.forEach(upgrade => {
                totalGear += upgrade.owned;
            });
            
            if (totalGear === 0) {
                const emptyDiv = document.createElement('div');
                emptyDiv.style.cssText = 'grid-column: 1/-1; color: rgba(255,255,255,0.5); font-size: 1.2em; text-align: center; padding: 40px;';
                emptyDiv.textContent = 'Purchase Support upgrades to see your gear here!';
                middleDisplay.appendChild(emptyDiv);
            } else {
                supportUpgrades.forEach(upgrade => {
                    for (let i = 0; i < upgrade.owned; i++) {
                        const gearDiv = document.createElement('div');
                        gearDiv.className = 'support-icon-display';
                        gearDiv.innerHTML = `<div class="emoji-fallback">${upgrade.icon}</div>`;
                        middleDisplay.appendChild(gearDiv);
                    }
                });
            }
        }
        
        function updateDisplay() {
            trooperCount.textContent = Math.floor(troopers).toLocaleString();
            perClick.textContent = clickPower.toLocaleString();
            perSecond.textContent = troopersPerSecond.toLocaleString();
        }
        
        function updateMiddleDisplayIfNeeded() {
            renderMiddleDisplay();
        }
        
        function updateUpgrades() {
            renderUpgrades();
        }
        
        let lastAffordableState = [...upgrades, ...supportUpgrades].map(u => troopers >= u.cost);
        
        // Show random facts periodically
        setInterval(() => {
            if (troopers >= 50 && Math.random() < 0.3) {
                showCharacterFact();
            }
        }, 15000);
        
        let lastUpdateTime = Date.now();
        setInterval(() => {
            const generated = troopersPerSecond / 10;
            troopers += generated;
            totalTroopersProduced += generated;
            const now = Date.now();
            if (now - lastUpdateTime >= 100) {
                updateDisplay();
                updateMiddleDisplayIfNeeded();
                
                const currentAffordableState = [...upgrades, ...supportUpgrades].map(u => troopers >= u.cost);
                const stateChanged = currentAffordableState.some((state, i) => state !== lastAffordableState[i]);
                
                if (stateChanged) {
                    updateUpgrades();
                    lastAffordableState = currentAffordableState;
                }
                
                lastUpdateTime = now;
            }
        }, 100);
        
        updateDisplay();
        renderMiddleDisplay();
    </script>
</body>
</html>
