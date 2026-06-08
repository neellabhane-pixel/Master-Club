<!DOCTYPE html>
<html>
<head>
<title>Master Club</title>

<style>
body{
background:#121212;
color:white;
font-family:Arial,sans-serif;
text-align:center;
padding:20px;
}

h1{
color:gold;
}

#balance{
color:#00ff88;
}

#period{
font-size:22px;
margin:10px;
}

#timer{
font-size:50px;
margin:15px;
color:gold;
}

button{
padding:12px 20px;
margin:6px;
font-size:18px;
border:none;
border-radius:10px;
color:white;
cursor:pointer;
}

.green{
background:green;
}

.red{
background:red;
}

.violet{
background:purple;
}

.betbtn{
background:#444;
}

.resetbtn{
background:#ff8800;
}

.history{
margin-top:20px;
padding:10px;
border:1px solid #444;
border-radius:10px;
}

#result{
font-size:24px;
margin-top:15px;
font-weight:bold;
}
</style>
</head>

<body>

<h1>MASTER CLUB</h1>

<h2 id="balance">Balance: ₹1000</h2>

<button class="resetbtn" onclick="resetBalance()">
Reset Balance
</button>

<div id="period">Period: 10001</div>

<div id="timer">10</div>

<h3>Select Bet Amount</h3>

<button class="betbtn" onclick="setBet(10)">₹10</button>
<button class="betbtn" onclick="setBet(50)">₹50</button>
<button class="betbtn" onclick="setBet(100)">₹100</button>

<h3 id="bet">Selected Bet: ₹0</h3>

<button class="green" onclick="predict('GREEN')">
GREEN
</button>

<button class="red" onclick="predict('RED')">
RED
</button>

<button class="violet" onclick="predict('VIOLET')">
VIOLET
</button>

<h3 id="choice">No Prediction Selected</h3>

<div id="result"></div>

<div class="history">
<h3>Result History</h3>
<div id="history"></div>
</div>

<script>

let period = 10001;
let timer = 10;
let choice = "";
let history = [];

let balance =
parseInt(localStorage.getItem("balance")) || 1000;

let betAmount = 0;

document.addEventListener("DOMContentLoaded", () => {

document.getElementById("balance").innerText =
"Balance: ₹" + balance;

});

function resetBalance(){

balance = 1000;

localStorage.setItem("balance", balance);

document.getElementById("balance").innerText =
"Balance: ₹" + balance;

}

function setBet(amount){

betAmount = amount;

document.getElementById("bet").innerText =
"Selected Bet: ₹" + amount;

}

function predict(color){

choice = color;

document.getElementById("choice").innerText =
"Your Prediction: " + color;

}

function getResult(){

let random = Math.floor(Math.random()*3);

if(random===0) return "GREEN";
if(random===1) return "RED";
return "VIOLET";

}

setInterval(()=>{

timer--;

document.getElementById("timer").innerText = timer;

if(timer===0){

let result = getResult();

if(choice===""){

document.getElementById("result").innerHTML =
"Result: " + result;

}
else if(choice===result){

balance += betAmount;

localStorage.setItem("balance", balance);

document.getElementById("balance").innerText =
"Balance: ₹" + balance;

document.getElementById("result").innerHTML =
"🎉 You Win! Result: " + result;

}
else{

balance -= betAmount;

localStorage.setItem("balance", balance);

document.getElementById("balance").innerText =
"Balance: ₹" + balance;

document.getElementById("result").innerHTML =
"❌ You Lose! Result: " + result;

}

history.unshift(
"Period " + period + " → " + result
);

if(history.length > 5){
history.pop();
}

document.getElementById("history").innerHTML =
history.join("<br>");

period++;

document.getElementById("period").innerText =
"Period: " + period;

timer = 10;
choice = "";

document.getElementById("choice").innerText =
"No Prediction Selected";

}

},1000);

</script>

</body>
</html>
