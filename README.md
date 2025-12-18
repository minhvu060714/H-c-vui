<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<title>Toán Lớp 3 Pro</title>
<style>
body{
  font-family:Arial;
  background:#e3f2fd;
  text-align:center;
}
.box{
  background:white;
  max-width:400px;
  margin:auto;
  margin-top:20px;
  padding:20px;
  border-radius:20px;
  box-shadow:0 5px 20px rgba(0,0,0,0.2);
}
h1{color:#1976D2}
button{
  padding:12px 20px;
  font-size:16px;
  border:none;
  border-radius:12px;
  margin:5px;
  background:#4CAF50;
  color:white;
}
button:active{transform:scale(0.95)}
input{
  font-size:20px;
  width:100px;
  text-align:center;
}
select{
  font-size:16px;
  padding:5px;
}
.star{font-size:24px}
.timer{color:red;font-weight:bold}
</style>
</head>

<body>
<div class="box">
<h1>🧮 Toán Lớp 3</h1>

<select id="mode">
  <option value="+">➕ Cộng</option>
  <option value="-">➖ Trừ</option>
  <option value="*">✖ Nhân</option>
  <option value="/">➗ Chia</option>
</select>

<p id="question">Bấm BẮT ĐẦU</p>
<p class="timer">⏱ <span id="time">10</span>s</p>

<input type="number" id="answer"><br><br>

<button onclick="check()">Trả lời</button>
<button onclick="newQuestion()">Bắt đầu</button>

<p id="result"></p>
<p>⭐ Điểm: <span id="score">0</span></p>
<p>🏆 Cấp độ: <span id="level">1</span></p>
<p class="star" id="stars"></p>
</div>

<script>
let a,b,op,score=0,level=1,time=10,timer;

function speak(text){
  let msg=new SpeechSynthesisUtterance(text);
  msg.lang="vi-VN";
  speechSynthesis.speak(msg);
}

function random(max){return Math.floor(Math.random()*max)+1;}

function startTimer(){
  clearInterval(timer);
  time=10;
  document.getElementById("time").innerText=time;
  timer=setInterval(()=>{
    time--;
    document.getElementById("time").innerText=time;
    if(time<=0){
      clearInterval(timer);
      document.getElementById("result").innerText="⏰ Hết giờ!";
      speak("Hết giờ rồi");
    }
  },1000);
}

function newQuestion(){
  let max=level*5;
  a=random(max);
  b=random(max);
  op=document.getElementById("mode").value;
  if(op=="/") a=a*b;

  let q=`${a} ${op} ${b} bằng bao nhiêu`;
  document.getElementById("question").innerText="❓ "+q;
  document.getElementById("answer").value="";
  document.getElementById("result").innerText="";
  speak(q);
  startTimer();
}

function check(){
  clearInterval(timer);
  let ans=Number(document.getElementById("answer").value);
  let correct;

  switch(op){
    case "+":correct=a+b;break;
    case "-":correct=a-b;break;
    case "*":correct=a*b;break;
    case "/":correct=a/b;break;
  }

  if(ans===correct){
    score++;
    document.getElementById("result").innerText="🎉 Chính xác!";
    speak("Chính xác, rất giỏi");
    if(score%5===0){level++;}
  }else{
    document.getElementById("result").innerText=
      `❌ Sai rồi! Đáp án là ${correct}`;
    speak("Sai rồi");
  }

  document.getElementById("score").innerText=score;
  document.getElementById("level").innerText=level;
  document.getElementById("stars").innerText="⭐".repeat(score%5);
}
</script>
</body>
</html>