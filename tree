<!doctype html>
<html lang="ru">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Схема мира</title>

  <style>
    :root{
      --text:#eaeaea;
      --muted:#b7b7b7;

      --border:rgba(255,255,255,.14);
      --shadow: 0 12px 35px rgba(0,0,0,.55);
      --radius: 14px;

      --line: rgba(220,220,220,.85);

      --MAIN_BG: #050607;
      --DETAIL_BG: #07090b;
    }

    *{box-sizing:border-box}
    body{
      margin:0;
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
      color:var(--text);
      min-height:100vh;
      background:#050607;
    }
    a{ color:inherit; }

    header{
      padding:14px 18px;
      display:flex;
      align-items:center;
      justify-content:space-between;
      border-bottom:1px solid rgba(255,255,255,.06);
      background:linear-gradient(to bottom, rgba(255,255,255,.04), transparent);
    }
    header .title{ font-weight:700; opacity:.95; }
    header .hint{ font-size:12px; color:var(--muted); }

    .app{ min-height:100vh; display:flex; flex-direction:column; }

    /* ===== MAIN ===== */
    #view-main{
      flex:1;
      overflow:auto;
      padding:18px;
      background: var(--MAIN_BG);
    }

    .canvas{
      position:relative;
      width:1600px;
      height:920px;
      margin:0 auto;
      border-radius:18px;
    }

    .lines{
      position:absolute;
      inset:0;
      width:100%;
      height:100%;
      pointer-events:none;
    }

    .node{
      position:absolute;
      width: 360px;
      min-height: 70px;
      padding:14px 16px;
      border:1px solid var(--border);
      border-radius: var(--radius);
      background:linear-gradient(180deg, rgba(255,255,255,.06), rgba(255,255,255,.03));
      box-shadow: var(--shadow);
      color:var(--text);
      cursor:pointer;
      user-select:none;

      display:flex;
      align-items:center;
      gap:12px;

      transition: transform .08s ease, border-color .12s ease, filter .12s ease;
    }
    .node:hover{
      transform: translateY(-1px);
      border-color: rgba(255,255,255,.28);
      filter: brightness(1.04);
    }
    .node:active{ transform: translateY(0px) scale(.995); }

    .node .icon{
      width:38px;
      height:38px;
      border-radius:12px;
      border:1px solid rgba(255,255,255,.14);
      object-fit:cover;
      background: rgba(255,255,255,.06);
      flex:0 0 auto;
    }
    .node .txt{ display:flex; flex-direction:column; gap:4px; min-width:0; }
    .node .big{ font-size:15px; font-weight:800; line-height:1.1; }
    .node .small{
      font-size:13px;
      color:var(--muted);
      line-height:1.2;
      white-space:nowrap;
      overflow:hidden;
      text-overflow:ellipsis;
      max-width: 270px;
    }

    /* ===== DETAIL ===== */
    #view-detail{
      flex:1;
      display:none;
      padding:18px;
      overflow:auto;
      background: var(--DETAIL_BG);
    }
    .detail-wrap{
      max-width: 980px;
      margin:0 auto;
      display:grid;
      gap:14px;
    }
    .backbar{
      display:flex;
      align-items:center;
      justify-content:space-between;
      gap:12px;
    }
    .btn{
      display:inline-flex;
      align-items:center;
      gap:10px;
      padding:10px 14px;
      border-radius: 12px;
      border:1px solid rgba(255,255,255,.14);
      background: rgba(255,255,255,.06);
      color:var(--text);
      cursor:pointer;
      text-decoration:none;
      width:max-content;
    }
    .btn:hover{ border-color: rgba(255,255,255,.28); background: rgba(255,255,255,.08); }

    .card{
      border:1px solid rgba(255,255,255,.12);
      border-radius: 16px;
      background:linear-gradient(180deg, rgba(255,255,255,.06), rgba(255,255,255,.03));
      box-shadow: var(--shadow);
      padding:16px;
    }

    .hero{
      display:flex;
      gap:14px;
      align-items:flex-start;
    }
    .cover{
      width:180px;
      height:130px;
      border-radius:16px;
      border:1px solid rgba(255,255,255,.14);
      object-fit:cover;
      background: rgba(255,255,255,.06);
      flex:0 0 auto;
    }
    .detail-title{
      font-size:22px;
      font-weight:850;
      margin:0 0 6px 0;
    }
    .detail-sub{
      margin:0;
      color:var(--muted);
    }

    .tags{ margin-top:8px; }
    .tag{
      display:inline-block;
      font-size:12px;
      color:var(--muted);
      border:1px solid rgba(255,255,255,.14);
      padding:6px 10px;
      border-radius:999px;
      margin:8px 8px 0 0;
      background:rgba(0,0,0,.22);
    }

    .grid2{
      display:grid;
      grid-template-columns: 1.2fr .8fr;
      gap:14px;
    }
    @media (max-width: 920px){
      .grid2{ grid-template-columns: 1fr; }
      .canvas{ width:1200px; }
      .hero{ flex-direction:column; }
      .cover{ width:100%; height:170px; }
    }

    .char-grid{ display:grid; gap:10px; }
    .char{
      display:flex;
      gap:10px;
      align-items:center;
      padding:10px;
      border-radius:14px;
      border:1px solid rgba(255,255,255,.12);
      background: rgba(0,0,0,.18);
    }
    .char img{
      width:52px;
      height:52px;
      border-radius:14px;
      border:1px solid rgba(255,255,255,.14);
      object-fit:cover;
      background: rgba(255,255,255,.06);
      flex:0 0 auto;
    }
    .char .name{ font-weight:800; }
    .char .note{ color:var(--muted); font-size:12px; margin-top:2px; }

    footer{
      padding:12px 18px;
      color:var(--muted);
      font-size:12px;
      border-top:1px solid rgba(255,255,255,.06);
      opacity:.9;
    }
  </style>
