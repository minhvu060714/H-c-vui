<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>Bé Vẽ Tranh EDU MASTER</title>
<style>
body{
 margin:0;font-family:Comic Sans MS,Arial;
 background:linear-gradient(#ffe6f2,#fff);
 text-align:center;
}
h1{color:#ff3399}
input,select,button{
 padding:6px 10px;margin:4px;
 border:none;border-radius:12px;
 background:#ff80bf;color:white;
 font-size:14px;
}
canvas{
 background:white;border:6px solid #ffb3d9;
 border-radius:20px;touch-action:none;
}
.color{
 width:30px;height:30px;border-radius:50%;
 display:inline-block;margin:3px;cursor:pointer;
 border:2px solid white;
}
#panel{font-size:18px;color:#ff3399;margin:6px}
</style>
</head>

<body>

<h1>🎨 Bé Vẽ Tranh EDU MASTER</h1>

<div>
 👧 Tên bé:
 <input id="name" placeholder="Nhập tên bé">
 🎓 Cấp độ:
 <select id="level">
  <option value="1">6–7 tuổi</option>
  <option value="2">8–9 tuổi</option>
  <option value="3">10 tuổi</option>
 </select>
</div>

<div id="panel">🎯 Nhiệm vụ: Vẽ một bông hoa</div>
<div id="panel">⭐ Sao: <span id="stars">0</span></div>

<div>
 <div class="color" style="background:black" onclick="setColor('black')"></div>
 <div class="color" style="background:red" onclick="setColor('red')"></div>
 <div class="color" style="background:orange" onclick="setColor('orange')"></div>
 <div class="color" style="background:yellow" onclick="setColor('yellow')"></div>
 <div class="color" style="background:green" onclick="setColor('green')"></div>
 <div class="color" style="background:blue" onclick="setColor('blue')"></div>
 <div class="color" style="background:pink" onclick="setColor('pink')"></div>
</div>

<button onclick="eraser()">🧽 Tẩy</button>
<button onclick="clearCanvas()">🗑️ Xoá</button>
<button onclick="saveImage()">💾 Lưu tranh</button>
<button onclick="complete()">✅ Hoàn thành</button>

<br><br>

<canvas id="canvas" width="360" height="420"></canvas>

<br>

<button onclick="newTask()">🎯 Nhiệm vụ mới</button>
<button onclick="ask()">📚 Câu hỏi</button>

<script>
const canvas=document.getElementById("canvas");
const ctx=canvas.getContext("2d");
let drawing=false,color="black",stars=0;
const starEl=document.getElementById("stars");

const tasks={
 1:["Vẽ bông hoa","Vẽ mặt cười","Vẽ con cá"],
 2:["Vẽ ngôi nhà","Vẽ gia đình","Vẽ con vật yêu thích"],
 3:["Vẽ ước mơ của em","Vẽ trường học","Vẽ một câu chuyện"]
};

const questions={
 1:["2 + 3 = ?","Chữ cái sau A là gì?"],
 2:["7 + 5 = ?","Chữ cái thứ 5 là gì?"],
 3:["15 - 6 = ?","Một năm có mấy tháng?"]
};

canvas.addEventListener("mousedown",start);
canvas.addEventListener("mouseup",()=>drawing=false);
canvas.addEventListener("mousemove",draw);
canvas.addEventListener("touchstart",start);
canvas.addEventListener("touchend",()=>drawing=false);
canvas.addEventListener("touchmove",draw);

function start(e){
 drawing=true;
 ctx.beginPath();
 ctx.moveTo(x(e),y(e));
}
function draw(e){
 if(!drawing)return;
 ctx.strokeStyle=color;
 ctx.lineWidth=6;
 ctx.lineCap="round";
 ctx.lineTo(x(e),y(e));
 ctx.stroke();
}
function x(e){return (e.touches?e.touches[0].clientX:e.clientX)-canvas.getBoundingClientRect().left;}
function y(e){return (e.touches?e.touches[0].clientY:e.clientY)-canvas.getBoundingClientRect().top;}

function setColor(c){color=c;}
function eraser(){color="white";}
function clearCanvas(){ctx.clearRect(0,0,canvas.width,canvas.height);}

function speak(text){
 const u=new SpeechSynthesisUtterance(text);
 u.lang="vi-VN";
 speechSynthesis.speak(u);
}

function newTask(){
 const lv=document.getElementById("level").value;
 const t=tasks[lv][Math.floor(Math.random()*tasks[lv].length)];
 document.getElementById("panel").innerText="🎯 Nhiệm vụ: "+t;
 speak("Nhiệm vụ mới. "+t);
}

function ask(){
 const lv=document.getElementById("level").value;
 const q=questions[lv][Math.floor(Math.random()*questions[lv].length)];
 speak("Câu hỏi. "+q);
 alert("📚 "+q);
}

function addStar(){
 stars++;
 starEl.innerText=stars;
}

function complete(){
 addStar();
 speak("Giỏi lắm. Con làm rất tốt");
 saveProgress();
}

function saveImage(){
 const a=document.createElement("a");
 a.download="tranh.png";
 a.href=canvas.toDataURL();
 a.click();
}

function saveProgress(){
 const name=document.getElementById("name").value||"Bé";
 localStorage.setItem(name+"_stars",stars);
}
</script>

</body>
</html>