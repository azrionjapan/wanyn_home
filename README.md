<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>ワンニャンホーム</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Zen+Maru+Gothic:wght@400;500;700;900&family=Noto+Sans+JP:wght@400;500;700;900&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#1E1B17;
  --bg-elev:#28241F;
  --bg-elev-2:#322D26;
  --accent:#E85D75;
  --accent-dark:#C64B62;
  --accent-2:#8FAE8B;
  --accent-2-dark:#729473;
  --accent-3:#F2B84B;
  --text:#F6EFE4;
  --text-muted:#B7ACA0;
  --text-faint:#7D7468;
  --border:#3C362E;
  --danger:#E8615D;
  --radius:16px;
}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent;}
html,body{margin:0;padding:0;background:#0F0D0B;color:var(--text);font-family:'Noto Sans JP',sans-serif;}
.display{font-family:'Zen Maru Gothic',sans-serif;}
.mono{font-family:'JetBrains Mono',monospace;}
button{font-family:inherit;cursor:pointer;}
input,select,textarea{font-family:inherit;}
::selection{background:var(--accent);color:white;}
a{color:inherit;}

#device-frame{
  max-width:430px;
  margin:0 auto;
  min-height:100vh;
  background:var(--bg);
  position:relative;
  overflow-x:hidden;
  box-shadow:0 0 60px rgba(0,0,0,0.6);
}
@media(min-width:431px){
  body{padding:24px 0;background:#0a0908;}
  #device-frame{min-height:calc(100vh - 48px);border-radius:32px;overflow:hidden;}
}

/* Top bar */
.topbar{
  position:sticky;top:0;z-index:40;
  background:rgba(30,27,23,0.92);backdrop-filter:blur(10px);
  display:flex;align-items:center;justify-content:space-between;
  padding:16px 18px;border-bottom:1px solid var(--border);
}
.topbar h1{font-size:16px;margin:0;font-weight:700;}
.topbar .icon-btn{background:none;border:none;color:var(--text);font-size:20px;padding:4px;display:flex;align-items:center;}
.brand{display:flex;align-items:center;gap:8px;}
.brand .mark{width:30px;height:30px;position:relative;flex:none;}
.brand .mark svg{width:100%;height:100%;}
.brand span{font-family:'Zen Maru Gothic',sans-serif;font-weight:900;font-size:16px;letter-spacing:.02em;}

/* House badge - signature element */
.house-tag{
  display:inline-flex;align-items:center;justify-content:center;
  clip-path:polygon(50% 0%, 100% 38%, 100% 100%, 0% 100%, 0% 38%);
  padding:7px 10px 4px;font-size:10px;font-weight:700;
  background:var(--accent-2);color:#16261a;
  min-width:56px;
}
.house-tag.urgent{background:var(--accent);color:white;}
.house-tag.gold{background:var(--accent-3);color:#3a2a04;}

/* Match ring - signature element */
.match-ring{
  --pct:70;
  width:56px;height:56px;border-radius:50%;
  background:conic-gradient(var(--accent-2) calc(var(--pct)*1%), rgba(255,255,255,0.08) 0);
  display:flex;align-items:center;justify-content:center;flex:none;
}
.match-ring-inner{
  width:44px;height:44px;border-radius:50%;background:var(--bg-elev);
  display:flex;flex-direction:column;align-items:center;justify-content:center;
  font-size:11px;font-weight:700;color:var(--accent-2);line-height:1;
}
.match-ring-inner small{font-size:8px;color:var(--text-faint);font-weight:500;}

/* Screens */
.screen{display:none;padding-bottom:96px;min-height:100vh;animation:fadein .25s ease;}
.screen.active{display:block;}
.screen.no-nav{padding-bottom:24px;}
@keyframes fadein{from{opacity:0;transform:translateY(6px);}to{opacity:1;transform:none;}}

.container{padding:16px 18px;}
.section-title{font-family:'Zen Maru Gothic',sans-serif;font-weight:900;font-size:19px;margin:4px 0 14px;}
.section-sub{color:var(--text-muted);font-size:13px;line-height:1.7;margin-bottom:16px;}

/* Buttons */
.btn{
  display:flex;align-items:center;justify-content:center;gap:6px;
  width:100%;padding:14px 16px;border-radius:100px;border:none;
  font-weight:700;font-size:15px;transition:transform .12s ease, filter .12s ease;
}
.btn:active{transform:scale(0.97);}
.btn-primary{background:var(--accent);color:white;}
.btn-primary:hover{filter:brightness(1.06);}
.btn-outline{background:transparent;color:var(--text);border:1.5px solid var(--border);}
.btn-outline-accent{background:transparent;color:var(--accent);border:1.5px solid var(--accent);}
.btn-secondary{background:var(--bg-elev-2);color:var(--text);}
.btn-org{background:var(--accent-2);color:#16261a;}
.btn-sm{padding:9px 14px;font-size:13px;width:auto;}
.btn-danger{background:transparent;color:var(--danger);border:1.5px solid rgba(232,97,93,0.4);}
.btn[disabled]{opacity:.4;pointer-events:none;}

/* Inputs */
.field{margin-bottom:16px;}
.field label{display:block;font-size:12px;font-weight:700;color:var(--text-muted);margin-bottom:7px;}
.field label .req{color:var(--accent);margin-left:4px;font-size:10px;background:rgba(232,93,117,0.15);padding:1px 6px;border-radius:6px;}
.field input[type=text],.field input[type=email],.field input[type=password],.field input[type=tel],.field input[type=date],.field input[type=number],.field select,.field textarea{
  width:100%;padding:13px 14px;border-radius:12px;border:1.5px solid var(--border);
  background:var(--bg-elev);color:var(--text);font-size:14px;outline:none;
}
.field textarea{resize:vertical;min-height:80px;}
.field input:focus,.field select:focus,.field textarea:focus{border-color:var(--accent);}
.field .hint{font-size:11px;color:var(--text-faint);margin-top:6px;}
.row2{display:grid;grid-template-columns:1fr 1fr;gap:10px;}

.chip-group{display:flex;flex-wrap:wrap;gap:8px;}
.chip{
  padding:9px 14px;border-radius:100px;border:1.5px solid var(--border);
  background:var(--bg-elev);color:var(--text-muted);font-size:13px;font-weight:600;
  transition:all .15s ease;user-select:none;
}
.chip.active{background:var(--accent);border-color:var(--accent);color:white;}
.chip.chip-outline-select.active{background:var(--accent-2);border-color:var(--accent-2);color:#16261a;}

.upload-box{
  border:1.5px dashed var(--border);border-radius:14px;padding:20px;text-align:center;
  color:var(--text-faint);font-size:12px;background:var(--bg-elev);
}
.upload-box.filled{border-color:var(--accent-2);color:var(--accent-2);border-style:solid;}
.upload-box .up-icon{font-size:26px;display:block;margin-bottom:6px;}

/* Cards */
.card{background:var(--bg-elev);border:1px solid var(--border);border-radius:var(--radius);padding:16px;margin-bottom:12px;}
.pet-card{display:flex;gap:12px;background:var(--bg-elev);border:1px solid var(--border);border-radius:var(--radius);padding:12px;margin-bottom:12px;position:relative;}
.pet-thumb{
  width:88px;height:88px;border-radius:12px;flex:none;
  display:flex;align-items:center;justify-content:center;font-size:34px;position:relative;
}
.pet-thumb .bookmark-btn{position:absolute;bottom:4px;right:4px;background:rgba(0,0,0,0.45);border:none;border-radius:50%;width:24px;height:24px;display:flex;align-items:center;justify-content:center;font-size:12px;color:white;}
.pet-info{flex:1;min-width:0;}
.pet-info .pname{font-weight:700;font-size:14.5px;margin:4px 0 2px;font-family:'Zen Maru Gothic',sans-serif;}
.pet-info .pmeta{color:var(--text-muted);font-size:12px;line-height:1.6;}
.tag-row{display:flex;gap:6px;flex-wrap:wrap;margin-top:6px;}
.small-tag{font-size:10px;padding:3px 8px;border-radius:100px;background:var(--bg-elev-2);color:var(--text-muted);}

.stat-pill{display:flex;justify-content:space-between;align-items:center;padding:12px 14px;background:var(--bg-elev-2);border-radius:12px;margin-bottom:8px;font-size:13px;}
.stat-pill b{font-family:'Zen Maru Gothic',sans-serif;}

.list-row{
  display:flex;align-items:center;justify-content:space-between;
  padding:15px 4px;border-bottom:1px solid var(--border);font-size:14px;
}
.list-row:last-child{border-bottom:none;}
.list-row .left{display:flex;align-items:center;gap:10px;}
.list-row .arrow{color:var(--text-faint);}
.list-row .desc{color:var(--text-faint);font-size:11px;margin-top:2px;}

/* Bottom nav */
.bottom-nav{
  position:fixed;bottom:0;left:50%;transform:translateX(-50%);
  width:100%;max-width:430px;background:rgba(30,27,23,0.96);backdrop-filter:blur(12px);
  border-top:1px solid var(--border);display:flex;z-index:50;padding:8px 4px calc(8px + env(safe-area-inset-bottom));
}
.nav-item{
  flex:1;display:flex;flex-direction:column;align-items:center;gap:3px;
  background:none;border:none;color:var(--text-faint);font-size:10px;padding:6px 0;font-weight:600;
}
.nav-item.active{color:var(--accent);}
.nav-item .ico{font-size:19px;}
.nav-item .badge-dot{position:relative;}
.nav-item .badge-dot::after{content:'';position:absolute;top:-2px;right:-6px;width:7px;height:7px;border-radius:50%;background:var(--accent);}

/* Search bar */
.search-bar{
  display:flex;align-items:center;gap:8px;background:var(--bg-elev);border:1.5px solid var(--border);
  border-radius:100px;padding:11px 16px;color:var(--text-faint);font-size:13px;
}
.tabs-row{display:flex;gap:6px;overflow-x:auto;padding:2px 0 4px;scrollbar-width:none;}
.tabs-row::-webkit-scrollbar{display:none;}
.tab-pill{flex:none;padding:8px 16px;border-radius:100px;font-size:13px;font-weight:700;background:var(--bg-elev);color:var(--text-muted);border:1.5px solid var(--border);}
.tab-pill.active{background:var(--accent);color:white;border-color:var(--accent);}

.filter-bar{display:flex;gap:8px;overflow-x:auto;padding:10px 0;scrollbar-width:none;}
.filter-bar::-webkit-scrollbar{display:none;}
.filter-chip{
  flex:none;display:flex;align-items:center;gap:5px;padding:8px 13px;border-radius:100px;
  background:var(--bg-elev);border:1.5px solid var(--border);font-size:12px;color:var(--text-muted);font-weight:600;
}
.filter-chip.on{background:rgba(232,93,117,0.14);border-color:var(--accent);color:var(--accent);}

.divider{height:1px;background:var(--border);margin:18px 0;}
.muted{color:var(--text-muted);}
.faint{color:var(--text-faint);font-size:12px;}
.center{text-align:center;}
.mt8{margin-top:8px;}.mt12{margin-top:12px;}.mt16{margin-top:16px;}.mt24{margin-top:24px;}
.mb8{margin-bottom:8px;}.mb12{margin-bottom:12px;}.mb16{margin-bottom:16px;}

.empty-state{padding:60px 20px;text-align:center;color:var(--text-faint);}
.empty-state .ico{font-size:38px;display:block;margin-bottom:10px;}
.empty-state .cta{margin-top:16px;}

/* toast */
#toast{
  position:fixed;bottom:100px;left:50%;transform:translateX(-50%) translateY(20px);
  background:#F6EFE4;color:#1E1B17;padding:12px 20px;border-radius:100px;font-size:13px;font-weight:700;
  z-index:200;opacity:0;transition:all .25s ease;pointer-events:none;box-shadow:0 8px 24px rgba(0,0,0,0.4);
  max-width:90%;text-align:center;
}
#toast.show{opacity:1;transform:translateX(-50%) translateY(0);}

/* step indicator */
.steps{display:flex;align-items:center;gap:4px;margin-bottom:22px;}
.steps .dot{flex:1;height:4px;border-radius:4px;background:var(--border);}
.steps .dot.done{background:var(--accent-2);}
.steps .dot.now{background:var(--accent);}

/* chat */
.chat-wrap{display:flex;flex-direction:column;padding:14px 14px 12px;gap:10px;min-height:calc(100vh - 250px);}
.msg{max-width:80%;padding:11px 14px;border-radius:16px;font-size:13.5px;line-height:1.6;}
.msg.bot{background:var(--bg-elev);border:1px solid var(--border);align-self:flex-start;border-bottom-left-radius:4px;}
.msg.user{background:var(--accent);color:white;align-self:flex-end;border-bottom-right-radius:4px;}
.chat-suggests{display:flex;flex-wrap:wrap;gap:8px;margin:4px 0 10px;}
.suggest-btn{padding:9px 14px;border-radius:100px;background:var(--bg-elev-2);border:1.5px solid var(--border);color:var(--text);font-size:12.5px;font-weight:600;}
.chat-input-bar{
  position:sticky;bottom:64px;display:flex;gap:8px;padding:10px 14px;background:rgba(30,27,23,0.96);backdrop-filter:blur(10px);border-top:1px solid var(--border);
}
.chat-input-bar input{flex:1;border-radius:100px;border:1.5px solid var(--border);background:var(--bg-elev);color:var(--text);padding:11px 16px;font-size:13.5px;outline:none;}
.chat-input-bar button{flex:none;width:42px;height:42px;border-radius:50%;background:var(--accent);border:none;color:white;font-size:16px;}
.pet-suggest-card{display:flex;gap:10px;background:var(--bg-elev-2);border-radius:12px;padding:10px;margin-top:6px;align-self:flex-start;max-width:88%;}

/* org */
.org-header{background:linear-gradient(160deg, var(--accent-2), var(--accent-2-dark));border-radius:18px;padding:20px;color:#0f1d13;margin-bottom:16px;}

.avatar-lg{width:72px;height:72px;border-radius:50%;background:var(--bg-elev-2);display:flex;align-items:center;justify-content:center;font-size:30px;border:2px solid var(--border);flex:none;}
.profile-head{display:flex;gap:14px;align-items:center;margin-bottom:6px;}
.rank-badge{display:inline-flex;align-items:center;gap:4px;font-size:11px;font-weight:700;padding:4px 10px;border-radius:100px;}
.rank-1{background:rgba(183,172,160,0.15);color:var(--text-muted);}
.rank-2{background:rgba(143,174,139,0.18);color:var(--accent-2);}
.rank-3{background:rgba(242,184,75,0.18);color:var(--accent-3);}

.toggle{position:relative;width:44px;height:26px;border-radius:100px;background:var(--bg-elev-2);border:1.5px solid var(--border);flex:none;}
.toggle.on{background:var(--accent);border-color:var(--accent);}
.toggle::after{content:'';position:absolute;top:2px;left:2px;width:19px;height:19px;border-radius:50%;background:white;transition:all .15s ease;}
.toggle.on::after{left:20px;}

.legal-text h4{font-family:'Zen Maru Gothic',sans-serif;font-size:14px;margin:18px 0 8px;color:var(--accent-2);}
.legal-text p, .legal-text li{font-size:12.5px;color:var(--text-muted);line-height:1.9;}
.legal-text ol,.legal-text ul{padding-left:18px;}

.credit-card-visual{
  border-radius:16px;padding:20px;background:linear-gradient(135deg,#3a3229,#221f1a);border:1px solid var(--border);
  margin-bottom:16px;position:relative;overflow:hidden;
}
.credit-card-visual::after{content:'🐾';position:absolute;right:-10px;bottom:-10px;font-size:80px;opacity:.06;}
.credit-card-visual .cc-num{font-family:'JetBrains Mono',monospace;font-size:17px;letter-spacing:2px;margin:22px 0 14px;}
.credit-card-visual .cc-bottom{display:flex;justify-content:space-between;font-size:11px;color:var(--text-muted);}

.back-btn{background:none;border:none;color:var(--text);font-size:20px;display:flex;align-items:center;padding:2px 6px 2px 0;}
.header-fixed{display:flex;align-items:center;gap:6px;}
.header-fixed h1{flex:1;text-align:center;margin-right:26px;}

input[type=checkbox]{accent-color:var(--accent);width:17px;height:17px;}
.check-row{display:flex;align-items:flex-start;gap:9px;font-size:12.5px;color:var(--text-muted);margin-bottom:10px;line-height:1.6;}
.check-row a{color:var(--accent-2);text-decoration:underline;}

.sticky-cta{position:sticky;bottom:0;background:linear-gradient(0deg, var(--bg) 60%, transparent);padding:18px 18px 10px;margin:0 -18px;}
</style>
</head>
<body>
<div id="device-frame">
  <div id="app-content"></div>
  <div id="bottom-nav-slot"></div>
</div>
<div id="toast"></div>

<script>
/* ============================= DATA ============================= */
const HOUSE_MARK = `<svg viewBox="0 0 32 32" fill="none"><path d="M16 3 L29 13 V28 H3 V13 Z" stroke="#E85D75" stroke-width="2.4" fill="none" stroke-linejoin="round"/><circle cx="16" cy="19" r="3.2" fill="#F2B84B"/></svg>`;

const BREEDS_DOG = ["柴犬","チワワ","トイプードル","ミックス（中型）","ミックス（小型）","ラブラドール","ポメラニアン","ダックスフンド","パピヨン","雑種（大型）"];
const BREEDS_CAT = ["雑種（短毛）","雑種（長毛）","アメリカンショートヘア","スコティッシュフォールド","キジトラ","三毛","サビ猫","black cat"];
const AREAS = ["北海道","東京都","神奈川県","大阪府","愛知県","福岡県","埼玉県","千葉県","兵庫県","京都府","香川県","沖縄県"];
const FACE_TYPES = ["丸顔","キツネ顔","たぬき顔","くちゃ顔（短頭種）","面長"];
const COAT_COLORS = ["ブラック","ホワイト","ブラウン","茶トラ","三毛","ハチワレ","サビ","クリーム","グレー","キジトラ"];
const BODY_TYPES = ["超小型","小型","中型","大型","超大型","スリム","がっしり","ぽっちゃり"];
const COAT_LENGTHS = ["短毛","長毛","巻き毛","無毛に近い"];

let idSeq = 1000;
const SAMPLE_ORGS = [
  {id:'org1', name:'NPO法人 みんなのシェルター大阪', license:'第27-動保-0142号', area:'大阪府 東淀川区', contact:'06-xxxx-xxxx', rating:4.8, petsCount:34, verified:true, desc:'年間200頭以上の保護犬猫の譲渡実績。医療ケア済みでお迎えいただけます。'},
  {id:'org2', name:'保護猫カフェ＆シェルター ふくねこ', license:'第13-動保-0987号', area:'東京都 世田谷区', contact:'03-xxxx-xxxx', rating:4.9, petsCount:21, verified:true, desc:'猫専門シェルター。譲渡後もLINEで相談し放題のサポート付き。'},
  {id:'org3', name:'一般社団法人 わんわん福祉会 福岡', license:'第40-動保-2201号', area:'福岡県 福津市', contact:'092-xxxx-xxxx', rating:4.6, petsCount:12, verified:true, desc:'高齢犬・障がい犬の受け入れに力を入れている団体です。'},
];

function makePet(o){ idSeq++; return Object.assign({id:'p'+idSeq, applied:false}, o); }
let SAMPLE_PETS = [
  makePet({species:'dog', name:'まめ', breed:'柴犬ミックス', sex:'オス', age:'2歳', area:'大阪府 東淀川区', size:'中型', bodyType:'がっしり', faceType:'たぬき顔', coatColor:'ブラウン', coatLength:'短毛', pickup:'both', orgId:'org1', urgent:true, emoji:'🐕', video:true, scan3d:true, desc:'人懐っこく元気いっぱいの男の子。お散歩が大好きで、他の犬とも仲良くできます。基本的なしつけはできています。'}),
  makePet({species:'cat', name:'モナ', breed:'キジトラ', sex:'メス', age:'1歳', area:'東京都 世田谷区', size:'小型', bodyType:'スリム', faceType:'丸顔', coatColor:'キジトラ', coatLength:'短毛', pickup:'delivery', orgId:'org2', urgent:false, emoji:'🐈', video:true, scan3d:false, desc:'甘えん坊でひざの上が大好き。多頭飼育のお家で育ったので他の猫とも馴染みやすいです。'}),
  makePet({species:'dog', name:'リノ', breed:'雑種（小型）', sex:'オス', age:'子犬（4ヶ月）', area:'香川県 東かがわ市', size:'小型', bodyType:'ぽっちゃり', faceType:'丸顔', coatColor:'茶トラ', coatLength:'短毛', pickup:'pickup', orgId:'org3', urgent:true, emoji:'🐶', video:false, scan3d:false, desc:'兄弟のマナと一緒に保護されました。人にも動物にも臆病なところがなく懐きやすいです。'}),
  makePet({species:'cat', name:'クロ', breed:'雑種（短毛）', sex:'オス', age:'5歳', area:'大阪府 東淀川区', size:'中型', bodyType:'がっしり', faceType:'面長', coatColor:'ブラック', coatLength:'短毛', pickup:'both', orgId:'org1', urgent:false, emoji:'🐈‍⬛', video:true, scan3d:true, desc:'落ち着いた性格の大人猫。留守番も得意なので共働きのご家庭にもおすすめです。'}),
  makePet({species:'dog', name:'ハナ', breed:'ポメラニアン', sex:'メス', age:'7歳', area:'東京都 世田谷区', size:'超小型', bodyType:'スリム', faceType:'キツネ顔', coatColor:'クリーム', coatLength:'長毛', pickup:'delivery', orgId:'org2', urgent:false, emoji:'🦮', video:true, scan3d:false, desc:'シニア期に入り穏やかな性格。持病はなく健康です。のんびり暮らせるお家を探しています。'}),
  makePet({species:'cat', name:'みかん', breed:'三毛', sex:'メス', age:'3歳', area:'福岡県 福津市', size:'小型', bodyType:'スリム', faceType:'丸顔', coatColor:'三毛', coatLength:'短毛', pickup:'both', orgId:'org3', urgent:false, emoji:'🐱', video:false, scan3d:false, desc:'マイペースで気ままな性格。窓辺で日向ぼっこするのが日課です。'}),
  makePet({species:'dog', name:'ソラ', breed:'ラブラドール', sex:'オス', age:'3歳', area:'大阪府 東淀川区', size:'大型', bodyType:'がっしり', faceType:'面長', coatColor:'ホワイト', coatLength:'短毛', pickup:'pickup', orgId:'org1', urgent:true, emoji:'🐕‍🦺', video:true, scan3d:true, desc:'広めのお庭があるご家庭希望。運動が大好きで、アジリティの経験もあります。'}),
  makePet({species:'cat', name:'コテツ', breed:'アメリカンショートヘア', sex:'オス', age:'2歳', area:'東京都 世田谷区', size:'中型', bodyType:'がっしり', faceType:'丸顔', coatColor:'グレー', coatLength:'短毛', pickup:'delivery', orgId:'org2', urgent:false, emoji:'🐈', video:true, scan3d:false, desc:'遊び好きで運動神経抜群。おもちゃで一緒に遊んでくれる方を待っています。'}),
];

/* ============================= STATE ============================= */
const S = {
  screen: 'splash',
  navTab: 'home',
  authed: false,
  user: null, // {email, name, kana, birthdate, phone, zip, address, idUploaded, membership:1, avatarEmoji}
  orgUser: null,
  filters: {species:'', keyword:'', area:'', breed:'', sex:'', age:'', size:'', bodyType:'', faceType:'', coatColor:'', coatLength:'', pickup:''},
  bookmarks: new Set(),
  notifications: [
    {id:1, title:'ようこそワンニャンホームへ', body:'まずはプロフィールを完成させて、AIマッチングの精度を上げましょう。', time:'たった今', read:false},
  ],
  applications: [], // {id, petId, status, step, fee}
  chatHistory: [],
  chatProfile: {stage:0, answers:{}},
  paymentMethods: [],
  pendingApplyPet: null,
  applyStep: 1,
  detailPetId: null,
  orgStep: 1,
  orgDraftPet: {},
  signupStep: 1,
  signupDraft: {},
};

function toast(msg){
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  clearTimeout(window.__toastTimer);
  window.__toastTimer = setTimeout(()=>t.classList.remove('show'), 2200);
}

/* ============================= ROUTER ============================= */
function nav(screen, opts){
  S.screen = screen;
  if(opts && opts.tab) S.navTab = opts.tab;
  render();
  window.scrollTo(0,0);
}
function switchTab(tab){
  S.navTab = tab;
  const map = {home:'home', chat:'ai-chat', bookmarks:'bookmarks', notifications:'notifications', mypage:'mypage'};
  nav(map[tab]);
}

/* ============================= HELPERS ============================= */
function petById(id){ return SAMPLE_PETS.find(p=>p.id===id); }
function orgById(id){ return SAMPLE_ORGS.find(o=>o.id===id); }
function speciesLabel(s){ return s==='dog' ? '犬' : '猫'; }
function pickupLabel(p){ return p==='both' ? 'お迎え／お届け両方可' : p==='pickup' ? 'お迎え（引取り）のみ' : 'お届け（配送）可'; }
function matchScore(pet){
  // simple deterministic pseudo-score for demo
  let s = 60;
  if(pet.urgent) s += 8;
  if(S.filters.species && S.filters.species===pet.species) s += 10;
  if(S.filters.area && pet.area.includes(S.filters.area)) s += 12;
  if(S.filters.faceType && pet.faceType===S.filters.faceType) s += 10;
  if(S.filters.coatColor && pet.coatColor===S.filters.coatColor) s += 10;
  s += (pet.id.charCodeAt(pet.id.length-1) % 9);
  return Math.min(s, 99);
}
function thumbColor(pet){
  const palette = ['#3a2f28','#2c3a2f','#3a2c33','#2c333a','#3a3628'];
  return palette[pet.id.charCodeAt(1) % palette.length];
}
function filteredPets(){
  return SAMPLE_PETS.filter(p=>{
    const f = S.filters;
    if(f.species && p.species!==f.species) return false;
    if(f.keyword && !(p.name+p.breed+p.desc).includes(f.keyword)) return false;
    if(f.area && !p.area.includes(f.area)) return false;
    if(f.breed && p.breed!==f.breed) return false;
    if(f.sex && p.sex!==f.sex) return false;
    if(f.size && p.size!==f.size) return false;
    if(f.bodyType && p.bodyType!==f.bodyType) return false;
    if(f.faceType && p.faceType!==f.faceType) return false;
    if(f.coatColor && p.coatColor!==f.coatColor) return false;
    if(f.coatLength && p.coatLength!==f.coatLength) return false;
    if(f.pickup && p.pickup!==f.pickup && p.pickup!=='both') return false;
    return true;
  });
}
function activeFilterCount(){
  return Object.values(S.filters).filter(v=>v).length;
}
function fmtYen(n){ return '¥' + n.toLocaleString(); }

/* ============================= RENDER ROOT ============================= */
function render(){
  const app = document.getElementById('app-content');
  const navSlot = document.getElementById('bottom-nav-slot');
  app.innerHTML = SCREENS[S.screen] ? SCREENS[S.screen]() : `<div class="container">Not found</div>`;
  const showNav = ['home','ai-chat','bookmarks','notifications','mypage'].includes(S.screen);
  navSlot.innerHTML = showNav ? renderBottomNav() : '';
}

function renderBottomNav(){
  const items = [
    {id:'home', ico:'🏠', label:'さがす'},
    {id:'chat', ico:'💬', label:'AI相談'},
    {id:'bookmarks', ico:'🔖', label:'ブックマーク'},
    {id:'notifications', ico:'🔔', label:'通知', badge:S.notifications.some(n=>!n.read)},
    {id:'mypage', ico:'👤', label:'マイページ'},
  ];
  const activeMap = {home:'home', 'ai-chat':'chat', bookmarks:'bookmarks', notifications:'notifications', mypage:'mypage'};
  return `<nav class="bottom-nav">
    ${items.map(i=>`
      <button class="nav-item ${activeMap[S.screen]===i.id?'active':''}" onclick="switchTab('${i.id}')">
        <span class="ico ${i.badge?'badge-dot':''}">${i.ico}</span>
        <span>${i.label}</span>
      </button>`).join('')}
  </nav>`;
}

function requireAuth(next){
  if(!S.authed){ nav('auth-gate'); window.__afterAuth = next; return false; }
  return true;
}

/* ============================= SCREENS ============================= */
const SCREENS = {};

/* ---- Splash ---- */
SCREENS['splash'] = () => `
<div class="screen active no-nav" style="min-height:100vh;display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;padding:24px;background:radial-gradient(circle at 50% 20%, #2c2620, var(--bg) 70%);">
  <div style="width:84px;height:84px;margin-bottom:18px;">${HOUSE_MARK}</div>
  <div class="display" style="font-size:26px;font-weight:900;">ワンニャンホーム</div>
  <div class="faint mt8" style="font-size:13px;">保護犬・保護猫と、AIでやさしく出会う。</div>
  <div style="margin-top:56px;width:100%;">
    <button class="btn btn-primary" onclick="nav('auth-gate')">はじめる</button>
    <div class="mt12 faint">すでに会員の方は <a style="color:var(--accent-2);font-weight:700;text-decoration:underline;" onclick="nav('login')">ログイン</a></div>
  </div>
</div>`;

/* ---- Auth gate (info before signup) ---- */
SCREENS['auth-gate'] = () => `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;"><button class="back-btn" onclick="nav('splash')">‹</button><h1>会員登録の前に</h1></div></div>
  <div class="container">
    <div class="card" style="background:linear-gradient(160deg,#2c2620,#221f1a);">
      <div class="display" style="font-size:18px;font-weight:900;margin-bottom:6px;">小さな命が、安心して<br>おうちに帰れるように。</div>
      <p class="section-sub" style="margin-bottom:0;">ワンニャンホームのご利用には会員登録（本人確認）が必須です。複数のペットの不正な引き取りや、虐待・転売目的の利用を防ぐための仕組みです。</p>
    </div>
    <div class="legal-text">
      <h4>🔒 ご登録の前に必ずお読みください</h4>
      <ul>
        <li>保護犬・保護猫の閲覧および応募には、氏名・住所・電話番号の登録と本人確認書類の提出が必要です。</li>
        <li>虚偽の情報でのご登録が確認された場合、直ちに退会処分とし、保護団体・関係機関への情報共有を行う場合があります。</li>
        <li>個人情報はSSL暗号化通信により保護され、譲渡が成立するまで団体側には一部情報のみ開示されます。</li>
        <li>お迎え後のトラブル防止のため、里親同士が個人を特定できるコミュニティ機能は設けておりません。</li>
      </ul>
      <h4>💳 メンバーシップについて</h4>
      <p>基本的な閲覧・検索・AI相談は無料でご利用いただけます。所在地の詳細表示や優先マッチングなどは有料メンバーシップ（年額 ¥3,600〜）でご提供しています。詳しくは登録後にご案内します。</p>
    </div>
    <button class="btn btn-primary mt16" onclick="nav('signup-account')">内容に同意して会員登録へ</button>
    <button class="btn btn-outline mt8" onclick="nav('login')">ログインはこちら</button>
  </div>
</div>`;

/* ---- Login ---- */
SCREENS['login'] = () => `
<div class="screen active no-nav" style="display:flex;flex-direction:column;justify-content:center;min-height:100vh;">
  <div class="container">
    <div class="center mb16">
      <div style="width:60px;height:60px;margin:0 auto 10px;">${HOUSE_MARK}</div>
      <div class="display" style="font-size:20px;font-weight:900;">ワンニャンホーム</div>
    </div>
    <div class="field"><label>メールアドレス</label><input type="email" id="li-email" placeholder="you@example.com"></div>
    <div class="field"><label>パスワード</label><input type="password" id="li-pass" placeholder="••••••••"></div>
    <button class="btn btn-primary" onclick="doLogin()">ログイン</button>
    <div class="center mt12 faint">パスワードをお忘れですか？</div>
    <div class="divider"></div>
    <button class="btn btn-outline" onclick="nav('auth-gate')">新規会員登録はこちら</button>
    <div class="divider"></div>
    <button class="btn btn-secondary" onclick="nav('org-login')">🏢 保護団体の方はこちら</button>
  </div>
</div>`;
function doLogin(){
  S.authed = true;
  if(!S.user){ S.user = defaultUser(); }
  toast('ログインしました');
  const next = window.__afterAuth; window.__afterAuth = null;
  nav(next || 'home');
}
function defaultUser(){
  return {
    email:'you@example.com', name:'', kana:'', birthdate:'', phone:'', zip:'', address:'',
    idUploaded:false, membership:1, avatarEmoji:'🙂', bio:'', notifyNew:true, notifyChat:true, notifyMail:false,
  };
}

/* ---- Signup step 1: account ---- */
SCREENS['signup-account'] = () => `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;"><button class="back-btn" onclick="nav('auth-gate')">‹</button><h1>会員登録</h1></div></div>
  <div class="container">
    <div class="steps"><div class="dot now"></div><div class="dot"></div><div class="dot"></div></div>
    <div class="section-title">アカウント情報</div>
    <div class="field"><label>メールアドレス<span class="req">必須</span></label><input type="email" id="su-email" placeholder="you@example.com" value="${S.signupDraft.email||''}"></div>
    <div class="field"><label>パスワード<span class="req">必須</span></label><input type="password" id="su-pass" placeholder="8文字以上32文字以内"></div>
    <div class="field"><label>パスワード（確認）<span class="req">必須</span></label><input type="password" id="su-pass2" placeholder="確認のため再入力"></div>
    <div class="hint mb16">暗号化して保存されるため、漏洩の心配はありません。</div>
    <button class="btn btn-primary" onclick="signupStep1Next()">次へ（本人情報の入力）</button>
  </div>
</div>`;
function signupStep1Next(){
  const email = document.getElementById('su-email').value.trim();
  const pass = document.getElementById('su-pass').value;
  const pass2 = document.getElementById('su-pass2').value;
  if(!email || !pass){ toast('メールアドレスとパスワードを入力してください'); return; }
  if(pass.length < 8){ toast('パスワードは8文字以上で入力してください'); return; }
  if(pass !== pass2){ toast('パスワードが一致しません'); return; }
  S.signupDraft.email = email;
  nav('signup-kyc');
}

/* ---- Signup step 2: KYC ---- */
SCREENS['signup-kyc'] = () => `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;"><button class="back-btn" onclick="nav('signup-account')">‹</button><h1>本人確認情報</h1></div></div>
  <div class="container">
    <div class="steps"><div class="dot done"></div><div class="dot now"></div><div class="dot"></div></div>
    <div class="section-sub">生き物を扱うサービスのため、正確な情報のご登録にご協力ください。</div>
    <div class="row2">
      <div class="field"><label>姓<span class="req">必須</span></label><input type="text" id="su-lname" placeholder="例）久高" value="${S.signupDraft.lname||''}"></div>
      <div class="field"><label>名<span class="req">必須</span></label><input type="text" id="su-fname" placeholder="例）龍大" value="${S.signupDraft.fname||''}"></div>
    </div>
    <div class="row2">
      <div class="field"><label>セイ（カナ）<span class="req">必須</span></label><input type="text" id="su-lkana" placeholder="クダカ" value="${S.signupDraft.lkana||''}"></div>
      <div class="field"><label>メイ（カナ）<span class="req">必須</span></label><input type="text" id="su-fkana" placeholder="リュウダイ" value="${S.signupDraft.fkana||''}"></div>
    </div>
    <div class="field"><label>生年月日<span class="req">必須</span></label><input type="date" id="su-birth" value="${S.signupDraft.birth||''}"></div>
    <div class="field"><label>電話番号<span class="req">必須</span></label><input type="tel" id="su-phone" placeholder="090-xxxx-xxxx" value="${S.signupDraft.phone||''}"></div>
    <div class="row2">
      <div class="field"><label>郵便番号<span class="req">必須</span></label><input type="text" id="su-zip" placeholder="123-4567" value="${S.signupDraft.zip||''}"></div>
      <div class="field"><label>都道府県<span class="req">必須</span></label>
        <select id="su-pref"><option value="">選択してください</option>${AREAS.map(a=>`<option ${S.signupDraft.pref===a?'selected':''}>${a}</option>`).join('')}</select>
      </div>
    </div>
    <div class="field"><label>市区町村・番地<span class="req">必須</span></label><input type="text" id="su-address" placeholder="例）東淀川区豊里1-2-3" value="${S.signupDraft.address||''}"></div>
    <div class="field">
      <label>本人確認書類（運転免許証・マイナンバーカード等）<span class="req">必須</span></label>
      <div class="upload-box ${S.signupDraft.idUploaded?'filled':''}" onclick="mockUploadID()">
        <span class="up-icon">${S.signupDraft.idUploaded?'✅':'📷'}</span>
        ${S.signupDraft.idUploaded ? 'アップロード済み（id_front.jpg）' : 'タップして画像をアップロード'}
      </div>
      <div class="hint">審査完了までは一部機能の利用が制限されます（通常1営業日以内）。</div>
    </div>
    <div class="check-row"><input type="checkbox" id="su-agree1"><span><a onclick="nav('terms')">利用規約</a>および<a onclick="nav('privacy-policy')">プライバシーポリシー</a>に同意します</span></div>
    <div class="check-row"><input type="checkbox" id="su-agree2"><span>虚偽申告・複数アカウント保有・虐待/転売目的の利用がないことを誓約します</span></div>
    <button class="btn btn-primary mt8" onclick="signupStep2Next()">登録内容を確認する</button>
  </div>
</div>`;
function mockUploadID(){ S.signupDraft.idUploaded = true; render(); toast('本人確認書類をアップロードしました'); }
function signupStep2Next(){
  const req = ['su-lname','su-fname','su-lkana','su-fkana','su-birth','su-phone','su-zip','su-pref','su-address'];
  let ok = true;
  const draft = {};
  req.forEach(id=>{ const v = document.getElementById(id).value; draft[id.replace('su-','')] = v; if(!v) ok=false; });
  if(!ok){ toast('未入力の必須項目があります'); return; }
  if(!S.signupDraft.idUploaded){ toast('本人確認書類をアップロードしてください'); return; }
  if(!document.getElementById('su-agree1').checked || !document.getElementById('su-agree2').checked){ toast('規約への同意が必要です'); return; }
  Object.assign(S.signupDraft, draft);
  S.user = {
    email:S.signupDraft.email, name:`${draft.lname} ${draft.fname}`, kana:`${draft.lkana} ${draft.fkana}`,
    birthdate:draft.birth, phone:draft.phone, zip:draft.zip, address:`${draft.pref}${draft.address}`,
    idUploaded:true, kycStatus:'pending', membership:1, avatarEmoji:'🙂', bio:'', notifyNew:true, notifyChat:true, notifyMail:false,
  };
  S.authed = true;
  nav('signup-complete');
}

/* ---- Signup complete ---- */
SCREENS['signup-complete'] = () => `
<div class="screen active no-nav" style="min-height:100vh;display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;padding:24px;">
  <div style="font-size:56px;">🏡</div>
  <div class="display mt12" style="font-size:20px;font-weight:900;">会員登録が完了しました</div>
  <p class="section-sub mt8">本人確認の審査結果は登録メールアドレスにご連絡します。審査完了までもAI相談・検索はご利用いただけます。</p>
  <button class="btn btn-primary mt16" onclick="nav('home')">保護犬・保護猫をさがす</button>
</div>`;

/* ---- Org login (stub) ---- */
SCREENS['org-login'] = () => `
<div class="screen active no-nav" style="display:flex;flex-direction:column;justify-content:center;min-height:100vh;">
  <div class="container">
    <div class="center mb16">
      <div style="font-size:40px;">🏢</div>
      <div class="display" style="font-size:19px;font-weight:900;">団体アカウント</div>
      <div class="faint">保護団体・シェルターの方向けログイン</div>
    </div>
    <div class="field"><label>団体メールアドレス</label><input type="email" id="oli-email" placeholder="shelter@example.com"></div>
    <div class="field"><label>パスワード</label><input type="password" id="oli-pass" placeholder="••••••••"></div>
    <button class="btn btn-org" onclick="doOrgLogin()">ログイン</button>
    <div class="divider"></div>
    <button class="btn btn-outline" onclick="nav('org-register-1')">新しく団体登録をする</button>
    <div class="center mt16"><a class="faint" onclick="nav('login')">← 里親希望の方はこちら</a></div>
  </div>
</div>`;
function doOrgLogin(){
  if(!S.orgUser) S.orgUser = SAMPLE_ORGS[0];
  toast('団体アカウントでログインしました');
  nav('org-dashboard');
}

/* ---- HOME / search ---- */
SCREENS['home'] = () => {
  const pets = filteredPets();
  return `
<div class="screen active">
  <div class="topbar">
    <div class="brand"><div class="mark">${HOUSE_MARK}</div><span>ワンニャンホーム</span></div>
    <button class="icon-btn" onclick="switchTab('notifications')">🔔${S.notifications.some(n=>!n.read)?'<span style=\"color:var(--accent)\">●</span>':''}</button>
  </div>
  <div class="container" style="padding-bottom:8px;">
    <div class="tabs-row mb8">
      ${['','dog','cat'].map(sp=>`<button class="tab-pill ${S.filters.species===sp?'active':''}" onclick="setSpecies('${sp}')">${sp===''?'すべて':speciesLabel(sp)}</button>`).join('')}
      <button class="tab-pill" onclick="nav('filters')">🎚️ 絞り込み ${activeFilterCount()>0?`(${activeFilterCount()})`:''}</button>
    </div>
    <div class="search-bar" onclick="promptKeyword()">
      <span>🔍</span><span id="kw-display">${S.filters.keyword || '犬種・猫種・名前で検索'}</span>
    </div>
    <div class="filter-bar">
      ${chipIf('area',S.filters.area)}${chipIf('breed',S.filters.breed)}${chipIf('faceType',S.filters.faceType)}${chipIf('coatColor',S.filters.coatColor)}${chipIf('bodyType',S.filters.bodyType)}
      <button class="filter-chip" onclick="nav('filters')">＋ 詳細条件</button>
    </div>
  </div>
  <div class="container" style="padding-top:0;">
    <div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:10px;">
      <span class="faint">${pets.length}件見つかりました</span>
      <span class="faint">🐾 AIおすすめ順</span>
    </div>
    ${pets.length===0 ? emptyState('😿','条件に合うペットが見つかりません','filters をリセット','resetFilters()') : pets.map(p=>petCard(p)).join('')}
  </div>
</div>`;
};
function chipIf(key,val){ return val ? `<span class="filter-chip on">${val} <span onclick="event.stopPropagation();clearFilter('${key}')" style="margin-left:2px;">✕</span></span>` : ''; }
function clearFilter(key){ S.filters[key]=''; render(); }
function setSpecies(sp){ S.filters.species = sp; render(); }
function promptKeyword(){
  const kw = prompt('犬種・猫種・名前などで検索', S.filters.keyword || '');
  if(kw!==null){ S.filters.keyword = kw.trim(); render(); }
}
function resetFilters(){ S.filters = {species:'', keyword:'', area:'', breed:'', sex:'', age:'', size:'', bodyType:'', faceType:'', coatColor:'', coatLength:'', pickup:''}; render(); }
function emptyState(ico,title,ctaLabel,ctaFn){
  return `<div class="empty-state"><span class="ico">${ico}</span><div style="font-weight:700;color:var(--text);">${title}</div>
  <button class="btn btn-outline-accent btn-sm cta" onclick="${ctaFn}">${ctaLabel}</button></div>`;
}
function petCard(p){
  const isBookmarked = S.bookmarks.has(p.id);
  const ms = matchScore(p);
  return `
  <div class="pet-card" onclick="openPet('${p.id}')">
    <div class="pet-thumb" style="background:${thumbColor(p)}">
      ${p.emoji}
      <button class="bookmark-btn" onclick="event.stopPropagation();toggleBookmark('${p.id}')">${isBookmarked?'🔖':'📑'}</button>
    </div>
    <div class="pet-info">
      <div style="display:flex;justify-content:space-between;align-items:flex-start;gap:6px;">
        <div>
          <span class="house-tag ${p.urgent?'urgent':''}">${p.urgent?'急募':'募集中'}</span>
          <div class="pname">${p.name}<span class="faint" style="font-weight:400;"> ・ ${p.breed}</span></div>
        </div>
        <div class="match-ring" style="--pct:${ms};"><div class="match-ring-inner">${ms}<small>MATCH</small></div></div>
      </div>
      <div class="pmeta">${p.sex} / ${p.age} / ${p.area}</div>
      <div class="tag-row">
        <span class="small-tag">${p.faceType}</span>
        <span class="small-tag">${p.coatColor}</span>
        <span class="small-tag">${p.size}</span>
        ${p.video?'<span class="small-tag">🎥動画</span>':''}
        ${p.scan3d?'<span class="small-tag">🧊3Dスキャン</span>':''}
      </div>
    </div>
  </div>`;
}
function toggleBookmark(id){
  if(S.bookmarks.has(id)) S.bookmarks.delete(id); else { S.bookmarks.add(id); toast('ブックマークに追加しました'); }
  render();
}

/* ---- FILTERS (goo-net style advanced) ---- */
SCREENS['filters'] = () => `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;"><button class="back-btn" onclick="nav('home')">‹</button><h1>詳細な絞り込み</h1></div></div>
  <div class="container" style="padding-bottom:110px;">
    <div class="section-title" style="font-size:15px;">基本条件</div>
    <div class="field"><label>種類</label>
      <div class="chip-group">
        ${['','dog','cat'].map(sp=>`<div class="chip ${S.filters.species===sp?'active':''}" onclick="fSet('species','${sp}')">${sp===''?'指定なし':speciesLabel(sp)}</div>`).join('')}
      </div>
    </div>
    <div class="field"><label>犬種・猫種</label>
      <div class="chip-group">${(S.filters.species==='cat'?BREEDS_CAT:S.filters.species==='dog'?BREEDS_DOG:[...BREEDS_DOG,...BREEDS_CAT]).map(b=>`<div class="chip ${S.filters.breed===b?'active':''}" onclick="fSet('breed','${b}')">${b}</div>`).join('')}</div>
    </div>
    <div class="field"><label>エリア（都道府県）</label>
      <select onchange="fSet('area', this.value)">
        <option value="">指定なし</option>
        ${AREAS.map(a=>`<option ${S.filters.area===a?'selected':''}>${a}</option>`).join('')}
      </select>
    </div>
    <div class="row2">
      <div class="field"><label>性別</label>
        <div class="chip-group">${['','オス','メス'].map(s=>`<div class="chip ${S.filters.sex===s?'active':''}" onclick="fSet('sex','${s}')">${s===''?'指定なし':s}</div>`).join('')}</div>
      </div>
    </div>

    <div class="divider"></div>
    <div class="section-title" style="font-size:15px;">🚗 ボディ・形状（グーネット式絞り込み）</div>
    <div class="field"><label>体の大きさ</label>
      <div class="chip-group">${['超小型','小型','中型','大型','超大型'].map(s=>`<div class="chip ${S.filters.size===s?'active':''}" onclick="fSet('size','${s}')">${s}</div>`).join('')}</div>
    </div>
    <div class="field"><label>体型</label>
      <div class="chip-group">${['スリム','がっしり','ぽっちゃり'].map(s=>`<div class="chip ${S.filters.bodyType===s?'active':''}" onclick="fSet('bodyType','${s}')">${s}</div>`).join('')}</div>
    </div>
    <div class="field"><label>毛の長さ</label>
      <div class="chip-group">${COAT_LENGTHS.map(s=>`<div class="chip ${S.filters.coatLength===s?'active':''}" onclick="fSet('coatLength','${s}')">${s}</div>`).join('')}</div>
    </div>

    <div class="divider"></div>
    <div class="section-title" style="font-size:15px;">✨ ルックス・特徴</div>
    <div class="field"><label>顔のタイプ</label>
      <div class="chip-group">${FACE_TYPES.map(s=>`<div class="chip chip-outline-select ${S.filters.faceType===s?'active':''}" onclick="fSet('faceType','${s}')">${s}</div>`).join('')}</div>
    </div>
    <div class="field"><label>毛色・カラー</label>
      <div class="chip-group">${COAT_COLORS.map(s=>`<div class="chip chip-outline-select ${S.filters.coatColor===s?'active':''}" onclick="fSet('coatColor','${s}')">${s}</div>`).join('')}</div>
    </div>

    <div class="divider"></div>
    <div class="section-title" style="font-size:15px;">🚚 受け渡し方法</div>
    <div class="field">
      <div class="chip-group">
        <div class="chip ${S.filters.pickup===''?'active':''}" onclick="fSet('pickup','')">指定なし</div>
        <div class="chip ${S.filters.pickup==='pickup'?'active':''}" onclick="fSet('pickup','pickup')">お迎え（取りに行く）</div>
        <div class="chip ${S.filters.pickup==='delivery'?'active':''}" onclick="fSet('pickup','delivery')">お届け（配送）</div>
      </div>
    </div>
  </div>
  <div class="sticky-cta" style="display:flex;gap:8px;">
    <button class="btn btn-outline" style="flex:0.5;" onclick="resetFilters();render();">リセット</button>
    <button class="btn btn-primary" onclick="nav('home')">${filteredPets().length}件を表示する</button>
  </div>
</div>`;
function fSet(k,v){ S.filters[k] = (S.filters[k]===v) ? '' : v; render(); }

/* ---- Pet Detail ---- */
SCREENS['pet-detail'] = () => {
  const p = petById(S.detailPetId);
  if(!p) return `<div class="container">見つかりませんでした</div>`;
  const org = orgById(p.orgId);
  const ms = matchScore(p);
  const bm = S.bookmarks.has(p.id);
  return `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;">
    <button class="back-btn" onclick="nav('home')">‹</button>
    <h1 style="flex:1;text-align:left;">${p.name}</h1>
    <button class="icon-btn" onclick="toggleBookmark('${p.id}');render()">${bm?'🔖':'📑'}</button>
  </div></div>
  <div style="height:230px;background:${thumbColor(p)};display:flex;align-items:center;justify-content:center;font-size:90px;position:relative;">
    ${p.emoji}
    <div style="position:absolute;top:12px;left:16px;"><span class="house-tag ${p.urgent?'urgent':''}">${p.urgent?'急募':'募集中'}</span></div>
    <div style="position:absolute;bottom:10px;right:14px;display:flex;gap:6px;">
      ${p.video?'<span class="small-tag" style="background:rgba(0,0,0,.5);color:#fff;">🎥 動画あり</span>':''}
      ${p.scan3d?'<span class="small-tag" style="background:rgba(0,0,0,.5);color:#fff;">🧊 3Dスキャン</span>':''}
    </div>
  </div>
  <div class="container">
    ${p.video || p.scan3d ? `<div class="card center" style="padding:14px;"><span style="font-size:13px;">${p.scan3d?'🧊 3Dモデルで360°ビュー':'🎥 動画でリアルな動きを確認'}（デモ）</span><div class="faint mt8">実際のアプリではLiDARスキャン・動画プレイヤーがここに表示されます</div></div>` : ''}

    <div style="display:flex;justify-content:space-between;align-items:center;margin:14px 0;">
      <div>
        <div class="display" style="font-size:22px;font-weight:900;">${p.name}</div>
        <div class="muted" style="font-size:13px;">${p.breed} / ${p.sex} / ${p.age}</div>
      </div>
      <div class="match-ring" style="--pct:${ms};width:64px;height:64px;"><div class="match-ring-inner" style="width:52px;height:52px;font-size:13px;">${ms}<small>適合度</small></div></div>
    </div>

    <div class="tag-row mb16">
      <span class="small-tag">📍${p.area}</span><span class="small-tag">${p.size}</span><span class="small-tag">${p.bodyType}</span>
      <span class="small-tag">${p.faceType}</span><span class="small-tag">${p.coatColor}</span><span class="small-tag">${p.coatLength}</span>
      <span class="small-tag">${pickupLabel(p.pickup)}</span>
    </div>

    <div class="section-title" style="font-size:15px;">プロフィール</div>
    <p class="section-sub">${p.desc}</p>

    <div class="card" onclick="nav('org-profile',{})" style="cursor:pointer;">
      <div style="display:flex;justify-content:space-between;align-items:center;">
        <div>
          <div style="font-weight:700;font-size:13.5px;">${org.name} ${org.verified?'✅':''}</div>
          <div class="faint">${S.user && S.user.membership>=2 ? org.area : org.area.split(' ')[0]+' ・ ▲▲区（メンバーシップで詳細表示）'}</div>
        </div>
        <span class="arrow">›</span>
      </div>
    </div>

    <div class="card">
      <div style="font-weight:700;font-size:13px;margin-bottom:8px;">💴 費用について</div>
      <div class="faint" style="line-height:1.8;">この子自体に価格はありません。ワクチン接種・不妊去勢手術・輸送などにかかった実費として<b style="color:var(--text);">手数料 ${fmtYen(feeFor(p))}</b>のお支払いをお願いしています。</div>
    </div>
  </div>
  <div class="sticky-cta" style="display:flex;gap:8px;">
    <button class="btn btn-secondary" style="flex:0.4;" onclick="openChatAbout('${p.id}')">💬 相談</button>
    <button class="btn btn-primary" onclick="startApply('${p.id}')">🏡 この子と家族になる</button>
  </div>
</div>`;
};
function feeFor(p){ return p.species==='dog' ? 38000 : 28000; }
function openPet(id){ S.detailPetId = id; nav('pet-detail'); }

/* ---- Org profile (public) ---- */
SCREENS['org-profile'] = () => {
  const p = petById(S.detailPetId); const org = orgById(p.orgId);
  return `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;"><button class="back-btn" onclick="nav('pet-detail')">‹</button><h1>団体プロフィール</h1></div></div>
  <div class="container">
    <div class="card center">
      <div style="font-size:40px;">🏢</div>
      <div class="display" style="font-weight:900;font-size:17px;margin-top:6px;">${org.name}</div>
      <div class="faint">動物取扱業登録：${org.license}</div>
      <div class="mt8">⭐ ${org.rating} ・ 掲載頭数 ${org.petsCount}頭 ${org.verified?'・ <span style="color:var(--accent-2);">本人確認済み団体</span>':''}</div>
    </div>
    <p class="section-sub">${org.desc}</p>
    <div class="stat-pill"><span>所在エリア</span><b>${S.user && S.user.membership>=2 ? org.area : 'メンバーシップで表示'}</b></div>
    <div class="stat-pill"><span>連絡先</span><b>${S.user && S.user.membership>=2 ? org.contact : 'アプリ内チャットのみ'}</b></div>
    <div class="section-title" style="font-size:15px;">掲載中のペット</div>
    ${SAMPLE_PETS.filter(x=>x.orgId===org.id).map(petCard).join('')}
  </div>
</div>`;
};

/* ---- Apply flow (multi step, single screen) ---- */
function startApply(petId){
  if(!requireAuth(()=>startApply(petId))) return;
  S.pendingApplyPet = petId; S.applyStep = 1; nav('apply-flow');
}
SCREENS['apply-flow'] = () => {
  const p = petById(S.pendingApplyPet);
  const step = S.applyStep;
  const fee = feeFor(p);
  return `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;"><button class="back-btn" onclick="applyBack()">‹</button><h1>${p.name}と家族になる</h1></div></div>
  <div class="container">
    <div class="steps">
      ${[1,2,3,4].map(i=>`<div class="dot ${step>i?'done':step===i?'now':''}"></div>`).join('')}
    </div>
    ${step===1?applyStep1(p,fee):''}
    ${step===2?applyStep2(p):''}
    ${step===3?applyStep3(p):''}
    ${step===4?applyStep4(p):''}
  </div>
</div>`;
};
function applyBack(){ if(S.applyStep>1){ S.applyStep--; render(); } else { nav('pet-detail'); } }
function applyStep1(p, fee){
  return `
  <div class="section-title">Step1. お受け渡し方法</div>
  <div class="chip-group mb16">
    ${p.pickup!=='delivery'?`<div class="chip ${S.applyDraftPickup==='pickup'?'active':''}" style="padding:16px;" onclick="setApplyPickup('pickup')">🚗 お迎え（施設まで取りに行く）</div>`:''}
    ${p.pickup!=='pickup'?`<div class="chip ${S.applyDraftPickup==='delivery'?'active':''}" style="padding:16px;" onclick="setApplyPickup('delivery')">📦 お届け（配送してもらう）</div>`:''}
  </div>
  <div class="card">
    <div style="font-weight:700;margin-bottom:8px;">お支払いいただく手数料</div>
    <div class="stat-pill"><span>医療・保護費用</span><b>${fmtYen(fee-8000)}</b></div>
    <div class="stat-pill"><span>${S.applyDraftPickup==='delivery'?'配送費（目安）':'事務手数料'}</span><b>${fmtYen(S.applyDraftPickup==='delivery'?8000+4000:8000)}</b></div>
    <div class="stat-pill" style="background:transparent;padding-top:12px;border-top:1px solid var(--border);border-radius:0;"><span style="font-weight:700;color:var(--text);">合計（デポジット）</span><b style="color:var(--accent);font-size:16px;">${fmtYen(S.applyDraftPickup==='delivery'?fee+4000:fee)}</b></div>
  </div>
  <p class="faint">※ 金額は保護・医療にかかった実費です。生体そのものへの対価ではありません。審査不成立の場合は返金または寄付への切替をお選びいただけます。</p>
  <button class="btn btn-primary mt8" onclick="applyGoStep(2)" ${!S.applyDraftPickup?'disabled':''}>次へ（お申込み内容の確認）</button>
  `;
}
function setApplyPickup(v){ S.applyDraftPickup = v; render(); }
function applyStep2(p){
  return `
  <div class="section-title">Step2. お申込み内容の確認</div>
  <div class="card">
    <div class="stat-pill"><span>お迎えする子</span><b>${p.name}（${p.breed}）</b></div>
    <div class="stat-pill"><span>受け渡し方法</span><b>${S.applyDraftPickup==='pickup'?'お迎え':'お届け'}</b></div>
    <div class="stat-pill"><span>お申込者</span><b>${S.user.name || '未設定'}</b></div>
    <div class="stat-pill"><span>ご連絡先</span><b>${S.user.phone || '未設定'}</b></div>
  </div>
  <div class="field"><label>飼育環境について（任意メモ）</label><textarea id="apply-note" placeholder="お住まいの形態、他のペットの有無など">${S.applyNote||''}</textarea></div>
  <div class="check-row"><input type="checkbox" id="apply-agree"><span>譲渡誓約書の内容を確認し、内容に同意します。動物虐待・転売は固く禁じられています。</span></div>
  <button class="btn btn-primary" onclick="applyStep2Next()">次へ（お支払い）</button>
  `;
}
function applyStep2Next(){
  if(!document.getElementById('apply-agree').checked){ toast('誓約書への同意が必要です'); return; }
  S.applyNote = document.getElementById('apply-note').value;
  applyGoStep(3);
}
function applyGoStep(n){ S.applyStep = n; render(); }
function applyStep3(p){
  const fee = feeFor(p) + (S.applyDraftPickup==='delivery'?4000:0);
  const hasCard = S.paymentMethods.length>0;
  return `
  <div class="section-title">Step3. お支払い（デポジット）</div>
  ${hasCard ? `
    <div class="credit-card-visual">
      <div style="display:flex;justify-content:space-between;"><span class="faint">登録済みカード</span><span>💳</span></div>
      <div class="cc-num">•••• •••• •••• ${S.paymentMethods[0].last4}</div>
      <div class="cc-bottom"><span>${S.paymentMethods[0].holder}</span><span>${S.paymentMethods[0].exp}</span></div>
    </div>
  `: `
    <div class="field"><label>カード番号<span class="req">必須</span></label><input type="text" id="pay-num" placeholder="4242 4242 4242 4242" maxlength="19"></div>
    <div class="row2">
      <div class="field"><label>有効期限</label><input type="text" id="pay-exp" placeholder="MM/YY"></div>
      <div class="field"><label>セキュリティコード</label><input type="text" id="pay-cvc" placeholder="123"></div>
    </div>
    <div class="field"><label>カード名義</label><input type="text" id="pay-holder" placeholder="TARO YAMADA"></div>
  `}
  <div class="card">
    <div class="stat-pill" style="background:transparent;padding:6px 4px;"><span style="font-weight:700;color:var(--text);">お支払い金額（一時預かり）</span><b style="color:var(--accent);font-size:17px;">${fmtYen(fee)}</b></div>
  </div>
  <p class="faint">審査（オンライン面談）に通過した時点で正式に決済が確定します。不成立の場合、全額返金または保護活動への寄付をお選びいただけます。</p>
  <button class="btn btn-primary" onclick="applyPay()">${fmtYen(fee)} を仮決済してオンライン審査に進む</button>
  `;
}
function applyPay(){
  if(S.paymentMethods.length===0){
    const num = document.getElementById('pay-num').value.trim();
    const exp = document.getElementById('pay-exp').value.trim();
    const cvc = document.getElementById('pay-cvc').value.trim();
    const holder = document.getElementById('pay-holder').value.trim();
    if(!num || !exp || !cvc || !holder){ toast('カード情報をすべて入力してください'); return; }
    S.paymentMethods.push({last4:num.replace(/\s/g,'').slice(-4)||'0000', exp, holder});
  }
  toast('デポジット決済が完了しました');
  applyGoStep(4);
}
function applyStep4(p){
  const appId = 'A'+Math.floor(Math.random()*90000+10000);
  if(!S.applyCreated){
    S.applications.push({id:appId, petId:p.id, orgId:p.orgId, status:'審査中（オンライン面談待ち）', createdAt:'2026/07/30'});
    p.applied = true;
    S.applyCreated = true;
    S.notifications.unshift({id:Date.now(), title:'オンライン面談の日程調整', body:`${orgById(p.orgId).name}からのご連絡です。マイページのチャットで日程をご相談ください。`, time:'たった今', read:false});
  }
  return `
  <div class="center" style="padding:20px 0;">
    <div style="font-size:52px;">🎉</div>
    <div class="display mt12" style="font-size:19px;font-weight:900;">お申込みを受け付けました</div>
    <p class="section-sub">次はオンライン面談で飼育環境の確認を行います。担当団体からチャットにてご連絡します。</p>
    <div class="card" style="text-align:left;">
      <div class="stat-pill"><span>お申込み番号</span><b class="mono">${appId}</b></div>
      <div class="stat-pill"><span>ステータス</span><b style="color:var(--accent-3);">審査中</b></div>
      <div class="stat-pill"><span>次のステップ</span><b>オンライン面談の日程調整</b></div>
    </div>
    <button class="btn btn-primary mt16" onclick="finishApply()">マイページで申込み状況を見る</button>
    <button class="btn btn-outline mt8" onclick="nav('home')">ほかの子も見てみる</button>
  </div>`;
}
function finishApply(){ S.applyCreated=false; S.applyDraftPickup=null; S.applyNote=''; nav('application-history'); }
function openChatAbout(petId){
  if(!requireAuth(()=>openChatAbout(petId))) return;
  const p = petById(petId);
  S.chatHistory.push({from:'bot', text:`${p.name}について何でも聞いてくださいね🐾 性格やお迎えまでの流れなど、お答えします。`});
  switchTab('chat');
}

/* ---- AI CHAT ---- */
SCREENS['ai-chat'] = () => {
  if(!S.authed){
    return `<div class="screen active"><div class="topbar"><div class="brand"><div class="mark">${HOUSE_MARK}</div><span>AIマッチング相談</span></div></div>
    ${emptyState('💬','ログインするとAIがあなたにぴったりの子を提案します','ログイン / 会員登録','nav(\'auth-gate\')')}</div>`;
  }
  if(S.chatHistory.length===0){
    S.chatHistory.push({from:'bot', text:'こんにちは🐾 わたしはワンニャンホームのAI相談員です。チャット形式でご希望をヒアリングして、ぴったりの保護犬・保護猫をご提案します。'});
    S.chatHistory.push({from:'bot', text:'まずは、犬・猫どちらをお探しですか？', suggests:['犬を探している','猫を探している','決めていない']});
  }
  return `
<div class="screen active">
  <div class="topbar"><div class="brand"><div class="mark">${HOUSE_MARK}</div><span>AIマッチング相談</span></div></div>
  <div class="chat-wrap">
    ${S.chatHistory.map(m=>renderMsg(m)).join('')}
  </div>
  <div class="chat-input-bar">
    <input type="text" id="chat-input" placeholder="メッセージを入力…" onkeydown="if(event.key==='Enter')sendChat()">
    <button onclick="sendChat()">➤</button>
  </div>
</div>`;
};
function renderMsg(m){
  let html = `<div class="msg ${m.from==='bot'?'bot':'user'}">${m.text}</div>`;
  if(m.suggests){
    html += `<div class="chat-suggests">${m.suggests.map(s=>`<button class="suggest-btn" onclick="pickSuggest('${s.replace(/'/g,"\\'")}')">${s}</button>`).join('')}</div>`;
  }
  if(m.petIds){
    html += m.petIds.map(id=>{
      const p = petById(id);
      return `<div class="pet-suggest-card" onclick="openPet('${id}')">
        <div class="pet-thumb" style="width:56px;height:56px;font-size:24px;background:${thumbColor(p)}">${p.emoji}</div>
        <div><div style="font-weight:700;font-size:13px;">${p.name}・${p.breed}</div><div class="faint">${p.area} / ${p.faceType}</div></div>
      </div>`;
    }).join('');
  }
  return html;
}
function pickSuggest(text){
  document.getElementById('chat-input').value = text;
  sendChat();
}
function sendChat(){
  const input = document.getElementById('chat-input');
  const text = input.value.trim();
  if(!text) return;
  S.chatHistory.push({from:'user', text});
  input.value='';
  render();
  setTimeout(()=>{ botReply(text); render(); document.getElementById('chat-input')?.focus(); }, 350);
}
function botReply(text){
  const st = S.chatProfile;
  if(text.includes('犬')){ st.species='dog'; }
  else if(text.includes('猫')){ st.species='cat'; }

  if(st.stage===0){
    st.stage=1;
    S.chatHistory.push({from:'bot', text:'ありがとうございます！お住まいのエリア（都道府県）を教えてください。', suggests:['大阪府','東京都','福岡県']});
    return;
  }
  if(st.stage===1){
    st.area = AREAS.find(a=>text.includes(a.slice(0,2))) || text;
    st.stage=2;
    S.chatHistory.push({from:'bot', text:'お迎えの方法は「取りに行く」「配送してもらう」どちらがご希望ですか？', suggests:['取りに行きたい','配送してほしい','どちらでも良い']});
    return;
  }
  if(st.stage===2){
    st.pickup = text.includes('配送') ? 'delivery' : text.includes('取り') ? 'pickup' : 'both';
    st.stage=3;
    S.chatHistory.push({from:'bot', text:'見た目の好みはありますか？（丸顔・キツネ顔・毛色など、気軽にどうぞ）', suggests:['丸顔がいい','キツネ顔がいい','特にこだわりなし']});
    return;
  }
  if(st.stage===3){
    if(text.includes('丸顔')) st.faceType='丸顔';
    else if(text.includes('キツネ')) st.faceType='キツネ顔';
    st.stage=4;
    // apply filters + recommend
    S.filters.species = st.species||''; S.filters.area = st.area||''; S.filters.faceType = st.faceType||'';
    const results = filteredPets().slice(0,3);
    S.chatHistory.push({from:'bot', text:'ありがとうございます！条件からAIがマッチ度の高い子をピックアップしました🐾 気になる子をタップすると詳細が見られます。', petIds: results.length ? results.map(p=>p.id) : SAMPLE_PETS.slice(0,3).map(p=>p.id)});
    S.chatHistory.push({from:'bot', text:'他にも「移動費っていくら？」「本人確認って何が必要？」など、なんでも質問してくださいね。'});
    return;
  }
  // free-form Q&A stage
  if(text.includes('費用') || text.includes('金額') || text.includes('いくら') || text.includes('手数料')){
    S.chatHistory.push({from:'bot', text:'ペット自体に金額はかけていません。ワクチン等の医療費や輸送費などの実費として、犬で約¥38,000〜、猫で約¥28,000〜の手数料をお願いしています。'});
  } else if(text.includes('本人確認') || text.includes('審査')){
    S.chatHistory.push({from:'bot', text:'ご登録時に氏名・住所・電話番号・身分証のアップロードが必要です。虐待・転売防止のため、通過するまでは一部機能が制限されます。'});
  } else if(text.includes('面談') || text.includes('会う') || text.includes('会える')){
    S.chatHistory.push({from:'bot', text:'お申込み後、施設スタッフとのオンライン面談で飼育環境を確認します。対面での面接は不要ですが、最終引き渡し時は必ず一度、対面または現地でのご確認をお願いしています。'});
  } else {
    S.chatHistory.push({from:'bot', text:'なるほど、ありがとうございます。もう少し詳しく教えていただけますか？条件を「さがす」画面の詳細フィルタにも反映できますよ。', suggests:['検索条件に反映して','担当団体に相談したい']});
  }
}

/* ---- BOOKMARKS ---- */
SCREENS['bookmarks'] = () => {
  const list = [...S.bookmarks].map(petById).filter(Boolean);
  return `
<div class="screen active">
  <div class="topbar"><h1>ブックマーク</h1></div>
  <div class="container">
    ${list.length===0 ? emptyState('🔖','ブックマークはまだありません','保護犬・保護猫をさがす','switchTab(\'home\')') : list.map(petCard).join('')}
  </div>
</div>`;
};

/* ---- NOTIFICATIONS ---- */
SCREENS['notifications'] = () => {
  S.notifications.forEach(n=>n.read=true);
  return `
<div class="screen active">
  <div class="topbar"><h1>通知</h1></div>
  <div class="container">
    ${S.notifications.length===0 ? emptyState('🔔','通知はありません','','') : S.notifications.map(n=>`
      <div class="card"><div style="font-weight:700;font-size:13.5px;margin-bottom:4px;">${n.title}</div><div class="faint" style="line-height:1.6;">${n.body}</div><div class="faint mt8">${n.time}</div></div>
    `).join('')}
  </div>
</div>`;
};

/* ---- MYPAGE ---- */
SCREENS['mypage'] = () => {
  if(!S.authed){
    return `<div class="screen active"><div class="topbar"><h1>マイページ</h1></div>${emptyState('👤','ログインして会員情報を確認しましょう','ログイン / 会員登録','nav(\'auth-gate\')')}</div>`;
  }
  const u = S.user;
  const rankName = u.membership===3?'スポンサー会員':u.membership===2?'プラス会員':'無料会員';
  const rankClass = u.membership===3?'rank-3':u.membership===2?'rank-2':'rank-1';
  return `
<div class="screen active">
  <div class="topbar"><h1>マイページ</h1></div>
  <div class="container">
    <div class="profile-head">
      <div class="avatar-lg">${u.avatarEmoji}</div>
      <div>
        <div class="display" style="font-weight:900;font-size:17px;">${u.name || '（お名前未設定）'}</div>
        <div class="faint">${u.email}</div>
        <span class="rank-badge ${rankClass}">🏅 ${rankName}</span>
        ${u.kycStatus==='pending' ? '<span class="rank-badge" style="background:rgba(242,184,75,.18);color:var(--accent-3);margin-left:4px;">審査中</span>':''}
      </div>
    </div>
    <div class="row2 mt16">
      <button class="btn btn-outline btn-sm" style="width:100%;" onclick="nav('profile-edit')">✏️ プロフィール編集</button>
      <button class="btn btn-outline btn-sm" style="width:100%;" onclick="nav('membership')">🏅 メンバーシップ</button>
    </div>

    <div class="divider"></div>
    <div class="list-row" onclick="nav('application-history')"><div class="left"><span>📮</span><div>応募・お申込み管理<div class="desc">${S.applications.length}件</div></div></div><span class="arrow">›</span></div>
    <div class="list-row" onclick="switchTab('bookmarks')"><div class="left"><span>🔖</span><div>ブックマーク<div class="desc">${S.bookmarks.size}件</div></div></div><span class="arrow">›</span></div>
    <div class="list-row" onclick="nav('payment-methods')"><div class="left"><span>💳</span><div>お支払い方法<div class="desc">${S.paymentMethods.length}件登録</div></div></div><span class="arrow">›</span></div>
    <div class="list-row" onclick="alert('デモ：専門家紹介一覧はまだありません。近日公開予定です。')"><div class="left"><span>🎓</span><div>ドッグトレーナー紹介<div class="desc">譲渡後の飼育サポート</div></div></div><span class="arrow">›</span></div>
    <div class="list-row" onclick="alert('デモ：ペット用品ECは近日公開予定です。')"><div class="left"><span>🛍️</span><div>ペット用品ショップ<div class="desc">首輪・フード・おもちゃ</div></div></div><span class="arrow">›</span></div>

    <div class="divider"></div>
    <div class="section-title" style="font-size:14px;">設定</div>
    <div class="list-row" onclick="nav('account-settings')"><div class="left"><span>⚙️</span><div>アカウント設定</div></div><span class="arrow">›</span></div>
    <div class="list-row" onclick="nav('notification-settings')"><div class="left"><span>🔔</span><div>通知設定</div></div><span class="arrow">›</span></div>
    <div class="list-row" onclick="nav('privacy-settings')"><div class="left"><span>🔒</span><div>プライバシー設定</div></div><span class="arrow">›</span></div>
    <div class="list-row" onclick="nav('privacy-policy')"><div class="left"><span>📄</span><div>プライバシーポリシー</div></div><span class="arrow">›</span></div>
    <div class="list-row" onclick="nav('terms')"><div class="left"><span>📜</span><div>利用規約</div></div><span class="arrow">›</span></div>
    <div class="list-row" onclick="nav('org-login')"><div class="left"><span>🏢</span><div>保護団体の方はこちら</div></div><span class="arrow">›</span></div>
    <div class="divider"></div>
    <button class="btn btn-outline mt8" onclick="doLogout()">ログアウト</button>
    <div class="center mt16"><a class="faint" style="text-decoration:underline;" onclick="confirmDeleteAccount()">退会する</a></div>
  </div>
</div>`;
};
function doLogout(){ S.authed=false; toast('ログアウトしました'); nav('splash'); }
function confirmDeleteAccount(){ if(confirm('本当に退会しますか？この操作は取り消せません。')){ S.authed=false; S.user=null; toast('退会が完了しました'); nav('splash'); } }

/* ---- Profile edit ---- */
SCREENS['profile-edit'] = () => {
  const u = S.user;
  return `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;"><button class="back-btn" onclick="nav('mypage')">‹</button><h1>プロフィール編集</h1></div></div>
  <div class="container">
    <div class="center mb16">
      <div class="avatar-lg" style="margin:0 auto;">${u.avatarEmoji}</div>
      <div class="chip-group center mt8" style="justify-content:center;">
        ${['🙂','😺','🐶','🐱','🧑','👩'].map(e=>`<div class="chip ${u.avatarEmoji===e?'active':''}" onclick="setAvatar('${e}')">${e}</div>`).join('')}
      </div>
    </div>
    <div class="field"><label>お名前</label><input type="text" id="pe-name" value="${u.name||''}"></div>
    <div class="field"><label>フリガナ</label><input type="text" id="pe-kana" value="${u.kana||''}"></div>
    <div class="field"><label>メールアドレス</label><input type="email" id="pe-email" value="${u.email||''}"></div>
    <div class="field"><label>電話番号</label><input type="tel" id="pe-phone" value="${u.phone||''}"></div>
    <div class="field"><label>生年月日</label><input type="date" id="pe-birth" value="${u.birthdate||''}"></div>
    <div class="field"><label>ご住所</label><input type="text" id="pe-address" value="${u.address||''}"></div>
    <div class="field"><label>自己紹介（任意・団体には公開されません）</label><textarea id="pe-bio" placeholder="ご家族構成やペット飼育経験など">${u.bio||''}</textarea></div>
    <div class="field">
      <label>本人確認書類</label>
      <div class="upload-box filled">✅ ${u.idUploaded?'提出済み（審査ステータス：'+(u.kycStatus==='pending'?'審査中':'承認済み')+'）':'未提出'}</div>
      <button class="btn btn-outline btn-sm mt8" onclick="mockReuploadID()">再アップロードする</button>
    </div>
    <button class="btn btn-primary mt8" onclick="saveProfile()">保存する</button>
  </div>
</div>`;
};
function setAvatar(e){ S.user.avatarEmoji = e; render(); }
function mockReuploadID(){ S.user.kycStatus='pending'; toast('書類を再提出しました。審査中です。'); render(); }
function saveProfile(){
  const u = S.user;
  u.name = document.getElementById('pe-name').value;
  u.kana = document.getElementById('pe-kana').value;
  u.email = document.getElementById('pe-email').value;
  u.phone = document.getElementById('pe-phone').value;
  u.birthdate = document.getElementById('pe-birth').value;
  u.address = document.getElementById('pe-address').value;
  u.bio = document.getElementById('pe-bio').value;
  toast('プロフィールを保存しました');
  nav('mypage');
}

/* ---- Membership ---- */
SCREENS['membership'] = () => {
  const u = S.user;
  const plans = [
    {tier:1, name:'無料会員', price:'¥0', perks:['基本的な閲覧・検索','AIチャット相談','ブックマーク']},
    {tier:2, name:'プラス会員', price:'¥3,600 / 年', perks:['団体の詳細所在地を表示','人気の子への優先応募権','3Dスキャン・動画の先行公開']},
    {tier:3, name:'スポンサー会員', price:'¥12,000 / 年', perks:['プラス会員の全特典','保護活動エリアへの投票権','アプリ内アワード選出権','団体への直接支援バッジ表示'] },
  ];
  return `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;"><button class="back-btn" onclick="nav('mypage')">‹</button><h1>メンバーシップ</h1></div></div>
  <div class="container">
    <p class="section-sub">保護活動の運営コストを支えるサブスクリプションです。基本機能は無料のままご利用いただけます。</p>
    ${plans.map(p=>`
      <div class="card" style="border-color:${u.membership===p.tier?'var(--accent)':'var(--border)'};">
        <div style="display:flex;justify-content:space-between;align-items:center;">
          <div style="font-weight:800;font-family:'Zen Maru Gothic',sans-serif;">${p.name}</div>
          <div style="color:var(--accent-3);font-weight:700;">${p.price}</div>
        </div>
        <ul style="margin:10px 0 4px;padding-left:18px;font-size:12.5px;color:var(--text-muted);line-height:1.9;">
          ${p.perks.map(x=>`<li>${x}</li>`).join('')}
        </ul>
        <button class="btn ${u.membership===p.tier?'btn-secondary':'btn-primary'} btn-sm mt8" style="width:100%;" onclick="setMembership(${p.tier})" ${u.membership===p.tier?'disabled':''}>${u.membership===p.tier?'現在のプラン':(p.tier===1?'無料プランに変更':'このプランにする')}</button>
      </div>
    `).join('')}
  </div>
</div>`;
};
function setMembership(tier){
  if(tier>1 && S.paymentMethods.length===0){ toast('お支払い方法の登録が必要です'); nav('payment-methods'); return; }
  S.user.membership = tier;
  toast('メンバーシップを更新しました');
  render();
}

/* ---- Payment methods ---- */
SCREENS['payment-methods'] = () => {
  return `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;"><button class="back-btn" onclick="nav('mypage')">‹</button><h1>お支払い方法</h1></div></div>
  <div class="container">
    ${S.paymentMethods.length? S.paymentMethods.map((c,i)=>`
      <div class="credit-card-visual">
        <div style="display:flex;justify-content:space-between;"><span class="faint">クレジットカード</span><span>💳</span></div>
        <div class="cc-num">•••• •••• •••• ${c.last4}</div>
        <div class="cc-bottom"><span>${c.holder}</span><span>${c.exp}</span></div>
        <button class="btn btn-danger btn-sm mt12" onclick="removeCard(${i})">このカードを削除</button>
      </div>
    `).join('') : emptyState('💳','登録済みのお支払い方法はありません','','')}
    <div class="divider"></div>
    <div class="section-title" style="font-size:15px;">カードを追加</div>
    <div class="field"><label>カード番号</label><input type="text" id="cc-num" placeholder="4242 4242 4242 4242"></div>
    <div class="row2">
      <div class="field"><label>有効期限</label><input type="text" id="cc-exp" placeholder="MM/YY"></div>
      <div class="field"><label>セキュリティコード</label><input type="text" id="cc-cvc" placeholder="123"></div>
    </div>
    <div class="field"><label>カード名義</label><input type="text" id="cc-holder" placeholder="TARO YAMADA"></div>
    <button class="btn btn-primary" onclick="addCard()">カードを登録する</button>
    <p class="faint mt8">カード情報は決済代行会社にて暗号化して管理されます（デモ環境のため実際の課金は発生しません）。</p>
  </div>
</div>`;
};
function addCard(){
  const num=document.getElementById('cc-num').value.trim();
  const exp=document.getElementById('cc-exp').value.trim();
  const cvc=document.getElementById('cc-cvc').value.trim();
  const holder=document.getElementById('cc-holder').value.trim();
  if(!num||!exp||!cvc||!holder){ toast('すべての項目を入力してください'); return; }
  S.paymentMethods.push({last4:num.replace(/\s/g,'').slice(-4)||'0000', exp, holder});
  toast('カードを登録しました');
  nav('payment-methods');
}
function removeCard(i){ S.paymentMethods.splice(i,1); render(); }

/* ---- Application history ---- */
SCREENS['application-history'] = () => {
  return `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;"><button class="back-btn" onclick="nav('mypage')">‹</button><h1>応募・お申込み管理</h1></div></div>
  <div class="container">
    ${S.applications.length===0 ? emptyState('📮','お申込み中の案件はありません','保護犬・保護猫をさがす','switchTab(\'home\')') :
      S.applications.map(a=>{
        const p = petById(a.petId); const org = orgById(a.orgId);
        return `<div class="card">
          <div style="display:flex;justify-content:space-between;"><span class="mono faint">#${a.id}</span><span style="color:var(--accent-3);font-weight:700;font-size:12.5px;">${a.status}</span></div>
          <div style="font-weight:700;margin-top:6px;">${p.name}（${p.breed}）</div>
          <div class="faint">${org.name}・お申込み日：${a.createdAt}</div>
          <button class="btn btn-outline btn-sm mt12" style="width:100%;" onclick="openChatAbout('${p.id}')">担当団体にチャットで連絡</button>
        </div>`;
      }).join('')}
  </div>
</div>`;
};

/* ---- Account settings ---- */
SCREENS['account-settings'] = () => {
  const u = S.user;
  return `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;"><button class="back-btn" onclick="nav('mypage')">‹</button><h1>アカウント設定</h1></div></div>
  <div class="container">
    <div class="list-row"><div class="left"><div>ユーザーID<div class="desc mono">UID-${(u.email||'').length*137}</div></div></div></div>
    <div class="list-row" onclick="nav('profile-edit')"><div class="left"><div>登録情報の変更</div></div><span class="arrow">›</span></div>
    <div class="list-row" onclick="changePassword()"><div class="left"><div>パスワードを変更</div></div><span class="arrow">›</span></div>
    <div class="list-row" onclick="nav('payment-methods')"><div class="left"><div>お支払い方法</div></div><span class="arrow">›</span></div>
    <div class="list-row" onclick="nav('membership')"><div class="left"><div>メンバーシップ管理</div></div><span class="arrow">›</span></div>
    <div class="divider"></div>
    <div class="field"><label>言語</label><select><option>日本語</option><option>English</option></select></div>
    <button class="btn btn-danger mt16" onclick="confirmDeleteAccount()">アカウントを削除する</button>
  </div>
</div>`;
};
function changePassword(){
  const np = prompt('新しいパスワードを入力してください（8文字以上）');
  if(np && np.length>=8){ toast('パスワードを変更しました'); } else if(np){ toast('8文字以上で入力してください'); }
}

/* ---- Notification settings ---- */
SCREENS['notification-settings'] = () => {
  const u = S.user;
  return `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;"><button class="back-btn" onclick="nav('mypage')">‹</button><h1>通知設定</h1></div></div>
  <div class="container">
    ${toggleRow('notifyNew','新着ペットのお知らせ','希望条件に合う子が掲載されたとき')}
    ${toggleRow('notifyChat','チャット・面談の通知','団体からのメッセージ、面談日程の連絡')}
    ${toggleRow('notifyMail','メールマガジン','保護活動レポートやキャンペーン情報')}
  </div>
</div>`;
};
function toggleRow(key,label,desc){
  const on = S.user[key];
  return `<div class="list-row"><div class="left"><div>${label}<div class="desc">${desc}</div></div></div>
    <div class="toggle ${on?'on':''}" onclick="toggleNotif('${key}')"></div></div>`;
}
function toggleNotif(key){ S.user[key] = !S.user[key]; render(); }

/* ---- Privacy settings ---- */
SCREENS['privacy-settings'] = () => {
  return `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;"><button class="back-btn" onclick="nav('mypage')">‹</button><h1>プライバシー設定</h1></div></div>
  <div class="container">
    <div class="list-row"><div class="left"><div>プロフィール公開範囲<div class="desc">団体への応募時のみニックネームを公開</div></div></div>
      <div class="toggle on"></div></div>
    <div class="list-row"><div class="left"><div>所在地の詳細開示<div class="desc">市区町村レベルまで団体に共有</div></div></div>
      <div class="toggle"></div></div>
    <div class="list-row" onclick="nav('privacy-policy')"><div class="left"><div>プライバシーポリシーを見る</div></div><span class="arrow">›</span></div>
    <div class="list-row" onclick="exportData()"><div class="left"><div>登録データをダウンロード</div></div><span class="arrow">›</span></div>
    <div class="list-row" onclick="confirmDeleteAccount()"><div class="left"><div style="color:var(--danger);">個人情報の削除をリクエスト</div></div><span class="arrow">›</span></div>
  </div>
</div>`;
};
function exportData(){ toast('登録データのエクスポートをメールで送信しました（デモ）'); }

/* ---- Privacy policy (full text) ---- */
SCREENS['privacy-policy'] = () => `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;"><button class="back-btn" onclick="nav(S.authed?'mypage':'auth-gate')">‹</button><h1>プライバシーポリシー</h1></div></div>
  <div class="container legal-text">
    <p class="faint">制定日：2026年7月30日</p>
    <p>「ワンニャンホーム」（以下「本サービス」）は、利用者および保護団体の個人情報を適切に取り扱うため、以下のとおりプライバシーポリシーを定めます。</p>
    <h4>1. 取得する情報</h4>
    <ul>
      <li>氏名、フリガナ、生年月日、住所、電話番号、メールアドレス</li>
      <li>本人確認書類の画像データ</li>
      <li>お支払い情報（決済代行会社を通じて処理し、カード番号自体は当社サーバーに保存しません）</li>
      <li>検索履歴・チャット相談履歴・アプリの利用状況</li>
    </ul>
    <h4>2. 利用目的</h4>
    <ul>
      <li>本人確認および不正利用（虐待・転売目的等）の防止</li>
      <li>保護犬・保護猫と利用者のマッチング、AIによるレコメンド</li>
      <li>保護団体との連絡調整、オンライン面談の実施</li>
      <li>手数料決済の処理、メンバーシップ料金の請求</li>
      <li>サービス改善、統計データの作成（個人を特定できない形式に加工）</li>
    </ul>
    <h4>3. 第三者提供</h4>
    <p>応募が成立した場合に限り、ニックネーム・お住まいの都道府県・年齢・性別を、応募先の保護団体に開示します。法令に基づく場合を除き、ご本人の同意なく第三者に個人情報を提供することはありません。</p>
    <h4>4. 保管・管理</h4>
    <p>取得した個人情報はSSL暗号化通信により保護し、アクセス権限を最小限に制限したサーバーにて管理します。決済情報はPCI DSS準拠の決済代行会社にて管理します。</p>
    <h4>5. 保存期間</h4>
    <p>退会後、法令で定める期間を除き、原則として90日以内に個人を特定できる情報を削除します。</p>
    <h4>6. Cookie等の利用</h4>
    <p>サービス改善のため、Cookie等の技術を利用する場合があります。ブラウザ設定により無効化が可能です。</p>
    <h4>7. 開示・訂正・削除請求</h4>
    <p>ご本人からの開示・訂正・削除のご請求には、本人確認のうえ速やかに対応します。マイページの「プライバシー設定」からリクエストが可能です。</p>
    <h4>8. お問い合わせ窓口</h4>
    <p>ワンニャンホーム運営事務局　support@wannyan-home.jp（デモ用ダミー窓口）</p>
  </div>
</div>`;

/* ---- Terms (full text) ---- */
SCREENS['terms'] = () => `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;"><button class="back-btn" onclick="nav(S.authed?'mypage':'auth-gate')">‹</button><h1>利用規約</h1></div></div>
  <div class="container legal-text">
    <p class="faint">制定日：2026年7月30日</p>
    <h4>第1条（適用）</h4>
    <p>本規約は、ワンニャンホーム（以下「当社」）が提供する保護犬・保護猫マッチングサービス「ワンニャンホーム」（以下「本サービス」）の利用条件を定めるものです。</p>
    <h4>第2条（会員登録）</h4>
    <ol>
      <li>本サービスの利用には会員登録および本人確認手続きが必要です。</li>
      <li>虚偽の情報での登録が判明した場合、当社は登録を拒否または取り消すことができます。</li>
      <li>同一利用者による複数アカウントの保有を禁止します。</li>
    </ol>
    <h4>第3条（禁止事項）</h4>
    <ul>
      <li>動物への虐待、遺棄、転売、繁殖目的での取得</li>
      <li>他の利用者・保護団体への迷惑行為、なりすまし</li>
      <li>本サービスを通じて知り得た個人情報の目的外利用</li>
      <li>虚偽の飼育環境情報の提出</li>
    </ul>
    <h4>第4条（手数料）</h4>
    <p>本サービスにおいて動物そのものへの対価は発生しません。譲渡にあたっては、保護・医療・輸送等にかかった実費として手数料が発生します。手数料の金額は各募集ページに表示します。</p>
    <h4>第5条（デポジットの取扱い）</h4>
    <p>お申込み時に一時預かり金（デポジット）としてお支払いいただいた手数料は、オンライン審査（飼育環境確認）を通過した時点で正式に確定します。審査不成立の場合、利用者は全額返金または保護活動への寄付への切替を選択できます。</p>
    <h4>第6条（譲渡誓約書）</h4>
    <p>正式な譲渡にあたっては、保護団体との間で譲渡誓約書を取り交わすものとします。誓約書を取り交わさない譲渡は動物虐待とみなされる可能性があり、当社は当該取引の仲介責任を負いません。</p>
    <h4>第7条（メンバーシップ）</h4>
    <p>有料メンバーシップは年額課金制とし、期間内の解約であっても原則として日割り返金は行いません。詳細はメンバーシップ規約に定めます。</p>
    <h4>第8条（免責事項）</h4>
    <p>当社は保護団体と利用者間のマッチングの場を提供するものであり、譲渡された動物の健康状態や譲渡後のトラブルについて一切の責任を負いません。ただし、悪質な事案が判明した場合は関係機関と連携し対応します。</p>
    <h4>第9条（規約の変更）</h4>
    <p>当社は必要と判断した場合、利用者への事前通知のうえ本規約を変更できるものとします。</p>
  </div>
</div>`;

/* ============================= ORG SIDE ============================= */
SCREENS['org-register-1'] = () => `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;"><button class="back-btn" onclick="nav('org-login')">‹</button><h1>団体登録（1/3）</h1></div></div>
  <div class="container">
    <div class="steps"><div class="dot now"></div><div class="dot"></div><div class="dot"></div></div>
    <div class="section-title">団体の基本情報</div>
    <div class="field"><label>団体名<span class="req">必須</span></label><input type="text" id="or-name" placeholder="例）NPO法人 ○○動物保護会" value="${S.orgDraftPet.orgName||''}"></div>
    <div class="field"><label>法人格・種別</label>
      <select id="or-type"><option>NPO法人</option><option>一般社団法人</option><option>任意団体</option><option>個人ボランティア</option></select>
    </div>
    <div class="field"><label>動物取扱業登録番号<span class="req">必須</span></label><input type="text" id="or-license" placeholder="第xx-動保-xxxx号"></div>
    <div class="field"><label>代表者名<span class="req">必須</span></label><input type="text" id="or-rep" placeholder="山田 花子"></div>
    <div class="field"><label>団体紹介文</label><textarea id="or-desc" placeholder="活動内容や保護動物の受け入れ方針など"></textarea></div>
    <button class="btn btn-org" onclick="orgStep1Next()">次へ（所在地・連絡先）</button>
  </div>
</div>`;
function orgStep1Next(){
  const name=document.getElementById('or-name').value, license=document.getElementById('or-license').value, rep=document.getElementById('or-rep').value;
  if(!name||!license||!rep){ toast('必須項目を入力してください'); return; }
  S.orgReg = {name, type:document.getElementById('or-type').value, license, rep, desc:document.getElementById('or-desc').value};
  nav('org-register-2');
}
SCREENS['org-register-2'] = () => `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;"><button class="back-btn" onclick="nav('org-register-1')">‹</button><h1>団体登録（2/3）</h1></div></div>
  <div class="container">
    <div class="steps"><div class="dot done"></div><div class="dot now"></div><div class="dot"></div></div>
    <div class="section-title">所在地・連絡先・施設情報</div>
    <div class="row2">
      <div class="field"><label>郵便番号</label><input type="text" id="or-zip" placeholder="123-4567"></div>
      <div class="field"><label>都道府県</label><select id="or-pref">${AREAS.map(a=>`<option>${a}</option>`).join('')}</select></div>
    </div>
    <div class="field"><label>住所</label><input type="text" id="or-address" placeholder="市区町村・番地"></div>
    <div class="field"><label>電話番号<span class="req">必須</span></label><input type="tel" id="or-phone" placeholder="06-xxxx-xxxx"></div>
    <div class="field"><label>メールアドレス<span class="req">必須</span></label><input type="email" id="or-email" placeholder="shelter@example.com"></div>
    <div class="field">
      <label>施設写真</label>
      <div class="upload-box ${S.orgFacilityUploaded?'filled':''}" onclick="mockUploadFacility()">
        <span class="up-icon">${S.orgFacilityUploaded?'✅':'🏚️'}</span>${S.orgFacilityUploaded?'アップロード済み':'施設内観・外観の写真をアップロード'}
      </div>
    </div>
    <div class="field">
      <label>登録証明書類（動物取扱業登録証など）<span class="req">必須</span></label>
      <div class="upload-box ${S.orgLicenseUploaded?'filled':''}" onclick="mockUploadLicense()">
        <span class="up-icon">${S.orgLicenseUploaded?'✅':'📄'}</span>${S.orgLicenseUploaded?'アップロード済み':'書類をアップロード'}
      </div>
    </div>
    <button class="btn btn-org" onclick="orgStep2Next()">次へ（確認・審査申請）</button>
  </div>
</div>`;
function mockUploadFacility(){ S.orgFacilityUploaded=true; render(); }
function mockUploadLicense(){ S.orgLicenseUploaded=true; render(); }
function orgStep2Next(){
  const phone=document.getElementById('or-phone').value, email=document.getElementById('or-email').value;
  if(!phone||!email){ toast('電話番号とメールアドレスは必須です'); return; }
  if(!S.orgLicenseUploaded){ toast('登録証明書類のアップロードが必要です'); return; }
  Object.assign(S.orgReg, {zip:document.getElementById('or-zip').value, pref:document.getElementById('or-pref').value, address:document.getElementById('or-address').value, phone, email});
  nav('org-register-3');
}
SCREENS['org-register-3'] = () => `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;"><button class="back-btn" onclick="nav('org-register-2')">‹</button><h1>団体登録（3/3）</h1></div></div>
  <div class="container">
    <div class="steps"><div class="dot done"></div><div class="dot done"></div><div class="dot now"></div></div>
    <div class="section-title">登録内容の確認</div>
    <div class="card">
      <div class="stat-pill"><span>団体名</span><b>${S.orgReg.name}</b></div>
      <div class="stat-pill"><span>登録番号</span><b>${S.orgReg.license}</b></div>
      <div class="stat-pill"><span>代表者</span><b>${S.orgReg.rep}</b></div>
      <div class="stat-pill"><span>所在地</span><b>${S.orgReg.pref||''}${S.orgReg.address||''}</b></div>
      <div class="stat-pill"><span>連絡先</span><b>${S.orgReg.phone}</b></div>
    </div>
    <div class="check-row"><input type="checkbox" id="or-agree"><span><a onclick="nav('terms')">利用規約</a>に同意し、掲載する動物の情報に虚偽がないことを誓約します</span></div>
    <button class="btn btn-org" onclick="orgSubmit()">審査を申請する</button>
  </div>
</div>`;
function orgSubmit(){
  if(!document.getElementById('or-agree').checked){ toast('規約への同意が必要です'); return; }
  S.orgUser = Object.assign({id:'orgNEW', rating:0, petsCount:0, verified:false}, S.orgReg);
  SAMPLE_ORGS.push(S.orgUser);
  nav('org-register-done');
}
SCREENS['org-register-done'] = () => `
<div class="screen active no-nav" style="min-height:100vh;display:flex;flex-direction:column;align-items:center;justify-content:center;text-align:center;padding:24px;">
  <div style="font-size:52px;">📋</div>
  <div class="display mt12" style="font-size:19px;font-weight:900;">審査申請を受け付けました</div>
  <p class="section-sub">通常1〜3営業日以内に審査結果をご連絡します。承認後、保護犬・保護猫の掲載が可能になります。</p>
  <button class="btn btn-org mt16" onclick="nav('org-dashboard')">団体ダッシュボードを見る（デモ）</button>
</div>`;

SCREENS['org-dashboard'] = () => {
  const org = S.orgUser || SAMPLE_ORGS[0];
  const myPets = SAMPLE_PETS.filter(p=>p.orgId===org.id);
  return `
<div class="screen no-nav active">
  <div class="topbar"><div class="brand"><div class="mark">${HOUSE_MARK}</div><span>団体ダッシュボード</span></div>
    <button class="icon-btn" onclick="nav('login')">🚪</button></div>
  <div class="container">
    <div class="org-header">
      <div style="font-weight:900;font-size:16px;">${org.name}</div>
      <div style="font-size:12px;opacity:.85;">${org.verified?'✅ 承認済み団体':'⏳ 審査中'}</div>
      <div class="row2 mt16" style="gap:8px;">
        <div style="background:rgba(255,255,255,.35);border-radius:12px;padding:10px;"><div style="font-size:11px;">掲載頭数</div><div style="font-weight:800;font-size:18px;">${myPets.length}</div></div>
        <div style="background:rgba(255,255,255,.35);border-radius:12px;padding:10px;"><div style="font-size:11px;">申込み件数</div><div style="font-weight:800;font-size:18px;">${S.applications.filter(a=>a.orgId===org.id).length}</div></div>
      </div>
    </div>
    <button class="btn btn-org" onclick="nav('org-pet-new')">＋ 新しい里親募集を掲載する</button>
    <div class="section-title mt16" style="font-size:15px;">掲載中のペット</div>
    ${myPets.map(p=>`
      <div class="pet-card">
        <div class="pet-thumb" style="background:${thumbColor(p)}">${p.emoji}</div>
        <div class="pet-info">
          <div class="pname">${p.name}<span class="faint" style="font-weight:400;"> ・ ${p.breed}</span></div>
          <div class="pmeta">${p.sex} / ${p.age}</div>
          <div class="tag-row"><span class="house-tag ${p.urgent?'urgent':''}">${p.urgent?'急募':'募集中'}</span>${p.applied?'<span class="small-tag">応募あり</span>':''}</div>
        </div>
      </div>`).join('')}
    <div class="divider"></div>
    <div class="list-row" onclick="alert('デモ：応募者管理画面')"><div class="left"><span>📮</span><div>応募者・面談管理</div></div><span class="arrow">›</span></div>
    <div class="list-row" onclick="alert('デモ：入金管理画面')"><div class="left"><span>💰</span><div>手数料・入金管理</div></div><span class="arrow">›</span></div>
    <div class="list-row" onclick="nav('privacy-policy')"><div class="left"><span>📄</span><div>プライバシーポリシー</div></div><span class="arrow">›</span></div>
    <div class="list-row" onclick="nav('terms')"><div class="left"><span>📜</span><div>利用規約</div></div><span class="arrow">›</span></div>
  </div>
</div>`;
};

/* Org: new pet listing */
SCREENS['org-pet-new'] = () => `
<div class="screen active no-nav">
  <div class="topbar"><div class="header-fixed" style="width:100%;"><button class="back-btn" onclick="nav('org-dashboard')">‹</button><h1>新規里親募集の掲載</h1></div></div>
  <div class="container">
    <div class="field"><label>種類<span class="req">必須</span></label>
      <div class="chip-group">${['dog','cat'].map(sp=>`<div class="chip ${S.orgDraftPet.species===sp?'active':''}" onclick="orgPetSet('species','${sp}')">${speciesLabel(sp)}</div>`).join('')}</div>
    </div>
    <div class="field"><label>名前<span class="req">必須</span></label><input type="text" id="op-name" value="${S.orgDraftPet.name||''}"></div>
    <div class="field"><label>犬種・猫種</label><input type="text" id="op-breed" placeholder="例）柴犬ミックス" value="${S.orgDraftPet.breed||''}"></div>
    <div class="row2">
      <div class="field"><label>性別</label><select id="op-sex"><option ${S.orgDraftPet.sex==='オス'?'selected':''}>オス</option><option ${S.orgDraftPet.sex==='メス'?'selected':''}>メス</option></select></div>
      <div class="field"><label>年齢</label><input type="text" id="op-age" placeholder="例）2歳" value="${S.orgDraftPet.age||''}"></div>
    </div>
    <div class="field"><label>ボディの大きさ</label><div class="chip-group">${BODY_TYPES.slice(0,5).map(s=>`<div class="chip ${S.orgDraftPet.size===s?'active':''}" onclick="orgPetSet('size','${s}')">${s}</div>`).join('')}</div></div>
    <div class="field"><label>体型</label><div class="chip-group">${['スリム','がっしり','ぽっちゃり'].map(s=>`<div class="chip ${S.orgDraftPet.bodyType===s?'active':''}" onclick="orgPetSet('bodyType','${s}')">${s}</div>`).join('')}</div></div>
    <div class="field"><label>顔のタイプ</label><div class="chip-group">${FACE_TYPES.map(s=>`<div class="chip ${S.orgDraftPet.faceType===s?'active':''}" onclick="orgPetSet('faceType','${s}')">${s}</div>`).join('')}</div></div>
    <div class="field"><label>毛色</label><div class="chip-group">${COAT_COLORS.map(s=>`<div class="chip ${S.orgDraftPet.coatColor===s?'active':''}" onclick="orgPetSet('coatColor','${s}')">${s}</div>`).join('')}</div></div>
    <div class="field"><label>毛の長さ</label><div class="chip-group">${COAT_LENGTHS.map(s=>`<div class="chip ${S.orgDraftPet.coatLength===s?'active':''}" onclick="orgPetSet('coatLength','${s}')">${s}</div>`).join('')}</div></div>
    <div class="field"><label>受け渡し方法</label><div class="chip-group">
      <div class="chip ${S.orgDraftPet.pickup==='both'?'active':''}" onclick="orgPetSet('pickup','both')">両方可</div>
      <div class="chip ${S.orgDraftPet.pickup==='pickup'?'active':''}" onclick="orgPetSet('pickup','pickup')">お迎えのみ</div>
      <div class="chip ${S.orgDraftPet.pickup==='delivery'?'active':''}" onclick="orgPetSet('pickup','delivery')">お届け可</div>
    </div></div>
    <div class="field"><label>プロフィール・性格</label><textarea id="op-desc" placeholder="性格や既往歴、しつけの状況など">${S.orgDraftPet.desc||''}</textarea></div>
    <div class="field">
      <label>写真・動画</label>
      <div class="upload-box ${S.orgDraftPet.video?'filled':''}" onclick="orgPetSet('video',true)">
        <span class="up-icon">${S.orgDraftPet.video?'✅':'🎥'}</span>${S.orgDraftPet.video?'動画アップロード済み':'数秒の動画をアップロード（自動で3Dモデル化）'}
      </div>
    </div>
    <div class="field"><label>緊急度</label><div class="chip-group">
      <div class="chip ${!S.orgDraftPet.urgent?'active':''}" onclick="orgPetSet('urgent',false)">通常募集</div>
      <div class="chip ${S.orgDraftPet.urgent?'active':''}" onclick="orgPetSet('urgent',true)">急募</div>
    </div></div>
    <button class="btn btn-org mt8" onclick="orgPetSubmit()">掲載する</button>
  </div>
</div>`;
function orgPetSet(k,v){ S.orgDraftPet[k] = v; render(); }
function orgPetSubmit(){
  const name=document.getElementById('op-name').value.trim();
  if(!S.orgDraftPet.species || !name){ toast('種類と名前は必須です'); return; }
  const org = S.orgUser || SAMPLE_ORGS[0];
  const p = makePet(Object.assign({
    breed:document.getElementById('op-breed').value||'雑種', sex:document.getElementById('op-sex').value, age:document.getElementById('op-age').value||'不明',
    area:(org.pref||org.area||'')+'', orgId:org.id, emoji:S.orgDraftPet.species==='dog'?'🐕':'🐈', video:!!S.orgDraftPet.video, scan3d:!!S.orgDraftPet.video, desc:document.getElementById('op-desc').value||'よろしくお願いします。',
  }, S.orgDraftPet, {name}));
  SAMPLE_PETS.unshift(p);
  toast('掲載しました！');
  S.orgDraftPet = {};
  nav('org-dashboard');
}

/* ============================= INIT ============================= */
render();
</script>
</body>
</html>



