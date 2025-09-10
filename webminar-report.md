<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Constellation Energy Market Intelligence Webinar</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            background: 
                radial-gradient(ellipse at top left, rgba(76, 175, 80, 0.15) 0%, transparent 50%),
                radial-gradient(ellipse at bottom right, rgba(46, 125, 50, 0.15) 0%, transparent 50%),
                linear-gradient(135deg, #0d1b0f 0%, #1b4332 30%, #2d5016 70%, #40531b 100%);
            color: white;
            overflow-x: hidden;
            min-height: 100vh;
            perspective: 1000px;
        }

        .slide-container {
            display: none;
            min-height: 100vh;
            padding: 20px;
            position: relative;
            animation: slideIn3D 0.8s cubic-bezier(0.23, 1, 0.32, 1);
            transform-style: preserve-3d;
        }

        .slide-container.active {
            display: block;
        }

        @keyframes slideIn3D {
            from { 
                opacity: 0; 
                transform: translateX(50px) rotateY(15deg) translateZ(-100px);
            }
            to { 
                opacity: 1; 
                transform: translateX(0) rotateY(0) translateZ(0);
            }
        }

        .slide-header {
            background: 
                linear-gradient(145deg, rgba(76, 175, 80, 0.25), rgba(46, 125, 50, 0.15)),
                rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(20px);
            padding: 30px;
            border-radius: 25px;
            margin-bottom: 30px;
            border: 2px solid transparent;
            background-clip: padding-box;
            box-shadow: 
                0 20px 40px rgba(0, 0, 0, 0.4),
                inset 0 1px 0 rgba(255, 255, 255, 0.2),
                0 1px 0 rgba(255, 255, 255, 0.1);
            transform: translateZ(20px);
            position: relative;
        }

        .slide-header::before {
            content: '';
            position: absolute;
            inset: 0;
            border-radius: 25px;
            padding: 2px;
            background: linear-gradient(145deg, rgba(76, 175, 80, 0.5), rgba(129, 199, 132, 0.3));
            mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
            mask-composite: exclude;
        }

        .slide-title {
            font-size: 3em;
            font-weight: 800;
            margin-bottom: 15px;
            background: linear-gradient(135deg, #a5d6a7 0%, #81c784 50%, #66bb6a 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            text-shadow: 0 4px 20px rgba(76, 175, 80, 0.3);
            letter-spacing: -0.02em;
            transform: translateZ(10px);
        }

        .slide-subtitle {
            font-size: 1.3em;
            opacity: 0.9;
            font-weight: 300;
            letter-spacing: 0.5px;
        }

        .slide-content {
            background: 
                linear-gradient(145deg, rgba(76, 175, 80, 0.12), rgba(46, 125, 50, 0.08)),
                rgba(255, 255, 255, 0.03);
            backdrop-filter: blur(20px);
            border-radius: 25px;
            padding: 40px;
            border: 1px solid rgba(76, 175, 80, 0.3);
            box-shadow: 
                0 25px 50px rgba(0, 0, 0, 0.4),
                inset 0 1px 0 rgba(255, 255, 255, 0.1);
            transform: translateZ(10px);
            position: relative;
        }

        .chart-container {
            background: 
                linear-gradient(145deg, rgba(255, 255, 255, 0.98), rgba(248, 250, 248, 0.95));
            border-radius: 20px;
            padding: 30px;
            margin: 25px 0;
            color: #1b4332;
            box-shadow: 
                0 20px 40px rgba(0, 0, 0, 0.3),
                0 10px 20px rgba(76, 175, 80, 0.2),
                inset 0 1px 0 rgba(255, 255, 255, 0.8);
            transform: translateZ(15px);
            position: relative;
            transition: all 0.4s cubic-bezier(0.23, 1, 0.32, 1);
        }

        .chart-container:hover {
            transform: translateZ(25px) translateY(-5px);
            box-shadow: 
                0 30px 60px rgba(0, 0, 0, 0.4),
                0 15px 30px rgba(76, 175, 80, 0.3);
        }

        .key-metrics {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 25px;
            margin: 30px 0;
            perspective: 1000px;
        }

        .metric-card {
            background: 
                linear-gradient(145deg, #4caf50 0%, #388e3c 50%, #2e7d32 100%);
            padding: 30px;
            border-radius: 20px;
            text-align: center;
            box-shadow: 
                0 15px 35px rgba(0, 0, 0, 0.4),
                0 5px 15px rgba(76, 175, 80, 0.3),
                inset 0 1px 0 rgba(255, 255, 255, 0.2),
                inset 0 -1px 0 rgba(0, 0, 0, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            transition: all 0.4s cubic-bezier(0.23, 1, 0.32, 1);
            transform: translateZ(5px);
            position: relative;
            overflow: hidden;
        }

        .metric-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            transition: left 0.5s;
        }

        .metric-card:hover {
            transform: translateZ(15px) translateY(-10px) rotateX(5deg);
            box-shadow: 
                0 25px 50px rgba(0, 0, 0, 0.5),
                0 10px 25px rgba(76, 175, 80, 0.4);
        }

        .metric-card:hover::before {
            left: 100%;
        }

        .metric-value {
            font-size: 2.5em;
            font-weight: 900;
            margin-bottom: 10px;
            text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
            letter-spacing: -0.02em;
        }

        .metric-label {
            font-size: 0.95em;
            opacity: 0.95;
            font-weight: 400;
            line-height: 1.4;
        }

        .bullet-points {
            list-style: none;
            padding: 0;
        }

        .bullet-points li {
            margin: 20px 0;
            padding-left: 40px;
            position: relative;
            line-height: 1.7;
            transition: all 0.3s ease;
            transform: translateZ(2px);
        }

        .bullet-points li:before {
            content: "▶";
            position: absolute;
            left: 0;
            color: #81c784;
            font-size: 1.2em;
            transform: translateZ(5px);
            text-shadow: 0 2px 10px rgba(129, 199, 132, 0.5);
        }

        .bullet-points li:hover {
            transform: translateZ(5px) translateX(5px);
            color: #a5d6a7;
        }

        .navigation {
            position: fixed;
            bottom: 30px;
            right: 30px;
            display: flex;
            gap: 15px;
            z-index: 1000;
            perspective: 1000px;
        }

        .nav-btn {
            background: 
                linear-gradient(145deg, rgba(76, 175, 80, 0.3), rgba(46, 125, 50, 0.2));
            backdrop-filter: blur(20px);
            border: none;
            color: white;
            padding: 15px 25px;
            border-radius: 30px;
            cursor: pointer;
            transition: all 0.4s cubic-bezier(0.23, 1, 0.32, 1);
            border: 2px solid rgba(76, 175, 80, 0.4);
            font-weight: 600;
            text-shadow: 0 1px 3px rgba(0, 0, 0, 0.3);
            box-shadow: 
                0 10px 25px rgba(0, 0, 0, 0.3),
                inset 0 1px 0 rgba(255, 255, 255, 0.2);
            transform: translateZ(10px);
        }

        .nav-btn:hover {
            background: 
                linear-gradient(145deg, rgba(76, 175, 80, 0.5), rgba(46, 125, 50, 0.4));
            transform: translateZ(20px) translateY(-3px) rotateX(10deg);
            box-shadow: 
                0 20px 40px rgba(0, 0, 0, 0.4),
                0 10px 20px rgba(76, 175, 80, 0.4),
                inset 0 1px 0 rgba(255, 255, 255, 0.3);
        }

        .nav-btn:active {
            transform: translateZ(5px) translateY(1px);
        }

        .slide-counter {
            position: fixed;
            top: 30px;
            right: 30px;
            background: 
                linear-gradient(145deg, rgba(76, 175, 80, 0.3), rgba(46, 125, 50, 0.2));
            backdrop-filter: blur(20px);
            padding: 15px 25px;
            border-radius: 25px;
            border: 2px solid rgba(76, 175, 80, 0.4);
            box-shadow: 
                0 10px 25px rgba(0, 0, 0, 0.3),
                inset 0 1px 0 rgba(255, 255, 255, 0.2);
            transform: translateZ(10px);
            font-weight: 600;
        }

        .table {
            width: 100%;
            border-collapse: collapse;
            margin: 25px 0;
            background: 
                linear-gradient(145deg, rgba(255, 255, 255, 0.98), rgba(248, 250, 248, 0.95));
            border-radius: 15px;
            overflow: hidden;
            color: #1b4332;
            box-shadow: 
                0 15px 35px rgba(0, 0, 0, 0.2),
                inset 0 1px 0 rgba(255, 255, 255, 0.8);
        }

        .table th, .table td {
            padding: 18px;
            text-align: left;
            border-bottom: 1px solid rgba(76, 175, 80, 0.1);
            transition: all 0.3s ease;
        }

        .table th {
            background: 
                linear-gradient(145deg, rgba(76, 175, 80, 0.15), rgba(129, 199, 132, 0.1));
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            font-size: 0.9em;
        }

        .table tr:hover {
            background: rgba(76, 175, 80, 0.05);
            transform: translateZ(2px);
        }

        .chart-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 25px;
            margin: 30px 0;
            perspective: 1000px;
        }

        .simple-chart {
            height: 250px;
            background: 
                linear-gradient(145deg, #66bb6a 0%, #4caf50 50%, #388e3c 100%);
            border-radius: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            text-align: center;
            box-shadow: 
                0 15px 35px rgba(0, 0, 0, 0.4),
                0 5px 15px rgba(76, 175, 80, 0.3),
                inset 0 1px 0 rgba(255, 255, 255, 0.2);
            transform: translateZ(10px);
            transition: all 0.4s cubic-bezier(0.23, 1, 0.32, 1);
            position: relative;
            overflow: hidden;
        }

        .simple-chart:hover {
            transform: translateZ(20px) translateY(-5px) rotateX(5deg);
        }

        .simple-chart::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: 
                radial-gradient(circle, rgba(255, 255, 255, 0.1) 0%, transparent 70%);
            animation: rotate 20s linear infinite;
        }

        @keyframes rotate {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        .highlight-box {
            background: 
                linear-gradient(145deg, #4caf50 0%, #43a047 50%, #388e3c 100%);
            padding: 30px;
            border-radius: 20px;
            margin: 30px 0;
            text-align: center;
            font-weight: 700;
            font-size: 1.1em;
            box-shadow: 
                0 15px 35px rgba(0, 0, 0, 0.4),
                0 5px 15px rgba(76, 175, 80, 0.3),
                inset 0 1px 0 rgba(255, 255, 255, 0.2);
            border: 1px solid rgba(255, 255, 255, 0.2);
            transform: translateZ(10px);
            transition: all 0.4s cubic-bezier(0.23, 1, 0.32, 1);
            position: relative;
            overflow: hidden;
        }

        .highlight-box:hover {
            transform: translateZ(15px) translateY(-3px);
        }

        .highlight-box::after {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
            animation: shimmer 3s infinite;
        }

        @keyframes shimmer {
            0% { left: -100%; }
            100% { left: 100%; }
        }

        .two-column {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 40px;
            align-items: start;
        }

        .animated-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: -1;
        }

        .floating-element {
            position: absolute;
            width: 20px;
            height: 20px;
            background: radial-gradient(circle, rgba(129, 199, 132, 0.3), transparent);
            border-radius: 50%;
            animation: float 6s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-20px) rotate(180deg); }
        }

        .floating-element:nth-child(1) { top: 10%; left: 10%; animation-delay: 0s; }
        .floating-element:nth-child(2) { top: 20%; right: 10%; animation-delay: 1s; }
        .floating-element:nth-child(3) { bottom: 20%; left: 20%; animation-delay: 2s; }
        .floating-element:nth-child(4) { bottom: 10%; right: 20%; animation-delay: 3s; }

        .data-visualization {
            position: relative;
            background: 
                linear-gradient(145deg, rgba(255, 255, 255, 0.95), rgba(240, 248, 240, 0.9));
            border-radius: 20px;
            padding: 30px;
            margin: 20px 0;
            color: #1b4332;
            box-shadow: 
                0 20px 40px rgba(0, 0, 0, 0.3),
                0 10px 20px rgba(76, 175, 80, 0.2);
            transform: translateZ(15px);
            overflow: hidden;
        }

        .bar-chart {
            display: flex;
            align-items: end;
            gap: 10px;
            height: 200px;
            padding: 20px 0;
        }

        .bar {
            flex: 1;
            background: linear-gradient(to top, #2e7d32, #4caf50, #66bb6a);
            border-radius: 5px 5px 0 0;
            position: relative;
            transition: all 0.4s cubic-bezier(0.23, 1, 0.32, 1);
            box-shadow: 0 5px 15px rgba(76, 175, 80, 0.3);
        }

        .bar:hover {
            transform: translateY(-10px) scaleY(1.1);
            box-shadow: 0 10px 25px rgba(76, 175, 80, 0.5);
        }

        .bar-label {
            position: absolute;
            bottom: -25px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 0.8em;
            font-weight: 600;
        }

        .bar-value {
            position: absolute;
            top: -30px;
            left: 50%;
            transform: translateX(-50%);
            font-weight: bold;
            color: #2e7d32;
        }

        @media (max-width: 768px) {
            .two-column {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            .slide-title {
                font-size: 2.5em;
            }
            .key-metrics {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="animated-bg">
        <div class="floating-element"></div>
        <div class="floating-element"></div>
        <div class="floating-element"></div>
        <div class="floating-element"></div>
    </div>

    <div class="slide-counter">
        <span id="slideNumber">1</span> / <span id="totalSlides">16</span>
    </div>

    <!-- Slide 1: Title -->
    <div class="slide-container active">
        <div class="slide-header">
            <div class="slide-title">Trade Talks Promote U.S. Energy Dominance</div>
            <div class="slide-subtitle">Constellation Energy Market Intelligence Webinar</div>
            <div class="slide-subtitle">September 10, 2025</div>
        </div>
        <div class="slide-content">
            <div class="key-metrics">
                <div class="metric-card">
                    <div class="metric-value">$1T+</div>
                    <div class="metric-label">Energy Export Commitments</div>
                </div>
                <div class="metric-card">
                    <div class="metric-value">5.5</div>
                    <div class="metric-label">Bcf/d Natural Gas Exports</div>
                </div>
                <div class="metric-card">
                    <div class="metric-value">107.4</div>
                    <div class="metric-label">Bcf/d Gas Production (Aug)</div>
                </div>
                <div class="metric-card">
                    <div class="metric-value">3,272</div>
                    <div class="metric-label">Bcf Natural Gas Storage</div>
                </div>
            </div>
            <div class="highlight-box">
                Recent trade negotiations have secured massive energy export commitments, positioning the U.S. as a dominant global energy supplier
            </div>
        </div>
    </div>

    <!-- Slide 2: Weather Outlook -->
    <div class="slide-container">
        <div class="slide-header">
            <div class="slide-title">Weather Outlook</div>
            <div class="slide-subtitle">Fall & Winter Forecasts</div>
        </div>
        <div class="slide-content">
            <div class="two-column">
                <div>
                    <h3>Fall Forecast</h3>
                    <ul class="bullet-points">
                        <li>October: 245 HDDs forecast</li>
                        <li>November: 510 HDDs forecast</li>
                        <li>Near-normal conditions Plains to Southeast</li>
                        <li>Warmer than average in North & interior West</li>
                        <li>Tropical season remains active through October</li>
                    </ul>
                </div>
                <div>
                    <h3>Winter Outlook</h3>
                    <ul class="bullet-points">
                        <li>Weak ENSO signal - neutral to weak La Niña</li>
                        <li>High variability expected (similar to last year)</li>
                        <li>Colder & stormier in Northwest</li>
                        <li>Warmer than normal in South & East</li>
                        <li>Multiple cold shots possible across South & East</li>
                    </ul>
                </div>
            </div>
            <div class="data-visualization">
                <h3>Summer 2025 Temperature Ranking</h3>
                <div class="bar-chart">
                    <div class="bar" style="height: 40%;">
                        <div class="bar-value">40°</div>
                        <div class="bar-label">Jun</div>
                    </div>
                    <div class="bar" style="height: 60%;">
                        <div class="bar-value">60°</div>
                        <div class="bar-label">Jul</div>
                    </div>
                    <div class="bar" style="height: 45%;">
                        <div class="bar-value">45°</div>
                        <div class="bar-label">Aug</div>
                    </div>
                </div>
                <div style="text-align: center; margin-top: 20px; font-weight: bold; color: #2e7d32;">
                    9th Warmest Summer on Record
                </div>
            </div>
        </div>
    </div>

    <!-- Slide 3: Trade Negotiations -->
    <div class="slide-container">
        <div class="slide-header">
            <div class="slide-title">Trade Negotiations</div>
            <div class="slide-subtitle">Massive Energy Export Commitments</div>
        </div>
        <div class="slide-content">
            <table class="table">
                <thead>
                    <tr>
                        <th>Country</th>
                        <th>LNG Commitment</th>
                        <th>Annual Value</th>
                        <th>Additional Benefits</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td><strong>South Korea</strong></td>
                        <td>0.4 Bcf/d</td>
                        <td>$511M</td>
                        <td>$250M investment in Philadelphia Navy Yard</td>
                    </tr>
                    <tr>
                        <td><strong>Japan</strong></td>
                        <td>0.54 Bcf/d</td>
                        <td>$690M</td>
                        <td>Nuclear licensing reform</td>
                    </tr>
                    <tr>
                        <td><strong>India</strong></td>
                        <td>0.8 Bcf/d</td>
                        <td>$1B LNG + Oil</td>
                        <td>250k bbls/d oil imports</td>
                    </tr>
                    <tr>
                        <td><strong>Mexico</strong></td>
                        <td>2.5 Bcf/d</td>
                        <td>$3.2B</td>
                        <td>Pipeline expansion, grid integration</td>
                    </tr>
                    <tr>
                        <td><strong>European Union</strong></td>
                        <td>1.35 Bcf/d</td>
                        <td>$1.7B</td>
                        <td>3-year commitment for LNG, oil, nuclear</td>
                    </tr>
                </tbody>
            </table>
            <div class="highlight-box">
                Total: 5.5+ Bcf/d of natural gas exports committed
            </div>
        </div>
    </div>

    <!-- Slide 4: LNG Infrastructure -->
    <div class="slide-container">
        <div class="slide-header">
            <div class="slide-title">LNG Infrastructure Capacity</div>
            <div class="slide-subtitle">Current vs Future Demand</div>
        </div>
        <div class="slide-content">
            <div class="key-metrics">
                <div class="metric-card">
                    <div class="metric-value">17</div>
                    <div class="metric-label">Bcf/d Current Capacity</div>
                </div>
                <div class="metric-card">
                    <div class="metric-value">2</div>
                    <div class="metric-label">Bcf/d Commissioning</div>
                </div>
                <div class="metric-card">
                    <div class="metric-value">$200B</div>
                    <div class="metric-label">2024 Energy Exports</div>
                </div>
            </div>
            <div class="data-visualization">
                <h3>LNG Capacity Analysis</h3>
                <div class="bar-chart">
                    <div class="bar" style="height: 85%;">
                        <div class="bar-value">17 Bcf/d</div>
                        <div class="bar-label">Current</div>
                    </div>
                    <div class="bar" style="height: 20%;">
                        <div class="bar-value">2 Bcf/d</div>
                        <div class="bar-label">Commissioning</div>
                    </div>
                    <div class="bar" style="height: 55%;">
                        <div class="bar-value">5.5 Bcf/d</div>
                        <div class="bar-label">Committed</div>
                    </div>
                </div>
            </div>
            <div class="highlight-box">
                Key Question: Can the U.S. energy industry scale to meet the unprecedented demand from trade commitments exceeding $1 trillion?
            </div>
        </div>
    </div>

    <!-- Slide 5: Natural Gas Production -->
    <div class="slide-container">
        <div class="slide-header">
            <div class="slide-title">Natural Gas Production</div>
            <div class="slide-subtitle">Record Levels Supporting Demand</div>
        </div>
        <div class="slide-content">
            <div class="key-metrics">
                <div class="metric-card">
                    <div class="metric-value">107.4</div>
                    <div class="metric-label">Bcf/d August Production</div>
                </div>
                <div class="metric-card">
                    <div class="metric-value">105.2</div>
                    <div class="metric-label">Bcf/d YTD Average</div>
                </div>
                <div class="metric-card">
                    <div class="metric-value">+3.5</div>
                    <div class="metric-label">Bcf/d vs 2024 Levels</div>
                </div>
            </div>
            <div class="data-visualization">
                <h3>Production Trend & Efficiency</h3>
                <div class="bar-chart">
                    <div class="bar" style="height: 70%;">
                        <div class="bar-value">101.9</div>
                        <div class="bar-label">Aug '24</div>
                    </div>
                    <div class="bar" style="height: 85%;">
                        <div class="bar-value">107.4</div>
                        <div class="bar-label">Aug '25</div>
                    </div>
                    <div class="bar" style="height: 80%;">
                        <div class="bar-value">106.8</div>
                        <div class="bar-label">Sep '25</div>
                    </div>
                </div>
            </div>
            <div class="chart-container">
                <h3>Production Efficiency Gains</h3>
                <ul class="bullet-points" style="color: #1b4332;">
                    <li>EQT reported 50% completion efficiency gain</li>
                    <li>Well costs decreased 10%: $1,000/ft → $900/ft</li>
                    <li>September production: 106.8-107.2 Bcf/d</li>
                    <li>EIA forecasts: 2025: 106.63 Bcf/d | 2026: 106.03 Bcf/d</li>
                </ul>
            </div>
        </div>
    </div>

    <!-- Slide 6: Natural Gas Storage -->
    <div class="slide-container">
        <div class="slide-header">
            <div class="slide-title">Natural Gas Storage</div>
            <div class="slide-subtitle">Healthy Pace Toward Full Storage</div>
        </div>
        <div class="slide-content">
            <div class="key-metrics">
                <div class="metric-card">
                    <div class="metric-value">3,272</div>
                    <div class="metric-label">Bcf Current Storage</div>
                </div>
                <div class="metric-card">
                    <div class="metric-value">3,912</div>
                    <div class="metric-label">Bcf October Forecast</div>
                </div>
                <div class="metric-card">
                    <div class="metric-value">55</div>
                    <div class="metric-label">Bcf Last Week Injection</div>
                </div>
            </div>
            <div class="data-visualization">
                <h3>Storage Levels vs Historical</h3>
                <div class="bar-chart">
                    <div class="bar" style="height: 60%;">
                        <div class="bar-value">3,099</div>
                        <div class="bar-label">5-Yr Avg</div>
                    </div>
                    <div class="bar" style="height: 75%;">
                        <div class="bar-value">3,345</div>
                        <div class="bar-label">2024</div>
                    </div>
                    <div class="bar" style="height: 70%;">
                        <div class="bar-value">3,272</div>
                        <div class="bar-label">Current</div>
                    </div>
                    <div class="bar" style="height: 90%;">
                        <div class="bar-value">3,912</div>
                        <div class="bar-label">Oct Fcst</div>
                    </div>
                </div>
            </div>
            <div class="chart-container">
                <h3>Storage Metrics</h3>
                <ul class="bullet-points" style="color: #1b4332;">
                    <li>73 Bcf (-2.2%) below year ago levels</li>
                    <li>173 Bcf (+5.5%) above 5-year average</li>
                    <li>On track to reach ~3.9 Tcf by end of October</li>
                    <li>EIA winter forecast: End March at 1,852 Bcf</li>
                    <li>Power burns averaged 43.4 Bcf/d vs 45.8 Bcf/d last year</li>
                </ul>
            </div>
        </div>
    </div>

    <!-- Slide 7: Global Situation -->
    <div class="slide-container">
        <div class="slide-header">
            <div class="slide-title">Global Natural Gas Dynamics</div>
            <div class="slide-subtitle">Russia-China Pipeline & Market Implications</div>
        </div>
        <div class="slide-content">
            <div class="two-column">
                <div>
                    <h3>Power of Siberia 2</h3>
                    <ul class="bullet-points">
                        <li>Russia-China signed binding memorandum</li>
                        <li>50 Bcm/yr capacity (~4.8 Bcf/d)</li>
                        <li>Existing Power of Siberia 1: 38 Bcm/yr</li>
                        <li>Total future capacity: 58 Bcm/yr (5.6 Bcf/d)</li>
                    </ul>
                </div>
                <div>
                    <h3>Market Implications</h3>
                    <ul class="bullet-points">
                        <li>China gains negotiating leverage</li>
                        <li>Russia needs to replace EU sales</li>
                        <li>EU aims to end Russian purchases by Dec 2027</li>
                        <li>China-US LNG trade went to zero in March</li>
                        <li>Opportunity for increased US-EU LNG trade</li>
                    </ul>
                </div>
            </div>
            <div class="data-visualization">
                <h3>Global Gas Flow Dynamics (Bcf/d)</h3>
                <div class="bar-chart">
                    <div class="bar" style="height: 65%;">
                        <div class="bar-value">3.7</div>
                        <div class="bar-label">Current RU→CN</div>
                    </div>
                    <div class="bar" style="height: 85%;">
                        <div class="bar-value">5.6</div>
                        <div class="bar-label">Future RU→CN</div>
                    </div>
                    <div class="bar" style="height: 75%;">
                        <div class="bar-value">5.5</div>
                        <div class="bar-label">US Export Commits</div>
                    </div>
                </div>
            </div>
            <div class="highlight-box">
                China balances dependency concerns while Russia seeks EU replacement markets
            </div>
        </div>
    </div>

    <!-- Slide 8: Offshore Wind Challenges -->
    <div class="slide-container">
        <div class="slide-header">
            <div class="slide-title">Offshore Wind Industry Headwinds</div>
            <div class="slide-subtitle">Policy Changes Create Market Uncertainty</div>
        </div>
        <div class="slide-content">
            <table class="table">
                <thead>
                    <tr>
                        <th>Project</th>
                        <th>Status</th>
                        <th>Capacity (MW)</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td><strong>Empire Wind (NY)</strong></td>
                        <td>Stop-work order lifted</td>
                        <td>810</td>
                    </tr>
                    <tr>
                        <td><strong>Revolution Wind (RI, CT)</strong></td>
                        <td>Stop-work order issued</td>
                        <td>704</td>
                    </tr>
                    <tr>
                        <td><strong>Maryland Offshore Wind</strong></td>
                        <td>Permit expected to be revoked</td>
                        <td>2,200</td>
                    </tr>
                    <tr>
                        <td><strong>South Coast Wind (MA)</strong></td>
                        <td>Permits to be reconsidered</td>
                        <td>2,400</td>
                    </tr>
                    <tr>
                        <td><strong>New England Wind 1 & 2</strong></td>
                        <td>Permit expected to be revoked</td>
                        <td>2,600</td>
                    </tr>
                </tbody>
            </table>
            <div class="data-visualization">
                <h3>Offshore Wind Capacity at Risk</h3>
                <div class="bar-chart">
                    <div class="bar" style="height: 15%;">
                        <div class="bar-value">810</div>
                        <div class="bar-label">Empire</div>
                    </div>
                    <div class="bar" style="height: 40%;">
                        <div class="bar-value">2,200</div>
                        <div class="bar-label">Maryland</div>
                    </div>
                    <div class="bar" style="height: 45%;">
                        <div class="bar-value">2,400</div>
                        <div class="bar-label">S. Coast</div>
                    </div>
                    <div class="bar" style="height: 50%;">
                        <div class="bar-value">2,600</div>
                        <div class="bar-label">NE Wind</div>
                    </div>
                </div>
            </div>
            <div class="highlight-box">
                Policy reversals create opportunities for fossil fuel infrastructure, including natural gas pipelines
            </div>
        </div>
    </div>

    <!-- Slide 9: PJM Capacity Auction -->
    <div class="slide-container">
        <div class="slide-header">
            <div class="slide-title">PJM Capacity Auction Results</div>
            <div class="slide-subtitle">Record Prices Reflect Supply-Demand Imbalance</div>
        </div>
        <div class="slide-content">
            <div class="key-metrics">
                <div class="metric-card">
                    <div class="metric-value">$269.92</div>
                    <div class="metric-label">$/MW-day Clearing Price</div>
                </div>
                <div class="metric-card">
                    <div class="metric-value">$388.57</div>
                    <div class="metric-label">$/MW-day Without Price Cap</div>
                </div>
                <div class="metric-card">
                    <div class="metric-value">+5,446</div>
                    <div class="metric-label">MW Demand Increase</div>
                </div>
            </div>
            <div class="data-visualization">
                <h3>PJM Capacity Price History</h3>
                <div class="bar-chart">
                    <div class="bar" style="height: 20%;">
                        <div class="bar-value">$76</div>
                        <div class="bar-label">2022/23</div>
                    </div>
                    <div class="bar" style="height: 35%;">
                        <div class="bar-value">$135</div>
                        <div class="bar-label">2023/24</div>
                    </div>
                    <div class="bar" style="height: 60%;">
                        <div class="bar-value">$204</div>
                        <div class="bar-label">2024/25</div>
                    </div>
                    <div class="bar" style="height: 85%;">
                        <div class="bar-value">$270</div>
                        <div class="bar-label">2025/26</div>
                    </div>
                </div>
            </div>
            <div class="chart-container">
                <h3>Auction Drivers</h3>
                <ul class="bullet-points" style="color: #1b4332;">
                    <li>Reserve margin increased from 17.8% to 19.1%</li>
                    <li>Supply offered decreased by 500 MW</li>
                    <li>Energy efficiency resources not eligible</li>
                    <li>Supply chain issues impair new capacity</li>
                    <li>Long interconnection queue delays</li>
                </ul>
            </div>
        </div>
    </div>

    <!-- Slide 10: MISO Auction Update -->
    <div class="slide-container">
        <div class="slide-header">
            <div class="slide-title">MISO Planning Resource Auction</div>
            <div class="slide-subtitle">Software Error Correction Impact</div>
        </div>
        <div class="slide-content">
            <div class="two-column">
                <div>
                    <h3>The Issue</h3>
                    <ul class="bullet-points">
                        <li>Software error in Loss of Load Expectation (LOLE) calculation</li>
                        <li>Error dates back to 2018/19 auction</li>
                        <li>Impacts Planning Reserve Margins (PRM)</li>
                        <li>Discovered in June 2025</li>
                    </ul>
                </div>
                <div>
                    <h3>The Solution</h3>
                    <ul class="bullet-points">
                        <li>MISO will NOT re-run the auction</li>
                        <li>Recalculating based on original volumes</li>
                        <li>Tariff allows correction up to one year back</li>
                        <li>Adjustments via miscellaneous charges</li>
                    </ul>
                </div>
            </div>
            <div class="data-visualization">
                <h3>MISO Reliability Metrics Timeline</h3>
                <div class="bar-chart">
                    <div class="bar" style="height: 45%;">
                        <div class="bar-value">Error</div>
                        <div class="bar-label">2018-2024</div>
                    </div>
                    <div class="bar" style="height: 75%;">
                        <div class="bar-value">Discovery</div>
                        <div class="bar-label">Jun 2025</div>
                    </div>
                    <div class="bar" style="height: 60%;">
                        <div class="bar-value">Fix</div>
                        <div class="bar-label">2025/26</div>
                    </div>
                </div>
            </div>
            <div class="highlight-box">
                Final settlement impacts will be revealed in upcoming seasonal statements
            </div>
        </div>
    </div>

    <!-- Slide 11: Gas Pricing -->
    <div class="slide-container">
        <div class="slide-header">
            <div class="slide-title">NYMEX Natural Gas Pricing</div>
            <div class="slide-subtitle">Forward Curve Analysis</div>
        </div>
        <div class="slide-content">
            <div class="key-metrics">
                <div class="metric-card">
                    <div class="metric-value">$3.92</div>
                    <div class="metric-label">Cal '26 Current</div>
                </div>
                <div class="metric-card">
                    <div class="metric-value">$3.93</div>
                    <div class="metric-label">Cal '27 Current</div>
                </div>
                <div class="metric-card">
                    <div class="metric-value">$3.81</div>
                    <div class="metric-label">Cal '28 Current</div>
                </div>
                <div class="metric-card">
                    <div class="metric-value">$3.69</div>
                    <div class="metric-label">Cal '29 Current</div>
                </div>
            </div>
            <div class="data-visualization">
                <h3>NYMEX Forward Curve</h3>
                <div class="bar-chart">
                    <div class="bar" style="height: 78%;">
                        <div class="bar-value">$3.92</div>
                        <div class="bar-label">2026</div>
                    </div>
                    <div class="bar" style="height: 79%;">
                        <div class="bar-value">$3.93</div>
                        <div class="bar-label">2027</div>
                    </div>
                    <div class="bar" style="height: 76%;">
                        <div class="bar-value">$3.81</div>
                        <div class="bar-label">2028</div>
                    </div>
                    <div class="bar" style="height: 74%;">
                        <div class="bar-value">$3.69</div>
                        <div class="bar-label">2029</div>
                    </div>
                </div>
            </div>
            <div class="chart-container">
                <h3>Forward Curve vs Historical Average</h3>
                <table class="table">
                    <tr><th>Year</th><th>Current</th><th>3-Yr Avg</th><th>vs Avg</th></tr>
                    <tr><td>2026</td><td>$3.92</td><td>$4.03</td><td style="color: #d32f2f;">-3%</td></tr>
                    <tr><td>2027</td><td>$3.93</td><td>$3.96</td><td style="color: #d32f2f;">-1%</td></tr>
                    <tr><td>2028</td><td>$3.81</td><td>$3.90</td><td style="color: #d32f2f;">-2%</td></tr>
                    <tr><td>2029</td><td>$3.69</td><td>$3.88</td><td style="color: #d32f2f;">-5%</td></tr>
                </table>
            </div>
        </div>
    </div>

    <!-- Slide 12: Power Prices -->
    <div class="slide-container">
        <div class="slide-header">
            <div class="slide-title">Regional Power Price Forwards</div>
            <div class="slide-subtitle">RTC Forward Power Prices ($/MWh)</div>
        </div>
        <div class="slide-content">
            <div class="chart-grid">
                <div class="chart-container">
                    <h4>Northeast Markets ($/MWh)</h4>
                    <div class="bar-chart" style="height: 150px;">
                        <div class="bar" style="height: 60%;">
                            <div class="bar-value">$47</div>
                            <div class="bar-label">NYISO A</div>
                        </div>
                        <div class="bar" style="height: 80%;">
                            <div class="bar-value">$55</div>
                            <div class="bar-label">NYISO J</div>
                        </div>
                        <div class="bar" style="height: 85%;">
                            <div class="bar-value">$65</div>
                            <div class="bar-label">ISONE</div>
                        </div>
                    </div>
                </div>
                <div class="chart-container">
                    <h4>PJM Markets ($/MWh)</h4>
                    <div class="bar-chart" style="height: 150px;">
                        <div class="bar" style="height: 70%;">
                            <div class="bar-value">$48</div>
                            <div class="bar-label">AD Hub</div>
                        </div>
                        <div class="bar" style="height: 80%;">
                            <div class="bar-value">$55</div>
                            <div class="bar-label">West Hub</div>
                        </div>
                        <div class="bar" style="height: 65%;">
                            <div class="bar-value">$45</div>
                            <div class="bar-label">NI Hub</div>
                        </div>
                    </div>
                </div>
                <div class="chart-container">
                    <h4>Western Markets ($/MWh)</h4>
                    <div class="bar-chart" style="height: 150px;">
                        <div class="bar" style="height: 75%;">
                            <div class="bar-value">$58</div>
                            <div class="bar-label">CAISO NP15</div>
                        </div>
                        <div class="bar" style="height: 70%;">
                            <div class="bar-value">$48</div>
                            <div class="bar-label">CAISO SP15</div>
                        </div>
                        <div class="bar" style="height: 68%;">
                            <div class="bar-value">$52</div>
                            <div class="bar-label">ERCOT</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Slide 13: DOE Emergency Orders -->
    <div class="slide-container">
        <div class="slide-header">
            <div class="slide-title">DOE Emergency Orders</div>
            <div class="slide-subtitle">Reliability Concerns Drive Plant Delays</div>
        </div>
        <div class="slide-content">
            <div class="two-column">
                <div>
                    <h3>J.H. Campbell Plant (MISO)</h3>
                    <ul class="bullet-points">
                        <li>Consumers Energy directed to delay shutdown</li>
                        <li>1.6 GW capacity</li>
                        <li>90-day extension from May 23rd</li>
                        <li>Based on MISO Summer Reliability Assessment</li>
                    </ul>
                </div>
                <div>
                    <h3>Eddystone Plant (PJM)</h3>
                    <ul class="bullet-points">
                        <li>Constellation ordered to continue operations</li>
                        <li>760 MW capacity (two units)</li>
                        <li>Extended until August 28th</li>
                        <li>Based on PJM Summer Outlook concerns</li>
                    </ul>
                </div>
            </div>
            <div class="data-visualization">
                <h3>Emergency Order Impact</h3>
                <div class="bar-chart">
                    <div class="bar" style="height: 85%;">
                        <div class="bar-value">1,600 MW</div>
                        <div class="bar-label">Campbell</div>
                    </div>
                    <div class="bar" style="height: 50%;">
                        <div class="bar-value">760 MW</div>
                        <div class="bar-label">Eddystone</div>
                    </div>
                    <div class="bar" style="height: 90%;">
                        <div class="bar-value">90 Days</div>
                        <div class="bar-label">Extension</div>
                    </div>
                </div>
            </div>
            <div class="highlight-box">
                Customer Takeaway: Strong load growth may delay additional thermal plant retirements. RTO costs will be passed through to customers.
            </div>
        </div>
    </div>

    <!-- Slide 14: Market Temperature -->
    <div class="slide-container">
        <div class="slide-header">
            <div class="slide-title">Market Temperature</div>
            <div class="slide-subtitle">Fundamental Analysis Rating</div>
        </div>
        <div class="slide-content">
            <div class="data-visualization" style="background: linear-gradient(90deg, #f44336 0%, #ff9800 25%, #ffeb3b 50%, #8bc34a 75%, #4caf50 100%);">
                <h3 style="color: white; text-align: center; margin-bottom: 30px; text-shadow: 0 2px 10px rgba(0,0,0,0.5);">Market Temperature Scale</h3>
                <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; color: white;">
                    <div style="text-align: center; background: rgba(0,0,0,0.4); padding: 20px; border-radius: 15px; backdrop-filter: blur(10px);">
                        <div style="font-weight: bold; font-size: 1.1em;">Weather</div>
                        <div style="font-size: 1.8em; margin: 10px 0;">Neutral</div>
                        <div style="font-size: 0.9em; opacity: 0.8;">Variable patterns expected</div>
                    </div>
                    <div style="text-align: center; background: rgba(0,0,0,0.4); padding: 20px; border-radius: 15px; backdrop-filter: blur(10px);">
                        <div style="font-weight: bold; font-size: 1.1em;">Economics</div>
                        <div style="font-size: 1.8em; margin: 10px 0;">Bearish</div>
                        <div style="font-size: 0.9em; opacity: 0.8;">Tariff concerns weigh</div>
                    </div>
                    <div style="text-align: center; background: rgba(0,0,0,0.4); padding: 20px; border-radius: 15px; backdrop-filter: blur(10px);">
                        <div style="font-weight: bold; font-size: 1.1em;">Production</div>
                        <div style="font-size: 1.8em; margin: 10px 0;">Bullish</div>
                        <div style="font-size: 0.9em; opacity: 0.8;">Record levels sustained</div>
                    </div>
                    <div style="text-align: center; background: rgba(0,0,0,0.4); padding: 20px; border-radius: 15px; backdrop-filter: blur(10px);">
                        <div style="font-weight: bold; font-size: 1.1em;">Storage</div>
                        <div style="font-size: 1.8em; margin: 10px 0;">Neutral</div>
                        <div style="font-size: 0.9em; opacity: 0.8;">Above average levels</div>
                    </div>
                    <div style="text-align: center; background: rgba(0,0,0,0.4); padding: 20px; border-radius: 15px; backdrop-filter: blur(10px);">
                        <div style="font-weight: bold; font-size: 1.1em;">Global Situation</div>
                        <div style="font-size: 1.8em; margin: 10px 0;">Bullish</div>
                        <div style="font-size: 0.9em; opacity: 0.8;">Export opportunities</div>
                    </div>
                    <div style="text-align: center; background: rgba(0,0,0,0.4); padding: 20px; border-radius: 15px; backdrop-filter: blur(10px);">
                        <div style="font-weight: bold; font-size: 1.1em;">LNG Production</div>
                        <div style="font-size: 1.8em; margin: 10px 0;">Bullish</div>
                        <div style="font-size: 0.9em; opacity: 0.8;">Strong demand growth</div>
                    </div>
                </div>
            </div>
            <div class="highlight-box">
                Overall Market Assessment: Moderately Bullish
            </div>
        </div>
    </div>

    <!-- Slide 15: Key Takeaways -->
    <div class="slide-container">
        <div class="slide-header">
            <div class="slide-title">Key Takeaways</div>
            <div class="slide-subtitle">Strategic Market Insights</div>
        </div>
        <div class="slide-content">
            <div class="key-metrics">
                <div class="metric-card" style="grid-column: span 2;">
                    <div class="metric-value">Trade Dominance</div>
                    <div class="metric-label">$1T+ in energy export commitments position U.S. as global leader</div>
                </div>
                <div class="metric-card" style="grid-column: span 2;">
                    <div class="metric-value">Infrastructure Gap</div>
                    <div class="metric-label">Current LNG capacity may need significant expansion</div>
                </div>
            </div>
            <ul class="bullet-points">
                <li><strong>Record Production:</strong> Natural gas production at near-record levels with improving efficiency</li>
                <li><strong>Storage Health:</strong> On track for full storage by October despite seasonal demand</li>
                <li><strong>Capacity Crunch:</strong> PJM auction results highlight supply-demand imbalance</li>
                <li><strong>Renewable Headwinds:</strong> Offshore wind policy changes create fossil fuel opportunities</li>
                <li><strong>Global Dynamics:</strong> Russia-China pipeline affects global LNG trade flows</li>
                <li><strong>Reliability Focus:</strong> DOE emergency orders show grid reliability concerns</li>
                <li><strong>Price Outlook:</strong> Forward curves reflect bullish long-term fundamentals</li>
            </ul>
            <div class="highlight-box">
                Next Webinar: Winter outlook, trade negotiation updates, and economic analysis in four weeks
            </div>
        </div>
    </div>

    <!-- Slide 16: Contact & Next Steps -->
    <div class="slide-container">
        <div class="slide-header">
            <div class="slide-title">Contact Information</div>
            <div class="slide-subtitle">Stay Connected for Market Updates</div>
        </div>
        <div class="slide-content">
            <div class="two-column">
                <div>
                    <h3>Market Intelligence Team</h3>
                    <ul class="bullet-points">
                        <li>Email: CMG@Constellation.com</li>
                        <li>Subscribe: www.Constellation.com/Subscribe</li>
                        <li>Next Webinar: Four weeks</li>
                        <li>Focus: Official winter outlook</li>
                    </ul>
                </div>
                <div>
                    <h3>Upcoming Events</h3>
                    <ul class="bullet-points">
                        <li>Constellation Sustainability Summit</li>
                        <li>Date: October 16-17, 2025</li>
                        <li>Location: Carmel, CA</li>
                        <li>Contact your BDM for invitations</li>
                    </ul>
                </div>
            </div>
            <div class="data-visualization">
                <div style="text-align: center; padding: 30px;">
                    <h2 style="color: #2e7d32; margin-bottom: 15px;">Thank You</h2>
                    <p style="font-size: 1.2em; margin-bottom: 10px;">For attending the Constellation Energy Market Intelligence Webinar</p>
                    <p style="font-style: italic; color: #388e3c;"><strong>September 10, 2025</strong></p>
                </div>
            </div>
            <div class="highlight-box">
                Join thought leaders in sustainability and energy market analysis
            </div>
        </div>
    </div>

    <div class="navigation">
