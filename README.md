<!DOCTYPE html><html lang="fr"><head><meta charset="UTF-8"><meta name="viewport" content="width=device-width,initial-scale=1"><title>Portail : Poki • Pulse • YouTube</title>
<style>
:root{--accent:#3ea6ff}
*{box-sizing:border-box;font-family:Arial,sans-serif}body{margin:0;background:#0f0f0f;color:#fff}
nav{display:flex;justify-content:space-between;align-items:center;padding:10px 15px;background:#181818;border-bottom:2px solid var(--accent);position:sticky;top:0;z-index:10;gap:8px;flex-wrap:wrap}
.logo{font-weight:bold;font-size:18px;cursor:pointer;user-select:none;color:var(--accent)}
.tabs{display:flex;gap:6px;flex-wrap:wrap}.tabs button{background:#272727;color:#fff;border:none;padding:8px 14px;border-radius:20px;font-weight:bold;cursor:pointer}.tabs button.on{background:var(--accent);color:#000}
.wrap{max-width:950px;margin:15px auto;padding:0 12px}.tab{display:none}.tab.on{display:block}
.box,.card{background:#1e1e1e;padding:14px;border-radius:12px;margin-bottom:14px;border:1px solid #2a2a2a}
input,textarea{width:100%;background:#121212;border:1px solid #444;color:#fff;padding:9px;border-radius:8px;margin-bottom:8px}
.btn{border:none;padding:8px 14px;border-radius:20px;font-weight:bold;cursor:pointer;color:#fff;margin:2px;font-size:13px}
.grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(275px,1fr));gap:14px}
video,iframe{width:100%;border-radius:8px;background:#000}
.badge{background:var(--accent);color:#000;font-size:11px;padding:1px 5px;border-radius:50%;margin-left:4px;font-weight:bold}
.banner{background:var(--accent);color:#000;text-align:center;padding:8px;font-weight:bold;display:none}
.coms{margin-top:10px;padding-top:8px;border-top:1px solid #333;font-size:13px}
.com-item{background:#141414;padding:6px 10px;border-radius:8px;margin-bottom:5px}
</style></head><body>

<div id="banner" class="banner"></div>

<nav>
  <div class="logo" onclick="tapLogo()">⚡ Mon Portail</div>
  <div class="tabs">
    <button id="b-poki" class="on" onclick="go('poki')">🎮 Mon Poki</button>
    <button id="b-pulse" onclick="go('pulse')">💬 Pulse</button>
    <button id="b-yt" onclick="go('yt')">▶ YouTube</button>
    <button id="b-admin" style="display:none;background:#f4212e;color:#fff" onclick="go('admin')">🛡️ Admin</button>
  </div>
  <input id="usr" placeholder="Ton pseudo..." style="width:140px;margin:0" onchange="localStorage.setItem('u',this.value)">
</nav>

<div id="maintScreen" style="display:none;text-align:center;padding:60px 20px">
  <h1>🚧 Site en maintenance</h1><p style="color:#aaa">L'administrateur met à jour le portail. Reviens vite !</p>
</div>

<div class="wrap" id="mainWrap">
  <div id="t-poki" class="tab on">
    <div class="box"><input id="gn" placeholder="Nom du jeu"><input id="gu" placeholder="Lien URL du jeu HTML5"><button class="btn" style="background:var(--accent);color:#000" onclick="add('poki',{n:gn.value,u:gu.value},[gn,gu])">+ Ajouter un jeu</button></div>
    <div id="gf" style="display:none;margin-bottom:14px"><button class="btn" style="background:#f4212e;margin-bottom:6px" onclick="gf.style.display='none';gp.src=''">✖ Fermer le jeu</button><iframe id="gp" height="480" frameborder="0" allowfullscreen></iframe></div>
    <div class="grid" id="l-poki"></div>
  </div>

  <div id="t-pulse" class="tab">
    <div class="box"><textarea id="pt" rows="2" placeholder="Écris un message public..."></textarea><button class="btn" style="background:var(--accent);color:#000" onclick="add('pulse',{t:pt.value},[pt])">Publier sur Pulse</button></div>
    <div id="l-pulse"></div>
  </div>

  <div id="t-yt" class="tab">
    <div class="box"><input id="vtitle" placeholder="Titre de la vidéo"><input id="vurl" placeholder="Lien direct vidéo (.mp4)"><button class="btn" style="background:var(--accent);color:#000" onclick="add('yt',{t:vtitle.value,u:vurl.value},[vtitle,vurl])">Publier la vidéo</button></div>
    <div class="grid" id="l-yt"></div>
  </div>

  <div id="t-admin" class="tab">
    <div class="box">
      <h3>🎨 Thème & Apparence du Site</h3>
      <button class="btn" style="background:#3ea6ff;color:#000" onclick="setTheme('#3ea6ff')">Bleu</button>
      <button class="btn" style="background:#ff3b30;color:#fff" onclick="setTheme('#ff3b30')">Rouge</button>
      <button class="btn" style="background:#00e676;color:#000" onclick="setTheme('#00e676')">Vert</button>
      <button class="btn" style="background:#bf5af2;color:#fff" onclick="setTheme('#bf5af2')">Violet</button>
      <button class="btn" style="background:#ffd60a;color:#000" onclick="setTheme('#ffd60a')">Or</button>
      <button class="btn" style="background:#444" onclick="const c=prompt('Code couleur HEX (ex: #ff007f):');if(c)setTheme(c)">🖌️ Autre couleur</button>
    </div>
    <div class="box">
      <h3>🛡️ Pouvoirs Administrateur</h3>
      <button class="btn" id="mBtn" style="background:#333" onclick="toggleMaint()">🚧 Maintenance : OFF</button>
      <button class="btn" style="background:#f59e0b;color:#000" onclick="setBanner()">📢 Modifier l'annonce</button>
      <button class="btn" style="background:#1d9bf0" onclick="certUser()">✔️ Certifier un pseudo</button>
      <button class="btn" style="background:#f4212e" onclick="banUser()">🚫 Bannir un pseudo</button>
      <button class="btn" style="background:#555" onclick="changePass()">🔑 Changer MDP Admin</button>
      <button class="btn" style="background:#222" onclick="logoutAdmin()">🔒 Quitter Admin</button>
      <p id="adminInfo" style="color:#aaa;font-size:13px;margin-top:10px"></p>
    </div>
    <div class="box">
      <h4>🧹 Modération & Remise à zéro</h4>
      <button class="btn" style="background:#f4212e" onclick="clearCat('poki')">Vider Poki</button>
      <button class="btn" style="background:#f4212e" onclick="clearCat('pulse')">Vider Pulse</button>
      <button class="btn" style="background:#f4212e" onclick="clearCat('yt')">Vider YouTube</button>
      <button class="btn" style="background:#990000" onclick="resetAll()">💥 TOUT EFFACER (Zéro)</button>
    </div>
  </div>
</div>

<script>
const ROOM = btoa(location.hostname || "local").replace(/[^a-zA-Z0-9]/g, "");
const API = "https://kvdb.io" + ROOM;
let db = JSON.parse(localStorage.getItem('backup_' + ROOM)) || {poki:[], pulse:[], yt:[], cfg:{pass:"admin1234", maint:false, banner:"", theme:"#3ea6ff", bans:[], certs:[]}};
let isAdmin = false, taps = 0;

usr.value = localStorage.getItem('u') || '';
const go = x => {
  document.querySelectorAll('.tab,.tabs button').forEach(e => e.classList.remove('on'));
  document.getElementById('t-' + x).classList.add('on');
  document.getElementById('b-' + x).classList.add('on');
};

function tapLogo(){
  taps++;
  if(taps >= 5){
    taps = 0;
    const p = prompt("Mot de passe Admin :");
    if(p === (db.cfg?.pass || "admin1234")){
      isAdmin = true;
      document.getElementById('b-admin').style.display = 'inline-block';
      go('admin'); render();
    } else if(p !== null) alert("Mot de passe incorrect !");
  }
}

async function pushDB(){
  localStorage.setItem('backup_' + ROOM, JSON.stringify(db));
  render();
  try { await fetch(API, {method:'POST', body:JSON.stringify(db)}); } catch(e) {}
}

async function load() {
  try {
    const r = await fetch(API);
    if (r.ok) {
      const d = await r.json();
      db = {poki:d.poki||[], pulse:d.pulse||[], yt:d.yt||[], cfg:Object.assign({pass:"admin1234",maint:false,banner:"",theme:"#3ea6ff",bans:[],certs:[]}, d.cfg||{})};
      localStorage.setItem('backup_' + ROOM, JSON.stringify(db));
      render();
    }
  } catch(e) { render(); }
}

function checkBan(){
  const u = (usr.value.trim() || 'Anonyme').toLowerCase();
  if((db.cfg.bans||[]).includes(u)){ alert("🚫 Tu es banni de ce site !"); return true; }
  return false;
}

async function add(cat, item, inputs) {
  if(checkBan()) return;
  if (Object.values(item).some(v => !v.trim())) return alert("Remplis tous les champs !");
  item.id = Date.now(); item.user = usr.value.trim() || 'Anonyme'; item.likes = 0; item.coms = [];
  db[cat].unshift(item);
  inputs.forEach(i => i.value = '');
  await pushDB();
}

async function likeItem(cat, id){
  const it = db[cat].find(x => x.id === id);
  if(it){ it.likes = (it.likes || 0) + 1; await pushDB(); }
}

async function addCom(cat, id){
  if(checkBan()) return;
  const txt = prompt("Écris ton commentaire :");
  if(!txt || !txt.trim()) return;
  const it = db[cat].find(x => x.id === id);
  if(it){
    it.coms = it.coms || [];
    it.coms.push({user: usr.value.trim() || 'Anonyme', txt: txt.trim()});
    await pushDB();
  }
}

async function delItem(cat, id){ db[cat] = db[cat].filter(x => x.id !== id); await pushDB(); }
async function clearCat(cat){ if(confirm("Tout effacer dans " + cat + " ?")){ db[cat] = []; await pushDB(); } }
async function resetAll(){ if(confirm("⚠️ Supprimer TOUS les jeux, messages et vidéos ?")){ db.poki=[]; db.pulse=[]; db.yt=[]; localStorage.removeItem('backup_' + ROOM); await pushDB(); alert("Tout est vidé !"); } }
async function setTheme(col){ db.cfg.theme = col; await pushDB(); }
async function toggleMaint(){ db.cfg.maint = !db.cfg.maint; await pushDB(); }
async function setBanner(){ const b = prompt("Texte de l'annonce (vide pour masquer) :", db.cfg.banner); if(b !== null){ db.cfg.banner = b.trim(); await pushDB(); } }
async function changePass(){ const p = prompt("Nouveau mot de passe Admin :"); if(p && p.trim()){ db.cfg.pass = p.trim(); await pushDB(); alert("Mot de passe mis à jour !"); } }
function logoutAdmin(){ isAdmin = false; document.getElementById('b-admin').style.display = 'none'; go('poki'); render(); }

async function certUser(){
  const u = prompt("Pseudo à certifier / décertifier :"); if(!u) return;
  const low = u.trim().toLowerCase();
  db.cfg.certs = db.cfg.certs || [];
  db.cfg.certs = db.cfg.certs.includes(low) ? db.cfg.certs.filter(x=>x!==low) : [...db.cfg.certs, low];
  await pushDB();
}

async function banUser(){
