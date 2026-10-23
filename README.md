# Mi-Ritmo2
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#243d83">
<title>MiRitmo</title>
<style>
:root{--navy:#243d83;--blue:#4168bd;--sky:#dceaff;--purple:#8d62c7;--pink:#e9a8d0;--ink:#20315f;--paper:#f7f8ff;--green:#4b9c83}
*{box-sizing:border-box}
body{margin:0;background:linear-gradient(145deg,#e9edff,#f8f2ff);color:var(--ink);font-family:system-ui,-apple-system,"Segoe UI",sans-serif}
button,input{font:inherit}
.app{width:min(100%,760px);margin:auto;min-height:100dvh;padding:clamp(10px,3vw,22px);padding-bottom:calc(18px + env(safe-area-inset-bottom))}
header{background:linear-gradient(135deg,var(--navy),var(--blue));color:white;border-radius:24px;padding:20px;box-shadow:0 8px 24px #273f8425;display:flex;align-items:center;gap:14px}
.logo{width:58px;height:58px;border-radius:18px;background:#ffffff20;display:grid;place-items:center;font-size:32px;flex-shrink:0}
h1{margin:0;font-size:clamp(24px,5vw,34px);line-height:1.1}header p{margin:5px 0 0;color:#e4eaff}
.date-card,.card{background:#fff;border:1px solid #e5e8fb;border-radius:20px;padding:16px;margin-top:14px;box-shadow:0 4px 16px #293e8010}
.date-line{display:flex;justify-content:space-between;align-items:center;gap:10px;flex-wrap:wrap}
.date-label{font-size:clamp(18px,4vw,23px);font-weight:800;color:var(--navy)}
.muted{color:#68769c;font-size:14px}
.pill{background:#edf1ff;color:var(--navy);padding:7px 11px;border-radius:99px;font-size:13px;font-weight:700}
.stats{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:10px;margin-top:12px}
.stat{background:#f4f6ff;border-radius:15px;padding:12px;text-align:center}
.stat strong{display:block;font-size:clamp(20px,4vw,27px);color:var(--navy)}
.stat span{font-size:12px;color:#69779d}
h2{font-size:19px;margin:0 0 12px;color:var(--navy)}
.progress{height:10px;background:#e9edfb;border-radius:99px;overflow:hidden;margin-top:10px}
.progress>div{height:100%;width:0;background:linear-gradient(90deg,var(--blue),var(--purple));transition:width .2s}
.tabs{display:flex;gap:8px;overflow:auto;margin-top:14px}
.tab{border:0;border-radius:99px;padding:10px 14px;background:#fff;color:var(--navy);font-weight:750;white-space:nowrap}
.tab.active{background:var(--navy);color:#fff}
.task-list{display:grid;gap:9px}
.task{display:flex;align-items:center;gap:11px;padding:12px;border:1px solid #e6eafa;border-radius:15px;background:#fff}
.task input{width:22px;height:22px;accent-color:var(--blue);flex-shrink:0}
.task .task-text{flex:1;min-width:0}
.task .task-text strong{display:block;font-size:15px}
.task .task-text small{color:#7b86a7}
.points{font-weight:800;color:var(--purple);white-space:nowrap}
.task.done{background:#f0faf6;border-color:#bce6d8}
.task.done .task-text strong{text-decoration:line-through;color:#658477}
.actions{display:flex;gap:8px;flex-wrap:wrap;margin-top:12px}
button.action{border:0;border-radius:12px;padding:11px 14px;background:var(--navy);color:#fff;font-weight:750}
button.secondary{background:#edf1ff;color:var(--navy)}
input[type="text"]{min-width:0;flex:1;border:1px solid #dce3f7;border-radius:12px;padding:11px;color:var(--ink)}
.note{font-size:12px;line-height:1.5;color:#7782a1;margin:14px 3px}
.hidden{display:none!important}
footer{text-align:center;color:#7b85a5;font-size:12px;padding:18px 0 4px}
@media(max-width:360px){.app{padding:9px}.date-card,.card{padding:12px}.stats{gap:6px}.stat{padding:9px 4px}.task{gap:8px;padding:10px}.task .task-text strong{font-size:14px}.points{font-size:13px}}
@media(max-width:240px){header{padding:12px;gap:8px}.logo{width:40px;height:40px;font-size:23px}h1{font-size:21px}.stats{grid-template-columns:1fr}.date-line{align-items:flex-start}.task{flex-wrap:wrap}.task .task-text{flex-basis:calc(100% - 45px)}}
@media(prefers-reduced-motion:reduce){*{transition:none!important}}
</style>
</head>
<body>
<main class="app">
<header>
  <div class="logo" aria-hidden="true">🏃🏻‍♀️</div>
  <div><h1>MiRitmo</h1><p>Tu día, a tu ritmo. 💙</p></div>
</header>

<section class="date-card" aria-live="polite">
  <div class="date-line">
    <div><div class="muted">HOY ES</div><div id="today" class="date-label">Cargando fecha…</div></div>
    <span class="pill" id="dateShort">Mi calendario</span>
  </div>
  <div class="stats">
    <div class="stat"><strong id="earned">0</strong><span>Puntos de hoy</span></div>
    <div class="stat"><strong id="completed">0/0</strong><span>Completadas</span></div>
    <div class="stat"><strong id="streak">0</strong><span>Días activos*</span></div>
  </div>
  <div class="stats">
    <div class="stat"><strong id="sleepSummary">—</strong><span>Horas de sueño</span></div>
    <div class="stat"><strong id="exerciseSummary">0 min</strong><span>Ejercicio</span></div>
    <div class="stat"><strong id="stepsSummary">0</strong><span>Pasos</span></div>
  </div>
  <div class="progress" role="progressbar" aria-label="Progreso de actividades" aria-valuemin="0" aria-valuemax="100" aria-valuenow="0" id="progressBar"><div id="progressFill"></div></div>
  <p class="muted" id="progressText">¡Cada pequeño paso cuenta!</p>
</section>

<nav class="tabs" aria-label="Secciones">
  <button class="tab active" data-tab="tasks">Mis actividades</button>
  <button class="tab" data-tab="calendar">Calendario</button>
  <button class="tab" data-tab="points">Mis puntos</button>
</nav>

<section class="card" id="tasksPanel">
  <h2>⌚ Conectar reloj inteligente</h2>
  <p class="muted">Elige la marca de tu reloj. La conexión automática requiere una aplicación complementaria compatible y permisos de salud; esta página no puede conectarse directamente a todos los sensores.</p>
  <label for="watchBrand" class="muted">Marca o sistema</label>
  <select id="watchBrand" style="width:100%;margin-top:6px;border:1px solid #dce3f7;border-radius:12px;padding:12px;background:#fff;color:#20315f">
    <option value="wearos">Samsung Galaxy Watch / Wear OS</option>
    <option value="apple">Apple Watch / iPhone</option>
    <option value="garmin">Garmin</option>
    <option value="huawei">Huawei</option>
    <option value="xiaomi">Xiaomi / Redmi</option>
    <option value="other">Otro reloj</option>
  </select>
  <div class="actions">
    <button id="connectWatch" class="action" type="button">Comprobar conexión</button>
    <button id="bluetoothWatch" class="action" type="button">Buscar reloj por Bluetooth</button>
    <button id="disconnectWatch" class="action secondary" type="button">Desconectar</button>
  </div>
  <p id="heartRateStatus" class="muted">Frecuencia cardiaca Bluetooth: esperando un reloj compatible.</p>
  <p id="connectionStatus" class="muted" aria-live="polite">Estado: sin conexión nativa. Puedes registrar datos manualmente.</p>
  <p class="note">Health Connect importa los datos que comparten las apps compatibles. La conexión Bluetooth directa busca dispositivos BLE y puede mostrar frecuencia cardiaca solo si anuncian el perfil estándar de pulso; no obtiene automáticamente pasos ni sueño de todos los relojes. La disponibilidad depende del modelo y sus permisos.</p>
  <h2>🌙 Sueño, ejercicio y pasos</h2>
  <p class="muted">Registra tus datos del día. Los pasos se ingresan manualmente; el HTML por sí solo no puede leer el sensor del reloj.</p>
  <div class="stats">
    <label class="stat">Horas de sueño
      <input id="sleepInput" type="number" min="0" max="24" step="0.25" placeholder="8" aria-label="Horas de sueño" style="width:100%;margin-top:8px;border:1px solid #dce3f7;border-radius:10px;padding:8px;text-align:center">
    </label>
    <label class="stat">Ejercicio (min)
      <input id="exerciseInput" type="number" min="0" max="1440" step="1" placeholder="30" aria-label="Minutos de ejercicio" style="width:100%;margin-top:8px;border:1px solid #dce3f7;border-radius:10px;padding:8px;text-align:center">
    </label>
    <label class="stat">Pasos
      <input id="stepsInput" type="number" min="0" max="200000" step="1" placeholder="5000" aria-label="Número de pasos" style="width:100%;margin-top:8px;border:1px solid #dce3f7;border-radius:10px;padding:8px;text-align:center">
    </label>
  </div>
  <div class="actions"><button id="saveHealth" class="action" type="button">Guardar datos</button><span class="muted" id="healthMessage" aria-live="polite"></span></div>
  <div class="progress" role="progressbar" aria-label="Meta diaria de pasos" aria-valuemin="0" aria-valuemax="100" aria-valuenow="0" id="stepsBar"><div id="stepsFill"></div></div>
  <p class="muted" id="stepsGoalText">Meta de ejemplo: 5,000 pasos al día. Puedes ajustarla a tus necesidades.</p>
  <hr style="border:0;border-top:1px solid #e8ebf8;margin:18px 0">
  <h2>⏳ Actividades pendientes</h2>
  <p class="muted">Aquí aparecen las actividades que todavía no marcas como terminadas.</p>
  <div id="pendingList" class="task-list"></div>
  <hr style="border:0;border-top:1px solid #e8ebf8;margin:18px 0">
  <h2>✨ Actividades cotidianas</h2>
  <p class="muted">Marca una actividad cuando la termines. Cada una suma puntos una sola vez al día.</p>
  <div id="taskList" class="task-list"></div>
  <form id="addForm" class="actions">
    <input id="newTask" type="text" maxlength="55" placeholder="Agregar otra actividad…" aria-label="Nueva actividad">
    <button class="action" type="submit">+ Agregar</button>
  </form>
  <div class="actions"><button id="resetDay" class="action secondary" type="button">Reiniciar día</button></div>
</section>

<section class="card hidden" id="calendarPanel">
  <h2>🗓️ Mi calendario</h2>
  <p class="muted">La fecha se actualiza automáticamente según la fecha del dispositivo. Los días con actividades completadas aparecen marcados.</p>
  <div class="date-line">
    <button class="action secondary" id="prevMonth" type="button" aria-label="Mes anterior">‹</button>
    <strong id="monthTitle">Mes</strong>
    <button class="action secondary" id="nextMonth" type="button" aria-label="Mes siguiente">›</button>
  </div>
  <div id="calendarGrid" style="display:grid;grid-template-columns:repeat(7,minmax(0,1fr));gap:5px;margin-top:14px;text-align:center"></div>
  <p class="muted">● Día actual · ✓ Día con actividades terminadas</p>
</section>

<section class="card hidden" id="pointsPanel">
  <h2>🏆 Mis puntos</h2>
  <p>Completa actividades cotidianas para ganar puntos. Tu progreso se guarda en este dispositivo.</p>
  <div class="stats">
    <div class="stat"><strong id="totalPoints">0</strong><span>Puntos acumulados</span></div>
    <div class="stat"><strong id="totalTasks">0</strong><span>Actividades hechas</span></div>
    <div class="stat"><strong id="level">🌱</strong><span>Tu nivel</span></div>
  </div>
  <p class="muted" id="levelText">¡Empieza con una actividad!</p>
  <h2 style="margin-top:18px">📅 Resumen de hoy</h2>
  <div id="todaySummary" class="muted">Aún no has completado actividades.</div>
</section>

<p class="note">*Los días activos se calculan a partir del uso registrado en este dispositivo. Para que el calendario avance correctamente, permite que el reloj o celular ajuste la fecha y hora automáticamente. Los datos del navegador pueden borrarse si eliminas sus datos.</p>
<footer>MiRitmo · Pequeños hábitos, grandes logros 💜</footer>
</main>
<script>
(function(){
'use strict';
const STORAGE='mir ritmo_app_v1'.replace(' ','');
const baseTasks=[
 {id:'bed',name:'Tender mi cama',points:10,category:'Rutina'},
 {id:'room',name:'Ordenar mi habitación',points:10,category:'Casa'},
 {id:'homework',name:'Hacer la tarea',points:20,category:'Escuela'},
 {id:'backpack',name:'Preparar mi mochila',points:10,category:'Escuela'},
 {id:'read',name:'Leer durante un rato',points:10,category:'Aprendizaje'},
 {id:'walk',name:'Caminar o moverme un rato',points:15,category:'Bienestar'},
 {id:'help',name:'Ayudar en casa',points:15,category:'Casa'},
 {id:'teeth',name:'Cepillarme los dientes',points:5,category:'Rutina'},
 {id:'clothes',name:'Preparar mi ropa para mañana',points:10,category:'Rutina'},
 {id:'organize',name:'Organizar mis pendientes',points:10,category:'Organización'},
 {id:'break',name:'Tomar un descanso de pantallas',points:10,category:'Bienestar'},
 {id:'kindness',name:'Hacer algo amable por alguien',points:15,category:'Convivencia'}
];
const $=id=>document.getElementById(id);
const dayKey=d=>`${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(d.getDate()).padStart(2,'0')}`;
const fresh=()=>({tasks:baseTasks.map(t=>({...t})),days:{},totals:{points:0,tasks:0}});
let data;
try{data=JSON.parse(localStorage.getItem(STORAGE))||fresh()}catch(e){data=fresh()}
if(!Array.isArray(data.tasks)||!data.days||!data.totals)data=fresh();
let currentDay=dayKey(new Date()),viewDate=new Date();
function save(){try{localStorage.setItem(STORAGE,JSON.stringify(data))}catch(e){}}
function dayRecord(key=currentDay){if(!data.days[key])data.days[key]={done:[],sleep:'',exercise:0,steps:0};if(!Array.isArray(data.days[key].done))data.days[key].done=[];return data.days[key]}
function escapeHtml(s){return String(s).replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]))}
function fmtDate(d,opts){return new Intl.DateTimeFormat('es-MX',opts).format(d)}
function syncDate(){const k=dayKey(new Date());if(k!==currentDay){currentDay=k;viewDate=new Date();}renderAll()}
function pointsToday(){const r=dayRecord();return data.tasks.reduce((n,t)=>n+(r.done.includes(t.id)?Number(t.points)||0:0),0)}
function renderTasks(){
 const rec=dayRecord();
 const makeTask=t=>`<label class="task ${rec.done.includes(t.id)?'done':''}"><input type="checkbox" data-task="${escapeHtml(t.id)}" ${rec.done.includes(t.id)?'checked':''} aria-label="Completar ${escapeHtml(t.name)}"><span class="task-text"><strong>${escapeHtml(t.name)}</strong><small>${escapeHtml(t.category||'Personal')}</small></span><span class="points">+${Number(t.points)||0} pts</span></label>`;
 $('taskList').innerHTML=data.tasks.map(makeTask).join('');
 $('pendingList').innerHTML=data.tasks.filter(t=>!rec.done.includes(t.id)).map(makeTask).join('') || '<p class="muted">¡No tienes actividades pendientes! 🎉</p>';
 document.querySelectorAll('[data-task]').forEach(el=>el.addEventListener('change',()=>toggleTask(el.dataset.task,el.checked)));
 $('sleepInput').value=rec.sleep??'';
 $('exerciseInput').value=rec.exercise??0;
 $('stepsInput').value=rec.steps??0;
}
function toggleTask(id,checked){
 const r=dayRecord(),had=r.done.includes(id),task=data.tasks.find(t=>t.id===id);if(!task)return;
 if(checked&&!had){r.done.push(id);data.totals.points=(data.totals.points||0)+(Number(task.points)||0);data.totals.tasks=(data.totals.tasks||0)+1}
 if(!checked&&had){r.done=r.done.filter(x=>x!==id);data.totals.points=Math.max(0,(data.totals.points||0)-(Number(task.points)||0));data.totals.tasks=Math.max(0,(data.totals.tasks||0)-1)}
 save();renderAll();
}
function renderStats(){
 const rec=dayRecord(),count=rec.done.length,total=data.tasks.length,earned=pointsToday(),pct=total?Math.round(count/total*100):0;
 $('today').textContent=fmtDate(new Date(),{weekday:'long',day:'numeric',month:'long',year:'numeric'});
 $('dateShort').textContent=fmtDate(new Date(),{day:'numeric',month:'short',year:'numeric'});
 $('earned').textContent=earned;$('completed').textContent=`${count}/${total}`;
 $('sleepSummary').textContent=rec.sleep!==''&&rec.sleep!=null?`${rec.sleep} h`:'—';
 $('exerciseSummary').textContent=`${Number(rec.exercise)||0} min`;
 $('stepsSummary').textContent=(Number(rec.steps)||0).toLocaleString('es-MX');
 const stepPct=Math.min(100,Math.round((Number(rec.steps)||0)/5000*100));
 $('stepsFill').style.width=stepPct+'%';$('stepsBar').setAttribute('aria-valuenow',stepPct);
 $('stepsGoalText').textContent=`${(Number(rec.steps)||0).toLocaleString('es-MX')} de 5,000 pasos (meta de ejemplo)`;
 $('progressFill').style.width=pct+'%';$('progressBar').setAttribute('aria-valuenow',pct);
 $('progressText').textContent=count===total&&total?'¡Terminaste todas tus actividades de hoy! 🎉':`Has completado el ${pct}% de tus actividades. ¡Sigue así!`;
 $('totalPoints').textContent=data.totals.points||0;$('totalTasks').textContent=data.totals.tasks||0;
 const p=data.totals.points||0,level=p>=500?'🏆':p>=200?'⭐':p>=50?'🚀':'🌱';
 $('level').textContent=level;$('levelText').textContent=p>=500?'¡Eres una estrella de los hábitos!':p>=200?'¡Vas genial! Sigue acumulando logros.':p>=50?'¡Buen comienzo! Cada hábito cuenta.':'¡Empieza con una actividad y suma tus primeros puntos!';
 $('todaySummary').textContent=count?`${count} actividades completadas y ${earned} puntos ganados hoy.`:'Aún no has completado actividades.';
 const activeDays=Object.values(data.days).filter(d=>d.done&&d.done.length).length;$('streak').textContent=activeDays;
}
function renderCalendar(){
 const y=viewDate.getFullYear(),m=viewDate.getMonth(),first=new Date(y,m,1),last=new Date(y,m+1,0);
 $('monthTitle').textContent=fmtDate(viewDate,{month:'long',year:'numeric'});
 const grid=$('calendarGrid');grid.innerHTML='';
 ['L','M','X','J','V','S','D'].forEach(x=>{const e=document.createElement('div');e.textContent=x;e.style.cssText='font-size:12px;font-weight:800;color:#69779d;padding:5px 0';grid.appendChild(e)});
 const offset=(first.getDay()+6)%7;
 for(let i=0;i<offset;i++){grid.appendChild(document.createElement('div'))}
 for(let d=1;d<=last.getDate();d++){
  const date=new Date(y,m,d),key=dayKey(date),rec=data.days[key],isToday=key===dayKey(new Date()),done=!!(rec&&rec.done&&rec.done.length);
  const e=document.createElement('div');e.textContent=(done?'✓ ':'')+d;
  e.style.cssText='padding:8px 0;border-radius:10px;font-size:13px;background:'+(isToday?'#243d83':done?'#d9f4e9':'#f2f4ff')+';color:'+(isToday?'white':done?'#276c57':'#263b78')+';font-weight:'+(isToday||done?'800':'500');
  e.title=fmtDate(date,{weekday:'long',day:'numeric',month:'long',year:'numeric'});grid.appendChild(e);
 }
}
function renderAll(){renderTasks();renderStats();renderCalendar()}
document.querySelectorAll('.tab').forEach(btn=>btn.addEventListener('click',()=>{
 document.querySelectorAll('.tab').forEach(b=>b.classList.toggle('active',b===btn));
 ['tasks','calendar','points'].forEach(name=>$(name+'Panel').classList.toggle('hidden',name!==btn.dataset.tab));
}));
$('saveHealth').addEventListener('click',()=>{
 const rec=dayRecord();
 const sleep=$('sleepInput').value,exercise=$('exerciseInput').value,steps=$('stepsInput').value;
 if(sleep!==''&&(Number(sleep)<0||Number(sleep)>24)){ $('healthMessage').textContent='Ingresa horas de sueño entre 0 y 24.';return; }
 if(exercise!==''&&(Number(exercise)<0||Number(exercise)>1440)){ $('healthMessage').textContent='Revisa los minutos de ejercicio.';return; }
 if(steps!==''&&(Number(steps)<0||Number(steps)>200000)){ $('healthMessage').textContent='Revisa la cantidad de pasos.';return; }
 rec.sleep=sleep===''?'':Number(sleep);rec.exercise=Number(exercise)||0;rec.steps=Number(steps)||0;
 save();renderAll();$('healthMessage').textContent='Datos guardados ✓';
});
$('addForm').addEventListener('submit',e=>{
 e.preventDefault();const input=$('newTask'),name=input.value.trim();if(!name)return;
 data.tasks.push({id:'custom_'+Date.now().toString(36),name,points:10,category:'Personal'});input.value='';save();renderAll();
});
$('resetDay').addEventListener('click',()=>{
 if(!confirm('¿Quieres desmarcar todas las actividades de hoy? Los puntos acumulados históricos no se borrarán.'))return;
 const r=dayRecord();
 r.done.forEach(id=>{const t=data.tasks.find(t=>t.id===id);if(t){data.totals.points=Math.max(0,(data.totals.points||0)-(Number(t.points)||0));data.totals.tasks=Math.max(0,(data.totals.tasks||0)-1)}});
 r.done=[];save();renderAll();
});
$('prevMonth').addEventListener('click',()=>{viewDate=new Date(viewDate.getFullYear(),viewDate.getMonth()-1,1);renderCalendar()});
$('nextMonth').addEventListener('click',()=>{viewDate=new Date(viewDate.getFullYear(),viewDate.getMonth()+1,1);renderCalendar()});
// Adaptador de integración: una app nativa autorizada puede enviar datos mediante
// window.postMessage({type:'MIRITMO_HEALTH_DATA', payload:{sleepHours:7.5, exerciseMinutes:30, steps:4200}}).
// Este receptor NO accede por sí solo a sensores; solo acepta datos de un puente instalado.
let nativeConnected=false;
$('connectWatch').addEventListener('click',()=>{
 const brand=$('watchBrand').value;
 const names={wearos:'Wear OS / Health Connect',apple:'Apple HealthKit',garmin:'Garmin Health API',huawei:'Huawei Health Kit',xiaomi:'Xiaomi / Redmi',other:'otro sistema'};
 const bridge=window.MiRitmoBridge;
 if(bridge && typeof bridge.connect==='function'){
   try{
     const result=bridge.connect(brand);
     nativeConnected=true;
     $('connectionStatus').textContent='Solicitud enviada a '+names[brand]+'. Autoriza el acceso en la app complementaria.';
     if(result && typeof result.then==='function') result.catch(()=>{nativeConnected=false;$('connectionStatus').textContent='No se pudo conectar. Revisa la app complementaria y sus permisos.'});
   }catch(e){$('connectionStatus').textContent='No se pudo iniciar la conexión. Revisa la app complementaria.'}
 }else{
   $('connectionStatus').textContent='No se detectó el puente nativo para '+names[brand]+'. La conexión automática todavía no está instalada; puedes seguir usando el registro manual.';
 }
});
$('bluetoothWatch').addEventListener('click',()=>{
 const bridge=window.MiRitmoBridge;
 if(bridge && typeof bridge.scanBluetooth==='function'){
   $('connectionStatus').textContent='Buscando relojes Bluetooth cercanos…';
   try{bridge.scanBluetooth()}catch(e){$('connectionStatus').textContent='No se pudo iniciar la búsqueda Bluetooth.'}
 }else $('connectionStatus').textContent='La búsqueda Bluetooth necesita la versión Android de MiRitmo.';
});
$('disconnectWatch').addEventListener('click',()=>{
 nativeConnected=false;
 try{if(window.MiRitmoBridge&&typeof window.MiRitmoBridge.disconnect==='function')window.MiRitmoBridge.disconnect()}catch(e){}
 $('connectionStatus').textContent='Desconectado. Los datos guardados no se han borrado.';
});
window.addEventListener('message',event=>{
 // A production native wrapper must restrict trusted origins and validate all payloads.
 const msg=event.data;
 if(!msg||msg.type!=='MIRITMO_HEALTH_DATA'||!msg.payload)return;
 const p=msg.payload,rec=dayRecord();
 if(Number.isFinite(Number(p.sleepHours))&&Number(p.sleepHours)>=0&&Number(p.sleepHours)<=24)rec.sleep=Number(p.sleepHours);
 if(Number.isFinite(Number(p.exerciseMinutes))&&Number(p.exerciseMinutes)>=0)rec.exercise=Math.round(Number(p.exerciseMinutes));
 if(Number.isFinite(Number(p.steps))&&Number(p.steps)>=0)rec.steps=Math.round(Number(p.steps));
 if(Number.isFinite(Number(p.heartRateBpm))&&Number(p.heartRateBpm)>0){
   $('heartRateStatus').textContent='Frecuencia cardiaca en vivo: '+Math.round(Number(p.heartRateBpm))+' lpm';
 }
 nativeConnected=true;save();renderAll();
 $('connectionStatus').textContent='Datos recibidos de la integración del reloj ✓';
});
renderAll();
// Revisa la fecha al volver a abrir la app y periódicamente mientras permanece abierta.
document.addEventListener('visibilitychange',()=>{if(!document.hidden)syncDate()});
setInterval(syncDate,60000);
})();
</script>
</body>
</html>