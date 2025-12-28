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
