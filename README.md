<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Search PN System</title>
  <style>
    body {
      font-family: Arial;
      padding: 20px;
      background: #f4f4f4;
    }
    input {
      width: 100%;
      padding: 10px;
      font-size: 16px;
      margin-bottom: 20px;
    }
    table {
      border-collapse: collapse;
      width: 100%;
      background: white;
    }
    th, td {
      border: 1px solid #ddd;
      padding: 8px;
      font-size: 14px;
    }
    th {
      background: #333;
      color: white;
    }
  </style>
</head>
<body>

<h2>🔍 Pencarian PN / Material</h2>

<input type="text" id="search" placeholder="Cari PN / Nama / Kode...">

<table id="table">
  <thead id="thead"></thead>
  <tbody id="tbody"></tbody>
</table>

<script>
let data = [];

fetch('data.json')
  .then(res => res.json())
  .then(json => {
    data = json;
    renderTable(data);
  });

document.getElementById("search").addEventListener("keyup", function() {
  const keyword = this.value.toLowerCase();
  
  const filtered = data.filter(row => 
    Object.values(row).some(val => 
      String(val).toLowerCase().includes(keyword)
    )
  );

  renderTable(filtered);
});

function renderTable(rows) {
  const thead = document.getElementById("thead");
  const tbody = document.getElementById("tbody");

  thead.innerHTML = "";
  tbody.innerHTML = "";

  if (rows.length === 0) return;

  // Header
  const headers = Object.keys(rows[0]);
  let headRow = "<tr>";
  headers.forEach(h => headRow += `<th>${h}</th>`);
  headRow += "</tr>";
  thead.innerHTML = headRow;

  // Body
  rows.forEach(row => {
    let tr = "<tr>";
    headers.forEach(h => {
      tr += `<td>${row[h] ?? ""}</td>`;
    });
    tr += "</tr>";
    tbody.innerHTML += tr;
  });
}
</script>

</body>
</html>
