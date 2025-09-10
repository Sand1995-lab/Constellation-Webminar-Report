<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Energy Market Intelligence Report - September 2025</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/3.9.1/chart.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            overflow-x: hidden;
            position: relative;
        }

        #canvas-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background: linear-gradient(135deg, #0F2027 0%, #203A43 50%, #2C5364 100%);
        }

        .page {
            min-height: 100vh;
            padding: 60px 20px;
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
            scroll-snap-align: start;
        }

        .content-wrapper {
            max-width: 1400px;
            width: 100%;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 30px;
            padding: 50px;
            box-shadow: 0 25px 50px rgba(0, 0, 0, 0.3);
            backdrop-filter: blur(10px);
            animation: slideIn 1s ease-out;
            transform-style: preserve-3d;
            transition: transform 0.3s ease;
        }

        .content-wrapper:hover {
            transform: rotateY(2deg) rotateX(-2deg);
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        h1 {
            font-size: 3.5em;
            background: linear-gradient(135deg, #00C851 0%, #00BFA5 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-align: center;
            margin-bottom: 30px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
            animation: glow 2s ease-in-out infinite alternate;
        }

        @keyframes glow {
            from { filter: brightness(1); }
            to { filter: brightness(1.2); }
        }

        h2 {
            font-size: 2.5em;
            color: #2C5364;
            margin: 30px 0 20px;
            border-left: 5px solid #00C851;
            padding-left: 20px;
        }

        h3 {
            font-size: 1.8em;
            color: #203A43;
            margin: 20px 0 15px;
            background: linear-gradient(90deg, rgba(0,200,81,0.1) 0%, transparent 100%);
            padding: 10px 20px;
            border-radius: 10px;
        }

        .highlight-box {
            background: linear-gradient(135deg, rgba(0,200,81,0.1) 0%, rgba(0,191,165,0.1) 100%);
            border-left: 4px solid #00C851;
            padding: 20px;
            margin: 20px 0;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            transform: translateZ(20px);
            transition: all 0.3s ease;
        }

        .highlight-box:hover {
            transform: translateZ(30px) scale(1.02);
            box-shadow: 0 10px 30px rgba(0,200,81,0.2);
        }

        .stat-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 30px;
            margin: 30px 0;
        }

        .stat-card {
            background: white;
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            text-align: center;
            transition: all 0.3s ease;
            border-top: 4px solid transparent;
            background-image: linear-gradient(white, white), 
                              linear-gradient(135deg, #00C851 0%, #00BFA5 100%);
            background-origin: border-box;
            background-clip: padding-box, border-box;
            transform-style: preserve-3d;
        }

        .stat-card:hover {
            transform: translateY(-10px) rotateX(5deg);
            box-shadow: 0 20px 40px rgba(0,200,81,0.3);
        }

        .stat-value {
            font-size: 2.5em;
            font-weight: bold;
            background: linear-gradient(135deg, #00C851 0%, #00BFA5 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .stat-label {
            color: #666;
            margin-top: 10px;
            font-size: 1.1em;
        }

        .chart-container {
            position: relative;
            height: 400px;
            margin: 30px 0;
            background: white;
            padding: 20px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        .key-points {
            background: linear-gradient(135deg, rgba(255,255,255,0.9) 0%, rgba(240,240,240,0.9) 100%);
            padding: 30px;
            border-radius: 20px;
            margin: 30px 0;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        .key-points li {
            margin: 15px 0;
            padding-left: 30px;
            position: relative;
            color: #333;
            font-size: 1.1em;
            line-height: 1.6;
        }

        .key-points li:before {
            content: "⚡";
            position: absolute;
            left: 0;
            color: #00C851;
            font-size: 1.3em;
        }

        .energy-icon {
            display: inline-block;
            width: 60px;
            height: 60px;
            background: linear-gradient(135deg, #00C851 0%, #00BFA5 100%);
            border-radius: 50%;
            margin: 0 auto 20px;
            position: relative;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { box-shadow: 0 0 0 0 rgba(0,200,81,0.7); }
            70% { box-shadow: 0 0 0 20px rgba(0,200,81,0); }
            100% { box-shadow: 0 0 0 0 rgba(0,200,81,0); }
        }

        .nav-dots {
            position: fixed;
            right: 30px;
            top: 50%;
            transform: translateY(-50%);
            z-index: 1000;
        }

        .nav-dot {
            width: 15px;
            height: 15px;
            border-radius: 50%;
            background: rgba(255,255,255,0.3);
            margin: 10px 0;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 2px solid #00C851;
        }

        .nav-dot:hover,
        .nav-dot.active {
            background: #00C851;
            transform: scale(1.3);
        }

        .gradient-text {
            background: linear-gradient(135deg, #00C851 0%, #00BFA5 50%, #00C851 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            background-size: 200% auto;
            animation: shine 3s linear infinite;
        }

        @keyframes shine {
            to { background-position: 200% center; }
        }

        .table-responsive {
            overflow-x: auto;
            margin: 30px 0;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        th {
            background: linear-gradient(135deg, #00C851 0%, #00BFA5 100%);
            color: white;
            padding: 15px;
            text-align: left;
            font-weight: 600;
        }

        td {
            padding: 15px;
            border-bottom: 1px solid #eee;
        }

        tr:hover {
            background: rgba(0,200,81,0.05);
        }

        .scroll-indicator {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            animation: bounce 2s infinite;
            color: white;
            font-size: 2em;
            z-index: 100;
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateX(-50%) translateY(0); }
            40% { transform: translateX(-50%) translateY(-20px); }
            60% { transform: translateX(-50%) translateY(-10px); }
        }
    </style>
</head>
<body>
    <div id="canvas-container"></div>
    
    <div class="nav-dots">
        <div class="nav-dot active" onclick="scrollToPage(0)"></div>
        <div class="nav-dot" onclick="scrollToPage(1)"></div>
        <div class="nav-dot" onclick="scrollToPage(2)"></div>
        <div class="nav-dot" onclick="scrollToPage(3)"></div>
        <div class="nav-dot" onclick="scrollToPage(4)"></div>
        <div class="nav-dot" onclick="scrollToPage(5)"></div>
        <div class="nav-dot" onclick="scrollToPage(6)"></div>
        <div class="nav-dot" onclick="scrollToPage(7)"></div>
        <div class="nav-dot" onclick="scrollToPage(8)"></div>
        <div class="nav-dot" onclick="scrollToPage(9)"></div>
        <div class="nav-dot" onclick="scrollToPage(10)"></div>
    </div>

    <div class="scroll-indicator">⬇</div>

    <!-- Page 1: Title Page -->
    <div class="page" id="page1">
        <div class="content-wrapper">
            <div class="energy-icon"></div>
            <h1 class="gradient-text">Energy Market Intelligence Report</h1>
            <h2 style="text-align: center; border: none;">Trade Talks Promote U.S. Energy Dominance</h2>
            <div class="highlight-box" style="text-align: center;">
                <h3>September 11, 2025</h3>
                <p style="font-size: 1.2em; color: #666;">Constellation Energy Market Intelligence Webinar</p>
            </div>
            <div class="stat-grid">
                <div class="stat-card">
                    <div class="stat-value">107.4</div>
                    <div class="stat-label">Bcf/day Production</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">3,272</div>
                    <div class="stat-label">Bcf Storage</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">$3.92</div>
                    <div class="stat-label">Cal'26 NYMEX</div>
                </div>
            </div>
        </div>
    </div>

    <!-- Page 2: Executive Summary -->
    <div class="page" id="page2">
        <div class="content-wrapper">
            <h1>Executive Summary</h1>
            <div class="key-points">
                <h3>Key Market Developments</h3>
                <ul style="list-style: none;">
                    <li>Summer 2025 ranked as the ninth warmest on record, with August fading quickly after a strong first half</li>
                    <li>Trade negotiations have secured over $1 trillion in U.S. energy export commitments through decade end</li>
                    <li>Natural gas production holding near record levels at 107.4 Bcf/day in August</li>
                    <li>Storage on track to reach effectively full capacity by end of October at 3,912 Bcf</li>
                    <li>PJM capacity auction results set new records with rapidly increasing demand</li>
                    <li>Offshore wind industry facing significant headwinds from regulatory changes</li>
                </ul>
            </div>
            <div class="highlight-box">
                <h3>Market Temperature Assessment</h3>
                <p>The overall market sentiment remains cautiously bullish, with strong fundamentals in production and LNG exports balanced against economic uncertainties and weather variability.</p>
            </div>
        </div>
    </div>

    <!-- Page 3: Weather Outlook -->
    <div class="page" id="page3">
        <div class="content-wrapper">
            <h1>Weather & Climate Outlook</h1>
            <div class="stat-grid">
                <div class="stat-card">
                    <div class="stat-value">245</div>
                    <div class="stat-label">October HDDs Forecast</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">510</div>
                    <div class="stat-label">November HDDs Forecast</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">Neutral</div>
                    <div class="stat-label">ENSO Status</div>
                </div>
            </div>
            <div class="highlight-box">
                <h3>October Forecast</h3>
                <p>Near-normal conditions expected from Plains to Southeast. Warmer-than-average temperatures likely across the North and interior West. Tropical activity remains a wild card.</p>
            </div>
            <div class="highlight-box">
                <h3>November Forecast</h3>
                <p>Eastern U.S. expected to experience mild conditions while cold air develops in western Canada. Potential for cold air bursts to move eastward before month's end.</p>
            </div>
            <div class="key-points">
                <h3>Winter 2025-26 Outlook</h3>
                <ul style="list-style: none;">
                    <li>No strong ENSO signal expected for second straight season</li>
                    <li>Fluctuation between ENSO neutral and weak La Niña conditions</li>
                    <li>NOAA forecast shows colder/stormier Northwest, warmer South and East</li>
                    <li>Multiple cold shots possible across South and East this winter</li>
                </ul>
            </div>
        </div>
    </div>

    <!-- Page 4: Trade & Export Developments -->
    <div class="page" id="page4">
        <div class="content-wrapper">
            <h1>Trade Negotiations & Energy Exports</h1>
            <h2>Major LNG Export Commitments</h2>
            <div class="table-responsive">
                <table>
                    <thead>
                        <tr>
                            <th>Country</th>
                            <th>LNG Volume</th>
                            <th>Annual Value</th>
                            <th>Additional Terms</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>South Korea</td>
                            <td>0.4 Bcf/d</td>
                            <td>$511M</td>
                            <td>Tariff reductions on carbon capture & battery tech</td>
                        </tr>
                        <tr>
                            <td>Japan</td>
                            <td>0.54 Bcf/d</td>
                            <td>$690M</td>
                            <td>Nuclear licensing reform</td>
                        </tr>
                        <tr>
                            <td>India</td>
                            <td>0.8 Bcf/d</td>
                            <td>$1Bn</td>
                            <td>Plus 250k bbls/d oil</td>
                        </tr>
                        <tr>
                            <td>Mexico</td>
                            <td>2.5 Bcf/d</td>
                            <td>$3.2Bn</td>
                            <td>Pipeline expansion, tariff-free electricity trade</td>
                        </tr>
                        <tr>
                            <td>European Union</td>
                            <td>1.35 Bcf/d</td>
                            <td>$1.7Bn</td>
                            <td>3-year commitment including oil & nuclear</td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <div class="highlight-box">
                <h3>Total Export Commitments</h3>
                <p style="font-size: 1.3em;"><strong>5.5 Bcf/d</strong> of natural gas heading overseas through new trade agreements, with over <strong>$1 Trillion</strong> in total energy commitments secured before decade end.</p>
            </div>
        </div>
    </div>

    <!-- Page 5: Natural Gas Fundamentals -->
    <div class="page" id="page5">
        <div class="content-wrapper">
            <h1>Natural Gas Market Fundamentals</h1>
            <div class="chart-container">
                <canvas id="gasProductionChart"></canvas>
            </div>
            <div class="key-points">
                <h3>Production Highlights</h3>
                <ul style="list-style: none;">
                    <li>August production averaged 107.4 Bcf/day vs. 101.9 Bcf/day in August 2024</li>
                    <li>Year-to-date production through 8/31 is 105.2 Bcf/day, up ~3.5 Bcf/d from 2024</li>
                    <li>EQT reports 50% gain in completion efficiency, 10% decrease in well costs</li>
                    <li>Production holding near record levels despite economic headwinds</li>
                </ul>
            </div>
            <div class="stat-grid">
                <div class="stat-card">
                    <div class="stat-value">55 Bcf</div>
                    <div class="stat-label">Last Week Injection</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">+5.5%</div>
                    <div class="stat-label">vs. 5-Year Average</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">43.4 Bcf/d</div>
                    <div class="stat-label">L48 Power Burns</div>
                </div>
            </div>
        </div>
    </div>

    <!-- Page 6: Storage Analysis -->
    <div class="page" id="page6">
        <div class="content-wrapper">
            <h1>Natural Gas Storage Analysis</h1>
            <div class="chart-container">
                <canvas id="storageChart"></canvas>
            </div>
            <div class="highlight-box">
                <h3>Storage Projections</h3>
                <p>EIA forecasts end-October storage at <strong>3,912 Bcf</strong>, approaching effective full capacity. With 10-year normal winter, storage expected to drop to <strong>1,852 Bcf</strong> by end of March 2026.</p>
            </div>
            <div class="key-points">
                <h3>Storage Dynamics</h3>
                <ul style="list-style: none;">
                    <li>Current storage: 3,272 Bcf (73 Bcf below last year)</li>
                    <li>173 Bcf (5.5%) above 5-year average</li>
                    <li>Second largest injection of summer recorded last week</li>
                    <li>Power burns declining seasonally, may accelerate storage fills</li>
                    <li>Producers may need to moderate output if 3.9 Tcf reached early</li>
                </ul>
            </div>
        </div>
    </div>

    <!-- Page 7: Global Energy Dynamics -->
    <div class="page" id="page7">
        <div class="content-wrapper">
            <h1>Global Energy Market Dynamics</h1>
            <h2>Russia-China Pipeline Development</h2>
            <div class="highlight-box">
                <h3>Power of Siberia 2 Pipeline</h3>
                <p>Russia and China signed legally binding memorandum for 50 Bcm/yr (~4.8 Bcf/d) pipeline from western Siberia. Combined with Power of Siberia 1 expansion, total export capacity to China would reach 58 Bcm (5.6 Bcf/day).</p>
            </div>
            <h2>LNG Export Infrastructure</h2>
            <div class="stat-grid">
                <div class="stat-card">
                    <div class="stat-value">17+ Bcf/d</div>
                    <div class="stat-label">U.S. LNG Export Capacity</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">2 Bcf/d</div>
                    <div class="stat-label">In Commissioning</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">$200 Bn</div>
                    <div class="stat-label">2024 U.S. Energy Exports</div>
                </div>
            </div>
            <div class="key-points">
                <h3>Market Implications</h3>
                <ul style="list-style: none;">
                    <li>China balancing reduced dependence on U.S. LNG with Russian pipeline gas</li>
                    <li>Europe seeking to end Russian gas purchases by December 2027</li>
                    <li>U.S. LNG exports to China dropped to zero in March 2025 due to tariffs</li>
                    <li>Growing question whether U.S. can scale to meet new export commitments</li>
                </ul>
            </div>
        </div>
    </div>

    <!-- Page 8: Power Markets -->
    <div class="page" id="page8">
        <div class="content-wrapper">
            <h1>Power Market Dynamics</h1>
            <h2>PJM Capacity Auction Results</h2>
            <div class="chart-container">
                <canvas id="pjmChart"></canvas>
            </div>
            <div class="highlight-box">
                <h3>Record Capacity Prices</h3>
                <p>PJM auction cleared at unprecedented levels as 5,446 MW increase in capacity requirements meets constrained supply. Reserve margin increased from 17.8% to 19.1%.</p>
            </div>
            <h2>Offshore Wind Challenges</h2>
            <div class="table-responsive">
                <table>
                    <thead>
                        <tr>
                            <th>Project</th>
                            <th>Status</th>
                            <th>Capacity (MW)</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>Empire Wind (NY)</td>
                            <td>Stop-work order lifted</td>
                            <td>810</td>
                        </tr>
                        <tr>
                            <td>Revolution Wind (RI, CT)</td>
                            <td>Stop-work order issued</td>
                            <td>704</td>
                        </tr>
                        <tr>
                            <td>Maryland Offshore Wind</td>
                            <td>Permit to be revoked</td>
                            <td>2,200</td>
                        </tr>
                        <tr>
                            <td>South Coast Wind (MA)</td>
                            <td>Permits reconsidered</td>
                            <td>2,400</td>
                        </tr>
                        <tr>
                            <td>New England Wind 1&2</td>
                            <td>Permit to be revoked</td>
                            <td>2,600</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>

    <!-- Page 9: Price Forecasts -->
    <div class="page" id="page9">
        <div class="content-wrapper">
            <h1>Energy Price Forecasts</h1>
            <h2>NYMEX Natural Gas Forward Curves</h2>
            <div class="chart-container">
                <canvas id="nymexChart"></canvas>
            </div>
            <div class="stat-grid">
                <div class="stat-card">
                    <div class="stat-value">$3.92</div>
                    <div class="stat-label">Cal 2026</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">$3.93</div>
                    <div class="stat-label">Cal 2027</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">$3.81</div>
                    <div class="stat-label">Cal 2028</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">$3.69</div>
                    <div class="stat-label">Cal 2029</div>
                </div>
            </div>
            <h2>Regional Power Price Indicators</h2>
            <div class="table-responsive">
                <table>
                    <thead>
                        <tr>
                            <th>Market Hub</th>
                            <th>2025 YTD</th>
                            <th>2026 Forward</th>
                            <th>2027 Forward</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>PJM West Hub</td>
                            <td>$33.07</td>
                            <td>$47.77</td>
                            <td>$54.40</td>
                        </tr>
                        <tr>
                            <td>NYISO Zone A</td>
                            <td>$32.65</td>
                            <td>$51.92</td>
                            <td>$52.87</td>
                        </tr>
                        <tr>
                            <td>New England</td>
                            <td>$41.47</td>
                            <td>$66.67</td>
                            <td>$67.14</td>
                        </tr>
                        <tr>
                            <td>ERCOT South</td>
                            <td>$27.07</td>
                            <td>$36.93</td>
                            <td>$56.00</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>

    <!-- Page 10: Market Outlook -->
    <div class="page" id="page10">
        <div class="content-wrapper">
            <h1>Market Outlook & Key Takeaways</h1>
            <div class="highlight-box" style="background: linear-gradient(135deg, rgba(0,200,81,0.2) 0%, rgba(0,191,165,0.2) 100%);">
                <h2 style="border: none; text-align: center;">Market Temperature Assessment</h2>
                <div class="stat-grid">
                    <div class="stat-card">
                        <div class="energy-icon" style="width: 40px; height: 40px;"></div>
                        <div class="stat-label">Weather: Neutral</div>
                    </div>
                    <div class="stat-card">
                        <div class="energy-icon" style="width: 40px; height: 40px;"></div>
                        <div class="stat-label">Production: Bullish</div>
                    </div>
                    <div class="stat-card">
                        <div class="energy-icon" style="width: 40px; height: 40px;"></div>
                        <div class="stat-label">Storage: Neutral</div>
                    </div>
                    <div class="stat-card">
                        <div class="energy-icon" style="width: 40px; height: 40px;"></div>
                        <div class="stat-label">LNG: Bullish</div>
                    </div>
                </div>
            </div>
            <div class="key-points">
                <h2>Strategic Implications</h2>
                <ul style="list-style: none;">
                    <li><strong>Supply Dynamics:</strong> Record production levels providing market stability, but storage approaching capacity limits may require production moderation</li>
                    <li><strong>Demand Growth:</strong> Data center expansion and LNG export commitments driving unprecedented demand growth in key markets</li>
                    <li><strong>Infrastructure Challenges:</strong> Offshore wind setbacks creating opportunities for natural gas infrastructure development</li>
                    <li><strong>Price Outlook:</strong> Forward curves reflect bullish near-term fundamentals with backwardation through 2027
