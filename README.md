[index (2).html](https://github.com/user-attachments/files/34202215/index.2.html)
<!doctype html>
<html lang="es">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<title>Recetario</title>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:wght@600;700&family=Figtree:wght@400;500;600;700&family=IBM+Plex+Mono:wght@400;500&display=swap">
<style>
/* Tablero oscuro: título, pastillas, avisos, tarjetas de indicadores con borde de color,
   paneles con barras y tabla, y debajo la lista de recetas con su ficha. */
:root{
  --bg:#0C1220; --panel:#131B2E; --panel2:#1B2540; --ink:#F2F5FB; --muted:#98A3BD; --line:#232E48;
  --accent:#9C8CF7; --accent-ink:#0C1220; --hot:#F0443A; --red:#F0645A; --amber:#F4B63F; --green:#34D399; --gray:#8793AD;
  --money:#F4B63F; --danger:#FF8C80; --alert-bg:#3A1411; --alert-line:#8A2A22;
  --font-display:'Bricolage Grotesque','Figtree',system-ui,sans-serif;
  --font-body:'Figtree',system-ui,-apple-system,'Segoe UI',sans-serif;
  --font-num:'IBM Plex Mono',ui-monospace,Menlo,Consolas,monospace;
  color-scheme:dark;
}
@media (prefers-color-scheme: light){
  :root:not([data-theme="dark"]){
    --bg:#F3F5FA; --panel:#FFFFFF; --panel2:#EAEEF7; --ink:#121A2C; --muted:#5E6A84; --line:#D8DFEC;
    --accent:#6D56E8; --accent-ink:#FFFFFF; --hot:#D6281D; --red:#D63A2F; --amber:#B7790A; --green:#0E9F6E; --gray:#6B7690;
    --money:#9A5B00; --danger:#B42318; --alert-bg:#FDECEA; --alert-line:#F2B8B2;
    color-scheme:light;
  }
}
:root[data-theme="light"]{
  --bg:#F3F5FA; --panel:#FFFFFF; --panel2:#EAEEF7; --ink:#121A2C; --muted:#5E6A84; --line:#D8DFEC;
  --accent:#6D56E8; --accent-ink:#FFFFFF; --hot:#D6281D; --red:#D63A2F; --amber:#B7790A; --green:#0E9F6E; --gray:#6B7690;
  --money:#9A5B00; --danger:#B42318; --alert-bg:#FDECEA; --alert-line:#F2B8B2;
  color-scheme:light;
}
*{box-sizing:border-box}
body{
  background:var(--bg);color:var(--ink);font-family:var(--font-body);font-size:15px;line-height:1.45;
  padding-block:24px 56px;
  padding-left:max(16px,env(safe-area-inset-left,0px));
  padding-right:max(16px,env(safe-area-inset-right,0px));
}
button,input,select,textarea{font:inherit;color:inherit}
h1,h2,h3{margin:0;text-wrap:balance}
:focus-visible{outline:2px solid var(--accent);outline-offset:2px}
.app{max-width:1120px;margin:0 auto;display:flex;flex-direction:column;gap:16px}
.app>:empty{display:none}

/* encabezado */
.top{display:flex;flex-wrap:wrap;align-items:baseline;justify-content:space-between;gap:6px 20px}
.top h1{font-family:var(--font-display);font-size:28px;font-weight:700;letter-spacing:-0.01em}
.top h1 .hot{color:var(--hot)}
.status{font-size:13px;color:var(--muted);display:inline-flex;align-items:center;gap:8px}
.status::before{content:"";width:9px;height:9px;border-radius:50%;background:var(--green)}
.status[data-s="saving"]::before{background:var(--amber)}
.status[data-s="error"]{color:var(--danger)}
.status[data-s="error"]::before{background:var(--red)}

/* pastillas */
.pills-row{display:flex;flex-wrap:wrap;align-items:center;gap:10px 16px}
.pills{display:flex;flex-wrap:wrap;gap:10px}
.pill{background:var(--panel);border:1px solid var(--line);color:var(--ink);border-radius:99px;padding:10px 20px;cursor:pointer;font-size:15px}
.pill:hover{border-color:var(--accent)}
.pill[aria-selected="true"]{background:var(--ink);color:var(--bg);border-color:var(--ink);font-weight:600}
.hint{font-size:13.5px;color:var(--muted)}

/* aviso */
.alert{display:flex;flex-wrap:wrap;align-items:center;gap:8px 12px;background:var(--alert-bg);border:1px solid var(--alert-line);color:var(--danger);border-radius:10px;padding:12px 16px}
.alert b{font-size:17px}
.alert .btn{border-color:var(--danger);color:var(--danger);background:none}

/* indicadores */
.tiles{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:12px}
.tile{background:var(--panel);border:1px solid var(--line);border-left:4px solid var(--tc,var(--gray));border-radius:12px;padding:14px 16px;min-width:0}
.tl{font-size:13px;color:var(--muted)}
.tv{font-size:32px;font-weight:700;line-height:1.15;margin:4px 0 2px;font-variant-numeric:tabular-nums;overflow-wrap:anywhere}
.tv.sm{font-size:24px}
.ts{font-size:13px;color:var(--muted);overflow:hidden;text-overflow:ellipsis;white-space:nowrap}

/* paneles */
.panel{background:var(--panel);border:1px solid var(--line);border-radius:14px;padding:18px;min-width:0}
.panel>h3,.ph{font-size:13px;font-weight:700;letter-spacing:.1em;text-transform:uppercase;color:var(--ink);margin:0 0 14px;font-family:var(--font-body)}
.panels{display:grid;grid-template-columns:minmax(0,1.5fr) minmax(0,1fr);gap:16px;align-items:start}
.bars{display:flex;flex-direction:column;gap:10px}
.bar{display:grid;grid-template-columns:minmax(80px,170px) minmax(0,1fr) auto;gap:12px;align-items:center;font-size:14px}
.bar .bl{color:var(--muted);overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.track{background:var(--panel2);border-radius:5px;height:16px;overflow:hidden}
.fill{background:var(--accent);height:100%;border-radius:5px;min-width:6px}
.bar .bv{min-width:44px;text-align:right;font-variant-numeric:tabular-nums}
.tbl-wrap{overflow-x:auto}
.tbl{width:100%;border-collapse:collapse;font-size:14.5px;font-variant-numeric:tabular-nums}
.tbl th{font-weight:500;color:var(--muted);text-align:right;padding:8px 10px;border-bottom:1px solid var(--line);white-space:nowrap}
.tbl td{padding:10px;border-bottom:1px solid var(--line);text-align:right;white-space:nowrap}
.tbl th:first-child,.tbl td:first-child{text-align:left;padding-left:2px}
.tbl tr:last-child td{border-bottom:0}
.link{background:none;border:0;padding:0;cursor:pointer;text-align:left;font-weight:500;color:var(--ink)}
.link:hover{color:var(--accent);text-decoration:underline}
.pos{color:var(--green)}
.neg{color:var(--danger)!important}
.note{font-size:12.5px;color:var(--muted);margin-top:10px}
.empty{color:var(--muted);padding:20px 8px;text-align:center}

/* lista + ficha */
#main{display:grid;grid-template-columns:minmax(250px,320px) minmax(0,1fr);gap:16px;align-items:start}
.pane-list,.pane-detail{min-width:0}
.back{display:none}
.list-tools{display:flex;gap:8px}
.in{width:100%;min-width:0;background:var(--panel2);border:1px solid var(--line);border-radius:8px;padding:8px 10px;min-height:38px}
.in:focus{border-color:var(--accent)}
textarea.in{resize:vertical;min-height:110px;line-height:1.5}
.btn{background:var(--panel2);border:1px solid var(--line);border-radius:8px;padding:8px 14px;min-height:38px;cursor:pointer;font-weight:600;font-size:14px;white-space:nowrap}
.btn:hover{border-color:var(--accent)}
.btn.primary{background:var(--accent);border-color:var(--accent);color:var(--accent-ink)}
.btn.danger{color:var(--danger)}
.btn.small{min-height:30px;padding:4px 11px;font-size:13px}
.chips{display:flex;flex-wrap:wrap;gap:6px;margin:12px 0}
.chip{border:1px solid var(--line);background:none;border-radius:99px;padding:4px 12px;font-size:13px;cursor:pointer;color:var(--muted)}
.chip[aria-pressed="true"]{background:var(--ink);border-color:var(--ink);color:var(--bg)}
.banner{font-size:13px;background:var(--panel2);border-radius:8px;padding:10px 12px;margin-bottom:12px;display:flex;gap:10px;align-items:center;justify-content:space-between;flex-wrap:wrap}
.list{list-style:none;margin:0;padding:0;display:flex;flex-direction:column;gap:6px}
.item{width:100%;text-align:left;display:flex;justify-content:space-between;align-items:center;gap:12px;background:none;border:1px solid var(--line);border-radius:10px;padding:11px 13px;cursor:pointer}
.item:hover{border-color:var(--accent)}
.item[aria-current="true"]{border-color:var(--accent);background:var(--panel2)}
.item .n{font-weight:600;min-width:0;overflow-wrap:anywhere}
.item .m{font-size:12.5px;color:var(--muted);margin-top:2px}
.item .p{font-variant-numeric:tabular-nums;font-size:14px;color:var(--money);white-space:nowrap;font-weight:600}

.sheet{display:flex;flex-direction:column;gap:20px}
.d-head{display:flex;justify-content:space-between;align-items:flex-start;gap:12px;flex-wrap:wrap}
.d-actions{display:flex;gap:6px;flex-wrap:wrap}
.title-wrap{min-width:0}
.sheet h2{font-family:var(--font-display);font-size:28px;line-height:1.15;font-weight:700;overflow-wrap:anywhere}
.tags{display:flex;gap:6px;flex-wrap:wrap;margin-top:8px}
.tag{font-size:12.5px;background:var(--panel2);border-radius:99px;padding:3px 10px;color:var(--muted)}
.sheet h3{font-size:13px;text-transform:uppercase;letter-spacing:.1em;color:var(--ink);font-weight:700;margin-bottom:10px}
.cols{display:grid;grid-template-columns:minmax(0,1fr) minmax(0,1.3fr);gap:24px}
.ing-list{list-style:none;margin:0;padding:0}
.ing-list li{display:flex;justify-content:space-between;gap:12px;padding:8px 0;border-bottom:1px solid var(--line)}
.ing-list li:last-child{border-bottom:0}
.ing-list .q{font-variant-numeric:tabular-nums;color:var(--muted);white-space:nowrap}
.steps{margin:0;padding-left:22px;display:flex;flex-direction:column;gap:8px}
.notes{white-space:pre-wrap;color:var(--muted)}
.meta-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:12px}
label.f{display:flex;flex-direction:column;gap:4px;font-size:12.5px;color:var(--muted);min-width:0}
.title-in{font-family:var(--font-display);font-size:24px;font-weight:700}

.ing-edit{display:flex;flex-direction:column;gap:12px}
.ing{display:grid;grid-template-columns:minmax(0,1fr) 84px 92px 36px;gap:8px;align-items:center;padding-bottom:12px;border-bottom:1px solid var(--line)}
.ing .x{height:38px;border:1px solid var(--line);background:none;border-radius:8px;cursor:pointer;color:var(--muted);font-size:18px;line-height:1}
.ing .x:hover{color:var(--danger);border-color:var(--danger)}
.buy{grid-column:1 / -1;display:flex;align-items:center;flex-wrap:wrap;gap:6px 8px;font-size:13px;color:var(--muted)}
.buy .in{width:96px}
.buy .in.u{width:76px}
.buy .c{margin-left:auto;font-variant-numeric:tabular-nums;color:var(--money);font-size:13.5px;font-weight:600}
.mny{position:relative;display:inline-flex;align-items:center}
.mny>span{position:absolute;left:9px;color:var(--muted);font-size:13px;pointer-events:none}
.mny .in{padding-left:22px;text-align:right;font-variant-numeric:tabular-nums}

.ticket{background:var(--panel2);border-radius:12px;padding:18px;font-variant-numeric:tabular-nums}
.ticket h3{margin-bottom:12px}
.ln{display:flex;align-items:center;gap:8px;padding:5px 0;min-width:0}
.ln .l{flex:0 1 auto;min-width:0}
.ln .dots{flex:1 1 20px;border-bottom:1px dotted var(--muted);opacity:.5;transform:translateY(4px);min-width:12px}
.ln .v{flex:0 0 auto;text-align:right;font-family:var(--font-num)}
.ln .v .in{width:112px;font-family:var(--font-num);text-align:right;background:var(--panel)}
.ln .v .in.s{width:84px}
.ln.sum{font-weight:600;border-top:1px solid var(--line);margin-top:6px;padding-top:10px}
.ln.big .v{font-size:20px;color:var(--money);font-weight:500}
.ln .hint{font-size:12.5px}
.cost-table{width:100%;border-collapse:collapse;font-size:14px}
.cost-table td{padding:7px 0;border-bottom:1px solid var(--line);vertical-align:top}
.cost-table td:last-child{text-align:right;font-family:var(--font-num);color:var(--money);white-space:nowrap}
.cost-table td.q{color:var(--muted);white-space:nowrap;padding:7px 12px}
.cost-table .warn{font-size:12.5px;color:var(--danger)}

/* calculadora de precio */
.crow{display:flex;justify-content:space-between;align-items:center;gap:12px;padding:9px 0}
.crow .cl{min-width:0}
.crow .cv{font-family:var(--font-num);font-weight:500;white-space:nowrap}
.crow .in.s{width:110px;text-align:right;font-family:var(--font-num);background:var(--panel)}
.cres{margin-top:6px;padding-top:12px;border-top:1px solid var(--line)}
.crow.big .cl{font-weight:600}
.crow .sub{font-size:13px;color:var(--muted);margin-right:8px;font-weight:400}
.crow.big .cv{font-size:26px;color:var(--money)}
/* copia de seguridad */
.top-r{display:flex;align-items:center;gap:14px;flex-wrap:wrap}
#bkOut,#bkIn{font-family:var(--font-num);font-size:12.5px}
/* artículos */
.src{font-size:12.5px;color:var(--muted)}
.buy .in.art-sel{width:auto;max-width:100%;flex:1 1 220px}
.art-note{font-size:13.5px;color:var(--muted);margin:0 0 14px;max-width:80ch}
.art-tools{display:flex;flex-wrap:wrap;gap:8px;margin-bottom:6px}
.art-tools .in{max-width:340px}
.art{display:grid;grid-template-columns:minmax(0,2fr) minmax(0,1.5fr) 84px 92px 130px;gap:8px;align-items:center;padding:14px 0;border-bottom:1px solid var(--line)}
.art:last-child{border-bottom:0}
.art-meta{grid-column:1 / -1;display:flex;flex-wrap:wrap;align-items:center;gap:6px 14px;font-size:13px;color:var(--muted)}
.art-meta .unit{font-variant-numeric:tabular-nums;color:var(--money);font-weight:600}
.art-meta .old{color:var(--amber);font-weight:600}
.art-meta .none{color:var(--danger);font-weight:600}
.art-meta .in.url{flex:1 1 220px;width:auto;min-height:30px;padding:3px 9px;font-size:13px}
a.btn{text-decoration:none;display:inline-flex;align-items:center;color:var(--ink)}
@media (max-width:860px){
  .art{grid-template-columns:minmax(0,1fr) minmax(0,1fr) 84px}
  .art>:nth-child(1){grid-column:1 / -1}
}
@media (max-width:860px){
  .panels{grid-template-columns:minmax(0,1fr)}
  #main{grid-template-columns:minmax(0,1fr)}
  .app[data-view="list"] .pane-detail{display:none}
  .app[data-view="detail"] .pane-list,
  .app[data-view="detail"] .dash{display:none}
  .back{display:inline-flex;align-items:center}
  .cols{grid-template-columns:minmax(0,1fr);gap:20px}
  .top h1{font-size:24px}
}
@media (max-width:520px){
  .ing{grid-template-columns:minmax(0,1fr) 72px 82px 36px}
  .sheet h2{font-size:24px}
  .pill{padding:9px 16px;font-size:14px}
  .tv{font-size:28px}
  .bar{grid-template-columns:minmax(70px,110px) minmax(0,1fr) auto}
}
@media (prefers-reduced-motion:reduce){*{transition:none!important}}
</style>

<style>html{-webkit-text-size-adjust:100%}body{margin:0}img{max-width:100%}[hidden]{display:none!important}</style>
</head>
<body>
<div class="app" id="app" data-view="list">
  <header class="top">
    <h1><span class="hot">Recetario</span> · Tablero de recetas</h1>
    <div class="top-r"><span class="status" id="status" data-s="saving">Cargando…</span><button class="btn small" data-act="backup">Copia de seguridad</button></div>
  </header>
  <div class="pills-row">
    <nav class="pills" role="tablist" aria-label="Secciones">
      <button class="pill" role="tab" data-tab="costos" aria-selected="true">Costos y precios</button>
      <button class="pill" role="tab" data-tab="personal" aria-selected="false">Mis recetas</button>
      <button class="pill" role="tab" data-tab="articulos" aria-selected="false">Artículos y precios</button>
    </nav>
    <span class="hint dash" id="hint"></span>
  </div>
  <section class="panel" id="backupPanel" hidden aria-label="Copia de seguridad">
    <h3>Copia de seguridad</h3>
    <p class="art-note">Copiá este texto y guardalo en un archivo de notas. Para pasar tus recetas y precios a otro dispositivo, o a la página en GitHub, pegalo en el cuadro de abajo y tocá Restaurar.</p>
    <label class="f">Tu copia<textarea class="in" id="bkOut" readonly style="min-height:90px"></textarea></label>
    <div class="art-tools" style="margin-top:8px"><button class="btn" data-act="bkCopy">Copiar</button></div>
    <label class="f" style="margin-top:14px">Pegar una copia<textarea class="in" id="bkIn" style="min-height:90px"></textarea></label>
    <div class="art-tools" style="margin-top:8px;align-items:center"><button class="btn primary" data-act="bkRestore">Restaurar</button><span class="hint" id="bkMsg"></span></div>
  </section>
  <div class="alert dash" id="alert"></div>
  <section class="tiles dash" id="tiles" aria-label="Indicadores"></section>
  <section class="panels dash" id="panels"></section>
  <section class="panel art-panel" id="artPanel" hidden aria-label="Artículos y precios">
    <h3>Base de artículos</h3>
    <p class="art-note">Cargá lo que cuesta cada artículo en Jumbo. Las recetas toman el precio de acá y se recalculan solas. Los precios no se actualizan solos: cuando cambien en la web, corregí el número y queda anotada la fecha.</p>
    <div class="art-tools"><input class="in" id="aq" type="search" placeholder="Buscar artículo" aria-label="Buscar artículo"><button class="btn primary" data-act="addArt">+ Nuevo artículo</button></div>
    <div id="artList"></div>
  </section>
  <datalist id="dl-art"></datalist>
  <main id="main">
    <section class="panel pane-list" id="paneList" aria-label="Lista de recetas">
      <h3>Recetas</h3>
      <div class="list-tools">
        <input class="in" id="q" type="search" placeholder="Buscar receta o ingrediente" aria-label="Buscar">
        <button class="btn primary" id="addBtn" data-act="add">+ Nueva</button>
      </div>
      <div class="chips" id="chips"></div>
      <div id="banner"></div>
      <ul class="list" id="list"></ul>
    </section>
    <section class="panel pane-detail" id="paneDetail" aria-label="Detalle de la receta"><div id="detail"></div></section>
  </main>
</div>

<script>
(function(){
  var KEY='recetario-v1';
  var UNITS=['g','kg','ml','l','un','cda','cdita','taza'];
  var UN={g:['m',1],kg:['m',1000],ml:['v',1],l:['v',1000],cda:['v',15],cdita:['v',5],taza:['v',240],un:['u',1]};
  var CATS=['Tarta','Torta','Cookie','Alfajor','Petite'];
  var TIPOS=[['personal','Solo mis recetas'],['venta','Solo costos y precios'],['ambos','Las dos solapas']];

  var recipes=[], tab='costos', selId=null, editing=false, confirmDel=false, view='list';
  var q='', cat='', ready=false, onlyIssues=false;
  var articles=[], aq='', artOnly=false, artConfirm=null, bkConfirm=false;
  var ref=null, mode='local', saveTimer=null, saving=false, dirty=false;

  function $(s){return document.querySelector(s)}
  function esc(s){return String(s==null?'':s).replace(/[&<>"']/g,function(c){return {'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]})}
  function rid(){return Math.random().toString(36).slice(2,10)}
  function money(n){return isFinite(n)?'$ '+Math.round(n).toLocaleString('es-AR'):'—'}
  function num(n){return (+n).toLocaleString('es-AR',{maximumFractionDigits:2})}
  function pct(n){return isFinite(n)?Math.round(n*100)+' %':'—'}
  function val(v){return v==null?'':v}
  function wide(){return !window.matchMedia('(max-width:860px)').matches}
  function plural(n,a,b){return n===1?a:b}

  /* ---------- datos de ejemplo ---------- */
  function ing(n,c,u,pp,pc,pu){return {id:rid(),nombre:n,cant:c,unidad:u,pPrecio:0,pCant:pc||1,pUnidad:pu||'kg',art:''}}
  function examples(){
    return [
      {id:rid(),ejemplo:true,nombre:'Alfajores de maicena',categoria:'Alfajor',tipo:'ambos',cm:'N/A',porciones:24,otros:1500,margen:120,precio:null,
        ingredientes:[ing('Maicena',250,'g',3800,1,'kg'),ing('Harina 000',150,'g',1200,1,'kg'),ing('Manteca',120,'g',3500,200,'g'),ing('Azúcar',100,'g',1400,1,'kg'),ing('Huevos',3,'un',4200,12,'un'),ing('Dulce de leche',400,'g',3500,400,'g'),ing('Coco rallado',60,'g',1500,100,'g')],
        pasos:'Mezclar la manteca pomada con el azúcar y sumar los huevos.\nIncorporar la maicena, la harina y el polvo de hornear.\nEstirar la masa, cortar discos y hornear 10 minutos a 170 °C.\nUnir de a dos con dulce de leche y pasar los bordes por coco.',
        notas:'Los costos salen de la solapa Artículos y precios. Cargá ahí lo que pagás.'},
      {id:rid(),ejemplo:true,nombre:'Tarta de zapallitos',categoria:'Tarta',tipo:'personal',cm:'26',porciones:6,otros:0,margen:100,precio:null,
        ingredientes:[ing('Zapallitos',4,'un'),ing('Cebolla',1,'un'),ing('Huevos',3,'un'),ing('Queso cremoso',200,'g'),ing('Tapa de tarta',1,'un')],
        pasos:'Saltear la cebolla y los zapallitos en rodajas.\nBatir los huevos y mezclar con el queso.\nArmar la tarta sobre la tapa y hornear 35 minutos a 190 °C.',
        notas:''}
    ];
  }
  function art(n,m,c,u,url){return {id:rid(),nombre:n,marca:m||'',cant:c,unidad:u,precio:0,fecha:'',url:url||''}}
  function seedArticles(){
    return [
      art('Dulce de leche','La Serenísima Repostero',400,'g','https://www.jumbo.com.ar/dulce-de-leche-la-serenisima-repostero-400g/p'),
      art('Maicena','',1,'kg'),art('Harina 000','',1,'kg'),art('Manteca','',200,'g'),art('Azúcar','',1,'kg'),
      art('Huevos','Maple',12,'un'),art('Coco rallado','',100,'g'),art('Zapallitos','',1,'un'),
      art('Cebolla','',1,'un'),art('Queso cremoso','',1,'kg'),art('Tapa de tarta','',1,'un')
    ];
  }
  function newRecipe(){
    return {id:rid(),nombre:'',categoria:'Tarta',tipo:tab==='costos'?'venta':'personal',cm:'',porciones:'',otros:0,margen:100,precio:null,ingredientes:[],pasos:'',notas:''};
  }
  function normalize(d){
    var list=(d&&Array.isArray(d.recipes))?d.recipes:[];
    return list.map(function(r){
      r.ingredientes=Array.isArray(r.ingredientes)?r.ingredientes:[];
      r.ingredientes.forEach(function(i){if(!i.id)i.id=rid()});
      if(!r.id)r.id=rid();
      if(!r.tipo)r.tipo='personal';
      if(r.cm===undefined)r.cm=(r.tiempo?'':'');
      if(r.ejemplo){if(r.categoria==='Merienda')r.categoria='Alfajor';if(r.categoria==='Almuerzo')r.categoria='Tarta'}
      return r;
    });
  }

  /* ---------- cálculos ---------- */
  function norm(s){return String(s||'').toLowerCase().normalize('NFD').replace(/[̀-ͯ]/g,'').trim()}
  function findArt(i){
    var k;
    if(i.art){for(k=0;k<articles.length;k++)if(articles[k].id===i.art)return articles[k]}
    if(!(+i.pPrecio>0)){
      var n=norm(i.nombre);
      if(n)for(k=0;k<articles.length;k++)if(norm(articles[k].nombre)===n)return articles[k];
    }
    return null;
  }
  function ingCalc(i){
    var cant=+i.cant||0,a0=findArt(i),pP,pC,pU;
    if(a0){pP=+a0.precio||0;pC=+a0.cant||0;pU=a0.unidad}
    else{pP=+i.pPrecio||0;pC=+i.pCant||0;pU=i.pUnidad||i.unidad}
    if(!pP||!pC)return {cost:0,st:'precio',art:a0};
    var a=UN[i.unidad]||UN.un,b=UN[pU]||UN.un;
    if(a[0]!==b[0])return {cost:0,st:'unidades',art:a0};
    if(!cant)return {cost:0,st:'ok',art:a0};
    return {cost:(cant*a[1])/(pC*b[1])*pP,st:'ok',art:a0};
  }
  function isNA(v){return /^n\/?a$/i.test(String(v==null?'':v).trim())}
  function portions(r){var n=parseFloat(String(r.porciones==null?'':r.porciones).replace(',','.'));return n>0?n:1}
  function naTxt(v){v=String(v==null?'':v).trim();return v===''?'':(isNA(v)?'N/A':v)}
  function isCookie(r){return r.categoria==='Cookie'}
  function unidTxt(r){var v=naTxt(r.unidades);return v===''?'':(v==='N/A'?'Unidades: N/A':v+' un')}
  function cmTxt(r){if(isCookie(r))return unidTxt(r);var v=naTxt(r.cm);return v===''?'':(v==='N/A'?'Cm: N/A':v+' cm')}
  function unidades(r){var n=parseFloat(String(r.unidades==null?'':r.unidades).replace(',','.'));return n>0?n:0}
  function ppuTxt(c){return c.uni>0?money(c.pv/c.uni):'—'}
  function porTxt(r){var v=naTxt(r.porciones);return v===''?'':(v==='N/A'?'Porciones: N/A':'Porciones: '+v)}
  function loadData(d){
    recipes=normalize(d);
    if(d&&Array.isArray(d.articles)){articles=d.articles;return}
    articles=seedArticles();
    var had=recipes.some(function(r){return r.ejemplo});
    if(had){recipes=recipes.filter(function(r){return !r.ejemplo}).concat(examples())}
    scheduleSave();
  }
  function today(){var d=new Date(),p=function(n){return (n<10?'0':'')+n};return d.getFullYear()+'-'+p(d.getMonth()+1)+'-'+p(d.getDate())}
  function fmtDate(s){if(!s)return 'sin fecha';var p=s.split('-');return p[2]+'/'+p[1]+'/'+p[0]}
  function stale(a){return +a.precio>0&&a.fecha&&(Date.now()-new Date(a.fecha+'T12:00:00').getTime())>30*864e5}
  function artLabel(a){return [a.nombre,a.marca].filter(Boolean).join(' ')+' · '+num(a.cant)+' '+a.unidad+(+a.precio>0?' a '+money(a.precio):' (sin precio)')}
  function artUse(a){var n=0;recipes.forEach(function(r){if(r.ingredientes.some(function(i){var f=findArt(i);return f&&f.id===a.id}))n++});return n}
  function unitPrice(a){
    var p=+a.precio||0,c=+a.cant||0,u=UN[a.unidad]||UN.un;
    if(!p||!c)return '';
    if(u[0]==='m')return money(p/(c*u[1])*1000)+' por kg';
    if(u[0]==='v')return money(p/(c*u[1])*1000)+' por litro';
    return money(p/c)+' por unidad';
  }
  function artOpts(sel){
    return '<option value="">Precio manual</option>'+articles.slice().sort(function(a,b){return (a.nombre||'zzz').localeCompare(b.nombre||'zzz','es')}).map(function(a){
      return '<option value="'+esc(a.id)+'"'+(a.id===sel?' selected':'')+'>'+esc([a.nombre,a.marca].filter(Boolean).join(' ')+' · '+num(a.cant)+' '+a.unidad)+'</option>';
    }).join('');
  }
  function calc(r){
    var ing=0;
    var rows=(r.ingredientes||[]).map(function(i){var c=ingCalc(i);ing+=c.cost;return c});
    var total=ing,por=portions(r),pp=total/por,margen=r.margen==null?100:+r.margen,unit=!isCookie(r)&&isNA(r.cm);
    var base=unit?pp:total,pv=Math.ceil(base*(1+margen/100)/10)*10,gan=pv-base;
    return {rows:rows,ing:ing,otros:0,total:total,pp:pp,sug:pv,pv:pv,gan:gan,real:pv>0?gan/pv:0,tanda:unit?gan*por:gan,pvTot:unit?pv*por:pv,por:por,unit:unit,cookie:isCookie(r),uni:unidades(r),custom:false};
  }

  /* ---------- guardado ---------- */
  function setStatus(s){
    var el=$('#status');
    var t={saving:'Guardando…',error:'No se pudo guardar',cuenta:'Guardado en tu cuenta',local:'Guardado en este navegador',load:'Cargando…'}[s]||'';
    el.textContent=t;el.dataset.s=(s==='saving'||s==='load')?'saving':(s==='error'?'error':'ok');
  }
  function payload(){return {v:2,recipes:recipes,articles:articles}}
  function localSave(){try{localStorage.setItem(KEY,JSON.stringify(payload()))}catch(e){}}
  function scheduleSave(){
    dirty=true;setStatus('saving');
    clearTimeout(saveTimer);saveTimer=setTimeout(flush,700);
  }
  function flush(){
    if(saving){saveTimer=setTimeout(flush,300);return}
    saving=true;dirty=false;localSave();
    var p=ref?ref.set(payload()):Promise.resolve();
    p.then(function(){setStatus(ref?'cuenta':'local')},function(){setStatus('error')}).then(function(){
      saving=false;if(dirty)scheduleSave();
    });
  }
  function touch(r){if(r&&r.ejemplo)delete r.ejemplo;scheduleSave()}

  function connect(){
    var done=function(){
      if(mode==='local'){
        try{var raw=localStorage.getItem(KEY);if(raw){loadData(JSON.parse(raw));ready=true;return}}catch(e){}
      }
    };
    var c=window.claude;
    if(!c||!c.use){done();return Promise.resolve()}
    return Promise.all([c.use('db'),c.use('user')]).then(function(a){
      var db=a[0],user=a[1];
      if(!db||!user)return null;
      return user.id().then(function(id){
        if(!id)return null;
        ref=db.collection('data/users/'+id).doc('recetario');
        return ref.get().then(function(s){
          mode='cuenta';
          if(s.exists){loadData(s.data());ready=true}
          else{
            try{var raw=localStorage.getItem(KEY);if(raw){loadData(JSON.parse(raw));ready=true;scheduleSave()}}catch(e){}
          }
        });
      });
    }).catch(function(){ref=null;mode='local'}).then(done);
  }

  /* ---------- estado derivado ---------- */
  function cur(){for(var i=0;i<recipes.length;i++)if(recipes[i].id===selId)return recipes[i];return null}
  function inTab(r){return r.tipo==='ambos'||(tab==='personal'?r.tipo==='personal':r.tipo==='venta')}
  function rowsTab(){return recipes.filter(inTab)}
  function hasIssue(r){
    if(tab==='personal')return !(r.pasos||'').trim();
    return r.ingredientes.length===0||calc(r).rows.some(function(x){return x.st!=='ok'});
  }
  function issueList(){return rowsTab().filter(hasIssue)}
  function visible(){
    var qq=q.trim().toLowerCase();
    return recipes.filter(function(r){
      if(r.id!==selId&&!inTab(r))return false;
      if(onlyIssues&&r.id!==selId&&!(inTab(r)&&hasIssue(r)))return false;
      if(cat&&r.categoria!==cat)return false;
      if(!qq)return true;
      if((r.nombre||'').toLowerCase().indexOf(qq)>=0)return true;
      return r.ingredientes.some(function(i){return (i.nombre||'').toLowerCase().indexOf(qq)>=0});
    }).sort(function(a,b){return (a.nombre||'zzz').localeCompare(b.nombre||'zzz','es')});
  }

  /* ---------- render: tablero ---------- */
  function tile(l,v,s,c,small){
    return '<div class="tile" style="--tc:var(--'+c+')"><div class="tl">'+l+'</div><div class="tv'+(small?' sm':'')+'">'+v+'</div><div class="ts">'+s+'</div></div>';
  }
  function barList(items,empty){
    if(!items.length)return '<div class="empty">'+empty+'</div>';
    var max=Math.max.apply(null,items.map(function(i){return i.v}))||1;
    return '<div class="bars">'+items.map(function(i){
      return '<div class="bar"><span class="bl" title="'+esc(i.l)+'">'+esc(i.l)+'</span><span class="track"><span class="fill" style="display:block;width:'+Math.max(2,Math.round(i.v/max*100))+'%"></span></span><span class="bv">'+esc(i.d)+'</span></div>';
    }).join('')+'</div>';
  }
  function avg(a){return a.length?a.reduce(function(s,x){return s+x},0)/a.length:null}

  function renderDash(){
    if(tab==='articulos'){renderArtDash();return}
    var list=rowsTab(),n=list.length,issues=issueList(),ni=issues.length;
    if(onlyIssues&&!ni)onlyIssues=false;
    var tiles='',panels='';
    if(tab==='personal'){
      var cats={},ings={},times=[];
      list.forEach(function(r){
        if(r.categoria)cats[r.categoria]=(cats[r.categoria]||0)+1;
        var seen={};
        r.ingredientes.forEach(function(i){var k=(i.nombre||'').trim().toLowerCase();if(k&&!seen[k]){seen[k]=1;ings[k]=ings[k]||{l:i.nombre.trim(),c:0};ings[k].c++}});
        var cmn=parseFloat(String(r.cm==null?'':r.cm).replace(',','.'));if(cmn>0&&!isCookie(r))times.push(cmn);
      });
      var catItems=Object.keys(cats).map(function(k){return {l:k,v:cats[k],d:String(cats[k])}}).sort(function(a,b){return b.v-a.v});
      var ingItems=Object.keys(ings).map(function(k){return {l:ings[k].l,v:ings[k].c,d:String(ings[k].c)}}).sort(function(a,b){return b.v-a.v}).slice(0,6);
      var at=avg(times);
      tiles=tile('Sin preparación',ni,'requieren carga','red')+
        tile('Recetas',n,'en esta solapa','accent')+
        tile('Categorías',catItems.length,'en uso','amber')+
        tile('Ingredientes',Object.keys(ings).length,'distintos','gray')+
        tile('Medida promedio',at==null?'—':Math.round(at*10)/10+' cm','promedio ('+times.length+' '+plural(times.length,'receta','recetas')+')','green')+
        tile('También con costos',list.filter(function(r){return r.tipo==='ambos'}).length,'en las dos solapas','ink');
      panels='<div class="panel"><h3>Por categoría</h3>'+barList(catItems,'Todavía no hay recetas.')+'</div>'+
        '<div class="panel"><h3>Ingredientes más usados</h3>'+barList(ingItems,'Cargá ingredientes para verlos acá.')+'</div>';
      $('#hint').textContent=n+' '+plural(n,'receta','recetas')+' en esta solapa';
    } else {
      var cs=list.map(function(r){return {r:r,c:calc(r)}}).filter(function(x){return x.c.total>0});
      var apps=avg(cs.map(function(x){return x.c.total})),apv=avg(cs.map(function(x){return x.c.pvTot})),arl=avg(cs.map(function(x){return x.c.real}));
      var best=null;cs.forEach(function(x){if(!best||x.c.tanda>best.c.tanda)best=x});
      tiles=tile('Datos incompletos',ni,'requieren precios','red')+
        tile('Recetas con costos',n,'en esta solapa','accent')+
        tile('Costo promedio',apps==null?'—':money(apps),'promedio ('+cs.length+' '+plural(cs.length,'receta','recetas')+')','amber',true)+
        tile('Precio de venta',apv==null?'—':money(apv),'promedio por receta','ink',true)+
        tile('Margen real',arl==null?'—':pct(arl),'promedio sobre el precio','green')+
        tile('Mayor ganancia',best?money(best.c.tanda):'—',best?esc(best.r.nombre||'Sin nombre'):'ganancia por receta','gray',true);
      var rowsH=list.slice().sort(function(a,b){return (a.nombre||'zzz').localeCompare(b.nombre||'zzz','es')}).map(function(r){
        var c=calc(r),has=c.total>0;
        return '<tr><td><button class="link" data-act="sel" data-id="'+esc(r.id)+'">'+esc(r.nombre||'Sin nombre')+'</button></td><td>'+esc(naTxt(r.porciones)||'—')+'</td><td>'+(has?money(c.total):'—')+'</td><td>'+(has?money(c.pv)+(c.unit?' c/u':''):'—')+'</td><td class="'+(has?(c.gan<0?'neg':'pos'):'')+'">'+(has?money(c.gan)+(c.unit?' c/u':''):'—')+'</td><td class="'+(has&&c.gan<0?'neg':'')+'">'+(has?pct(c.real):'—')+'</td></tr>';
      }).join('');
      var w={};
      list.forEach(function(r){r.ingredientes.forEach(function(i,k){
        var key=(i.nombre||'').trim().toLowerCase(),x=ingCalc(i);
        if(!key||!x.cost)return;
        w[key]=w[key]||{l:i.nombre.trim(),v:0};w[key].v+=x.cost;
      })});
      var wItems=Object.keys(w).map(function(k){return {l:w[k].l,v:w[k].v,d:money(w[k].v)}}).sort(function(a,b){return b.v-a.v}).slice(0,6);
      panels='<div class="panel"><h3>Costos por receta</h3>'+(n?'<div class="tbl-wrap"><table class="tbl"><thead><tr><th>Receta</th><th>Porciones</th><th>Costo total</th><th>Precio</th><th>Ganancia</th><th>Margen</th></tr></thead><tbody>'+rowsH+'</tbody></table></div><div class="note">Precio y ganancia son de la receta completa. Con Cm N/A son por unidad (c/u). Tocá una receta para abrir su ficha.</div>':'<div class="empty">Todavía no hay recetas con costos.</div>')+'</div>'+
        '<div class="panel"><h3>Ingredientes que más pesan</h3>'+barList(wItems,'Cargá precios de compra para verlos acá.')+'<div class="note">Suma del costo de cada ingrediente en todas las recetas.</div></div>';
      $('#hint').textContent='Importes en pesos ($)';
    }
    $('#tiles').innerHTML=tiles;
    $('#panels').innerHTML=panels;
    var al='';
    if(ni){
      var what=tab==='personal'?plural(ni,'receta sin preparación cargada','recetas sin preparación cargada'):plural(ni,'receta con precios de compra o unidades sin completar','recetas con precios de compra o unidades sin completar');
      al=onlyIssues
        ?'<span>Mostrando solo las '+ni+' '+what+'.</span><button class="btn small" data-act="issues">Quitar filtro</button>'
        :'<span>⚠ Hay <b>'+ni+'</b> '+what+'.</span><button class="btn small" data-act="issues">Ver</button>'+(tab==='costos'?'<button class="btn small" data-act="goArt">Ir a artículos</button>':'');
    }
    $('#alert').innerHTML=al;
  }

  /* ---------- render: lista ---------- */
  function renderChips(){
    var present=[];
    recipes.filter(inTab).forEach(function(r){if(r.categoria&&present.indexOf(r.categoria)<0)present.push(r.categoria)});
    present.sort(function(a,b){return CATS.indexOf(a)-CATS.indexOf(b)});
    if(cat&&present.indexOf(cat)<0)cat='';
    var h='';
    if(present.length>1){
      h='<button class="chip" data-act="cat" data-v="" aria-pressed="'+(!cat)+'">Todas</button>'+
        present.map(function(c){return '<button class="chip" data-act="cat" data-v="'+esc(c)+'" aria-pressed="'+(cat===c)+'">'+esc(c)+'</button>'}).join('');
    }
    $('#chips').innerHTML=h;
  }
  function renderList(){
    renderChips();
    var hasEx=recipes.some(function(r){return r.ejemplo});
    $('#banner').innerHTML=hasEx?'<div class="banner"><span>Hay recetas de ejemplo. Editalas o borralas cuando quieras.</span><button class="btn small" data-act="clearEx">Borrar ejemplos</button></div>':'';
    var list=visible(),h='';
    if(!ready){h='<li class="empty">Cargando tu recetario…</li>'}
    else if(!list.length){
      h='<li class="empty">'+(recipes.filter(inTab).length?'No hay recetas con ese filtro.':(tab==='costos'?'Todavía no hay recetas con costos. Creá una con “+ Nueva” o pasá una de tus recetas a esta solapa desde su ficha.':'Todavía no hay recetas. Creá la primera con “+ Nueva”.'))+'</li>';
    } else {
      h=list.map(function(r){
        var c=calc(r),meta=[r.categoria,cmTxt(r)].filter(Boolean).join(' · ');
        var right=tab==='costos'?'<div class="p">'+(c.total>0?money(c.pv)+(c.unit?' c/u':''):'—')+'</div>':'';
        return '<li><button class="item" data-act="sel" data-id="'+esc(r.id)+'"'+(r.id===selId?' aria-current="true"':'')+'><div><div class="n">'+esc(r.nombre||'Sin nombre')+'</div><div class="m">'+esc(meta||'Sin categoría')+'</div></div>'+right+'</button></li>';
      }).join('');
    }
    $('#list').innerHTML=h;
  }

  /* ---------- render: ficha ---------- */
  function opts(list,sel){return list.map(function(o){var v=Array.isArray(o)?o[0]:o,l=Array.isArray(o)?o[1]:o;return '<option value="'+esc(v)+'"'+(v===sel?' selected':'')+'>'+esc(l)+'</option>'}).join('')}
  function qty(i){return num(i.cant||0)+' '+(i.unidad||'')}
  function field(label,id,f,v,type,extra){
    return '<label class="f">'+label+'<input class="in" id="'+id+'" data-f="'+f+'" type="'+(type||'text')+'" value="'+esc(val(v))+'" '+(extra||'')+'></label>';
  }
  function stText(st){return st==='precio'?'Falta el precio':(st==='unidades'?'Revisá las unidades':'')}

  function ticket(r,c){
    var h='<div class="ticket"><h3>Ficha de costos</h3><div class="src" style="margin:-4px 0 8px">'+(c.unit?'Cm: N/A · el precio y la ganancia se calculan por unidad':'El precio y la ganancia se calculan sobre la receta completa')+'</div>';
    if(!editing){
      h+='<table class="cost-table"><tbody>'+r.ingredientes.map(function(i,k){
        var x=c.rows[k];
        return '<tr><td>'+esc(i.nombre||'Ingrediente')+(x.art?'<div class="src">'+esc(artLabel(x.art))+'</div>':'')+(x.st!=='ok'?'<div class="warn">'+stText(x.st)+'</div>':'')+'</td><td class="q">'+esc(qty(i))+'</td><td>'+(x.st==='ok'?money(x.cost):'—')+'</td></tr>';
      }).join('')+'</tbody></table><div style="height:10px"></div>';
    }
    h+='<div class="crow"><span class="cl">Costo total</span><span class="cv" data-out="total">'+money(c.total)+'</span></div>'+
      '<div class="crow"><label class="cl" for="f-porciones-t">Porciones</label><input class="in s" id="f-porciones-t" data-f="porciones" type="text" inputmode="decimal" placeholder="N/A" value="'+esc(val(r.porciones))+'"></div>'+
      '<div class="crow"><label class="cl" for="f-margen">Margen (%)</label><input class="in s" id="f-margen" data-f="margen" type="number" inputmode="decimal" min="0" step="any" value="'+esc(val(r.margen==null?100:r.margen))+'"></div>'+
      (c.unit?'<div class="crow"><span class="cl">Costo por unidad</span><span class="cv" data-out="pp">'+money(c.pp)+'</span></div>':'')+'<div class="cres"><div class="crow big"><span class="cl">'+(c.unit?'Precio de venta por unidad':'Precio de venta')+'</span><span class="cv" data-out="sug">'+money(c.pv)+'</span></div>'+(c.cookie?'<div class="crow"><span class="cl">Precio por unidad</span><span class="cv" data-out="ppu">'+ppuTxt(c)+'</span></div>':'')+
      '<div class="crow"><span class="cl">Ganancia (%)</span><span class="cv"><span class="sub'+(c.gan<0?' neg':'')+'" data-out="gan">'+money(c.gan)+'</span> <span class="'+(c.gan<0?'neg':'')+'" data-out="real">'+pct(c.real)+'</span></span></div></div></div>';
    return h;
  }

  function ingEdit(r,c,costos){
    return '<div class="ing-edit">'+r.ingredientes.map(function(i,k){
      var x=c.rows[k];
      var row='<div class="ing"><input class="in" data-i="'+k+'" data-k="nombre" list="dl-art" value="'+esc(i.nombre)+'" placeholder="Ingrediente" aria-label="Ingrediente">'+
        '<input class="in" data-i="'+k+'" data-k="cant" type="number" inputmode="decimal" min="0" step="any" value="'+esc(val(i.cant))+'" placeholder="Cant." aria-label="Cantidad">'+
        '<select class="in" data-i="'+k+'" data-k="unidad" aria-label="Unidad">'+opts(UNITS,i.unidad)+'</select>'+
        '<button class="x" data-act="delIng" data-idx="'+k+'" aria-label="Quitar ingrediente" title="Quitar">×</button>';
      if(costos){
        row+='<div class="buy"><select class="in art-sel" data-i="'+k+'" data-k="art" aria-label="Artículo de la base">'+artOpts(i.art||(x.art?x.art.id:''))+'</select>'+(x.art?'':'<span>o lo compro a</span><span class="mny"><span>$</span><input class="in" data-i="'+k+'" data-k="pPrecio" type="number" inputmode="decimal" min="0" step="any" value="'+esc(val(i.pPrecio||''))+'" aria-label="Precio de compra"></span>'+
          '<span>por</span><input class="in" style="width:72px" data-i="'+k+'" data-k="pCant" type="number" inputmode="decimal" min="0" step="any" value="'+esc(val(i.pCant))+'" aria-label="Cantidad comprada"><select class="in u" data-i="'+k+'" data-k="pUnidad" aria-label="Unidad de compra">'+opts(UNITS,i.pUnidad||'kg')+'</select>')+
          '<span class="c" data-out="ic'+k+'">'+(x.st==='ok'?money(x.cost):stText(x.st))+'</span></div>';
      }
      return row+'</div>';
    }).join('')+'<div><button class="btn small" data-act="addIng">+ Agregar ingrediente</button></div></div>';
  }

  function renderDetail(){
    var el=$('#detail'),r=cur();
    $('#dl-art').innerHTML=articles.map(function(a){return '<option value="'+esc(a.nombre)+'">'}).join('');
    if(!r){
      el.innerHTML='<div class="empty">'+(ready?'Elegí una receta de la lista o creá una nueva.':'Cargando…')+'</div>';
      return;
    }
    var c=calc(r),costos=tab==='costos',h='<div class="sheet">';
    var actions=editing
      ?'<button class="btn primary" data-act="done">Listo</button>'
      :'<button class="btn" data-act="edit">Editar</button>';
    actions+='<button class="btn" data-act="dup">Duplicar</button>';
    actions+=confirmDel
      ?'<button class="btn danger" data-act="delYes">Sí, eliminar</button><button class="btn" data-act="delNo">Cancelar</button>'
      :'<button class="btn danger" data-act="del">Eliminar</button>';
    h+='<div class="d-head"><button class="btn small back" data-act="back">← Recetas</button><div class="d-actions">'+actions+'</div></div>';

    if(editing){
      h+='<label class="f">Nombre de la receta<input class="in title-in" id="f-nombre" data-f="nombre" value="'+esc(r.nombre)+'" placeholder="Ej: Bizcochuelo de naranja"></label>';
      h+='<div class="meta-grid">'+
        '<label class="f">Categoría<select class="in" id="f-categoria" data-f="categoria">'+opts(CATS.concat(CATS.indexOf(r.categoria)<0&&r.categoria?[r.categoria]:[]),r.categoria)+'</select></label>'+
        '<label class="f">Aparece en<select class="in" id="f-tipo" data-f="tipo">'+opts(TIPOS,r.tipo)+'</select></label>'+
        (r.categoria==='Cookie'?field('Unidades','f-unidades','unidades',r.unidades,'text','inputmode="decimal" placeholder="N/A"'):field('Cm','f-cm','cm',r.cm,'text','inputmode="decimal" placeholder="N/A"'))+
        field('Porciones','f-porciones','porciones',r.porciones,'text','inputmode="decimal" placeholder="N/A"')+
        '</div>';
    } else {
      h+='<div class="title-wrap"><h2>'+esc(r.nombre||'Sin nombre')+'</h2><div class="tags">'+
        (r.categoria?'<span class="tag">'+esc(r.categoria)+'</span>':'')+
        (cmTxt(r)?'<span class="tag">'+esc(cmTxt(r))+'</span>':'')+
        (porTxt(r)?'<span class="tag">'+esc(porTxt(r))+'</span>':'')+
        (r.tipo==='ambos'?'<span class="tag">En las dos solapas</span>':'')+
        (r.ejemplo?'<span class="tag">Ejemplo</span>':'')+'</div></div>';
    }

    if(editing){
      h+='<div><h3>Ingredientes</h3>'+ingEdit(r,c,costos)+'</div>';
      h+='<div class="cols"><label class="f"><h3 style="margin:0">Preparación (un paso por línea)</h3><textarea class="in" id="f-pasos" data-f="pasos" style="min-height:160px">'+esc(r.pasos)+'</textarea></label>'+
         '<label class="f"><h3 style="margin:0">Notas</h3><textarea class="in" id="f-notas" data-f="notas" style="min-height:160px">'+esc(r.notas)+'</textarea></label></div>';
      if(costos)h+=ticket(r,c);
    } else {
      var steps=(r.pasos||'').split('\n').map(function(s){return s.trim()}).filter(Boolean);
      h+='<div class="cols"><div><h3>Ingredientes</h3>'+(r.ingredientes.length?'<ul class="ing-list">'+r.ingredientes.map(function(i){return '<li><span>'+esc(i.nombre||'Ingrediente')+'</span><span class="q">'+esc(qty(i))+'</span></li>'}).join('')+'</ul>':'<div class="notes">Sin ingredientes todavía. Tocá Editar para agregarlos.</div>')+'</div>'+
         '<div><h3>Preparación</h3>'+(steps.length?'<ol class="steps">'+steps.map(function(s){return '<li>'+esc(s)+'</li>'}).join('')+'</ol>':'<div class="notes">Sin pasos cargados.</div>')+
         (r.notas?'<h3 style="margin-top:20px">Notas</h3><div class="notes">'+esc(r.notas)+'</div>':'')+'</div></div>';
      if(costos)h+=ticket(r,c);
    }
    h+='</div>';
    el.innerHTML=h;
  }

  function patch(){
    var r=cur();if(!r)return;
    var c=calc(r);
    function set(k,v){document.querySelectorAll('[data-out="'+k+'"]').forEach(function(e){e.textContent=v})}
    set('ing',money(c.ing));set('total',money(c.total));set('pp',money(c.pp));set('sug',money(c.sug));
    set('gan',money(c.gan));set('real',pct(c.real));set('tanda',money(c.tanda));set('ppu',ppuTxt(c));
    ['gan','real','tanda'].forEach(function(k){document.querySelectorAll('[data-out="'+k+'"]').forEach(function(e){e.classList.toggle('neg',c.gan<0)})});
    c.rows.forEach(function(x,k){set('ic'+k,x.st==='ok'?money(x.cost):stText(x.st))});
    var p=$('#f-precio');if(p)p.placeholder=c.sug;
    var hint=$('#priceHint');if(hint)hint.textContent=c.custom?'Precio fijado por vos.':'Se usa el precio sugerido.';
    if(!!c.custom!==!!document.querySelector('[data-act="useSug"]'))refreshDetailKeepFocus();
    renderDash();
    if(tab==='costos')renderList();
  }
  function refreshDetailKeepFocus(){
    var active=document.activeElement,id=active&&active.id,start=active&&active.selectionStart;
    renderDetail();
    if(id){var n=document.getElementById(id);if(n){n.focus();try{n.setSelectionRange(start,start)}catch(e){}}}
  }

  function renderAll(){
    document.querySelectorAll('.pill').forEach(function(b){b.setAttribute('aria-selected',String(b.dataset.tab===tab))});
    var isArt=tab==='articulos';
    $('#app').dataset.view=isArt?'list':view;
    $('#artPanel').hidden=!isArt;$('#main').hidden=isArt;$('#panels').hidden=isArt;
    renderDash();
    if(isArt){renderArt();return}
    renderList();renderDetail();
  }

  /* ---------- artículos ---------- */
  function renderArtDash(){
    var n=articles.length,sin=articles.filter(function(a){return !(+a.precio>0)}).length,old=articles.filter(stale).length;
    var used=articles.filter(function(a){return artUse(a)>0}).length;
    var last=articles.reduce(function(m,a){return a.fecha&&a.fecha>m?a.fecha:m},'');
    if(artOnly&&!sin)artOnly=false;
    $('#tiles').innerHTML=tile('Sin precio',sin,'falta cargar','red')+
      tile('Artículos',n,'en la base','accent')+
      tile('Para revisar',old,'precio de hace más de 30 días','amber')+
      tile('En uso',used,'en alguna receta','green')+
      tile('Última carga',last?fmtDate(last):'—','fecha del último precio','gray',true);
    $('#hint').textContent='Importes en pesos ($) · precios de Jumbo Argentina';
    var al='';
    if(sin){
      al=artOnly
        ?'<span>Mostrando solo los '+sin+' '+plural(sin,'artículo sin precio','artículos sin precio')+'.</span><button class="btn small" data-act="artOnly">Quitar filtro</button>'
        :'<span>⚠ Hay <b>'+sin+'</b> '+plural(sin,'artículo sin precio','artículos sin precio')+'. Sin precio, las recetas no pueden calcular el costo.</span><button class="btn small" data-act="artOnly">Ver</button>';
    }
    $('#alert').innerHTML=al;
  }
  function jumboSearch(a){
    var t=[a.nombre,a.marca].filter(Boolean).join(' ').trim();
    return a.url||('https://www.jumbo.com.ar/'+encodeURIComponent(t)+'?_q='+encodeURIComponent(t)+'&map=ft');
  }
  function artMeta(a){
    var u=unitPrice(a),st=stale(a),h='';
    h+=u?'<span class="unit" data-aout="unit">'+esc(u)+'</span>':'<span class="none" data-aout="unit">Sin precio</span>';
    h+='<span data-aout="fecha" class="'+(st?'old':'')+'">'+(+a.precio>0?'Actualizado '+fmtDate(a.fecha)+(st?' · revisar':''):'')+'</span>';
    var n=artUse(a);
    h+='<span>'+(n?'En '+n+' '+plural(n,'receta','recetas'):'Sin uso')+'</span>';
    return h;
  }
  function artRow(a){
    var conf=artConfirm===a.id;
    return '<div class="art" data-aid="'+esc(a.id)+'">'+
      '<input class="in" data-a="nombre" value="'+esc(a.nombre)+'" placeholder="Artículo (ej: Dulce de leche)" aria-label="Nombre del artículo">'+
      '<input class="in" data-a="marca" value="'+esc(a.marca)+'" placeholder="Marca y variedad" aria-label="Marca y variedad">'+
      '<input class="in" data-a="cant" type="number" inputmode="decimal" min="0" step="any" value="'+esc(val(a.cant))+'" placeholder="Cant." aria-label="Cantidad del envase">'+
      '<select class="in" data-a="unidad" aria-label="Unidad del envase">'+opts(UNITS,a.unidad)+'</select>'+
      '<span class="mny"><span>$</span><input class="in" data-a="precio" type="number" inputmode="decimal" min="0" step="any" value="'+esc(val(a.precio||''))+'" placeholder="Precio" aria-label="Precio en Jumbo"></span>'+
      '<div class="art-meta"><span data-ameta>'+artMeta(a)+'</span>'+
      '<input class="in url" data-a="url" value="'+esc(a.url)+'" placeholder="Link del producto en Jumbo (opcional)" aria-label="Link del producto">'+
      '<a class="btn small" href="'+esc(jumboSearch(a))+'" target="_blank" rel="noopener">'+(a.url?'Abrir en Jumbo':'Buscar en Jumbo')+'</a>'+
      (conf?'<button class="btn small danger" data-act="delArtYes" data-id="'+esc(a.id)+'">Sí, quitar</button><button class="btn small" data-act="delArtNo">Cancelar</button>':'<button class="btn small danger" data-act="delArt" data-id="'+esc(a.id)+'">Quitar</button>')+
      '</div></div>';
  }
  function renderArt(){
    var qq=norm(aq);
    var list=articles.filter(function(a){
      if(artOnly&&+a.precio>0)return false;
      return !qq||norm(a.nombre+' '+a.marca).indexOf(qq)>=0;
    }).sort(function(a,b){return (a.nombre||'zzz').localeCompare(b.nombre||'zzz','es')});
    $('#artList').innerHTML=list.length?list.map(artRow).join(''):'<div class="empty">'+(articles.length?'No hay artículos con ese filtro.':'Todavía no hay artículos. Sumá el primero con “+ Nuevo artículo”.')+'</div>';
  }
  function onArtInput(t){
    var row=t.closest('.art');if(!row)return;
    var a=null;for(var k=0;k<articles.length;k++)if(articles[k].id===row.dataset.aid)a=articles[k];
    if(!a)return;
    var f=t.dataset.a;
    if(f==='cant'||f==='precio'){a[f]=parse(t.value)||0;if(f==='precio')a.fecha=+a.precio>0?today():''}
    else a[f]=t.value;
    scheduleSave();
    var m=row.querySelector('[data-ameta]');if(m)m.innerHTML=artMeta(a);
    var lk=row.querySelector('a.btn');if(lk){lk.href=jumboSearch(a);lk.textContent=a.url?'Abrir en Jumbo':'Buscar en Jumbo'}
    renderArtDash();
  }

  /* ---------- eventos ---------- */
  var NUMF={otros:1,margen:1,precio:1};
  var NUMK={cant:1,pPrecio:1,pCant:1};
  function parse(v){if(v==='')return null;var n=parseFloat(String(v).replace(',','.'));return isFinite(n)?n:null}

  document.addEventListener('input',function(e){
    var t=e.target,r=cur();
    if(t&&t.dataset&&t.dataset.a){onArtInput(t);return}
    if(!r||!t||!t.dataset)return;
    if(t.dataset.f){
      var f=t.dataset.f;
      r[f]=NUMF[f]?parse(t.value):t.value;
      if(f==='nombre'||f==='categoria'||f==='tipo'||f==='cm')renderList();
      if(f==='porciones'){document.querySelectorAll('[data-f="porciones"]').forEach(function(e){if(e!==t)e.value=t.value})}
      touch(r);patch();
      if(f==='cm'||f==='categoria')refreshDetailKeepFocus();
    } else if(t.dataset.i!==undefined){
      var i=r.ingredientes[+t.dataset.i];if(!i)return;
      var k=t.dataset.k;
      i[k]=NUMK[k]?(parse(t.value)||0):t.value;
      touch(r);patch();
      if(k==='art'){var fa=findArt(i);if(fa&&!i.nombre)i.nombre=fa.nombre;renderDetail()}
      if(k==='nombre'&&q)renderList();
    }
  });
  $('#q').addEventListener('input',function(e){q=e.target.value;renderList()});
  $('#aq').addEventListener('input',function(e){aq=e.target.value;renderArt()});

  function select(id){selId=id;editing=false;confirmDel=false;view='detail';renderAll();
    if(wide()){var d=$('#paneDetail');if(d&&d.scrollIntoView)d.scrollIntoView({block:'start'})}else window.scrollTo(0,0)}
  function selectFirst(){
    var l=visible();selId=l.length?l[0].id:null;editing=false;confirmDel=false;
  }

  document.addEventListener('click',function(e){
    var tb=e.target.closest('.pill');
    if(tb){tab=tb.dataset.tab;cat='';onlyIssues=false;view='list';selectFirst();if(!wide())selId=null;renderAll();return}
    var b=e.target.closest('[data-act]');if(!b)return;
    var act=b.dataset.act,r=cur();
    switch(act){
      case 'sel':select(b.dataset.id);break;
      case 'cat':cat=b.dataset.v;renderList();break;
      case 'backup':
        var bp=$('#backupPanel');bp.hidden=!bp.hidden;
        if(!bp.hidden){$('#bkOut').value=JSON.stringify(payload());$('#bkIn').value='';$('#bkMsg').textContent='';bkConfirm=false}
        break;
      case 'bkCopy':
        var bo=$('#bkOut');bo.select();
        var done2=function(){$('#bkMsg').textContent='Copiado'};
        try{navigator.clipboard.writeText(bo.value).then(done2,function(){try{document.execCommand('copy');done2()}catch(e){}})}catch(e){try{document.execCommand('copy');done2()}catch(e2){}}
        break;
      case 'bkRestore':
        var txt=$('#bkIn').value.trim(),obj=null;
        try{obj=JSON.parse(txt)}catch(e){}
        if(!obj||!Array.isArray(obj.recipes)){$('#bkMsg').textContent='El texto no es una copia válida. Pegá la copia completa.';bkConfirm=false;break}
        if(!bkConfirm){bkConfirm=true;$('#bkMsg').textContent='Esto reemplaza todo lo que hay ahora ('+obj.recipes.length+' recetas). Tocá Restaurar otra vez para confirmar.';break}
        loadData(obj);ready=true;bkConfirm=false;editing=false;view='list';
        selectFirst();if(!wide())selId=null;
        scheduleSave();$('#backupPanel').hidden=true;renderAll();break;
      case 'goArt':tab='articulos';artConfirm=null;renderAll();window.scrollTo(0,0);break;
      case 'artOnly':artOnly=!artOnly;renderDash();renderArt();break;
      case 'addArt':
        aq='';artOnly=false;$('#aq').value='';
        articles.push({id:rid(),nombre:'',marca:'',cant:1,unidad:'kg',precio:0,fecha:'',url:''});
        scheduleSave();renderDash();renderArt();
        var ns=document.querySelectorAll('.art [data-a="nombre"]');if(ns.length)ns[ns.length-1].focus();break;
      case 'delArt':artConfirm=b.dataset.id;renderArt();break;
      case 'delArtNo':artConfirm=null;renderArt();break;
      case 'delArtYes':
        articles=articles.filter(function(x){return x.id!==b.dataset.id});
        artConfirm=null;scheduleSave();renderDash();renderArt();break;
      case 'issues':onlyIssues=!onlyIssues;renderDash();renderList();break;
      case 'back':view='list';editing=false;confirmDel=false;renderAll();break;
      case 'add':
        var n=newRecipe();recipes.push(n);selId=n.id;editing=true;confirmDel=false;view='detail';
        scheduleSave();renderAll();var nf=$('#f-nombre');if(nf)nf.focus();break;
      case 'edit':editing=true;confirmDel=false;renderDetail();break;
      case 'done':editing=false;renderAll();break;
      case 'dup':
        if(!r)break;
        var cp=JSON.parse(JSON.stringify(r));cp.id=rid();cp.nombre=(r.nombre||'Receta')+' (copia)';delete cp.ejemplo;
        cp.ingredientes.forEach(function(i){i.id=rid()});
        recipes.push(cp);selId=cp.id;editing=true;scheduleSave();renderAll();break;
      case 'del':confirmDel=true;renderDetail();break;
      case 'delNo':confirmDel=false;renderDetail();break;
      case 'delYes':
        recipes=recipes.filter(function(x){return x.id!==selId});
        confirmDel=false;editing=false;scheduleSave();
        selectFirst();if(!wide()){selId=null;view='list'}
        renderAll();break;
      case 'addIng':
        if(!r)break;
        r.ingredientes.push(ing('',null,'g',0,1,'kg'));touch(r);renderDetail();renderDash();
        var rows=document.querySelectorAll('.ing [data-k="nombre"]');if(rows.length)rows[rows.length-1].focus();break;
      case 'delIng':
        if(!r)break;
        r.ingredientes.splice(+b.dataset.idx,1);touch(r);renderDetail();renderDash();break;
      case 'useSug':
        if(!r)break;
        r.precio=null;touch(r);renderDetail();renderList();renderDash();break;
      case 'clearEx':
        recipes=recipes.filter(function(x){return !x.ejemplo});
        if(!cur())selectFirst();
        scheduleSave();renderAll();break;
    }
  });

  /* ---------- arranque ---------- */
  setStatus('load');
  renderAll();
  connect().then(function(){
    if(!ready){recipes=examples();articles=seedArticles();ready=true;if(mode!=='cuenta')mode='local'}
    selectFirst();
    if(!wide()){selId=null;view='list'}
    setStatus(mode==='cuenta'?'cuenta':'local');
    renderAll();
  });
})();
</script>

</body>
</html>
