<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Ma semaine en douceur</title>

  <link rel="manifest" href="manifest.json">
  <meta name="theme-color" content="#2D6A4F">

  <style>
    body {
      font-family: -apple-system, BlinkMacSystemFont;
      background: #F7FBF9;
      margin: 0;
      padding: 16px;
      color: #2D6A4F;
    }
    h1 {
      text-align: center;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 16px;
    }
    th, td {
      border: 1px solid #CAD2C5;
      padding: 8px;
      text-align: center;
    }
    th {
      background: #E9F5EF;
    }
    td:first-child {
      text-align: left;
      font-weight: 600;
    }
    select, input {
      transform: scale(1.2);
    }
  </style>
</head>
<body>

<h1>🌿 Ma semaine en douceur</h1>

<table>
  <tr>
    <th>Habitudes</th>
    <th>L</th><th>M</th><th>M</th><th>J</th><th>V</th><th>S</th><th>D</th>
  </tr>

  <tr><td>Étirements</td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td></tr>
  <tr><td>Seance sport</td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td></tr>
  <tr><td>7h de sommeil</td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td></tr>
  <tr><td>Manger sain</td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td></tr>
<tr><td>Boire 1L d'eau</td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td></tr>
<tr><td>Pas de Fast food</td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td></tr>
<tr><td>Sans Alcool</td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td></tr>
<tr><td>Avancer bricolage</td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td></tr>
<tr><td>30 à 45 min de lecture</td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td></tr>
<tr><td>Pas de film</td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td></tr>
<tr><td>10K pas/Jours</td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td></tr>
<tr><td>Profiter d'un moment avec sa/son chéri/e</td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td><td><input type="checkbox"></td></tr>

  <tr>
    <td>🙂 État général</td>
    <td><select><option></option><option>😕</option><option>😐</option><option>🙂</option></select></td>
    <td><select><option></option><option>😕</option><option>😐</option><option>🙂</option></select></td>
    <td><select><option></option><option>😕</option><option>😐</option><option>🙂</option></select></td>
    <td><select><option></option><option>😕</option><option>😐</option><option>🙂</option></select></td>
    <td><select><option></option><option>😕</option><option>😐</option><option>🙂</option></select></td>
    <td><select><option></option><option>😕</option><option>😐</option><option>🙂</option></select></td>
    <td><select><option></option><option>😕</option><option>😐</option><option>🙂</option></select></td>
  </tr>
</table>

</body>
</html>

<script>
const habitsCount = 11;
const days = ["Lundi","Mardi","Mercredi","Jeudi","Vendredi","Samedi","Dimanche"];

function saveData() {
  const data = {
    checks: {},
    moods: {},
    date: new Date().toISOString()
  };

  document.querySelectorAll("input[type=checkbox]").forEach((c, i) => {
    data.checks[i] = c.checked;
  });

  document.querySelectorAll("select").forEach((s, i) => {
    data.moods[i] = s.value;
  });

  localStorage.setItem("currentWeek", JSON.stringify(data));
}

function loadData() {
  const data = JSON.parse(localStorage.getItem("currentWeek"));
  if (!data) return;

  document.querySelectorAll("input[type=checkbox]").forEach((c, i) => {
    c.checked = data.checks[i] || false;
  });

  document.querySelectorAll("select").forEach((s, i) => {
    s.value = data.moods[i] || "";
  });
}

function calculateDailySummary() {
  const summary = {};

  days.forEach((day, d) => {
    let count = 0;
    for (let h = 0; h < habitsCount; h++) {
      const index = h * 7 + d;
      if (document.querySelectorAll("input")[index]?.checked) count++;
    }
    summary[day] = Math.round((count / habitsCount) * 100);
  });

  return summary;
}

function calculateWeeklySummary() {
  const total = document.querySelectorAll("input[type=checkbox]").length;
  const done = [...document.querySelectorAll("input[type=checkbox]")].filter(c => c.checked).length;
  return Math.round((done / total) * 100);
}

function archiveWeek() {
  const history = JSON.parse(localStorage.getItem("history")) || [];
  history.push({
    date: new Date().toLocaleDateString(),
    daily: calculateDailySummary(),
    weekly: calculateWeeklySummary()
  });
  localStorage.setItem("history", JSON.stringify(history));
  localStorage.removeItem("currentWeek");
  alert("Bilan hebdomadaire enregistré ✅");
}

document.addEventListener("change", saveData);
window.onload = loadData;
</script>

<button onclick="archiveWeek()" style="
  margin-top:16px;
  padding:12px;
  width:100%;
  background:#2D6A4F;
  color:white;
  border:none;
  border-radius:8px;
  font-size:16px;">
📊 Enregistrer le bilan de la semaine
</button>

<div id="bilan" style="display:none; margin-top:24px;">
  <h2>📊 Bilan & historique</h2>

  <div id="bilan-semaine" style="margin-bottom:16px;"></div>

  <h3>📅 Historique des semaines</h3>
  <div id="historique"></div>

  <button onclick="showTracker()" style="
    margin-top:16px;
    padding:12px;
    width:100%;
    background:#52796F;
    color:white;
    border:none;
    border-radius:8px;
    font-size:16px;">
⬅️ Retour à la semaine
  </button>
