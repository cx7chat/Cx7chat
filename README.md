<!DOCTYPE html>
<html lang="tg">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#07080d">
<title>Чоти Олиҷаноб</title>
<style>
:root{
  --bg:#07080d;
  --panel:#0d0f17;
  --panel-2:#121522;
  --line:rgba(255,255,255,.07);
  --text:#e8eaf3;
  --muted:#7d849b;
  --indigo:#6366f1;
  --indigo-2:#4f46e5;
  --cyan:#22d3ee;
  --green:#34d399;
  --red:#f43f5e;
  --bubble-in:#171b2a;
  --radius:18px;
}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{height:100%}
body{
  margin:0;background:var(--bg);color:var(--text);
  font-family:Inter,system-ui,-apple-system,"Segoe UI",Roboto,"Helvetica Neue",Arial,sans-serif;
  overflow:hidden;height:100dvh;
}
body::before{
  content:"";position:fixed;inset:0;pointer-events:none;z-index:0;
  background:
    radial-gradient(600px 400px at 10% -10%,rgba(99,102,241,.22),transparent 60%),
    radial-gradient(500px 400px at 100% 110%,rgba(34,211,238,.13),transparent 60%);
}
button{font:inherit;color:inherit;border:0;background:none;cursor:pointer}
input,textarea{font:inherit;color:inherit}
svg{display:block}
::-webkit-scrollbar{width:6px}
::-webkit-scrollbar-thumb{background:rgba(255,255,255,.1);border-radius:6px}

/* ---------- Auth Screen ---------- */
#authScreen{
  position:fixed;inset:0;z-index:9999;display:grid;place-items:center;background:var(--bg);
}
.auth-box{
  width:100%;max-width:400px;padding:30px;background:var(--panel);
  border:1px solid var(--line);border-radius:var(--radius);
  box-shadow:0 14px 44px rgba(0,0,0,.65);animation:rise .5s cubic-bezier(.2,.9,.3,1) both;
}
.auth-box h2{margin-top:0;text-align:center;margin-bottom:20px;color:var(--text);font-size:22px;}
.auth-box input{
  width:100%;padding:12px 14px;margin-bottom:12px;border-radius:13px;border:1px solid var(--line);
  background:rgba(255,255,255,.04);color:#fff;outline:none;font-size:15px;transition:border-color .2s;
}
.auth-box input:focus{border-color:rgba(99,102,241,.6)}
.auth-box button{
  width:100%;padding:12px;border-radius:13px;border:0;
  background:linear-gradient(135deg,var(--indigo),var(--indigo-2));
  color:#fff;font-weight:600;cursor:pointer;margin-top:6px;font-size:15px;
  box-shadow:0 8px 22px rgba(99,102,241,.45);transition:transform .15s;
}
.auth-box button:active{transform:scale(.98)}
.auth-box .switch{text-align:center;margin-top:16px;font-size:13.5px;color:var(--muted);cursor:pointer;}
.auth-box .switch span{color:var(--cyan);text-decoration:underline;}

/* ---------- Shared ---------- */
@keyframes rise{from{opacity:0;transform:translateY(26px) scale(.97)}to{opacity:1;transform:none}}
.app.appear{animation:appIn .9s cubic-bezier(.2,.9,.3,1) backwards}
@keyframes appIn{from{opacity:0;transform:scale(.97);filter:blur(10px)}}
@keyframes msgOut{to{opacity:0;transform:scale(.88)}}
@keyframes pop2{from{opacity:0;transform:scale(.92)}}

.msgs-wrap{flex:1;min-height:0;position:relative;display:flex}
.messages{min-width:0}
.bubble{-webkit-touch-callout:none}
.bubble img.pic{-webkit-user-drag:none;user-select:none}
.to-bottom{
  position:absolute;right:16px;bottom:14px;width:42px;height:42px;border-radius:50%;display:grid;place-items:center;
  background:rgba(22,26,42,.94);border:1px solid rgba(99,102,241,.45);box-shadow:0 8px 24px rgba(0,0,0,.5);color:var(--text);
  opacity:0;transform:translateY(10px) scale(.9);pointer-events:none;transition:opacity .25s,transform .25s;
}
.to-bottom.show{opacity:1;transform:none;pointer-events:auto}
.to-bottom .nb{
  position:absolute;top:-7px;right:-4px;min-width:20px;height:20px;padding:0 5px;border-radius:10px;font-size:11px;font-weight:700;
  background:linear-gradient(135deg,var(--indigo),var(--cyan));color:#fff;display:none;place-items:center;
}
.to-bottom .nb.on{display:grid}
.emoji-panel{
  display:none;grid-template-columns:repeat(8,1fr);gap:2px;max-height:176px;overflow-y:auto;margin-bottom:10px;padding:8px;
  border-radius:16px;background:rgba(255,255,255,.04);border:1px solid var(--line);
}
.emoji-panel.show{display:grid;animation:rise .25s both}
.emoji-panel button{font-size:24px;line-height:1;padding:7px 0;border-radius:10px;transition:background .15s,transform .15s}
.emoji-panel button:hover{background:rgba(255,255,255,.08)}
.emoji-panel button:active{transform:scale(.82)}
#msgMenu{
  position:fixed;z-index:110;min-width:176px;padding:6px;border-radius:14px;display:none;
  background:#161a2b;border:1px solid rgba(99,102,241,.35);box-shadow:0 14px 44px rgba(0,0,0,.65);
}
#msgMenu.show{display:block;animation:pop2 .15s both}
#msgMenu button{display:flex;align-items:center;gap:10px;width:100%;padding:11px 12px;border-radius:9px;font-size:14.5px;text-align:left}
#msgMenu button:hover{background:rgba(255,255,255,.07)}
#msgMenu button.danger{color:#fb7185}