</head>

<body>
<div class="app">
  <header>
    <div class="title">Схема мира</div>
    <div class="hint">Кликни по блоку → откроется страница касты</div>
  </header>

  <!-- MAIN -->
  <main id="view-main">
    <div class="canvas" id="canvas">

      <svg class="lines" id="svgLines" viewBox="0 0 1600 920" preserveAspectRatio="none" aria-hidden="true">
        <defs>
          <marker id="arrow" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto">
            <path d="M 0 0 L 10 5 L 0 10 z" fill="rgba(220,220,220,.9)"></path>
          </marker>
        </defs>
      </svg>

      <!-- ===== УЗЛЫ (РАСКЛАДКА КАК НА ТВОЕЙ КАРТИНКЕ) ===== -->

      <!-- ЭФИР (центр сверху) -->
      <button class="node" data-id="aether" style="left:620px; top:40px;">
        <img class="icon" src="img/aether.png" alt="">
        <div class="txt">
          <div class="big">ЭФИР / Первотворение</div>
        </div>
      </button>

      <!-- СЛЕВА / СПРАВА ОТ ЭФИРА -->
      <button class="node" data-id="forces" style="left:250px; top:155px;">
        <img class="icon" src="img/forces.png" alt="">
        <div class="txt">
          <div class="big">Прямые дети-сущности</div>
          <div class="small">Мать-Природа, Смерть, Магия</div>
        </div>
      </button>

      <button class="node" data-id="elves" style="left:980px; top:155px;">
        <img class="icon" src="img/elves.png" alt="">
        <div class="txt">
          <div class="big">Прямые дети-существа</div>
          <div class="small">Люминэр &amp; другие эльфы</div>
        </div>
      </button>

      <!-- ЦЕНТР -->
      <button class="node" data-id="birth_beings" style="left:520px; top:295px;">
        <img class="icon" src="img/birth_beings.png" alt="">
        <div class="txt">
          <div class="big">Порождение Существ</div>
          <div class="small">от взаимодействия сил</div>
        </div>
      </button>

      <!-- СПРАВА ПОД ЭЛЬФАМИ -->
      <button class="node" data-id="birth_races" style="left:1120px; top:305px;">
        <img class="icon" src="img/birth_races.png" alt="">
        <div class="txt">
          <div class="big">Порождение Рас</div>
          <div class="small">высшие, лесные, ночные эльфы</div>
        </div>
      </button>

      <!-- СРЕДНИЙ РЯД -->
      <button class="node" data-id="magic" style="left:190px; top:440px;">
        <img class="icon" src="img/magic.png" alt="">
        <div class="txt">
          <div class="big">МАГИЯ</div>
          <div class="small">Сияющая Основа &amp; Дикий Поток</div>
        </div>
      </button>

      <button class="node" data-id="vampires" style="left:630px; top:440px;">
        <img class="icon" src="img/vampires.png" alt="">
        <div class="txt">
          <div class="big">Вампиры Нокторна</div>
          <div class="small">«Ошибка системы», Проклятие Пламени</div>
        </div>
      </button>

      <button class="node" data-id="morgots" style="left:1080px; top:440px;">
        <img class="icon" src="img/morgots.png" alt="">
        <div class="txt">
          <div class="big">Морготы</div>
          <div class="small">Некроманты, падшие слуги Смерти</div>
        </div>
      </button>

      <!-- НИЖНИЙ ЛЕВЫЙ КУСОК (СМЕЩЕН ЛЕВЕЕ И РАЗНЕСЕН) -->
      <button class="node" data-id="mages" style="left:40px; top:585px; width:320px;">
        <img class="icon" src="img/mages.png" alt="">
        <div class="txt">
          <div class="big">Маги</div>
          <div class="small">Неофит → Верховный Магистр</div>
        </div>
      </button>

      <button class="node" data-id="witches" style="left:390px; top:585px; width:320px;">
        <img class="icon" src="img/witches.png" alt="">
        <div class="txt">
          <div class="big">Ведьмы</div>
          <div class="small">Светлые и Тёмные</div>
        </div>
      </button>

      <button class="node" data-id="outcasts" style="left:720px; top:585px; width:320px;">
        <img class="icon" src="img/outcasts.png" alt="">
        <div class="txt">
          <div class="big">Изгои &amp; Хранители</div>
          <div class="small">Тёмные Ведьмы, Хранители Завесы</div>
        </div>
      </button>

      <!-- ПРАВО НИЗ (как на картинке) -->
      <button class="node" data-id="progenitors" style="left:1100px; top:700px; width:420px;">
        <img class="icon" src="img/progenitors.png" alt="">
        <div class="txt">
          <div class="big">Шесть Прародителей</div>
          <div class="small">Аль-Нарим, Морвенна, Касар, Сильра…</div>
        </div>
      </button>

      <button class="node" data-id="clans" style="left:1100px; top:815px; width:420px;">
        <img class="icon" src="img/clans.png" alt="">
        <div class="txt">
          <div class="big">Кланы, Гибриды</div>
          <div class="small">Фералы, Стефан Блэк</div>
        </div>
      </button>
    </div>
  </main>

  <!-- DETAIL -->
  <section id="view-detail">
    <div class="detail-wrap">
      <div class="backbar">
        <a class="btn" href="#/">← На главную</a>
      </div>

      <div class="card">
        <div class="hero">
          <img class="cover" id="detail-cover" alt="">
          <div style="min-width:0;">
            <h1 class="detail-title" id="detail-title"></h1>
            <p class="detail-sub" id="detail-sub"></p>
            <div class="tags" id="detail-tags"></div>
          </div>
        </div>
      </div>

      <div class="grid2">
        <div class="card">
          <h2 style="margin:0 0 10px 0;">Описание</h2>
          <div id="detail-desc" style="white-space:pre-wrap; line-height:1.55;"></div>
        </div>

        <div class="card">
          <h2 style="margin:0 0 10px 0;">Персонажи</h2>
          <div class="char-grid" id="detail-chars"></div>

          <hr style="border:none;border-top:1px solid rgba(255,255,255,.10); margin:14px 0;" />

          <h2 style="margin:0 0 10px 0;">Связи по схеме</h2>
          <div id="detail-links"></div>
        </div>
      </div>
    </div>
  </section>

  <footer>
   t.me/the_Black_Generation
  </footer>
