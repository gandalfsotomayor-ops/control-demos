<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black">
<title>CONTROL DEMOS</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{height:100%}
body{
  background:#0c0e12;color:#e0e6f0;
  font-family:system-ui,-apple-system,sans-serif;
  max-width:480px;margin:0 auto;
  min-height:100vh;overflow-x:hidden;
  padding-bottom:70px;
}
button{cursor:pointer;border:none;background:none;font-family:inherit;-webkit-appearance:none}
input,select,textarea{font-family:inherit;-webkit-appearance:none;outline:none;border-radius:0}

/* COLORES */
:root{
  --bg:#0c0e12;--s1:#13171e;--s2:#1a1f28;--s3:#1f2530;
  --b1:#262d38;--b2:#303a48;
  --t1:#e0e6f0;--t2:#8a96a8;--t3:#445060;
  --green:#00cc7a;--gdim:rgba(0,204,122,.14);
  --yellow:#f0be30;--ydim:rgba(240,190,48,.14);
  --red:#ff2d50;--rdim:rgba(255,45,80,.14);
  --blue:#2d70ff;--bdim:rgba(45,112,255,.14);
}

/* TOPBAR */
.topbar{
  position:sticky;top:0;z-index:100;
  background:rgba(12,14,18,.97);
  backdrop-filter:blur(10px);-webkit-backdrop-filter:blur(10px);
  border-bottom:1px solid var(--b1);
  padding:12px 16px 10px;
  display:flex;align-items:center;justify-content:space-between;
}
.topbar-title{font-size:17px;font-weight:700;letter-spacing:2px;text-transform:uppercase}
.topbar-sub{font-size:10px;color:var(--t3);letter-spacing:.5px;margin-top:2px}

/* NAVBAR */
.navbar{
  position:fixed;bottom:0;left:50%;transform:translateX(-50%);
  width:100%;max-width:480px;
  background:rgba(19,23,30,.98);
  border-top:1px solid var(--b1);
  display:flex;z-index:200;
  padding-bottom:env(safe-area-inset-bottom,0);
}
.nav-item{
  flex:1;display:flex;flex-direction:column;align-items:center;
  padding:10px 4px 8px;color:var(--t3);font-size:9px;
  letter-spacing:.5px;text-transform:uppercase;gap:4px;
  border:none;background:none;cursor:pointer;transition:color .15s;
}
.nav-item svg{width:22px;height:22px;stroke:currentColor;fill:none;stroke-width:1.5}
.nav-item.active{color:var(--blue)}

/* SCREENS */
.screen{display:none;animation:fadein .2s ease}
.screen.active{display:block}
@keyframes fadein{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:translateY(0)}}

/* CARDS */
.card{
  background:var(--s1);border:1px solid var(--b1);
  border-radius:10px;padding:15px;
  cursor:pointer;transition:background .12s;
}
.card:active{background:var(--s2)}
.card.listo{border-left:3px solid var(--green)}
.card.riesgo{border-left:3px solid var(--yellow)}
.card.nolisto{border-left:3px solid var(--red)}

/* STATS */
.stats{display:grid;grid-template-columns:repeat(4,1fr);gap:8px;margin-bottom:14px}
.stat{background:var(--s1);border:1px solid var(--b1);border-radius:8px;padding:12px 8px;text-align:center}
.stat-n{font-size:26px;font-weight:700;line-height:1}
.stat-l{font-size:8px;color:var(--t2);letter-spacing:1px;text-transform:uppercase;margin-top:4px}

/* BADGES */
.badge{
  display:inline-flex;align-items:center;gap:4px;
  font-size:9px;font-weight:700;letter-spacing:1px;text-transform:uppercase;
  padding:4px 9px;border-radius:4px;
}
.badge.listo{background:var(--gdim);color:var(--green);border:1px solid rgba(0,204,122,.2)}
.badge.riesgo{background:var(--ydim);color:var(--yellow);border:1px solid rgba(240,190,48,.2)}
.badge.nolisto{background:var(--rdim);color:var(--red);border:1px solid rgba(255,45,80,.2)}
.badge.prestamo{background:var(--bdim);color:var(--blue);border:1px solid rgba(45,112,255,.2)}
.dot{width:6px;height:6px;border-radius:50%;display:inline-block}
.dot.listo{background:var(--green)}
.dot.riesgo{background:var(--yellow)}
.dot.nolisto{background:var(--red)}

/* FUEL */
.fuel{display:flex;gap:3px}
.fuel-s{height:7px;flex:1;border-radius:2px;background:var(--s2);border:1px solid var(--b1)}
.fuel-s.ok{background:var(--green);border-color:var(--green)}
.fuel-s.warn{background:var(--yellow);border-color:var(--yellow)}
.fuel-s.danger{background:var(--red);border-color:var(--red)}

