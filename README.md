# sctomatnum.github.io
<!DOCTYPE html>
<html>
<head>
  <title>PN Search System</title>
  <style>
    body { font-family: Arial; padding: 20px; }
    input { padding: 10px; width: 300px; }
    table { border-collapse: collapse; margin-top: 20px; }
    th, td { border: 1px solid #ccc; padding: 8px; }
  </style>
</head>
<body>

<h2>PN Search System</h2>

<input type="text" id="search" placeholder="Cari PN atau Nama..." onkeyup="searchData()">

<table>
  <thead>
    <tr>
      <th>PN</th>
      <th>Nama</th>
      <th>Model</th>
      <th>Deskripsi</th>
      <th>Lokasi</th>
      <th>Stock</th>
    </tr>
  </thead>
  <tbody id="tableData"></tbody>
</table>

<script>
const data = [
  ["12345","Filter Oli","PC2000-8","Filter engine","A1",5],
  ["67890","Pump Hydraulic","EX2600-7","Main pump","B2",2],
  ["11223","Air Filter","PC2000-8","Filter udara","A2",10],
  ["44556","Fuel Pump","EX2600-7","Pompa bahan bakar","C1",3]
];

function displayData(filtered){
  let html = "";
  filtered.forEach(row => {
    html += "<tr>" + row.map(d => `<td>${d}</td>`).join("") + "</tr>";
  });
  document.getElementById("tableData").innerHTML = html;
}

function searchData(){
  let keyword = document.getElementById("search").value.toLowerCase();
  let filtered = data.filter(row =>
    row[0].toLowerCase().includes(keyword) ||
    row[1].toLowerCase().includes(keyword)
  );
  displayData(filtered);
}

displayData(data);
</script>

</body>
</html>
