<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Guía: Streamlit + Colab + GitHub</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    background: #1e1e2e;
    min-height: 100vh;
    font-family: 'JetBrains Mono', 'Fira Code', monospace;
    color: #cdd6f4;
    font-size: 13px;
  }
  .topbar {
    background: #181825;
    border-bottom: 1px solid #313244;
    padding: 10px 20px;
    display: flex;
    align-items: center;
    gap: 12px;
    position: sticky;
    top: 0;
    z-index: 10;
  }
  .dots { display: flex; gap: 6px; }
  .dot { width: 12px; height: 12px; border-radius: 50%; }
  .dot.r { background: #f38ba8; }
  .dot.y { background: #f9e2af; }
  .dot.g { background: #a6e3a1; }
  .fname { color: #6c7086; font-size: 12px; margin-left: 8px; }
  .tabs { display: flex; gap: 0; margin-left: auto; }
  .tab { padding: 4px 14px; font-size: 11px; color: #6c7086; border: 1px solid transparent; cursor: pointer; border-radius: 4px 4px 0 0; }
  .tab.active { background: #1e1e2e; color: #cdd6f4; border-color: #313244; border-bottom-color: #1e1e2e; }
  .content { padding: 24px 20px 48px; max-width: 860px; margin: 0 auto; }
  .section-label { color: #6c7086; font-size: 10px; letter-spacing: 0.12em; text-transform: uppercase; margin: 32px 0 8px; }
  .section-label:first-child { margin-top: 0; }
  .cell { background: #181825; border: 1px solid #313244; border-radius: 6px; margin-bottom: 10px; overflow: hidden; }
  .cell-header { display: flex; align-items: center; gap: 10px; padding: 8px 14px; background: #1e1e2e; border-bottom: 1px solid #313244; }
  .cell-num { color: #6c7086; font-size: 11px; min-width: 20px; }
  .cell-type { font-size: 10px; padding: 2px 8px; border-radius: 3px; letter-spacing: 0.08em; }
  .ct-bash { background: #1e3a1e; color: #a6e3a1; border: 1px solid #2d5a2d; }
  .ct-python { background: #1a2a4a; color: #89b4fa; border: 1px solid #2a4a7a; }
  .ct-markdown { background: #2a1e3a; color: #cba6f7; border: 1px solid #4a3a6a; }
  .ct-magic { background: #3a2a1e; color: #fab387; border: 1px solid #6a4a2a; }
  .ct-info { background: #1a3a3a; color: #94e2d5; border: 1px solid #2a5a5a; }
  .cell-title { color: #a6adc8; font-size: 12px; margin-left: 4px; }
  .cell-body { padding: 14px 18px; }
  .comment { color: #6c7086; }
  .kw { color: #cba6f7; }
  .fn { color: #89b4fa; }
  .str { color: #a6e3a1; }
  .num { color: #fab387; }
  .var { color: #cdd6f4; }
  .op { color: #89dceb; }
  .cmd { color: #f9e2af; }
  .flag { color: #f38ba8; }
  .path { color: #94e2d5; }
  .out { color: #a6e3a1; font-size: 11px; border-left: 2px solid #a6e3a1; padding-left: 10px; margin-top: 10px; }
  .err { color: #f38ba8; font-size: 11px; border-left: 2px solid #f38ba8; padding-left: 10px; margin-top: 10px; }
  .warn { color: #f9e2af; font-size: 11px; border-left: 2px solid #f9e2af; padding-left: 10px; margin-top: 10px; }
  .line { display: block; line-height: 1.8; white-space: pre; }
  .indent1 { padding-left: 24px; }
  .indent2 { padding-left: 48px; }
  .prose-cell { background: #181825; border: 1px solid #313244; border-left: 3px solid #cba6f7; border-radius: 6px; padding: 14px 18px; margin-bottom: 10px; color: #a6adc8; font-size: 12px; line-height: 1.9; }
  .prose-cell strong { color: #cdd6f4; font-weight: 500; }
  .prose-cell .hl { color: #f9e2af; }
  .prose-cell .ok { color: #a6e3a1; }
  .prose-cell .info { color: #89b4fa; }
  .checklist { list-style: none; margin-top: 8px; }
  .checklist li { display: flex; align-items: flex-start; gap: 10px; padding: 4px 0; color: #a6adc8; font-size: 12px; line-height: 1.6; }
  .checklist li .box { width: 14px; height: 14px; border: 1px solid #45475a; border-radius: 2px; flex-shrink: 0; margin-top: 2px; display: flex; align-items: center; justify-content: center; }
  .flow { display: flex; align-items: center; gap: 8px; flex-wrap: wrap; margin: 12px 0; }
  .flow-step { background: #1e1e2e; border: 1px solid #313244; border-radius: 4px; padding: 6px 12px; font-size: 11px; color: #cdd6f4; }
  .flow-arrow { color: #45475a; font-size: 16px; }
  .tip-block { background: #1a2a1a; border: 1px solid #2d5a2d; border-radius: 6px; padding: 12px 16px; margin-bottom: 10px; }
  .tip-block .tip-label { color: #a6e3a1; font-size: 10px; letter-spacing: 0.1em; text-transform: uppercase; margin-bottom: 6px; }
  .tip-block ul { padding-left: 16px; list-style: none; }
  .tip-block ul li { color: #a6adc8; font-size: 12px; line-height: 1.8; padding-left: 12px; position: relative; }
  .tip-block ul li::before { content: '→'; position: absolute; left: -2px; color: #a6e3a1; }
  .divider { border: none; border-top: 1px solid #313244; margin: 28px 0; }
  .inline-code { background: #313244; border-radius: 3px; padding: 1px 5px; color: #89b4fa; font-size: 12px; }
</style>
</head>
<body>

<div class="topbar">
  <div class="dots">
    <div class="dot r"></div>
    <div class="dot y"></div>
    <div class="dot g"></div>
  </div>
  <span class="fname">clase_streamlit_setup.ipynb</span>
  <div class="tabs" style="margin-left: auto;">
    <div class="tab active">Notebook</div>
    <div class="tab">Terminal</div>
  </div>
</div>

<div class="content">

  <div class="prose-cell" style="border-left-color: #89b4fa; margin-bottom: 20px;">
    <strong style="font-size: 14px; color: #cdd6f4;">Guía: Grabar una clase de Streamlit con Colab + GitHub</strong><br>
    <span style="color: #6c7086; font-size: 11px;">Flujo completo · paso a paso</span>
    <div class="flow" style="margin-top: 12px;">
      <div class="flow-step" style="border-color: #f9e2af; color: #f9e2af;">GitHub</div>
      <div class="flow-arrow">→</div>
      <div class="flow-step" style="border-color: #89b4fa; color: #89b4fa;">Google Colab</div>
      <div class="flow-arrow">→</div>
      <div class="flow-step" style="border-color: #a6e3a1; color: #a6e3a1;">Streamlit</div>
      <div class="flow-arrow">→</div>
      <div class="flow-step" style="border-color: #f38ba8; color: #f38ba8;">OBS / Loom</div>
    </div>
  </div>

  <p class="section-label">── FASE 1 · GitHub ──────────────────────────────────────</p>

  <div class="prose-cell">
    <strong>Paso 1.1 · Crear el repositorio</strong><br>
    Ir a <span class="ok">github.com</span> → "New repository" →<br>
    <span class="hl">Name:</span> clase-streamlit &nbsp;|&nbsp; <span class="hl">Visibility:</span> Public &nbsp;|&nbsp; ☑ Add README
  </div>

  <p class="section-label" style="margin-top:16px;">requirements.txt</p>
  <div class="cell">
    <div class="cell-header">
      <span class="cell-num">[1]</span>
      <span class="cell-type ct-markdown">TEXT</span>
      <span class="cell-title">requirements.txt</span>
    </div>
    <div class="cell-body">
      <span class="line"><span class="str">streamlit</span></span>
      <span class="line"><span class="str">pandas</span></span>
      <span class="line"><span class="str">matplotlib</span></span>
      <span class="line"><span class="str">plotly</span></span>
      <span class="line"><span class="str">numpy</span></span>
    </div>
  </div>

  <p class="section-label">app.py · ejemplo base</p>
  <div class="cell">
    <div class="cell-header">
      <span class="cell-num">[2]</span>
      <span class="cell-type ct-python">PYTHON</span>
      <span class="cell-title">app.py</span>
    </div>
    <div class="cell-body">
      <span class="line"><span class="kw">import</span> <span class="var">streamlit</span> <span class="kw">as</span> <span class="var">st</span></span>
      <span class="line"><span class="kw">import</span> <span class="var">pandas</span> <span class="kw">as</span> <span class="var">pd</span></span>
      <span class="line"><span class="kw">import</span> <span class="var">numpy</span> <span class="kw">as</span> <span class="var">np</span></span>
      <span class="line"> </span>
      <span class="line"><span class="var">st</span>.<span class="fn">set_page_config</span>(<span class="var">page_title</span><span class="op">=</span><span class="str">"Mi Clase de Streamlit"</span>, <span class="var">page_icon</span><span class="op">=</span><span class="str">"🎓"</span>)</span>
      <span class="line"><span class="var">st</span>.<span class="fn">title</span>(<span class="str">"🎓 Clase: Introducción a Streamlit"</span>)</span>
      <span class="line"><span class="var">st</span>.<span class="fn">markdown</span>(<span class="str">"Bienvenidos a esta clase en vivo."</span>)</span>
      <span class="line"> </span>
      <span class="line"><span class="var">st</span>.sidebar.<span class="fn">header</span>(<span class="str">"Configuración"</span>)</span>
      <span class="line"><span class="var">nombre</span> <span class="op">=</span> <span class="var">st</span>.sidebar.<span class="fn">text_input</span>(<span class="str">"Tu nombre:"</span>, <span class="str">"Estudiante"</span>)</span>
      <span class="line"><span class="var">st</span>.<span class="fn">header</span>(<span class="fn">f</span><span class="str">"Hola, {nombre}!"</span>)</span>
      <span class="line"> </span>
      <span class="line"><span class="var">n</span> <span class="op">=</span> <span class="var">st</span>.<span class="fn">slider</span>(<span class="str">"Número de puntos:"</span>, <span class="num">10</span>, <span class="num">200</span>, <span class="num">50</span>)</span>
      <span class="line"><span class="var">datos</span> <span class="op">=</span> <span class="var">pd</span>.<span class="fn">DataFrame</span>(<span class="var">np</span>.random.<span class="fn">randn</span>(<span class="var">n</span>, <span class="num">2</span>), <span class="var">columns</span><span class="op">=</span>[<span class="str">"X"</span>, <span class="str">"Y"</span>])</span>
      <span class="line"><span class="var">st</span>.<span class="fn">line_chart</span>(<span class="var">datos</span>)</span>
    </div>
  </div>

  <hr class="divider">
  <p class="section-label">── FASE 2 · Google Colab ────────────────────────────────</p>

  <div class="prose-cell">
    Ir a <span class="ok">colab.research.google.com</span> → "Nuevo notebook" → guardar como <span class="hl">Clase_Streamlit_Setup.ipynb</span>
  </div>

  <div class="cell">
    <div class="cell-header">
      <span class="cell-num">[3]</span>
      <span class="cell-type ct-bash">BASH</span>
      <span class="cell-title">Paso 2.1 · Clonar el repositorio</span>
    </div>
    <div class="cell-body">
      <span class="line"><span class="comment"># Reemplaza TU_USUARIO con tu nombre de GitHub</span></span>
      <span class="line"><span class="cmd">!git</span> <span class="flag">clone</span> <span class="path">https://github.com/TU_USUARIO/clase-streamlit.git</span></span>
      <span class="line"><span class="cmd">%cd</span> <span class="path">clase-streamlit</span></span>
    </div>
  </div>

  <div class="cell">
    <div class="cell-header">
      <span class="cell-num">[4]</span>
      <span class="cell-type ct-bash">BASH</span>
      <span class="cell-title">Paso 2.2 · Instalar dependencias</span>
    </div>
    <div class="cell-body">
      <span class="line"><span class="cmd">!pip</span> <span class="flag">install</span> <span class="flag">-r</span> <span class="path">requirements.txt</span> <span class="flag">-q</span></span>
    </div>
  </div>

  <div class="cell">
    <div class="cell-header">
      <span class="cell-num">[5]</span>
      <span class="cell-type ct-bash">BASH</span>
      <span class="cell-title">Paso 2.3 · Instalar localtunnel</span>
    </div>
    <div class="cell-body">
      <span class="line"><span class="cmd">!npm</span> <span class="flag">install</span> <span class="flag">-g</span> <span class="var">localtunnel</span> <span class="flag">-q</span></span>
    </div>
  </div>

  <div class="cell">
    <div class="cell-header">
      <span class="cell-num">[6]</span>
      <span class="cell-type ct-python">PYTHON</span>
      <span class="cell-title">Paso 2.4 · Lanzar Streamlit en segundo plano</span>
    </div>
    <div class="cell-body">
      <span class="line"><span class="kw">import</span> <span class="var">subprocess</span>, <span class="var">threading</span>, <span class="var">time</span></span>
      <span class="line"> </span>
      <span class="line"><span class="kw">def</span> <span class="fn">run_streamlit</span>():</span>
      <span class="line indent1"><span class="var">subprocess</span>.<span class="fn">run</span>([<span class="str">"streamlit"</span>, <span class="str">"run"</span>, <span class="str">"app.py"</span>,</span>
      <span class="line indent2"><span class="str">"--server.port"</span>, <span class="str">"8501"</span>,</span>
      <span class="line indent2"><span class="str">"--server.headless"</span>, <span class="str">"true"</span>,</span>
      <span class="line indent2"><span class="str">"--server.runOnSave"</span>, <span class="str">"true"</span>])</span>
      <span class="line"> </span>
      <span class="line"><span class="var">t</span> <span class="op">=</span> <span class="var">threading</span>.<span class="fn">Thread</span>(<span class="var">target</span><span class="op">=</span><span class="fn">run_streamlit</span>)</span>
      <span class="line"><span class="var">t</span>.daemon <span class="op">=</span> <span class="kw">True</span></span>
      <span class="line"><span class="var">t</span>.<span class="fn">start</span>()</span>
      <span class="line"><span class="var">time</span>.<span class="fn">sleep</span>(<span class="num">5</span>)</span>
      <span class="line"><span class="fn">print</span>(<span class="str">"✅ Streamlit iniciado en puerto 8501"</span>)</span>
      <div class="out">✅ Streamlit iniciado en puerto 8501</div>
    </div>
  </div>

  <div class="cell">
    <div class="cell-header">
      <span class="cell-num">[7]</span>
      <span class="cell-type ct-python">PYTHON</span>
      <span class="cell-title">Paso 2.5 · Obtener IP pública</span>
    </div>
    <div class="cell-body">
      <span class="line"><span class="kw">import</span> <span class="var">urllib.request</span></span>
      <span class="line"><span class="var">ip</span> <span class="op">=</span> <span class="var">urllib.request</span>.<span class="fn">urlopen</span>(<span class="str">'https://ipv4.icanhazip.com'</span>).<span class="fn">read</span>().<span class="fn">decode</span>(<span class="str">'utf8'</span>).<span class="fn">strip</span>()</span>
      <span class="line"><span class="fn">print</span>(<span class="fn">f</span><span class="str">"IP del servidor: {ip}"</span>)</span>
      <div class="out">IP del servidor: 34.82.xxx.xxx</div>
    </div>
  </div>

  <div class="cell">
    <div class="cell-header">
      <span class="cell-num">[8]</span>
      <span class="cell-type ct-bash">BASH</span>
      <span class="cell-title">Paso 2.6 · Abrir túnel → obtener URL pública</span>
    </div>
    <div class="cell-body">
      <span class="line"><span class="cmd">!lt</span> <span class="flag">--port</span> <span class="num">8501</span></span>
      <div class="out">your url is: https://xxxx.loca.lt</div>
      <div class="warn">⚠ Usa esa URL en tu navegador para ver y grabar la app</div>
    </div>
  </div>

  <div class="prose-cell" style="border-left-color: #89b4fa;">
    <strong>Alternativa · pyngrok (más estable)</strong>
  </div>

  <div class="cell">
    <div class="cell-header">
      <span class="cell-num">[9]</span>
      <span class="cell-type ct-python">PYTHON</span>
      <span class="cell-title">ngrok · túnel alternativo</span>
    </div>
    <div class="cell-body">
      <span class="line"><span class="cmd">!pip</span> <span class="flag">install</span> <span class="var">pyngrok</span> <span class="flag">-q</span></span>
      <span class="line"><span class="kw">from</span> <span class="var">pyngrok</span> <span class="kw">import</span> <span class="var">ngrok</span></span>
      <span class="line"> </span>
      <span class="line"><span class="comment"># Authtoken desde ngrok.com → Dashboard → "Your Authtoken"</span></span>
      <span class="line"><span class="var">ngrok</span>.<span class="fn">set_auth_token</span>(<span class="str">"TU_AUTHTOKEN"</span>)</span>
      <span class="line"><span class="var">public_url</span> <span class="op">=</span> <span class="var">ngrok</span>.<span class="fn">connect</span>(<span class="num">8501</span>)</span>
      <span class="line"><span class="fn">print</span>(<span class="fn">f</span><span class="str">"🚀 Tu app: {public_url}"</span>)</span>
      <div class="out">🚀 Tu app: NgrokTunnel: "https://abc123.ngrok.io"</div>
    </div>
  </div>

  <hr class="divider">
  <p class="section-label">── FASE 3 · Editar código en vivo ──────────────────────</p>

  <div class="cell">
    <div class="cell-header">
      <span class="cell-num">[10]</span>
      <span class="cell-type ct-magic">MAGIC</span>
      <span class="cell-title">Opción A · Editar directo en Colab con %%writefile</span>
    </div>
    <div class="cell-body">
      <span class="line"><span class="op">%%writefile</span> <span class="path">app.py</span></span>
      <span class="line"> </span>
      <span class="line"><span class="kw">import</span> <span class="var">streamlit</span> <span class="kw">as</span> <span class="var">st</span></span>
      <span class="line"> </span>
      <span class="line"><span class="var">st</span>.<span class="fn">title</span>(<span class="str">"🎓 Clase en Vivo - Tema del Día"</span>)</span>
      <span class="line"><span class="comment"># Aquí vas agregando código en vivo</span></span>
      <span class="line"><span class="var">st</span>.<span class="fn">write</span>(<span class="str">"¡Hola desde la clase!"</span>)</span>
      <div class="out">Overwriting app.py</div>
    </div>
  </div>

  <div class="cell">
    <div class="cell-header">
      <span class="cell-num">[11]</span>
      <span class="cell-type ct-bash">BASH</span>
      <span class="cell-title">Opción B · Editar en GitHub y hacer pull</span>
    </div>
    <div class="cell-body">
      <span class="line"><span class="comment"># Edita app.py en github.com y luego:</span></span>
      <span class="line"><span class="cmd">!git</span> <span class="flag">pull</span> <span class="var">origin</span> <span class="var">main</span></span>
      <span class="line"><span class="comment"># Streamlit recarga automáticamente con --server.runOnSave true</span></span>
      <div class="out">Already up to date.</div>
    </div>
  </div>

  <div class="cell">
    <div class="cell-header">
      <span class="cell-num">[12]</span>
      <span class="cell-type ct-python">PYTHON</span>
      <span class="cell-title">Reiniciar Streamlit si algo falla</span>
    </div>
    <div class="cell-body">
      <span class="line"><span class="kw">import</span> <span class="var">os</span>, <span class="var">subprocess</span>, <span class="var">threading</span>, <span class="var">time</span></span>
      <span class="line"><span class="var">os</span>.<span class="fn">system</span>(<span class="str">"pkill -f streamlit"</span>)</span>
      <span class="line"><span class="var">time</span>.<span class="fn">sleep</span>(<span class="num">2</span>)</span>
      <span class="line"> </span>
      <span class="line"><span class="kw">def</span> <span class="fn">run_streamlit</span>():</span>
      <span class="line indent1"><span class="var">subprocess</span>.<span class="fn">run</span>([<span class="str">"streamlit"</span>, <span class="str">"run"</span>, <span class="str">"app.py"</span>,</span>
      <span class="line indent2"><span class="str">"--server.port"</span>, <span class="str">"8501"</span>,</span>
      <span class="line indent2"><span class="str">"--server.headless"</span>, <span class="str">"true"</span>])</span>
      <span class="line"><span class="var">t</span> <span class="op">=</span> <span class="var">threading</span>.<span class="fn">Thread</span>(<span class="var">target</span><span class="op">=</span><span class="fn">run_streamlit</span>)</span>
      <span class="line"><span class="var">t</span>.daemon <span class="op">=</span> <span class="kw">True</span>; <span class="var">t</span>.<span class="fn">start</span>()</span>
      <span class="line"><span class="fn">print</span>(<span class="str">"✅ Streamlit reiniciado"</span>)</span>
      <div class="out">✅ Streamlit reiniciado</div>
    </div>
  </div>

  <hr class="divider">
  <p class="section-label">── FASE 4 · Grabar la pantalla ─────────────────────────</p>

  <div class="prose-cell">
    <strong>Opción A · OBS Studio</strong> — mejor calidad<br>
    <span class="hl">obsproject.com</span> → instalar → "+" en Fuentes → "Captura de pantalla" → seleccionar ventana del navegador → "Iniciar grabación"<br><br>
    <strong>Config recomendada:</strong> 1920×1080 · 30 FPS · MP4 · 4000 Kbps
  </div>

  <div class="prose-cell">
    <strong>Opción B · Loom</strong> — más rápido, sin configuración<br>
    <span class="ok">loom.com</span> → extensión de Chrome → "Screen + Cam" → seleccionar ventana → "Start Recording"<br>
    Al terminar obtienes un link para compartir directamente.
  </div>

  <div class="prose-cell">
    <strong>Opción C · Nativo del sistema</strong><br>
    <span class="hl">Windows:</span> Win + G &nbsp;|&nbsp; <span class="hl">Mac:</span> Cmd + Shift + 5 &nbsp;|&nbsp; <span class="hl">Linux:</span> Kazam
  </div>

  <hr class="divider">
  <p class="section-label">── FASE 5 · Guardar al terminar ────────────────────────</p>

  <div class="cell">
    <div class="cell-header">
      <span class="cell-num">[13]</span>
      <span class="cell-type ct-bash">BASH</span>
      <span class="cell-title">Configurar git (solo la primera vez)</span>
    </div>
    <div class="cell-body">
      <span class="line"><span class="cmd">!git</span> <span class="flag">config</span> <span class="flag">--global</span> <span class="var">user.email</span> <span class="str">"tu@email.com"</span></span>
      <span class="line"><span class="cmd">!git</span> <span class="flag">config</span> <span class="flag">--global</span> <span class="var">user.name</span>  <span class="str">"Tu Nombre"</span></span>
    </div>
  </div>

  <div class="cell">
    <div class="cell-header">
      <span class="cell-num">[14]</span>
      <span class="cell-type ct-bash">BASH</span>
      <span class="cell-title">Commit y push al finalizar la clase</span>
    </div>
    <div class="cell-body">
      <span class="line"><span class="cmd">!git</span> <span class="flag">add</span> <span class="path">.</span></span>
      <span class="line"><span class="cmd">!git</span> <span class="flag">commit</span> <span class="flag">-m</span> <span class="str">"Clase: tema del día"</span></span>
      <span class="line"><span class="cmd">!git</span> <span class="flag">push</span> <span class="var">origin</span> <span class="var">main</span></span>
      <div class="warn">⚠ Usa un Personal Access Token de GitHub como contraseña</div>
    </div>
  </div>

  <div class="prose-cell" style="border-left-color: #f9e2af;">
    <strong>Crear Personal Access Token en GitHub:</strong><br>
    Foto de perfil → Settings → Developer settings → Personal access tokens → Tokens (classic)<br>
    → "Generate new token" → marcar permiso <span class="hl">repo</span> → copiar y guardar<br>
    → Usarlo como contraseña cuando git lo pida
  </div>

  <hr class="divider">
  <p class="section-label">── CHECKLIST antes de grabar ───────────────────────────</p>

  <div class="cell" style="border-left: 3px solid #a6e3a1;">
    <div class="cell-body">
      <ul class="checklist">
        <li><div class="box"></div>Repositorio de GitHub creado con app.py y requirements.txt</li>
        <li><div class="box"></div>Notebook de Colab funcionando y Streamlit corriendo</li>
        <li><div class="box"></div>URL pública de la app abierta en el navegador</li>
        <li><div class="box"></div>OBS o Loom configurado y probado</li>
        <li><div class="box"></div>Micrófono probado</li>
        <li><div class="box"></div>Notificaciones del sistema cerradas</li>
        <li><div class="box"></div>Teléfono en silencio</li>
        <li><div class="box"></div>Link del repo listo para compartir con estudiantes</li>
      </ul>
    </div>
  </div>

  <hr class="divider">
  <p class="section-label">── TIPS ─────────────────────────────────────────────────</p>

  <div class="tip-block">
    <div class="tip-label">// tips para una clase fluida</div>
    <ul>
      <li>Prepara el código base antes y expande en vivo</li>
      <li>Usa comentarios numerados: <span class="inline-code"># Paso 1</span>, <span class="inline-code"># Paso 2</span>…</li>
      <li>Comparte el link del repo al inicio de la clase</li>
      <li><span class="inline-code">--server.runOnSave true</span> recarga Streamlit al guardar automáticamente</li>
      <li>Haz commits frecuentes para que los estudiantes vean el historial</li>
      <li>Graba en segmentos si la clase es larga — más fácil de editar</li>
    </ul>
  </div>

</div>
</body>
</html>
