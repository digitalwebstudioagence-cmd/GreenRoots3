<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no">
<title>GreenRoots</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Fredoka+One&family=Nunito:wght@700;800;900&display=swap');
*{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;}
:root{--g:#3a9e50;--gd:#2d7a3a;--gold:#FFD700;--coin:#F4A320;--soil:#8B6347;--wet:#5a3a20;--panel:rgba(255,255,255,0.96);--sh:0 4px 16px rgba(0,0,0,0.14);--r:16px;}
body{font-family:'Nunito',sans-serif;background:linear-gradient(180deg,#87CEEB 0%,#b8e4f9 38%,#5DBB63 38%,#3a8a40 100%);min-height:100vh;overflow-x:hidden;user-select:none;}

/* HEADER */
#hdr{background:linear-gradient(135deg,#2d7a3a,#1a5c28);padding:10px 14px;display:flex;justify-content:space-between;align-items:center;box-shadow:0 3px 14px rgba(0,0,0,0.3);position:sticky;top:0;z-index:100;}
#hdr h1{font-family:'Fredoka One',cursive;color:#fff;font-size:1.55rem;text-shadow:2px 3px 0 rgba(0,0,0,0.25);}
#hdr h1 b{color:#FFD700;}
.pills{display:flex;gap:7px;}
.pill{background:rgba(255,255,255,0.14);border:1.5px solid rgba(255,255,255,0.22);border-radius:30px;padding:5px 11px;color:#fff;font-weight:800;font-size:0.83rem;display:flex;align-items:center;gap:4px;}
.pill.gld{background:linear-gradient(135deg,#FFD700,#F4A320);color:#5a3800;border-color:#e09000;}

/* XP */
#xpbar{background:rgba(0,0,0,0.2);padding:5px 14px;display:flex;align-items:center;gap:10px;}
#xplbl{font-size:0.7rem;color:rgba(255,255,255,0.9);font-weight:800;min-width:88px;}
#xpbg{flex:1;height:9px;background:rgba(255,255,255,0.2);border-radius:9px;overflow:hidden;}
#xpfill{height:100%;background:linear-gradient(90deg,#FFD700,#ff7000);border-radius:9px;transition:width .5s;}

/* WEATHER */
#wbar{background:rgba(255,255,255,0.13);padding:5px 14px;display:flex;align-items:center;gap:8px;font-size:0.78rem;color:#fff;font-weight:700;}
.wchip{background:rgba(255,255,255,0.18);border-radius:18px;padding:2px 9px;font-size:0.7rem;}

/* DAILY */
#daily{background:linear-gradient(135deg,#FF6B6B,#FF8E53);margin:10px 12px;border-radius:var(--r);padding:12px 16px;display:flex;align-items:center;gap:10px;cursor:pointer;box-shadow:var(--sh);}
#daily:active{opacity:.85;}
#daily .dtxt{flex:1;color:#fff;}
#daily .dtit{font-weight:800;font-size:.92rem;}
#daily .dsub{font-size:.72rem;opacity:.88;}

/* TABS */
#tabs{display:flex;background:rgba(0,0,0,0.12);}
.tab{flex:1;padding:9px 2px;text-align:center;font-weight:800;font-size:0.72rem;color:rgba(255,255,255,0.65);cursor:pointer;border-bottom:3px solid transparent;}
.tab.on{color:#fff;border-bottom-color:#FFD700;background:rgba(255,255,255,0.08);}
.tab span{font-size:1rem;display:block;}

/* PAGES */
.pg{display:none;padding:12px 12px 24px;}
.pg.on{display:block;}

/* FARM TOOLS */
.tools{display:flex;gap:7px;margin-bottom:10px;overflow-x:auto;scrollbar-width:none;padding-bottom:2px;}
.tools::-webkit-scrollbar{display:none;}
.tbtn{flex-shrink:0;background:var(--panel);border-radius:28px;padding:7px 13px;font-size:0.78rem;font-weight:800;cursor:pointer;box-shadow:var(--sh);border:2.5px solid transparent;white-space:nowrap;}
.tbtn.on{border-color:var(--g);background:#eafaea;color:#1a5c28;}
.tbtn:active{transform:scale(0.93);}

/* FARM GRID */
#fgrid{display:grid;grid-template-columns:repeat(5,1fr);gap:6px;max-width:420px;margin:0 auto;}
.plot{aspect-ratio:1/1;border-radius:12px;border:3px solid #6B4226;cursor:pointer;display:flex;flex-direction:column;align-items:center;justify-content:center;position:relative;overflow:hidden;box-shadow:0 3px 7px rgba(0,0,0,0.18),inset 0 -3px 0 rgba(0,0,0,0.1);transition:transform .15s;}
.plot:active{transform:scale(0.88);}
.pe{font-size:1.6rem;line-height:1;filter:drop-shadow(1px 2px 1px rgba(0,0,0,0.25));}
.ptm{font-size:0.52rem;font-weight:900;color:#fff;text-shadow:1px 1px 0 rgba(0,0,0,0.6);margin-top:1px;}
.pbar{position:absolute;bottom:0;left:0;height:4px;background:linear-gradient(90deg,#4CAF50,#8BC34A);}
.wd{position:absolute;top:3px;right:3px;font-size:.7rem;}
.fb{position:absolute;top:3px;left:3px;font-size:.7rem;}
/* plot states */
.p0{background:var(--soil);}
.p1{background:var(--wet);}
.p2{background:var(--wet);}
.p3{background:var(--wet);border-color:#FFD700;animation:glow .9s ease-in-out infinite alternate;}
.p4{background:#3a2010;border-color:#c0392b;}
.plk{background:#9e8070;border-color:#7a5e4a;opacity:.75;}
.plkp{font-size:0.52rem;font-weight:800;color:#FFD700;text-shadow:1px 1px 0 rgba(0,0,0,.5);}
@keyframes glow{from{box-shadow:0 3px 7px rgba(0,0,0,.2),0 0 5px rgba(255,215,0,.3);}to{box-shadow:0 3px 7px rgba(0,0,0,.2),0 0 20px rgba(255,215,0,.8);}}
.p3 .pe{animation:bop .5s ease infinite alternate;}
@keyframes bop{from{transform:translateY(0);}to{transform:translateY(-5px);}}
#thint{font-size:0.72rem;color:rgba(255,255,255,.85);font-weight:700;text-align:center;padding:8px 0 0;}

/* SHOP */
.stit{font-family:'Fredoka One',cursive;color:#fff;font-size:.98rem;text-shadow:1px 2px 0 rgba(0,0,0,.25);background:rgba(0,0,0,.14);padding:4px 13px;border-radius:18px;display:inline-block;margin-bottom:9px;}
.sgrid{display:grid;grid-template-columns:repeat(3,1fr);gap:7px;margin-bottom:14px;}
.sc{background:var(--panel);border-radius:var(--r);padding:9px 7px;text-align:center;cursor:pointer;box-shadow:var(--sh);border:3px solid transparent;position:relative;}
.sc:active{transform:scale(0.93);}
.sc.sel{border-color:var(--g);background:#eafbea;}
.sc.lk{opacity:.5;filter:grayscale(.8);cursor:default;}
.sc .se{font-size:1.8rem;display:block;margin-bottom:2px;}
.sc .sn{font-size:.68rem;font-weight:800;color:#333;}
.sc .sp{font-size:.68rem;color:var(--coin);font-weight:800;}
.sc .st{font-size:.6rem;color:#999;}
.sc .ss{font-size:.62rem;color:var(--g);font-weight:700;}
.lkbg{position:absolute;top:3px;right:5px;font-size:.58rem;background:#e74c3c;color:#fff;border-radius:7px;padding:1px 4px;font-weight:800;}

/* MARKET */
.igrid{display:grid;grid-template-columns:repeat(2,1fr);gap:8px;}
.ic{background:var(--panel);border-radius:var(--r);padding:11px;cursor:pointer;box-shadow:var(--sh);display:flex;align-items:center;gap:9px;}
.ic:active{transform:scale(0.95);}
.ic .ie{font-size:1.9rem;}
.ic .in{font-weight:800;font-size:.82rem;color:#333;}
.ic .iq{font-size:.72rem;color:#666;}
.ic .ipr{font-size:.74rem;color:var(--coin);font-weight:800;}
.sabtn{background:linear-gradient(135deg,#FFD700,#F4A320);border-radius:var(--r);padding:13px;text-align:center;font-family:'Fredoka One',cursive;font-size:1rem;color:#5a3800;cursor:pointer;box-shadow:var(--sh);margin-bottom:11px;}
.sabtn:active{transform:scale(0.97);}

/* UPGRADES */
.ugc{background:var(--panel);border-radius:var(--r);padding:13px;margin-bottom:9px;display:flex;align-items:center;gap:11px;box-shadow:var(--sh);cursor:pointer;}
.ugc:active{transform:scale(0.98);}
.ugc.mx{opacity:.6;cursor:default;}
.ugc .ui{font-size:2rem;flex-shrink:0;}
.ugc .un{font-weight:800;font-size:.9rem;color:#222;}
.ugc .ud{font-size:.72rem;color:#666;margin-top:2px;}
.ugc .ul{font-size:.68rem;color:var(--g);font-weight:800;margin-top:2px;}
.ugc .uc{flex-shrink:0;background:linear-gradient(135deg,#FFD700,#F4A320);border-radius:18px;padding:5px 11px;font-weight:800;font-size:.82rem;color:#5a3800;}
.ugc .uc.na{background:#ddd;color:#888;}

/* ACHIEVEMENTS */
.acc{background:var(--panel);border-radius:var(--r);padding:11px 13px;margin-bottom:8px;display:flex;align-items:center;gap:9px;box-shadow:var(--sh);}
.acc.lka{opacity:.4;filter:grayscale(1);}
.acc .ai{font-size:1.8rem;}
.acc .an{font-weight:800;color:#222;font-size:.87rem;}
.acc .ad{font-size:.72rem;color:#666;}
.acc .ack{margin-left:auto;font-size:1.2rem;}

/* TOAST */
#toast{position:fixed;top:72px;left:50%;transform:translateX(-50%) translateY(-18px);background:rgba(20,20,20,.93);color:#fff;padding:9px 20px;border-radius:28px;font-weight:800;font-size:.84rem;opacity:0;transition:all .3s;z-index:9999;pointer-events:none;white-space:nowrap;max-width:90vw;text-align:center;}
#toast.on{opacity:1;transform:translateX(-50%) translateY(0);}

/* FLOAT */
.ffx{position:fixed;font-weight:800;font-size:.95rem;pointer-events:none;animation:fup 1.2s ease-out forwards;z-index:9999;}
@keyframes fup{0%{opacity:1;transform:translateY(0) scale(1);}100%{opacity:0;transform:translateY(-80px) scale(1.3);}}

/* MODAL */
#mover{position:fixed;inset:0;background:rgba(0,0,0,.5);z-index:600;display:none;align-items:center;justify-content:center;}
#mover.on{display:flex;}
#mdl{background:#fff;border-radius:22px;padding:22px;max-width:310px;width:90%;text-align:center;box-shadow:0 18px 50px rgba(0,0,0,.3);}
#mdl h3{font-family:'Fredoka One',cursive;font-size:1.3rem;color:#2d7a3a;margin-bottom:7px;}
#mdl p{font-size:.87rem;color:#555;margin-bottom:16px;line-height:1.5;}
.mbtns{display:flex;gap:9px;}
.mbtns button{flex:1;padding:11px;border-radius:13px;border:none;font-family:'Nunito',sans-serif;font-weight:800;font-size:.9rem;cursor:pointer;}
.mbtns button:active{transform:scale(0.96);}
.mok{background:linear-gradient(135deg,#FFD700,#F4A320);color:#5a3800;}
.mno{background:#eee;color:#666;}
</style>
</head>
<body>

<div id="hdr">
  <h1>Green<b>Roots</b> &#127807;</h1>
  <div class="pills">
    <div class="pill">&#11088; Niv.<span id="hlv">1</span></div>
    <div class="pill gld">&#129689; <span id="hmn">50</span></div>
  </div>
</div>
<div id="xpbar">
  <div id="xplbl">XP: 0/100</div>
  <div id="xpbg"><div id="xpfill" style="width:0%"></div></div>
</div>
<div id="wbar">
  <span id="wi">&#9728;&#65039;</span>
  <span id="wn">Ensoleill&eacute;</span>
  <span id="wb" class="wchip">Normal</span>
  <span id="sc" class="wchip" style="margin-left:auto">&#127800; Printemps</span>
</div>
<div id="daily" onclick="claimDaily()">
  <div style="font-size:2rem">&#127873;</div>
  <div class="dtxt">
    <div class="dtit">R&eacute;compense du jour !</div>
    <div id="dsub" class="dsub">Cliquez pour r&eacute;clamer</div>
  </div>
  <div style="color:white;font-size:1.3rem">&#8250;</div>
</div>

<div id="tabs">
  <div class="tab on" onclick="goTab('farm')"><span>&#127806;</span>Ferme</div>
  <div class="tab" onclick="goTab('shop')"><span>&#127793;</span>Graines</div>
  <div class="tab" onclick="goTab('market')"><span>&#127978;</span>March&eacute;</div>
  <div class="tab" onclick="goTab('upg')"><span>&#9889;</span>Amélior.</div>
  <div class="tab" onclick="goTab('ach')"><span>&#127942;</span>Troph&eacute;es</div>
</div>

<!-- FARM -->
<div id="farm" class="pg on">
  <div class="tools">
    <div class="tbtn on" id="tb-plant" onclick="setTool('plant')">&#127793; Planter</div>
    <div class="tbtn" id="tb-water" onclick="setTool('water')">&#128167; Arroser (<span id="wc">3</span>)</div>
    <div class="tbtn" id="tb-fert" onclick="setTool('fert')">&#129514; Engrais (<span id="fc">1</span>)</div>
    <div class="tbtn" id="tb-harvest" onclick="setTool('harvest')">&#129530; R&eacute;colter</div>
    <div class="tbtn" id="tb-del" onclick="setTool('del')">&#128465;&#65039; Supprimer</div>
  </div>
  <div id="fgrid"></div>
  <div id="thint">Choisissez une graine dans <b>Graines</b> puis tapez sur une parcelle vide !</div>
</div>

<!-- SHOP -->
<div id="shop" class="pg">
  <div class="stit">&#127793; Graines</div>
  <div id="sgr" class="sgrid"></div>
  <div class="stit">&#127795; Arbres fruitiers</div>
  <div id="tgr" class="sgrid"></div>
  <div class="stit">&#127812; Sp&eacute;ciaux</div>
  <div id="xgr" class="sgrid"></div>
</div>

<!-- MARKET -->
<div id="market" class="pg">
  <div id="minfo"></div>
  <div id="sabw"></div>
  <div id="igrid" class="igrid"></div>
  <div id="noinv" style="display:none;color:rgba(255,255,255,.8);text-align:center;padding:30px;font-weight:700;font-size:.95rem;">&#127806; Rien &agrave; vendre<br><small>Allez r&eacute;colter !</small></div>
</div>

<!-- UPGRADES -->
<div id="upg" class="pg"><div id="ulist"></div></div>

<!-- ACHIEVEMENTS -->
<div id="ach" class="pg"><div id="alist"></div></div>

<div id="toast"></div>
<div id="mover">
  <div id="mdl">
    <h3 id="mt">D&eacute;bloquer ?</h3>
    <p id="mb"></p>
    <div class="mbtns">
      <button class="mno" onclick="closeM()">Annuler</button>
      <button class="mok" id="mok">Confirmer</button>
    </div>
  </div>
</div>

<script>
// ========== EMOJIS (all unicode escaped) ==========
var E={
  carrot:"\uD83E\uDD55",wheat:"\uD83C\uDF3E",potato:"\uD83E\uDD54",
  tomato:"\uD83C\uDF45",corn:"\uD83C\uDF3D",pepper:"\uD83C\uDF36\uFE0F",
  eggplant:"\uD83C\uDF46",pumpkin:"\uD83C\uDF83",broccoli:"\uD83E\uDD66",
  garlic:"\uD83E\uDDC4",onion:"\uD83E\uDDC5",strawberry:"\uD83C\uDF53",
  apple:"\uD83C\uDF4E",lemon:"\uD83C\uDF4B",orange:"\uD83C\uDF4A",
  cherry:"\uD83C\uDF52",coconut:"\uD83E\uDD65",
  mushroom:"\uD83C\uDF44",cactus:"\uD83C\uDF35",sunflower:"\uD83C\uDF3B",
  tulip:"\uD83C\uDF37",fourleaf:"\uD83C\uDF40",golden:"\u2728",
  coin:"\uD83E\uDE99",star:"\u2B50",lock:"\uD83D\uDD12",
  sprout:"\uD83C\uDF31",dead:"\uD83D\uDC80",
  water:"\uD83D\uDCA7",fert:"\uD83E\uDDEA",check:"\u2705",
  sun:"\u2600\uFE0F",cloud:"\u26C5",rain:"\uD83C\uDF27\uFE0F",
  wind:"\uD83C\uDF2C\uFE0F",hot:"\uD83C\uDF21\uFE0F",fog:"\uD83C\uDF2B\uFE0F",storm:"\u26C8\uFE0F",
  spring:"\uD83C\uDF38",autumn:"\uD83C\uDF42",winter:"\u2744\uFE0F",
  spd:"\u26A1",cash:"\uD83D\uDCB0",book:"\uD83D\uDCDA",luck:"\uD83C\uDF40",
  trophy:"\uD83C\uDFC6",gear:"\u2699\uFE0F",farmer:"\uD83D\uDC68\u200D\uD83C\uDF3E",
  house:"\uD83C\uDFE1",gem:"\uD83D\uDC8E",rich:"\uD83E\uDD11",
  map:"\uD83D\uDDFA\uFE0F",cal:"\uD83D\uDCC5",gift:"\uD83C\uDF81",
  party:"\uD83C\uDF89",basket:"\uD83E\uDDFA",trash:"\uD83D\uDDD1\uFE0F",
  store:"\uD83C\uDFEA",tree:"\uD83C\uDF33",herb:"\uD83C\uDF3F",
  warn:"\u26A0\uFE0F",ok:"\u2705"
};

// ========== CROPS ==========
var CROPS=[
  {id:"carrot",   name:"Carotte",    cat:"seed", unl:1,  cost:5,   sell:12,  grow:15,  xp:8,  season:null},
  {id:"wheat",    name:"Ble",        cat:"seed", unl:1,  cost:8,   sell:20,  grow:22,  xp:12, season:null},
  {id:"potato",   name:"Pomme T.",   cat:"seed", unl:2,  cost:10,  sell:27,  grow:30,  xp:16, season:null},
  {id:"tomato",   name:"Tomate",     cat:"seed", unl:2,  cost:14,  sell:36,  grow:42,  xp:22, season:null},
  {id:"corn",     name:"Mais",       cat:"seed", unl:3,  cost:18,  sell:50,  grow:58,  xp:30, season:"summer"},
  {id:"pepper",   name:"Piment",     cat:"seed", unl:4,  cost:22,  sell:62,  grow:68,  xp:36, season:null},
  {id:"eggplant", name:"Aubergine",  cat:"seed", unl:5,  cost:26,  sell:74,  grow:78,  xp:42, season:null},
  {id:"pumpkin",  name:"Citrouille", cat:"seed", unl:6,  cost:30,  sell:90,  grow:92,  xp:50, season:"autumn"},
  {id:"broccoli", name:"Brocoli",    cat:"seed", unl:6,  cost:28,  sell:82,  grow:88,  xp:46, season:null},
  {id:"garlic",   name:"Ail",        cat:"seed", unl:7,  cost:36,  sell:104, grow:104, xp:56, season:null},
  {id:"onion",    name:"Oignon",     cat:"seed", unl:7,  cost:33,  sell:95,  grow:98,  xp:52, season:null},
  {id:"strawberry",name:"Fraise",    cat:"seed", unl:8,  cost:42,  sell:118, grow:115, xp:62, season:"spring"},
  {id:"apple",    name:"Pommier",    cat:"tree", unl:5,  cost:80,  sell:55,  grow:180, xp:80, season:null,   qty:3},
  {id:"lemon",    name:"Citronnier", cat:"tree", unl:7,  cost:100, sell:68,  grow:220, xp:100,season:null,   qty:3},
  {id:"orange",   name:"Oranger",    cat:"tree", unl:9,  cost:120, sell:78,  grow:250, xp:120,season:null,   qty:4},
  {id:"cherry",   name:"Cerisier",   cat:"tree", unl:11, cost:150, sell:92,  grow:300, xp:150,season:"spring",qty:4},
  {id:"coconut",  name:"Cocotier",   cat:"tree", unl:13, cost:200, sell:125, grow:360, xp:200,season:"summer",qty:5},
  {id:"mushroom", name:"Champignon", cat:"spec", unl:6,  cost:60,  sell:165, grow:135, xp:92, season:"autumn"},
  {id:"cactus",   name:"Cactus",     cat:"spec", unl:8,  cost:76,  sell:205, grow:155, xp:112,season:"summer"},
  {id:"sunflower",name:"Tournesol",  cat:"spec", unl:10, cost:92,  sell:245, grow:175, xp:132,season:"summer"},
  {id:"tulip",    name:"Tulipe",     cat:"spec", unl:11, cost:112, sell:295, grow:205, xp:152,season:"spring"},
  {id:"fourleaf", name:"Trefle",     cat:"spec", unl:14, cost:180, sell:500, grow:300, xp:250,season:null},
  {id:"golden",   name:"Graine Or",  cat:"spec", unl:20, cost:500, sell:2000,grow:600, xp:1000,season:null}
];

var PCOST=[0,0,0,0,0,40,40,55,55,70,90,90,110,110,140,170,170,200,220,250,300,340,380,430,500,580,660,750,850,960,1100,1280,1460,1640,1820,2000,2300,2600,2950,3400];
var NP=40;

var UPGRADES=[
  {id:"spd", name:"Engrais de base",  icon:"spd",  desc:"Pousse +20% / niveau", maxLv:5, base:80,  fx:"speed"},
  {id:"sel", name:"Bazar ameliore",   icon:"cash", desc:"Vente +15% / niveau",  maxLv:5, base:120, fx:"sell"},
  {id:"wat", name:"Arrosoir magique", icon:"water",desc:"+2 charges eau",        maxLv:5, base:100, fx:"water"},
  {id:"frt", name:"Usine engrais",    icon:"fert", desc:"+1 engrais / niveau",   maxLv:5, base:150, fx:"fert"},
  {id:"hrv", name:"Super Recolte",    icon:"basket",desc:"+1 item recolte",      maxLv:3, base:200, fx:"harvest"},
  {id:"xpb", name:"Livre jardinage",  icon:"book", desc:"XP +25% / niveau",      maxLv:4, base:160, fx:"xp"},
  {id:"lck", name:"Trefle chanceux",  icon:"luck", desc:"Double recolte 8%",     maxLv:3, base:300, fx:"luck"}
];

var ACHS=[
  {id:"h1",  ic:"sprout", name:"Premier Pas",        desc:"1ere recolte",              ok:function(s){return s.th>=1;}},
  {id:"h10", ic:"farmer", name:"Petit Fermier",       desc:"10 recoltes",               ok:function(s){return s.th>=10;}},
  {id:"h100",ic:"house",  name:"Grand Fermier",       desc:"100 recoltes",              ok:function(s){return s.th>=100;}},
  {id:"h500",ic:"star",   name:"Maitre Fermier",      desc:"500 recoltes",              ok:function(s){return s.th>=500;}},
  {id:"m1",  ic:"coin",   name:"Econome",             desc:"100 pieces en banque",      ok:function(s){return s.money>=100;}},
  {id:"m2",  ic:"gem",    name:"Riche Fermier",       desc:"1000 pieces en banque",     ok:function(s){return s.money>=1000;}},
  {id:"m3",  ic:"rich",   name:"Millionnaire",        desc:"10000 pieces en banque",    ok:function(s){return s.money>=10000;}},
  {id:"l5",  ic:"star",   name:"Apprenti",            desc:"Niveau 5",                  ok:function(s){return s.lv>=5;}},
  {id:"l10", ic:"star",   name:"Confirme",            desc:"Niveau 10",                 ok:function(s){return s.lv>=10;}},
  {id:"l20", ic:"star",   name:"Expert",              desc:"Niveau 20",                 ok:function(s){return s.lv>=20;}},
  {id:"u20", ic:"map",    name:"Grand Proprietaire",  desc:"20 terrains debloques",     ok:function(s){return s.plots.filter(function(p){return !p.lk;}).length>=20;}},
  {id:"ugm", ic:"gear",   name:"Ingenieur",           desc:"Amelioration au maximum",   ok:function(s){return Object.values(s.upg||{}).some(function(v){return v>=5;});}},
  {id:"ty",  ic:"herb",   name:"Botaniste",           desc:"10 types plantes differents",ok:function(s){return (s.pt||[]).length>=10;}},
  {id:"d7",  ic:"cal",    name:"Assidu",              desc:"7 recompenses de suite",    ok:function(s){return (s.ds||0)>=7;}}
];

var WEATHERS=[
  {id:"sun",  name:"Ensoleille", ic:E.sun,   desc:"Normal",        sm:1.0},
  {id:"cld",  name:"Nuageux",    ic:E.cloud, desc:"Pousse -10%",   sm:0.9},
  {id:"rain", name:"Pluvieux",   ic:E.rain,  desc:"Auto-arrosage", sm:1.3, aw:true},
  {id:"wnd",  name:"Venteux",    ic:E.wind,  desc:"Vente +20%",    sm:1.0, sv:1.2},
  {id:"hot",  name:"Canicule",   ic:E.hot,   desc:"Fletrit vite",  sm:1.4, wf:true},
  {id:"fog",  name:"Brumeux",    ic:E.fog,   desc:"Normal",        sm:1.0},
  {id:"stm",  name:"Orageux",    ic:E.storm, desc:"Pousse +30%",   sm:1.6}
];
var SEASONS=["spring","summer","autumn","winter"];
var SNAMES={spring:E.spring+" Printemps",summer:E.sun+" Ete",autumn:E.autumn+" Automne",winter:E.winter+" Hiver"};
var SBONUS={spring:1.1,summer:1.2,autumn:1.0,winter:0.8};

// ========== STATE ==========
function defState(){
  var plots=[];
  for(var i=0;i<NP;i++) plots.push({id:i,lk:i>=8,pl:null,pa:null,wt:false,ft:false,wi:false});
  return {money:50,lv:1,xp:0,xpn:100,sel:"carrot",tool:"plant",th:0,te:0,wc:3,mwc:3,frc:1,mfc:1,upg:{},achs:[],pt:[],ds:0,ld:null,lwc:0,wi:0,si:0,sd:0,inv:{},plots:plots};
}

var S=(function(){
  try{
    var r=localStorage.getItem("gr5");
    if(r){
      var p=JSON.parse(r);
      while(p.plots.length<NP) p.plots.push({id:p.plots.length,lk:true,pl:null,pa:null,wt:false,ft:false,wi:false});
      if(!p.inv) p.inv={};
      if(!p.upg) p.upg={};
      if(!p.achs) p.achs=[];
      if(!p.pt) p.pt=[];
      return p;
    }
  }catch(e){}
  return defState();
})();

function sv(){try{localStorage.setItem("gr5",JSON.stringify(S));}catch(e){}}
function gc(id){for(var i=0;i<CROPS.length;i++) if(CROPS[i].id===id) return CROPS[i]; return null;}
function gu(id){return S.upg[id]||0;}
function smul(){var m=1+gu("spd")*0.2; m*=SBONUS[SEASONS[S.si]]; m*=WEATHERS[S.wi].sm; return m;}
function vmul(){var m=1+gu("sel")*0.15; if(WEATHERS[S.wi].sv) m*=WEATHERS[S.wi].sv; return m;}
function xmul(){return 1+gu("xpb")*0.25;}
function lchance(){return gu("lck")*0.08;}

function pstate(p){
  if(!p.pl) return 0;
  if(p.wi) return 4;
  var c=gc(p.pl), el=(Date.now()-p.pa)/1000*smul();
  if(el<c.grow*0.3) return 1;
  if(el<c.grow) return 2;
  return 3;
}
function ppct(p){
  if(!p.pl) return 0;
  var c=gc(p.pl);
  return Math.min(100,((Date.now()-p.pa)/1000*smul()/c.grow)*100);
}

// Toast
function toast(msg){
  var t=document.getElementById("toast");
  t.textContent=msg; t.classList.add("on");
  clearTimeout(t._t); t._t=setTimeout(function(){t.classList.remove("on");},2200);
}
// Float FX
function ffx(x,y,txt,col){
  var el=document.createElement("div");
  el.className="ffx"; el.textContent=txt; el.style.color=col||"#FFD700";
  el.style.left=x+"px"; el.style.top=y+"px";
  document.body.appendChild(el);
  setTimeout(function(){if(el.parentNode)el.parentNode.removeChild(el);},1300);
}
// XP
function gxp(amt){
  S.xp+=Math.round(amt*xmul());
  while(S.xp>=S.xpn){S.xp-=S.xpn;S.lv++;S.xpn=Math.round(S.xpn*1.4+50);toast(E.party+" Niveau "+S.lv+" !");}
  checkAchs();
}
// Money
function gmoney(amt){var r=Math.round(amt*vmul());S.money+=r;return r;}

// Weather
function tickW(){
  var now=Date.now();
  if(now-S.lwc>180000){
    S.lwc=now; S.wi=Math.floor(Math.random()*WEATHERS.length);
    S.sd=(S.sd||0)+1; if(S.sd>30){S.sd=0;S.si=(S.si+1)%4;}
    var w=WEATHERS[S.wi];
    if(w.aw){S.plots.forEach(function(p){if(p.pl&&!p.wi)p.wt=true;});toast(E.rain+" Pluie ! Arrosage auto !");}
    drawWeather();
  }
  if(WEATHERS[S.wi].wf){
    S.plots.forEach(function(p){if(p.pl&&!p.wt&&!p.wi&&pstate(p)===2&&Math.random()<0.004)p.wi=true;});
  }
}
function drawWeather(){
  var w=WEATHERS[S.wi];
  document.getElementById("wi").textContent=w.ic;
  document.getElementById("wn").textContent=w.name;
  document.getElementById("wb").textContent=w.desc;
  document.getElementById("sc").textContent=SNAMES[SEASONS[S.si]];
}

// Daily
function checkDaily(){
  var today=new Date().toDateString();
  if(S.ld===today){
    document.getElementById("dsub").textContent="Reviens demain !";
    document.getElementById("daily").style.opacity="0.55";
  } else {
    document.getElementById("dsub").textContent=E.gift+" Disponible ! Cliquez !";
    document.getElementById("daily").style.opacity="1";
  }
}
function claimDaily(){
  var today=new Date().toDateString();
  if(S.ld===today){toast("Deja reclame !"); return;}
  var yest=new Date(Date.now()-86400000).toDateString();
  S.ds=(S.ld===yest)?(S.ds||0)+1:1;
  S.ld=today;
  var r=Math.round(25+S.ds*15+Math.random()*30);
  S.money+=r; S.wc=S.mwc; S.frc=S.mfc;
  toast(E.gift+" +"+E.coin+r+" | Serie: "+S.ds+" jour(s) !");
  checkAchs(); sv(); drawAll();
}

// Tabs
var curTab="farm";
function goTab(t){
  curTab=t;
  var ids=["farm","shop","market","upg","ach"];
  document.querySelectorAll(".tab").forEach(function(el,i){el.classList.toggle("on",ids[i]===t);});
  document.querySelectorAll(".pg").forEach(function(el){el.classList.remove("on");});
  document.getElementById(t).classList.add("on");
  if(t==="market") drawMarket();
  if(t==="upg") drawUpg();
  if(t==="ach") drawAch();
  if(t==="shop") drawShop();
}

// Shop
function drawShop(){
  drawSec("seed","sgr"); drawSec("tree","tgr"); drawSec("spec","xgr");
}
function drawSec(cat,gid){
  var g=document.getElementById(gid); g.innerHTML="";
  var ssn=SEASONS[S.si];
  CROPS.forEach(function(c){
    if(c.cat!==cat) return;
    var lk=c.unl>S.lv;
    var div=document.createElement("div");
    div.className="sc"+(lk?" lk":"")+(S.sel===c.id?" sel":"");
    var snote="";
    if(c.season) snote="<div style=\"font-size:.6rem;color:"+(c.season!==ssn?"#e74c3c":"#27ae60")+"\">"+( c.season!==ssn?E.warn+" Hors saison":E.ok+" En saison")+"</div>";
    div.innerHTML="<span class=\"se\">"+E[c.id]+"</span>"
      +"<div class=\"sn\">"+c.name+"</div>"
      +"<div class=\"sp\">"+E.coin+c.cost+"</div>"
      +"<div class=\"st\">"+c.grow+"s</div>"
      +"<div class=\"ss\">Vente "+c.sell+"</div>"
      +snote+(lk?"<div class=\"lkbg\">Niv."+c.unl+"</div>":"");
    if(!lk){
      (function(crop){
        div.addEventListener("click",function(){
          S.sel=crop.id; drawShop(); goTab("farm");
          toast(E[crop.id]+" "+crop.name+" selectionne !");
        });
      })(c);
    }
    g.appendChild(div);
  });
}

// Tools
function setTool(t){
  S.tool=t;
  document.querySelectorAll(".tbtn").forEach(function(b){b.classList.remove("on");});
  document.getElementById("tb-"+t).classList.add("on");
  var hints={plant:"Tapez une parcelle vide pour planter",water:"Tapez une plante pour l'arroser",fert:"Tapez une plante pour l'engraisser (2x plus vite)",harvest:"Tapez une plante prete (brillante) pour recolter",del:"Tapez une parcelle pour la vider"};
  document.getElementById("thint").textContent=hints[t]||"";
}

// Farm
function drawFarm(){
  var g=document.getElementById("fgrid"); g.innerHTML="";
  S.plots.forEach(function(p,idx){
    var el=document.createElement("div"); el.className="plot";
    if(p.lk){
      var cost=PCOST[p.id]||9999;
      el.classList.add("plk");
      el.innerHTML="<span style=\"font-size:1.3rem;\">"+E.lock+"</span><span class=\"plkp\">"+E.coin+cost+"</span>";
      (function(pid){el.addEventListener("click",function(){tryUnlock(pid);});})(p.id);
    } else {
      var ps=pstate(p);
      el.classList.add("p"+ps);
      if(p.pl){
        var c=gc(p.pl);
        var pct=ppct(p);
        var el2=(Date.now()-p.pa)/1000*smul();
        var rem=Math.max(0,Math.ceil(c.grow-el2));
        el.innerHTML="<span class=\"pe\">"+(p.wi?E.dead:E[c.id])+"</span>";
        if(ps!==3&&!p.wi) el.innerHTML+="<div class=\"ptm\">"+(rem>0?rem+"s":"Pret!")+"</div><div class=\"pbar\" style=\"width:"+pct+"%\"></div>";
        if(p.wt) el.innerHTML+="<span class=\"wd\">"+E.water+"</span>";
        if(p.ft) el.innerHTML+="<span class=\"fb\">"+E.fert+"</span>";
      } else {
        el.innerHTML="<span style=\"font-size:1.4rem;opacity:.2\">+</span>";
      }
      (function(pid){el.addEventListener("click",function(ev){clickPlot(pid,ev);});})(p.id);
    }
    g.appendChild(el);
  });
  document.getElementById("wc").textContent=S.wc;
  document.getElementById("fc").textContent=S.frc;
}

function clickPlot(id,ev){
  var p=S.plots[id];
  var ps=pstate(p);
  var rect=ev.currentTarget.getBoundingClientRect();
  var cx=rect.left+rect.width/2, cy=rect.top;

  if(S.tool==="plant"){
    if(ps!==0){toast("Parcelle deja occupee !"); return;}
    var c=gc(S.sel);
    if(!c){toast("Choisissez une graine d abord !"); return;}
    if(c.unl>S.lv){toast(E.lock+" Niveau "+c.unl+" requis !"); return;}
    if(S.money<c.cost){toast("Pas assez ! Besoin: "+E.coin+c.cost); return;}
    S.money-=c.cost; p.pl=c.id; p.pa=Date.now(); p.wt=false; p.ft=false; p.wi=false;
    if(S.pt.indexOf(c.id)<0) S.pt.push(c.id);
    ffx(cx,cy,E.sprout+" Plante !","#4CAF50");
  } else if(S.tool==="water"){
    if(!p.pl||p.wi){toast("Rien a arroser !"); return;}
    if(p.wt){toast("Deja arrose !"); return;}
    if(S.wc<=0){toast("Plus d'eau ! Revenez demain."); return;}
    S.wc--; p.wt=true; ffx(cx,cy,E.water+" Arrose !","#2196F3");
  } else if(S.tool==="fert"){
    if(!p.pl||p.wi){toast("Rien a engraisser !"); return;}
    if(p.ft){toast("Deja engraisse !"); return;}
    if(S.frc<=0){toast("Plus d'engrais ! Revenez demain."); return;}
    S.frc--; p.ft=true;
    var c2=gc(p.pl), el3=(Date.now()-p.pa)/1000, rem3=c2.grow-el3*smul();
    if(rem3>0) p.pa=Date.now()-(el3+rem3*0.5/smul())*1000;
    ffx(cx,cy,E.fert+" x2 !","#9C27B0");
  } else if(S.tool==="harvest"){
    if(ps!==3){
      if(p.pl&&!p.wi){var c3=gc(p.pl),el4=(Date.now()-p.pa)/1000*smul();toast("Encore "+Math.max(0,Math.ceil(c3.grow-el4))+"s...");}
      else if(p.wi) toast("Plante fletrie ! Supprimer avec poubelle.");
      else toast("Rien a recolter !");
      return;
    }
    var c4=gc(p.pl);
    var qty=1+(c4.qty?c4.qty-1:0)+(gu("hrv")>0&&Math.random()<0.5?1:0);
    if(Math.random()<lchance()) qty*=2;
    S.inv[c4.id]=(S.inv[c4.id]||0)+qty;
    S.th++; gxp(c4.xp*qty);
    ffx(cx,cy,E[c4.id]+" +"+qty,"#FFD700");
    p.pl=null; p.pa=null; p.wt=false; p.ft=false; p.wi=false;
  } else if(S.tool==="del"){
    if(!p.pl&&ps===0){toast("Parcelle deja vide !"); return;}
    p.pl=null; p.pa=null; p.wt=false; p.ft=false; p.wi=false;
    ffx(cx,cy,E.trash,"#e74c3c");
  }
  checkAchs(); sv(); drawFarm(); updHdr();
}

function tryUnlock(id){
  var cost=PCOST[id]||9999;
  openM("Debloquer terrain #"+(id+1),"Cout: "+E.coin+cost+"   Solde: "+E.coin+S.money,function(){
    if(S.money<cost){toast("Pas assez de pieces !"); return;}
    S.money-=cost; S.plots[id].lk=false;
    toast(E.sprout+" Terrain #"+(id+1)+" debloque !");
    checkAchs(); sv(); drawAll();
  });
}

// Market
function drawMarket(){
  var items=[];
  Object.keys(S.inv).forEach(function(k){if(S.inv[k]>0)items.push([k,S.inv[k]]);});
  var ni=document.getElementById("noinv"),ig=document.getElementById("igrid"),sw=document.getElementById("sabw"),mi=document.getElementById("minfo");
  if(items.length===0){sw.innerHTML="";ig.innerHTML="";ni.style.display="block";mi.innerHTML=""; return;}
  ni.style.display="none";
  var vm=vmul();
  var tot=0; items.forEach(function(it){var c=gc(it[0]);if(c)tot+=Math.round(c.sell*vm*it[1]);});
  mi.innerHTML="<div style=\"text-align:center;color:rgba(255,255,255,.9);font-size:.78rem;font-weight:700;padding:6px 0;\">Bonus vente x"+vm.toFixed(2)+"</div>";
  sw.innerHTML="<div class=\"sabtn\" onclick=\"sellAll()\">"+E.cash+" Tout vendre - "+E.coin+tot+"</div>";
  ig.innerHTML="";
  items.forEach(function(it){
    var cid=it[0],qty=it[1],c=gc(cid); if(!c) return;
    var pr=Math.round(c.sell*vm);
    var card=document.createElement("div"); card.className="ic";
    card.innerHTML="<div class=\"ie\">"+E[cid]+"</div><div><div class=\"in\">"+c.name+"</div><div class=\"iq\">x"+qty+" en stock</div><div class=\"ipr\">"+E.coin+pr+" / unite</div></div>";
    (function(crop,cardEl){
      cardEl.addEventListener("click",function(){
        if((S.inv[crop.id]||0)<=0) return;
        S.inv[crop.id]--; var earn=gmoney(crop.sell); S.te+=earn;
        var r2=cardEl.getBoundingClientRect(); ffx(r2.left+r2.width/2,r2.top,"+"+E.coin+earn,"#F4A320");
        checkAchs(); sv(); updHdr(); drawMarket();
      });
    })(c,card);
    ig.appendChild(card);
  });
}
function sellAll(){
  var tot=0;
  Object.keys(S.inv).forEach(function(k){
    var c=gc(k); if(!c||!S.inv[k]) return;
    var earn=Math.round(c.sell*vmul()*S.inv[k]); tot+=earn; S.money+=earn; S.te+=earn; S.inv[k]=0;
  });
  if(tot>0){toast(E.cash+" Tout vendu: "+E.coin+tot+" !");checkAchs();sv();updHdr();drawMarket();}
}

// Upgrades
function drawUpg(){
  var list=document.getElementById("ulist"); list.innerHTML="";
  UPGRADES.forEach(function(u){
    var lv=gu(u.id),mx=lv>=u.maxLv,cost=mx?0:Math.round(u.base*Math.pow(2,lv));
    var d=document.createElement("div"); d.className="ugc"+(mx?" mx":"");
    d.innerHTML="<div class=\"ui\">"+E[u.icon]+"</div>"
      +"<div><div class=\"un\">"+u.name+"</div><div class=\"ud\">"+u.desc+"</div><div class=\"ul\">Niveau "+lv+"/"+u.maxLv+"</div></div>"
      +"<div class=\"uc"+((!mx&&S.money<cost)?" na":"")+"\">"+( mx?E.check+" MAX":E.coin+cost)+"</div>";
    if(!mx){
      (function(up,c2){
        d.addEventListener("click",function(){
          if(S.money<c2){toast("Pas assez !"); return;}
          S.money-=c2; S.upg[up.id]=(S.upg[up.id]||0)+1;
          if(up.fx==="water"){S.mwc+=2;S.wc=Math.min(S.wc+2,S.mwc);}
          if(up.fx==="fert"){S.mfc+=1;S.frc=Math.min(S.frc+1,S.mfc);}
          toast(E[up.icon]+" "+up.name+" ameliore !");
          checkAchs(); sv(); updHdr(); drawUpg();
        });
      })(u,cost);
    }
    list.appendChild(d);
  });
}

// Achievements
function checkAchs(){
  ACHS.forEach(function(a){
    if(S.achs.indexOf(a.id)<0&&a.ok(S)){
      S.achs.push(a.id);
      toast(E.trophy+" Trophee: "+a.name+" !");
      if(curTab==="ach") drawAch();
    }
  });
}
function drawAch(){
  var list=document.getElementById("alist"); list.innerHTML="";
  ACHS.forEach(function(a){
    var ok=S.achs.indexOf(a.id)>=0;
    var d=document.createElement("div"); d.className="acc"+(ok?"":" lka");
    d.innerHTML="<div class=\"ai\">"+E[a.ic]+"</div>"
      +"<div><div class=\"an\">"+a.name+"</div><div class=\"ad\">"+a.desc+"</div></div>"
      +"<div class=\"ack\">"+(ok?E.check:E.lock)+"</div>";
    list.appendChild(d);
  });
}

// Header
function updHdr(){
  document.getElementById("hlv").textContent=S.lv;
  document.getElementById("hmn").textContent=S.money;
  var pct=Math.min(100,S.xp/S.xpn*100);
  document.getElementById("xpfill").style.width=pct+"%";
  document.getElementById("xplbl").textContent="XP: "+S.xp+"/"+S.xpn;
}

// Modal
var MCB=null;
function openM(t,b,cb){
  document.getElementById("mt").textContent=t;
  document.getElementById("mb").textContent=b;
  MCB=cb; document.getElementById("mover").classList.add("on");
  document.getElementById("mok").onclick=function(){closeM();if(MCB)MCB();};
}
function closeM(){document.getElementById("mover").classList.remove("on");}

function drawAll(){updHdr();drawFarm();drawWeather();checkDaily();if(curTab==="market")drawMarket();if(curTab==="upg")drawUpg();if(curTab==="ach")drawAch();if(curTab==="shop")drawShop();}

function gameLoop(){tickW();if(curTab==="farm")drawFarm();if(curTab==="market")drawMarket();updHdr();}

drawShop(); drawAll();
setInterval(gameLoop,1000);
</script>
</body>
</html>