</div>

<script>
  /* =========================
     ✅ ФОНЫ (меняй тут)
     ========================= */
  const MAIN_BG =
      'linear-gradient(rgba(0,0,0,.55), rgba(0,0,0,.75)), url("img/bg_main.png") center / cover no-repeat';
  const DETAIL_BG =
      'linear-gradient(rgba(0,0,0,.55), rgba(0,0,0,.75)), url("img/bg_detail.jpg") center / cover no-repeat';

  document.documentElement.style.setProperty('--MAIN_BG', MAIN_BG);
  document.documentElement.style.setProperty('--DETAIL_BG', DETAIL_BG);

  /* =========================
     ДАННЫЕ УЗЛОВ
     ========================= */
  const NODES = {
    aether: {
      title: "ЭФИР / Первотворение",
      subtitle: "Источник первичных сущностей и рас",
      cover: "img/cover_aether.jpg",
      tags: ["исток", "космогония"],
      description: "Здесь будет описание Эфира.",
      characters: [{name:"—", img:"img/char_placeholder.png", note:"добавь персонажа"}],
    },
    forces: {
      title: "Прямые дети-сущности",
      subtitle: "Мать-Природа, Смерть, Магия",
      cover: "img/cover_forces.jpg",
      tags: ["сущности", "силы"],
      description: "Здесь будет описание сущностей.",
      characters: [
        {name:"Мать-Природа", img:"img/char_placeholder.png", note:"роль/титул"},
        {name:"Смерть", img:"img/char_placeholder.png", note:"роль/титул"},
        {name:"Магия", img:"img/char_placeholder.png", note:"роль/титул"},
      ],
    },
    elves: {
      title: "Прямые дети-существа",
      subtitle: "Люминэр и другие эльфы",
      cover: "img/cover_elves.jpg",
      tags: ["перворождённые", "эльфы"],
      description: "Здесь будет описание первородных существ.",
      characters: [{name:"Люминэр", img:"img/char_placeholder.png", note:"описание"}],
    },
    birth_beings: {
      title: "Порождение Существ",
      subtitle: "от взаимодействия сил",
      cover: "img/cover_birth_beings.jpg",
      tags: ["генезис"],
      description: "Как силы создают новые существа.",
      characters: [],
    },
    birth_races: {
      title: "Порождение Рас",
      subtitle: "высшие, лесные, ночные эльфы",
      cover: "img/cover_birth_races.jpg",
      tags: ["расы"],
      description: "Описание рас и их отличий.",
      characters: [],
    },
    magic: {
      title: "МАГИЯ",
      subtitle: "Сияющая Основа и Дикий Поток",
      cover: "img/cover_magic.jpg",
      tags: ["магия", "источник"],
      description: "Описание магии и двух потоков.",
      characters: [],
    },
    mages: {
      title: "Маги",
      subtitle: "Неофит → Верховный Магистр",
      cover: "img/cover_mages.jpg",
      tags: ["орден", "академия"],
      description: "Описание иерархий и правил магов.",
      characters: [],
    },
    witches: {
      title: "Ведьмы",
      subtitle: "Светлые и Тёмные",
      cover: "img/cover_witches.jpg",
      tags: ["ковены", "поток"],
      description: "Описание ведьм и дверей Потока.",
      characters: [],
    },
    outcasts: {
      title: "Изгои & Хранители",
      subtitle: "Тёмные Ведьмы, Хранители Завесы",
      cover: "img/cover_outcasts.jpg",
      tags: ["завеса", "тайна"],
      description: "Описание хранителей и их задач.",
      characters: [
        {name:"Моргин", img:"img/char_placeholder.png", note:"хранитель/изгой"},
        {name:"Сильверст", img:"img/char_placeholder.png", note:"хранитель/изгой"},
        {name:"Эль Фаба", img:"img/char_placeholder.png", note:"хранитель/изгой"},
      ],
    },
    vampires: {
      title: "Вампиры Нокторна",
      subtitle: "«Ошибка системы», Проклятие Пламени",
      cover: "img/cover_vampires.jpg",
      tags: ["вампиры", "аномалия"],
      description: "Описание Нокторна и проклятия.",
      characters: [],
    },
    morgots: {
      title: "Морготы",
      subtitle: "Некроманты, падшие слуги Смерти",
      cover: "img/cover_morgots.jpg",
      tags: ["некромантия", "смерть"],
      description: "Описание морготов и их силы.",
      characters: [],
    },
    progenitors: {
      title: "Шесть Прародителей",
      subtitle: "Аль-Нарим, Морвенна, Касар, Сильра, Даррик, Элиадор",
      cover: "img/cover_progenitors.jpg",
      tags: ["прародители", "династии"],
      description: "Описание прародителей и их влияния.",
      characters: [],
    },
    clans: {
      title: "Кланы, Гибриды",
      subtitle: "Фералы, Стефан Блэк",
      cover: "img/cover_clans.jpg",
      tags: ["кланы", "гибриды"],
      description: "Описание кланов и гибридов.",
      characters: [],
    },
  };

  /* =========================
     СВЯЗИ (стрелки)
     ========================= */
  const EDGES = [
    ["aether","forces"],
    ["aether","elves"],
    ["forces","birth_beings"],
    ["elves","birth_races"],
    ["birth_beings","magic"],
    ["birth_beings","vampires"],
    ["birth_beings","morgots"],
    ["magic","mages"],
    ["magic","witches"],
    ["magic","outcasts"],
    ["vampires","progenitors"],
    ["progenitors","clans"],
  ];

  const canvas = document.getElementById("canvas");
  const svg = document.getElementById("svgLines");

  function rectInCanvas(el){
    const r = el.getBoundingClientRect();
    const c = canvas.getBoundingClientRect();
    return { x:r.left-c.left, y:r.top-c.top, w:r.width, h:r.height };
  }

  function anchors(el){
    const r = rectInCanvas(el);
    const cx = r.x + r.w/2;
    const cy = r.y + r.h/2;
    const pad = 10;
    return {
      top:    { x: cx,      y: r.y - pad },
      bottom: { x: cx,      y: r.y + r.h + pad },
      left:   { x: r.x-pad, y: cy },
      right:  { x: r.x+r.w+pad, y: cy },
      center: { x: cx,      y: cy },
      rect: r
    };
  }

  function clearEdges(){
    [...svg.querySelectorAll("path.edge")].forEach(p=>p.remove());
  }

  // Кубическая кривая
  function cubicPath(p0, c1, c2, p1){
    return `M ${p0.x} ${p0.y} C ${c1.x} ${c1.y}, ${c2.x} ${c2.y}, ${p1.x} ${p1.y}`;
  }

  // Отрисовка одной стрелки
  function drawOneEdge(fromId, toId){
    const fromEl = document.querySelector(`.node[data-id="${fromId}"]`);
    const toEl   = document.querySelector(`.node[data-id="${toId}"]`);
    if(!fromEl || !toEl) return;

    const A = anchors(fromEl);
    const B = anchors(toEl);

    // --- Стиль "как на картинке": выход из низа/центра, дуга в сторону, вход сверху ---
    let start, end, c1, c2;

    // Специальные ветвления как у тебя красным:
    if(fromId === "aether" && toId === "forces"){
      start = A.bottom;
      end   = B.top;
      c1 = { x: start.x - 220, y: start.y + 25 };
      c2 = { x: end.x + 120,   y: end.y - 55 };
    }
    else if(fromId === "aether" && toId === "elves"){
      start = A.bottom;
      end   = B.top;
      c1 = { x: start.x + 220, y: start.y + 25 };
      c2 = { x: end.x - 120,   y: end.y - 55 };
    }
    else if(fromId === "forces" && toId === "birth_beings"){
      start = A.bottom;
      end   = B.top;
      c1 = { x: start.x + 40,  y: start.y + 90 };
      c2 = { x: end.x - 140,   y: end.y - 90 };
    }
    else if(fromId === "elves" && toId === "birth_races"){
      start = A.bottom;
      end   = B.top;
      c1 = { x: start.x + 80,  y: start.y + 70 };
      c2 = { x: end.x - 40,    y: end.y - 70 };
    }
    else if(fromId === "birth_beings" && toId === "magic"){
      start = A.bottom;
      end   = B.top;
      // дуга влево, чтобы не лезла в вампиров
      c1 = { x: start.x - 320, y: start.y + 20 };
      c2 = { x: end.x + 140,   y: end.y - 80 };
    }
    else if(fromId === "birth_beings" && toId === "vampires"){
      start = A.bottom;
      end   = B.top;
      c1 = { x: start.x + 40,  y: start.y + 110 };
      c2 = { x: end.x - 40,    y: end.y - 110 };
    }
    else if(fromId === "birth_beings" && toId === "morgots"){
      start = A.bottom;
      end   = B.top;
      // длинная дуга вправо (как ты нарисовал)
      c1 = { x: start.x + 380, y: start.y + 10 };
      c2 = { x: end.x - 140,   y: end.y - 70 };
    }
    else if(fromId === "magic" && toId === "mages"){
      start = A.bottom;
      end   = B.top;
      c1 = { x: start.x - 260, y: start.y + 35 };
      c2 = { x: end.x + 90,    y: end.y - 70 };
    }
    else if(fromId === "magic" && toId === "witches"){
      start = A.bottom;
      end   = B.top;
      c1 = { x: start.x - 60,  y: start.y + 90 };
      c2 = { x: end.x + 40,    y: end.y - 90 };
    }
    else if(fromId === "magic" && toId === "outcasts"){
      start = A.bottom;
      end   = B.top;
      // дуга направо (как ты нарисовал), но повыше, чтобы не цеплять другие блоки
      c1 = { x: start.x + 260, y: start.y + 40 };
      c2 = { x: end.x - 140,   y: end.y - 80 };
    }
    else if(fromId === "vampires" && toId === "progenitors"){
      start = A.bottom;
      end   = B.top;
      // дуга вправо вниз, как у тебя к прародителям
      c1 = { x: start.x + 220, y: start.y + 80 };
      c2 = { x: end.x - 160,   y: end.y - 110 };
    }
    else if(fromId === "progenitors" && toId === "clans"){
      start = A.bottom;
      end   = B.top;
      c1 = { x: start.x, y: start.y + 90 };
      c2 = { x: end.x,   y: end.y - 90 };
    }
    else {
      // универсальный красивый вариант (на всякий)
      start = A.bottom;
      end   = B.top;
      const dx = end.x - start.x;
      const dy = end.y - start.y;
      c1 = { x: start.x + dx*0.35, y: start.y + Math.max(80, dy*0.35) };
      c2 = { x: end.x   - dx*0.35, y: end.y   - Math.max(80, dy*0.35) };
    }

    const d = cubicPath(start, c1, c2, end);
    const path = document.createElementNS("http://www.w3.org/2000/svg","path");
    path.setAttribute("d", d);
    path.setAttribute("fill","none");
    path.setAttribute("stroke","var(--line)");
    path.setAttribute("stroke-width","2");
    path.setAttribute("marker-end","url(#arrow)");
    path.setAttribute("class","edge");
    svg.appendChild(path);
  }

  function drawEdges(){
    clearEdges();
    EDGES.forEach(([a,b]) => drawOneEdge(a,b));
  }

  /* =========================
     РОУТИНГ
     ========================= */
  const viewMain = document.getElementById("view-main");
  const viewDetail = document.getElementById("view-detail");

  function parseRoute(){
    const h = location.hash || "#/";
    const id = h.replace(/^#\/?/, "").trim();
    return { id };
  }

  function showMain(){
    viewDetail.style.display = "none";
    viewMain.style.display = "block";
    document.title = "Схема мира";
  }

  function showDetail(id){
    const data = NODES[id];
    if(!data){ showMain(); return; }

    document.getElementById("detail-title").textContent = data.title;
    document.getElementById("detail-sub").textContent = data.subtitle || "";

    const cover = document.getElementById("detail-cover");
    cover.src = data.cover || "";
    cover.style.opacity = data.cover ? "1" : ".35";

    const tagsWrap = document.getElementById("detail-tags");
    tagsWrap.innerHTML = "";
    (data.tags || []).forEach(t=>{
      const span = document.createElement("span");
      span.className = "tag";
      span.textContent = t;
      tagsWrap.appendChild(span);
    });

    document.getElementById("detail-desc").textContent = data.description || "";

    const charsWrap = document.getElementById("detail-chars");
    charsWrap.innerHTML = "";
    const chars = data.characters || [];
    if(chars.length){
      chars.forEach(ch=>{
        const row = document.createElement("div");
        row.className = "char";

        const img = document.createElement("img");
        img.src = ch.img || "img/char_placeholder.png";
        img.alt = "";

        const txt = document.createElement("div");
        const nm = document.createElement("div");
        nm.className = "name";
        nm.textContent = ch.name || "Без имени";
        const note = document.createElement("div");
        note.className = "note";
        note.textContent = ch.note || "";

        txt.appendChild(nm);
        if(ch.note) txt.appendChild(note);

        row.appendChild(img);
        row.appendChild(txt);

        charsWrap.appendChild(row);
      });
    } else {
      charsWrap.innerHTML = `<div class="hint">Персонажей пока нет.</div>`;
    }

    const linksWrap = document.getElementById("detail-links");
    linksWrap.innerHTML = "";
    const related = EDGES
      .filter(([a,b]) => a===id || b===id)
      .map(([a,b]) => a===id ? b : a);

    if(related.length){
      const ul = document.createElement("ul");
      ul.style.margin = "0 0 0 18px";
      related.forEach(otherId=>{
        const li = document.createElement("li");
        li.style.margin = "6px 0";
        const a = document.createElement("a");
        a.href = `#/${otherId}`;
        a.textContent = NODES[otherId]?.title || otherId;
        li.appendChild(a);
        ul.appendChild(li);
      });
      linksWrap.appendChild(ul);
    } else {
      linksWrap.innerHTML = `<div class="hint">Нет связей.</div>`;
    }

    viewMain.style.display = "none";
    viewDetail.style.display = "block";
    document.title = data.title;
  }

  function renderRoute(){
    const { id } = parseRoute();
    if(!id){ showMain(); return; }
    showDetail(id);
  }

  // клики по блокам
  document.querySelectorAll(".node").forEach(btn=>{
    btn.addEventListener("click", ()=>{
      location.hash = `#/${btn.getAttribute("data-id")}`;
    });
  });

  window.addEventListener("hashchange", renderRoute);
  window.addEventListener("resize", drawEdges);

  window.addEventListener("load", ()=>{
    drawEdges();
    renderRoute();
  });
</script>
</body>
</html>
