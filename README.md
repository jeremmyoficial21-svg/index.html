<!doctype html>
<html lang="es">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Circuito RL en Serie – EDO</title>

<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&family=JetBrains+Mono&display=swap" rel="stylesheet">

<style>
:root{
  --bg:#0f172a;--card:#111827;--accent:#38bdf8;
  --text:#e5e7eb;--muted:#94a3b8;--border:rgba(255,255,255,.1)
}
*{box-sizing:border-box}
body{
  margin:0;font-family:Inter,sans-serif;color:var(--text);
  background:radial-gradient(circle at 20% 20%,rgba(56,189,248,.1),transparent 40%),var(--bg)
}
header{text-align:center;padding:28px;border-bottom:1px solid var(--border)}
h1{margin:0;color:var(--accent)}
.container{max-width:1100px;margin:auto;padding:24px}
.grid{display:grid;grid-template-columns:2fr 1.2fr;gap:20px}
.card{background:var(--card);border:1px solid var(--border);border-radius:14px;padding:20px}
label{font-size:13px;color:var(--muted)}
input,select{
  width:100%;padding:8px;margin-top:4px;
  background:#020617;border:1px solid var(--border);
  color:var(--text);border-radius:8px;font-family:JetBrains Mono
}
.form{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:14px}
.row{display:grid;grid-template-columns:1fr 80px;gap:6px}
button{
  margin-top:16px;padding:10px;border:0;border-radius:10px;
  background:linear-gradient(135deg,#38bdf8,#7dd3fc);
  font-weight:600;cursor:pointer
}
canvas{
  width:100%;height:260px;background:#020617;
  border-radius:10px;border:1px solid var(--border)
}
.math{
  margin-top:14px;padding:10px;
  background:rgba(56,189,248,.08);
  border:1px dashed rgba(56,189,248,.5);
  font-family:JetBrains Mono
}
footer{text-align:center;margin:30px 0;color:var(--muted);font-size:13px}
@media(max-width:900px){.grid{grid-template-columns:1fr}}
</style>
</head>

<body>

<header>
<h1>⚡ Circuito RL en Serie</h1>
<p>Ecuación diferencial homogénea de primer orden</p>
</header>

<main class="container">
<div class="grid">

<section class="card">
<h2>Parámetros</h2>
<div class="form">

<div>
<label>Resistencia R</label>
<div class="row">
<input id="R" type="number" value="100">
<select id="Ru"><option value="ohm">Ω</option><option value="kohm">kΩ</option></select>
</div>
</div>

<div>
<label>Inductancia L</label>
<div class="row">
<input id="L" type="number" value="10">
<select id="Lu"><option value="H">H</option><option value="mH">mH</option></select>
</div>
</div>

<div>
<label>Corriente inicial I₀ (A)</label>
<input id="I0" type="number" value="1">
</div>

<div>
<label>Tiempo máximo (s)</label>
<input id="tmax" type="number" value="0.3">
</div>

</div>

<button id="calc">Calcular</button>

<div class="math">
L·dI/dt + R·I = 0<br><br>
I(t) = I₀·e<sup>−(R/L)t</sup>
</div>
</section>

<aside class="card">
<h2>Respuesta</h2>
<canvas id="c"></canvas>
<div class="math" id="tau">τ = —</div>
</aside>

</div>

<footer>
HTML + CSS + JavaScript · Uso educativo libre
</footer>
</main>

<script>
document.addEventListener("DOMContentLoaded",()=>{

const c=document.getElementById("c"),ctx=c.getContext("2d");
const calc=document.getElementById("calc");

function resize(){
  const r=window.devicePixelRatio||1;
  c.width=c.clientWidth*r;c.height=c.clientHeight*r;
  ctx.setTransform(r,0,0,r,0,0);
}
resize();window.addEventListener("resize",resize);

function Rval(){return Ru.value==="kohm"?+R.value*1000:+R.value}
function Lval(){return Lu.value==="mH"?+L.value*1e-3:+L.value}

calc.onclick=()=>{
  const R0=Rval(),L0=Lval(),I0=+I0v.value||+I0.value,t=+tmax.value;
  if(R0<=0||L0<=0||I0<=0||t<=0){alert("Valores > 0");return}

  document.getElementById("tau").textContent=
    "τ = "+(L0/R0).toExponential(3)+" s";

  ctx.clearRect(0,0,c.width,c.height);

  const w=c.clientWidth,h=c.clientHeight;
  const m={l:50,r:20,t:20,b:40};
  const pw=w-m.l-m.r,ph=h-m.t-m.b;

  ctx.strokeStyle="#38bdf8";ctx.lineWidth=2;ctx.beginPath();
  for(let i=0;i<=200;i++){
    const tt=i/200*t;
    const I=I0*Math.exp(-(R0/L0)*tt);
    const x=m.l+(tt/t)*pw;
    const y=m.t+ph-(I/I0)*ph;
    i?ctx.lineTo(x,y):ctx.moveTo(x,y);
  }
  ctx.stroke();
};

});
</script>

</body>
</html>
