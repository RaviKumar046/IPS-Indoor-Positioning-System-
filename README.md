<!DOCTYPE html>
<html lang="en" class="dark">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>ESP32 Tag</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@200;300;400;500;600;700;800&display=swap" rel="stylesheet">
  <style>
    :root {
      /* Professional palette using RGBA values */
      --bg: rgba(7, 16, 38, 1); /* deep slate */
      --bg-secondary: rgba(11, 18, 32, 1); /* slightly lighter slate */
      --bg-gradient: linear-gradient(135deg, rgba(7,16,38,1) 0%, rgba(11,18,32,1) 50%, rgba(7,20,40,1) 100%);
      --glass: rgba(255, 255, 255, 0.03);
      --glass-strong: rgba(255, 255, 255, 0.05);
      --card: rgba(255, 255, 255, 0.03);
      --border: rgba(148, 163, 184, 0.08);
      --border-hover: rgba(148, 163, 184, 0.16);
      --border-accent: rgba(59, 130, 246, 0.12);
      --text: rgba(230, 238, 248, 1); /* soft off-white */
      --text-muted: rgba(159, 179, 217, 1);
      --text-dim: rgba(127, 152, 182, 1);
      --accent: rgba(59, 130, 246, 1); /* professional blue */
      --accent-light: rgba(96, 165, 250, 1);
      --accent-dark: rgba(30, 58, 138, 1);
      --accent-green: rgba(16, 185, 129, 1); /* current location green */
      --success: rgba(22, 163, 74, 1);
      --danger: rgba(239, 68, 68, 1);
      --warning: rgba(245, 158, 11, 1);
      --gradient-primary: linear-gradient(135deg, rgba(59,130,246,1) 0%, rgba(99,102,241,1) 100%);
      --gradient-card: linear-gradient(145deg, rgba(59,130,246,0.06), rgba(99,102,241,0.03));
      --radius: 16px;
      --radius-small: 12px;
      --shadow: 0 10px 25px -5px rgba(2, 6, 23, 0.6);
      --shadow-lg: 0 20px 40px -10px rgba(2, 6, 23, 0.7);
    }

    * {
      box-sizing: border-box;
    }

    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
    }

    body {
      font-family: 'Inter', -apple-system, sans-serif;
      background: var(--bg-gradient);
      background-attachment: fixed;
      color: var(--text);
      padding: 2rem;
      min-height: 100vh;
      overflow-x: hidden;
      position: relative;
      line-height: 1.6;
    }



    .wrap {
      max-width: 1400px;
      margin: 0 auto;
      display: grid;
      grid-template-columns: repeat(12, 1fr);
      gap: 1.5rem;
      align-items: start;
      position: relative;
      z-index: 1;
    }

    header {
      grid-column: 1 / -1;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1.5rem 2rem;
      background: var(--card);
      backdrop-filter: blur(30px);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      margin-bottom: 0.5rem;
    }

    .status-badge {
      display: flex;
      align-items: center;
      gap: 0.75rem;
      padding: 0.75rem 1.25rem;
      background: rgba(14, 165, 233, 0.1);
      border: 1px solid var(--border);
      border-radius: var(--radius-small);
      font-size: 0.875rem;
    }

    .header-controls {
      display: flex;
      align-items: center;
      gap: 1rem;
    }

    .control-buttons {
      display: flex;
      gap: 0.5rem;
    }

    .btn-control {
      padding: 0.65rem 1.25rem;
      border: none;
      border-radius: var(--radius-small);
      font-weight: 600;
      font-size: 0.875rem;
      cursor: pointer;
      transition: all 0.3s ease;
      text-transform: uppercase;
      letter-spacing: 0.05em;
    }

    .btn-start {
      background: var(--gradient-primary);
      color: white;
      border: 1px solid var(--accent);
    }

    .btn-start:hover:not(:disabled) {
      transform: translateY(-2px);
      box-shadow: 0 4px 12px rgba(14, 165, 233, 0.4);
    }

    .btn-stop {
      background: var(--danger);
      color: white;
      border: 1px solid var(--danger);
    }

    .btn-stop:hover:not(:disabled) {
      background: #dc2626;
      transform: translateY(-2px);
      box-shadow: 0 4px 12px rgba(239, 68, 68, 0.4);
    }

    .btn-reset {
      background: rgba(36, 230, 19, 0.15);
      color: var(--text-muted);
      border: 1px solid var(--border);
    }

    .btn-reset:hover:not(:disabled) {
      background: rgba(148, 163, 184, 0.25);
      color: var(--text);
      transform: translateY(-2px);
    }

    .btn-control:disabled {
      opacity: 0.4;
      cursor: not-allowed;
      transform: none !important;
    }



    h1 {
      font-size: clamp(1.5rem, 4vw, 2.25rem);
      font-weight: 800;
      margin: 0;
      background: var(--gradient-primary);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      letter-spacing: -0.025em;
    }

    .lead {
      margin: 0.5rem 0 0;
      color: var(--text-muted);
      font-size: clamp(0.875rem, 2.5vw, 1rem);
      font-weight: 400;
      letter-spacing: 0.025em;
    }



    .card {
      background: var(--card);
      backdrop-filter: blur(30px);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      padding: 1.75rem;
      transition: all 0.3s ease;
      position: relative;
      overflow: hidden;
      display: flex;
      flex-direction: column;
    }



    .card:hover {
      border-color: var(--border-hover);
    }

    .card-header {
      display: flex;
      align-items: center;
      gap: 0.75rem;
      margin-bottom: 1.5rem;
      padding-bottom: 1rem;
      border-bottom: 1px solid rgba(255,255,255,0.05);
    }

    .card-title {
      font-size: clamp(1rem, 3vw, 1.25rem);
      font-weight: 700;
      color: var(--text);
      margin: 0;
      flex: 1;
    }

    .main {
      grid-column: 1 / -1;
      display: flex;
      flex-direction: column;
      gap: 1.5rem;
    }

    .predicted {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 1.5rem;
    }

    @media (max-width: 768px) {
      .predicted {
        grid-template-columns: 1fr;
      }
    }

    .map-canvas-container {
      position: relative;
      width: 100%;
      height: 500px;
      background: rgba(15, 23, 42, 0.4);
      border-radius: var(--radius-small);
      overflow: hidden;
      border: 1px solid var(--border);
    }

    #mapCanvas {
      width: 100%;
      height: 100%;
      display: block;
    }

    .map-info {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 0.75rem 1rem;
      background: rgba(14, 165, 233, 0.05);
      border-radius: var(--radius-small);
      border: 1px solid var(--border);
      margin-top: 1rem;
      font-size: 0.875rem;
    }

    .map-info-item {
      display: flex;
      flex-direction: column;
      gap: 0.25rem;
    }

    .map-info-label {
      color: var(--text-dim);
      font-size: 0.75rem;
      text-transform: uppercase;
      letter-spacing: 0.05em;
    }

    .map-info-value {
      color: var(--text);
      font-weight: 600;
    }

    .map-legend {
      display: flex;
      gap: 1.5rem;
      margin-top: 1rem;
      flex-wrap: wrap;
    }

    .legend-item {
      display: flex;
      align-items: center;
      gap: 0.5rem;
      font-size: 0.875rem;
      color: var(--text-muted);
    }

    .legend-dot {
      width: 12px;
      height: 12px;
      border-radius: 50%;
      flex-shrink: 0;
    }

    .legend-line {
      width: 24px;
      height: 2px;
      flex-shrink: 0;
    }

    .loc {
      background: var(--gradient-card);
      backdrop-filter: blur(20px);
      border: 1px solid var(--border-accent);
      border-radius: var(--radius);
      padding: 2rem;
      text-align: center;
      position: relative;
      box-shadow: 0 8px 20px rgba(14, 165, 233, 0.2);
    }



    .loc .title {
      font-size: 0.875rem;
      font-weight: 600;
      color: var(--text-muted);
      margin-bottom: 1rem;
      letter-spacing: 0.1em;
      text-transform: uppercase;
    }

    .loc .value {
      font-size: clamp(2rem, 8vw, 3rem);
      font-weight: 800;
      background: var(--gradient-primary);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      letter-spacing: -0.05em;
      margin: 0;
    }

    .stats {
      display: grid;
      grid-template-columns: 1fr;
      gap: 1rem;
    }

    .stat-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1rem 1.25rem;
      background: rgba(14, 165, 233, 0.05);
      border: 1px solid var(--border);
      border-radius: var(--radius-small);
      transition: all 0.3s ease;
    }

    .stat-item:hover {
      background: rgba(255,255,255,0.06);
    }

    .stat-label {
      font-size: 0.875rem;
      color: var(--text-dim);
      font-weight: 500;
    }

    .stat-value {
      font-size: 1.5rem;
      font-weight: 700;
      color: var(--text);
    }

    .top3-list {
      display: flex;
      flex-direction: column;
      gap: 1rem;
      margin: 0;
      padding: 0;
      list-style: none;
      flex: 1;
    }

    .top3-item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 1.25rem 1.5rem;
      border: 1px solid var(--border);
      border-left: 3px solid var(--accent);
      border-radius: var(--radius-small);
      cursor: pointer;
      transition: all 0.3s ease;
      background: rgba(14, 165, 233, 0.03);
      backdrop-filter: blur(10px);
    }





    .top3-item:hover {
      background: rgba(14, 165, 233, 0.08);
      border-left-color: var(--accent-light);
      transform: translateX(4px);
    }

    .top3-item.selected {
      background: rgba(14, 165, 233, 0.12);
      border-left-color: var(--accent-green);
      border-left-width: 4px;
    }

    .top3-content {
      display: flex;
      align-items: center;
      gap: 1.25rem;
      flex: 1;
    }

    .top3-rank {
      width: 32px;
      height: 32px;
      border-radius: 50%;
      background: var(--gradient-primary);
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 700;
      font-size: 0.875rem;
      color: white;
      flex-shrink: 0;
    }

    .top3-name {
      font-weight: 700;
      font-size: 1.125rem;
      color: var(--text);
      flex: 1;
    }

    .top3-bar {
      width: 160px;
      height: 10px;
      border-radius: 9999px;
      background: rgba(255,255,255,0.12);
      overflow: hidden;
      flex-shrink: 0;
      box-shadow: inset 0 2px 4px rgba(0,0,0,0.2);
    }

    .top3-fill {
      height: 100%;
      border-radius: 9999px;
      background: var(--gradient-primary);
      transition: width 0.6s cubic-bezier(0.4, 0, 0.2, 1);
      box-shadow: 0 0 20px currentColor;
      position: relative;
    }



    .top3-prob {
      font-size: 1.125rem;
      font-weight: 800;
      color: var(--accent);
      min-width: 80px;
      text-align: right;
    }

    .prob-table-container {
      overflow: auto;
      flex: 1;
    }

    table {
      width: 100%;
      border-collapse: separate;
      border-spacing: 0;
      font-size: 0.9375rem;
      min-width: 400px;
    }

    th, td {
      padding: 1.25rem 1rem;
      text-align: left;
    }

    th {
      color: var(--text-muted);
      font-weight: 600;
      font-size: 0.8125rem;
      text-transform: uppercase;
      letter-spacing: 0.1em;
      position: sticky;
      top: 0;
      background: var(--glass);
      z-index: 10;
    }

    tr {
      border-bottom: 1px solid var(--border);
      transition: all 0.2s ease;
    }

    tr:hover {
      background: rgba(255,255,255,0.05);
    }

    .prob-percent {
      font-weight: 800;
      color: var(--accent);
      text-align: right;
    }

    .btn {
      border: none;
      padding: 1rem 2rem;
      border-radius: 16px;
      font-weight: 700;
      font-size: 0.9375rem;
      cursor: pointer;
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
      backdrop-filter: blur(30px);
      position: relative;
      overflow: hidden;
      text-transform: uppercase;
      letter-spacing: 0.05em;
      flex: 1;
      min-width: 120px;
    }

    .btn-primary {
      background: var(--gradient-primary);
      color: white;
      box-shadow: 0 4px 12px rgba(14, 165, 233, 0.3);
      border: 1px solid var(--accent);
    }

    .btn-primary:hover:not(:disabled) {
      transform: translateY(-2px);
      box-shadow: 0 8px 20px rgba(14, 165, 233, 0.4);
    }

    .btn-secondary {
      background: rgba(148, 163, 184, 0.1);
      color: var(--text-muted);
      border: 1px solid var(--border);
    }

    .btn-secondary:hover:not(:disabled) {
      background: rgba(148, 163, 184, 0.15);
      border-color: var(--border-hover);
      color: var(--text);
    }

    .btn:disabled {
      opacity: 0.4;
      cursor: not-allowed;
      transform: none !important;
    }

    input {
      width: 100%;
      padding: 1.125rem 1.5rem;
      border: 1px solid var(--border);
      border-radius: var(--radius);
      background: rgba(255,255,255,0.06);
      backdrop-filter: blur(30px);
      color: var(--text);
      font-size: 0.9375rem;
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
      font-family: inherit;
      font-weight: 500;
    }

    input:focus {
      outline: none;
      border-color: var(--accent);
      box-shadow: 0 0 0 4px rgba(59,130,246,0.15), 0 0 0 1px var(--accent);
      background: rgba(255,255,255,0.1);
      transform: scale(1.02);
    }

    input::placeholder {
      color: var(--text-dim);
    }

    label {
      font-size: 0.875rem;
      color: var(--text-dim);
      font-weight: 500;
      margin-bottom: 0.75rem;
      display: block;
    }

    .status {
      display: flex;
      gap: 1rem;
      align-items: center;
    }

    .dot {
      width: 16px;
      height: 16px;
      border-radius: 50%;
      box-shadow: 0 0 20px currentColor;
      animation: pulse 1.5s infinite;
      position: relative;
      flex-shrink: 0;
    }



    .dot.ok { background: var(--success); color: var(--success); }
    .dot.fail { background: var(--danger); color: var(--danger); }

    @keyframes pulse {
      0%, 100% { opacity: 1; transform: scale(1); }
      50% { opacity: 0.7; transform: scale(1.1); }
    }







    .metric-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 1rem;
      margin-top: 1rem;
    }

    .metric-grid > div:last-child {
      text-align: right;
    }

    ol {
      padding-left: 1.75rem;
      margin: 0;
      color: var(--text-muted);
      font-size: 0.9375rem;
      line-height: 1.7;
      font-weight: 400;
    }

    footer {
      grid-column: 1 / -1;
      margin-top: 1rem;
      color: var(--text-dim);
      font-size: 0.875rem;
      text-align: center;
      padding: 1.5rem;
      border-top: 1px solid var(--border);
    }

    /* Responsive Design */

    @media (max-width: 768px) {
      .predicted { 
        grid-template-columns: 1fr; 
        text-align: center; 
        gap: 1.5rem; 
      }
      .controls { justify-content: center; }
      .metric-grid { grid-template-columns: 1fr; }
      .metric-badge { justify-content: center; }
      body { padding: 1rem; }
      .card { padding: 1.5rem; }
    }

    @media (max-width: 480px) {
      .wrap { gap: 1.5rem; }
      .top3-content { gap: 0.75rem; }
      .top3-bar { width: 120px; }
    }

    /* Scrollbar */
    ::-webkit-scrollbar { 
      width: 8px; 
      height: 8px;
    }
    ::-webkit-scrollbar-track { 
      background: rgba(255,255,255,0.03); 
    }
    ::-webkit-scrollbar-thumb { 
      background: var(--gradient-primary); 
      border-radius: 4px; 
      border: 2px solid transparent;
      background-clip: content-box;
    }
    ::-webkit-scrollbar-thumb:hover { 
      background: var(--accent-green); 
    }
  </style>