</div>

<button onclick="showBilan()" style="
  margin-top:12px;
  padding:12px;
  width:100%;
  background:#84A98C;
  color:white;
  border:none;
  border-radius:8px;
  font-size:16px;">
📈 Voir le bilan & l’historique
</button>

<script>
function showBilan() {
  document.querySelector("table").style.display = "none";
  document.querySelector("button").style.display = "none";
  document.getElementById("bilan").style.display = "block";
  renderBilan();
}

function showTracker() {
  document.querySelector("table").style.display = "table";
  document.getElementById("bilan").style.display = "none";
}

function renderBilan() {
  const history = JSON.parse(localStorage.getItem("history")) || [];
  const current = calculateWeeklySummary();

  document.getElementById("bilan-semaine").innerHTML = `
    <strong>Cette semaine :</strong><br>
    ✅ Réussite : <b>${current}%</b>
  `;

  if (history.length === 0) {
    document.getElementById("historique").innerHTML =
      "<p>Aucun historique pour le moment.</p>";
    return;
  }

  let html = "<ul>";
  history.forEach((w, i) => {
    html += `<li>📅 ${w.date} — ${w.weekly}%</li>`;
  });
  html += "</ul>";

  document.getElementById("historique").innerHTML = html;
}
</script>

<script>
function calculateDailyDetails() {
  const days = ["Lundi","Mardi","Mercredi","Jeudi","Vendredi","Samedi","Dimanche"];
  const habitsCount = 11;
  const checkboxes = document.querySelectorAll("input[type=checkbox]");
  const details = [];

  days.forEach((day, d) => {
    let count = 0;
    for (let h = 0; h < habitsCount; h++) {
      const index = h * 7 + d;
      if (checkboxes[index]?.checked) count++;
    }
    const percent = Math.round((count / habitsCount) * 100);
    details.push({ day, count, percent });
  });

  return details;
}
</script>

<script>
function renderBilan() {
  const history = JSON.parse(localStorage.getItem("history")) || [];
  const weeklyPercent = calculateWeeklySummary();
  const daily = calculateDailyDetails();

  let dailyHtml = "<ul>";
  daily.forEach(d => {
    dailyHtml += `<li>${d.day} : ${d.count} / 11 → ${d.percent}%</li>`;
  });
  dailyHtml += "</ul>";

  document.getElementById("bilan-semaine").innerHTML = `
    <strong>📊 Cette semaine</strong><br>
    Réussite globale : <b>${weeklyPercent}%</b><br><br>
    <strong>Détail jour par jour :</strong>
    ${dailyHtml}
  `;

  if (history.length === 0) {
    document.getElementById("historique").innerHTML =
      "<p>Aucun historique pour le moment.</p>";
    return;
  }

  let html = "<ul>";
  history.forEach(w => {
    html += `<li>📅 ${w.date} — ${w.weekly}%</li>`;
  });
  html += "</ul>";

  document.getElementById("historique").innerHTML = html;
}
</script>

<script>
function getWeekNumber(date) {
  const d = new Date(Date.UTC(date.getFullYear(), date.getMonth(), date.getDate()));
  const dayNum = d.getUTCDay() || 7;
  d.setUTCDate(d.getUTCDate() + 4 - dayNum);
  const yearStart = new Date(Date.UTC(d.getUTCFullYear(),0,1));
  return Math.ceil((((d - yearStart) / 86400000) + 1) / 7);
}

function checkWeeklyReset() {
  const now = new Date();
  const currentWeek = getWeekNumber(now);
  const savedWeek = localStorage.getItem("weekNumber");

  if (savedWeek && savedWeek != currentWeek) {
    archiveWeek();
    localStorage.removeItem("currentWeek");
  }

  localStorage.setItem("weekNumber", currentWeek);
}

window.onload = () => {
  checkWeeklyReset();
  loadData();
};
</script>

<canvas id="chart" width="300" height="160" style="margin:16px 0;"></canvas>

<script>
function drawChart(daily) {
  const canvas = document.getElementById("chart");
  if (!canvas) return;
  const ctx = canvas.getContext("2d");

  ctx.clearRect(0, 0, canvas.width, canvas.height);

  const barWidth = 30;
  const gap = 10;
  const maxHeight = 100;

  daily.forEach((d, i) => {
    const height = (d.percent / 100) * maxHeight;
    ctx.fillStyle = "#84A98C";
    ctx.fillRect(
      i * (barWidth + gap),
      maxHeight - height + 20,
      barWidth,
      height
    );

    ctx.fillStyle = "#2D6A4F";
    ctx.font = "12px sans-serif";
    ctx.fillText(d.day[0], i * (barWidth + gap) + 10, 140);
  });
}
</script>

drawChart(daily);

<button onclick="exportPDF()" style="
  margin-top:12px;
  padding:12px;
  width:100%;
  background:#2D6A4F;
  color:white;
  border:none;
  border-radius:8px;
  font-size:16px;">
📄 Exporter le bilan en PDF
</button>

<script>
function exportPDF() {
  const tracker = document.querySelector("table");
  const bilan = document.getElementById("bilan");

  tracker.style.display = "none";
  bilan.style.display = "block";

  window.print();

  tracker.style.display = "table";
}
</script>
