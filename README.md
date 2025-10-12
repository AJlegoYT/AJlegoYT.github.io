Subscribe to AJLEGO on YouTube!        
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            color: white;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
        }
        
        h1 {
            margin: 20px 0;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            font-size: 2.5em;
        }
        
        .credit {
            position: absolute;
            top: 20px;
            right: 20px;
            font-size: 0.9em;
            font-weight: bold;
            color: rgba(255,255,255,0.8);
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
            letter-spacing: 1px;
        }
        
        .container {
            display: flex;
            gap: 30px;
            max-width: 1200px;
            width: 100%;
            flex-wrap: wrap;
            justify-content: center;
        }
        
        .clicker-section {
            background: rgba(255,255,255,0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 40px;
            text-align: center;
            flex: 1;
            min-width: 300px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.3);
        }
        
        .counter {
            font-size: 3em;
            font-weight: bold;
            margin: 20px 0;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
        }
        
        .brick {
            width: 200px;
            height: 200px;
            cursor: pointer;
            position: relative;
            margin: 30px auto;
            transition: transform 0.2s ease, filter 0.2s ease;
            filter: drop-shadow(0 10px 30px rgba(0,0,0,0.6));
            animation: idle-float 3s ease-in-out infinite;
            -webkit-user-drag: none;
        }
        
        @keyframes idle-float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-8px) rotate(2deg); }
        }
        
        .brick:hover {
            transform: scale(1.15) translateY(-10px) !important;
            filter: drop-shadow(0 15px 50px rgba(100,200,255,0.8)) 
                    drop-shadow(0 0 30px rgba(255,255,255,0.5))
                    brightness(1.1);
            animation: none;
        }
        
        .brick:active {
            transform: scale(0.92) !important;
            filter: drop-shadow(0 5px 15px rgba(255,255,255,0.9))
                    drop-shadow(0 0 20px rgba(100,200,255,1))
                    brightness(1.2);
            animation: none;
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
            background: radial-gradient(circle, rgba(255,255,255,0.1), transparent);
            pointer-events: none;
            -webkit-user-drag: none;
            -khtml-user-drag: none;
            -moz-user-drag: none;
            -o-user-drag: none;
            user-drag: none;
        }
        
        .helmet-image-fallback {
            width: 100%;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 4em;
        }
        
        .upgrades-section {
            background: rgba(255,255,255,0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            flex: 1;
            min-width: 300px;
            max-height: 600px;
            overflow-y: auto;
            box-shadow: 0 8px 32px rgba(0,0,0,0.3);
        }
        
        .upgrades-section h2 {
            margin-bottom: 20px;
            font-size: 1.8em;
        }
        
        .upgrade {
            background: rgba(255,255,255,0.15);
            border-radius: 10px;
            padding: 15px;
            margin: 15px 0;
            cursor: pointer;
            transition: all 0.3s;
            border: 2px solid transparent;
            user-select: none;
        }
        
        .upgrade:hover:not(.disabled) {
            background: rgba(255,255,255,0.25);
            border-color: #ffd700;
        }
        
        .upgrade.disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }
        
        .upgrade-title {
            font-size: 1.3em;
            font-weight: bold;
            margin-bottom: 5px;
        }
        
        .upgrade-desc {
            font-size: 0.9em;
            margin: 5px 0;
            opacity: 0.9;
        }
        
        .upgrade-cost {
            font-size: 1.1em;
            color: #ffd700;
            font-weight: bold;
            margin-top: 8px;
        }
        
        .upgrade-owned {
            font-size: 0.9em;
            color: #90EE90;
            margin-top: 5px;
        }
        
        .stats {
            background: rgba(255,255,255,0.1);
            padding: 15px;
            border-radius: 10px;
            margin-top: 20px;
        }
        
        .stat-line {
            margin: 8px 0;
            font-size: 1.1em;
        }
        
        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
        }
        
        .trooper-icon {
            font-size: 2em;
            animation: float 2s ease-in-out infinite;
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
            <div style="font-size: 1.2em; margin-bottom: 10px;">Clone Troopers</div>
            
            <div class="brick" id="brick">
                <div class="helmet">
                    <img src="https://i.imgur.com/PjHMSnO.jpeg" 
                         alt="Clone Trooper Helmet" 
                         class="helmet-image"
                         onload="console.log('Image loaded successfully'); this.style.display='block';"
                         onerror="console.log('Image failed to load'); this.style.display='none'; this.nextElementSibling.style.display='flex';">
                    <div class="helmet-image-fallback" style="display:none;">🪖</div>
                </div>
            </div>
            
            <div class="stats">
                <div class="stat-line">Per Click: <span id="perClick">1</span> troopers</div>
                <div class="stat-line">Per Second: <span id="perSecond">0</span> troopers</div>
            </div>
        </div>
        
        <div class="upgrades-section">
            <h2>🛠️ Support</h2>
            <div id="upgradesContainer"></div>
        </div>
    </div>

    <script>
        let totalTroopersProduced = 0;
        let troopers = 0;
        let clickPower = 1;
        let troopersPerSecond = 0;
        
        const upgrades = [
            {
                id: 'click1',
                name: 'Better Molds',
                desc: '+1 click power',
                baseCost: 15,
                cost: 15,
                owned: 0,
                effect: () => { clickPower += 1; },
                costMultiplier: 1.8
            },
            {
                id: 'auto1',
                name: 'Clone Cadets',
                desc: '+1 trooper per second',
                baseCost: 50,
                cost: 50,
                owned: 0,
                effect: () => {},
                costMultiplier: 1.5
            },
            {
                id: 'auto2',
                name: 'Training Facility',
                desc: '+5 troopers per second',
                baseCost: 300,
                cost: 300,
                owned: 0,
                effect: () => {},
                costMultiplier: 1.5
            },
            {
                id: 'click2',
                name: 'Advanced Assembly',
                desc: '+5 click power',
                baseCost: 1000,
                cost: 1000,
                owned: 0,
                effect: () => { clickPower += 5; },
                costMultiplier: 2
            },
            {
                id: 'auto3',
                name: 'Kamino Cloning Vats',
                desc: '+25 troopers per second',
                baseCost: 2000,
                cost: 2000,
                owned: 0,
                effect: () => {},
                costMultiplier: 1.5
            },
            {
                id: 'click3',
                name: 'Mass Production',
                desc: '+25 click power',
                baseCost: 10000,
                cost: 10000,
                owned: 0,
                effect: () => { clickPower += 25; },
                costMultiplier: 2.5
            },
            {
                id: 'auto4',
                name: 'Clone Army Factory',
                desc: '+100 troopers per second',
                baseCost: 15000,
                cost: 15000,
                owned: 0,
                effect: () => {},
                costMultiplier: 1.5
            },
            {
                id: 'auto5',
                name: 'Republic Armada',
                desc: '+500 troopers per second',
                baseCost: 75000,
                cost: 75000,
                owned: 0,
                effect: () => {},
                costMultiplier: 1.5
            }
        ];
        
        const supportUpgrades = [
            {
                id: 'support1',
                name: 'Efficient Training',
                desc: 'Clone Cadets produce 2x troopers',
                baseCost: 500,
                cost: 500,
                owned: 0,
                requires: 'auto1',
                revealAt: 100,
                upgradeId: 'auto1',
                baseBonus: 1,
                effect: () => {},
                costMultiplier: 10
            },
            {
                id: 'support2',
                name: 'Enhanced Facilities',
                desc: 'Training Facilities produce 2x troopers',
                baseCost: 3000,
                cost: 3000,
                owned: 0,
                requires: 'auto2',
                revealAt: 1000,
                upgradeId: 'auto2',
                baseBonus: 5,
                effect: () => {},
                costMultiplier: 10
            },
            {
                id: 'support3',
                name: 'Optimized Cloning',
                desc: 'Kamino Vats produce 2x troopers',
                baseCost: 20000,
                cost: 20000,
                owned: 0,
                requires: 'auto3',
                revealAt: 5000,
                upgradeId: 'auto3',
                baseBonus: 25,
                effect: () => {},
                costMultiplier: 10
            },
            {
                id: 'support4',
                name: 'Automated Production',
                desc: 'Clone Factories produce 2x troopers',
                baseCost: 150000,
                cost: 150000,
                owned: 0,
                requires: 'auto4',
                revealAt: 50000,
                upgradeId: 'auto4',
                baseBonus: 100,
                effect: () => {},
                costMultiplier: 10
            },
            {
                id: 'support5',
                name: 'Fleet Coordination',
                desc: 'Republic Armadas produce 2x troopers',
                baseCost: 750000,
                cost: 750000,
                owned: 0,
                requires: 'auto5',
                revealAt: 200000,
                upgradeId: 'auto5',
                baseBonus: 500,
                effect: () => {},
                costMultiplier: 10
            },
            {
                id: 'support6',
                name: 'Master Builder',
                desc: '+10 click power',
                baseCost: 15000,
                cost: 15000,
                owned: 0,
                requires: 'click2',
                revealAt: 2500,
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
        const upgradesContainer = document.getElementById('upgradesContainer');
        
        brick.addEventListener('click', () => {
            troopers += clickPower;
            totalTroopersProduced += clickPower;
            updateDisplay();
            updateUpgrades();
        });
        
        function buyUpgrade(upgrade) {
            if (troopers >= upgrade.cost) {
                troopers -= upgrade.cost;
                upgrade.owned++;
                upgrade.effect();
                upgrade.cost = Math.floor(upgrade.baseCost * Math.pow(upgrade.costMultiplier, upgrade.owned));
                troopersPerSecond = calculateTroopersPerSecond();
                updateDisplay();
                updateUpgrades();
            }
        }
        
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
        
        function buySupportUpgrade(upgrade) {
            if (troopers >= upgrade.cost) {
                troopers -= upgrade.cost;
                upgrade.owned++;
                upgrade.effect();
                upgrade.cost = Math.floor(upgrade.baseCost * Math.pow(upgrade.costMultiplier, upgrade.owned));
                troopersPerSecond = calculateTroopersPerSecond();
                updateDisplay();
                updateUpgrades();
            }
        }
        
        function renderUpgrades() {
            upgradesContainer.innerHTML = '';
            
            upgrades.forEach(upgrade => {
                const div = document.createElement('div');
                const canAfford = troopers >= upgrade.cost;
                div.className = 'upgrade' + (canAfford ? '' : ' disabled');
                div.innerHTML = `
                    <div class="upgrade-title">${upgrade.name}</div>
                    <div class="upgrade-desc">${upgrade.desc}</div>
                    <div class="upgrade-cost">Cost: ${upgrade.cost.toLocaleString()} troopers</div>
                    <div class="upgrade-owned">Owned: ${upgrade.owned}</div>
                `;
                
                if (canAfford) {
                    div.onclick = () => {
                        buyUpgrade(upgrade);
                    };
                }
                
                upgradesContainer.appendChild(div);
            });
            
            supportUpgrades.forEach(upgrade => {
                const requiredUpgrade = upgrades.find(u => u.id === upgrade.requires);
                const requirementMet = requiredUpgrade && requiredUpgrade.owned > 0;
                const trooperThresholdMet = totalTroopersProduced >= upgrade.revealAt;
                
                if (requirementMet && trooperThresholdMet) {
                    const div = document.createElement('div');
                    const canAfford = troopers >= upgrade.cost;
                    div.className = 'upgrade' + (canAfford ? '' : ' disabled');
                    div.style.borderLeft = '4px solid #ffd700';
                    div.innerHTML = `
                        <div class="upgrade-title">🛠️ ${upgrade.name}</div>
                        <div class="upgrade-desc">${upgrade.desc}</div>
                        <div class="upgrade-cost">Cost: ${upgrade.cost.toLocaleString()} troopers</div>
                        <div class="upgrade-owned">Owned: ${upgrade.owned}</div>
                    `;
                    
                    if (canAfford) {
                        div.onclick = () => {
                            buySupportUpgrade(upgrade);
                        };
                    }
                    
                    upgradesContainer.appendChild(div);
                }
            });
        }
        
        function updateDisplay() {
            trooperCount.textContent = Math.floor(troopers).toLocaleString();
            perClick.textContent = clickPower.toLocaleString();
            perSecond.textContent = troopersPerSecond.toLocaleString();
        }
        
        function updateUpgrades() {
            renderUpgrades();
        }
        
        let lastAffordableState = [...upgrades, ...supportUpgrades].map(u => troopers >= u.cost);
        
        let lastUpdateTime = Date.now();
        setInterval(() => {
            const generated = troopersPerSecond / 10;
            troopers += generated;
            totalTroopersProduced += generated;
            const now = Date.now();
            if (now - lastUpdateTime >= 100) {
                updateDisplay();
                
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
    </script>
</body>
</html>
