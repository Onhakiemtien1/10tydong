<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>10 Tỷ Đồng Live</title>
  <style>
    body {
      background-color: black;
      color: lime;
      font-family: 'Courier New', monospace;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      font-size: 3rem;
    }
    #money {
      transition: all 0.2s ease-in-out;
    }
  </style>
</head>
<body>
  <div id="money">Đang tải...</div>

  <script>
    const moneyDiv = document.getElementById("money");
    let currentMoney = 0;

    async function fetchMoney() {
      try {
        const res = await fetch("https://docs.google.com/spreadsheets/d/13SFbXX4SSiLSx6pIqeZ_UgcSKivxMEg5fmCzdRqdd_g/gviz/tq?tqx=out:json&tq=select B limit 1");
        const text = await res.text();
        const json = JSON.parse(text.substring(47).slice(0, -2));
        const value = json.table.rows[0].c[0].v;

        // Làm sạch và hiển thị
        currentMoney = parseFloat(value.toString().replace(/,/g, ''));
        moneyDiv.textContent = "₫" + currentMoney.toLocaleString("vi-VN");
      } catch (error) {
        moneyDiv.textContent = "Lỗi tải dữ liệu";
        console.error("Lỗi khi lấy dữ liệu:", error);
      }
    }

    // Gọi lần đầu và cập nhật mỗi 3 giây
    fetchMoney();
    setInterval(fetchMoney, 3000);
  </script>
</body>
