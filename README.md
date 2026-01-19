Regjister-Veprimtarish
│
├── index.html        (Login)
├── teacher.html      (Mësues)
├── coordinator.html  (Koordinator)
├── director.html     (Drejtoria)
├── style.css
└── script.js
<!DOCTYPE html>
<html lang="sq">
<head>
  <meta charset="UTF-8">
  <title>Login</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

<h2>Hyrje në Sistem</h2>

<form onsubmit="login(event)">
  <input type="text" id="username" placeholder="Username" required>
  <input type="password" id="password" placeholder="Password" required>

  <select id="role">
    <option value="teacher">Mësues</option>
    <option value="coordinator">Koordinator</option>
    <option value="director">Drejtori</option>
  </select>

  <button type="submit">Hyr</button>
</form>

<script src="script.js"></script>
</body>
</html>
<!DOCTYPE html>
<html>
<head>
  <title>Mësues</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

<h2>Paneli i Mësuesit</h2>

<form onsubmit="addActivity(event)">
  <input type="text" id="activity" placeholder="Emri i veprimtarisë" required>
  <input type="date" id="date" required>
  <input type="number" id="hours" placeholder="Orë" required>
  <input type="number" id="absences" placeholder="Mungesa nxënësish">
  <input type="file" id="photo">
  <button type="submit">Ruaj</button>
</form>

<div id="list"></div>

<script src="script.js"></script>
</body>
</html>
<!DOCTYPE html>
<html>
<head>
  <title>Koordinator</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

<h2>Raport Javor</h2>
<button onclick="showReport()">Shfaq Raportin</button>

<div id="report"></div>

<script src="script.js"></script>
</body>
</html>
<!DOCTYPE html>
<html>
<head>
  <title>Drejtoria</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

<h2>Veprimtaritë Jashtëmësimore</h2>
<div id="directorView"></div>

<script src="script.js"></script>
</body>
</html>
<!DOCTYPE html>
<html>
<head>
  <title>Drejtoria</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>

<h2>Veprimtaritë Jashtëmësimore</h2>
<div id="directorView"></div>

<script src="script.js"></script>
</body>
</html>
body {
  font-family: Arial;
  background: #f2f2f2;
  padding: 20px;
}

input, select, button {
  display: block;
  margin: 10px 0;
  padding: 8px;
}

button {
  background: #2c7be5;
  color: white;
  border: none;
  cursor: pointer;
}
function login(e) {
  e.preventDefault();
  let role = document.getElementById("role").value;

  if (role === "teacher") location.href = "teacher.html";
  if (role === "coordinator") location.href = "coordinator.html";
  if (role === "director") location.href = "director.html";
}

function addActivity(e) {
  e.preventDefault();

  let data = {
    activity: activity.value,
    date: date.value,
    hours: hours.value,
    absences: absences.value
  };

  let activities = JSON.parse(localStorage.getItem("activities")) || [];
  activities.push(data);
  localStorage.setItem("activities", JSON.stringify(activities));

  alert("U ruajt me sukses!");
}

function showReport() {
  let activities = JSON.parse(localStorage.getItem("activities")) || [];
  let output = "";

  activities.forEach(a => {
    output += `<p>${a.activity} | ${a.date} | Orë: ${a.hours} | Mungesa: ${a.absences}</p>`;
  });

  document.getElementById("report").innerHTML = output;
}

window.onload = function () {
  let activities = JSON.parse(localStorage.getItem("activities")) || [];
  let output = "";

  activities.forEach(a => {
    output += `<p>${a.activity} - ${a.date} - ${a.hours} orë</p>`;
  });

  if (document.getElementById("directorView"))
    directorView.innerHTML = output;
};