/* BUTTONS */
.btn{
  display:inline-flex;align-items:center;justify-content:center;gap:6px;
  font-size:12px;font-weight:700;letter-spacing:1.5px;text-transform:uppercase;
  padding:13px 18px;border-radius:8px;transition:all .12s;cursor:pointer;border:none;
  font-family:inherit;
}
.btn:active{transform:scale(.97)}
.btn-primary{background:var(--blue);color:#fff}
.btn-ghost{background:transparent;color:var(--t2);border:1px solid var(--b2)}
.btn-ghost:active{background:var(--s2)}
.btn-danger{background:var(--rdim);color:var(--red);border:1px solid rgba(255,45,80,.25)}
.btn-full{width:100%}
.btn-sm{padding:9px 14px;font-size:10px}

/* CHIPS */
.chips{display:flex;flex-wrap:wrap;gap:6px}
.chip{
  font-size:11px;letter-spacing:.3px;text-transform:uppercase;
  padding:8px 14px;border-radius:20px;
  border:1px solid var(--b2);background:var(--s2);color:var(--t2);
  transition:all .12s;white-space:nowrap;cursor:pointer;
  font-family:inherit;-webkit-appearance:none;
}
.chip:active{transform:scale(.97)}
.chip.sel{background:var(--blue);color:#fff;border-color:var(--blue)}
.chip.sel-g{background:var(--green);color:#000;border-color:var(--green)}
.chip.sel-y{background:var(--yellow);color:#000;border-color:var(--yellow)}
.chip.sel-r{background:var(--red);color:#fff;border-color:var(--red)}

/* FORM */
.f-label{font-size:9px;color:var(--t2);letter-spacing:2px;text-transform:uppercase;margin-bottom:7px;display:block}
.f-input{
  width:100%;background:var(--s2);border:1px solid var(--b2);
  border-radius:8px;padding:13px 14px;color:var(--t1);font-size:15px;
  transition:border-color .15s;font-family:inherit;
}
.f-input:focus{border-color:var(--blue)}
.f-textarea{resize:none;min-height:72px}

/* DIVIDER */
.div{height:1px;background:var(--b1);margin:16px 0}

/* SECTION LABEL */
.slbl{font-size:9px;color:var(--t3);letter-spacing:2px;text-transform:uppercase;margin-bottom:10px}

/* DETAIL ROW */
.drow{display:flex;justify-content:space-between;align-items:center;padding:10px 0;border-bottom:1px solid var(--b1)}
.drow:last-child{border-bottom:none}
.dk{font-size:9px;color:var(--t3);letter-spacing:1px;text-transform:uppercase}
.dv{font-size:13px;font-weight:600}

/* VIN */
.vin{
  font-family:'Courier New',monospace;font-size:16px;font-weight:700;
  letter-spacing:4px;color:var(--blue);
  background:var(--s2);border:1px solid var(--b2);
  border-radius:6px;padding:8px 12px;display:inline-block;text-transform:uppercase;
}

/* ACTION TAG */
.atag{font-size:9px;font-weight:700;letter-spacing:1px;text-transform:uppercase;padding:4px 9px;border-radius:3px}
.at-lavado{background:var(--bdim);color:var(--blue)}
.at-gas{background:var(--ydim);color:var(--yellow)}
.at-acomodar{background:rgba(160,100,255,.14);color:#b47aff}
.at-ok{background:var(--gdim);color:var(--green)}

/* MODAL */
.overlay{
  display:none;position:fixed;inset:0;background:rgba(0,0,0,.85);
  z-index:500;align-items:flex-end;justify-content:center;
}
.overlay.open{display:flex;animation:fadein .2s ease}
.modal{
  background:var(--s1);border:1px solid var(--b2);
  border-radius:16px 16px 0 0;padding:22px 18px 44px;
  width:100%;max-width:480px;max-height:90vh;overflow-y:auto;
}
.modal-handle{width:36px;height:4px;border-radius:2px;background:var(--b2);margin:0 auto 18px}

/* TOAST */
.toast{
  position:fixed;bottom:88px;left:50%;transform:translateX(-50%) translateY(8px);
  background:var(--s2);border:1px solid var(--b2);
  border-radius:8px;padding:11px 20px;
  font-size:12px;font-weight:600;letter-spacing:.5px;
  color:var(--t1);opacity:0;transition:all .22s;
  z-index:999;white-space:nowrap;pointer-events:none;
}
.toast.show{opacity:1;transform:translateX(-50%) translateY(0)}

/* ALERT */
.alert-row{
  display:flex;gap:12px;align-items:flex-start;
  padding:14px;background:var(--s1);border:1px solid var(--b1);border-radius:8px;
}
.alert-ico{font-size:20px;flex-shrink:0}
.alert-title{font-size:13px;font-weight:700;margin-bottom:3px}
.alert-sub{font-size:10px;color:var(--t2);text-transform:uppercase;letter-spacing:.3px}

/* EMPTY */
.empty{display:flex;flex-direction:column;align-items:center;justify-content:center;padding:56px 20px;gap:10px;text-align:center}
.empty-ico{font-size:40px;opacity:.2}
.empty-title{font-size:15px;font-weight:700;letter-spacing:1.5px;text-transform:uppercase;color:var(--t2)}
.empty-sub{font-size:10px;color:var(--t3);letter-spacing:1px;text-transform:uppercase}

/* UTIL */
.px{padding-left:16px;padding-right:16px}
.pt{padding-top:14px}
.pb{padding-bottom:20px}
.gap8{display:flex;flex-direction:column;gap:8px}
.gap14{display:flex;flex-direction:column;gap:14px}
.row{display:flex;justify-content:space-between;align-items:center}
.row-c{display:flex;align-items:center;gap:8px}
.mb8{margin-bottom:8px}
.mb12{margin-bottom:12px}
.mb14{margin-bottom:14px}
.mb16{margin-bottom:16px}
.mt8{margin-top:8px}
.mt14{margin-top:14px}
.c-green{color:var(--green)}
.c-yellow{color:var(--yellow)}
.c-red{color:var(--red)}
.c-dim{color:var(--t2)}
.c-dimmer{color:var(--t3)}
.sm{font-size:12px}
.xs{font-size:10px}
.bold{font-weight:700}
.upper{text-transform:uppercase;letter-spacing:.5px}
</style>
</head>
<body>

<!-- ======= INICIO ======= -->
<div class="screen active" id="sc-inicio">
  <div class="topbar">
    <div>
      <div class="topbar-title">CONTROL DEMOS</div>
      <div class="topbar-sub" id="hdr-fecha"></div>
    </div>
    <button class="btn btn-primary btn-sm" onclick="ir('sc-registro')">+ AGREGAR</button>
  </div>
  <div class="px pt pb">
    <div class="stats" id="stats-box"></div>
    <div class="card mb14" onclick="ir('sc-apertura')" style="padding:14px">
      <div class="row">
        <div>
          <div class="slbl" style="margin-bottom:3px">VISTA APERTURA</div>
          <div id="banner-txt" class="bold" style="font-size:14px"></div>
        </div>
        <svg width="20" height="20" fill="none" stroke="var(--blue)" stroke-width="2" viewBox="0 0 24 24"><path d="M5 12h14M12 5l7 7-7 7" stroke-linecap="round" stroke-linejoin="round"/></svg>
      </div>
    </div>
    <div class="slbl">DEMOS ACTIVOS</div>
    <div class="gap8" id="list-inicio"></div>
  </div>
</div>

<!-- ======= REGISTRO ======= -->
<div class="screen" id="sc-registro">
  <div class="topbar">
    <div class="row-c">
      <button class="btn btn-ghost btn-sm" onclick="atras()">← VOLVER</button>
      <span class="topbar-title" style="font-size:15px">NUEVA UNIDAD</span>
    </div>
  </div>
  <div class="px pt pb gap14">

    <div>
      <label class="f-label">MODELO</label>
      <div class="chips" id="chips-modelo">
        <button class="chip" onclick="elegir(this,'modelo','JAC T6 PHEV')">T6 PHEV</button>
        <button class="chip" onclick="elegir(this,'modelo','JAC T9 4x2')">T9 4x2</button>
        <button class="chip" onclick="elegir(this,'modelo','JAC T9 4x4')">T9 4x4</button>
        <button class="chip" onclick="elegir(this,'modelo','JAC 8')">JAC 8</button>
        <button class="chip" onclick="elegir(this,'modelo','Otro')">Otro</button>
      </div>
    </div>

    <div>
      <label class="f-label">COLOR</label>
      <input class="f-input" id="reg-color" type="text" placeholder="Ej: Blanco perla">
    </div>

    <div>
      <label class="f-label">VIN — ÚLTIMOS 8 DÍGITOS</label>
      <input class="f-input" id="reg-vin" type="text" placeholder="XXXXXXXX" maxlength="8"
        style="letter-spacing:4px;font-size:18px;text-transform:uppercase;font-family:'Courier New',monospace">
    </div>

    <div class="div"></div>

    <div>
      <label class="f-label">ESTATUS</label>
      <div class="chips" id="chips-estatus">
        <button class="chip" onclick="elegir(this,'estatus','Activo')">Activo</button>
        <button class="chip" onclick="elegir(this,'estatus','En préstamo')">En préstamo</button>
        <button class="chip" onclick="elegir(this,'estatus','Sin stock')">Sin stock</button>
      </div>
    </div>

    <div>
      <label class="f-label">UBICACIÓN</label>
      <div class="chips" id="chips-ubicacion">
        <button class="chip" onclick="elegir(this,'ubicacion','Est. público')">Est. público</button>
        <button class="chip" onclick="elegir(this,'ubicacion','Agencia')">Agencia</button>
        <button class="chip" onclick="elegir(this,'ubicacion','Taller')">Taller</button>
        <button class="chip" onclick="elegir(this,'ubicacion','Cliente')">Cliente</button>
      </div>
    </div>

    <div>
      <label class="f-label">ZONA</label>
      <div class="chips" id="chips-zona">
        <button class="chip" onclick="elegir(this,'zona','Entrada')">Entrada</button>
        <button class="chip" onclick="elegir(this,'zona','Fila A')">Fila A</button>
        <button class="chip" onclick="elegir(this,'zona','Fila B')">Fila B</button>
        <button class="chip" onclick="elegir(this,'zona','Fondo')">Fondo</button>
        <button class="chip" onclick="elegir(this,'zona','Calle')">Calle</button>
      </div>
    </div>

    <div class="div"></div>

    <div>
      <label class="f-label">GASOLINA</label>
      <div class="chips" id="chips-gasolina">
        <button class="chip" onclick="elegir(this,'gasolina','Vacío')">Vacío</button>
        <button class="chip" onclick="elegir(this,'gasolina','1/4')">1/4</button>
        <button class="chip" onclick="elegir(this,'gasolina','1/2')">1/2</button>
        <button class="chip" onclick="elegir(this,'gasolina','3/4')">3/4</button>
        <button class="chip" onclick="elegir(this,'gasolina','Lleno')">Lleno</button>
      </div>
    </div>

    <div>
      <label class="f-label">LIMPIEZA</label>
      <div class="chips" id="chips-limpieza">
        <button class="chip" onclick="elegir(this,'limpieza','Limpio')">✓ Limpio</button>
        <button class="chip" onclick="elegir(this,'limpieza','Sucio')">⚠ Sucio</button>
        <button class="chip" onclick="elegir(this,'limpieza','Urgente')">🔴 Urgente</button>
      </div>
    </div>

    <div>
      <label class="f-label">OBSERVACIÓN</label>
      <textarea class="f-input f-textarea" id="reg-obs" placeholder="Notas (opcional)..."></textarea>
    </div>

    <button class="btn btn-primary btn-full mt8" onclick="guardar()">GUARDAR UNIDAD</button>
    <button class="btn btn-ghost btn-full" onclick="atras()">CANCELAR</button>
  </div>
</div>

<!-- ======= FLOTA ======= -->
<div class="screen" id="sc-flota">
  <div class="topbar">
    <div class="topbar-title">FLOTA</div>
    <button class="btn btn-primary btn-sm" onclick="ir('sc-registro')">+ DEMO</button>
  </div>
  <div class="px pt pb">
    <div class="chips mb14" id="filtros">
      <button class="chip sel" onclick="filtrar(this,'todos')">Todos</button>
      <button class="chip" onclick="filtrar(this,'listo')">✓ Listo</button>
      <button class="chip" onclick="filtrar(this,'riesgo')">⚠ Riesgo</button>
      <button class="chip" onclick="filtrar(this,'nolisto')">✕ No listo</button>
    </div>
    <div class="gap8" id="list-flota"></div>
  </div>
</div>

<!-- ======= APERTURA ======= -->
<div class="screen" id="sc-apertura">
  <div class="topbar">
    <div>
      <div class="topbar-title">APERTURA</div>
      <div class="topbar-sub" id="aper-fecha"></div>
    </div>
    <div id="aper-badge"></div>
  </div>
  <div class="px pt pb gap8" id="list-apertura"></div>
</div>

<!-- ======= ALERTAS ======= -->
<div class="screen" id="sc-alertas">
  <div class="topbar">
    <div class="topbar-title">ALERTAS</div>
    <div id="alert-badge"></div>
  </div>
  <div class="px pt pb gap8" id="list-alertas"></div>
</div>

<!-- ======= DETALLE ======= -->
<div class="screen" id="sc-detalle">
  <div class="topbar">
    <button class="btn btn-ghost btn-sm" onclick="atras()">← VOLVER</button>
    <button class="btn btn-ghost btn-sm" onclick="abrirEditar()">EDITAR</button>
  </div>
  <div class="px pt pb" id="detalle-body"></div>
</div>

<!-- ======= NAVBAR ======= -->
<nav class="navbar">
  <button class="nav-item active" id="nav-inicio" onclick="navIr('inicio')">
    <svg viewBox="0 0 24 24"><path d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" stroke-linecap="round" stroke-linejoin="round"/></svg>
    INICIO
  </button>
  <button class="nav-item" id="nav-flota" onclick="navIr('flota')">
    <svg viewBox="0 0 24 24"><path d="M9 17a2 2 0 11-4 0 2 2 0 014 0zM19 17a2 2 0 11-4 0 2 2 0 014 0z"/><path d="M13 16V6a1 1 0 00-1-1H4a1 1 0 00-1 1v10l3-1M13 16H9m0 0l-3 1m13-1h-4m0 0v-5l-3-3H9" stroke-linecap="round" stroke-linejoin="round"/></svg>
    FLOTA
  </button>
  <button class="nav-item" id="nav-apertura" onclick="navIr('apertura')">
    <svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="10"/><path d="M12 6v6l4 2" stroke-linecap="round"/></svg>
    APERTURA
  </button>
  <button class="nav-item" id="nav-alertas" onclick="navIr('alertas')">
    <svg viewBox="0 0 24 24"><path d="M18 8A6 6 0 006 8c0 7-3 9-3 9h18s-3-2-3-9M13.73 21a2 2 0 01-3.46 0" stroke-linecap="round" stroke-linejoin="round"/></svg>
    ALERTAS
  </button>
</nav>

<!-- ======= MODAL EDITAR ======= -->
<div class="overlay" id="modal-overlay" onclick="cerrarModal(event)">
  <div class="modal" onclick="event.stopPropagation()">
    <div class="modal-handle"></div>
    <div class="bold upper mb14" style="font-size:15px;letter-spacing:1.5px">EDITAR UNIDAD</div>
    <div id="modal-body"></div>
  </div>
</div>

<!-- ======= TOAST ======= -->
<div class="toast" id="toast"></div>

<script>
// ============================================================
// STORAGE
// ============================================================
const KEY = 'ctrl_demos_v3';
function leer(){ try{ return JSON.parse(localStorage.getItem(KEY)||'[]'); }catch{ return []; } }
function escribir(d){ localStorage.setItem(KEY, JSON.stringify(d)); }

// ============================================================
// LÓGICA
// ============================================================
function estado(d){
  if(!d.estatus || d.estatus==='Sin stock') return null;
  if(d.limpieza==='Urgente' || d.gasolina==='Vacío') return 'nolisto';
  if(d.limpieza==='Sucio'   || d.gasolina==='1/4')   return 'riesgo';
  if(d.limpieza==='Limpio'  && ['1/2','3/4','Lleno'].includes(d.gasolina)) return 'listo';
  return 'riesgo';
}
function accion(d){
  if(d.limpieza==='Urgente'||d.limpieza==='Sucio') return 'lavado';
  if(d.gasolina==='Vacío'  ||d.gasolina==='1/4')   return 'gas';
  if(d.ubicacion!=='Est. público')                  return 'acomodar';
  return 'ok';
}
const ELBL={listo:'LISTO',riesgo:'RIESGO',nolisto:'NO LISTO'};
const ALBL={lavado:'MOVER A LAVADO',gas:'CARGAR GASOLINA',acomodar:'REACOMODAR',ok:'SIN ACCIÓN'};
const ACLS={lavado:'at-lavado',gas:'at-gas',acomodar:'at-acomodar',ok:'at-ok'};

function fuelHTML(g){
  const n={Vacío:0,'1/4':1,'1/2':2,'3/4':3,'Lleno':4}[g]||0;
  return Array.from({length:4},(_,i)=>{
    let c='';
    if(i<n) c=n<=1?'danger':n===2?'warn':'ok';
    return `<div class="fuel-s ${c}"></div>`;
  }).join('');
}

// ============================================================
// NAVEGACIÓN
// ============================================================
let pantActual='sc-inicio', pantAnterior='sc-inicio', detalleId=null;

function ir(id){
  document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  pantAnterior=pantActual; pantActual=id;
  refrescar(id);
}
function atras(){ ir(pantAnterior); }
function navIr(tab){
  const mapa={inicio:'sc-inicio',flota:'sc-flota',apertura:'sc-apertura',alertas:'sc-alertas'};
  document.querySelectorAll('.nav-item').forEach(b=>b.classList.remove('active'));
  document.getElementById('nav-'+tab).classList.add('active');
  ir(mapa[tab]);
}
function refrescar(id){
  if(id==='sc-inicio')   pintarInicio();
  if(id==='sc-flota')    pintarFlota(filtroActivo);
  if(id==='sc-apertura') pintarApertura();
  if(id==='sc-alertas')  pintarAlertas();
}

// ============================================================
// TARJETA
// ============================================================
function tarjeta(d, clickable=true){
  const e=estado(d), a=accion(d);
  const cls=e||'';
  const click=clickable?`onclick="abrirDetalle('${d.id}')"` : '';
  return `
  <div class="card ${cls}" ${click}>
    <div class="row mb8">
      <div>
        <div class="bold upper" style="font-size:16px">${d.modelo||'—'}</div>
        <div class="xs c-dim" style="margin-top:2px">${d.color||''}</div>
      </div>
      ${e?`<span class="badge ${e}"><span class="dot ${e}"></span>${ELBL[e]}</span>`:`<span class="badge prestamo">PRÉSTAMO</span>`}
    </div>
    <div class="row mb8">
      <div class="vin" style="font-size:13px;padding:5px 10px;letter-spacing:3px">${d.vin8||'——————'}</div>
      <div style="text-align:right">
        <div class="fuel">${fuelHTML(d.gasolina)}</div>
        <div class="xs c-dim" style="margin-top:3px">${d.gasolina||'—'}</div>
      </div>
    </div>
    <div class="row">
      <div class="xs c-dimmer">${d.ubicacion||'—'}${d.zona?' · '+d.zona:''}</div>
      <span class="atag ${ACLS[a]}">${ALBL[a]}</span>
    </div>
  </div>`;
}

function ordenar(arr){
  return [...arr].sort((a,b)=>({nolisto:0,riesgo:1,listo:2,null:3}[estado(a)||'null'])-({nolisto:0,riesgo:1,listo:2,null:3}[estado(b)||'null']));
}

// ============================================================
// PANTALLA: INICIO
// ============================================================
function pintarInicio(){
  const todos=leer();
  const activos=todos.filter(d=>d.estatus==='Activo');
  const nL=activos.filter(d=>estado(d)==='listo').length;
  const nR=activos.filter(d=>estado(d)==='riesgo').length;
  const nN=activos.filter(d=>estado(d)==='nolisto').length;

  document.getElementById('hdr-fecha').textContent=
    new Date().toLocaleDateString('es-MX',{weekday:'long',day:'numeric',month:'long',year:'numeric'}).toUpperCase();

  document.getElementById('stats-box').innerHTML=`
    <div class="stat"><div class="stat-n">${activos.length}</div><div class="stat-l">TOTAL</div></div>
    <div class="stat"><div class="stat-n c-green">${nL}</div><div class="stat-l">LISTAS</div></div>
    <div class="stat"><div class="stat-n c-yellow">${nR}</div><div class="stat-l">RIESGO</div></div>
    <div class="stat"><div class="stat-n c-red">${nN}</div><div class="stat-l">NO LISTAS</div></div>`;

  let txt='';
  if(nN>0) txt=`<span class="c-red">${nN} unidad${nN>1?'es':''} NO lista${nN>1?'s':''}</span>`;
  else if(nR>0) txt=`<span class="c-yellow">${nR} en riesgo</span>`;
  else if(activos.length>0) txt=`<span class="c-green">Flota lista ✓</span>`;
  else txt='<span class="c-dim">Sin unidades registradas</span>';
  document.getElementById('banner-txt').innerHTML=txt;

  const el=document.getElementById('list-inicio');
  if(!activos.length){
    el.innerHTML=`<div class="empty"><div class="empty-ico">🚗</div><div class="empty-title">SIN UNIDADES</div><div class="empty-sub">TOCA "+ AGREGAR"</div></div>`;
    return;
  }
  el.innerHTML=ordenar(activos).map(d=>tarjeta(d)).join('');
}

// ============================================================
// PANTALLA: FLOTA
// ============================================================
let filtroActivo='todos';
function pintarFlota(f){
  filtroActivo=f;
  const todos=leer();
  const lista=f==='todos'?todos:todos.filter(d=>estado(d)===f);
  const el=document.getElementById('list-flota');
  el.innerHTML=lista.length?ordenar(lista).map(d=>tarjeta(d)).join(''):
    `<div class="empty"><div class="empty-ico">🔍</div><div class="empty-title">SIN RESULTADOS</div></div>`;
}
function filtrar(btn,f){
  document.querySelectorAll('#filtros .chip').forEach(c=>c.classList.remove('sel'));
  btn.classList.add('sel');
  pintarFlota(f);
}

// ============================================================
// PANTALLA: APERTURA
// ============================================================
function pintarApertura(){
  const activos=leer().filter(d=>d.estatus==='Activo');
  document.getElementById('aper-fecha').textContent=
    new Date().toLocaleDateString('es-MX',{weekday:'long',day:'numeric',month:'long'}).toUpperCase();

  const nN=activos.filter(d=>estado(d)==='nolisto').length;
  const nR=activos.filter(d=>estado(d)==='riesgo').length;
  document.getElementById('aper-badge').innerHTML=
    nN>0?`<span class="badge nolisto">${nN} CRÍTICO${nN>1?'S':''}</span>`:
    nR>0?`<span class="badge riesgo">${nR} RIESGO</span>`:
    `<span class="badge listo">TODO LISTO</span>`;

  const el=document.getElementById('list-apertura');
  if(!activos.length){
    el.innerHTML=`<div class="empty"><div class="empty-ico">📋</div><div class="empty-title">SIN DEMOS</div></div>`;
    return;
  }
  el.innerHTML=ordenar(activos).map(d=>{
    const e=estado(d), a=accion(d);
    const borde={listo:'var(--green)',riesgo:'var(--yellow)',nolisto:'var(--red)'}[e]||'var(--b2)';
    const clim=d.limpieza==='Urgente'?'c-red':d.limpieza==='Sucio'?'c-yellow':'c-green';
    return `
    <div class="card ${e||''}" style="border-left:3px solid ${borde}">
      <div class="row mb8">
        <div class="row-c">
          <span class="dot ${e||''}"></span>
          <div>
            <div class="bold upper" style="font-size:15px">${d.modelo||'—'}</div>
            <div class="xs c-dim">${d.vin8||'—'} · ${d.color||'—'}</div>
          </div>
        </div>
        <span class="badge ${e||''}" style="font-size:8px">${ELBL[e]||'—'}</span>
      </div>
      <div class="drow"><span class="dk">GASOLINA</span><div class="row-c"><div class="fuel">${fuelHTML(d.gasolina)}</div><span class="dv sm">${d.gasolina||'—'}</span></div></div>
      <div class="drow"><span class="dk">LIMPIEZA</span><span class="dv sm ${clim}">${d.limpieza||'—'}</span></div>
      <div class="drow"><span class="dk">ZONA</span><span class="dv sm">${d.zona||'—'} · ${d.ubicacion||'—'}</span></div>
      <div class="drow" style="border:none"><span class="dk">ACCIÓN</span><span class="atag ${ACLS[a]}">${ALBL[a]}</span></div>
      ${d.obs?`<div class="xs c-dim mt8">${d.obs}</div>`:''}
      <button class="btn btn-ghost btn-full btn-sm mt8" onclick="abrirDetalle('${d.id}')">VER DETALLE →</button>
    </div>`;
  }).join('');
}

// ============================================================
// PANTALLA: ALERTAS
// ============================================================
function pintarAlertas(){
  const activos=leer().filter(d=>d.estatus==='Activo');
  const lista=[];
  activos.forEach(d=>{
    const t=`${d.modelo||'—'} · ${d.vin8||'—'}`;
    if(d.limpieza==='Urgente') lista.push({p:0,t,s:'LIMPIEZA URGENTE — Ir a lavado',i:'🔴',c:'var(--red)'});
    if(d.gasolina==='Vacío')   lista.push({p:0,t,s:'SIN GASOLINA — Cargar antes de apertura',i:'⛽',c:'var(--red)'});
    if(d.gasolina==='1/4')     lista.push({p:1,t,s:'GASOLINA BAJA — Riesgo operativo',i:'⚠️',c:'var(--yellow)'});
    if(d.limpieza==='Sucio')   lista.push({p:1,t,s:'UNIDAD SUCIA — Requiere limpieza',i:'🧹',c:'var(--yellow)'});
  });
  lista.sort((a,b)=>a.p-b.p);
  const nc=lista.filter(a=>a.p===0).length;
  document.getElementById('alert-badge').innerHTML=
    nc>0?`<span class="badge nolisto">${nc} CRÍTICA${nc>1?'S':''}</span>`:
    `<span class="badge listo">SIN CRÍTICAS</span>`;
  const el=document.getElementById('list-alertas');
  el.innerHTML=lista.length?lista.map(a=>`
    <div class="alert-row" style="border-left:3px solid ${a.c}">
      <div class="alert-ico">${a.i}</div>
      <div><div class="alert-title">${a.t}</div><div class="alert-sub">${a.s}</div></div>
    </div>`).join(''):
    `<div class="empty"><div class="empty-ico">✅</div><div class="empty-title">SIN ALERTAS</div><div class="empty-sub">FLOTA EN ORDEN</div></div>`;
}

// ============================================================
// DETALLE
// ============================================================
function abrirDetalle(id){
  detalleId=id;
  const d=leer().find(x=>x.id===id);
  if(!d) return;
  const e=estado(d), a=accion(d);
  const clim=d.limpieza==='Urgente'?'c-red':d.limpieza==='Sucio'?'c-yellow':'c-green';
  document.getElementById('detalle-body').innerHTML=`
    <div class="row mb12">
      <div>
        <div class="bold upper" style="font-size:22px">${d.modelo||'—'}</div>
        <div class="c-dim sm" style="margin-top:3px">${d.color||'—'}</div>
      </div>
      ${e?`<span class="badge ${e}"><span class="dot ${e}"></span>${ELBL[e]}</span>`:`<span class="badge prestamo">PRÉSTAMO</span>`}
    </div>
    <div class="vin mb14">${d.vin8||'——————'}</div>

    <div class="card" style="cursor:default;margin-bottom:12px">
      <div class="slbl">IDENTIFICACIÓN</div>
      <div class="drow"><span class="dk">MODELO</span><span class="dv">${d.modelo||'—'}</span></div>
      <div class="drow"><span class="dk">COLOR</span><span class="dv">${d.color||'—'}</span></div>
      <div class="drow"><span class="dk">VIN_8</span><span class="dv" style="font-family:'Courier New',monospace;letter-spacing:2px;color:var(--blue)">${d.vin8||'—'}</span></div>
      <div class="drow"><span class="dk">ESTATUS</span><span class="dv">${d.estatus||'—'}</span></div>
    </div>

    <div class="card" style="cursor:default;margin-bottom:12px">
      <div class="slbl">UBICACIÓN</div>
      <div class="drow"><span class="dk">LUGAR</span><span class="dv">${d.ubicacion||'—'}</span></div>
      <div class="drow"><span class="dk">ZONA</span><span class="dv">${d.zona||'—'}</span></div>
    </div>

    <div class="card" style="cursor:default;margin-bottom:12px">
      <div class="slbl">CONDICIÓN</div>
      <div class="drow"><span class="dk">GASOLINA</span><div class="row-c"><div class="fuel">${fuelHTML(d.gasolina)}</div><span class="dv sm">${d.gasolina||'—'}</span></div></div>
      <div class="drow"><span class="dk">LIMPIEZA</span><span class="dv ${clim}">${d.limpieza||'—'}</span></div>
      ${d.obs?`<div class="drow"><span class="dk">OBS</span><span class="dv sm" style="max-width:60%;text-align:right">${d.obs}</span></div>`:''}
    </div>

    <div class="card" style="cursor:default;background:var(--s2);margin-bottom:16px">
      <div class="slbl">ACCIÓN REQUERIDA</div>
      <span class="atag ${ACLS[a]}" style="font-size:11px;padding:6px 14px">${ALBL[a]}</span>
    </div>

    <div style="display:flex;gap:10px">
      <button class="btn btn-primary" style="flex:1" onclick="abrirEditar()">EDITAR</button>
      <button class="btn btn-danger" style="flex:1" onclick="eliminar('${d.id}')">ELIMINAR</button>
    </div>`;
  ir('sc-detalle');
}

// ============================================================
// FORM STATE
// ============================================================
const FS={};
function elegir(el,campo,val){
  el.closest('.chips').querySelectorAll('.chip').forEach(c=>c.classList.remove('sel','sel-g','sel-y','sel-r'));
  FS[campo]=val;
  const colores={
    gasolina:{Vacío:'sel-r','1/4':'sel-y','1/2':'sel-g','3/4':'sel-g','Lleno':'sel-g'},
    limpieza:{Limpio:'sel-g',Sucio:'sel-y',Urgente:'sel-r'}
  };
  el.classList.add(colores[campo]?.[val]||'sel');
}
function resetForm(){
  Object.keys(FS).forEach(k=>delete FS[k]);
  ['reg-color','reg-vin','reg-obs'].forEach(id=>{const el=document.getElementById(id);if(el)el.value='';});
  document.querySelectorAll('#sc-registro .chip').forEach(c=>c.classList.remove('sel','sel-g','sel-y','sel-r'));
}

// ============================================================
// GUARDAR
// ============================================================
function guardar(){
  const vin=(document.getElementById('reg-vin').value||'').trim().toUpperCase();
  if(!FS.modelo)     { toast('⚠ Selecciona un modelo'); return; }
  if(vin.length<4)   { toast('⚠ Mínimo 4 dígitos del VIN'); return; }
  if(!FS.gasolina)   { toast('⚠ Indica nivel de gasolina'); return; }
  if(!FS.limpieza)   { toast('⚠ Indica estado de limpieza'); return; }
  const d={
    id:Date.now().toString(),
    modelo:FS.modelo,
    color:(document.getElementById('reg-color').value||'').trim()||'Sin especificar',
    vin8:vin,
    estatus:FS.estatus||'Activo',
    ubicacion:FS.ubicacion||'Agencia',
    zona:FS.zona||'',
    gasolina:FS.gasolina,
    limpieza:FS.limpieza,
    obs:(document.getElementById('reg-obs').value||'').trim(),
    ts:new Date().toISOString()
  };
  const todos=leer(); todos.push(d); escribir(todos);
  resetForm();
  toast('✓ Unidad registrada');
  ir('sc-inicio');
}

// ============================================================
// EDITAR
// ============================================================
let ES={};
function abrirEditar(){
  const d=leer().find(x=>x.id===detalleId);
  if(!d) return;
  ES={gasolina:d.gasolina,limpieza:d.limpieza,zona:d.zona,ubicacion:d.ubicacion,estatus:d.estatus};

  function mkChips(campo,ops,val){
    const colores={
      gasolina:{Vacío:'sel-r','1/4':'sel-y','1/2':'sel-g','3/4':'sel-g','Lleno':'sel-g'},
      limpieza:{Limpio:'sel-g',Sucio:'sel-y',Urgente:'sel-r'}
    };
    return ops.map(v=>{
      const sc=val===v?(colores[campo]?.[v]||'sel'):'';
      return `<button class="chip ${sc}" onclick="editChip(this,'${campo}','${v.replace(/'/g,"\\'")}',${!!(colores[campo])})">${v}</button>`;
    }).join('');
  }

  document.getElementById('modal-body').innerHTML=`
    <div class="gap14">
      <div><label class="f-label">GASOLINA</label><div class="chips">${mkChips('gasolina',['Vacío','1/4','1/2','3/4','Lleno'],d.gasolina)}</div></div>
      <div><label class="f-label">LIMPIEZA</label><div class="chips">${mkChips('limpieza',['Limpio','Sucio','Urgente'],d.limpieza)}</div></div>
      <div><label class="f-label">ZONA</label><div class="chips">${mkChips('zona',['Entrada','Fila A','Fila B','Fondo','Calle'],d.zona)}</div></div>
      <div><label class="f-label">UBICACIÓN</label><div class="chips">${mkChips('ubicacion',['Est. público','Agencia','Taller','Cliente'],d.ubicacion)}</div></div>
      <div><label class="f-label">ESTATUS</label><div class="chips">${mkChips('estatus',['Activo','En préstamo','Sin stock'],d.estatus)}</div></div>
      <div><label class="f-label">OBSERVACIÓN</label><textarea class="f-input f-textarea" id="edit-obs" style="min-height:60px">${d.obs||''}</textarea></div>
      <button class="btn btn-primary btn-full" onclick="guardarEdicion()">GUARDAR CAMBIOS</button>
    </div>`;
  document.getElementById('modal-overlay').classList.add('open');
}
function editChip(el,campo,val,usar_color){
  el.closest('.chips').querySelectorAll('.chip').forEach(c=>c.classList.remove('sel','sel-g','sel-y','sel-r'));
  ES[campo]=val;
  if(usar_color){
    const colores={gasolina:{Vacío:'sel-r','1/4':'sel-y','1/2':'sel-g','3/4':'sel-g',Lleno:'sel-g'},limpieza:{Limpio:'sel-g',Sucio:'sel-y',Urgente:'sel-r'}};
    el.classList.add(colores[campo]?.[val]||'sel');
  } else {
    el.classList.add('sel');
  }
}
function guardarEdicion(){
  const todos=leer();
  const i=todos.findIndex(x=>x.id===detalleId);
  if(i===-1) return;
  Object.assign(todos[i],ES);
  todos[i].obs=(document.getElementById('edit-obs').value||'').trim();
  escribir(todos);
  cerrarModal();
  toast('✓ Cambios guardados');
  abrirDetalle(detalleId);
}
function cerrarModal(e){
  if(!e||e.target===document.getElementById('modal-overlay')){
    document.getElementById('modal-overlay').classList.remove('open');
  }
}

// ============================================================
// ELIMINAR
// ============================================================
function eliminar(id){
  const d=leer().find(x=>x.id===id);
  if(!d||!confirm(`¿Eliminar ${d.modelo} (${d.vin8})?`)) return;
  escribir(leer().filter(x=>x.id!==id));
  toast('Unidad eliminada');
  navIr('inicio');
}

// ============================================================
// TOAST
// ============================================================
let _tt;
function toast(msg){
  const el=document.getElementById('toast');
  el.textContent=msg; el.classList.add('show');
  clearTimeout(_tt); _tt=setTimeout(()=>el.classList.remove('show'),2500);
}

// ============================================================
// INIT
// ============================================================
document.addEventListener('DOMContentLoaded', pintarInicio);
</script>
</body>
</html
