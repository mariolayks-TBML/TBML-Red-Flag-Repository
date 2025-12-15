 <div id="snowflakes"></div>
    
    <div class="container">
        <div class="header">
            <h1 class="title">🎄 TBML CHRISTMAS GIFT VALUATION CHALLENGE 🎁</h1></p>
        
        </div>
        
        <div class="game-section">
            <div class="instruction-box">
                <h2>🎯 The Game</h2>
                <p><strong>You are Santa's Compliance Officer.</strong> Below are 5 "Christmas Gift" imports to the North Pole from various countries. Your job: assign <strong>realistic invoice prices</strong> for each gift.</p>
                <p>⚠️ But here's the twist: <strong>Some traders DELIBERATELY misprice goods to launder cash.</strong></p>
                <p>Your invoice valuations are judged against <strong>market reality</strong>. Huge deviations trigger red flags! 🚩</p>
            </div>
            
            <div id="gifts-container"></div>
            
            <div class="control-panel">
                <button class="btn btn-submit" onclick="calculateResults()">SUBMIT VALUES & SHOW RED FLAGS 🚨</button>
                <button class="btn btn-reset" onclick="resetGame()">START OVER</button>
            </div>
        </div>
        
        <div id="results" class="results-section">
            <h2 style="color: var(--color-red); text-align: center;">📊 COMPLIANCE AUDIT RESULTS</h2>
            
            <div id="results-content"></div>
        </div>
        
        <div class="footer">
            <p>🎅 <strong>Meva Private Christmas Edition by Dr Mariola Marzouk</strong> | Trade-Based Money Laundering Detection Game</p>
            <p>Data sourced from FATF (2006-2023), FinCEN advisories, Zdanowicz research, and actual TBML case studies.</p>
        </div>
    </div>

    <script>
        // Gift data with real-world TBML typologies
        const gifts = [
            {
                id: 1,
                name: "🎁 Decorative Gold Watches",
                emoji: "⌚",
                country: "China",
                quantity: 500,
                realMarketPrice: 12.50, // per unit USD
                highRiskScenario: "UNDERVALUED EXPORT - Seller invoices at $0.50 each, pockets $6,000 in laundered cash elsewhere",
                lowRiskScenario: "Normal market pricing, legitimate Xmas decoration import"
            },
            {
                id: 2,
                name: "🧥 Luxury Winter Scarves",
                emoji: "🧣",
                country: "Italy",
                quantity: 200,
                realMarketPrice: 45.00, // per unit USD
                highRiskScenario: "OVERVALUED IMPORT - Invoiced at $450/each (10x actual cost), money ends up in criminal proceeds",
                lowRiskScenario: "Legitimate high-end fashion pricing for premium Italian goods"
            },
            {
                id: 3,
                name: "💎 Precious Metal Ingots (Gold)",
                emoji: "🏆",
                country: "UAE/Dubai",
                quantity: 50,
                realMarketPrice: 2000.00, // per unit (spot + 5% markup)
                highRiskScenario: "UNDERVALUED EXPORT - Priced at $100/unit to hide $95,000 outflow, matches Palermo Mafia case typology",
                lowRiskScenario: "Standard commodity import at current spot price"
            },
            {
                id: 4,
                name: "🚜 Industrial Smelting Equipment",
                emoji: "⚙️",
                country: "Germany",
                quantity: 5,
                realMarketPrice: 8500.00, // per unit USD
                highRiskScenario: "OVERVALUED IMPORT - Invoiced at $85,000/unit (10x cost), creates fake expense for money laundering",
                lowRiskScenario: "Normal German engineering equipment pricing"
            },
            {
                id: 5,
                name: "🌟 Unspecified 'Miscellaneous Electronics'",
                emoji: "📦",
                country: "Hong Kong",
                quantity: 1000,
                realMarketPrice: 3.50, // per unit USD
                highRiskScenario: "VAGUE DESCRIPTION + MISPRICE - Classic shell company tactic: generic goods, impossible to verify",
                lowRiskScenario: "Legitimate bulk electronics import at competitive Asian pricing"
            }
        ];
        
        // Initialize game
        function initGame() {
            const container = document.getElementById('gifts-container');
            container.innerHTML = '';
            
            gifts.forEach(gift => {
                const giftHtml = `
                    <div class="gift-item">
                        <div class="gift-info">
                            <div class="gift-name">${gift.emoji} ${gift.name}</div>
                            <div class="gift-market">📍 From: <strong>${gift.country}</strong> | Qty: <strong>${gift.quantity} units</strong></div>
                            <div class="gift-market">📊 Real Market Price: <strong>$${gift.realMarketPrice.toFixed(2)} per unit</strong></div>
                            <div class="gift-hint">⚠️ TBML Risk: ${gift.highRiskScenario.substring(0, 60)}...</div>
                        </div>
                        <div class="input-group">
                            <input type="number" 
                                   id="price-${gift.id}" 
                                   placeholder="Your $ value/unit"
                                   step="0.01"
                                   min="0"
                                   style="width: 120px;">
                        </div>
                    </div>
                `;
                container.innerHTML += giftHtml;
            });
        }
        
        // Calculate results
        function calculateResults() {
            const resultsDiv = document.getElementById('results');
            const resultsContent = document.getElementById('results-content');
            
            let totalDeviationScore = 0;
            let flaggedItems = 0;
            let resultsHTML = '';
            
            gifts.forEach(gift => {
                const inputValue = parseFloat(document.getElementById(`price-${gift.id}`).value);
                
                if (!inputValue) {
                    alert('⚠️ Please enter prices for ALL gifts!');
                    return;
                }
                
                const deviation = Math.abs((inputValue - gift.realMarketPrice) / gift.realMarketPrice) * 100;
                const totalInvoice = inputValue * gift.quantity;
                const realMarketTotal = gift.realMarketPrice * gift.quantity;
                const moneySuspicious = Math.abs(totalInvoice - realMarketTotal);
                
                totalDeviationScore += deviation;
                
                let riskLevel = "✅ NORMAL";
                let flagColor = "green";
                let isFlag = false;
                
                if (deviation > 50) {
                    riskLevel = "🚩 HIGH RISK";
                    flagColor = "red";
                    flaggedItems++;
                    isFlag = true;
                } else if (deviation > 25) {
                    riskLevel = "⚠️ MEDIUM RISK";
                    flagColor = "orange";
                }
                
                resultsHTML += `
                    <div class="result-card" style="border-left: 5px solid ${flagColor};">
                        <div class="result-title">${gift.name}</div>
                        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin: 10px 0;">
                            <div>
                                <div class="stat-label">Your Invoice Price (per unit)</div>
                                <div class="stat-number" style="color: ${flagColor};">$${inputValue.toFixed(2)}</div>
                            </div>
                            <div>
                                <div class="stat-label">Market Reality (per unit)</div>
                                <div class="stat-number" style="color: var(--color-green);">$${gift.realMarketPrice.toFixed(2)}</div>
                            </div>
                        </div>
                        <div style="margin: 10px 0; padding: 10px; background: rgba(0,0,0,0.05); border-radius: 5px;">
                            <strong>Deviation: ${deviation.toFixed(1)}%</strong> | 
                            <strong style="color: ${flagColor};">${riskLevel}</strong> | 
                            💰 <strong>${moneySuspicious > 0 ? `$${moneySuspicious.toFixed(2)} unaccounted` : 'No major gap'}</strong>
                        </div>
                        ${isFlag ? `<div class="fraud-indicator">
                            <h4>🚨 RED FLAG DETECTED</h4>
                            <p><strong>Why This Matters:</strong> ${gift.highRiskScenario}</p>
                        </div>` : ''}
                    </div>
                `;
            });
            
            const avgDeviation = totalDeviationScore / gifts.length;
            let overallRisk = "✅ PASSED";
            let overallColor = "green";
            
            if (avgDeviation > 40) {
                overallRisk = "🚨 FAILED - MAJOR RED FLAGS";
                overallColor = "red";
            } else if (avgDeviation > 20) {
                overallRisk = "⚠️ MARGINAL PASS - Suspicious Patterns";
                overallColor = "orange";
            }
            
            resultsHTML = `
                <div class="stat-display">
                    <div class="stat-box">
                        <div class="stat-label">OVERALL COMPLIANCE SCORE</div>
                        <div class="stat-number" style="color: ${overallColor};">${(100 - Math.min(avgDeviation, 100)).toFixed(0)}%</div>
                    </div>
                    <div class="stat-box">
                        <div class="stat-label">RED FLAGS RAISED</div>
                        <div class="stat-number" style="color: var(--color-red);">${flaggedItems}/5</div>
                    </div>
                </div>
                
                <h3 style="color: ${overallColor}; text-align: center;">${overallRisk}</h3>
                <p style="text-align: center; color: #666; font-size: 0.95rem;"><strong>Average Pricing Deviation: ${avgDeviation.toFixed(1)}%</strong></p>
                
                ${resultsHTML}
                
                <div class="fraud-indicator">
                    <h4>💡 What You Just Learned (Real TBML Tactics)</h4>
                    <ul>
                        <li><strong>Under-invoiced exports:</strong> Seller ships $1,000 goods for $50 invoice. Buyer pays full $1,000 elsewhere, pockets laundered cash difference.</li>
                        <li><strong>Over-invoiced imports:</strong> Buyer invoiced for $1,000 of $100 goods. Sends extra $900 abroad disguised as legitimate payment.</li>
                        <li><strong>Commodity mismatch:</strong> $0.10 razors invoiced at $35 each (actual case: Venezuela-USA trade).</li>
                        <li><strong>Multiple invoicing:</strong> Same goods invoiced 3+ times to justify repeat payments.</li>
                        <li><strong>Vague descriptions:</strong> "Electronics" instead of specific products = impossible to verify market rates.</li>
                    </ul>
                </div>
            `;
            
            resultsContent.innerHTML = resultsHTML;
            resultsDiv.classList.add('show');
        }
        
        // Reset game
        function resetGame() {
            document.getElementById('results').classList.remove('show');
            initGame();
        }
        
        // Create snowflakes
        function createSnowflakes() {
            const snowflakesDiv = document.getElementById('snowflakes');
            const snowflakeCount = 15;
            
            for (let i = 0; i < snowflakeCount; i++) {
                const snowflake = document.createElement('div');
                snowflake.className = 'snowflake';
                snowflake.textContent = '❄️';
                snowflake.style.left = Math.random() * 100 + '%';
                snowflake.style.animationDuration = (Math.random() * 10 + 10) + 's';
                snowflake.style.opacity = Math.random() * 0.5 + 0.3;
                snowflakesDiv.appendChild(snowflake);
            }
        }
        
        // Initialize on load
        window.addEventListener('DOMContentLoaded', () => {
            createSnowflakes();
            initGame();
        });
    </script>
</body>
</html>
