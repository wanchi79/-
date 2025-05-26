<!-- index.html 內容與 Scoring Sheet Index 相同 -->
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <title>線上評分表</title>
  <style>
    table, th, td {
      border: 1px solid black;
      border-collapse: collapse;
    }
    th, td {
      padding: 5px;
      text-align: center;
    }
    input[type='number'] {
      width: 60px;
    }
  </style>
</head>
<body>
  <h1>線上評分表</h1>
  <p>評分標準：造形30%、創意20%、服裝15%、客家元素20%、團隊精神15%</p>
  <table id="scoreTable">
    <thead>
      <tr>
        <th>隊伍編號</th>
        <th>造形<br>(30%)</th>
        <th>創意<br>(20%)</th>
        <th>服裝<br>(15%)</th>
        <th>客家元素<br>(20%)</th>
        <th>團隊精神<br>(15%)</th>
        <th>總分</th>
      </tr>
    </thead>
    <tbody>
      <!-- 動態生成 140 隊伍資料 -->
    </tbody>
  </table>

  <script>
    const tbody = document.querySelector("#scoreTable tbody");

    for (let i = 1; i <= 140; i++) {
      const row = document.createElement("tr");

      const teamCell = document.createElement("td");
      teamCell.textContent = `隊伍 ${i}`;
      row.appendChild(teamCell);

      const weights = [0.3, 0.2, 0.15, 0.2, 0.15];

      for (let j = 0; j < 5; j++) {
        const cell = document.createElement("td");
        const input = document.createElement("input");
        input.type = "number";
        input.min = 0;
        input.max = 100;
        input.dataset.weight = weights[j];
        input.addEventListener("input", updateTotal);
        cell.appendChild(input);
        row.appendChild(cell);
      }

      const totalCell = document.createElement("td");
      totalCell.className = "total";
      totalCell.textContent = "0";
      row.appendChild(totalCell);

      tbody.appendChild(row);
    }

    function updateTotal(event) {
      const row = event.target.closest("tr");
      const inputs = row.querySelectorAll("input");
      let sum = 0;
      inputs.forEach(input => {
        const val = parseFloat(input.value);
        const weight = parseFloat(input.dataset.weight);
        if (!isNaN(val)) sum += val * weight;
      });
      row.querySelector(".total").textContent = sum.toFixed(2);
    }
  </script>
</body>
</html>
# -
