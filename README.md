<!DOCTYPE html>
<html lang="nl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MiniKlussen | Kleine klussen, grote plannen!</title>
<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial,sans-serif;background:#eef3fa;color:#102744}
header{background:#102b4b;color:white;padding:28px 6%;text-align:center}
header h1{font-size:38px;margin:5px}
header p{color:#c8dcf5}
nav{background:#173d65;padding:15px;text-align:center;position:sticky;top:0}
nav a{color:white;text-decoration:none;margin:0 14px;font-weight:bold}
main{max-width:1100px;margin:30px auto;padding:0 18px}
h2{color:#123b69}
.hero{background:linear-gradient(120deg,#12365c,#0879e8);color:white;padding:45px 25px;border-radius:18px;text-align:center}
.hero h2{color:white;font-size:32px}
.stats{display:grid;grid-template-columns:1fr 1fr;gap:18px;margin:22px 0}
.card{background:white;border-radius:15px;padding:22px;box-shadow:0 3px 12px #152d4812}
.number{font-size:32px;font-weight:bold;color:#0868cf}
.progress{height:13px;background:#dce5f1;border-radius:20px;overflow:hidden;margin-top:12px}
.bar{height:100%;background:#0879e8;width:0%}
.jobs{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:15px}
.job{background:white;border-radius:14px;padding:20px;text-align:center;border:1px solid #dce5f1}
.job .emoji{font-size:35px}
.price{font-size:23px;color:#0871d8;font-weight:bold}
button{background:#0875df;color:white;border:0;border-radius:9px;padding:12px 18px;cursor:pointer;font-weight:bold}
button:hover{background:#0756a8}
select,input{width:100%;padding:12px;border:1px solid #ccd8e7;border-radius:8px;margin:8px 0 15px;font-size:15px}
section{margin:30px 0}
footer{background:#102b4b;color:white;text-align:center;padding:25px;margin-top:40px}
.small{font-size:13px;color:#687b91}
@media(max-width:600px){.stats{grid-template-columns:1fr}nav a{margin:5px;display:inline-block}header h1{font-size:30px}}
</style>
</head>
<body>

<header>
<h1>🔨 MiniKlussen</h1>
<p>Kleine klussen, grote plannen!</p>
</header>

<nav>
<a href="#home">Home</a>
<a href="#klussen">Klussen</a>
<a href="#aanvragen">Aanvragen</a>
<a href="#doel">Mijn doel</a>
<a href="#ouder">Ouderbeheer</a>
</nav>

<main>
<section class="hero" id="home">
<h2>Welkom bij MiniKlussen!</h2>
<p>Hulp nodig bij kleine klusjes? Bekijk ons aanbod!</p>
<a href="#klussen"><button>Bekijk onze klusjes</button></a>
</section>

<div class="stats">
<div class="card">
<h3>💰 Mijn inkomsten</h3>
<div class="number" id="income">€0</div>
</div>
<div class="card" id="doel">
<h3>🚲 Mijn fatbike-doel</h3>
<div class="number">€829</div>
<p id="remaining">Nog €829 nodig!</p>
<div class="progress"><div class="bar" id="bar"></div></div>
<p id="percentage">0% gespaard</p>
</div>
</div>

<section id="klussen">
<h2>🛠️ Onze klusjes</h2>
<div class="jobs">
<div class="job"><div class="emoji">🚗</div><h3>Auto wassen</h3><div class="price">€15</div></div>
<div class="job"><div class="emoji">🧹</div><h3>Tuin opruimen</h3><div class="price">€20</div></div>
<div class="job"><div class="emoji">🍂</div><h3>Bladeren vegen</h3><div class="price">€10</div></div>
<div class="job"><div class="emoji">🏠</div><h3>Oprit vegen</h3><div class="price">€12</div></div>
<div class="job"><div class="emoji">🪟</div><h3>Ramen wassen</h3><div class="price">€15</div></div>
<div class="job"><div class="emoji">🛒</div><h3>Kleine boodschappen</h3><div class="price">€8</div></div>
</div>
</section>

<section id="aanvragen" class="card">
<h2>📩 Een klus aanvragen</h2>
<p>Kies welke klus je wilt aanvragen.</p>
<label for="job">Welke klus?</label>
<select id="job">
<option value="Auto wassen">Auto wassen - €15</option>
<option value="Tuin opruimen">Tuin opruimen - €20</option>
<option value="Bladeren vegen">Bladeren vegen - €10</option>
<option value="Oprit vegen">Oprit vegen - €12</option>
<option value="Ramen wassen">Ramen wassen - €15</option>
<option value="Kleine boodschappen">Kleine boodschappen - €8</option>
</select>
<button onclick="requestJob()">Aanvraag simuleren</button>
<p id="message"></p>
<p class="small">Dit is een demo. Er wordt nog geen echte aanvraag verstuurd.</p>
</section>

<section class="card">
<h2>📋 Mijn aanvragen</h2>
<div id="requests">Nog geen aanvragen.</div>
</section>

<section id="ouder" class="card">
<h2>👨‍👩‍👦 Ouderbeheer</h2>
<p>Hier kunnen je ouders de demo-aanvragen bekijken.</p>
<button onclick="showParent()">Bekijk aanvragen</button>
<div id="parent"></div>
<p class="small">Dit is geen beveiligde ouderlogin. Gebruik dit onderdeel alleen als demo.</p>
</section>
</main>

<footer>
<h2 style="color:white">MiniKlussen 🛠️</h2>
<p>Kleine klussen, grote plannen!</p>
<p>© 2026 MiniKlussen</p>
</footer>

<script>
let income=0;
let requests=[];

const prices={
"Auto wassen":15,
"Tuin opruimen":20,
"Bladeren vegen":10,
"Oprit vegen":12,
"Ramen wassen":15,
"Kleine boodschappen":8
};

function update(){
document.getElementById("income").textContent="€"+income;
let remaining=Math.max(0,829-income);
let percentage=Math.min(100,Math.round(income/829*100));
document.getElementById("remaining").textContent="Nog €"+remaining+" nodig!";
document.getElementById("percentage").textContent=percentage+"% gespaard";
document.getElementById("bar").style.width=percentage+"%";
}

function requestJob(){
let job=document.getElementById("job").value;
requests.push({job:job,price:prices[job],status:"Wacht op ouder"});
document.getElementById("message").textContent="Aanvraag gesimuleerd! Je ouder moet deze eerst bekijken.";
render();
}

function render(){
let el=document.getElementById("requests");
if(requests.length===0){
el.textContent="Nog geen aanvragen.";
return;
}
el.innerHTML=requests.map((r,i)=>
"<div class='card' style='margin:10px 0'>"+
"<b>"+r.job+"</b> - €"+r.price+
"<p>Status: "+r.status+"</p></div>"
).join("");
}

function showParent(){
let el=document.getElementById("parent");
if(requests.length===0){
el.textContent="Er zijn nog geen aanvragen.";
return;
}
el.innerHTML=requests.map((r,i)=>
"<div class='card' style='margin:10px 0'>"+
"<b>"+r.job+"</b> - €"+r.price+
"<p>Status: "+r.status+"</p>"+
(r.status==="Wacht op ouder"?
"<button onclick='approve("+i+")'>Goedkeuren</button>":"")
+"</div>"
).join("");
}

function approve(i){
requests[i].status="Goedgekeurd";
showParent();
render();
}

update();
</script>
</body>
</html> <img width="556" height="648" alt="image" src="https://github.com/user-attachments/assets/d172d1fd-2ce7-4fc7-ae57-90a0d6aabc2c" />
<p>Kleine klussen, grote plannen!</p>
<p>Voor jongeren van 12 tot 15 jaar!</p> 