</head>
<body>
  <div class="wrap">
    <header class="card">
      <div>
        <h1>ESP32 Tag</h1>
        <b class="lead">Real-time indoor positioning system</b>
      </div>
      <div class="header-controls">
        <div class="control-buttons">
          <button id="startBtn" class="btn-control btn-start">Start</button>
          <button id="stopBtn" class="btn-control btn-stop" disabled>Stop</button>
          <button id="resetBtn" class="btn-control btn-reset">Reset</button>
        </div>
        <div class="status-badge">
          <div id="statusDot" class="dot fail" aria-hidden="true"></div>
          <div id="statusText" style="color: var(--text-muted); font-size: 0.875rem;">Ready</div>
        </div>
      </div>
    </header>

    <main class="main">
      <section class="card">
        <div class="card-header">
          <h2 class="card-title">Mini Campus</h2>
        </div>
        <div class="map-canvas-container">
          <canvas id="mapCanvas"></canvas>
        </div>
        <div class="map-info">
          <div class="map-info-item">
            <span class="map-info-label">Building</span>
            <span class="map-info-value" id="buildingId">TRI01</span>
          </div>
          <div class="map-info-item">
            <span class="map-info-label">Floor</span>
            <span class="map-info-value" id="floorId">1</span>
          </div>
          <div class="map-info-item">
            <span class="map-info-label">Total Nodes</span>
            <span class="map-info-value" id="nodeCount">0</span>
          </div>
        </div>
        <div class="map-legend">
          <div class="legend-item">
            <div class="legend-dot" style="background: #0ea5e9;"></div>
            <span>Rooms</span>
          </div>
          <div class="legend-item">
            <div class="legend-dot" style="background: #10b981; box-shadow: 0 0 10px #10b981; width: 16px; height: 16px;"></div>
            <span>Current Location</span>
          </div>
          <div class="legend-item">
            <div class="legend-dot" style="background: #f59e0b;"></div>
            <span>Corners</span>
          </div>
          <div class="legend-item">
            <div class="legend-line" style="background: rgba(148, 163, 184, 0.3);"></div>
            <span>Connections</span>
          </div>
        </div>
      </section>

      <section class="card predicted" aria-live="polite">
        <div class="loc" id="predictedBox">
          <div class="title">Predicted Location</div>
          <div class="value" id="predictedLocation">Loading...</div>
        </div>

        <div class="stats">
          <div class="stat-item">
            <div class="stat-label">Confidence</div>
            <div id="confidence" class="stat-value">--</div>
          </div>
          <div class="stat-item">
            <div class="stat-label">Last Updated</div>
            <div id="lastUpdated" class="stat-value">--</div>
          </div>
        </div>
      </section>

      <section class="card">
        <div class="card-header">
          <h2 class="card-title">Top 3 Predictions</h2>
        </div>
        <ul class="top3-list" id="top3List" role="list"></ul>
      </section>

      <section class="card">
        <div class="card-header">
          <h2 class="card-title">Complete Probability Matrix</h2>
        </div>
        <div class="prob-table-container">
          <table id="probTable" role="table" aria-label="probability table">
            <thead>
              <tr>
                <th>Location</th>
                <th>Probability</th>
              </tr>
            </thead>
            <tbody></tbody>
          </table>
        </div>
      </section>
    </main>

    <footer>
      Indoor Positioning System &copy; 2025
    </footer>
  </div>

  <script>
    // Config
    const API_URL = 'https://ips-u8u0.onrender.com';
    let ws = null;
    let reconnectInterval = null;
    let isTracking = false;
    let mapData = null;
    let currentLocation = null;

    // DOM elements
    const predictedLocationEl = document.getElementById("predictedLocation");
    const confidenceEl = document.getElementById("confidence");
    const lastUpdatedEl = document.getElementById("lastUpdated");
    const top3ListEl = document.getElementById("top3List");
    const probTableBody = document.querySelector("#probTable tbody");
    const statusDot = document.getElementById("statusDot");
    const statusText = document.getElementById("statusText");
    const startBtn = document.getElementById("startBtn");
    const stopBtn = document.getElementById("stopBtn");
    const resetBtn = document.getElementById("resetBtn");
    const mapCanvas = document.getElementById("mapCanvas");
    const buildingIdEl = document.getElementById("buildingId");
    const floorIdEl = document.getElementById("floorId");
    const nodeCountEl = document.getElementById("nodeCount");

    // Load map data
    function loadMapData() {
      // Embedded map data
      mapData = {
        "buildingId": "Mini Campus",
        "floorId": "1",
        "width": 1.0,
        "height": 1.0,
        "backgroundImage": null,
        "nodes": [
          { "id": "MINI_CAMPUS_F1_CORNER_A", "label": "Corner A", "x": 0.10, "y": 0.90 },
          { "id": "MINI_CAMPUS_F1_CORNER_B", "label": "Corner B", "x": 0.90, "y": 0.90 },
          { "id": "MINI_CAMPUS_F1_CORNER_C", "label": "Mini Reception", "x": 0.50, "y": 0.10 },
          { "id": "MINI_CAMPUS_F1_OAT", "label": "Open Air Theatre", "x": 0.50, "y": 0.50 },
          { "id": "MINI_CAMPUS_F1_ROOM_103", "label": "Room 103", "x": 0.180000, "y": 0.740000 },
          { "id": "MINI_CAMPUS_F1_ROOM_104", "label": "Room 104", "x": 0.260000, "y": 0.580000 },
          { "id": "MINI_CAMPUS_F1_ROOM_105", "label": "Room 105", "x": 0.340000, "y": 0.420000 },
          { "id": "MINI_CAMPUS_F1_ROOM_106", "label": "Room 106", "x": 0.420000, "y": 0.260000 },
          { "id": "MINI_CAMPUS_F1_ROOM_122", "label": "Room 122", "x": 0.820000, "y": 0.740000 },
          { "id": "MINI_CAMPUS_F1_ROOM_123", "label": "Room 123", "x": 0.740000, "y": 0.580000 },
          { "id": "MINI_CAMPUS_F1_ROOM_124", "label": "Room 124", "x": 0.660000, "y": 0.420000 },
          { "id": "MINI_CAMPUS_F1_ROOM_125", "label": "Room 125", "x": 0.580000, "y": 0.260000 },
          { "id": "MINI_CAMPUS_F1_ROOM_109", "label": "Room 109", "x": 0.166667, "y": 0.88 },
          { "id": "MINI_CAMPUS_F1_ROOM_110", "label": "Room 110", "x": 0.233333, "y": 0.88 },
          { "id": "MINI_CAMPUS_F1_ROOM_111", "label": "Room 111", "x": 0.300000, "y": 0.88 },
          { "id": "MINI_CAMPUS_F1_ROOM_112", "label": "Room 112", "x": 0.366667, "y": 0.88 },
          { "id": "MINI_CAMPUS_F1_ROOM_113", "label": "Room 113", "x": 0.433333, "y": 0.88 },
          { "id": "MINI_CAMPUS_F1_ROOM_114", "label": "Room 114", "x": 0.500000, "y": 0.88 },
          { "id": "MINI_CAMPUS_F1_ROOM_115", "label": "Room 115", "x": 0.566667, "y": 0.88 },
          { "id": "MINI_CAMPUS_F1_ROOM_116", "label": "Room 116", "x": 0.633333, "y": 0.88 },
          { "id": "MINI_CAMPUS_F1_ROOM_117", "label": "Room 117", "x": 0.700000, "y": 0.88 },
          { "id": "MINI_CAMPUS_F1_ROOM_118", "label": "Room 118", "x": 0.766667, "y": 0.88 },
          { "id": "MINI_CAMPUS_F1_ROOM_119", "label": "Room 119", "x": 0.833333, "y": 0.88 }
        ],
        "edges": [
          { "from": "MINI_CAMPUS_F1_CORNER_A", "to": "MINI_CAMPUS_F1_CORNER_B" },
          { "from": "MINI_CAMPUS_F1_CORNER_B", "to": "MINI_CAMPUS_F1_CORNER_C" },
          { "from": "MINI_CAMPUS_F1_CORNER_C", "to": "MINI_CAMPUS_F1_CORNER_A" },
          { "from": "MINI_CAMPUS_F1_CORNER_A", "to": "MINI_CAMPUS_F1_ROOM_103" },
          { "from": "MINI_CAMPUS_F1_ROOM_103", "to": "MINI_CAMPUS_F1_ROOM_104" },
          { "from": "MINI_CAMPUS_F1_ROOM_104", "to": "MINI_CAMPUS_F1_ROOM_105" },
          { "from": "MINI_CAMPUS_F1_ROOM_105", "to": "MINI_CAMPUS_F1_ROOM_106" },
          { "from": "MINI_CAMPUS_F1_ROOM_106", "to": "MINI_CAMPUS_F1_CORNER_C" },
          { "from": "MINI_CAMPUS_F1_CORNER_B", "to": "MINI_CAMPUS_F1_ROOM_122" },
          { "from": "MINI_CAMPUS_F1_ROOM_122", "to": "MINI_CAMPUS_F1_ROOM_123" },
          { "from": "MINI_CAMPUS_F1_ROOM_123", "to": "MINI_CAMPUS_F1_ROOM_124" },
          { "from": "MINI_CAMPUS_F1_ROOM_124", "to": "MINI_CAMPUS_F1_ROOM_125" },
          { "from": "MINI_CAMPUS_F1_ROOM_125", "to": "MINI_CAMPUS_F1_CORNER_C" },
          { "from": "MINI_CAMPUS_F1_CORNER_A", "to": "MINI_CAMPUS_F1_ROOM_109" },
          { "from": "MINI_CAMPUS_F1_ROOM_109", "to": "MINI_CAMPUS_F1_ROOM_110" },
          { "from": "MINI_CAMPUS_F1_ROOM_110", "to": "MINI_CAMPUS_F1_ROOM_111" },
          { "from": "MINI_CAMPUS_F1_ROOM_111", "to": "MINI_CAMPUS_F1_ROOM_112" },
          { "from": "MINI_CAMPUS_F1_ROOM_112", "to": "MINI_CAMPUS_F1_ROOM_113" },
          { "from": "MINI_CAMPUS_F1_ROOM_113", "to": "MINI_CAMPUS_F1_ROOM_114" },
          { "from": "MINI_CAMPUS_F1_ROOM_114", "to": "MINI_CAMPUS_F1_ROOM_115" },
          { "from": "MINI_CAMPUS_F1_ROOM_115", "to": "MINI_CAMPUS_F1_ROOM_116" },
          { "from": "MINI_CAMPUS_F1_ROOM_116", "to": "MINI_CAMPUS_F1_ROOM_117" },
          { "from": "MINI_CAMPUS_F1_ROOM_117", "to": "MINI_CAMPUS_F1_ROOM_118" },
          { "from": "MINI_CAMPUS_F1_ROOM_118", "to": "MINI_CAMPUS_F1_ROOM_119" },
          { "from": "MINI_CAMPUS_F1_ROOM_119", "to": "MINI_CAMPUS_F1_CORNER_B" }
        ]
      };
      
      buildingIdEl.textContent = mapData.buildingId;
      floorIdEl.textContent = `Floor ${mapData.floorId}`;
      nodeCountEl.textContent = mapData.nodes.length;
      drawMap();
    }

    // Draw map on canvas
    function drawMap() {
      if (!mapData || !mapCanvas) return;
      
      const ctx = mapCanvas.getContext('2d');
      const dpr = window.devicePixelRatio || 1;
      const rect = mapCanvas.getBoundingClientRect();
      
      // Set canvas size accounting for device pixel ratio
      mapCanvas.width = rect.width * dpr;
      mapCanvas.height = rect.height * dpr;
      ctx.scale(dpr, dpr);
      
      const width = rect.width;
      const height = rect.height;
      const padding = 40;
      const drawWidth = width - padding * 2;
      const drawHeight = height - padding * 2;
      
      // Clear canvas
      ctx.clearRect(0, 0, width, height);
      
      // Helper to convert normalized coords to canvas coords
      const toCanvasX = (x) => padding + x * drawWidth;
      const toCanvasY = (y) => padding + (1 - y) * drawHeight; // Flip Y axis
      
      // Draw edges first
      ctx.strokeStyle = 'rgba(148, 163, 184, 0.3)';
      ctx.lineWidth = 2;
      mapData.edges.forEach(edge => {
        const fromNode = mapData.nodes.find(n => n.id === edge.from);
        const toNode = mapData.nodes.find(n => n.id === edge.to);
        if (fromNode && toNode) {
          ctx.beginPath();
          ctx.moveTo(toCanvasX(fromNode.x), toCanvasY(fromNode.y));
          ctx.lineTo(toCanvasX(toNode.x), toCanvasY(toNode.y));
          ctx.stroke();
        }
      });
      
      // Draw nodes
      mapData.nodes.forEach(node => {
        const x = toCanvasX(node.x);
        const y = toCanvasY(node.y);
        const isCorner = node.id.includes('CORNER');
        const isOAT = node.id.includes('OAT');
        // Check if this node matches the current location
        const isCurrent = currentLocation && (
          node.label.toLowerCase() === currentLocation.toLowerCase() ||
          node.label.toLowerCase().includes(currentLocation.toLowerCase()) ||
          currentLocation.toLowerCase().includes(node.label.toLowerCase()) ||
          node.id.toLowerCase().includes(currentLocation.toLowerCase()) ||
          // Handle "Room 103" matching "103"
          (currentLocation.match(/\d+/) && node.label.includes(currentLocation.match(/\d+/)[0]))
        );
        
        // Draw node circle
        ctx.beginPath();
        ctx.arc(x, y, isCurrent ? 18 : 8, 0, Math.PI * 2);
        
        if (isCurrent) {
          // Big green glowing dot for current location with pulsing effect
          const pulsePhase = (Date.now() % 1500) / 1500; // 0 to 1 over 1.5 seconds
          const opacity = 0.6 + 0.4 * Math.sin(pulsePhase * Math.PI * 2);
          const glowIntensity = 20 + 15 * Math.sin(pulsePhase * Math.PI * 2);
          
          ctx.fillStyle = `rgba(16, 185, 129, ${opacity})`;
          ctx.shadowBlur = glowIntensity;
          ctx.shadowColor = '#10b981';
        } else if (isCorner) {
          ctx.fillStyle = '#f59e0b';
        } else if (isOAT) {
          ctx.fillStyle = '#8b5cf6';
        } else {
          ctx.fillStyle = '#0ea5e9';
        }
        
        ctx.fill();
        ctx.shadowBlur = 0;
        
        // Draw node border
        ctx.strokeStyle = isCurrent ? '#ffffff' : 'rgba(255, 255, 255, 0.3)';
        ctx.lineWidth = isCurrent ? 3 : 2;
        ctx.stroke();
        
        // Draw label
        ctx.fillStyle = '#f1f5f9';
        ctx.font = isCurrent ? 'bold 13px Inter' : '10px Inter';
        ctx.textAlign = 'center';
        ctx.textBaseline = 'bottom';
        ctx.fillText(node.label, x, y - (isCurrent ? 22 : 12));
      });
    }
    
    // Animation loop for blinking effect
    let animationFrameId = null;
    function animateMap() {
      if (currentLocation && mapData) {
        drawMap();
        animationFrameId = requestAnimationFrame(animateMap);
      }
    }

    // Helper functions
    function formatPct(v) {
      return (v * 100).toFixed(2) + "%";
    }

    function setStatus(ok, text) {
      statusDot.className = "dot " + (ok ? "ok" : "fail");
      statusText.textContent = text;
    }

    function render(data) {
      // Update current location for map
      currentLocation = data.location;
      console.log('Current location set to:', currentLocation);
      
      // Start animation if not already running
      if (currentLocation && !animationFrameId) {
        animateMap();
      } else if (!currentLocation && animationFrameId) {
        cancelAnimationFrame(animationFrameId);
        animationFrameId = null;
        drawMap();
      } else {
        drawMap();
      }
      
      // Predicted location
      predictedLocationEl.textContent = data.location || "—";
      
      // Confidence
      const conf = (data.probs && data.probs[data.location] !== undefined) 
        ? data.probs[data.location] 
        : (data.top3 && data.top3[0] ? data.top3[0][1] : 0);
      confidenceEl.textContent = formatPct(conf);
      
      // Last updated
      lastUpdatedEl.textContent = new Date().toLocaleString();

      // Top 3 list
      top3ListEl.innerHTML = "";
      (data.top3 || []).forEach(([name, prob], idx) => {
        const li = document.createElement("li");
        li.className = "top3-item";
        li.tabIndex = 0;
        li.setAttribute("role", "button");
        li.dataset.name = name;
        li.dataset.prob = prob;

        const content = document.createElement("div");
        content.className = "top3-content";

        const rank = document.createElement("div");
        rank.className = "top3-rank";
        rank.textContent = (idx + 1).toString();

        const nameEl = document.createElement("div");
        nameEl.className = "top3-name";
        nameEl.textContent = name;

        const barWrap = document.createElement("div");
        barWrap.className = "top3-bar";
        const barFill = document.createElement("div");
        barFill.className = "top3-fill";
        barFill.style.width = Math.max(5, Math.round(prob * 100)) + "%";
        barWrap.appendChild(barFill);

        content.appendChild(rank);
        content.appendChild(nameEl);
        content.appendChild(barWrap);

        const probEl = document.createElement("div");
        probEl.className = "top3-prob";
        probEl.textContent = formatPct(prob);

        li.appendChild(content);
        li.appendChild(probEl);

        // Click handler
        li.addEventListener("click", () => {
          document.querySelectorAll(".top3-item").forEach(e => e.classList.remove("selected"));
          li.classList.add("selected");
          predictedLocationEl.textContent = name;
          confidenceEl.textContent = formatPct(prob);
        });

        li.addEventListener("keydown", (ev) => {
          if (ev.key === "Enter" || ev.key === " ") {
            li.click();
            ev.preventDefault();
          }
        });

        top3ListEl.appendChild(li);
      });

      // Probability table
      const probs = data.probs || {};
      console.log('Probability data:', probs);
      const rows = Object.keys(probs)
        .map(k => ({ k, v: probs[k] }))
        .sort((a, b) => b.v - a.v);
      
      probTableBody.innerHTML = "";
      
      if (rows.length === 0) {
        // Show a message when no data is available
        const tr = document.createElement("tr");
        const td = document.createElement("td");
        td.colSpan = 2;
        td.style.textAlign = "center";
        td.style.color = "var(--text-dim)";
        td.style.fontStyle = "italic";
        td.style.padding = "2rem";
        td.textContent = "No probability data available. Click 'Start' to begin tracking.";
        tr.appendChild(td);
        probTableBody.appendChild(tr);
      } else {
        rows.forEach(r => {
          const tr = document.createElement("tr");
          const td1 = document.createElement("td");
          td1.textContent = r.k;
          const td2 = document.createElement("td");
          td2.className = "prob-percent";
          td2.textContent = formatPct(r.v);
          tr.appendChild(td1);
          tr.appendChild(td2);
          probTableBody.appendChild(tr);
        });
      }
    }

    function connectWebSocket() {
      if (!isTracking) return;
      
      const wsUrl = API_URL.replace('https://', 'wss://').replace('http://', 'ws://');
      console.log('Connecting to WebSocket:', `${wsUrl}/ws`);
      
      ws = new WebSocket(`${wsUrl}/ws`);
      
      ws.onopen = () => {
        console.log('WebSocket connected');
        setStatus(true, 'Live WebSocket Connected');
        if (reconnectInterval) {
          clearInterval(reconnectInterval);
          reconnectInterval = null;
        }
        
        // Send heartbeat every 30 seconds
        const heartbeat = setInterval(() => {
          if (ws.readyState === WebSocket.OPEN) {
            ws.send('ping');
          } else {
            clearInterval(heartbeat);
          }
        }, 30000);
      };
      
      ws.onmessage = (event) => {
        const data = JSON.parse(event.data);
        console.log('Received prediction:', data);
        console.log('Data structure:', {
          location: data.location,
          hasProbs: !!data.probs,
          probsKeys: data.probs ? Object.keys(data.probs).length : 0,
          hasTop3: !!data.top3,
          top3Length: data.top3 ? data.top3.length : 0
        });
        render(data);
      };
      
      ws.onerror = (error) => {
        console.error('WebSocket error:', error);
        setStatus(false, 'WebSocket error');
      };
      
      ws.onclose = () => {
        console.log('WebSocket disconnected');
        
        if (isTracking) {
          setStatus(false, 'Disconnected - Reconnecting...');
          // Auto-reconnect after 3 seconds
          if (!reconnectInterval) {
            reconnectInterval = setInterval(() => {
              console.log('Attempting to reconnect...');
              connectWebSocket();
            }, 3000);
          }
        } else {
          setStatus(false, 'Stopped');
        }
      };
    }

    function disconnectWebSocket() {
      if (reconnectInterval) {
        clearInterval(reconnectInterval);
        reconnectInterval = null;
      }
      if (ws) {
        ws.close();
        ws = null;
      }
    }

    function startTracking() {
      if (isTracking) return;
      
      isTracking = true;
      startBtn.disabled = true;
      stopBtn.disabled = false;
      setStatus(false, "Connecting to Live API...");
      connectWebSocket();
    }

    function stopTracking() {
      if (!isTracking) return;
      
      isTracking = false;
      startBtn.disabled = false;
      stopBtn.disabled = true;
      disconnectWebSocket();
      setStatus(false, 'Stopped');
      
      // Stop animation
      if (animationFrameId) {
        cancelAnimationFrame(animationFrameId);
        animationFrameId = null;
      }
      currentLocation = null;
      drawMap();
    }

    function resetData() {
      // Reset display
      predictedLocationEl.textContent = "--";
      confidenceEl.textContent = "--";
      lastUpdatedEl.textContent = "--";
      top3ListEl.innerHTML = "";
      probTableBody.innerHTML = "";
      
      // If tracking, reconnect
      if (isTracking) {
        disconnectWebSocket();
        setTimeout(() => {
          connectWebSocket();
        }, 500);
      }
    }

    // Button event listeners
    startBtn.addEventListener('click', startTracking);
    stopBtn.addEventListener('click', stopTracking);
    resetBtn.addEventListener('click', resetData);

    // Page visibility handling - reconnect WebSocket if page becomes visible
    document.addEventListener("visibilitychange", () => {
      if (!document.hidden && isTracking && ws && ws.readyState !== WebSocket.OPEN) {
        connectWebSocket();
      }
    });

    // Initialize - ready state, user must click Start
    document.addEventListener("DOMContentLoaded", () => {
      setStatus(false, "Ready to start");
      predictedLocationEl.textContent = "--";
      confidenceEl.textContent = "--";
      lastUpdatedEl.textContent = "--";
      
      // Show initial message in probability table
      const tr = document.createElement("tr");
      const td = document.createElement("td");
      td.colSpan = 2;
      td.style.textAlign = "center";
      td.style.color = "var(--text-dim)";
      td.style.fontStyle = "italic";
      td.style.padding = "2rem";
      td.textContent = "No probability data available. Click 'Start' to begin tracking.";
      tr.appendChild(td);
      probTableBody.appendChild(tr);
      
      loadMapData();
    });

    // Redraw map on window resize
    window.addEventListener('resize', () => {
      if (mapData) {
        // Cancel animation temporarily
        if (animationFrameId) {
          cancelAnimationFrame(animationFrameId);
          animationFrameId = null;
        }
        drawMap();
        // Restart animation if there's a current location
        if (currentLocation) {
          animateMap();
        }
      }
    });
  </script>
</body>
</html>