/* ---------- Layout ---------- */
.app{
  position:relative;z-index:1;height:100dvh;max-width:1500px;margin:0 auto;
  display:grid;grid-template-columns:370px 1fr;
}
.sidebar{
  display:flex;flex-direction:column;min-height:0;background:rgba(13,15,23,.85);
  border-right:1px solid var(--line);backdrop-filter:blur(10px);
}
.me-bar{display:flex;align-items:center;gap:12px;padding:16px 16px 10px}
.me-bar .info{flex:1;min-width:0}
.me-bar .nm{font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.me-bar .st{font-size:12.5px;color:var(--green);display:flex;align-items:center;gap:6px}
.icon-btn{
  width:40px;height:40px;border-radius:12px;display:grid;place-items:center;color:var(--muted);
  transition:background .2s,color .2s,transform .15s;flex:none;
}
.icon-btn:hover{background:rgba(255,255,255,.06);color:var(--text)}
.icon-btn:active{transform:scale(.92)}
.search{margin:6px 16px 10px;position:relative}
.search svg{position:absolute;left:14px;top:50%;transform:translateY(-50%);color:var(--muted)}
.search input{
  width:100%;padding:11px 14px 11px 42px;border-radius:13px;border:1px solid var(--line);
  background:rgba(255,255,255,.04);outline:none;font-size:14.5px;transition:border-color .2s;
}
.search input:focus{border-color:rgba(99,102,241,.6)}
.list{flex:1;overflow-y:auto;padding:4px 10px 14px}
.chat-item{
  display:flex;align-items:center;gap:12px;width:100%;padding:11px 12px;border-radius:15px;text-align:left;
  transition:background .2s,transform .15s;position:relative;
}
.chat-item:hover{background:rgba(255,255,255,.04)}
.chat-item.active{background:linear-gradient(90deg,rgba(99,102,241,.22),rgba(99,102,241,.06));}
.chat-item.active::before{content:"";position:absolute;left:0;top:18%;bottom:18%;width:3px;border-radius:3px;background:linear-gradient(var(--indigo),var(--cyan))}
.chat-item:active{transform:scale(.985)}
.av{position:relative;flex:none}
.av img{width:50px;height:50px;border-radius:50%;object-fit:cover;display:block}
.av.sm img{width:42px;height:42px}
.dot{
  position:absolute;right:0;bottom:1px;width:13px;height:13px;border-radius:50%;
  background:#4b5169;border:2.5px solid var(--panel);
}
.dot.on{background:var(--green);box-shadow:0 0 8px rgba(52,211,153,.7)}
.ci-body{flex:1;min-width:0}
.ci-top{display:flex;justify-content:space-between;gap:8px;align-items:baseline}
.ci-name{font-weight:600;font-size:15px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.ci-time{font-size:11.5px;color:var(--muted);flex:none}
.ci-bot{display:flex;justify-content:space-between;align-items:center;gap:8px;margin-top:3px}
.ci-last{font-size:13.5px;color:var(--muted);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.ci-last.typing{color:var(--cyan)}
.badge{
  min-width:21px;height:21px;padding:0 6px;border-radius:11px;font-size:12px;font-weight:600;
  background:linear-gradient(135deg,var(--indigo),var(--cyan));color:#fff;display:grid;place-items:center;flex:none;
  animation:pop .35s cubic-bezier(.3,1.6,.5,1);
}
@keyframes pop{from{transform:scale(0)}to{transform:scale(1)}}
.empty-list{padding:30px 10px;text-align:center;color:var(--muted);font-size:14px}

/* ---------- Chat area ---------- */
.chat{display:flex;flex-direction:column;min-height:0;min-width:0;position:relative;background:rgba(7,8,13,.55)}
.chat-head{
  display:flex;align-items:center;gap:12px;padding:12px 16px;border-bottom:1px solid var(--line);
  background:rgba(13,15,23,.75);backdrop-filter:blur(14px);-webkit-backdrop-filter:blur(14px);
}
.back{display:none}
.ch-info{flex:1;min-width:0}
.ch-name{font-weight:600;font-size:16px}
.ch-status{font-size:12.5px;color:var(--muted);margin-top:1px;transition:color .2s}
.ch-status.on{color:var(--green)}
.ch-status.typing{color:var(--cyan)}
.messages{
  flex:1;overflow-y:auto;padding:20px 18px 10px;display:flex;flex-direction:column;gap:6px;
  scroll-behavior:smooth;
}
.placeholder{margin:auto;text-align:center;color:var(--muted);padding:20px}
.placeholder .big{
  width:90px;height:90px;margin:0 auto 16px;border-radius:28px;display:grid;place-items:center;
  background:linear-gradient(135deg,rgba(99,102,241,.25),rgba(34,211,238,.15));border:1px solid rgba(99,102,241,.3);
}
.day{align-self:center;margin:10px 0;padding:5px 14px;border-radius:20px;font-size:12px;color:var(--muted);background:rgba(255,255,255,.05)}
.row{display:flex;animation:msgIn .38s cubic-bezier(.2,.9,.3,1) both}
.row.me{justify-content:flex-end}
@keyframes msgIn{from{opacity:0;transform:translateY(12px) scale(.96)}to{opacity:1;transform:none}}
.bubble{
  max-width:min(76%,520px);padding:9px 13px 6px;border-radius:var(--radius);position:relative;
  word-wrap:break-word;overflow-wrap:anywhere;font-size:15.5px;line-height:1.42;
}
.row.me .bubble{
  background:linear-gradient(135deg,#6366f1,#4f46e5);color:#fff;border-bottom-right-radius:6px;
  box-shadow:0 6px 22px rgba(79,70,229,.3);
}
.row.them .bubble{background:var(--bubble-in);border:1px solid var(--line);border-bottom-left-radius:6px}
.txt{white-space:pre-wrap}
.meta{display:flex;justify-content:flex-end;align-items:center;gap:4px;margin-top:3px;font-size:11px;opacity:.65}
.row.me .meta{color:#dfe3ff;opacity:.8}
.tick{color:var(--cyan)}
.row.me .tick{color:#a5f3fc}
.bubble.media{padding:5px 5px 6px}
.bubble.media .cap{padding:6px 8px 0}
.bubble.media .meta{padding:0 8px}
.bubble img.pic{display:block;max-width:100%;max-height:340px;border-radius:13px;cursor:zoom-in;transition:filter .2s}
.bubble img.pic:hover{filter:brightness(1.08)}
.missing{padding:18px 22px;color:var(--muted);font-size:13px}
.voice{display:flex;align-items:center;gap:11px;min-width:210px;padding:3px 4px 0}
.play{
  width:38px;height:38px;border-radius:50%;flex:none;display:grid;place-items:center;
  background:rgba(255,255,255,.18);transition:transform .15s,background .2s;
}
.row.them .play{background:linear-gradient(135deg,var(--indigo),var(--cyan))}
.play:active{transform:scale(.9)}
.wave{flex:1;display:flex;align-items:center;gap:2px;height:30px}
.wave i{flex:1;min-width:2px;border-radius:2px;background:currentColor;opacity:.35;transition:opacity .15s}
.wave i.f{opacity:1}
.vdur{font-size:12px;opacity:.8;min-width:34px;text-align:right;font-variant-numeric:tabular-nums}

/* ---------- Composer ---------- */
.composer{padding:10px 14px calc(12px + env(safe-area-inset-bottom));background:rgba(13,15,23,.75);border-top:1px solid var(--line);backdrop-filter:blur(14px);-webkit-backdrop-filter:blur(14px)}
.preview{
  display:none;align-items:center;gap:12px;margin-bottom:10px;padding:8px;border-radius:14px;
  background:rgba(99,102,241,.1);border:1px solid rgba(99,102,241,.3);animation:rise .3s both;
}
.preview.show{display:flex}
.preview img{width:56px;height:56px;border-radius:10px;object-fit:cover}
.preview span{flex:1;font-size:13.5px;color:var(--muted)}
.comp-row{display:flex;align-items:flex-end;gap:8px}
.input-wrap{
  flex:1;display:flex;align-items:flex-end;border-radius:22px;background:rgba(255,255,255,.05);
  border:1px solid var(--line);transition:border-color .2s,box-shadow .2s;
}
.input-wrap:focus-within{border-color:rgba(99,102,241,.6);box-shadow:0 0 0 4px rgba(99,102,241,.12)}
.input-wrap textarea{
  flex:1;resize:none;border:0;outline:none;background:none;padding:12px 2px;
  min-height:46px;max-height:130px;line-height:1.4;font-size:15.5px;
}
.input-wrap textarea::placeholder{color:#5d647d}
.input-wrap .icon-btn{width:44px;height:44px;border-radius:50%}
.send-btn{
  width:48px;height:48px;border-radius:50%;flex:none;display:grid;place-items:center;color:#fff;
  background:linear-gradient(135deg,var(--indigo),var(--indigo-2));
  box-shadow:0 8px 22px rgba(99,102,241,.45);transition:transform .15s,box-shadow .2s;
}
.send-btn:hover{box-shadow:0 10px 28px rgba(99,102,241,.65)}
.send-btn:active{transform:scale(.9)}
.send-btn.is-send{background:linear-gradient(135deg,var(--cyan),var(--indigo))}

/* recording bar */
.rec-bar{display:none;align-items:center;gap:12px;animation:rise .25s both}
.composer.recording .comp-row,.composer.recording .preview{display:none}
.composer.recording .rec-bar{display:flex}
.rec-pill{
  flex:1;display:flex;align-items:center;gap:12px;padding:6px 16px;height:48px;border-radius:24px;
  background:rgba(244,63,94,.1);border:1px solid rgba(244,63,94,.35);min-width:0;
}
.rec-dot{width:11px;height:11px;border-radius:50%;background:var(--red);flex:none;animation:pulse 1.1s infinite}
@keyframes pulse{0%{box-shadow:0 0 0 0 rgba(244,63,94,.7)}100%{box-shadow:0 0 0 14px rgba(244,63,94,0)}}
.rec-time{font-variant-numeric:tabular-nums;font-weight:600;min-width:42px}
.rec-bars{flex:1;display:flex;align-items:center;gap:3px;height:32px;min-width:0}
.rec-bars i{flex:1;max-width:6px;height:4px;border-radius:3px;background:linear-gradient(var(--red),#fb7185);transition:height .08s}
.send-btn.rec-send{background:linear-gradient(135deg,var(--red),#e11d48);box-shadow:0 8px 24px rgba(244,63,94,.5);animation:ring 1.6s infinite}
@keyframes ring{50%{box-shadow:0 8px 24px rgba(244,63,94,.5),0 0 0 8px rgba(244,63,94,.12)}}

/* ---------- Typing dots / lightbox / toast ---------- */
.dots{display:inline-flex;gap:3px;margin-left:3px;vertical-align:middle}
.dots i{width:4px;height:4px;border-radius:50%;background:currentColor;animation:bounce 1.2s infinite}
.dots i:nth-child(2){animation-delay:.15s}.dots i:nth-child(3){animation-delay:.3s}
@keyframes bounce{0%,60%,100%{transform:translateY(0);opacity:.4}30%{transform:translateY(-4px);opacity:1}}
#lightbox{
  position:fixed;inset:0;z-index:90;display:none;align-items:center;justify-content:center;padding:20px;
  background:rgba(3,4,8,.92);backdrop-filter:blur(8px);cursor:zoom-out;
}
#lightbox.show{display:flex;animation:fade .25s}
#lightbox img{max-width:100%;max-height:100%;border-radius:14px;box-shadow:0 20px 80px rgba(0,0,0,.7)}
@keyframes fade{from{opacity:0}}
#toast{
  position:fixed;left:50%;bottom:90px;transform:translate(-50%,20px);z-index:120;padding:12px 20px;border-radius:14px;
  background:#1b1f31;border:1px solid rgba(99,102,241,.4);box-shadow:0 10px 40px rgba(0,0,0,.5);
  font-size:14px;opacity:0;pointer-events:none;transition:.3s;width:max-content;max-width:90%;text-align:center;
}
#toast.show{opacity:1;transform:translate(-50%,0)}

/* ---------- Mobile ---------- */
@media (max-width:820px){
  .app{display:block;position:relative;overflow:hidden}
  .sidebar{position:absolute;inset:0}
  .chat{position:absolute;inset:0;transform:translateX(100%);transition:transform .38s cubic-bezier(.2,.9,.3,1);background:var(--bg)}
  .app.chat-open .chat{transform:none}
  .back{display:grid}
  .bubble{max-width:86%}
  .messages{padding:16px 12px 8px}
}
@media (prefers-reduced-motion:reduce){*{animation-duration:.01ms!important;transition-duration:.01ms!important}}
</style>
</head>
<body>

<!-- Экрани Бақайдгирӣ ва Логин -->
<div id="authScreen">
  <div class="auth-box">
    <h2 id="authTitle">Воридшавӣ</h2>
    <input type="email" id="emailIn" placeholder="Эл. почта (Email)" autocomplete="email">
    <input type="password" id="passIn" placeholder="Парол (ҳадди ақал 6 аломат)" autocomplete="current-password">
    <button id="authActionBtn">Даромадан</button>
    <div class="switch" id="authSwitch">Ҳисоб надоред? <span>Регистратсия кунед</span></div>
  </div>
</div>

<div class="app" id="app" style="display:none">
  <!-- Sidebar -->
  <aside class="sidebar">
    <div class="me-bar">
      <div class="av sm"><img id="meAv" alt=""><span class="dot on"></span></div>
      <div class="info">
        <div class="nm" id="meName"></div>
        <div class="st">● онлайн</div>
      </div>
      <button class="icon-btn" id="renameBtn" title="Иваз кардани ном" aria-label="Иваз кардани ном">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 20h9"/><path d="M16.5 3.5a2.1 2.1 0 0 1 3 3L7 19l-4 1 1-4z"/></svg>
      </button>
      <button class="icon-btn" id="logoutBtn" title="Баромадан аз ҳисоб" aria-label="Баромадан">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M9 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h4"/><polyline points="16 17 21 12 16 7"/><line x1="21" y1="12" x2="9" y2="12"/></svg>
      </button>
    </div>
    <div class="search">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><circle cx="11" cy="11" r="7"/><path d="m21 21-4.3-4.3"/></svg>
      <input id="searchInput" type="search" placeholder="Ҷустуҷӯ…">
    </div>
    <div class="list" id="list"></div>
  </aside>

  <!-- Chat area -->
  <main class="chat">
    <div class="chat-head" id="chatHead" style="display:none">
      <button class="icon-btn back" id="backBtn" aria-label="Бозгашт">
        <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="m15 18-6-6 6-6"/></svg>
      </button>
      <div class="av sm"><img id="chAv" alt=""><span class="dot" id="chDot"></span></div>
      <div class="ch-info">
        <div class="ch-name" id="chName"></div>
        <div class="ch-status" id="chStatus"></div>
      </div>
      <button class="icon-btn" id="clearBtn" title="Тоза кардани суҳбат" aria-label="Тоза кардани суҳбат">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M3 6h18M8 6V4a1 1 0 0 1 1-1h6a1 1 0 0 1 1 1v2m2 0v14a2 2 0 0 1-2 2H8a2 2 0 0 1-2-2V6"/></svg>
      </button>
    </div>

    <div class="msgs-wrap">
    <div class="messages" id="messages">
      <div class="placeholder">
        <div class="big">
          <svg width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="#a5b4fc" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M21 11.5a8.4 8.4 0 0 1-9 8.4 8.6 8.6 0 0 1-3.7-.8L3 21l1.9-5.3A8.4 8.4 0 1 1 21 11.5z"/></svg>
        </div>
        <div style="font-size:17px;color:var(--text);font-weight:600;margin-bottom:6px">Суҳбатро интихоб кунед</div>
        <div style="font-size:14px">Аз рӯйхати тарафи чап як нафарро пахш кунед.</div>
      </div>
    </div>
    <button class="to-bottom" id="toBottom" aria-label="Ба поён">
      <span class="nb" id="newBadge"></span>
      <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="m6 9 6 6 6-6"/></svg>
    </button>
    </div>

    <div class="composer" id="composer" style="display:none">
      <div class="emoji-panel" id="emojiPanel"></div>
      <div class="preview" id="preview">
        <img id="prevImg" alt="">
        <span>Акс омода аст. Тавсиф илова кунед ё фиристед.</span>
        <button class="icon-btn" id="prevClose" aria-label="Бекор кардан">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round"><path d="M18 6 6 18M6 6l12 12"/></svg>
        </button>
      </div>

      <div class="comp-row">
        <div class="input-wrap">
          <button class="icon-btn" id="emojiBtn" title="Эмоҷӣ" aria-label="Эмоҷӣ">
            <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.9" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="9.5"/><path d="M8 14.2a4.6 4.6 0 0 0 8 0"/><path d="M9 9.5h.01M15 9.5h.01" stroke-width="2.6"/></svg>
          </button>
          <textarea id="input" rows="1" placeholder="Паём нависед…" enterkeyhint="send" autocomplete="off"></textarea>
          <button class="icon-btn" id="attachBtn" title="Фиристодани акс" aria-label="Акс">
            <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.9" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="18" height="18" rx="3"/><circle cx="9" cy="9" r="1.8"/><path d="m21 15-5-5L5 21"/></svg>
          </button>
        </div>
        <button class="send-btn" id="mainBtn" aria-label="Фиристодан"></button>
      </div>

      <div class="rec-bar" id="recBar">
        <button class="icon-btn" id="recCancel" title="Бекор кардан" aria-label="Бекор кардан" style="color:var(--red)">
          <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M3 6h18M8 6V4a1 1 0 0 1 1-1h6a1 1 0 0 1 1 1v2m2 0v14a2 2 0 0 1-2 2H8a2 2 0 0 1-2-2V6"/></svg>
        </button>
        <div class="rec-pill">
          <span class="rec-dot"></span>
          <span class="rec-time" id="recTime">0:00</span>
          <div class="rec-bars" id="recBars"></div>
        </div>
        <button class="send-btn rec-send" id="recSend" aria-label="Фиристодани паёми овозӣ">
          <svg width="22" height="22" viewBox="0 0 24 24" fill="currentColor"><path d="M3.4 20.4 21 12 3.4 3.6 3.3 10l12.6 2-12.6 2z"/></svg>
        </button>
      </div>
      <input type="file" id="fileInput" accept="image/*" hidden>
    </div>
  </main>
</div>

<div id="lightbox"><img alt=""></div>
<div id="msgMenu"></div>
<div id="toast"></div>

<!-- Пайвасткунии Firebase ва Логикаи Чат -->
<script type="module">
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-app.js";
  import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, signOut, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-auth.js";

  const firebaseConfig = {
    apiKey: "AIzaSyDVEziZjjnuo64PF7gyMSt4GnJADS4JCao",
    authDomain: "cx7chat.firebaseapp.com",
    projectId: "cx7chat",
    storageBucket: "cx7chat.firebasestorage.app",
    messagingSenderId: "992192050521",
    appId: "1:992192050521:web:44e108d36144fe964d0848",
    measurementId: "G-09NGBR7HNJ"
  };

  const firebaseApp = initializeApp(firebaseConfig);
  const auth = getAuth(firebaseApp);

  const authScreen = document.getElementById('authScreen');
  const appScreen = document.getElementById('app');
  const emailIn = document.getElementById('emailIn');
  const passIn = document.getElementById('passIn');
  const authActionBtn = document.getElementById('authActionBtn');
  const authTitle = document.getElementById('authTitle');
  const authSwitch = document.getElementById('authSwitch');
  const logoutBtn = document.getElementById('logoutBtn');

  let isRegistering = false;

  authSwitch.addEventListener('click', () => {
    isRegistering = !isRegistering;
    authTitle.textContent = isRegistering ? 'Регистратсия' : 'Воридшавӣ';
    authActionBtn.textContent = isRegistering ? 'Сабти ном шудан' : 'Даромадан';
    authSwitch.innerHTML = isRegistering ? 'Ҳисоб доред? <span>Ворид шавед</span>' : 'Ҳисоб надоред? <span>Регистратсия кунед</span>';
  });

  authActionBtn.addEventListener('click', async () => {
    const email = emailIn.value.trim();
    const password = passIn.value.trim();

    if (!email || !password) {
      alert('Лутфан почта ва паролро пур кунед!');
      return;
    }

    try {
      if (isRegistering) {
        await createUserWithEmailAndPassword(auth, email, password);
        alert('Сабти ном бомуваффақият анҷом ёфт!');
      } else {
        await signInWithEmailAndPassword(auth, email, password);
      }
    } catch (error) {
      alert('Хатогӣ: ' + error.message);
    }
  });

  logoutBtn.addEventListener('click', async () => {
    if (confirm.call(window, 'Мехоҳед аз ҳисоб бароед?')) {
      await signOut(auth);
    }
  });

  onAuthStateChanged(auth, (user) => {
    if (user) {
      authScreen.style.display = 'none';
      appScreen.style.display = 'grid';
      // Нишон додани номи почта ба сифати номи корбар
      document.getElementById('meName').textContent = user.email.split('@')[0];
      document.getElementById('meAv').src = 'data:image/svg+xml;charset=utf-8,' + encodeURIComponent('<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><rect width="100" height="100" fill="#6366f1"/><text x="50" y="50" text-anchor="middle" dominant-baseline="central" font-size="46" fill="#fff">' + user.email.charAt(0).toUpperCase() + '</text></svg>');
    } else {
      authScreen.style.display = 'grid';
      appScreen.style.display = 'none';
    }
  });
</script>

<script>
(function () {
  'use strict';
  var $ = function (s) { return document.querySelector(s); };
  var KEY = 'choti_olijanob_v1';
  var ICON_MIC = '<svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="9" y="2" width="6" height="12" rx="3"/><path d="M5 11a7 7 0 0 0 14 0M12 18v4"/></svg>';
  var ICON_SEND = '<svg width="22" height="22" viewBox="0 0 24 24" fill="currentColor"><path d="M3.4 20.4 21 12 3.4 3.6 3.3 10l12.6 2-12.6 2z"/></svg>';
  var ICON_PLAY = '<svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M7 4.5v15a1 1 0 0 0 1.5.86l12-7.5a1 1 0 0 0 0-1.72l-12-7.5A1 1 0 0 0 7 4.5z"/></svg>';
  var ICON_PAUSE = '<svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><rect x="6" y="4" width="4.5" height="16" rx="1.2"/><rect x="13.5" y="4" width="4.5" height="16" rx="1.2"/></svg>';

  function pad(n) { return n < 10 ? '0' + n : '' + n; }
  function hhmm(ts) { var d = new Date(ts); return pad(d.getHours()) + ':' + pad(d.getMinutes()); }
  function fmtDur(s) { s = Math.max(0, Math.round(s)); return Math.floor(s / 60) + ':' + pad(s % 60); }
  function dayKey(ts) { var d = new Date(ts); return d.getFullYear() + '-' + d.getMonth() + '-' + d.getDate(); }
  function dayLabel(ts) {
    var now = Date.now();
    if (dayKey(ts) === dayKey(now)) return 'Имрӯз';
    if (dayKey(ts) === dayKey(now - 864e5)) return 'Дирӯз';
    var d = new Date(ts);
    return pad(d.getDate()) + '.' + pad(d.getMonth() + 1) + '.' + d.getFullYear();
  }
  function hash(str) { var h = 0; for (var i = 0; i < str.length; i++) h = (h * 31 + str.charCodeAt(i)) | 0; return Math.abs(h); }
  function avatar(name, hue) {
    var ch = (name.trim().charAt(0) || '?').toUpperCase();
    var svg = '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100">' +
      '<defs><linearGradient id="g" x1="0" y1="0" x2="1" y2="1">' +
      '<stop offset="0" stop-color="hsl(' + hue + ',75%,60%)"/><stop offset="1" stop-color="hsl(' + ((hue + 50) % 360) + ',80%,42%)"/>' +
      '</linearGradient></defs><rect width="100" height="100" fill="url(#g)"/>' +
      '<text x="50" y="50" text-anchor="middle" dominant-baseline="central" font-family="Arial,sans-serif" font-size="46" font-weight="700" fill="#fff">' + ch + '</text></svg>';
    return 'data:image/svg+xml;charset=utf-8,' + encodeURIComponent(svg);
  }
  var toastTimer;
  function toast(msg) {
    var t = $('#toast'); t.textContent = msg; t.classList.add('show');
    clearTimeout(toastTimer); toastTimer = setTimeout(function () { t.classList.remove('show'); }, 3200);
  }
  function rand(a, b) { return a + Math.random() * (b - a); }
  function pick(arr) { return arr[Math.floor(Math.random() * arr.length)]; }

  var CONTACTS = [
    { id: 'rustam', name: 'Рустам Ҷалолов', hue: 238, online: true,
      replies: ['Салом! Чӣ хел ҳастӣ?', 'Хеле хуб, ташаккур!', 'Ҳа, розӣ ҳастам 👍', 'Ин ғояи олӣ аст!', 'Баъдтар сӯҳбат мекунем, ҳозир каме банд ҳастам.', 'Ҳаҳа, ин хандаовар буд 😄'] },
    { id: 'nilufar', name: 'Нилуфар', hue: 320, online: true,
      replies: ['Ассалом! Рӯзат ба хайр 🌸', 'Чӣ хабар? Ҳама хуб аст?', 'Воқеан? Ин ҷолиб аст!', 'Ман ҳам ҳамин тавр фикр мекардам.', 'Ташаккури зиёд ✨'] },
    { id: 'firdavs', name: 'Фирдавс Назаров', hue: 190, online: true,
      replies: ['Ҳа, мешавад.', 'Биё, фардо вомехӯрем!', 'Лоиҳа тақрибан тайёр аст.', 'Ҳамааш дуруст пеш меравад 🚀', 'Ман инро санҷида мебинам.'] },
    { id: 'mehrgon', name: 'Меҳргон', hue: 155, online: false, seen: 'Дирӯз соати 22:14 буд', replies: [] },
    { id: 'team', name: 'Гурӯҳи дӯстон', hue: 265, online: true,
      replies: ['Салом ба ҳама! 🎉', 'Кӣ имшаб омода аст?', 'Ман розӣ ҳастам!', 'Пешниҳоди хуб, дастгирӣ мекунам.'] }
  ];
  CONTACTS.forEach(function (c) { c.avatar = avatar(c.name, c.hue); });
  function byId(id) { for (var i = 0; i < CONTACTS.length; i++) if (CONTACTS[i].id === id) return CONTACTS[i]; return null; }

  var state = { name: 'Ман', chats: {}, unread: {} };
  var activeId = null;
  var typing = {};
  var pendingImage = null;

  var STORE = KEY + ':main';
  function load() {
    try {
      var s = JSON.parse(localStorage.getItem(STORE));
      if (s && typeof s === 'object') {
        state.chats = s.chats || {};
        state.unread = s.unread || {};
      }
    } catch (e) {}
  }
  function save() {
    try { localStorage.setItem(STORE, JSON.stringify({ chats: state.chats, unread: state.unread })); return; } catch (e) {}
    try {
      var lite = { unread: state.unread, chats: {} };
      Object.keys(state.chats).forEach(function (k) {
        lite.chats[k] = state.chats[k].map(function (m) {
          if (m.type === 'text') return m;
          var c = {}; for (var p in m) c[p] = m[p]; c.src = null; return c;
        });
      });
      localStorage.setItem(STORE, JSON.stringify(lite));
    } catch (e2) {}
  }
  function msgs(id) { return state.chats[id] || (state.chats[id] = []); }
  function lastMsg(id) { var a = state.chats[id]; return a && a.length ? a[a.length - 1] : null; }
  function uid() { return Date.now().toString(36) + Math.random().toString(36).slice(2, 7); }

  function seed() {
    var has = false;
    CONTACTS.forEach(function (c) { if (state.chats[c.id] && state.chats[c.id].length) has = true; });
    if (has) return;
    var now = Date.now();
    function add(id, text, ago, unread) {
      msgs(id).push({ id: uid(), from: 'them', type: 'text', text: text, ts: now - ago });
      if (unread) state.unread[id] = (state.unread[id] || 0) + 1;
    }
    add('rustam', 'Салом! Хуш омадӣ ба Чоти Олиҷаноб 👋', 4 * 60e3, true);
    add('rustam', 'Биё як чизе нависем!', 3 * 60e3, true);
    add('nilufar', 'Ассалом! Рӯзат ба хайр 🌸', 52 * 60e3, true);
    add('firdavs', 'Лоиҳаро дидӣ? Хеле зебо шудааст.', 3 * 36e5, false);
    add('mehrgon', 'Фардо бо ҳам сӯҳбат мекунем.', 26 * 36e5, false);
    add('team', 'Имшаб кӣ меояд?', 40 * 60e3, true);
    save();
  }

  function startApp() {
    seed();
    save();
    var first = CONTACTS.slice().sort(function (a, b) {
      var la = lastMsg(a.id), lb = lastMsg(b.id);
      return (lb ? lb.ts : 0) - (la ? la.ts : 0);
    })[0];
    renderList();
    if (first) openChat(first.id);
    $('#app').classList.add('appear');
  }

  var listEl = $('#list'), searchEl = $('#searchInput');
  searchEl.addEventListener('input', renderList);

  function previewText(m) {
    if (!m) return 'Паём нест';
    var p = m.from === 'me' ? 'Шумо: ' : '';
    if (m.type === 'image') return p + '📷 Акс' + (m.text ? ' · ' + m.text : '');
    if (m.type === 'voice') return p + '🎤 Паёми овозӣ';
    return p + m.text;
  }
  function renderList() {
    var q = searchEl.value.trim().toLowerCase();
    var items = CONTACTS.filter(function (c) { return !q || c.name.toLowerCase().indexOf(q) !== -1; });
    items.sort(function (a, b) {
      var la = lastMsg(a.id), lb = lastMsg(b.id);
      return (lb ? lb.ts : 0) - (la ? la.ts : 0);
    });
    listEl.innerHTML = '';
    if (!items.length) {
      var e = document.createElement('div'); e.className = 'empty-list'; e.textContent = 'Ҳеҷ чиз ёфт нашуд'; listEl.appendChild(e); return;
    }
    items.forEach(function (c) {
      var m = lastMsg(c.id), un = state.unread[c.id] || 0;
      var b = document.createElement('button');
      b.className = 'chat-item' + (c.id === activeId ? ' active' : '');
      b.innerHTML =
        '<div class="av"><img alt=""><span class="dot' + (c.online ? ' on' : '') + '"></span></div>' +
        '<div class="ci-body"><div class="ci-top"><span class="ci-name"></span><span class="ci-time"></span></div>' +
        '<div class="ci-bot"><span class="ci-last"></span></div></div>';
      b.querySelector('img').src = c.avatar;
      b.querySelector('.ci-name').textContent = c.name;
      b.querySelector('.ci-time').textContent = m ? hhmm(m.ts) : '';
      var last = b.querySelector('.ci-last');
      if (typing[c.id]) { last.className = 'ci-last typing'; last.innerHTML = 'менависад<span class="dots"><i></i><i></i><i></i></span>'; }
      else last.textContent = previewText(m);
      if (un > 0) {
        var bd = document.createElement('span'); bd.className = 'badge'; bd.textContent = un > 99 ? '99+' : un;
        b.querySelector('.ci-bot').appendChild(bd);
      }
      b.addEventListener('click', function () { openChat(c.id); });
      listEl.appendChild(b);
    });
  }

  var messagesEl = $('#messages'), chatHead = $('#chatHead'), composer = $('#composer');
  var inputEl = $('#input'), mainBtn = $('#mainBtn');

  function openChat(id) {
    if (activeId !== id) { stopAudio(); clearPending(); inputEl.value = ''; autoGrow(); updateMainBtn(); emojiPanel.classList.remove('show'); closeMenu(); }
    activeId = id;
    state.unread[id] = 0; save();
    var c = byId(id);
    chatHead.style.display = 'flex';
    composer.style.display = 'block';
    autoGrow();
    $('#chAv').src = c.avatar;
    $('#chName').textContent = c.name;
    $('#chDot').className = 'dot' + (c.online ? ' on' : '');
    updateStatus();
    $('#app').classList.add('chat-open');
    renderMessages();
    renderList();
    if (window.innerWidth > 820) inputEl.focus();
  }
  $('#backBtn').addEventListener('click', function () {
    $('#app').classList.remove('chat-open');
    activeId = null;
    stopAudio();
    renderList();
  });

  function updateStatus() {
    if (!activeId) return;
    var c = byId(activeId), s = $('#chStatus');
    if (typing[activeId]) { s.className = 'ch-status typing'; s.innerHTML = 'менависад<span class="dots"><i></i><i></i><i></i></span>'; }
    else if (c.online) { s.className = 'ch-status on'; s.textContent = 'онлайн'; }
    else { s.className = 'ch-status'; s.textContent = c.seen || 'оффлайн'; }
  }

  function renderMessages() {
    messagesEl.innerHTML = '';
    var arr = msgs(activeId), prev = null;
    if (!arr.length) {
      var p = document.createElement('div'); p.className = 'placeholder';
      p.innerHTML = '<div style="font-size:15px">Ҳоло паём нест. Аввалин шуда нависед 👋</div>';
      messagesEl.appendChild(p);
    }
    arr.forEach(function (m) {
      if (!prev || dayKey(prev.ts) !== dayKey(m.ts)) addDay(m.ts);
      messagesEl.appendChild(buildMsg(m, false));
      prev = m;
    });
    scrollDown(true);
    newCount = 0; updateToBottom();
  }
  function addDay(ts) {
    var d = document.createElement('div'); d.className = 'day'; d.textContent = dayLabel(ts); messagesEl.appendChild(d);
  }
  function scrollDown(instant) {
    if (instant) { var sb = messagesEl.style.scrollBehavior; messagesEl.style.scrollBehavior = 'auto'; messagesEl.scrollTop = messagesEl.scrollHeight; messagesEl.style.scrollBehavior = sb; }
    else messagesEl.scrollTop = messagesEl.scrollHeight;
  }

  function bars(id, n) {
    var h = hash(id), out = [];
    for (var i = 0; i < n; i++) { h = (h * 1103515245 + 12345) & 0x7fffffff; out.push(18 + (h % 82)); }
    return out;
  }

  function buildMsg(m, animate) {
    var row = document.createElement('div');
    row.className = 'row ' + (m.from === 'me' ? 'me' : 'them');
    row.dataset.id = m.id;
    if (animate === false) row.style.animation = 'none';
    var b = document.createElement('div');
    b.className = 'bubble' + (m.type === 'image' ? ' media' : '');
    var isMe = m.from === 'me';
    var contact = activeId ? byId(activeId) : null;
    var tick = isMe ? '<span class="tick">' + ((contact && contact.online) ? '✓✓' : '✓') + '</span>' : '';

    if (m.type === 'text') {
      var t = document.createElement('div'); t.className = 'txt'; t.textContent = m.text; b.appendChild(t);
    } else if (m.type === 'image') {
      if (m.src) {
        var img = document.createElement('img'); img.className = 'pic'; img.src = m.src; img.alt = 'Акс';
        img.addEventListener('click', function () { openLightbox(m.src); });
        b.appendChild(img);
      } else {
        var ms = document.createElement('div'); ms.className = 'missing'; ms.textContent = '🖼 Акс (дар хотира нест)'; b.appendChild(ms);
      }
      if (m.text) { var cp = document.createElement('div'); cp.className = 'cap txt'; cp.textContent = m.text; b.appendChild(cp); }
    } else if (m.type === 'voice') {
      b.appendChild(buildVoice(m));
    }
    var meta = document.createElement('div'); meta.className = 'meta';
    meta.innerHTML = '<span>' + hhmm(m.ts) + '</span>' + tick;
    b.appendChild(meta);
    row.appendChild(b);
    return row;
  }

  var curAudio = null, curReset = null;
  function stopAudio() {
    if (curAudio) { try { curAudio.pause(); } catch (e) {} }
    if (curReset) curReset();
    curAudio = null; curReset = null;
  }
  function buildVoice(m) {
    var wrap = document.createElement('div'); wrap.className = 'voice';
    var btn = document.createElement('button'); btn.className = 'play'; btn.innerHTML = ICON_PLAY; btn.setAttribute('aria-label', 'Пахш');
    var wave = document.createElement('div'); wave.className = 'wave';
    var hs = bars(m.id, 28), bs = [];
    hs.forEach(function (h) { var i = document.createElement('i'); i.style.height = h + '%'; wave.appendChild(i); bs.push(i); });
    var dur = document.createElement('span'); dur.className = 'vdur'; dur.textContent = fmtDur(m.dur || 0);
    wrap.appendChild(btn); wrap.appendChild(wave); wrap.appendChild(dur);
    if (!m.src) { btn.disabled = true; btn.style.opacity = '.4'; return wrap; }

    var audio = null;
    function reset() {
      btn.innerHTML = ICON_PLAY; bs.forEach(function (i) { i.classList.remove('f'); }); dur.textContent = fmtDur(m.dur || 0);
    }
    function progress() {
      var total = m.dur || audio.duration || 1;
      var p = Math.min(1, audio.currentTime / total);
      var n = Math.round(p * bs.length);
      bs.forEach(function (i, k) { i.classList.toggle('f', k < n); });
      dur.textContent = fmtDur(audio.currentTime);
    }
    btn.addEventListener('click', function () {
      if (audio && curAudio === audio && !audio.paused) { audio.pause(); btn.innerHTML = ICON_PLAY; return; }
      if (curAudio !== audio) stopAudio();
      if (!audio) {
        audio = new Audio(m.src);
        audio.addEventListener('timeupdate', progress);
        audio.addEventListener('ended', function () { reset(); if (curAudio === audio) { curAudio = null; curReset = null; } });
        audio.addEventListener('error', function () { reset(); toast('Паёми овозӣ пахш нашуд'); });
      }
      curAudio = audio; curReset = reset;
      var pr = audio.play(); if (pr && pr.catch) pr.catch(function () { reset(); });
      btn.innerHTML = ICON_PAUSE;
    });
    wave.addEventListener('click', function (e) {
      if (!audio) return;
      var r = wave.getBoundingClientRect(), p = (e.clientX - r.left) / r.width;
      var total = m.dur || audio.duration; if (isFinite(total)) { audio.currentTime = p * total; progress(); }
    });
    return wrap;
  }

  function pushMsg(chatId, msg) {
    msgs(chatId).push(msg);
    if (msg.from === 'them' && chatId !== activeId) state.unread[chatId] = (state.unread[chatId] || 0) + 1;
    save();
    if (chatId === activeId) {
      var stick = msg.from === 'me' || nearBottom();
      var ph = messagesEl.querySelector('.placeholder'); if (ph) ph.remove();
      var arr = msgs(chatId), prev = arr.length > 1 ? arr[arr.length - 2] : null;
      if (!prev || dayKey(prev.ts) !== dayKey(msg.ts)) addDay(msg.ts);
      messagesEl.appendChild(buildMsg(msg, true));
      if (stick) scrollDown(false); else newCount++;
      updateToBottom();
    }
    renderList();
  }

  function sendCurrent() {
    if (!activeId) return;
    emojiPanel.classList.remove('show');
    var text = inputEl.value.trim();
    if (pendingImage) {
      pushMsg(activeId, { id: uid(), from: 'me', type: 'image', src: pendingImage, text: text, ts: Date.now() });
      clearPending(); inputEl.value = ''; autoGrow(); updateMainBtn();
      scheduleReply(activeId, 'image');
    } else if (text) {
      pushMsg(activeId, { id: uid(), from: 'me', type: 'text', text: text, ts: Date.now() });
      inputEl.value = ''; autoGrow(); updateMainBtn();
      scheduleReply(activeId, 'text');
    }
    if (window.innerWidth > 820) inputEl.focus();
  }

  inputEl.addEventListener('keydown', function (e) {
    if (e.key === 'Enter' && !e.shiftKey && !e.isComposing) { e.preventDefault(); sendCurrent(); }
  });
  inputEl.addEventListener('input', function () { autoGrow(); updateMainBtn(); });
  function autoGrow() { inputEl.style.height = 'auto'; inputEl.style.height = Math.min(inputEl.scrollHeight, 130) + 'px'; }
  function updateMainBtn() {
    var has = inputEl.value.trim().length > 0 || !!pendingImage;
    mainBtn.innerHTML = has ? ICON_SEND : ICON_MIC;
    mainBtn.classList.toggle('is-send', has);
    mainBtn.setAttribute('aria-label', has ? 'Фиристодан' : 'Сабти паёми овозӣ');
  }
  mainBtn.addEventListener('click', function () {
    if (inputEl.value.trim() || pendingImage) sendCurrent(); else startRec();
  });

  function scheduleReply(id, kind) {
    var c = byId(id);
    if (!c || !c.online || !c.replies.length) return;
    setTimeout(function () {
      typing[id] = true; updateStatus(); renderList();
      setTimeout(function () {
        typing[id] = false;
        var text;
        if (kind === 'image') text = pick(['Акси хеле зебо! 😍', 'Вой, чӣ аксе! 📷', 'Ташаккур барои акс!']);
        else if (kind === 'voice') text = pick(['Паёми овозиро шунидам 🎧', 'Овози зебо доред! 😊', 'Фаҳмидам, ташаккур!']);
        else text = pick(c.replies);
        pushMsg(id, { id: uid(), from: 'them', type: 'text', text: text, ts: Date.now() });
        updateStatus();
      }, rand(1100, 2300));
    }, rand(500, 1100));
  }

  var fileInput = $('#fileInput');
  $('#attachBtn').addEventListener('click', function () { fileInput.click(); });
  fileInput.addEventListener('change', function () {
    var f = fileInput.files && fileInput.files[0];
    fileInput.value = '';
    if (!f) return;
    if (!/^image\//.test(f.type)) { toast('Лутфан танҳо файли расм интихоб кунед'); return; }
    var fr = new FileReader();
    fr.onerror = function () { toast('Акс хонда нашуд'); };
    fr.onload = function () {
      var im = new Image();
      im.onerror = function () { toast('Ин формати акс дастгирӣ намешавад'); };
      im.onload = function () {
        var max = 960, w = im.naturalWidth, h = im.naturalHeight, k = Math.min(1, max / Math.max(w, h));
        var cv = document.createElement('canvas'); cv.width = Math.round(w * k); cv.height = Math.round(h * k);
        var cx = cv.getContext('2d'); cx.drawImage(im, 0, 0, cv.width, cv.height);
        pendingImage = cv.toDataURL('image/jpeg', 0.78);
        $('#prevImg').src = pendingImage;
        $('#preview').classList.add('show');
        updateMainBtn();
        inputEl.focus();
      };
      im.src = fr.result;
    };
    fr.readAsDataURL(f);
  });
  function clearPending() { pendingImage = null; $('#preview').classList.remove('show'); updateMainBtn(); }
  $('#prevClose').addEventListener('click', clearPending);

  var lb = $('#lightbox');
  function openLightbox(src) { lb.querySelector('img').src = src; lb.classList.add('show'); }
  lb.addEventListener('click', function () { lb.classList.remove('show'); });
  document.addEventListener('keydown', function (e) { if (e.key === 'Escape') lb.classList.remove('show'); });

  var recording = false, mr = null, stream = null, chunks = [], cancelled = false;
  var recStart = 0, recTimer = null, actx = null, analyser = null, raf = null, mimeUsed = '';
  var recBars = $('#recBars'), recBarEls = [];
  for (var bi = 0; bi < 26; bi++) { var el = document.createElement('i'); recBars.appendChild(el); recBarEls.push(el); }

  function startRec() {
    if (!activeId || recording) return;
    if (!navigator.mediaDevices || !navigator.mediaDevices.getUserMedia || !window.MediaRecorder) {
      toast('Браузери шумо сабти овозро дастгирӣ намекунад'); return;
    }
    stopAudio();
    navigator.mediaDevices.getUserMedia({ audio: true }).then(function (s) {
      stream = s; chunks = []; cancelled = false;
      var types = ['audio/webm;codecs=opus', 'audio/webm', 'audio/mp4', 'audio/ogg;codecs=opus'];
      mimeUsed = '';
      for (var i = 0; i < types.length; i++) {
        if (window.MediaRecorder.isTypeSupported && MediaRecorder.isTypeSupported(types[i])) { mimeUsed = types[i]; break; }
      }
      try { mr = mimeUsed ? new MediaRecorder(stream, { mimeType: mimeUsed }) : new MediaRecorder(stream); }
      catch (e) { toast('Сабти овоз оғоз нашуд'); releaseStream(); return; }
      mr.ondataavailable = function (ev) { if (ev.data && ev.data.size) chunks.push(ev.data); };
      mr.onstop = onRecStop;
      mr.start();
      recording = true; recStart = Date.now();
      composer.classList.add('recording');
      $('#recTime').textContent = '0:00';
      recTimer = setInterval(function () { $('#recTime').textContent = fmtDur((Date.now() - recStart) / 1000); }, 250);
      startViz();
    }).catch(function () {
      toast('Барои сабт ба микрофон иҷозат диҳед');
    });
  }
  function startViz() {
    try {
      var AC = window.AudioContext || window.webkitAudioContext;
      actx = new AC();
      var src = actx.createMediaStreamSource(stream);
      analyser = actx.createAnalyser(); analyser.fftSize = 128; analyser.smoothingTimeConstant = 0.7;
      src.connect(analyser);
      var data = new Uint8Array(analyser.frequencyBinCount);
      (function loop() {
        if (!recording) return;
        analyser.getByteFrequencyData(data);
        for (var i = 0; i < recBarEls.length; i++) {
          var v = data[Math.min(data.length - 1, Math.floor(i * 1.3) + 1)] / 255;
          recBarEls[i].style.height = Math.max(4, Math.round(v * 30)) + 'px';
        }
        raf = requestAnimationFrame(loop);
      })();
    } catch (e) {
      var t = 0;
      (function fake() { if (!recording) return; t += 0.25;
        recBarEls.forEach(function (el, i) { el.style.height = (6 + Math.abs(Math.sin(t + i * .5)) * 18) + 'px'; });
        raf = requestAnimationFrame(fake); })();
    }
  }
  function releaseStream() {
    if (raf) cancelAnimationFrame(raf); raf = null;
    if (stream) { stream.getTracks().forEach(function (t) { t.stop(); }); stream = null; }
    if (actx) { try { actx.close(); } catch (e) {} actx = null; }
    clearInterval(recTimer);
    composer.classList.remove('recording');
    recBarEls.forEach(function (el) { el.style.height = '4px'; });
    recording = false;
  }
  function stopRec(send) {
    if (!recording || !mr) return;
    cancelled = !send;
    var d = (Date.now() - recStart) / 1000;
    recDuration = d;
    recording = false;
    try { mr.stop(); } catch (e) { releaseStream(); }
  }
  var recDuration = 0;
  function onRecStop() {
    var chatId = activeId, dur = recDuration, type = mimeUsed || (chunks[0] && chunks[0].type) || 'audio/webm';
    releaseStream();
    if (cancelled) { chunks = []; return; }
    if (dur < 0.8) { toast('Паём хеле кӯтоҳ аст'); chunks = []; return; }
    var blob = new Blob(chunks, { type: type }); chunks = [];
    var fr = new FileReader();
    fr.onload = function () {
      if (!chatId) return;
      pushMsg(chatId, { id: uid(), from: 'me', type: 'voice', src: fr.result, dur: dur, ts: Date.now() });
      scheduleReply(chatId, 'voice');
    };
    fr.readAsDataURL(blob);
  }
  function cancelRec() { stopRec(false); }
  $('#recCancel').addEventListener('click', cancelRec);
  $('#recSend').addEventListener('click', function () { stopRec(true); });

  var EMOJIS = '😀 😃 😄 😁 😆 😅 😂 🤣 😊 😇 🙂 😉 😍 🥰 😘 😋 😎 🤩 🥳 🤗 🤔 😐 😴 😢 😭 😡 🤯 😱 🙏 👍 👎 👏 🙌 💪 🤝 ✌️ 👋 ❤️ 💙 💜 🔥 ✨ 🎉 🎁 🌹 🌸 ☀️ 🌙 ⭐ 🚀 💯 ✅ ❌ 🍕 ☕ 🎵'.split(' ');
  var emojiPanel = $('#emojiPanel');
  function insertAtCursor(t) {
    var a = inputEl.selectionStart, b = inputEl.selectionEnd;
    if (typeof a !== 'number') { a = b = inputEl.value.length; }
    inputEl.value = inputEl.value.slice(0, a) + t + inputEl.value.slice(b);
    var pos = a + t.length;
    if (window.innerWidth > 820) inputEl.focus();
    try { inputEl.setSelectionRange(pos, pos); } catch (e) {}
    autoGrow(); updateMainBtn();
  }
  EMOJIS.forEach(function (e) {
    var b = document.createElement('button'); b.type = 'button'; b.textContent = e;
    b.addEventListener('click', function () { insertAtCursor(e); });
    emojiPanel.appendChild(b);
  });
  $('#emojiBtn').addEventListener('click', function () { emojiPanel.classList.toggle('show'); });

  var toBottom = $('#toBottom'), newBadge = $('#newBadge'), newCount = 0;
  function nearBottom() { return messagesEl.scrollHeight - messagesEl.scrollTop - messagesEl.clientHeight < 160; }
  function updateToBottom() {
    var show = !nearBottom();
    if (!show) newCount = 0;
    toBottom.classList.toggle('show', show);
    newBadge.textContent = newCount > 99 ? '99+' : newCount;
    newBadge.classList.toggle('on', show && newCount > 0);
  }
  messagesEl.addEventListener('scroll', updateToBottom);
  toBottom.addEventListener('click', function () {
    newCount = 0;
    messagesEl.scrollTo({ top: messagesEl.scrollHeight, behavior: 'smooth' });
  });

  var menu = $('#msgMenu'), menuStamp = 0, pressTimer = null, pressXY = null;
  function closeMenu() { menu.classList.remove('show'); }
  function findMsg(id) { var a = msgs(activeId); for (var i = 0; i < a.length; i++) if (a[i].id === id) return a[i]; return null; }
  function addItem(label, cls, fn) {
    var b = document.createElement('button'); b.type = 'button'; b.textContent = label; if (cls) b.className = cls;
    b.addEventListener('click', function () { closeMenu(); fn(); });
    menu.appendChild(b);
  }
  function fallbackCopy(t) {
    var ta = document.createElement('textarea'); ta.value = t; ta.style.cssText = 'position:fixed;opacity:0;top:0;left:0';
    document.body.appendChild(ta); ta.select();
    var ok = false; try { ok = document.execCommand('copy'); } catch (e) {}
    ta.remove(); toast(ok ? 'Нусха шуд ✓' : 'Нусха нашуд');
  }
  function copyText(t) {
    if (navigator.clipboard && navigator.clipboard.writeText) {
      navigator.clipboard.writeText(t).then(function () { toast('Нусха шуд ✓'); }, function () { fallbackCopy(t); });
    } else fallbackCopy(t);
  }
  function deleteMsg(id, row) {
    var cid = activeId, arr = msgs(cid), idx = -1;
    for (var i = 0; i < arr.length; i++) if (arr[i].id === id) { idx = i; break; }
    if (idx < 0) return;
    if (arr[idx].type === 'voice') stopAudio();
    arr.splice(idx, 1); save();
    row.style.animation = 'msgOut .22s forwards';
    setTimeout(function () {
      if (cid === activeId) {
        var prev = row.previousElementSibling, next = row.nextElementSibling;
        row.remove();
        if (prev && prev.classList.contains('day') && (!next || next.classList.contains('day'))) prev.remove();
        if (!msgs(cid).length) renderMessages();
        updateToBottom();
      }
      renderList();
    }, 220);
  }
  function openMenu(row, x, y, touch) {
    var m = findMsg(row.dataset.id); if (!m) return;
    menu.innerHTML = '';
    if (m.type === 'text' || (m.type === 'image' && m.text)) addItem('📋  Нусха кардан', '', function () { copyText(m.text); });
    addItem('🗑  Нест кардан', 'danger', function () { deleteMsg(m.id, row); });
    menu.classList.add('show');
    var w = menu.offsetWidth, h = menu.offsetHeight;
    var left = Math.max(8, Math.min(x, window.innerWidth - w - 8));
    var top = touch ? (y - h - 14 >= 8 ? y - h - 14 : y + 14) : y;
    top = Math.max(8, Math.min(top, window.innerHeight - h - 8));
    menu.style.left = left + 'px'; menu.style.top = top + 'px';
  }
  messagesEl.addEventListener('contextmenu', function (e) {
    var row = e.target.closest ? e.target.closest('.row') : null;
    if (!row) return;
    e.preventDefault();
    if (Date.now() - menuStamp < 900) return;
    openMenu(row, e.clientX, e.clientY, false);
  });
  messagesEl.addEventListener('pointerdown', function (e) {
    if (e.pointerType !== 'touch') return;
    var row = e.target.closest ? e.target.closest('.row') : null;
    if (!row) return;
    pressXY = [e.clientX, e.clientY];
    clearTimeout(pressTimer);
    pressTimer = setTimeout(function () {
      menuStamp = Date.now();
      openMenu(row, pressXY[0], pressXY[1], true);
      try { if (navigator.vibrate) navigator.vibrate(15); } catch (_) {}
    }, 450);
  });
  messagesEl.addEventListener('pointermove', function (e) {
    if (pressXY && (Math.abs(e.clientX - pressXY[0]) > 10 || Math.abs(e.clientY - pressXY[1]) > 10)) clearTimeout(pressTimer);
  });
  ['pointerup', 'pointercancel'].forEach(function (ev) { messagesEl.addEventListener(ev, function () { clearTimeout(pressTimer); }); });
  document.addEventListener('pointerdown', function (e) { if (!menu.contains(e.target)) closeMenu(); });
  messagesEl.addEventListener('scroll', closeMenu);
  window.addEventListener('resize', closeMenu);
  document.addEventListener('keydown', function (e) { if (e.key === 'Escape') { closeMenu(); emojiPanel.classList.remove('show'); } });

  $('#clearBtn').addEventListener('click', function () {
    if (!activeId) return;
    if (!msgs(activeId).length) { toast('Суҳбат аллакай холӣ аст'); return; }
    if (!window.confirm('Тамоми суҳбатро тоза кунам?')) return;
    stopAudio();
    state.chats[activeId] = []; save();
    renderMessages(); renderList();
  });

  window.addEventListener('beforeunload', function () { if (recording) releaseStream(); });
  document.addEventListener('visibilitychange', function () { if (document.hidden && curAudio) { curAudio.pause(); if (curReset) curReset(); } });

  load();
  updateMainBtn();
  startApp();
})();
</script>
</body>
</html>
