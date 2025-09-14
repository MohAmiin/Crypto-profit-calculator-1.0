<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mobile Crypto Profit Calculator</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #0f2027, #203a43, #2c5364);
            color: #f5f5f5;
            min-height: 100vh;
            padding: 15px;
            line-height: 1.5;
        }

        .container {
            max-width: 100%;
            margin: 0 auto;
        }

        header {
            text-align: center;
            margin-bottom: 25px;
            padding: 15px 10px;
        }

        h1 {
            font-size: 1.8rem;
            margin-bottom: 10px;
            background: linear-gradient(90deg, #00c6ff, #0072ff);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }

        .tagline {
            font-size: 1rem;
            opacity: 0.9;
        }

        .calculator-card {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            border-radius: 12px;
            padding: 20px 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            border: 1px solid rgba(255, 255, 255, 0.1);
            margin-bottom: 20px;
        }

        .calculator-card h2 {
            font-size: 1.4rem;
            margin-bottom: 20px;
            color: #00c6ff;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .input-group {
            margin-bottom: 15px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 500;
            font-size: 1rem;
        }

        input {
            width: 100%;
            padding: 14px 15px;
            border-radius: 8px;
            border: 1px solid rgba(255, 255, 255, 0.1);
            background: rgba(0, 0, 0, 0.2);
            color: #fff;
            font-size: 1rem;
            -webkit-appearance: none;
        }

        input:focus {
            outline: none;
            border-color: #00c6ff;
            box-shadow: 0 0 0 2px rgba(0, 198, 255, 0.3);
        }

        .calculate-btn {
            width: 100%;
            padding: 16px;
            background: linear-gradient(90deg, #00c6ff, #0072ff);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            margin-top: 10px;
            transition: all 0.2s;
        }

        .calculate-btn:active {
            transform: scale(0.98);
            background: linear-gradient(90deg, #00a5dd, #0062cc);
        }

        .results-container {
            display: grid;
            grid-template-columns: 1fr;
            gap: 12px;
            margin-top: 25px;
        }

        .result-box {
            background: rgba(0, 0, 0, 0.2);
            padding: 15px;
            border-radius: 10px;
            text-align: center;
        }

        .result-title {
            font-size: 0.9rem;
            opacity: 0.8;
            margin-bottom: 5px;
        }

        .result-value {
            font-size: 1.3rem;
            font-weight: 700;
        }

        .profit {
            color: #00ff8c;
        }

        .loss {
            color: #ff3860;
        }

        .chart-container {
            margin-top: 30px;
            height: 200px;
            position: relative;
            background: rgba(0, 0, 0, 0.1);
            border-radius: 10px;
            overflow: hidden;
            padding: 10px;
            display: flex;
            align-items: flex-end;
            justify-content: space-around;
        }

        .chart-bar {
            width: 60px;
            background: linear-gradient(to top, #0072ff, #00c6ff);
            border-top-left-radius: 5px;
            border-top-right-radius: 5px;
            position: relative;
            transition: height 1s ease;
        }

        .chart-bar.sell {
            background: linear-gradient(to top, #00ff8c, #00d977);
        }

        .chart-label {
            position: absolute;
            bottom: -30px;
            width: 100%;
            text-align: center;
            font-size: 0.8rem;
            font-weight: 600;
        }

        .chart-value {
            position: absolute;
            top: -25px;
            width: 100%;
            text-align: center;
            font-weight: 600;
            font-size: 0.9rem;
        }

        .info-card {
            display: none;
        }

        .disclaimer {
            margin-top: 30px;
            text-align: center;
            font-size: 0.8rem;
            opacity: 0.7;
        }

        footer {
            margin-top: 40px;
            text-align: center;
            opacity: 0.8;
            padding: 15px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            font-size: 0.9rem;
        }

        /* Desktop styles */
        @media (min-width: 768px) {
            body {
                padding: 30px;
            }
            
            .container {
                max-width: 1200px;
            }
            
            header {
                margin-bottom: 40px;
            }
            
            h1 {
                font-size: 2.8rem;
            }
            
            .tagline {
                font-size: 1.3rem;
            }
            
            .main-content {
                display: grid;
                grid-template-columns: 1fr 1fr;
                gap: 30px;
            }
            
            .calculator-card {
                padding: 30px;
            }
            
            .calculator-card h2 {
                font-size: 1.8rem;
            }
            
            .results-container {
                grid-template-columns: 1fr 1fr;
                gap: 15px;
            }
            
            .info-card {
                display: block;
                background: rgba(255, 255, 255, 0.05);
                backdrop-filter: blur(10px);
                border-radius: 12px;
                padding: 30px;
                box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
                border: 1px solid rgba(255, 255, 255, 0.1);
            }
            
            .info-card h2 {
                font-size: 1.8rem;
                margin-bottom: 25px;
                color: #00c6ff;
                display: flex;
                align-items: center;
                gap: 10px;
            }
            
            .info-content h3 {
                font-size: 1.3rem;
                margin: 20px 0 12px;
                color: #00c6ff;
            }
            
            .info-content p, .info-content li {
                margin-bottom: 12px;
                font-size: 1rem;
            }
            
            .info-content ol, .info-content ul {
                padding-left: 20px;
            }
            
            .tip-box {
                background: rgba(0, 198, 255, 0.1);
                border-left: 4px solid #00c6ff;
                padding: 15px;
                border-radius: 8px;
                margin-top: 20px;
            }
            
            .chart-container {
                height: 250px;
            }
            
            .chart-bar {
                width: 80px;
            }
        }

        /* Large desktop styles */
        @media (min-width: 1200px) {
            .results-container {
                grid-template-columns: 1fr 1fr 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1><i class="fas fa-coins"></i> Crypto Profit Calculator</h1>
            <p class="tagline">Calculate your potential cryptocurrency gains and losses</p>
        </header>

        <div class="main-content">
            <div class="calculator-card">
                <h2><i class="fas fa-calculator"></i> Calculate Your Profit</h2>
                
                <div class="input-group">
                    <label for="investment"><i class="fas fa-dollar-sign"></i> Initial Investment ($)</label>
                    <input type="number" id="investment" placeholder="Enter amount in USD" value="">
                </div>
                
                <div class="input-group">
                    <label for="buyPrice"><i class="fas fa-arrow-down"></i> Buy Price ($)</label>
                    <input type="number" id="buyPrice" placeholder="Price per coin when buying" value="">
                </div>
                
                <div class="input-group">
                    <label for="sellPrice"><i class="fas fa-arrow-up"></i> Sell Price ($)</label>
                    <input type="number" id="sellPrice" placeholder="Price per coin when selling" value="">
                </div>
                
                <div class="input-group">
                    <label for="coins"><i class="fas fa-coins"></i> Coins (Optional)</label>
                    <input type="number" id="coins" placeholder="Will be calculated automatically">
                </div>
                
                <button class="calculate-btn" id="calculate">
                    <i class="fas fa-calculator"></i> Calculate Profit/Loss
                </button>

                <div class="results-container">
                    <div class="result-box">
                        <div class="result-title">Coins Owned</div>
                        <div class="result-value" id="coinsResult">0.020000</div>
                    </div>
                    
                    <div class="result-box">
                        <div class="result-title">Initial Investment</div>
                        <div class="result-value" id="investmentResult">$1,000.00</div>
                    </div>
                    
                    <div class="result-box">
                        <div class="result-title">Final Value</div>
                        <div class="result-value" id="finalResult">$1,200.00</div>
                    </div>
                    
                    <div class="result-box">
                        <div class="result-title">Profit/Loss</div>
                        <div class="result-value profit" id="profitResult">$200.00</div>
                    </div>
                    
                    <div class="result-box">
                        <div class="result-title">Return on Investment (ROI)</div>
                        <div class="result-value profit" id="roiResult">20.00%</div>
                    </div>
                    
                    <div class="result-box">
                        <div class="result-title">Price Change</div>
                        <div class="result-value profit" id="priceChangeResult">20.00%</div>
                    </div>
                </div>

                <div class="chart-container">
                    <div class="chart-bar" id="buyChart">
                        <div class="chart-value">$50,000</div>
                        <div class="chart-label">Buy Price</div>
                    </div>
                    <div class="chart-bar sell" id="sellChart">
                        <div class="chart-value">$60,000</div>
                        <div class="chart-label">Sell Price</div>
                    </div>
                </div>

                <p class="disclaimer">
                    Disclaimer: This calculator is for illustrative purposes only. Cryptocurrency investments are subject to high market risk.
                </p>
            </div>

            <div class="info-card">
                <h2><i class="fas fa-info-circle"></i> How It Works</h2>
                
                <div class="info-content">
                    <p>Our calculator helps you determine the potential profit or loss from your cryptocurrency investments. Simply enter your investment details and let the calculator do the rest.</p>
                    
                    <h3><i class="fas fa-list-ol"></i> Instructions:</h3>
                    <ol>
                        <li>Enter your initial investment amount in USD</li>
                        <li>Input the buy price of the cryptocurrency</li>
                        <li>Input the expected sell price</li>
                        <li>Optionally, you can enter the number of coins instead of investment amount</li>
                        <li>Click "Calculate Profit/Loss" to see results</li>
                    </ol>
                    
                    <h3><i class="fas fa-calculator"></i> Calculations:</h3>
                    <ul>
                        <li><strong>Coins:</strong> Investment Amount ÷ Buy Price</li>
                        <li><strong>Final Value:</strong> Coins × Sell Price</li>
                        <li><strong>Profit/Loss:</strong> Final Value - Investment Amount</li>
                        <li><strong>ROI:</strong> (Profit / Investment) × 100%</li>
                        <li><strong>Price Change:</strong> ((Sell Price - Buy Price) / Buy Price) × 100%</li>
                    </ul>
                    
                    <div class="tip-box">
                        <h3><i class="fas fa-lightbulb"></i> Pro Tip:</h3>
                        <p>You can enter the number of coins directly instead of the investment amount. The calculator will automatically compute the investment value based on the buy price.</p>
                    </div>
                </div>
            </div>
        </div>

        <footer>
            <p>Crypto Profit Calculator © 2023 | All calculations are estimates</p>
        </footer>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Get DOM elements
            const investmentInput = document.getElementById('investment');
            const buyPriceInput = document.getElementById('buyPrice');
            const sellPriceInput = document.getElementById('sellPrice');
            const coinsInput = document.getElementById('coins');
            const calculateBtn = document.getElementById('calculate');
            
            // Result elements
            const coinsResult = document.getElementById('coinsResult');
            const investmentResult = document.getElementById('investmentResult');
            const finalResult = document.getElementById('finalResult');
            const profitResult = document.getElementById('profitResult');
            const roiResult = document.getElementById('roiResult');
            const priceChangeResult = document.getElementById('priceChangeResult');
            
            // Chart elements
            const buyChart = document.getElementById('buyChart');
            const sellChart = document.getElementById('sellChart');
            
            // Initialize with default values
            calculateProfit();
            
            // Add event listeners
            calculateBtn.addEventListener('click', calculateProfit);
            
            investmentInput.addEventListener('input', function() {
                coinsInput.value = '';
                calculateProfit();
            });
            
            buyPriceInput.addEventListener('input', calculateProfit);
            sellPriceInput.addEventListener('input', calculateProfit);
            
            coinsInput.addEventListener('input', function() {
                investmentInput.value = '';
                calculateProfit();
            });
            
            function calculateProfit() {
                // Get input values
                let investment = parseFloat(investmentInput.value) || 0;
                const buyPrice = parseFloat(buyPriceInput.value) || 0;
                const sellPrice = parseFloat(sellPriceInput.value) || 0;
                const coins = parseFloat(coinsInput.value) || 0;
                
                let calculatedCoins = coins;
                
                // Calculate coins if investment is provided
                if (investment > 0 && buyPrice > 0) {
                    calculatedCoins = investment / buyPrice;
                }
                
                // Calculate investment if coins are provided
                if (coins > 0 && buyPrice > 0) {
                    investment = coins * buyPrice;
                    investmentInput.value = investment.toFixed(2);
                }
                
                // Calculate results
                const finalValue = calculatedCoins * sellPrice;
                const profit = finalValue - investment;
                const roi = investment > 0 ? (profit / investment) * 100 : 0;
                const priceChange = buyPrice > 0 ? ((sellPrice - buyPrice) / buyPrice) * 100 : 0;
                
                // Update results
                coinsResult.textContent = calculatedCoins.toFixed(6);
                investmentResult.textContent = formatCurrency(investment);
                finalResult.textContent = formatCurrency(finalValue);
                
                // Style profit/loss accordingly
                if (profit >= 0) {
                    profitResult.className = 'result-value profit';
                    profitResult.textContent = formatCurrency(profit);
                } else {
                    profitResult.className = 'result-value loss';
                    profitResult.textContent = formatCurrency(profit);
                }
                
                roiResult.textContent = roi.toFixed(2) + '%';
                
                if (roi >= 0) {
                    roiResult.className = 'result-value profit';
                } else {
                    roiResult.className = 'result-value loss';
                }
                
                priceChangeResult.textContent = priceChange.toFixed(2) + '%';
                
                if (priceChange >= 0) {
                    priceChangeResult.className = 'result-value profit';
                } else {
                    priceChangeResult.className = 'result-value loss';
                }
                
                // Update chart
                updateChart(buyPrice, sellPrice);
            }
            
            function formatCurrency(amount) {
                if (isNaN(amount)) return '$0.00';
                return '$' + amount.toLocaleString('en-US', {
                    minimumFractionDigits: 2,
                    maximumFractionDigits: 2
                });
            }
            
            function updateChart(buyPrice, sellPrice) {
                if (buyPrice <= 0 || sellPrice <= 0) return;
                
                const maxPrice = Math.max(buyPrice, sellPrice) * 1.2;
                const buyHeight = (buyPrice / maxPrice) * 100;
                const sellHeight = (sellPrice / maxPrice) * 100;
                
                buyChart.style.height = buyHeight + '%';
                sellChart.style.height = sellHeight + '%';
                
                // Update chart labels
                buyChart.querySelector('.chart-value').textContent = formatCurrency(buyPrice);
                sellChart.querySelector('.chart-value').textContent = formatCurrency(sellPrice);
            }
        });
    </script>
</body>
</html>
