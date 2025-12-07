# circuito RL en serie
<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Circuito RL – Ecuación Diferencial de 1er Orden</title>

  <!-- Tipografías -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&family=JetBrains+Mono&display=swap" rel="stylesheet">

  <style>
    :root {
      --bg: #0f172a;
      --card: #111827;
      --accent: #38bdf8;
      --accent2: #22c55e;
      --text: #e5e7eb;
      --muted: #94a3b8;
      --border: rgba(255,255,255,0.08);
    }

    * { box-sizing: border-box; }

    body {
      margin: 0;
      font-family: 'Inter', sans-serif;
      background:
        radial-gradient(circle at 20% 20%, rgba(56,189,248,.08), transparent 40%),
        radial-gradient(circle at 80% 10%, rgba(34,197,94,.08), transparent 40%),
        var(--bg);
      color: var(--text);
      line-height: 1.6;
    }

    header {
      padding: 30px 20px;
      border-bottom: 1px solid var(--border);
      text-align: center;
    }

    header h1 {
      margin: 0 0 8px;
      color: var(--accent);
      font-size: 28px;
      font-weight: 700;
    }

    header p {
      margin: 0;
      color: var(--muted);
      font-size: 15px;
    }

    .container {
      max-width: 1100px;
      margin: auto;
      padding: 24px;
    }

    .grid {
      display: grid;
      grid-template-columns: 2fr 1.2fr;
      gap: 20px;
    }

    .card {
      background: linear-gradient(180deg, rgba(255,255,255,0.04), rgba(255,255,255,0.01)), var(--card);
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 20px;
    }

    h2 {
      margin-top: 0;
      color: #e0f2fe;
    }

    label {
      font-size: 13px;
      color: var(--muted);
    }

    input, select {
      width: 100%;
      margin-top: 5px;
      padding: 9px;
      background: #020617;
      border: 1px solid var(--border);
      border-radius: 10px;
      color: var(--text);
      font-family: 'JetBrains Mono', monospace;
    }

    .form-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
      gap: 14px;
    }

    .row {
      display: grid;
      grid-template-columns: 1fr 90px;
      gap: 6px;
    }

    button {
      padding: 10px 14px;
      margin-top: 14px;
      border-radius: 12px;
      border: none;
      background: linear-gradient(135deg, var(--accent), #7dd3fc);
      font-weight: 600;
      cursor: pointer;
      color: #001018;
    }

    .math {
      margin-top: 18px;
      padding: 12px;
      border-radius: 10px;
      background: rgba(56,189,248,.08);
      border: 1px dashed rgba(56,189,248,.5);
      font-family: 'JetBrains Mono', monospace;
    }

    .highlight {
      color: var(--accent2);
      font-weight: 600;
    }

    canvas {
      width: 100%;
      height: 260px;
      background: #020617;
      border-radius: 12px;
      border: 1px solid var(--border);
    }

    footer {
      text-align: center;
      margin: 30px 0 10px;
      color: var(--muted);
      font-size: 13px;
    }

    @media (max-width: 900px) {
      .grid { grid-template-columns: 1fr; }
    }
  </style>
</head>

<body>

<header>
  <h1>⚡ Circuito RL en Serie</h1>
  <p>Ecuación diferencial homogénea de primer orden aplicada a circuitos eléctricos</p>
</header>

<main class="container">

  <div class="grid">

    <section class="card">
      <h2>🔢 Parámetros del circuito</h2>

      <div class="form-grid">
        <div>
          <label>Resistencia R</label>
          <div class="row">
            <input type="number" id="R_val" placeholder="100">
            <select id="R_unit">
              <option value="ohm">Ω</option>
              <option value="kohm">kΩ</option>
            </select>
          </div>
        </div>

        <div>
          <label>Inductancia L</label>
          <div class="row">
            <input type="number" id="L_val" placeholder="10">
            <select id="L_unit">
              <option value="H">H</option>
              <option value="mH">mH</option>
            </select>
          </div>
        </div>

        <div>
          <label>Corriente inicial I₀ (A)</label>
          <input type="number" id="I0" placeholder="1.5">
        </div>

        <div>
          <label>Tiempo máximo (s)</label>
          <input type="number" id="tmax" placeholder="0.1">
        </div>
      </div>

      <button id="run">Calcular y graficar</button>

      <div class="math">
        <strong>Modelo matemático:</strong><br><br>
        L · dI/dt + R · I = 0<br><br>
        <span class="highlight">
          I(t) = I₀ · e<sup>−(R/L)·t</sup>
        </span>
      </div>
    </section>

    <aside class="card">
      <h2>📈 Respuesta del circuito</h2>
      <canvas id="plot"></canvas>

      <div class="math">
        Constante de tiempo:<br>
        <span class="highlight" id="lbl_tau">τ = —</span>
      </div>
    </aside>

  </div>

  <section class="card" style="margin-top:20px">
    <h2>📘 Interpretación física</h2>
    <p>
      La corriente en un circuito RL disminuye exponencialmente debido a la disipación de energía
      en la resistencia y al efecto de la inductancia, que se opone a cambios bruscos de corriente.
    </p>
    <ul>
      <li>R grande → corriente cae más rápido</li>
      <li>L grande → sistema más lento</li>
      <li>τ define el tiempo característico</li>
    </ul>
  </section>

  <footer>
    Herramienta educativa – HTML · CSS · JavaScript – Uso libre
  </footer>

</main>

<script>
  // funciones de conversión
  function toOhm(val, unit){
    if(isNaN(val) || val <= 0) return NaN;
    return unit === 'kohm' ? val * 1e3 : val;
  }
  function toHenry(val, unit){
    if(isNaN(val) || val <= 0) return NaN;
    if(unit === 'mH') return val * 1e-3;
    return val;
  }

  // canvas simple para mostrar I(t)
  const canvas = document.getElementById('plot');
  const ctx = canvas.getContext('2d');

  function drawSimple(data){
    canvas.width = canvas.clientWidth * devicePixelRatio;
    canvas.height = canvas.clientHeight * devicePixelRatio;
    ctx.save(); ctx.scale(devicePixelRatio, devicePixelRatio);
    ctx.clearRect(0,0,canvas.clientWidth, canvas.clientHeight);

    const w = canvas.clientWidth, h = canvas.clientHeight;
    const margin = {l:50, r:12, t:12, b:30};
    const pw = w - margin.l - margin.r, ph = h - margin.t - margin.b;
    const Imax = Math.max(...data.map(d=>d.I));
    const tmin = data[0].t, tmax = data[data.length-1].t;

    // eje y labels
    ctx.fillStyle = '#9ca3af'; ctx.font = '12px system-ui';
    for(let i=0;i<=4;i++){
      const y = margin.t + ph - (i/4)*ph;
      const val = (i/4)*Imax;
      ctx.fillText(val.toFixed(2), 6, y+4);
      ctx.strokeStyle = 'rgba(255,255,255,0.03)'; ctx.beginPath();
      ctx.moveTo(margin.l, y); ctx.lineTo(margin.l+pw, y); ctx.stroke();
    }
    // eje x labels
    for(let i=0;i<=6;i++){
      const x = margin.l + (i/6)*pw;
      const tval = tmin + (i/6)*(tmax-tmin);
      ctx.fillText(tval.toFixed(3), x-10, margin.t+ph+20);
    }

    // curva
    ctx.beginPath();
    data.forEach((pt,i)=>{
      const x = margin.l + ((pt.t - tmin)/(tmax-tmin || 1))*pw;
      const y = margin.t + ph - (pt.I / (Imax || 1)) * ph;
      if(i===0) ctx.moveTo(x,y); else ctx.lineTo(x,y);
    });
    ctx.strokeStyle = '#38bdf8'; ctx.lineWidth = 2; ctx.stroke();
    ctx.restore();
  }

  document.getElementById('run').addEventListener('click', ()=>{
    const Rv = parseFloat(document.getElementById('R_val').value);
    const Runit = document.getElementById('R_unit').value;
    const Lv = parseFloat(document.getElementById('L_val').value);
    const Lunit = document.getElementById('L_unit').value;
    const I0 = parseFloat(document.getElementById('I0').value);
    const tmax = parseFloat(document.getElementById('tmax').value);

    const R = toOhm(Rv, Runit);
    const L = toHenry(Lv, Lunit);

    if(!isFinite(R) || !isFinite(L) || !isFinite(I0) || !isFinite(tmax)){
      alert('Por favor completa todos los campos con valores válidos (>0).');
      return;
    }

    const tau = L / R;
    document.getElementById('lbl_tau').textContent = 'τ = ' + tau.toExponential(3) + ' s';

    // generar datos
    const steps = 200;
    const data = [];
    for(let i=0;i<=steps;i++){
      const t = (i/steps) * tmax;
      const I = I0 * Math.exp( - (R/L) * t );
      data.push({t, I});
    }

    drawSimple(data);
  });
<script>
const canvas = document.getElementById('plot');
const ctx = canvas.getContext('2d');

/* Ajustar tamaño real del canvas */
function resizeCanvas(){
  const ratio = window.devicePixelRatio || 1;
  canvas.width = canvas.clientWidth * ratio;
  canvas.height = canvas.clientHeight * ratio;
  ctx.setTransform(ratio,0,0,ratio,0,0);
}
resizeCanvas();
window.addEventListener('resize', resizeCanvas);

/* Conversiones */
function toOhm(v,u){ return u==='kohm' ? v*1000 : v; }
function toHenry(v,u){ return u==='mH' ? v*1e-3 : v; }

/* Dibujo del gráfico */
function draw(data){
  ctx.clearRect(0,0,canvas.width,canvas.height);

  const w = canvas.clientWidth;
  const h = canvas.clientHeight;
  const m = {l:50,r:15,t:15,b:35};
  const pw = w-m.l-m.r;
  const ph = h-m.t-m.b;

  const Imax = Math.max(...data.map(d=>d.I));
  const tmax = data[data.length-1].t || 1;

  ctx.strokeStyle="#38bdf8";
  ctx.lineWidth=2;
  ctx.beginPath();

  data.forEach((p,i)=>{
    const x = m.l + (p.t/tmax)*pw;
    const y = m.t + ph - (p.I/Imax)*ph;
    if(i===0) ctx.moveTo(x,y);
    else ctx.lineTo(x,y);
  });
  ctx.stroke();

  /* Ejes */
  ctx.strokeStyle="rgba(255,255,255,0.2)";
  ctx.beginPath();
  ctx.moveTo(m.l,m.t);
  ctx.lineTo(m.l,m.t+ph);
  ctx.lineTo(m.l+pw,m.t+ph);
  ctx.stroke();
}

/* Evento botón */
document.getElementById('run').onclick = () => {
  const R = toOhm(+R_val.value, R_unit.value);
  const L = toHenry(+L_val.value, L_unit.value);
  const I0 = +I0.value;
  const tmax = +document.getElementById('tmax').value;

  if(R<=0 || L<=0 || I0<=0 || tmax<=0){
    alert("Todos los valores deben ser mayores que cero");
    return;
  }

  const tau = L/R;
  document.getElementById('lbl_tau').textContent =
    "τ = " + tau.toExponential(3) + " s";

  const data=[];
  for(let i=0;i<=200;i++){
    const t=i/200*tmax;
    data.push({t, I:I0*Math.exp(-(R/L)*t)});
  }

  draw(data);
};
</script>

</body>
</html>
