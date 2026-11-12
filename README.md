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
  import { getFirestore, collection, addDoc, onSnapshot, query, orderBy } from "https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore.js";

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
  const db = getFirestore(firebaseApp);

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
    if (confirm('Мехоҳед аз ҳисоб бароед?')) {
      await signOut(auth);
    }
  });

  // Рӯйхати мустақили чатҳо (Ҳоло ҳамаи чатҳои пештараи сунъӣ тоза карда шуданд ва динамикӣ мешаванд)
  let CONTACTS = [];
  let state = { chats: {}, unread: {} };
  let activeId = null;
  let typing = {};
  let pendingImage = null;

  onAuthStateChanged(auth, (user) => {
    if (user) {
      authScreen.style.display = 'none';
      appScreen.style.display = 'grid';
      
      // Намоиши номи корбар аз Email
      let username = user.email.split('@')[0];
      document.getElementById('meName').textContent = username;
      document.getElementById('meAv').src = 'data:image/svg+xml;charset=utf-8,' + encodeURIComponent('<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><rect width="100" height="100" fill="#6366f1"/><text x="50" y="50" text-anchor="middle" dominant-baseline="central" font-size="46" fill="#fff">' + username.charAt(0).toUpperCase() + '</text></svg>');

      // Ҳар касе ки ворид мешавад ё сабти ном мекунад, ба таври автоматӣ ба рӯйхати чатҳо илова мешавад (барои тест бо худ ё дигарон)
      CONTACTS = [
        { id: user.uid, name: username + ' (Худатон)', hue: 238, online: true, replies: ['Салом! Паёми худро гирифтам ✓'] }
      ];

      startApp();
    } else {
      authScreen.style.display = 'grid';
      appScreen.style.display = 'none';
    }
  });

  function startApp() {
    renderList();
    if (CONTACTS.length > 0) openChat(CONTACTS[0].id);
    document.getElementById('app').classList.add('appear');
  }

  // Функсияҳои боқимондаи чат
  var $ = function (s) { return document.querySelector(s); };
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
  function avatar(name, hue) {
    var ch = (name.trim().charAt(0) || '?').toUpperCase();
    var svg = '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100">' +
      '<defs><linearGradient id="g" x1="0" y1="0" x2="1" y2="1">' +
      '<stop offset="0" stop-color="hsl(' + hue + ',75%,60%)"/><stop offset="1" stop-color="hsl(' + ((hue + 50) % 360) + ',80%,42%)"/>' +
      '</linearGradient></defs><rect width="100" height="100" fill="url(#g)"/>' +
      '<text x="50" y="50" text-anchor="middle" dominant-baseline="central" font-family="Arial,sans-serif" font-size="46" font-weight="700" fill="#fff">' + ch + '</text></svg>';
    return 'data:image/svg+xml;charset=utf-8,' + encodeURIComponent(svg);
  }

  function toast(msg) {
    var t = $('#toast'); t.textContent = msg; t.classList.add('show');
    setTimeout(function () { t.classList.remove('show'); }, 3200);
  }

  function byId(id) { for (var i = 0; i < CONTACTS.length; i++) if (CONTACTS[i].id === id) return CONTACTS[i]; return null; }
  function msgs(id) { return state.chats[id] || (state.chats[id] = []); }
  function lastMsg(id) { var a = state.chats[id]; return a && a.length ? a[a.length - 1] : null; }
  function uid() { return Date.now().toString(36) + Math.random().toString(36).slice(2, 7); }

  var listEl = $('#list'), searchEl = $('#searchInput');
  searchEl.addEventListener('input', renderList);

  function previewText(m) {
    if (!m) return 'Паём нест';
    var p = m.from === 'me' ? 'Шумо: ' : '';
    if (m.type === 'image') return p + '📷 Акс';
    if (m.type === 'voice') return p + '🎤 Паёми овозӣ';
    return p + m.text;
  }

  function renderList() {
    var q = searchEl.value.trim().toLowerCase();
    var items = CONTACTS.filter(function (c) { return !q || c.name.toLowerCase().indexOf(q) !== -1; });
    listEl.innerHTML = '';
    items.forEach(function (c) {
      c.avatar = avatar(c.name, c.hue || 200);
      var m = lastMsg(c.id), un = state.unread[c.id] || 0;
      var b = document.createElement('button');
      b.className = 'chat-item' + (c.id === activeId ? ' active' : '');
      b.innerHTML =
        '<div class="av"><img src="' + c.avatar + '"><span class="dot on"></span></div>' +
        '<div class="ci-body"><div class="ci-top"><span class="ci-name">' + c.name + '</span><span class="ci-time">' + (m ? hhmm(m.ts) : '') + '</span></div>' +
        '<div class="ci-bot"><span class="ci-last">' + previewText(m) + '</span></div></div>';
      b.addEventListener('click', function () { openChat(c.id); });
      listEl.appendChild(b);
    });
  }

  var messagesEl = $('#messages'), chatHead = $('#chatHead'), composer = $('#composer');
  var inputEl = $('#input'), mainBtn = $('#mainBtn');

  function openChat(id) {
    activeId = id;
    state.unread[id] = 0;
    var c = byId(id);
    chatHead.style.display = 'flex';
    composer.style.display = 'block';
    $('#chAv').src = c.avatar;
    $('#chName').textContent = c.name;
    $('#chStatus').textContent = 'онлайн';
    $('#app').classList.add('chat-open');
    renderMessages();
    renderList();
  }

  $('#backBtn').addEventListener('click', function () {
    $('#app').classList.remove('chat-open');
    activeId = null;
    renderList();
  });

  function renderMessages() {
    messagesEl.innerHTML = '';
    var arr = msgs(activeId);
    if (!arr.length) {
      messagesEl.innerHTML = '<div class="placeholder"><div style="font-size:15px">Ҳоло паём нест. Аввалин шуда нависед 👋</div></div>';
      return;
    }
    arr.forEach(function (m) {
      messagesEl.appendChild(buildMsg(m));
    });
    messagesEl.scrollTop = messagesEl.scrollHeight;
  }

  function buildMsg(m) {
    var row = document.createElement('div');
    row.className = 'row ' + (m.from === 'me' ? 'me' : 'them');
    var b = document.createElement('div');
    b.className = 'bubble';
    b.innerHTML = '<div class="txt">' + m.text + '</div><div class="meta"><span>' + hhmm(m.ts) + '</span></div>';
    row.appendChild(b);
    return row;
  }

  function pushMsg(chatId, msg) {
    msgs(chatId).push(msg);
    if (chatId === activeId) renderMessages();
    renderList();
  }

  function sendCurrent() {
    if (!activeId) return;
    var text = inputEl.value.trim();
    if (text) {
      pushMsg(activeId, { id: uid(), from: 'me', text: text, ts: Date.now() });
      inputEl.value = '';
      
      // Ҷавоби худкори демо барои санҷиш
      setTimeout(() => {
        pushMsg(activeId, { id: uid(), from: 'them', text: 'Паёми шумо қабул шуд: ' + text, ts: Date.now() });
      }, 1000);
    }
  }

  mainBtn.addEventListener('click', sendCurrent);
  inputEl.addEventListener('keydown', function (e) {
    if (e.key === 'Enter' && !e.shiftKey) { e.preventDefault(); sendCurrent(); }
  });

  $('#clearBtn').addEventListener('click', function () {
    if (!activeId) return;
    state.chats[activeId] = [];
    renderMessages();
    renderList();
  });
</script>
</body>
</html>
