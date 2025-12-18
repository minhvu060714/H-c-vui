<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>Học Toán Lớp 3</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f2f8ff;
      text-align: center;
      padding: 20px;
    }
    .box {
      background: white;
      padding: 20px;
      border-radius: 15px;
      max-width: 350px;
      margin: auto;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }
    button {
      font-size: 18px;
      padding: 10px 20px;
      margin-top: 10px;
      border: none;
      border-radius: 10px;
      background: #4CAF50;
      color: white;
    }
    input {
      font-size: 18px;
      width: 80px;
      text-align: center;
    }
  </style>
</head>
<body>

  <div class="box">
    <h2>📘 Học Toán Lớp 3</h2>
    <p id="question">Bấm Bắt đầu</p>

    <input type="number" id="answer">
    <br><br>
    <button onclick="check()">Trả lời</button>
    <button onclick="newQuestion()">Bắt đầu</button>

    <p id="result"></p>
    <p>⭐ Điểm: <span id="score">0</span></p>
  </div>

<script>
let a, b, score = 0;

function newQuestion() {
  a = Math.floor(Math.random() * 10);
  b = Math.floor(Math.random() * 10);
  document.getElementById("question").innerText =
    `❓ ${a} + ${b} = ?`;
  document.getElementById("result").innerText = "";
  document.getElementById("answer").value = "";
}

function check() {
  let ans = parseInt(document.getElementById("answer").value);
  if (ans === a + b) {
    document.getElementById("result").innerText = "🎉 Đúng rồi!";
    score++;
  } else {
    document.getElementById("result").innerText = "❌ Sai rồi!";
  }
  document.getElementById("score").innerText = score;
}
</script>

</body>
</html>
