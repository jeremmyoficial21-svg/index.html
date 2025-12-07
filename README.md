# index.html
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
            <input type="number" placeholder="100">
            <select>
              <option>Ω</option>
              <option>kΩ</option>
            </select>
          </div>
        </div>

        <div>
          <label>Inductancia L</label>
          <div class="row">
            <input type="number" placeholder="10">
            <select>
              <option>H</option>
              <option>mH</option>
            </select>
          </div>
        </div>

        <div>
          <label>Corriente inicial I₀ (A)</label>
          <input type="number" placeholder="1.5">
        </div>

        <div>
          <label>Tiempo máximo (s)</label>
          <input type="number" placeholder="0.1">
        </div>
      </div>

      <button>Calcular</button>

      <div class="math">
        <strong>Modelo matemático:</strong><br><br>
        L · dI/dt + R · I = 0<br><br>
        <span class="highlight">
          I(t) = I₀ · e<sup>−(R/L)t</sup>
        </span>
      </div>
    </section>

    <aside class="card">
      <h2>📈 Respuesta del circuito</h2>
      <canvas></canvas>

      <div class="math">
        Constante de tiempo:<br>
        <span class="highlight">τ = L / R</span>
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

</body>
</html>
