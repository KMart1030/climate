<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Computer Science Certification Project — Climate Action App</title>
  <style>
    :root{
      --bg:#0f172a;          /* slate-900 */
      --panel:#111827;       /* gray-900 */
      --muted:#cbd5e1;       /* slate-300 */
      --text:#e5e7eb;        /* gray-200 */
      --accent:#22c55e;      /* green-500 */
      --accent-2:#38bdf8;    /* sky-400 */
      --danger:#f43f5e;      /* rose-500 */
      --card:#0b1220;
      --chip:#1f2937;
      --border:#22304b;
      --focus:#fbbf24;       /* amber-400 */
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family:system-ui,-apple-system,Segoe UI,Roboto,Inter,Arial,Helvetica,sans-serif;
      background: radial-gradient(1200px 800px at 10% -10%, #16213e 0%, var(--bg) 60%) fixed;
      color:var(--text);
      line-height:1.45;
    }
    header{
      position:sticky; top:0; z-index:20;
      backdrop-filter: blur(8px);
      background: #0b1020cc; border-bottom:1px solid var(--border);
    }
    .wrap{max-width:1100px;margin:auto;padding:18px}
    h1{font-size:clamp(22px,4vw,36px); margin:0 0 6px}
    h2{font-size:clamp(18px,3vw,26px); margin:18px 0 10px}
    p.lead{color:var(--muted); margin:6px 0 0}
    nav{display:flex;gap:8px; flex-wrap:wrap; margin-top:12px}
    nav button{
      background:var(--chip); color:var(--text);
      border:1px solid var(--border); border-radius:10px;
      padding:10px 14px; cursor:pointer; font-weight:600;
    }
    nav button.active{outline:2px solid var(--accent-2)}
    main{padding:20px 16px 60px}
    .grid{display:grid; gap:18px}
    @media (min-width:900px){ .grid-2{grid-template-columns:1fr 1fr} }
    .card{
      background: linear-gradient(180deg, #0c1325, #0a1122);
      border:1px solid var(--border); border-radius:14px;
      padding:18px;
      box-shadow: 0 10px 20px #00000040 inset, 0 1px 0 #ffffff06;
    }
    label{display:block; margin:10px 0 6px; font-weight:600}
    input, select, textarea{
      width:100%; padding:10px 12px; border-radius:10px;
      border:1px solid var(--border); background:#0a1224; color:var(--text);
      outline:none;
    }
    input:focus, select:focus, textarea:focus{outline:2px solid var(--focus)}
    .row{display:grid; grid-template-columns:1fr 1fr; gap:12px}
    .btn{
      display:inline-flex; align-items:center; justify-content:center; gap:8px;
      padding:10px 14px; border-radius:10px; border:1px solid var(--border);
      background:#0a1327; color:var(--text); cursor:pointer; font-weight:700;
    }
    .btn.primary{background:linear-gradient(90deg, #1f9d5a, #16a34a); border-color:#1f9d5a}
    .btn.subtle{background:#0a1224}
    .btn.danger{background:#1e0d15; border-color:#3b0d1a; color:#fecdd3}
    details{
      border:1px solid var(--border); border-radius:12px; overflow:hidden;
      background:#0b1220;
    }
    summary{
      list-style:none; padding:14px 16px; cursor:pointer; font-weight:700;
      display:flex; align-items:center; justify-content:space-between; gap:10px;
    }
    summary::-webkit-details-marker{display:none}
    details > div{padding:0 16px 16px}
    .pill{
      display:inline-block; padding:5px 10px; border-radius:999px; background:var(--chip);
      border:1px solid var(--border); color:var(--muted); font-size:12px; margin-left:6px;
    }
    .total{
      font-size:clamp(22px, 4vw, 34px); font-weight:900;
      background:linear-gradient(90deg, #60a5fa, #34d399); -webkit-background-clip:text; color:transparent;
    }
    .muted{color:var(--muted)}
    table{width:100%; border-collapse:collapse; font-size:14px}
    th,td{padding:10px; border-bottom:1px dashed var(--border)}
    th{text-align:left; color:#c7d2fe}
    .flex{display:flex; gap:10px; flex-wrap:wrap; align-items:center}
    .badge{background:#13213e; border:1px solid #2a3f79; padding:8px 10px; border-radius:10px}
    .right{margin-left:auto}
    .footer{opacity:.8; font-size:12px; margin-top:22px}
    .notice{border-left:4px solid var(--accent-2); padding:8px 12px; background:#0a1428; border-radius:8px}
    .sr-only{position:absolute;left:-10000px;top:auto;width:1px;height:1px;overflow:hidden;}
  </style>
</head>
<body>
  <header>
    <div class="wrap">
      <h1>Climate Action Hub <span class="pill">Computer Science Certification Project</span></h1>
      <p class="lead">Track your daily carbon footprint (energy, food, transport), get tips & challenges, and earn rewards for eco-friendly actions.</p>
      <nav aria-label="Primary">
        <button class="tab-btn active" data-tab="tracker" aria-controls="panel-tracker">Tracker</button>
        <button class="tab-btn" data-tab="tips" aria-controls="panel-tips">Tips & Challenges</button>
        <button class="tab-btn" data-tab="rewards" aria-controls="panel-rewards">Rewards</button>
        <button class="tab-btn" data-tab="about" aria-controls="panel-about">Assumptions</button>
      </nav>
    </div>
  </header>
  <main class="wrap">
    <!-- TRACKER -->
    <section id="panel-tracker" role="region" aria-labelledby="tracker" class="tab-panel">
      <div class="grid grid-2">
        <div class="card">
          <h2>1) Energy</h2>
          <div class="row">
            <div>
              <label for="kwh">Electricity (kWh)</label>
              <input id="kwh" type="number" inputmode="decimal" min="0" placeholder="e.g., 12" />
            </div>
            <div>
              <label for="therms">Natural Gas (therms)</label>
              <input id="therms" type="number" inputmode="decimal" min="0" placeholder="e.g., 0.8" />
            </div>
          </div>
          <div class="row">
            <div>
              <label for="heatingOil">Heating Oil (gallons)</label>
              <input id="heatingOil" type="number" inputmode="decimal" min="0" placeholder="optional" />
            </div>
            <div>
              <label for="gridFactor">Grid Factor
                <span class="pill">kg CO₂e / kWh</span>
              </label>
              <select id="gridFactor">
                <!-- TODO: customize for your region -->
                <option value="0.42">US average ~0.42</option>
                <option value="0.25">Cleaner grid 0.25</option>
                <option value="0.65">Coal-heavy grid 0.65</option>
              </select>
            </div>
          </div>
        </div>
        <div class="card">
          <h2> Transport</h2>
          <div class="row">
            <div>
              <label for="carMiles">Car Miles</label>
              <input id="carMiles" type="number" min="0" placeholder="e.g., 18" />
            </div>
            <div>
              <label for="carMPG">Vehicle Type</label>
              <select id="carMPG">
                <!-- TODO: adjust/add your common vehicles -->
                <option value="28">Gas — 28 MPG (compact)</option>
                <option value="22">Gas — 22 MPG (sedan/SUV)</option>
                <option value="18">Gas — 18 MPG (truck)</option>
                <option value="0">EV — enter kWh/100mi below</option>
              </select>
            </div>
          </div>
          <div class="row">
            <div>
              <label for="evKwhPer100">EV usage (kWh/100 mi)</label>
              <input id="evKwhPer100" type="number" min="0" placeholder="e.g., 28 (leave 0 if gas)" />
            </div>
            <div>
              <label for="busMiles">Bus / Rail Miles</label>
              <input id="busMiles" type="number" min="0" placeholder="e.g., 6" />
            </div>
          </div>
          <div class="row">
            <div>
              <label for="flightMiles">Flight Miles</label>
              <input id="flightMiles" type="number" min="0" placeholder="e.g., 450" />
            </div>
            <div>
              <label for="rfi">Flight RFI (non-CO₂ effects)</label>
              <select id="rfi">
                <option value="1.0">Off (1.0)</option>
                <option value="1.7" selected>On (1.7)</option>
              </select>
            </div>
          </div>
        </div>
        <div class="card">
          <h2> Food</h2>
          <div class="row">
            <div>
              <label for="diet">Diet (per day)</label>
              <select id="diet">
                <!-- TODO: tune numbers based on source you prefer -->
                <option value="5.0">Omnivore — 5.0 kg CO₂e</option>
                <option value="4.0">Low-meat — 4.0 kg</option>
                <option value="3.0">Vegetarian — 3.0 kg</option>
                <option value="2.5">Vegan — 2.5 kg</option>
              </select>
            </div>
            <div>
              <label for="mealAdjust">Extra food choices</label>
              <select id="mealAdjust">
                <option value="0">None</option>
                <option value="0.5">+ Beef/Dairy heavy day (+0.5 kg)</option>
                <option value="-0.4">– Plant-forward day (−0.4 kg)</option>
              </select>
            </div>
          </div>
          <label for="date">Date</label>
          <input id="date" type="date" />
        </div>
        <div class="card" id="results">
          <h2>Today’s Estimate</h2>
          <div class="flex">
            <div>
              <div class="total" id="totalKg">0.00 kg CO₂e</div>
              <div class="muted" id="breakdown">—</div>
            </div>
            <button class="btn primary right" id="calcBtn" aria-label="Calculate footprint">
              Calculate
            </button>
          </div>
          <div class="footer muted">Estimates only. See <em>Assumptions</em> tab for factors and notes.</div>
          <hr style="border:0;border-top:1px dashed var(--border);margin:16px 0">
          <div class="flex">
            <button class="btn subtle" id="saveBtn">Save Day</button>
            <button class="btn danger" id="clearHistoryBtn">Clear History</button>
          </div>
          <div style="margin-top:12px;overflow:auto">
            <table id="historyTable" aria-label="Saved entries">
              <thead>
                <tr><th>Date</th><th>Energy</th><th>Transport</th><th>Food</th><th>Total (kg)</th></tr>
              </thead>
              <tbody></tbody>
            </table>
          </div>
        </div>
      </div>
    </section>
    <!-- TIPS & CHALLENGES -->
    <section id="panel-tips" class="tab-panel" hidden>
      <div class="grid">
        <div class="card">
          <h2>Quick Tips</h2>
          <details open>
            <summary>Energy at Home</summary>
            <div>
              <ul>
                <li>Switch to LED bulbs and enable “sleep” on your devices.</li>
                <li>Wash clothes in cold water; air-dry when possible.</li>
                <li>Set thermostat wisely (winter 68°F/20°C, summer 78°F/26°C).</li>
              </ul>
            </div>
          </details>
          <details>
            <summary>Food & Diet</summary>
            <div>
              <ul>
                <li>Choose plant-forward meals a few times per week.</li>
                <li>Reduce food waste: plan meals & store leftovers.</li>
                <li>Buy seasonal/locally grown when you can.</li>
              </ul>
            </div>
          </details>
          <details>
            <summary>Transport</summary>
            <div>
              <ul>
                <li>Batch errands; keep tires properly inflated.</li>
                <li>Use transit, carpool, or bike for short trips.</li>
                <li>For flights, pack light and avoid very short hops.</li>
              </ul>
            </div>
          </details>
        </div>
        <div class="card">
          <h2>Weekly Challenge</h2>
          <p class="muted">Click to get a random challenge. Complete it to earn bonus points in Rewards.</p>
          <div id="challengeBox" class="notice" style="margin:10px 0;">Press “New Challenge” to start.</div>
          <div class="flex">
            <button class="btn primary" id="newChallengeBtn">New Challenge</button>
            <button class="btn subtle" id="addChallengeToRewardsBtn">Add to Rewards</button>
          </div>
          <div class="footer muted">Challenges are stored in your browser until you clear them.</div>
        </div>
      </div>
    </section>
    <!-- REWARDS -->
    <section id="panel-rewards" class="tab-panel" hidden>
      <div class="grid grid-2">
        <div class="card">
          <h2>Earn Rewards</h2>
          <label for="action">Choose an eco-action</label>
          <select id="action">
            <!-- TODO: edit actions & points -->
            <option value='{"name":"Recycled items","pts":10,"unit":"times"}'>Recycled items (+10)</option>
            <option value='{"name":"Biked/walked instead of driving","pts":5,"unit":"miles"}'>Biked/walked instead of driving (+5/mi)</option>
            <option value='{"name":"Took public transit","pts":15,"unit":"trips"}'>Took public transit (+15/trip)</option>
            <option value='{"name":"Cold-wash laundry","pts":10,"unit":"loads"}'>Cold-wash laundry (+10/load)</option>
            <option value='{"name":"Unplugged/turned off devices","pts":5,"unit":"sessions"}'>Unplugged devices (+5)</option>
          </select>
          <div class="row">
            <div>
              <label for="quantity">Quantity</label>
              <input id="quantity" type="number" min="1" value="1" />
            </div>
            <div>
              <label>&nbsp;</label>
              <button class="btn primary" id="addRewardBtn">Add Action</button>
            </div>
          </div>
          <div class="flex" style="margin-top:10px">
            <div class="badge">Total Points: <strong id="totalPoints">0</strong></div>
            <div class="badge">Level: <strong id="levelName">Seedling</strong></div>
            <button class="btn danger right" id="clearRewardsBtn">Reset</button>
          </div>
        </div>
        <div class="card">
          <h2>History</h2>
          <table id="rewardsTable" aria-label="Rewards history">
            <thead><tr><th>Date</th><th>Action</th><th>Qty</th><th>Points</th></tr></thead>
            <tbody></tbody>
          </table>
          <p class="footer muted">Badges unlock at 100 (🌱), 300 (🌿), 600 (🌳) points.</p>
        </div>
      </div>
    </section>
    <!-- ASSUMPTIONS -->
    <section id="panel-about" class="tab-panel" hidden>
      <div class="card">
        <h2>Assumptions & Factors</h2>
        <ul class="muted">
          <li><strong>Electricity:</strong> default factor 0.42 kg CO₂e/kWh (US avg). Change via dropdown.</li>
          <li><strong>Natural Gas:</strong> 5.30 kg CO₂e per therm.</li>
          <li><strong>Heating Oil:</strong> 10.16 kg CO₂e per gallon.</li>
          <li><strong>Gas Cars:</strong> gallons = miles / MPG; <em>8.887 kg CO₂e per gallon</em>.</li>
          <li><strong>EVs:</strong> kWh = miles × (kWh/100mi) / 100; emissions use your electricity factor.</li>
          <li><strong>Bus/Rail:</strong> 0.12 kg CO₂e per passenger-mile (blended estimate).</li>
          <li><strong>Flights:</strong> 0.15 kg CO₂e per mile × Radiative Forcing Index (RFI, default 1.7).</li>
          <li><strong>Food:</strong> daily diet factor dropdown (omnivore→vegan). Adjust using the extra menu.</li>
        </ul>
        <p class="notice">These are ballpark values for learning purposes. For precise inventories, plug in location-specific grid factors and verified LCA numbers. <!-- TODO: replace with your preferred sources. --></p>
      </div>
    </section>
  </main>
  <script>
    // ===== Utilities =====
    const $ = sel => document.querySelector(sel);
    const $$ = sel => [...document.querySelectorAll(sel)];
    const fmt = n => Number(n).toLocaleString(undefined,{maximumFractionDigits:2});
    // ===== Tabs =====
    $$(".tab-btn").forEach(btn=>{
      btn.addEventListener("click", ()=>{
        $$(".tab-btn").forEach(b=>b.classList.remove("active"));
        btn.classList.add("active");
        $$(".tab-panel").forEach(p=>p.hidden = true);
        document.querySelector(`#panel-${btn.dataset.tab}`).hidden = false;
      });
    });
    // ===== Calculation Factors (edit if needed) =====
    const FACTORS = {
      gasPerGallon: 8.887,     // kg CO2e / gallon gasoline
      ngPerTherm: 5.30,        // kg / therm
      oilPerGallon: 10.16,     // kg / gallon
      busRailPerMile: 0.12,    // kg / passenger-mile (blended)
      flightPerMile: 0.15      // kg / mile before RFI
    };
    // ===== Tracker: compute footprint =====
    function compute(){
      const kwh = +$("#kwh").value || 0;
      const therms = +$("#therms").value || 0;
      const oil = +$("#heatingOil").value || 0;
      const grid = +$("#gridFactor").value || 0.42;
      const carMiles = +$("#carMiles").value || 0;
      const mpg = +$("#carMPG").value || 0;
      const evK100 = +$("#evKwhPer100").value || 0;
      const busMiles = +$("#busMiles").value || 0;
      const flightMiles = +$("#flightMiles").value || 0;
      const rfi = +$("#rfi").value || 1.0;
      const diet = +$("#diet").value || 0;
      const adjust = +$("#mealAdjust").value || 0;
      // Energy
      const elec = kwh * grid;
      const gas = therms * FACTORS.ngPerTherm;
      const oilKg = oil * FACTORS.oilPerGallon;
      const energyKg = elec + gas + oilKg;
      // Transport
      // If mpg==0 treat as EV miles; otherwise gasoline car.
      const carKg = mpg>0 ? (carMiles/mpg) * FACTORS.gasPerGallon
                          : (carMiles * (evK100/100)) * grid;
      const busRailKg = busMiles * FACTORS.busRailPerMile;
      const flightKg = flightMiles * FACTORS.flightPerMile * rfi;
      const transportKg = carKg + busRailKg + flightKg;
      // Food
      const foodKg = diet + adjust;
      const total = energyKg + transportKg + foodKg;
      $("#totalKg").textContent = `${fmt(total)} kg CO₂e`;
      $("#breakdown").textContent =
        `Energy ${fmt(energyKg)} • Transport ${fmt(transportKg)} • Food ${fmt(foodKg)}`;
      return {energyKg, transportKg, foodKg, total};
    }
    $("#calcBtn").addEventListener("click", compute);
    // ===== History (localStorage) =====
    const KEY_HISTORY = "climate_history_v1";
    function loadHistory(){
      const data = JSON.parse(localStorage.getItem(KEY_HISTORY) || "[]");
      const tbody = $("#historyTable tbody");
      tbody.innerHTML = "";
      data.forEach(row=>{
        const tr = document.createElement("tr");
        tr.innerHTML = `<td>${row.date}</td>
                        <td>${fmt(row.energyKg)}</td>
                        <td>${fmt(row.transportKg)}</td>
                        <td>${fmt(row.foodKg)}</td>
                        <td><strong>${fmt(row.total)}</strong></td>`;
        tbody.appendChild(tr);
      });
    }
    $("#saveBtn").addEventListener("click", ()=>{
      const {energyKg, transportKg, foodKg, total} = compute();
      const date = $("#date").value || new Date().toISOString().slice(0,10);
      const entry = {date, energyKg, transportKg, foodKg, total};
      const data = JSON.parse(localStorage.getItem(KEY_HISTORY) || "[]");
      data.push(entry);
      localStorage.setItem(KEY_HISTORY, JSON.stringify(data));
      loadHistory();
    });
    $("#clearHistoryBtn").addEventListener("click", ()=>{
      if(confirm("Clear all saved tracker entries?")){
        localStorage.removeItem(KEY_HISTORY);
        loadHistory();
      }
    });
    // ===== Challenges =====
    const CHALLENGES = [
      "Go car-free for 2 days this week.",
      "Swap 3 meals to plant-based.",
      "Line-dry laundry twice this week.",
      "Cut phantom load: unplug chargers nightly.",
      "Batch errands into one round-trip.",
      "Lower thermostat 2°F (or raise 2°F in summer).",
      "No food waste: clean-out-the-fridge meal."
    ];
    function newChallenge(){
      const pick = CHALLENGES[Math.floor(Math.random()*CHALLENGES.length)];
      $("#challengeBox").textContent = pick;
      localStorage.setItem("current_challenge", pick);
    }
    $("#newChallengeBtn").addEventListener("click", newChallenge);
    $("#addChallengeToRewardsBtn").addEventListener("click", ()=>{
      const txt = localStorage.getItem("current_challenge");
      if(!txt){ alert("Generate a challenge first."); return; }
      addReward({name:`Challenge: ${txt}`, pts:50, unit:"", qty:1}); // bonus points
    });
    (function initChallenge(){
      const saved = localStorage.getItem("current_challenge");
      if(saved) $("#challengeBox").textContent = saved;
    })();
    // ===== Rewards =====
    const KEY_REWARDS = "climate_rewards_v1";
    const KEY_POINTS  = "climate_points_v1";
    function getPoints(){ return +(localStorage.getItem(KEY_POINTS)||0); }
    function setPoints(v){ localStorage.setItem(KEY_POINTS, v); updateBadges(); }
    function levelName(points){
      if(points>=600) return "Forest (🌳)";
      if(points>=300) return "Grove (🌿)";
      if(points>=100) return "Seedling+ (🌱)";
      return "Seedling";
    }
    function updateBadges(){
      $("#totalPoints").textContent = fmt(getPoints());
      $("#levelName").textContent = levelName(getPoints());
    }
    function loadRewards(){
      const data = JSON.parse(localStorage.getItem(KEY_REWARDS) || "[]");
      const tbody = $("#rewardsTable tbody");
      tbody.innerHTML = "";
      data.forEach(r=>{
        const tr = document.createElement("tr");
        tr.innerHTML = `<td>${r.date}</td><td>${r.name}</td><td>${r.qty}</td><td>${r.points}</td>`;
        tbody.appendChild(tr);
      });
      updateBadges();
    }
    function addReward({name, pts, unit, qty}){
      const points = Math.max(1, Math.round(pts * (qty||1)));
      const row = {date: new Date().toLocaleDateString(), name, qty, points};
      const data = JSON.parse(localStorage.getItem(KEY_REWARDS) || "[]");
      data.unshift(row);
      localStorage.setItem(KEY_REWARDS, JSON.stringify(data));
      setPoints(getPoints()+points);
      loadRewards();
    }
    $("#addRewardBtn").addEventListener("click", ()=>{
      const obj = JSON.parse($("#action").value);
      const qty = Math.max(1, +$("#quantity").value||1);
      addReward({name: obj.name, pts: obj.pts, unit: obj.unit, qty});
    });
    $("#clearRewardsBtn").addEventListener("click", ()=>{
      if(confirm("Reset all reward points and history?")){
        localStorage.removeItem(KEY_REWARDS);
        localStorage.removeItem(KEY_POINTS);
        loadRewards();
      }
    });
    // ===== Init =====
    (function init(){
      // default date = today
      $("#date").value = new Date().toISOString().slice(0,10);
      loadHistory();
      loadRewards();
    })();
  </script>
</body>
</html>

