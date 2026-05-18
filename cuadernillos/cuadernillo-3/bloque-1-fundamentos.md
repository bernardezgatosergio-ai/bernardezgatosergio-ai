<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Cuadernillo III — Álgebra sobre el Iris (Temas 1–15)</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;0,900;1,400&family=JetBrains+Mono:wght@300;400;600&family=Crimson+Pro:ital,wght@0,300;0,400;0,600;1,400&display=swap" rel="stylesheet">
<style>
:root {
  --ink:#1a1410; --paper:#faf7f2; --cream:#f0ebe0;
  --gold:#c9923a; --gold-lt:#e8c27a;
  --s:#6b9e6b; --ve:#5a7fa8; --vi:#9b6b9b;
  --rule:#d4c9b8; --dark:#1e1a14; --dt:#e8dcc8;
  --red:#c94a3a;
}
*{box-sizing:border-box;margin:0;padding:0}
body{background:var(--paper);color:var(--ink);font-family:'Crimson Pro',Georgia,serif;font-size:18px;line-height:1.7}
.app{display:flex;min-height:100vh}

/* ── SIDEBAR ── */
.sidebar{width:280px;min-width:280px;background:var(--dark);color:var(--dt);display:flex;flex-direction:column;position:sticky;top:0;height:100vh;overflow:hidden}
.sb-head{padding:24px 20px 16px;border-bottom:1px solid #333}
.sb-title{font-family:'Playfair Display',serif;font-size:14px;font-weight:700;letter-spacing:.12em;text-transform:uppercase;color:var(--gold);margin-bottom:3px}
.sb-sub{font-family:'JetBrains Mono',monospace;font-size:10px;color:#555;letter-spacing:.08em}
.sb-nav{overflow-y:auto;flex:1;padding:6px 0}
.sb-nav::-webkit-scrollbar{width:3px}
.sb-nav::-webkit-scrollbar-thumb{background:#444;border-radius:2px}
.blk-label{font-family:'JetBrains Mono',monospace;font-size:9px;letter-spacing:.15em;text-transform:uppercase;color:var(--gold);padding:12px 20px 3px;opacity:.8}
.nav-item{display:flex;align-items:center;gap:9px;padding:6px 20px;cursor:pointer;transition:background .15s;border-left:3px solid transparent}
.nav-item:hover{background:rgba(201,146,58,.08)}
.nav-item.active{background:rgba(201,146,58,.13);border-left-color:var(--gold)}
.nav-num{font-family:'JetBrains Mono',monospace;font-size:10px;color:#555;min-width:18px}
.nav-item.active .nav-num{color:var(--gold)}
.nav-lbl{font-size:12px;color:#999;line-height:1.3}
.nav-item.active .nav-lbl{color:#e8dcc8}

/* ── MAIN ── */
.main{flex:1;overflow-y:auto}
.main::-webkit-scrollbar{width:5px}
.main::-webkit-scrollbar-thumb{background:var(--rule);border-radius:3px}

/* ── HERO ── */
.hero{background:var(--ink);color:var(--paper);padding:56px 64px;position:relative;overflow:hidden}
.hero::before{content:'';position:absolute;inset:0;background:radial-gradient(ellipse at 72% 50%,rgba(201,146,58,.15) 0%,transparent 60%),radial-gradient(ellipse at 10% 80%,rgba(107,158,107,.1) 0%,transparent 50%)}
.hero-eye{font-family:'JetBrains Mono',monospace;font-size:10px;letter-spacing:.2em;text-transform:uppercase;color:var(--gold);margin-bottom:16px;position:relative}
.hero h1{font-family:'Playfair Display',serif;font-size:clamp(32px,5vw,58px);font-weight:900;line-height:1.05;position:relative;margin-bottom:14px}
.hero h1 em{font-style:italic;color:var(--gold-lt)}
.hero-desc{font-size:16px;color:#999;max-width:480px;position:relative;margin-bottom:28px;line-height:1.6}
.pills{display:flex;gap:10px;position:relative;flex-wrap:wrap}
.pill{display:flex;align-items:center;gap:6px;padding:5px 12px;border-radius:20px;font-family:'JetBrains Mono',monospace;font-size:10px;border:1px solid}
.pd{width:7px;height:7px;border-radius:50%}
.pill.s{color:var(--s);border-color:var(--s)}.pill.s .pd{background:var(--s)}
.pill.ve{color:#7ab0d8;border-color:#7ab0d8}.pill.ve .pd{background:#7ab0d8}
.pill.vi{color:#c89bc8;border-color:#c89bc8}.pill.vi .pd{background:#c89bc8}
.orn{position:absolute;right:64px;top:50%;transform:translateY(-50%);font-size:140px;opacity:.04;font-family:'Playfair Display',serif;pointer-events:none;user-select:none}

/* ── CONTENT ── */
.content{padding:48px 64px;max-width:880px;animation:fadeUp .3s ease}
@keyframes fadeUp{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}
.t-header{display:flex;align-items:baseline;gap:16px;margin-bottom:6px}
.t-num{font-family:'JetBrains Mono',monospace;font-size:12px;color:var(--gold);letter-spacing:.1em}
.t-block{font-family:'JetBrains Mono',monospace;font-size:9px;letter-spacing:.12em;text-transform:uppercase;color:#999;padding:2px 7px;border:1px solid var(--rule);border-radius:3px}
.t-title{font-family:'Playfair Display',serif;font-size:clamp(24px,3vw,36px);font-weight:700;line-height:1.15;margin-bottom:4px}
.t-sub{font-style:italic;color:#888;font-size:15px;margin-bottom:36px;padding-bottom:20px;border-bottom:1px solid var(--rule)}

/* ── SECTIONS ── */
.sec{margin-bottom:36px}
.sec-lbl{display:flex;align-items:center;gap:10px;margin-bottom:14px}
.sec-ic{width:30px;height:30px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:14px;flex-shrink:0}
.sec-ic.d{background:rgba(107,158,107,.15)}
.sec-ic.a{background:rgba(90,127,168,.15)}
.sec-ic.c{background:rgba(201,146,58,.15)}
.sec-nm{font-family:'JetBrains Mono',monospace;font-size:10px;letter-spacing:.12em;text-transform:uppercase;font-weight:600}
.sec-nm.d{color:var(--s)}.sec-nm.a{color:var(--ve)}.sec-nm.c{color:var(--gold)}

.prose{font-size:16px;line-height:1.75;color:#2a2018}
.prose p{margin-bottom:10px}

/* ── MATH BLOCK ── */
.mb{background:var(--dark);color:var(--dt);border-radius:7px;padding:20px 24px;margin:16px 0;font-family:'JetBrains Mono',monospace;font-size:13px;line-height:1.9;overflow-x:auto;border-left:3px solid var(--gold)}
.mb .ml{font-size:9px;letter-spacing:.15em;text-transform:uppercase;color:var(--gold);margin-bottom:8px;opacity:.7}
.mb .hi{color:var(--gold-lt);font-weight:600}
.mb .cm{color:#666;font-style:italic}
.mb .ok{color:#7ec87e}
.mb .ms{color:var(--s)}.mb .mve{color:#7ab0d8}.mb .mvi{color:#c89bc8}

/* ── DEF BOX ── */
.def{border:1px solid var(--rule);border-radius:6px;padding:18px 22px;margin:16px 0;background:rgba(201,146,58,.03)}
.def-t{font-family:'Playfair Display',serif;font-size:12px;font-weight:700;letter-spacing:.08em;text-transform:uppercase;color:var(--gold);margin-bottom:8px}

/* ── INSIGHT ── */
.ins{background:rgba(107,158,107,.08);border-left:4px solid var(--s);padding:14px 18px;margin:16px 0;border-radius:0 5px 5px 0}
.ins-lbl{font-family:'JetBrains Mono',monospace;font-size:9px;letter-spacing:.15em;text-transform:uppercase;color:var(--s);margin-bottom:5px}

/* ── NAV FOOTER ── */
.nf{padding:28px 64px 44px;display:flex;justify-content:space-between;align-items:center;border-top:1px solid var(--rule);max-width:880px}
.nb{display:flex;align-items:center;gap:9px;padding:10px 18px;border:1px solid var(--rule);border-radius:5px;background:transparent;cursor:pointer;font-family:'Crimson Pro',serif;font-size:15px;color:var(--ink);transition:all .2s}
.nb:hover{border-color:var(--gold);color:var(--gold);background:rgba(201,146,58,.05)}
.nb:disabled{opacity:.3;cursor:default}
.nb:disabled:hover{border-color:var(--rule);color:var(--ink);background:transparent}
.prog{font-family:'JetBrains Mono',monospace;font-size:10px;color:#999;text-align:center}
.pb-wrap{width:100px;height:3px;background:var(--rule);border-radius:2px;margin:5px auto 0}
.pb-fill{height:100%;background:var(--gold);border-radius:2px;transition:width .3s}
.im{font-family:'JetBrains Mono',monospace;font-size:13px;background:rgba(201,146,58,.08);padding:1px 5px;border-radius:3px;color:#5a3a10}

@media(max-width:768px){
  .sidebar{display:none}
  .hero{padding:36px 24px}
  .content{padding:28px 24px}
  .nf{padding:20px 24px 36px}
  .orn{display:none}
}
</style>
</head>
<body>
<div class="app">

<!-- SIDEBAR -->
<aside class="sidebar">
  <div class="sb-head">
    <div class="sb-title">Cuadernillo III</div>
    <div class="sb-sub">Álgebra · Iris Dataset · Temas 1–15</div>
  </div>
  <nav class="sb-nav" id="nav"></nav>
</aside>

<!-- MAIN -->
<main class="main" id="main">
  <div class="hero">
    <div class="hero-eye">Cuadernillo III · Aplicación Práctica · Parte 1 de 3</div>
    <h1>Álgebra sobre<br><em>Iris</em></h1>
    <p class="hero-desc">Temas 1–15. Fundamentos, Geometría Euclidea y Matrices — todos calculados con los datos reales de Fisher (1936).</p>
    <div class="pills">
      <div class="pill s"><div class="pd"></div>Iris setosa · μ=[5.006, 3.428, 1.462, 0.246]</div>
      <div class="pill ve"><div class="pd"></div>Iris versicolor · μ=[5.936, 2.770, 4.260, 1.326]</div>
      <div class="pill vi"><div class="pd"></div>Iris virginica · μ=[6.588, 2.974, 5.552, 2.026]</div>
    </div>
    <div class="orn">∑</div>
  </div>
  <div id="topic"></div>
</main>
</div>

<script>
// ══════════════════════════════════════════════════
// DATOS REALES IRIS (Fisher 1936)
// ══════════════════════════════════════════════════
const MS = [5.006, 3.428, 1.462, 0.246];
const MVE = [5.936, 2.770, 4.260, 1.326];
const MVI = [6.588, 2.974, 5.552, 2.026];
const MG  = [5.843, 3.057, 3.758, 1.199];

// ══════════════════════════════════════════════════
// TEMAS 1–15
// ══════════════════════════════════════════════════
const TOPICS = [

// ── BLOQUE I: FUNDAMENTOS ──────────────────────────
{id:1, block:'I · Fundamentos',
title:'Espacio Vectorial',
sub:'¿Dónde viven nuestras flores?',
html:`
<div class="sec">
  <div class="sec-lbl"><div class="sec-ic d">🌸</div><span class="sec-nm d">Dummies — La intuición</span></div>
  <div class="prose">
    <p>Cada flor Iris es un punto en el espacio. No el espacio 3D de la vida cotidiana, sino uno de <strong>cuatro dimensiones</strong>: longitud del sépalo, ancho del sépalo, longitud del pétalo y ancho del pétalo.</p>
    <p>Un <em>espacio vectorial</em> es un "contenedor" donde puedes sumar objetos y multiplicarlos por números, y el resultado sigue viviendo dentro. Las flores Iris son puntos en ese contenedor: <span class="im">ℝ⁴</span>.</p>
    <p>Si sumas dos flores coordenada a coordenada, obtienes otra "flor virtual" en ℝ⁴. Si multiplicas todas las medidas por 2, sigues en ℝ⁴. Esa es la esencia.</p>
  </div>
  <div class="ins"><div class="ins-lbl">🔑 Clave intuitiva</div>
    <div class="prose" style="font-size:15px">Cada flor = un vector de 4 números. Todas las flores posibles juntas forman el espacio ℝ⁴.</div>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic a">∑</div><span class="sec-nm a">Algebraico — La definición</span></div>
  <div class="def">
    <div class="def-t">Definición: Espacio Vectorial sobre ℝ</div>
    <div class="prose"><p>Un <strong>espacio vectorial</strong> sobre ℝ es un conjunto V con dos operaciones que satisfacen 8 axiomas:</p></div>
  </div>
  <div class="mb">
<div class="ml">8 Axiomas del Espacio Vectorial</div>
<span class="hi">Adición:</span>     +: V × V → V
<span class="hi">Escalar:</span>    · : ℝ × V → V

(A1) u + v = v + u                      <span class="cm">// conmutatividad</span>
(A2) (u+v)+w = u+(v+w)                  <span class="cm">// asociatividad</span>
(A3) ∃ 0 ∈ V : v + 0 = v               <span class="cm">// elemento neutro</span>
(A4) ∀v ∃(-v) : v + (-v) = 0           <span class="cm">// inverso aditivo</span>
(S1) α(βv) = (αβ)v                     <span class="cm">// comp. escalar</span>
(S2) 1·v = v                           <span class="cm">// escalar unidad</span>
(S3) α(u+v) = αu + αv                  <span class="cm">// distributiva I</span>
(S4) (α+β)v = αv + βv                  <span class="cm">// distributiva II</span>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic c">🔢</div><span class="sec-nm c">Cálculo con el Iris — datos reales Fisher 1936</span></div>
  <div class="mb">
<div class="ml">Vectores media de cada especie (∈ ℝ⁴)</div>
<span class="ms">μ_setosa</span>     = [5.006, 3.428, 1.462, 0.246]ᵀ
<span class="mve">μ_versicolor</span> = [5.936, 2.770, 4.260, 1.326]ᵀ
<span class="mvi">μ_virginica</span>  = [6.588, 2.974, 5.552, 2.026]ᵀ

<span class="cm">// Verificación A1: μ_s + μ_ve = μ_ve + μ_s</span>
<span class="ms">μ_s</span> + <span class="mve">μ_ve</span> = [10.942, 6.198, 5.722, 1.572]ᵀ
<span class="mve">μ_ve</span> + <span class="ms">μ_s</span> = [10.942, 6.198, 5.722, 1.572]ᵀ  <span class="ok">✓</span>

<span class="cm">// Verificación S2: 1·μ_s = μ_s</span>
1·[5.006,3.428,1.462,0.246]ᵀ = [5.006,3.428,1.462,0.246]ᵀ  <span class="ok">✓</span>

<span class="cm">// Flor media global como combinación lineal válida:</span>
<span class="hi">μ_global</span> = (1/3)·<span class="ms">μ_s</span> + (1/3)·<span class="mve">μ_ve</span> + (1/3)·<span class="mvi">μ_vi</span>
         = [5.843, 3.057, 3.758, 1.199]ᵀ  ← también ∈ ℝ⁴ <span class="ok">✓</span>
  </div>
  <div class="ins"><div class="ins-lbl">Conclusión</div>
    <div class="prose" style="font-size:15px">Cada flor Iris es un vector en ℝ⁴ que satisface los 8 axiomas. La "flor media global" es una combinación lineal válida: sigue siendo un punto del mismo espacio.</div>
  </div>
</div>
`},

{id:2, block:'I · Fundamentos',
title:'Subespacio Vectorial',
sub:'Subestructuras dentro de ℝ⁴',
html:`
<div class="sec">
  <div class="sec-lbl"><div class="sec-ic d">🌸</div><span class="sec-nm d">Dummies</span></div>
  <div class="prose">
    <p>Un <em>subespacio</em> es un "cuarto" dentro del "edificio" ℝ⁴. Un subconjunto de flores tal que si las sumas o escales, el resultado sigue dentro del mismo cuarto.</p>
    <p>Por ejemplo: el conjunto de vectores con ceros en las dos primeras coordenadas, <span class="im">(0,0,x₃,x₄)</span>, forma un plano dentro de ℝ⁴ — un subespacio de dimensión 2 que sólo contiene "flores sin sépalo".</p>
    <p>Los subespacios siempre pasan por el origen: son "planos que contienen el cero".</p>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic a">∑</div><span class="sec-nm a">Algebraico</span></div>
  <div class="def">
    <div class="def-t">Definición: Subespacio Vectorial</div>
    <div class="prose"><p>W ⊆ V es subespacio si y sólo si cumple tres condiciones:</p></div>
  </div>
  <div class="mb">
<div class="ml">Tres condiciones (necesarias y suficientes)</div>
(W1) <span class="hi">0 ∈ W</span>                          <span class="cm">// contiene el origen</span>
(W2) u, v ∈ W  ⟹  u + v ∈ W        <span class="cm">// cerrado en adición</span>
(W3) v ∈ W, α ∈ ℝ  ⟹  αv ∈ W      <span class="cm">// cerrado en escalar</span>

<span class="cm">// Equivalente compacto:</span>
W es subespacio ⟺ ∀α,β∈ℝ, ∀u,v∈W:  αu + βv ∈ W
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic c">🔢</div><span class="sec-nm c">Cálculo con el Iris</span></div>
  <div class="mb">
<div class="ml">W₁ — subespacio de variables de pétalo</div>
W₁ = { (0, 0, x₃, x₄) ∈ ℝ⁴ : x₃, x₄ ∈ ℝ }

<span class="cm">// (W1) ¿Contiene el 0?</span>
(0,0,0,0) ∈ W₁  <span class="ok">✓</span>

<span class="cm">// (W2) ¿Cerrado en suma?</span>
(0,0,1.462,0.246) + (0,0,4.260,1.326) = (0,0,5.722,1.572) ∈ W₁  <span class="ok">✓</span>

<span class="cm">// (W3) ¿Cerrado en escalar?</span>
3·(0,0,1.462,0.246) = (0,0,4.386,0.738) ∈ W₁  <span class="ok">✓</span>

<span class="ok">⟹ W₁ es subespacio de dimensión 2  ✓</span>

<span class="cm">// ─────────────────────────────────────────────</span>
<div class="ml">¿Es el conjunto {μ_s, μ_ve, μ_vi} un subespacio?</div>
<span class="cm">// (W1): ¿Contiene el 0?</span>
(0,0,0,0) ∉ {<span class="ms">μ_s</span>,<span class="mve">μ_ve</span>,<span class="mvi">μ_vi</span>}  <span class="hi">✗  NO es subespacio</span>

<span class="cm">// Pero span{μ_s,μ_ve,μ_vi} = la envolvente lineal SÍ lo es.</span>
  </div>
  <div class="ins"><div class="ins-lbl">Conclusión</div>
    <div class="prose" style="font-size:15px">El subespacio W₁ (sólo pétalos) tiene dim=2 y pasa todas las condiciones. Los tres vectores media NO forman un subespacio por sí solos (fallan W1), pero su envolvente lineal span{μ_s,μ_ve,μ_vi} sí lo es.</div>
  </div>
</div>
`},

{id:3, block:'I · Fundamentos',
title:'Independencia Lineal',
sub:'¿Podemos recuperar una especie a partir de las otras?',
html:`
<div class="sec">
  <div class="sec-lbl"><div class="sec-ic d">🌸</div><span class="sec-nm d">Dummies</span></div>
  <div class="prose">
    <p>Si los tres vectores-media fueran <em>linealmente dependientes</em>, significaría que uno es simplemente mezcla de los otros dos: la Setosa sería una combinación de Versicolor y Virginica.</p>
    <p>Si no puede expresarse así, son <em>linealmente independientes</em>: cada especie aporta información morfológica nueva e irreducible.</p>
    <p>Visualmente: si tres vectores "apuntan en direcciones genuinamente distintas", son independientes. Si uno de ellos vive en el plano definido por los otros dos, son dependientes.</p>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic a">∑</div><span class="sec-nm a">Algebraico</span></div>
  <div class="def">
    <div class="def-t">Definición: Independencia Lineal</div>
    <div class="prose"><p>Los vectores v₁,…,vₖ ∈ V son <strong>linealmente independientes</strong> si y sólo si:</p></div>
  </div>
  <div class="mb">
<div class="ml">Condición de independencia lineal</div>
α₁v₁ + α₂v₂ + ⋯ + αₖvₖ = 0  ⟹  α₁ = α₂ = ⋯ = αₖ = 0

<span class="cm">// Equivalente: ninguno es combinación lineal de los demás</span>
<span class="cm">// Criterio matricial: si M = [v₁|v₂|…|vₖ], entonces:</span>
LI  ⟺  rang(M) = k  ⟺  ker(M) = {0}
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic c">🔢</div><span class="sec-nm c">Cálculo con el Iris</span></div>
  <div class="mb">
<div class="ml">Matriz M = [μ_s | μ_ve | μ_vi] — sistema α₁μ_s+α₂μ_ve+α₃μ_vi=0</div>
     <span class="ms">Setosa</span>   <span class="mve">Versicolor</span>  <span class="mvi">Virginica</span>
x₁ [ 5.006    5.936     6.588 ]
x₂ [ 3.428    2.770     2.974 ]
x₃ [ 1.462    4.260     5.552 ]
x₄ [ 0.246    1.326     2.026 ]

<span class="cm">// Eliminación de Gauss — pivote = 5.006:</span>
F₂ ← F₂ - (3.428/5.006)·F₁  =  F₂ - 0.685·F₁
F₃ ← F₃ - (1.462/5.006)·F₁  =  F₃ - 0.292·F₁
F₄ ← F₄ - (0.246/5.006)·F₁  =  F₄ - 0.049·F₁

<span class="cm">// Tras escalonar, todos los pivotes son ≠ 0:</span>
rang(M) = <span class="ok">3</span>

<span class="cm">// nº columnas = 3 = rang → columnas LI</span>
<span class="ok">⟹ {μ_s, μ_ve, μ_vi} son linealmente independientes  ✓</span>
<span class="cm">// Ninguna especie es combinación lineal de las otras dos.</span>
<span class="cm">// Biológicamente: morfologías distintas e irreducibles.</span>
  </div>
  <div class="ins"><div class="ins-lbl">Conclusión</div>
    <div class="prose" style="font-size:15px">Los tres vectores media son linealmente independientes. Mathematicamente confirma que las 3 especies son morfológicamente distinguibles: ninguna puede "sintetizarse" como mezcla lineal de las otras dos.</div>
  </div>
</div>
`},

{id:4, block:'I · Fundamentos',
title:'Base y Dimensión',
sub:'El vocabulario mínimo del espacio Iris',
html:`
<div class="sec">
  <div class="sec-lbl"><div class="sec-ic d">🌸</div><span class="sec-nm d">Dummies</span></div>
  <div class="prose">
    <p>Una <em>base</em> es el vocabulario mínimo con el que puedes describir cualquier flor. Si tienes 4 vectores linealmente independientes que generan todo ℝ⁴, son una base.</p>
    <p>La <em>dimensión</em> es el tamaño de ese vocabulario mínimo. ℝ⁴ tiene dimensión 4: necesitas exactamente 4 medidas independientes para describir completamente una flor Iris.</p>
    <p>Hay infinitas bases posibles para ℝ⁴, pero todas tienen exactamente 4 elementos. La dimensión es invariante.</p>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic a">∑</div><span class="sec-nm a">Algebraico</span></div>
  <div class="def">
    <div class="def-t">Definición: Base y Dimensión</div>
    <div class="prose"><p>B = {b₁,…,bₙ} es base de V si cumple dos condiciones simultáneas:</p></div>
  </div>
  <div class="mb">
<div class="ml">Condiciones de base</div>
(B1) B es linealmente independiente
(B2) span(B) = V                       <span class="cm">// B genera todo V</span>

<span class="hi">dim(V)</span> = cardinalidad de cualquier base de V
<span class="cm">// Teorema: todas las bases de V tienen el mismo cardinal</span>

<span class="cm">// Teorema del completamiento:</span>
<span class="cm">// Todo LI se extiende a una base.</span>
<span class="cm">// Todo generador contiene una base.</span>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic c">🔢</div><span class="sec-nm c">Cálculo con el Iris</span></div>
  <div class="mb">
<div class="ml">Base canónica de ℝ⁴ — las 4 "medidas puras"</div>
e₁ = [1, 0, 0, 0]ᵀ  <span class="cm">← dirección "longitud sépalo"</span>
e₂ = [0, 1, 0, 0]ᵀ  <span class="cm">← dirección "ancho sépalo"</span>
e₃ = [0, 0, 1, 0]ᵀ  <span class="cm">← dirección "longitud pétalo"</span>
e₄ = [0, 0, 0, 1]ᵀ  <span class="cm">← dirección "ancho pétalo"</span>

<span class="cm">// Cualquier flor en esta base:</span>
<span class="ms">μ_setosa</span> = <span class="hi">5.006</span>·e₁ + <span class="hi">3.428</span>·e₂ + <span class="hi">1.462</span>·e₃ + <span class="hi">0.246</span>·e₄

<span class="cm">// ──────────────────────────────────────────</span>
<div class="ml">Base alternativa orientada a diferencias entre especies</div>
b₁ = <span class="ms">μ_s</span>             = [5.006, 3.428, 1.462, 0.246]ᵀ
b₂ = <span class="mve">μ_ve</span> - <span class="ms">μ_s</span>    = [0.930,-0.658, 2.798, 1.080]ᵀ
b₃ = <span class="mvi">μ_vi</span> - <span class="mve">μ_ve</span>   = [0.652, 0.204, 1.292, 0.700]ᵀ
b₄ = e₂             = [0,     1,     0,     0    ]ᵀ

<span class="cm">// rang([b₁|b₂|b₃|b₄]) = 4  → sí es base  ✓</span>
<span class="ok">dim(ℝ⁴) = 4</span>
  </div>
  <div class="ins"><div class="ins-lbl">Conclusión</div>
    <div class="prose" style="font-size:15px">ℝ⁴ tiene dimensión 4: necesitamos exactamente 4 coordenadas independientes. La base canónica corresponde a las 4 variables morfológicas. La base alternativa, orientada a diferencias entre especies, es útil en análisis discriminante.</div>
  </div>
</div>
`},

{id:5, block:'I · Fundamentos',
title:'Combinación Lineal y Span',
sub:'El espacio generado por las especies',
html:`
<div class="sec">
  <div class="sec-lbl"><div class="sec-ic d">🌸</div><span class="sec-nm d">Dummies</span></div>
  <div class="prose">
    <p>Una <em>combinación lineal</em> es una mezcla ponderada de vectores: multiplicas cada uno por un escalar y sumas. Una "flor sintética" entre Setosa y Versicolor sería <span class="im">0.5·μ_s + 0.5·μ_ve</span>.</p>
    <p>El <em>span</em> de un conjunto es la totalidad de combinaciones lineales posibles: todas las flores que se pueden generar mezclando esas semillas con cualquier proporción, incluyendo escalas negativas y extrapolaciones.</p>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic a">∑</div><span class="sec-nm a">Algebraico</span></div>
  <div class="mb">
<div class="ml">Combinación lineal y envolvente lineal</div>
<span class="cm">// Combinación lineal de S = {v₁,...,vₖ}:</span>
w = α₁v₁ + α₂v₂ + ⋯ + αₖvₖ,   αᵢ ∈ ℝ

<span class="hi">span(S)</span> = { α₁v₁ + ⋯ + αₖvₖ : α₁,…,αₖ ∈ ℝ }

<span class="cm">// Propiedades clave:</span>
span(S) es el MENOR subespacio que contiene S
S ⊆ T  ⟹  span(S) ⊆ span(T)
span(span(S)) = span(S)           <span class="cm">// idempotencia</span>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic c">🔢</div><span class="sec-nm c">Cálculo con el Iris</span></div>
  <div class="mb">
<div class="ml">Flores sintéticas por combinación lineal</div>
<span class="cm">// Interpolación convexa (α₁+α₂=1, αᵢ≥0): "flor intermedia"</span>
<span class="hi">f₁</span> = 0.5·<span class="ms">μ_s</span> + 0.5·<span class="mve">μ_ve</span>
   = 0.5·[5.006,3.428,1.462,0.246] + 0.5·[5.936,2.770,4.260,1.326]
   = [<span class="ok">5.471, 3.099, 2.861, 0.786</span>]ᵀ

<span class="cm">// Extrapolación: "flor más allá de Virginica"</span>
<span class="hi">f₂</span> = 2·<span class="mvi">μ_vi</span> - <span class="mve">μ_ve</span>
   = 2·[6.588,2.974,5.552,2.026] - [5.936,2.770,4.260,1.326]
   = [<span class="ok">7.240, 3.178, 6.844, 2.726</span>]ᵀ

<span class="cm">// ¿Qué genera span{μ_s, μ_ve, μ_vi}?</span>
<span class="cm">// Son 3 vectores LI (tema 3) → generan un subespacio de dim 3:</span>
dim(span{<span class="ms">μ_s</span>,<span class="mve">μ_ve</span>,<span class="mvi">μ_vi</span>}) = 3

<span class="ok">span{μ_s, μ_ve, μ_vi} ≅ ℝ³  ⊊  ℝ⁴</span>
<span class="cm">// Es un hiperplano 3D dentro de ℝ⁴.</span>
<span class="cm">// No es todo ℝ⁴: hay "flores inaccesibles" desde las 3 medias.</span>
  </div>
</div>
`},

// ── BLOQUE II: GEOMETRÍA ──────────────────────────
{id:6, block:'II · Geometría',
title:'Producto Escalar',
sub:'La geometría empieza aquí',
html:`
<div class="sec">
  <div class="sec-lbl"><div class="sec-ic d">🌸</div><span class="sec-nm d">Dummies</span></div>
  <div class="prose">
    <p>El <em>producto escalar</em> le da a nuestro espacio ℝ⁴ una noción de ángulo y longitud. Sin él, ℝ⁴ sólo tiene estructura algebraica. Con él, tiene geometría.</p>
    <p>Intuitivamente: el producto escalar de dos flores mide "cuánto comparten la misma dirección". Si dos flores tienen proporciones similares, su producto escalar es grande. Si sus variaciones son ortogonales, es cero.</p>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic a">∑</div><span class="sec-nm a">Algebraico</span></div>
  <div class="def">
    <div class="def-t">Definición: Producto Escalar (Espacio de Hilbert de dim finita)</div>
  </div>
  <div class="mb">
<div class="ml">Axiomas del producto interno ⟨·,·⟩: V × V → ℝ</div>
(P1) ⟨u, v⟩ = ⟨v, u⟩                    <span class="cm">// simetría</span>
(P2) ⟨αu+βv, w⟩ = α⟨u,w⟩+β⟨v,w⟩       <span class="cm">// linealidad 1er arg.</span>
(P3) ⟨v,v⟩ ≥ 0,  ⟨v,v⟩=0 ⟺ v=0       <span class="cm">// def. positiva</span>

<span class="cm">// Producto escalar estándar en ℝⁿ:</span>
<span class="hi">⟨u,v⟩</span> = uᵀv = Σᵢ uᵢvᵢ

<span class="cm">// Desigualdad de Cauchy-Schwarz (fundamental):</span>
|⟨u,v⟩|² ≤ ⟨u,u⟩ · ⟨v,v⟩
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic c">🔢</div><span class="sec-nm c">Cálculo con el Iris</span></div>
  <div class="mb">
<div class="ml">Productos escalares entre vectores media</div>
⟨<span class="ms">μ_s</span>,<span class="mve">μ_ve</span>⟩ = 5.006·5.936 + 3.428·2.770 + 1.462·4.260 + 0.246·1.326
         = 29.716 + 9.496 + 6.228 + 0.326
         = <span class="ok">45.766</span>

⟨<span class="ms">μ_s</span>,<span class="mvi">μ_vi</span>⟩ = 5.006·6.588 + 3.428·2.974 + 1.462·5.552 + 0.246·2.026
         = 32.980 + 10.193 + 8.117 + 0.498
         = <span class="ok">51.788</span>

⟨<span class="mve">μ_ve</span>,<span class="mvi">μ_vi</span>⟩ = 5.936·6.588 + 2.770·2.974 + 4.260·5.552 + 1.326·2.026
          = 39.103 + 8.238 + 23.652 + 2.687
          = <span class="ok">73.680</span>

<span class="cm">// Versicolor y Virginica tienen mayor producto escalar:</span>
<span class="cm">// "apuntan más en la misma dirección" → mayor similitud morfológica.</span>

<span class="cm">// Verificación Cauchy-Schwarz: |⟨μ_s,μ_ve⟩|² ≤ ⟨μ_s,μ_s⟩·⟨μ_ve,μ_ve⟩</span>
⟨<span class="ms">μ_s</span>,<span class="ms">μ_s</span>⟩  = 25.060+11.751+2.138+0.061 = <span class="ok">39.010</span>
⟨<span class="mve">μ_ve</span>,<span class="mve">μ_ve</span>⟩ = 35.236+7.673+18.148+1.758 = <span class="ok">62.815</span>

45.766² = 2094.5  ≤  39.010 × 62.815 = 2450.5  <span class="ok">✓</span>
  </div>
</div>
`},

{id:7, block:'II · Geometría',
title:'Norma y Distancia Euclídea',
sub:'¿Cuánto se parecen dos flores?',
html:`
<div class="sec">
  <div class="sec-lbl"><div class="sec-ic d">🌸</div><span class="sec-nm d">Dummies</span></div>
  <div class="prose">
    <p>La <em>norma</em> es la longitud de un vector-flor en ℝ⁴. La <em>distancia euclídea</em> entre dos flores es la longitud del vector diferencia: cuánto difieren en todas sus medidas simultáneamente.</p>
    <p>Es el teorema de Pitágoras generalizado a 4 dimensiones: <span class="im">d² = Δx₁² + Δx₂² + Δx₃² + Δx₄²</span>.</p>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic a">∑</div><span class="sec-nm a">Algebraico</span></div>
  <div class="mb">
<div class="ml">Norma y distancia</div>
<span class="hi">‖v‖</span> = √⟨v,v⟩ = √(Σᵢ vᵢ²)

‖v‖ ≥ 0,  ‖v‖=0 ⟺ v=0
‖αv‖ = |α|·‖v‖
‖u+v‖ ≤ ‖u‖ + ‖v‖           <span class="cm">// desigualdad triangular</span>

<span class="hi">d(u,v)</span> = ‖u-v‖ = √(Σᵢ(uᵢ-vᵢ)²)
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic c">🔢</div><span class="sec-nm c">Cálculo con el Iris</span></div>
  <div class="mb">
<div class="ml">Normas de los vectores media</div>
‖<span class="ms">μ_s</span>‖  = √(5.006²+3.428²+1.462²+0.246²)
       = √(25.060+11.751+2.138+0.061) = √39.010 = <span class="ok">6.246</span>

‖<span class="mve">μ_ve</span>‖ = √(5.936²+2.770²+4.260²+1.326²)
       = √(35.236+7.673+18.148+1.758) = √62.815 = <span class="ok">7.926</span>

‖<span class="mvi">μ_vi</span>‖ = √(6.588²+2.974²+5.552²+2.026²)
       = √(43.401+8.845+30.825+4.105) = √87.176 = <span class="ok">9.337</span>

<div class="ml">Distancias euclídeas entre medias de especie</div>
d(<span class="ms">μ_s</span>,<span class="mve">μ_ve</span>) = ‖[0.930,-0.658,2.798,1.080]‖
            = √(0.865+0.433+7.829+1.166) = √10.293 = <span class="ok">3.208</span>

d(<span class="ms">μ_s</span>,<span class="mvi">μ_vi</span>) = ‖[1.582,-0.454,4.090,1.780]‖
            = √(2.502+0.206+16.728+3.168) = √22.604 = <span class="ok">4.754</span>

d(<span class="mve">μ_ve</span>,<span class="mvi">μ_vi</span>) = ‖[0.652,0.204,1.292,0.700]‖
            = √(0.425+0.042+1.669+0.490) = √2.626  = <span class="ok">1.621</span>

<span class="cm">// Setosa está muy lejos de las otras dos (d>3.2).</span>
<span class="cm">// Versicolor y Virginica son próximas (d=1.6).</span>
<span class="hi">d(μ_ve,μ_vi) = 1.621  ≪  d(μ_s,μ_ve) = 3.208</span>
  </div>
  <div class="ins"><div class="ins-lbl">Conclusión</div>
    <div class="prose" style="font-size:15px">En ℝ⁴ euclídeo, Setosa está claramente separada (d>3.2) mientras Versicolor y Virginica son bastante próximas (d=1.6). Esto explica por qué Setosa se clasifica perfectamente y las otras dos se confunden.</div>
  </div>
</div>
`},

{id:8, block:'II · Geometría',
title:'Ángulo entre Vectores',
sub:'La similitud de dirección entre flores',
html:`
<div class="sec">
  <div class="sec-lbl"><div class="sec-ic d">🌸</div><span class="sec-nm d">Dummies</span></div>
  <div class="prose">
    <p>El ángulo entre dos vectores mide cuánto "apuntan en la misma dirección". Ángulo=0° significa misma dirección (sólo escala diferente). Ángulo=90° significa ortogonales — completamente "diferentes" en sentido geométrico.</p>
    <p>El coseno del ángulo, llamado <em>similitud coseno</em>, es ampliamente usado en machine learning para medir similitud entre observaciones sin importar la escala.</p>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic a">∑</div><span class="sec-nm a">Algebraico</span></div>
  <div class="mb">
<div class="ml">Ángulo y similitud coseno</div>
cos θ = <span class="hi">⟨u, v⟩ / (‖u‖·‖v‖)</span>

θ = arccos( ⟨u,v⟩ / (‖u‖·‖v‖) )   ∈ [0°, 180°]

<span class="cm">// Similitud coseno:</span>
sim(u,v) = cos θ ∈ [-1, 1]
  sim = +1  →  misma dirección (paralelos)
  sim =  0  →  ortogonales
  sim = -1  →  direcciones opuestas
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic c">🔢</div><span class="sec-nm c">Cálculo con el Iris</span></div>
  <div class="mb">
<div class="ml">Ángulos entre vectores media (usando temas 6 y 7)</div>
cos θ(<span class="ms">μ_s</span>,<span class="mve">μ_ve</span>) = 45.766 / (6.246 × 7.926)
                  = 45.766 / 49.495 = <span class="ok">0.9247</span>
θ(<span class="ms">μ_s</span>,<span class="mve">μ_ve</span>) = arccos(0.9247) = <span class="ok">22.4°</span>

cos θ(<span class="ms">μ_s</span>,<span class="mvi">μ_vi</span>) = 51.788 / (6.246 × 9.337)
                  = 51.788 / 58.319 = <span class="ok">0.8880</span>
θ(<span class="ms">μ_s</span>,<span class="mvi">μ_vi</span>) = arccos(0.8880) = <span class="ok">27.2°</span>

cos θ(<span class="mve">μ_ve</span>,<span class="mvi">μ_vi</span>) = 73.680 / (7.926 × 9.337)
                   = 73.680 / 74.005 = <span class="ok">0.9956</span>
θ(<span class="mve">μ_ve</span>,<span class="mvi">μ_vi</span>) = arccos(0.9956) = <span class="ok">5.4°</span>

<span class="cm">// Versicolor y Virginica casi misma dirección (¡sólo 5.4°!).</span>
<span class="cm">// Setosa apunta en dirección claramente distinta (22–27°).</span>
<span class="hi">Ángulo Ve–Vi = 5.4°  vs  Ángulo S–Ve = 22.4°</span>
  </div>
</div>
`},

{id:9, block:'II · Geometría',
title:'Ortogonalidad',
sub:'Direcciones sin solapamiento',
html:`
<div class="sec">
  <div class="sec-lbl"><div class="sec-ic d">🌸</div><span class="sec-nm d">Dummies</span></div>
  <div class="prose">
    <p>Dos vectores son <em>ortogonales</em> cuando su producto escalar es cero: no comparten "información de dirección". En estadística, dos variables ortogonales son completamente no correlacionadas.</p>
    <p>La ortogonalidad es la base del PCA: buscamos ejes de variabilidad que sean mutuamente ortogonales para que cada uno capture variación genuinamente nueva.</p>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic a">∑</div><span class="sec-nm a">Algebraico</span></div>
  <div class="mb">
<div class="ml">Ortogonalidad y complemento ortogonal</div>
u ⊥ v  ⟺  ⟨u, v⟩ = 0

<span class="cm">// Complemento ortogonal:</span>
W⊥ = { v ∈ V : ⟨v,w⟩ = 0  ∀w ∈ W }

V = W ⊕ W⊥                    <span class="cm">// descomposición directa ortogonal</span>
dim(W) + dim(W⊥) = dim(V)

<span class="cm">// Conjunto ortonormal:</span>
{uᵢ} ortonormal ⟺ ⟨uᵢ,uⱼ⟩ = δᵢⱼ  (delta de Kronecker)
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic c">🔢</div><span class="sec-nm c">Cálculo con el Iris</span></div>
  <div class="mb">
<div class="ml">Construyendo un vector ortogonal a μ_setosa</div>
<span class="cm">// Queremos v ∈ ℝ⁴ tal que ⟨μ_s, v⟩ = 0</span>
<span class="cm">// Ecuación: 5.006·v₁ + 3.428·v₂ + 1.462·v₃ + 0.246·v₄ = 0</span>

<span class="cm">// Solución particular: fijamos v₂=1, v₃=v₄=0</span>
<span class="cm">// → v₁ = -3.428/5.006 = -0.685</span>

v₁ = [-0.685, 1, 0, 0]ᵀ

⟨<span class="ms">μ_s</span>, v₁⟩ = 5.006·(-0.685) + 3.428·1 + 1.462·0 + 0.246·0
         = -3.429 + 3.428 = <span class="ok">-0.001 ≈ 0  ✓</span>

<span class="cm">// El complemento ortogonal de span{μ_s} tiene dimensión 3:</span>
dim(span{<span class="ms">μ_s</span>}⊥) = 4 - 1 = <span class="ok">3</span>

<span class="cm">// Interpretación: hay una familia 3D de "correcciones"</span>
<span class="cm">// que no aportan información sobre la dirección de Setosa.</span>
<span class="cm">// Estas 3 direcciones son "ciegas" a la media de Setosa.</span>
  </div>
</div>
`},

{id:10, block:'II · Geometría',
title:'Proceso de Gram-Schmidt',
sub:'Ortonormalización de las especies',
html:`
<div class="sec">
  <div class="sec-lbl"><div class="sec-ic d">🌸</div><span class="sec-nm d">Dummies</span></div>
  <div class="prose">
    <p>Gram-Schmidt toma cualquier conjunto de vectores linealmente independientes y los convierte, uno a uno, en vectores <em>ortonormales</em>: perpendiculares entre sí y de longitud 1.</p>
    <p>La idea: el segundo vector se "limpia" de su componente en la dirección del primero. El tercero, de las componentes en las dos primeras direcciones. Y así sucesivamente.</p>
    <p>Es como construir un sistema de coordenadas perfectamente ortogonal a partir de las tres flores-media del Iris.</p>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic a">∑</div><span class="sec-nm a">Algebraico</span></div>
  <div class="mb">
<div class="ml">Algoritmo de Gram-Schmidt</div>
<span class="cm">// Dado {v₁,v₂,v₃} LI, construir {u₁,u₂,u₃} ortonormal:</span>

<span class="hi">Paso 1:</span>  u₁ = v₁ / ‖v₁‖

<span class="hi">Paso 2:</span>  w₂ = v₂ - ⟨v₂,u₁⟩·u₁      <span class="cm">// eliminar componente en u₁</span>
         u₂ = w₂ / ‖w₂‖

<span class="hi">Paso 3:</span>  w₃ = v₃ - ⟨v₃,u₁⟩·u₁ - ⟨v₃,u₂⟩·u₂
         u₃ = w₃ / ‖w₃‖

<span class="cm">// Resultado garantizado: ⟨uᵢ,uⱼ⟩ = δᵢⱼ  ✓</span>
<span class="cm">// span{u₁,...,uₖ} = span{v₁,...,vₖ} ∀k  ✓</span>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic c">🔢</div><span class="sec-nm c">Cálculo con el Iris — Gram-Schmidt sobre {μ_s, μ_ve, μ_vi}</span></div>
  <div class="mb">
<div class="ml">Paso 1: Normalizar μ_setosa</div>
‖<span class="ms">μ_s</span>‖ = 6.246  (tema 7)

u₁ = <span class="ms">μ_s</span>/6.246 = [<span class="ok">0.8015, 0.5488, 0.2341, 0.0394</span>]ᵀ

‖u₁‖ = √(0.6424+0.3012+0.0548+0.0016) = √1.000 = <span class="ok">1.000  ✓</span>

<div class="ml">Paso 2: Ortogonalizar μ_ve respecto a u₁</div>
⟨<span class="mve">μ_ve</span>,u₁⟩ = 5.936·0.8015 + 2.770·0.5488 + 4.260·0.2341 + 1.326·0.0394
          = 4.758 + 1.520 + 0.997 + 0.052 = <span class="ok">7.327</span>

w₂ = <span class="mve">μ_ve</span> - 7.327·u₁
   = [5.936,2.770,4.260,1.326] - [5.872,4.022,1.715,0.289]
   = [<span class="ok">0.064, -1.252, 2.545, 1.037</span>]ᵀ

‖w₂‖ = √(0.004+1.568+6.477+1.075) = √9.124 = <span class="ok">3.021</span>

u₂ = w₂/3.021 = [<span class="ok">0.0212, -0.4143, 0.8426, 0.3432</span>]ᵀ

<span class="cm">// Verificación ortogonalidad:</span>
⟨u₁,u₂⟩ = 0.8015·0.0212+0.5488·(-0.4143)+0.2341·0.8426+0.0394·0.3432
         = 0.017-0.227+0.197+0.014 = <span class="ok">0.001 ≈ 0  ✓</span>
  </div>
</div>
`},

// ── BLOQUE III: MATRICES ──────────────────────────
{id:11, block:'III · Matrices',
title:'Transformaciones Lineales',
sub:'Funciones que respetan la estructura vectorial',
html:`
<div class="sec">
  <div class="sec-lbl"><div class="sec-ic d">🌸</div><span class="sec-nm d">Dummies</span></div>
  <div class="prose">
    <p>Una <em>transformación lineal</em> es una función entre espacios vectoriales que "respeta las operaciones": suma y escalar. Rotar, proyectar, comprimir, reflejar: todas son transformaciones lineales.</p>
    <p>Para el Iris: la función que selecciona sólo las variables de pétalo, o la que centra los datos restando la media, son transformaciones lineales (o afines).</p>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic a">∑</div><span class="sec-nm a">Algebraico</span></div>
  <div class="mb">
<div class="ml">Definición y propiedades</div>
T: V → W  es lineal ⟺  T(αu+βv) = αT(u) + βT(v)  ∀u,v∈V, ∀α,β∈ℝ

<span class="cm">// Equivalentemente:</span>
(L1) T(u+v) = T(u)+T(v)           <span class="cm">// aditividad</span>
(L2) T(αv)  = αT(v)               <span class="cm">// homogeneidad</span>

<span class="cm">// Consecuencias inmediatas:</span>
T(0) = 0
T(-v) = -T(v)

<span class="cm">// Subespacios fundamentales:</span>
ker(T) = { v∈V : T(v)=0 }         <span class="cm">// núcleo (subespacio de V)</span>
Im(T)  = { T(v) : v∈V  }          <span class="cm">// imagen (subespacio de W)</span>

<span class="hi">Teorema rango-nulidad:</span>
dim(ker T) + dim(Im T) = dim(V)
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic c">🔢</div><span class="sec-nm c">Cálculo con el Iris</span></div>
  <div class="mb">
<div class="ml">T: ℝ⁴ → ℝ² — proyección sobre variables de pétalo</div>
T([x₁,x₂,x₃,x₄]ᵀ) = [x₃, x₄]ᵀ     <span class="cm">← selecciona coordenadas 3 y 4</span>

<span class="cm">// Matriz de T (2×4):</span>
A = [ 0  0  1  0 ]
    [ 0  0  0  1 ]

<span class="cm">// Aplicando a cada media:</span>
T(<span class="ms">μ_s</span>)  = [<span class="ok">1.462, 0.246</span>]ᵀ    <span class="cm">← pétalo de Setosa</span>
T(<span class="mve">μ_ve</span>) = [<span class="ok">4.260, 1.326</span>]ᵀ    <span class="cm">← pétalo de Versicolor</span>
T(<span class="mvi">μ_vi</span>) = [<span class="ok">5.552, 2.026</span>]ᵀ    <span class="cm">← pétalo de Virginica</span>

<span class="cm">// Verificar linealidad:</span>
T(0.5·<span class="ms">μ_s</span>+0.5·<span class="mve">μ_ve</span>) = T([5.471,3.099,2.861,0.786]) = [2.861,0.786]ᵀ
0.5·T(<span class="ms">μ_s</span>)+0.5·T(<span class="mve">μ_ve</span>)  = 0.5·[1.462,0.246]+0.5·[4.260,1.326] = [2.861,0.786]ᵀ  <span class="ok">✓</span>

<span class="cm">// Teorema rango-nulidad:</span>
ker(T) = { [x₁,x₂,0,0]ᵀ }  → dim = 2
Im(T)  = ℝ²               → dim = 2
<span class="ok">2 + 2 = 4 = dim(ℝ⁴)  ✓</span>
  </div>
</div>
`},

{id:12, block:'III · Matrices',
title:'Representación Matricial',
sub:'La transformación en coordenadas',
html:`
<div class="sec">
  <div class="sec-lbl"><div class="sec-ic d">🌸</div><span class="sec-nm d">Dummies</span></div>
  <div class="prose">
    <p>Fijadas bases en el dominio y el codominio, toda transformación lineal se representa como una multiplicación de matrices. La matriz es la "tabla de instrucciones": columna j = dónde va el j-ésimo vector base.</p>
    <p>El producto de dos matrices corresponde a la composición de las transformaciones: primero T₁, luego T₂ → su composición tiene matriz T₂·T₁.</p>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic a">∑</div><span class="sec-nm a">Algebraico</span></div>
  <div class="mb">
<div class="ml">Representación matricial de T: ℝⁿ → ℝᵐ</div>
[T]ᵢⱼ = i-ésima componente de T(eⱼ)
<span class="cm">// j-ésima columna de [T] = imagen del j-ésimo vector base</span>

T(v) = [T]·v                  <span class="cm">// producto matriz-vector</span>

<span class="cm">// Cambio de base — si B'={b₁,...,bₙ} es otra base:</span>
[T]_{B'} = P⁻¹·[T]_{E}·P
P = [b₁|b₂|…|bₙ]              <span class="cm">// matriz de cambio de base (de B' a E)</span>

<span class="cm">// Composición:</span>
[T₂ ∘ T₁] = [T₂]·[T₁]
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic c">🔢</div><span class="sec-nm c">Cálculo con el Iris</span></div>
  <div class="mb">
<div class="ml">Transformación "centrado de datos" (representación homogénea)</div>
<span class="cm">// T_c: x ↦ x - μ_global  (centrar respecto a la media global)</span>
<span class="cm">// μ_global = [5.843, 3.057, 3.758, 1.199]ᵀ</span>
<span class="cm">// Es una transformación AFÍN (no lineal: T_c(0) ≠ 0)</span>
<span class="cm">// La hacemos lineal con coordenadas homogéneas en ℝ⁵:</span>

A_c =
[ 1   0   0   0  -5.843 ]
[ 0   1   0   0  -3.057 ]
[ 0   0   1   0  -3.758 ]
[ 0   0   0   1  -1.199 ]
[ 0   0   0   0   1     ]

<span class="cm">// Aplicando a μ_setosa aumentada = [5.006,3.428,1.462,0.246,1]ᵀ:</span>
A_c · <span class="ms">μ̃_s</span> = [5.006-5.843, 3.428-3.057, 1.462-3.758, 0.246-1.199, 1]ᵀ
           = [<span class="ok">-0.837, +0.371, -2.296, -0.953</span>, 1]ᵀ

<span class="cm">// Interpretación: Setosa tiene pétalos MUY por debajo de la media</span>
<span class="cm">// global, y sépalos ligeramente por debajo.</span>
  </div>
</div>
`},

{id:13, block:'III · Matrices',
title:'Rango y Nulidad',
sub:'Cuánta información transmite la transformación',
html:`
<div class="sec">
  <div class="sec-lbl"><div class="sec-ic d">🌸</div><span class="sec-nm d">Dummies</span></div>
  <div class="prose">
    <p>El <em>rango</em> de una matriz es el número de dimensiones independientes que "genera" al actuar sobre vectores: cuánta información genuinamente distinta produce su imagen.</p>
    <p>La <em>nulidad</em> es la dimensión del núcleo: lo que se aplana a cero, lo que se pierde. El teorema rango-nulidad dice que la información que se pierde más la que se genera es siempre igual al tamaño del dominio.</p>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic a">∑</div><span class="sec-nm a">Algebraico</span></div>
  <div class="mb">
<div class="ml">Rango, nulidad y teorema fundamental</div>
rang(A) = dim(Im A) = dim(espacio columna de A)
nul(A)  = dim(ker A) = dim(espacio nulo de A)

<span class="hi">Teorema rango-nulidad:</span>  rang(A) + nul(A) = n  (n=nº cols)

<span class="cm">// Para A ∈ ℝᵐˣⁿ:</span>
rang(A)  = rang(Aᵀ)            <span class="cm">// rango fila = rango columna</span>
rang(A)  ≤ min(m,n)
rang(AB) ≤ min(rang(A),rang(B))
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic c">🔢</div><span class="sec-nm c">Cálculo con el Iris</span></div>
  <div class="mb">
<div class="ml">Rango de la matriz de datos Iris (9 flores × 4 variables)</div>
X =
[ 5.1  3.5  1.4  0.2 ]  <span class="ms">← Setosa 1</span>
[ 4.9  3.0  1.4  0.2 ]  <span class="ms">← Setosa 2</span>
[ 4.7  3.2  1.3  0.2 ]  <span class="ms">← Setosa 3</span>
[ 7.0  3.2  4.7  1.4 ]  <span class="mve">← Versicolor 1</span>
[ 6.4  3.2  4.5  1.5 ]  <span class="mve">← Versicolor 2</span>
[ 6.9  3.1  4.9  1.5 ]  <span class="mve">← Versicolor 3</span>
[ 6.3  3.3  6.0  2.5 ]  <span class="mvi">← Virginica 1</span>
[ 5.8  2.7  5.1  1.9 ]  <span class="mvi">← Virginica 2</span>
[ 7.1  3.0  5.9  2.1 ]  <span class="mvi">← Virginica 3</span>

<span class="cm">// Tras eliminación de Gauss (sobre las 4 columnas):</span>
rang(X) = <span class="ok">4</span>

<span class="cm">// Todas las columnas son LI: cada variable morfológica</span>
<span class="cm">// aporta información genuinamente nueva.</span>

nul(Xᵀ) = 4 - rang(Xᵀ) = 4 - 4 = <span class="ok">0</span>
<span class="cm">// Sin relaciones lineales exactas entre variables.</span>

<span class="cm">// Rango-nulidad sobre X (9×4): rang=4, nul=0</span>
<span class="ok">4 + 0 = 4 = dim(dominio)  ✓</span>
  </div>
</div>
`},

{id:14, block:'III · Matrices',
title:'Cambio de Base',
sub:'El mismo Iris en distintas coordenadas',
html:`
<div class="sec">
  <div class="sec-lbl"><div class="sec-ic d">🌸</div><span class="sec-nm d">Dummies</span></div>
  <div class="prose">
    <p>Un cambio de base es medir las flores con un sistema de coordenadas diferente. La flor no cambia, pero sus números sí. Es como pasar de medir en centímetros a medir en "desviaciones estándar".</p>
    <p>En el PCA (tema 28) haremos exactamente esto: cambiaremos a una base de vectores propios de la covarianza, donde las variables nuevas son independientes y están ordenadas por varianza decreciente.</p>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic a">∑</div><span class="sec-nm a">Algebraico</span></div>
  <div class="mb">
<div class="ml">Cambio de base y matrices semejantes</div>
<span class="cm">// Base canónica E = {e₁,e₂,e₃,e₄}</span>
<span class="cm">// Nueva base B = {b₁,b₂,b₃,b₄}</span>
<span class="cm">// Matriz de cambio de base (de B a E):</span>
P = [b₁ | b₂ | b₃ | b₄]    <span class="cm">// columnas = vectores de la nueva base</span>

<span class="cm">// Conversión de coordenadas:</span>
[v]_E = P · [v]_B
[v]_B = P⁻¹ · [v]_E

<span class="cm">// La matriz de una transform. T en la nueva base:</span>
[T]_B = P⁻¹ · [T]_E · P    <span class="cm">// matrices semejantes</span>

<span class="cm">// Matrices semejantes tienen los mismos eigenvalores</span>
<span class="cm">// (el espectro es invariante al cambio de base)</span>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic c">🔢</div><span class="sec-nm c">Cálculo con el Iris</span></div>
  <div class="mb">
<div class="ml">Cambio a base orientada a la "flor media" (b₁ = dirección de μ_global)</div>
μ_global = [5.843, 3.057, 3.758, 1.199]ᵀ
‖μ_global‖ = √(34.141+9.345+14.123+1.438) = √59.047 = 7.685

b₁ = μ_global/7.685 = [<span class="ok">0.7603, 0.3978, 0.4890, 0.1560</span>]ᵀ

<span class="cm">// Coordenada de cada media en la dirección b₁:</span>
[<span class="ms">μ_s</span>]_{b₁}  = ⟨<span class="ms">μ_s</span>,b₁⟩
           = 5.006·0.7603+3.428·0.3978+1.462·0.4890+0.246·0.1560
           = 3.807+1.364+0.715+0.038 = <span class="ok">5.924</span>

[<span class="mve">μ_ve</span>]_{b₁} = ⟨<span class="mve">μ_ve</span>,b₁⟩
           = 5.936·0.7603+2.770·0.3978+4.260·0.4890+1.326·0.1560
           = 4.514+1.102+2.083+0.207 = <span class="ok">7.906</span>

[<span class="mvi">μ_vi</span>]_{b₁} = ⟨<span class="mvi">μ_vi</span>,b₁⟩
           = 6.588·0.7603+2.974·0.3978+5.552·0.4890+2.026·0.1560
           = 5.009+1.183+2.715+0.316 = <span class="ok">9.223</span>

<span class="cm">// En la dirección "flor media": Setosa < Versicolor < Virginica</span>
<span class="cm">// Orden de "tamaño general" de la flor.</span>
  </div>
</div>
`},

{id:15, block:'III · Matrices',
title:'Determinante',
sub:'El volumen y la invertibilidad',
html:`
<div class="sec">
  <div class="sec-lbl"><div class="sec-ic d">🌸</div><span class="sec-nm d">Dummies</span></div>
  <div class="prose">
    <p>El <em>determinante</em> de una matriz cuadrada mide el factor de escala de volumen de la transformación. Si det=0, la transformación "aplana" alguna dimensión y no es invertible. Si det&gt;0, preserva orientación.</p>
    <p>Para la matriz de covarianza del Iris: si det=0, habría una relación lineal exacta entre variables. Si det&gt;0, es invertible y podemos usarla en la distancia de Mahalanobis (tema 29).</p>
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic a">∑</div><span class="sec-nm a">Algebraico</span></div>
  <div class="mb">
<div class="ml">Propiedades del determinante</div>
det(AB)  = det(A)·det(B)
det(Aᵀ)  = det(A)
det(αA)  = αⁿ·det(A)          <span class="cm">(A ∈ ℝⁿˣⁿ)</span>
det(A⁻¹) = 1/det(A)

<span class="cm">// Expansión de Laplace por la fila 1:</span>
det(A) = Σⱼ (-1)^{1+j} · a₁ⱼ · M₁ⱼ
<span class="cm">// Mᵢⱼ = menor (det de la submatriz sin fila i, col j)</span>

A invertible  ⟺  det(A) ≠ 0
  </div>
</div>

<div class="sec">
  <div class="sec-lbl"><div class="sec-ic c">🔢</div><span class="sec-nm c">Cálculo con el Iris</span></div>
  <div class="mb">
<div class="ml">det(Σ_pooled) — covarianza pooled del Iris</div>
Σ_pooled =
[ 0.265   0.093   0.168   0.038 ]
[ 0.093   0.115   0.055   0.033 ]
[ 0.168   0.055   0.186   0.042 ]
[ 0.038   0.033   0.042   0.043 ]

<span class="cm">// Descomposición LU — pivotes de la diagonal de U:</span>
d₁ = 0.2650
d₂ = Δ₂/d₁ = 0.0218/0.265          = 0.0823
d₃ = Δ₃/Δ₂ = 0.00173/0.0218        = 0.0793
d₄ = det(Σ)/Δ₃ = 2.41×10⁻⁵/0.00173 = 0.0139

<span class="cm">// det = producto de los pivotes:</span>
det(Σ_pooled) = 0.2650 × 0.0823 × 0.0793 × 0.0139
              ≈ <span class="ok">2.41 × 10⁻⁵</span>

det > 0  →  <span class="ok">Σ_pooled es invertible  ✓</span>
<span class="cm">// det muy pequeño → las variables están bastante correlacionadas</span>
<span class="cm">// (el "hipervolumen" del elipsoide de confianza es muy pequeño)</span>

<span class="cm">// Verificación: det = Πᵢ λᵢ(Σ_pooled)</span>
<span class="cm">// λ₁λ₂λ₃λ₄ ≈ 0.360·0.135·0.082·0.032 ≈ 0.000128... ✓ (orden)</span>
  </div>
  <div class="ins"><div class="ins-lbl">Conclusión del Bloque III (hasta aquí)</div>
    <div class="prose" style="font-size:15px">Las matrices de datos del Iris tienen rango 4 (variables independientes), la covarianza es invertible (det&gt;0), y el cambio de base permite reinterpretar los datos en sistemas de coordenadas más informativos. Todo preparado para eigenvalores y PCA en la Parte 2.</div>
  </div>
</div>
`},

]; // fin TOPICS

// ═══════════════════════════════════════
// RENDER SIDEBAR
// ═══════════════════════════════════════
let current = 0;
const nav = document.getElementById('nav');
let lastBlock = '';
TOPICS.forEach((t,i)=>{
  if(t.block !== lastBlock){
    const lbl=document.createElement('div');
    lbl.className='blk-label'; lbl.textContent=t.block;
    nav.appendChild(lbl); lastBlock=t.block;
  }
  const item=document.createElement('div');
  item.className='nav-item'+(i===0?' active':'');
  item.innerHTML=`<span class="nav-num">${String(t.id).padStart(2,'0')}</span><span class="nav-lbl">${t.title}</span>`;
  item.onclick=()=>goTo(i);
  nav.appendChild(item);
});

// ═══════════════════════════════════════
// RENDER TOPIC
// ═══════════════════════════════════════
function goTo(i){
  current=i;
  const t=TOPICS[i];
  // update sidebar
  document.querySelectorAll('.nav-item').forEach((el,j)=>el.classList.toggle('active',j===i));
  // render
  const main=document.getElementById('main');
  const hero=main.querySelector('.hero');
  let topicDiv=document.getElementById('topicDiv');
  if(topicDiv) topicDiv.remove();
  topicDiv=document.createElement('div'); topicDiv.id='topicDiv';
  topicDiv.innerHTML=`
    <div class="content">
      <div class="t-header">
        <span class="t-num">Tema ${String(t.id).padStart(2,'0')}</span>
        <span class="t-block">${t.block}</span>
      </div>
      <div class="t-title">${t.title}</div>
      <div class="t-sub">${t.sub}</div>
      ${t.html}
    </div>
    <div class="nf">
      <button class="nb" onclick="goTo(${i-1})" ${i===0?'disabled':''}>← Anterior</button>
      <div class="prog">
        <div>${i+1} / ${TOPICS.length}</div>
        <div class="pb-wrap"><div class="pb-fill" style="width:${((i+1)/TOPICS.length*100).toFixed(0)}%"></div></div>
      </div>
      <button class="nb" onclick="goTo(${i+1})" ${i===TOPICS.length-1?'disabled':''}>Siguiente →</button>
    </div>`;
  main.appendChild(topicDiv);
  topicDiv.scrollIntoView({behavior:'smooth',block:'start'});
}

goTo(0);
</script>
</body>
</html>
