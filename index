<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<meta name="theme-color" content="#f2f2f7" media="(prefers-color-scheme: light)">
<meta name="theme-color" content="#000000" media="(prefers-color-scheme: dark)">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-title" content="Measurements">
<meta name="apple-mobile-web-app-status-bar-style" content="default">
<link rel="apple-touch-icon" href="icon.png">
<link rel="icon" type="image/png" href="icon.png">
<style>:root{padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}body{margin:0}img{max-width:100%}[hidden]{display:none!important}</style>
<title>Home Measurements</title>
<style>
/* Layout: iOS-style grouped lists. Sticky blurred header with a large title that compacts on scroll, search, room filter.
   Rooms are inset groups of rows; a row pushes a full-screen detail view with measurements, a size compare, and saved finds. */
:root{
  --bg:#f2f2f7; --surface:#ffffff; --fill:#e9e9ee; --ink:#111113; --muted:#6c6c72; --sep:rgba(60,60,67,.16);
  --accent:#0a6cdf; --tape:#f5c518; --tape-ink:#2a2200; --good:#1f7a36; --good-bg:#e3f4e7; --bad:#c4161c; --bad-bg:#fbe5e5;
  --bar:#f2f2f7; --scrim:rgba(0,0,0,.35); --toast:#1c1c1e; --toast-ink:#ffffff;
  --sans:-apple-system,BlinkMacSystemFont,"SF Pro Text","Helvetica Neue",system-ui,"Segoe UI",Roboto,sans-serif;
  --display:-apple-system,BlinkMacSystemFont,"SF Pro Display","Helvetica Neue",system-ui,"Segoe UI",Roboto,sans-serif;
  color-scheme:light;
}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){
  --bg:#000000; --surface:#1c1c1e; --fill:#2c2c2e; --ink:#f5f5f7; --muted:#9a9aa1; --sep:rgba(84,84,88,.55);
  --accent:#3b9bff; --tape:#f5c518; --tape-ink:#2a2200; --good:#4cd471; --good-bg:#12301b; --bad:#ff6961; --bad-bg:#3a1414;
  --bar:#000000; --scrim:rgba(0,0,0,.55); --toast:#f5f5f7; --toast-ink:#111113; color-scheme:dark}}
:root[data-theme="dark"]{
  --bg:#000000; --surface:#1c1c1e; --fill:#2c2c2e; --ink:#f5f5f7; --muted:#9a9aa1; --sep:rgba(84,84,88,.55);
  --accent:#3b9bff; --tape:#f5c518; --tape-ink:#2a2200; --good:#4cd471; --good-bg:#12301b; --bad:#ff6961; --bad-bg:#3a1414;
  --bar:#000000; --scrim:rgba(0,0,0,.55); --toast:#f5f5f7; --toast-ink:#111113; color-scheme:dark}
*{box-sizing:border-box;-webkit-tap-highlight-color:transparent}
body{background:var(--bg);color:var(--ink);font-family:var(--sans);font-size:17px;line-height:1.35;padding-inline:16px;padding-block:0 96px;-webkit-font-smoothing:antialiased}
.wrap{max-width:720px;margin:0 auto}
button{font:inherit;color:inherit}
.num{font-variant-numeric:tabular-nums}

/* header */
header.top{position:sticky;top:env(safe-area-inset-top,0px);z-index:5;margin-inline:-16px;padding:8px 16px 10px;background:var(--bar);-webkit-backdrop-filter:saturate(180%) blur(20px);backdrop-filter:saturate(180%) blur(20px);border-bottom:.5px solid transparent;transition:border-color .2s}
header.top.compact{border-bottom-color:var(--sep)}
.titlebar{display:flex;align-items:flex-end;justify-content:space-between;gap:12px;min-height:44px}
h1{font-family:var(--display);font-weight:700;font-size:32px;letter-spacing:.01em;margin:6px 0 2px;line-height:1.1;transition:font-size .2s}
header.compact h1{font-size:19px;margin-top:0}
.seg{display:inline-flex;background:var(--fill);border-radius:9px;padding:2px;flex:none;margin-bottom:4px}
.seg button{border:0;background:transparent;font-size:13px;font-weight:600;padding:5px 12px;border-radius:7px;cursor:pointer;color:var(--ink);min-width:44px}
.seg button[aria-pressed="true"]{background:var(--surface);box-shadow:0 1px 3px rgba(0,0,0,.14)}
.search{position:relative;margin-top:8px}
.search svg{position:absolute;left:10px;top:50%;transform:translateY(-50%);width:17px;height:17px;color:var(--muted);pointer-events:none}
.search input{width:100%;font:17px var(--sans);color:var(--ink);background:var(--fill);border:0;border-radius:11px;padding:10px 38px 10px 34px;outline:none;-webkit-appearance:none;appearance:none}
.search input::placeholder{color:var(--muted)}
.search input::-webkit-search-cancel-button{display:none}
.search input:focus{box-shadow:0 0 0 2px var(--accent)}
.clearbtn{position:absolute;right:6px;top:50%;transform:translateY(-50%);border:0;background:var(--muted);color:var(--surface);width:20px;height:20px;border-radius:50%;font-size:13px;line-height:20px;cursor:pointer;padding:0}
.chips{display:flex;gap:8px;overflow-x:auto;scrollbar-width:none;margin:10px -16px 0;padding-inline:16px}
.chips::-webkit-scrollbar{display:none}
.chip{flex:none;font-size:14px;font-weight:600;background:var(--surface);border:0;border-radius:999px;padding:7px 13px;cursor:pointer;white-space:nowrap;box-shadow:inset 0 0 0 .5px var(--sep)}
.chip[aria-pressed="true"]{background:var(--ink);color:var(--bg);box-shadow:none}

/* lists */
.sechead{position:sticky;top:calc(env(safe-area-inset-top,0px) + var(--hdr,160px) - 1px);z-index:3;margin:10px -16px 8px;padding:10px 20px 8px;background:var(--bg);font-family:var(--display);font-size:26px;font-weight:700;letter-spacing:.005em;line-height:1.15;color:var(--ink);display:flex;flex-direction:column;gap:1px}
.sechead span{font-family:var(--sans);font-size:14px;font-weight:400;color:var(--muted);letter-spacing:0}
.sechead.small{font-size:20px}
.row .shopic{width:40px;height:40px;border-radius:10px;flex:none;display:grid;place-items:center;background:var(--tape);color:var(--tape-ink)}
.row .shopic svg{width:22px;height:22px}
.row.shop .ttl{font-weight:600}
.group{background:var(--surface);border-radius:12px;overflow:hidden}
.row{display:flex;align-items:center;gap:12px;width:100%;text-align:left;background:transparent;border:0;padding:11px 14px 11px 16px;min-height:52px;cursor:pointer;position:relative}
.row+.row::before{content:"";position:absolute;top:0;left:16px;right:0;border-top:.5px solid var(--sep)}
.row.hasthumb+.row::before,.row+.row.hasthumb::before{left:16px}
.row:active{background:var(--fill)}
.row .body{flex:1;min-width:0}
.row .ttl{font-size:17px;font-weight:500;display:block;overflow-wrap:anywhere}
.row .grp{font-size:13px;color:var(--muted);display:block}
.row .sub{font-size:14px;color:var(--muted);display:block;margin-top:2px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.row .sub b{color:var(--ink);font-weight:500}
.thumb{width:40px;height:40px;border-radius:8px;object-fit:cover;flex:none;background:var(--fill)}
.badge{flex:none;font-size:12px;font-weight:700;background:var(--tape);color:var(--tape-ink);border-radius:999px;min-width:22px;height:22px;padding:0 7px;display:inline-grid;place-items:center}
.chev{flex:none;width:8px;height:13px;color:var(--muted);opacity:.6}
.row.add{color:var(--accent);font-weight:500;min-height:46px}
.recents{margin-top:4px}
.empty{color:var(--muted);text-align:center;padding:48px 16px;font-size:15px}
.empty b{display:block;color:var(--ink);font-size:20px;margin-bottom:6px}
mark{background:var(--tape);color:var(--tape-ink);border-radius:3px;padding:0 1px}

/* detail view */
.scrim{position:fixed;inset:0;background:var(--scrim);z-index:20;display:flex;justify-content:center}
.view{background:var(--bg);width:100%;max-width:720px;height:100%;overflow-y:auto;-webkit-overflow-scrolling:touch;padding:0 16px calc(48px + env(safe-area-inset-bottom,0px));overscroll-behavior:contain}
@media (min-width:760px){.scrim{align-items:center;padding:24px}.view{border-radius:16px;height:auto;max-height:100%}}
.nav{position:sticky;top:0;z-index:2;margin-inline:-16px;padding:calc(6px + env(safe-area-inset-top,0px)) 8px 6px;display:flex;align-items:center;gap:8px;min-height:50px;background:var(--bar);-webkit-backdrop-filter:saturate(180%) blur(20px);backdrop-filter:saturate(180%) blur(20px);border-bottom:.5px solid var(--sep)}
.navbtn{border:0;background:transparent;color:var(--accent);font-size:17px;padding:8px;cursor:pointer;display:flex;align-items:center;gap:4px;min-height:44px;max-width:60%}
.navbtn span{white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.navbtn svg{width:11px;height:19px;flex:none}
.navtitle{flex:1;text-align:center;font-weight:600;font-size:17px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;opacity:0;transition:opacity .15s}
.nav.scrolled .navtitle{opacity:1}
.navspacer{width:60px;flex:none}
.hero{padding:14px 4px 4px}
.hero .crumb{font-size:13px;color:var(--muted);font-weight:500;text-transform:uppercase;letter-spacing:.03em}
.hero h2{font-family:var(--display);font-size:30px;font-weight:700;margin:2px 0 0;line-height:1.12;overflow-wrap:anywhere;text-wrap:balance}
.note{font-size:15px;color:var(--muted);margin:8px 4px 0}
.warn{font-size:15px;margin:12px 0 0;padding:11px 14px;border-radius:12px;background:var(--bad-bg);color:var(--ink)}
.warn b{color:var(--bad)}
.cmp{margin-top:16px;background:var(--surface);border-radius:12px;padding:12px 14px 14px;display:grid;gap:10px}
.cmp .head{display:flex;align-items:baseline;justify-content:space-between;gap:10px}
.cmp .head b{font-size:17px;font-weight:600}
.cmp .head small{display:block;font-size:13px;color:var(--muted);margin-top:2px}
.cmp .dims{display:grid;grid-template-columns:repeat(auto-fit,minmax(120px,1fr));gap:8px}
.cmp .dim{display:grid;gap:4px}
.cmp .dim label{font-size:13px;font-weight:600;color:var(--muted);text-transform:uppercase;letter-spacing:.03em}
.cmp .dim .box{display:flex;align-items:center;background:var(--fill);border-radius:9px;padding-right:10px}
.cmp .dim .box:focus-within{box-shadow:0 0 0 2px var(--accent)}
.cmp input{width:100%;min-width:0;font:600 17px var(--sans);color:var(--ink);background:transparent;border:0;padding:9px 6px 9px 11px;outline:none}
.cmp .u{font-size:15px;color:var(--muted)}
.verdict{font-size:15px;font-weight:600;border-radius:9px;padding:9px 12px}
.verdict.ok{background:var(--good-bg);color:var(--good)}
.verdict.no{background:var(--bad-bg);color:var(--bad)}
.verdict span{display:block;font-weight:400;font-size:14px;margin-top:2px}
.m .fits{grid-column:1/-1;display:flex;flex-wrap:wrap;gap:6px}
.m{display:grid;grid-template-columns:1fr auto;gap:2px 12px;padding:11px 14px 11px 16px;position:relative;align-items:center}
.m+.m::before,.group>.m+.row::before,.group>.m+form::before{content:"";position:absolute;top:0;left:16px;right:0;border-top:.5px solid var(--sep)}
.m .lbl{min-width:0;font-size:16px;overflow-wrap:anywhere}
.m .lbl .suf{color:var(--muted)}
.m .valbtn{border:0;background:transparent;text-align:right;cursor:pointer;padding:4px 0 4px 8px;border-radius:8px}
.m .val{font-size:20px;font-weight:600;font-variant-numeric:tabular-nums;white-space:nowrap;display:block}
.m .val .approx{color:var(--muted);font-weight:500;margin-right:1px}
.m .ft{display:block;font-size:13px;color:var(--muted);font-variant-numeric:tabular-nums}
.m .na{font-size:15px;color:var(--muted);font-weight:500;white-space:normal}
.m .foot{grid-column:1/-1;font-size:13px;color:var(--muted)}
.m .fit{grid-column:1/-1;justify-self:start;font-size:13px;font-weight:600;border-radius:6px;padding:2px 8px;margin-top:2px}
.fit.ok{background:var(--good-bg);color:var(--good)}
.fit.no{background:var(--bad-bg);color:var(--bad)}
.m .mine{grid-column:1/-1;font-size:13px;color:var(--muted);display:flex;gap:6px;align-items:center}
.link{border:0;background:transparent;color:var(--accent);font-size:15px;cursor:pointer;padding:6px 4px;min-height:32px}
.link.danger{color:var(--bad)}
.foot-note{font-size:13px;color:var(--muted);margin:8px 16px 0}
h3.sec{font-size:13px;font-weight:500;text-transform:uppercase;letter-spacing:.02em;color:var(--muted);margin:28px 16px 7px}
.form{display:grid;gap:10px;padding:14px;position:relative}
.form input[type=url],.form input[type=text],.form select{width:100%;font:17px var(--sans);color:var(--ink);background:var(--fill);border:0;border-radius:10px;padding:11px 12px;outline:none}
.form input:focus,.form select:focus{box-shadow:0 0 0 2px var(--accent)}
.form .pair{display:grid;grid-template-columns:1fr 110px;gap:8px}
.form .chk{display:flex;align-items:center;gap:10px;font-size:16px}
.form .chk input{width:20px;height:20px;accent-color:var(--accent)}
.form .hint{font-size:13px;color:var(--muted)}
.btns{display:flex;gap:8px;flex-wrap:wrap;align-items:center}
.btn{font-size:16px;font-weight:600;border-radius:10px;padding:11px 16px;cursor:pointer;border:0;background:var(--fill);color:var(--accent);display:inline-flex;align-items:center;gap:6px;min-height:44px}
.btn.primary{background:var(--accent);color:#fff}
.btn.danger{color:var(--bad)}
.btn.armed{background:var(--bad);color:#fff}
.btn[disabled]{opacity:.45;cursor:default}
.spacer{flex:1}
.status{font-size:14px;color:var(--muted);min-height:1.2em}
.status.err{color:var(--bad)}
.save{display:flex;gap:12px;align-items:center;padding:10px 14px 10px 16px;position:relative}
.save+.save::before,.form+.save::before{content:"";position:absolute;top:0;left:16px;right:0;border-top:.5px solid var(--sep)}
.save .pic{width:64px;height:64px;border-radius:10px;background:var(--fill);display:grid;place-items:center;color:var(--muted);overflow:hidden;border:0;padding:0;flex:none;cursor:zoom-in}
.save .pic.linkic{cursor:default}
.save .pic img{width:100%;height:100%;object-fit:cover}
.save .pic svg{width:24px;height:24px}
.save .info{flex:1;min-width:0}
.save a{color:var(--accent);font-weight:600;text-decoration:none;word-break:break-all}
.save .n{font-size:15px;margin-top:2px;overflow-wrap:anywhere}
.save .d{font-size:13px;color:var(--muted);margin-top:2px}
.save .acts{display:flex;flex-direction:column;align-items:flex-end}
.buy{flex:none;width:30px;height:30px;border-radius:50%;border:2px solid var(--muted);background:transparent;display:grid;place-items:center;cursor:pointer;padding:0;color:#fff}
.buy svg{width:16px;height:16px;opacity:0}
.buy[aria-checked="true"]{background:var(--good);border-color:var(--good)}
.buy[aria-checked="true"] svg{opacity:1}
.buy[disabled]{cursor:default}
.save.isbought .d .tag{color:var(--good);font-weight:600}
.tabs{display:grid;grid-template-columns:1fr 1fr;background:var(--fill);border-radius:10px;padding:2px;margin-top:8px}
.tabs button{border:0;background:transparent;font-size:15px;font-weight:600;padding:7px 10px;border-radius:8px;cursor:pointer;color:var(--ink)}
.tabs button[aria-selected="true"]{background:var(--surface);box-shadow:0 1px 3px rgba(0,0,0,.14)}
.tabs .n{color:var(--muted);font-weight:500}
.save .where{border:0;background:transparent;padding:0;color:var(--accent);font-size:13px;cursor:pointer;text-align:left}
.save.editing{display:block;padding:0}
.viewer{position:fixed;inset:0;z-index:40;background:rgba(0,0,0,.92);display:flex;align-items:center;justify-content:center;padding:16px;cursor:zoom-out}
.viewer img{max-height:100%;max-width:100%;border-radius:10px}
.gate{position:fixed;inset:0;z-index:60;background:var(--bg);display:grid;place-items:center;padding:24px 16px}
.gatebox{width:100%;max-width:380px;display:grid;gap:12px;background:var(--surface);border-radius:16px;padding:22px 18px}
.gatebox h2{font-family:var(--display);font-size:26px;margin:0}
.gatebox p{margin:0;color:var(--muted);font-size:15px}
.gatebox input{width:100%;font:17px var(--sans);color:var(--ink);background:var(--fill);border:0;border-radius:10px;padding:12px;outline:none}
.gatebox input:focus{box-shadow:0 0 0 2px var(--accent)}
.gatebox .btn{justify-content:center}
.toast{position:fixed;left:50%;bottom:calc(20px + env(safe-area-inset-bottom,0px));transform:translateX(-50%);z-index:50;background:var(--toast);color:var(--toast-ink);border-radius:14px;padding:10px 10px 10px 16px;display:flex;align-items:center;gap:14px;font-size:15px;font-weight:500;box-shadow:0 8px 30px rgba(0,0,0,.25);max-width:calc(100% - 32px)}
.toast button{border:0;background:transparent;color:var(--tape);font-weight:700;font-size:15px;padding:6px 8px;cursor:pointer}
:focus-visible{outline:2px solid var(--accent);outline-offset:2px}
@media (prefers-reduced-motion:no-preference){
  .view{animation:push .26s cubic-bezier(.2,.8,.2,1)}
  @keyframes push{from{transform:translateX(24px);opacity:.4}to{transform:none;opacity:1}}
  @media (min-width:760px){.view{animation:pop .2s ease-out}@keyframes pop{from{transform:scale(.98);opacity:.5}to{transform:none;opacity:1}}}
  .toast{animation:rise .2s ease-out}@keyframes rise{from{transform:translate(-50%,10px);opacity:0}to{transform:translateX(-50%);opacity:1}}
}
</style>

</head>
<body>
<div class="wrap">
  <header class="top" id="top">
    <div class="titlebar"><h1>Home Measurements</h1>
      <div class="seg" role="group" aria-label="Units"><button id="uIn" aria-pressed="true">in</button><button id="uCm" aria-pressed="false">cm</button></div></div>
    <div class="tabs" role="tablist" aria-label="View"><button id="tSpaces" role="tab">Spaces</button><button id="tBought" role="tab">Purchased <span class="n" id="boughtN"></span></button></div>
    <div class="search">
      <svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" aria-hidden="true"><circle cx="8.5" cy="8.5" r="6"/><path d="m13 13 5 5"/></svg>
      <input id="q" type="search" placeholder="Search" autocomplete="off" autocorrect="off" spellcheck="false" enterkeyhint="search" aria-label="Search spaces">
      <button id="clear" class="clearbtn" aria-label="Clear search" hidden>×</button>
    </div>
    <div class="chips" id="chips" role="toolbar" aria-label="Filter by room"></div>
  </header>
  <main id="out"></main>
</div>
<div id="viewHost"></div>
<div id="toastHost" aria-live="polite"></div>

<script>
// Values in inches. "~" prefix = approximate (around/about/roughly in the original note).
// Row shape: [label, value, direction word, footnote]
const H = [
 {room:"Living Room", spaces:[
  {name:"Overall", m:[["Fireplace wall to single-window wall","269","long"],["Back of barstools to big window wall","~207","wide"]]},
  {name:"Single-Window Wall", m:[["Wall width","211"],["Small window width","66"],["Small window height","77"]]},
  {name:"Fireplace Wall", m:[["Wall width","211"]]},
  {name:"Full Window Wall", m:[["Wall width","270"],["Window-to-window width only","187"]]},
  {name:"Bar", m:[["Bar width only","127"]]},
  {name:"Walkways", m:[["Living room walkway 1","51","wide"],["Living room walkway 2","51","wide"]]},
  {name:"Couches + Rug", dims:{"Back of couch":"width"}, m:[["Couches where they go together","43 × 49"],["Back of couch","~83"],["Rug to cover all ground of couch","137 × 132"]]}
 ]},
 {room:"Kitchen", spaces:[
  {group:"Buffet Area", name:"Buffet Counter", m:[["Width",null]]},
  {group:"Buffet Area", name:"Buffet Window", note:"Measured molding to molding", m:[["Width","30"],["Height","66"]]},
  {group:"Buffet Area", name:"Buffet Area Notes", dims:{"Back and wall":"width","With plug in area":"width","To plug in":"width"}, note:"Recorded as written in the original note", m:[["Back and wall","71"],["With plug in area","25"],["To plug in","10"]]}
 ]},
 {room:"Entry", view:"Walking in through the front door", spaces:[
  {name:"Entry Closet", dims:{"Doorway":"width"}, m:[["Closet","45","wide"],["Doorway","28"],["Depth","23"]]},
  {name:"Back Window", m:[["Width","65"],["Height","77"]]},
  {name:"Back Wall", note:"Includes the window", m:[["Width","96"]]},
  {name:"Right Wall", m:[["Width","42"],["Height","~108"]]},
  {name:"Back Right Wall", m:[["Width","92"]]},
  {name:"Entrance Wall with Door", m:[["Wall width","81"],["Door only","44","wide"]]},
  {name:"Walkway to the Left", note:"Measured from the stairs to the back wall with the window", m:[["Length","90"]]}
 ]},
 {room:"Loft", view:"From the hall entry looking toward the balcony", spaces:[
  {group:"Office Nook", name:"Left Wall", m:[["Width/depth","63"],["Height","94"]]},
  {group:"Office Nook", name:"Wall with Window", m:[["Wall width","90"],["Wall height","94"]]},
  {group:"Office Nook", name:"Window Only", m:[["Width","63"],["Height","57"],["Floor to window sill","29.5"]]},
  {group:"Office Nook", name:"Right Side Wall", note:"Wall to the right of the window wall", m:[["Depth/width","30.5"],["Height","94"]]},
  {group:"Balcony", name:"Bars / Railing", m:[["Width","236"],["Floor to top of bar","36.75"]]},
  {group:"Balcony", name:"Side Walls", m:[["Wall depth (both sides)","17"]]},
  {group:"TV Wall Nook", name:"TV Wall", note:"Measured from the left side of the nook to the right side", m:[["Width","60"]]},
  {group:"TV Wall Nook", name:"Left Side of TV Wall", m:[["Depth/width","8"],["Height","95"]]},
  {group:"TV Wall Nook", name:"Right Side Wall", note:"Wall to the right of the outlet", m:[["Depth","25.5"],["Height","95"]]},
  {group:"Couch Nook", name:"Back Wall with Two Outlets", note:"Wall opposite the balcony", m:[["Width","139"],["Height","94"]]},
  {group:"Couch Nook", name:"Wall to the Left of the Couch", note:"When standing at the balcony facing the couch", m:[["Depth","31"]]}
 ]},
 {room:"Upstairs Hall", spaces:[
  {name:"Hall Walkway", note:"Left toward Bedroom 1", m:[["Width","46"]]},
  {group:"Right Hall Wall", name:"Right of Bathroom Door", note:"Bathroom door to loft entry", m:[["Width","124"],["Height","94"],["Bathroom door to thermostat","~77","wide"],["Floor to thermostat","55"]]},
  {group:"Right Hall Wall", name:"Left of Bathroom Door", note:"Wall has an outlet; measured from molding to the double-bedroom wall", m:[["Width","72.5"]]},
  {name:"Utility Closet Wall", note:"Wall opposite the bathroom-door wall", m:[["Stairs to utility closet door molding","93","wide"],["Height","94"]]},
  {group:"Double-Bedroom Wall + Hall", name:"Bedroom 1 / Bedroom 2 Sides", dims:{"Bedroom 1 side: door molding to right corner wall":"width","Bedroom 2 side: door molding to left corner wall":"width"}, m:[["Bedroom 1 side: door molding to right corner wall","32"],["Bedroom 2 side: door molding to left corner wall","18"]]},
  {group:"Double-Bedroom Wall + Hall", name:"Bedroom 3 Wall", dims:{"Molding to corner":"width"}, note:"Wall opposite the double-bedroom doors; contains a light switch", m:[["Molding to corner","47"]]},
  {group:"Double-Bedroom Wall + Hall", name:"Wall Between Bedrooms 2 and 3", m:[["Width","40"]]},
  {group:"Double-Bedroom Wall + Hall", name:"Hall at Double-Bedroom Entry", m:[["Width","40"]]}
 ]},
 {room:"Guest Bathroom", view:"From the door entry", spaces:[
  {name:"Sink / Counter", m:[["Left of sink: black counter ledge to ceiling","57","tall"],["Mirror to mirror","32","wide"],["Mirror wall to drawers","21","deep/long"]]},
  {name:"Toilet Trash Can Space", note:"Space left of the toilet to the counter", m:[["Width","9"],["Depth","21"]]},
  {name:"Shower", m:[["Shower curtain width","56"],["Shower floor: back of shower to drain","40","long"],["Shower floor width","16"]]},
  {name:"Shower Ledge", note:"Left of the shower-spout wall; on the wall opposite the shower curtain", m:[["Depth","2.5"],["Width","54"]]}
 ]},
 {room:"Guest Bedroom 1", view:"From the door entry", spaces:[
  {name:"Left Wall", m:[["Doorstop to window","120","wide"]]},
  {name:"Back Window Wall", m:[["Wall width","64"],["Window only","34.5","wide"],["Entire window-sill ledge","36.5","wide"],["Floor to window sill","20.75"],["Right side of window to nook corner","31","wide"],["Wall/nook depth on right side of window","12"]]},
  {name:"Back Wall to Right of Window Nook", m:[["Width","70"]]},
  {name:"Right Wall", m:[["Width","142"],["Height","94"],["Outlet to outlet","89","wide"],["Left corner to Outlet 1","16.5",null,"Recorded as a depth measurement and noted as “pushing it.”"],["Right-corner outlet to closet door","30.5","wide"]]},
  {name:"Door Wall", note:"Wall opposite the window wall. Contains an outlet and two light switches.", m:[["Closet-door molding to entry-door molding","60","wide"],["Floor to bottom of light switches","41.5"]]}
 ]},
 {room:"Bedroom 2", view:"From the door entry", spaces:[
  {name:"Right Wall", m:[["Doorstop to window wall","123","wide"],["Outlet to ethernet cable outlet near doorstop","64","wide"],["End of window ledge/corner to left outlet","42","wide"]]},
  {name:"Back Window Wall Nook", m:[["Window only","34","wide"],["Floor to window-sill ledge","20.5"],["Window ledge to left corner","29.5","wide"],["Corner ledge to start of window","31.5","wide"],["Wall nook depth, left of window","12.5"]]},
  {name:"Back Wall to Left of Window Nook", note:"Wall with the outlet", m:[["Wall width","70"],["Left of outlet","41","wide"],["Right of outlet","26","wide"]]},
  {name:"Left Wall", dims:{"Outlet to outlet":"width"}, m:[["Doorstop to corner","114","wide"],["Height","~94"],["Outlet to outlet","~80"]]},
  {name:"Door Wall", m:[["Door molding to door molding","60","wide"],["Switch to switch","50","wide"],["Floor to bottom of switch","41.5"]]}
 ]},
 {room:"Bedroom 3", view:"From the door entry", spaces:[
  {name:"Right Wall", m:[["Width to door molding","77"]]},
  {name:"Right Window Wall", dims:{"Corner to window (left)":"width"}, m:[["Wall width","90"],["Corner to window ledge (left)","36","wide"],["Corner to window (left)","37.75"],["Floor to window sill","23.5"],["Window to corner (right)","18.5","wide"],["Window ledge to corner (right)","16.75","wide"],["Wall depth to left of window nook","24.75"]]},
  {name:"Front Wall", m:[["Doorstop to corner","80","wide"],["Doorstop to outlet","~53","wide"],["Right outlet to corner","23","wide"],["Front-wall nook depth (right of right outlet)","~36.5"]]},
  {name:"Left Wall", note:"Wall with the closet doors", warn:"The closet door hits this wall when opened.", m:[["Outlet to molding","17.5","wide"]]}
 ]},
 {room:"Master Bedroom", view:"From the door entry", spaces:[
  {name:"Right Wall with Two Windows", dims:{"Window molding to window molding":"width"}, m:[["Window molding to window molding","78.5"],["Farthest right corner to farthest edge of doorway molding","133","wide"],["Big window wall to right-side entrance outlets (rug planning)","178","wide"],["Window, molding to molding","42","wide"],["Floor to window sill","23.75"]]},
  {name:"Door Entry Wall", note:"Wall containing the entry door and sliding bathroom door", m:[["Bathroom-door molding to left corner","41.5","wide"],["Between bathroom door and bedroom door, molding to molding","32","wide"],["Floor to light switch","41.25"]]},
  {name:"Left Wall", note:"From the entrance door", m:[["Doorstop to corner","~141","wide"]]},
  {name:"Back Wall with Tall Window", m:[["Left of window: molding to corner","44.5","wide"],["Window, outer molding to outer molding","66","wide"],["Window sill / window-only width","~57.5"],["Right of window: outer molding to corner","45","wide"]]},
  {group:"Bed + Walkways", name:"Foot of Bed to TV Wall", checkLabel:{depth:"TV console depth"}, checkIntro:"Type the depth of a TV console you’re looking at to see how much room is left to walk between the console and the end of the bed.", dims:{"End of bed to TV wall":"depth"}, walk:{"End of bed to TV wall":true}, m:[["End of bed to TV wall","74.5"]]},
  {group:"Bed + Walkways", name:"Mitch’s Side Walkway", m:[["Bed to big window walkway","52","wide"]]},
  {group:"Bed + Walkways", name:"Bed", checkOnly:[], m:[["Bed width","~72"],["Bed length","~75"]]}
 ]},
 {room:"Master Bathroom", spaces:[
  {group:"Vanity", name:"Big Cabinet Under Amanda’s Sink", dims:{"Left to plumbing":"width","Plumbing to right":"width"}, m:[["Depth","19"],["Left to plumbing","13"],["Plumbing to right","10"],["Door to plumbing depth","9"]]},
  {group:"Vanity", name:"Mirror Area", m:[["Mirror to mirror","37.5","wide"],["Black back/top to top of mirror","41.5","tall"],["Counter flat to top of mirror","45","tall"]]},
  {group:"Vanity", name:"Mitch’s Sink Side", m:[["Wall to right of Mitch’s sink","26","wide"],["Black to black","23","wide"]]},
  {group:"Vanity", name:"Amanda’s Sink Side", m:[["Wall to left of Amanda’s sink","24.25","wide"],["Black to black","23","wide"],["Wall left of Amanda’s sink (additional measurement)","24.5","wide"]]},
  {group:"Vanity", name:"Counter", m:[["Entire counter width","~97"],["Counter depth","~21.5"],["Outlet to switch","11","wide"]]},
  {group:"Vanity", name:"Sink / Mirror Spacing", dims:{"Right of Amanda’s sink to edge of mirror":"width","Left of sink to edge of mirror":"width"}, m:[["Depth to the left of Amanda’s sink","6.5"],["Sink to mirror","5","deep"],["Right of Amanda’s sink to edge of mirror","7"],["Left of sink to edge of mirror","7",null,"Original note says “left of kitchen sink.” Sink not specified."]]},
  {name:"Toilet Room", m:[["Behind toilet","36","wide"],["Toilet height","~28"],["Wall to right of toilet (measured sitting on toilet)","71","wide"]]},
  {group:"Bathtub Area", name:"Bathtub", note:"Viewpoint: looking straight at the bathtub", m:[["Wall to the left of the bathtub","41.5","wide"],["Wall to beginning of tub, left side","17","wide"],["Widest part of tub","32","wide"],["Floor of tub","~47","long"],["Floor of tub","~18.5","wide"],["Right side of tub to wall","~16","wide"],["Wall to far-right side of tub","~41","wide"],["Wall height","~119"],["Farthest outer side of tub to total edge of wall","~8","deep"]]},
  {group:"Bathtub Area", name:"Tub Window", m:[["Window sill","~59","wide"],["Space on either side of window","~20","wide each"]]},
  {group:"Bathtub Area", name:"Rug in Front of Tub", note:"A 60 inch wide runner rug would be pretty good for in front of the tub. Preferably no more than 24 inches wide.", m:[["Runner rug","60","wide"],["Preferably no more than","24","wide"]]},
  {group:"Shower Area", name:"Shower Ledge", m:[["Width","47"],["Depth","12"],["Top of ledge to ceiling","~95"]]},
  {group:"Shower Area", name:"Rug in Front of Shower", m:[["Absolute maximum width","43"],["Preferred width","42.5"],["Maximum depth","~23.5"]]}
 ]},
 {room:"Master Closet", spaces:[
  {name:"Shoe Cabinets", m:[["Height","~80"],["Cabinet width","19.5"]]},
  {name:"Mirrors", m:[["Amanda’s side: ideal height","~74"],["Amanda’s side: maximum width","~21"],["Mitch’s side","Same size (noted as perfect)"]]},
  {name:"Standard Cubbies", m:[["Depth","~14.5"],["Usable width inside cubby","~16.5"],["Usable height inside cubby","~14.5"]]},
  {name:"Bottom Three Cubbies", m:[["Usable width","~16"],["Depth","~15.5"],["Height","~12.25"]]},
  {name:"Val’s Seating Area", m:[["Width","~24.5"],["Depth","~15.25"],["Small ledge depth","~4.5"],["Small ledge width","~22.5"],["Walls on each side, depth","16"],["Top of cubby to bottom of highest window","~27.5","tall"]]},
  {name:"Wall Beside Amanda’s Blazers", m:[["Depth of the small side wall","~16"]]},
  {name:"Wall Beside Mitch’s Shirts", note:"Facing the closet window: the small wall to the left of the door on Mitch’s-shirt side", m:[["Width","~24.5"]]},
  {name:"Closet Rugs", m:[["Amanda’s side","~40 × 18","width × depth"],["Mitch’s side","~40 × 18","width × depth"]]}
 ]}
];

// ---------- search helpers ----------
const SYN={wishlist:"item",shop:"buy",shopping:"buy",purchase:"buy",bath:"bathroom",tub:"bathtub",primary:"master",main:"master",bdrm:"bedroom",foyer:"entry",entryway:"entry",entrance:"entry",sofa:"couch",television:"tv",rail:"railing"};
function stem(w){ if(w.length>4&&w.endsWith("ies")) return w.slice(0,-3)+"y"; if(w.length>4&&/(ches|shes|xes)$/.test(w)) return w.slice(0,-2); if(w.length>3&&w.endsWith("s")&&!w.endsWith("ss")) return w.slice(0,-1); return w; }
function norm(t){ return String(t??"").toLowerCase().replace(/[’']/g,"").split(/[^a-z0-9.]+/).filter(Boolean).map(stem); }
const slug=s=>s.toLowerCase().replace(/[’']/g,"").replace(/[^a-z0-9]+/g,"-").replace(/^-|-$/g,"");
const $=s=>document.querySelector(s);
const esc=s=>String(s??"").replace(/[&<>"]/g,c=>({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;"}[c]));
const ROOMS=H.map(r=>r.room);
const ls={get(k){try{return localStorage.getItem(k)}catch(_){return null}},set(k,v){try{localStorage.setItem(k,v)}catch(_){}}};
const CHEV='<svg class="chev" viewBox="0 0 8 13" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="m1.5 1.5 5 5-5 5"/></svg>';
const BACK='<svg viewBox="0 0 11 19" fill="none" stroke="currentColor" stroke-width="2.6" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M9 2 2 9.5 9 17"/></svg>';
const BAG='<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M5 8h14l-1.2 12H6.2z"/><path d="M9 8V6a3 3 0 0 1 6 0v2"/></svg>';
const CHECK='<svg viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="m3.5 8.5 3 3 6-7"/></svg>';
const LINKIC='<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><path d="M10 14a4.5 4.5 0 0 0 6.4 0l3-3a4.5 4.5 0 0 0-6.4-6.4l-1.2 1.2"/><path d="M14 10a4.5 4.5 0 0 0-6.4 0l-3 3a4.5 4.5 0 0 0 6.4 6.4l1.2-1.2"/></svg>';

// ---------- state ----------
let tab=ls.get("hm-tab")==="bought"?"bought":"spaces", room="All", q="", unit=ls.get("hm-unit")==="cm"?"cm":"in", counts={}, bought={}, firstPhoto={}, saves=[], customs=[], SP=[];
let db=null, assets=null, canWrite=false, storeReady=false;
let recents=[]; try{recents=JSON.parse(ls.get("hm-recent")||"[]").slice(0,6)}catch(_){}

// Every room starts with a space for things to buy that don't depend on a measurement.
H.forEach(r=>r.spaces.unshift({name:"Items to Buy",shop:true,m:[]}));
H.forEach(r=>r.spaces.forEach(s=>{ s.room=r.room; s.view=r.view; s.id=slug(r.room+"-"+(s.group?s.group+"-":"")+s.name).slice(0,180); }));
function rebuild(){
  const added=customs.filter(c=>c.kind==="measure");
  SP=[];
  H.forEach(r=>{
    const extra=customs.filter(c=>c.kind==="space"&&c.room===r.room).map(c=>({id:"c-"+c.id,docId:c.id,custom:true,room:r.room,view:r.view,name:c.name||"Untitled space",note:c.note||"",m:[]}));
    [...r.spaces,...extra].forEach(s=>{
      const sp={...s,m:[...(s.custom?[]:s.m)]};
      added.filter(a=>a.space===sp.id).forEach(a=>sp.m.push([a.label||"Measurement",(a.approx?"~":"")+(a.value??""),null,null,a.id]));
      sp.title=" "+norm([sp.room,sp.group,sp.name].filter(Boolean).join(" ")).join(" ");
      sp.hay=" "+norm([sp.room,sp.group,sp.name,sp.note,sp.view,sp.warn,...sp.m.map(x=>x[0])].filter(Boolean).join(" ")).join(" ");
      SP.push(sp);
    });
  });
  setTimeout(tryPending,0);
}
rebuild();

// ---------- formatting ----------
const r1=n=>String(+n.toFixed(1));
function conv(n){ return unit==="cm"?r1(n*2.54):String(+n.toFixed(3)); }
const U=()=>unit==="cm"?" cm":"″";
function ftIn(n){ if(unit==="cm"||!(n>=36)) return ""; const f=Math.floor(n/12), i=+(n-f*12).toFixed(2); return `${f}′ ${i}″`; }
// Parse a stored value: {approx, nums:[...]} or null for text.
function pv(v){ if(v==null||v==="") return null; const approx=v.startsWith("~"); const raw=approx?v.slice(1):v;
  const m=raw.match(/^(\d+(?:\.\d+)?)(?: × (\d+(?:\.\d+)?))?$/); if(!m) return {text:raw}; return {approx,nums:m[2]?[+m[1],+m[2]]:[+m[1]]}; }
function fmt(v){ const p=pv(v); if(!p) return {html:"Not entered",na:true,plain:"Not entered"}; if(p.text) return {html:esc(p.text),na:true,plain:p.text};
  const s=p.nums.map(conv).join(" × ")+U(); const plain=(p.approx?"about ":"")+s;
  return {html:`${p.approx?'<span class="approx" title="approximate">≈</span>':""}${s}`,ft:p.nums.length===1?ftIn(p.nums[0]):"",plain,single:p.nums.length===1?p.nums[0]:null}; }
function parseVal(t){
  let s=String(t).trim().toLowerCase().replace(/["”″]|inches|inch|in\b/g,"").trim();
  const num=p=>{ p=p.trim(); let m=p.match(/^(\d+)\s+(\d+)\/(\d+)$/); if(m) return +m[1]+ +m[2]/+m[3]; m=p.match(/^(\d+)\/(\d+)$/); if(m) return +m[1]/+m[2]; return /^\d+(\.\d+)?$/.test(p)?+p:NaN; };
  const r=n=>String(+n.toFixed(3));
  const parts=s.split(/\s*[x×]\s*/);
  if(parts.length===2&&!isNaN(num(parts[0]))&&!isNaN(num(parts[1]))) return r(num(parts[0]))+" × "+r(num(parts[1]));
  if(parts.length===1&&!isNaN(num(s))) return r(num(s));
  return String(t).trim();
}
function hl(text){
  const ws=q.toLowerCase().replace(/[’']/g,"").split(/[^a-z0-9.]+/).filter(w=>w.length>1).flatMap(w=>{const s=stem(w);return [w,s,s.replace(/y$/,"i")];}).map(w=>w.replace(/[.*+?^${}()|[\]\\]/g,"\\$&")).sort((a,b)=>b.length-a.length);
  if(!ws.length) return esc(text);
  const parts=String(text).split(new RegExp("("+ws.join("|")+")","ig"));
  return parts.map((p,i)=>i%2?"<mark>"+esc(p)+"</mark>":esc(p)).join("");
}
function matches(s,words,f){ return words.every(w=>s[f].includes(" "+w)||(SYN[w]&&s[f].includes(" "+SYN[w]))); }
function search(pool,words){ if(!words.length) return pool; const t=pool.filter(s=>matches(s,words,"title")); return t.length?t:pool.filter(s=>matches(s,words,"hay")); }

// ---------- toast ----------
let toastT=null;
function toast(msg,undo,ms){
  clearTimeout(toastT); const host=$("#toastHost");
  host.innerHTML=`<div class="toast" role="status"><span>${esc(msg)}</span>${undo?'<button id="undo">Undo</button>':""}</div>`;
  let done=false; const finish=()=>{ if(!done){done=true; host.innerHTML="";} };
  if(undo) $("#undo").onclick=()=>{ done=true; host.innerHTML=""; clearTimeout(toastT); undo(); };
  toastT=setTimeout(finish,ms||(undo?5000:1800));
  return ()=>done;
}

// ---------- header ----------
function units(){ $("#uIn").setAttribute("aria-pressed",unit==="in"); $("#uCm").setAttribute("aria-pressed",unit==="cm"); }
$("#uIn").onclick=()=>{unit="in";ls.set("hm-unit",unit);units();render();refreshView();};
$("#uCm").onclick=()=>{unit="cm";ls.set("hm-unit",unit);units();render();refreshView();};
addEventListener("scroll",()=>$("#top").classList.toggle("compact",scrollY>24),{passive:true});
function chips(){
  $("#chips").innerHTML=["All",...ROOMS,"Saved"].map(r=>`<button class="chip" aria-pressed="${r===room}" data-r="${esc(r)}">${esc(r==="Saved"?"Has saved finds":r)}</button>`).join("");
}
$("#chips").addEventListener("click",e=>{const b=e.target.closest(".chip"); if(!b) return; room=b.dataset.r; ls.set("hm-room",room); chips(); render(); window.scrollTo({top:0});});

function tabs(){ $("#tSpaces").setAttribute("aria-selected",tab==="spaces"); $("#tBought").setAttribute("aria-selected",tab==="bought");
  const n=saves.filter(x=>x.purchased).length; $("#boughtN").textContent=n?`(${n})`:""; }
$("#tSpaces").onclick=()=>{tab="spaces";ls.set("hm-tab",tab);tabs();render();window.scrollTo({top:0});};
$("#tBought").onclick=()=>{tab="bought";ls.set("hm-tab",tab);tabs();render();window.scrollTo({top:0});};

// ---------- saved item row (shared by a space and the Purchased tab) ----------
function spaceTitle(id){ const s=SP.find(x=>x.id===id); return s?(s.group?s.group+" · ":"")+s.name:"Deleted space"; }
function saveRow(x,inBought){
  const pic=x.asset?`<button class="pic" data-view="${esc(x.asset)}" aria-label="View photo"><img src="${esc(blobUrl(x.asset))}" alt="Saved photo" loading="lazy"></button>`:`<div class="pic linkic">${LINKIC}</div>`;
  let host=""; if(x.url){try{host=new URL(x.url).hostname.replace(/^www\./,"")}catch(_){host=x.url}}
  const day=t=>t?new Date(t).toLocaleDateString(undefined,{month:"short",day:"numeric"}):"";
  const safe=x.url&&/^https?:/i.test(x.url);
  const buy=`<button class="buy" role="checkbox" aria-checked="${!!x.purchased}" aria-label="Purchased" data-buy="${esc(x.id)}" ${canWrite?"":"disabled"}>${CHECK}</button>`;
  const meta=inBought
    ? `<button class="where" data-open="${esc(x.space)}">${esc(spaceTitle(x.space))}</button><div class="d"><span class="tag">Purchased</span>${x.purchasedAt?" "+day(x.purchasedAt):""}</div>`
    : `<div class="d">${x.purchased?`<span class="tag">Purchased</span>${x.purchasedAt?" "+day(x.purchasedAt):""} · `:""}${x.asset?"Photo":"Link"} · saved ${day(x.created)}</div>`;
  return `<div class="save${x.purchased?" isbought":""}">${buy}${pic}<div class="info">${x.url?(safe?`<a href="${esc(x.url)}" target="_blank" rel="noopener">${esc(host)}</a>`:`<div class="n">${esc(x.url)}</div>`):""}${x.note?`<div class="n">${esc(x.note)}</div>`:""}${meta}</div>${canWrite&&!inBought?`<div class="acts"><button class="link" data-edits="${esc(x.id)}">Edit</button><button class="link danger" data-del="${esc(x.id)}">Delete</button></div>`:""}</div>`;
}
// Checkmarks, photo viewer and "go to space" work the same everywhere.
document.addEventListener("click",async e=>{
  const b=e.target.closest("[data-buy]");
  if(b&&canWrite&&db){ const x=saves.find(s=>s.id===b.dataset.buy); if(!x) return; const now=!x.purchased;
    b.setAttribute("aria-checked",now); b.disabled=true;
    try{ await db.collection("saves").doc(x.id).update({purchased:now,purchasedAt:now?Date.now():null}); toast(now?"Marked purchased":"Marked not purchased"); }
    catch(err){ b.setAttribute("aria-checked",!now); denied(err); toast("Couldn’t update. Try again."); }
    finally{ b.disabled=!canWrite; } return; }
  const v=e.target.closest("[data-view]");
  if(v){ const el=document.createElement("div"); el.className="viewer"; el.innerHTML=`<img src="${esc(blobUrl(v.dataset.view))}" alt="Saved photo">`; el.onclick=()=>el.remove(); document.body.appendChild(el); return; }
  const o=e.target.closest("[data-open]");
  if(o&&SP.some(s=>s.id===o.dataset.open)) openView(o.dataset.open);
});
function renderBought(){
  const words=norm(q);
  const items=saves.filter(x=>x.purchased).map(x=>({x,s:SP.find(s=>s.id===x.space)}))
    .filter(({x,s})=>room==="All"||room==="Saved"||s?.room===room)
    .filter(({x,s})=>{ if(!words.length) return true; const hay=" "+norm([s?.room,s?.group,s?.name,x.note,x.url].filter(Boolean).join(" ")).join(" "); return words.every(w=>hay.includes(" "+w)||(SYN[w]&&hay.includes(" "+SYN[w]))); })
    .sort((a,b)=>(b.x.purchasedAt||0)-(a.x.purchasedAt||0));
  let html="";
  [...ROOMS,null].forEach(rn=>{
    const list=items.filter(({s})=>rn?s?.room===rn:!s); if(!list.length) return;
    html+=`<section><div class="sechead">${esc(rn||"Other")}<span>${list.length} purchased</span></div><div class="group">${list.map(({x})=>saveRow(x,true)).join("")}</div></section>`;
  });
  if(!html) html=q?`<div class="empty"><b>No purchased items match “${esc(q)}”</b></div>`:`<div class="empty"><b>No purchased items yet</b>Tap the circle next to a saved link or photo to mark it purchased.</div>`;
  $("#out").innerHTML=html;
  $("#out").querySelectorAll(".pic img").forEach(img=>img.addEventListener("error",()=>{img.replaceWith(document.createTextNode("Missing"));}));
}

// ---------- list ----------
function rowHtml(s){
  if(s.shop){ const c=counts[s.id]||0;
    return `<button class="row shop" data-id="${esc(s.id)}"><span class="shopic">${BAG}</span><span class="body"><span class="ttl">${hl(s.name)}</span><span class="sub">${c?`${c} saved ${c===1?"item":"items"}${bought[s.id]?` · ${bought[s.id]} purchased`:""}`:`Links and photos for this room`}</span></span>${c?`<span class="badge" aria-label="${c} saved">${c}</span>`:""}${CHEV}</button>`; }
  const peek=s.m.slice(0,3).map(([l,v,suf])=>{const f=fmt(v);return `${hl(l)} <b>${f.html}</b>${suf?" "+esc(suf):""}`}).join(" · ")||"No measurements yet";
  const ph=firstPhoto[s.id];
  return `<button class="row${ph?" hasthumb":""}" data-id="${esc(s.id)}">${ph?`<img class="thumb" src="${esc(blobUrl(ph))}" alt="" loading="lazy">`:""}<span class="body">${s.group?`<span class="grp">${hl(s.group)}</span>`:""}<span class="ttl">${hl(s.name)}</span><span class="sub num">${peek}</span></span>${counts[s.id]?`<span class="badge" aria-label="${counts[s.id]} saved">${counts[s.id]}</span>`:""}${CHEV}</button>`;
}
function render(){
  tabs();
  if(tab==="bought") return renderBought();
  const words=norm(q);
  const list=search(SP.filter(s=>room==="All"||room===s.room||(room==="Saved"&&counts[s.id])),words);
  const showAdd=canWrite&&!q&&room!=="Saved";
  let html="";
  const rec=!q&&room==="All"?recents.map(id=>SP.find(s=>s.id===id)).filter(Boolean).slice(0,3):[];
  if(rec.length) html+=`<section><div class="sechead small">Recently Viewed</div><div class="group recents">${rec.map(rowHtml).join("")}</div></section>`;
  const rooms=room==="All"||room==="Saved"?ROOMS:[room];
  rooms.forEach(rn=>{
    const items=list.filter(s=>s.room===rn);
    if(!items.length&&!(showAdd&&room===rn)) return;
    const view=H.find(h=>h.room===rn).view;
    html+=`<section><div class="sechead">${esc(rn)}${view&&!q?`<span>Viewpoint: ${esc(view)}</span>`:""}</div><div class="group">${items.map(rowHtml).join("")}${showAdd?`<button class="row add" data-addspace="${esc(rn)}">Add Space</button>`:""}</div></section>`;
  });
  if(!list.length&&!showAdd) html=room==="Saved"&&!q?`<div class="empty"><b>No saved finds yet</b>Open a space and save a link or photo.</div>`:`<div class="empty"><b>No results for “${esc(q)}”</b>Try a room or object, like closet, window or rug.</div>`;
  if(!q&&room==="All"&&started) html+=backupHtml();
  $("#out").innerHTML=html;
  $("#out").querySelectorAll(".thumb").forEach(i=>i.addEventListener("error",()=>i.remove()));
}
$("#out").addEventListener("click",e=>{
  const c=e.target.closest(".row[data-id]"); if(c) return openView(c.dataset.id);
  const a=e.target.closest("[data-addspace]"); if(a) openSpaceForm(a.dataset.addspace);
});
function onSearch(){ const v=$("#q").value.trim(); if(v===q) return; q=v; $("#clear").hidden=!q;
  if(q&&room!=="All"){ room="All"; chips(); }
  render(); }
["input","keyup","search","change","compositionend"].forEach(ev=>$("#q").addEventListener(ev,onSearch));
$("#q").addEventListener("keydown",e=>{ if(e.key==="Enter"){ e.preventDefault(); onSearch(); $("#q").blur(); }});
$("#clear").onclick=()=>{$("#q").value="";onSearch();$("#q").focus();};

// ---------- storage ----------
// ---------- shared storage (your private GitHub repository) ----------
// Links, photos, checkmarks and added measurements are saved in a private GitHub repository you own:
// data.json holds the items and photos/ holds the pictures. Each phone connects once with the
// repository name and an access key, which stay on that phone.
const mem={saves:{},custom:{}}; const listeners={saves:[],custom:[]}; const URLS={}; const loadingPhoto={};
let GH=null, started=false, dataEtag=null, pollT=null;
try{ GH=JSON.parse(localStorage.getItem("hm-gh")||"null"); }catch(_){}
const clone=o=>JSON.parse(JSON.stringify(o));
const newId=n=>{ const a=new Uint8Array(n||10); crypto.getRandomValues(a); return [...a].map(b=>b.toString(16).padStart(2,"0")).join(""); };
function b64FromBytes(u8){ let s=""; for(let i=0;i<u8.length;i+=0x8000) s+=String.fromCharCode.apply(null,u8.subarray(i,i+0x8000)); return btoa(s); }
const b64FromText=t=>b64FromBytes(new TextEncoder().encode(t));
const textFromB64=b=>new TextDecoder().decode(Uint8Array.from(atob(String(b).replace(/\s/g,"")),c=>c.charCodeAt(0)));
async function gh(path,opts={}){
  const r=await fetch(`https://api.github.com/repos/${GH.repo}${path}`,{...opts,cache:"no-store",headers:{"Authorization":`Bearer ${GH.token}`,"Accept":"application/vnd.github+json",...(opts.body?{"Content-Type":"application/json"}:{}),...(opts.headers||{})}});
  return r;
}
function blobUrl(id){ if(!URLS[id]&&id) loadPhoto(id); return URLS[id]||"data:,"; }
async function loadPhoto(id){
  if(loadingPhoto[id]||!GH) return; loadingPhoto[id]=true;
  try{
    let blob=null, cache=null;
    try{ cache=await caches.open("hm-photos"); const hit=await cache.match("/photo/"+id); if(hit) blob=await hit.blob(); }catch(_){}
    if(!blob){ const r=await gh(`/contents/photos/${id}.jpg`,{headers:{"Accept":"application/vnd.github.raw"}}); if(!r.ok) return; blob=await r.blob();
      try{ await cache?.put("/photo/"+id,new Response(blob,{headers:{"Content-Type":"image/jpeg"}})); }catch(_){} }
    URLS[id]=URL.createObjectURL(blob); render(); refreshView("saves");
  }finally{ loadingPhoto[id]=false; }
}
function emit(c){ listeners[c].forEach(({fn,dir})=>{ const docs=Object.entries(mem[c]).sort((a,b)=>((a[1].created||0)-(b[1].created||0))*(dir==="desc"?-1:1)).map(([id,d])=>({id,exists:true,data:()=>d})); fn({docs}); }); }
function cacheSave(){ try{ localStorage.setItem("hm-cache",JSON.stringify(mem)); }catch(_){} }
function cacheLoad(){ try{ const c=JSON.parse(localStorage.getItem("hm-cache")||"null"); if(c){ mem.saves=c.saves||{}; mem.custom=c.custom||{}; } }catch(_){} }
// Read data.json. Returns {sha, data} or null when nothing has changed since the last read.
async function readData(force){
  const r=await gh("/contents/data.json",{headers:(!force&&dataEtag)?{"If-None-Match":dataEtag}:{}});
  if(r.status===304) return null;
  if(r.status===404) return {sha:null,data:{saves:{},custom:{}}};
  if(!r.ok) throw {code:"load_failed",status:r.status};
  dataEtag=r.headers.get("ETag");
  const j=await r.json(); let text;
  if(j.content) text=textFromB64(j.content);
  else { const b=await gh(`/git/blobs/${j.sha}`); text=textFromB64((await b.json()).content); }
  const data=JSON.parse(text||"{}"); data.saves=data.saves||{}; data.custom=data.custom||{};
  return {sha:j.sha,data};
}
function applyData(data){ mem.saves=data.saves; mem.custom=data.custom; cacheSave(); emit("saves"); emit("custom"); }
// Apply one change on top of the latest saved copy, so two phones saving at once don't overwrite each other.
async function writeOp(op,message){
  for(let i=0;i<5;i++){
    const cur=await readData(true); op(cur.data);
    const r=await gh("/contents/data.json",{method:"PUT",body:JSON.stringify({message,content:b64FromText(JSON.stringify(cur.data,null,1)),...(cur.sha?{sha:cur.sha}:{})})});
    if(r.ok){ dataEtag=null; applyData(cur.data); return; }
    if(r.status!==409&&r.status!==422) throw {code:"save_failed",status:r.status};
    await new Promise(res=>setTimeout(res,300+Math.random()*500));
  }
  throw {code:"save_failed"};
}
async function guarded(c,optimistic,op,message){
  optimistic(); emit(c);
  try{ await writeOp(op,message); }catch(e){ try{ const cur=await readData(true); applyData(cur.data); }catch(_){} throw e; }
}
const ghDb={collection:c=>({
  orderBy:(f,dir)=>({onSnapshot:fn=>{ const l={fn,dir}; listeners[c].push(l); setTimeout(()=>emit(c),0); return ()=>{listeners[c]=listeners[c].filter(x=>x!==l)}; }}),
  add:async d=>{ const id=newId(); const v=clone(d); await guarded(c,()=>{mem[c][id]=v;},data=>{data[c][id]=v;},"Add item"); return {id}; },
  doc:id=>({
    set:async d=>{ const v=clone(d); await guarded(c,()=>{mem[c][id]=v;},data=>{data[c][id]=v;},"Save item"); },
    update:async p=>{ if(!mem[c][id]) throw {code:"invalid_argument"}; const v=clone(p);
      await guarded(c,()=>{Object.assign(mem[c][id],v);},data=>{ if(data[c][id]) Object.assign(data[c][id],v); },"Update item"); },
    delete:async()=>{ await guarded(c,()=>{delete mem[c][id];},data=>{delete data[c][id];},"Delete item"); }
  })
})};
const ghAssets={
  upload:async blob=>{ const id=newId(16);
    const r=await gh(`/contents/photos/${id}.jpg`,{method:"PUT",body:JSON.stringify({message:"Add photo",content:b64FromBytes(new Uint8Array(await blob.arrayBuffer()))})});
    if(!r.ok) throw {code:"upload_failed",status:r.status};
    URLS[id]=URL.createObjectURL(blob); return {id,url:URLS[id]}; },
  delete:async id=>{ const r=await gh(`/contents/photos/${id}.jpg`); if(r.ok){ const j=await r.json(); await gh(`/contents/photos/${id}.jpg`,{method:"DELETE",body:JSON.stringify({message:"Delete photo",sha:j.sha})}); }
    try{ (await caches.open("hm-photos")).delete("/photo/"+id); }catch(_){} delete URLS[id]; return {deleted:true}; }
};
async function loadAll(){
  try{ const cur=await readData(false); if(cur) applyData(cur.data); }
  catch(e){ if(e?.status===401) return showGate("connect","This phone’s access key no longer works. It may have expired. Paste a new one."); toast("Couldn’t load the latest. Check your connection."); }
}
function startData(){
  if(started) return; started=true;
  db=ghDb; assets=ghAssets; canWrite=true;
  db.collection("saves").orderBy("created","desc").onSnapshot(snap=>{
    saves=snap.docs.map(d=>({id:d.id,...d.data()}));
    counts={}; bought={}; firstPhoto={};
    saves.forEach(s=>{counts[s.space]=(counts[s.space]||0)+1; if(s.purchased) bought[s.space]=(bought[s.space]||0)+1; if(s.asset&&!firstPhoto[s.space]) firstPhoto[s.space]=s.asset;});
    storeReady=true; render(); refreshView("saves");
  });
  db.collection("custom").orderBy("created","asc").onSnapshot(snap=>{
    customs=snap.docs.map(d=>({id:d.id,...d.data()}));
    rebuild(); render(); refreshView("meas");
  });
  loadAll();
  // Pick up what the other phone added: when the app is opened and every 20 seconds while it's open.
  document.addEventListener("visibilitychange",()=>{ if(document.visibilityState==="visible") loadAll(); });
  pollT=setInterval(()=>{ if(document.visibilityState==="visible") loadAll(); },20000);
  render(); refreshView();
}
async function initStore(){
  if(GH?.repo&&GH?.token){ cacheLoad(); hideGate(); startData(); } else showGate("connect");
}

// ---------- connect this phone ----------
function hideGate(){ $("#gate")?.remove(); }
function showGate(mode,msg){
  hideGate();
  const g=document.createElement("div"); g.id="gate"; g.className="gate";
  g.innerHTML=`<form class="gatebox" id="gForm"><h2>Home Measurements</h2>
    <p>${esc(msg||"Connect this phone to your private GitHub repository where your links and photos are saved. You only do this once on each phone.")}</p>
    <input id="gRepo" type="text" autocomplete="off" autocapitalize="off" spellcheck="false" placeholder="yourname/home-measurements-data" aria-label="Data repository" value="${esc(GH?.repo||"")}" required>
    <input id="gTok" type="password" autocomplete="off" placeholder="Access key (starts with github_pat_)" aria-label="Access key" required>
    <button class="btn primary" type="submit" id="gGo">Connect</button>
    <div class="status" id="gSt"></div></form>`;
  document.body.appendChild(g);
  const st=(m,err)=>{ const e=$("#gSt"); e.textContent=m; e.className="status"+(err?" err":""); };
  $("#gForm").addEventListener("submit",async e=>{ e.preventDefault();
    let repo=$("#gRepo").value.trim().replace(/^https?:\/\/github\.com\//i,"").replace(/\.git$/,"").replace(/\/+$/,"");
    const token=$("#gTok").value.trim();
    if(!/^[\w.-]+\/[\w.-]+$/.test(repo)){ st("Type the repository as your-github-name/repository-name.",1); return; }
    st("Connecting…"); $("#gGo").disabled=true;
    const prev=GH; GH={repo,token};
    try{
      const r=await gh("");
      if(r.status===401) throw "That access key didn’t work. Copy it again from GitHub.";
      if(r.status===404) throw "Couldn’t find that repository with this key. Check the name, and that the key was given access to it.";
      if(!r.ok) throw "GitHub didn’t answer. Check your connection and try again.";
      const j=await r.json();
      if(j.permissions&&!j.permissions.push) throw "This key can read the repository but can’t save to it. Give it Contents: Read and write.";
      try{ localStorage.setItem("hm-gh",JSON.stringify(GH)); }catch(_){}
      if(started) location.reload(); else { cacheLoad(); hideGate(); startData(); }
    }catch(m){ GH=prev; $("#gGo").disabled=false; st(typeof m==="string"?m:"Couldn’t connect. Check your connection and try again.",1); }
  });
}
function disconnect(){ try{ localStorage.removeItem("hm-gh"); localStorage.removeItem("hm-cache"); }catch(_){} location.reload(); }

// ---------- backup and restore ----------
const blobToDataURL=b=>new Promise((res,rej)=>{ const r=new FileReader(); r.onload=()=>res(r.result); r.onerror=()=>rej(r.error); r.readAsDataURL(b); });
async function exportBackup(){
  try{
    toast("Preparing backup…");
    const photos={};
    for(const s of Object.values(mem.saves)) if(s.asset&&!photos[s.asset]){
      try{ if(!URLS[s.asset]) await loadPhoto(s.asset); if(URLS[s.asset]) photos[s.asset]=await blobToDataURL(await (await fetch(URLS[s.asset])).blob()); }catch(_){} }
    const data={app:"home-measurements",version:1,exported:new Date().toISOString(),saves:mem.saves,custom:mem.custom,photos};
    const name=`home-measurements-backup-${new Date().toISOString().slice(0,10)}.json`;
    const file=new File([JSON.stringify(data)],name,{type:"application/json"});
    if(navigator.canShare&&navigator.canShare({files:[file]})){
      try{ await navigator.share({files:[file],title:"Home Measurements backup"}); ls.set("hm-backup",Date.now()); render(); return; }catch(e){ if(e?.name==="AbortError") return; }
    }
    const a=document.createElement("a"); a.href=URL.createObjectURL(file); a.download=name; document.body.appendChild(a); a.click(); a.remove();
    setTimeout(()=>URL.revokeObjectURL(a.href),5000);
    ls.set("hm-backup",Date.now()); render(); toast("Backup saved");
  }catch(_){ toast("Couldn’t make the backup. Try again."); }
}
async function importBackup(file){
  let data; try{ data=JSON.parse(await file.text()); if(data?.app!=="home-measurements"||typeof data.saves!=="object") throw 0; }
  catch(_){ toast("That file isn’t a Home Measurements backup."); return; }
  try{
    toast("Restoring…");
    for(const [id,u] of Object.entries(data.photos||{})){
      const blob=await (await fetch(u)).blob();
      const ex=await gh(`/contents/photos/${id}.jpg`); const sha=ex.ok?(await ex.json()).sha:null;
      const r=await gh(`/contents/photos/${id}.jpg`,{method:"PUT",body:JSON.stringify({message:"Restore photo",content:b64FromBytes(new Uint8Array(await blob.arrayBuffer())),...(sha?{sha}:{})})});
      if(!r.ok) throw 0; URLS[id]=URL.createObjectURL(blob);
    }
    await writeOp(d=>{ Object.assign(d.saves,data.saves||{}); Object.assign(d.custom,data.custom||{}); },"Restore backup");
    toast(`Restored ${Object.keys(data.saves||{}).length} saved items`);
  }catch(_){ toast("Couldn’t finish restoring. Check your connection and try again."); }
}
function backupHtml(){
  const last=+ls.get("hm-backup"); const when=last?new Date(last).toLocaleDateString(undefined,{month:"short",day:"numeric",year:"numeric"}):"never";
  return `<section><div class="sechead small">Connection and Backup</div><div class="group">
    <div class="save"><div class="info"><div class="n">Saving to ${esc(GH?.repo||"")} on GitHub. Everything added on either phone shows up on both.</div><div class="d">Last backup file: ${when}</div></div></div>
    <input id="bkFile" type="file" accept="application/json,.json" hidden>
    <button class="row add" id="bkSave">Save a Backup File</button>
    <label class="row add" for="bkFile" tabindex="0">Restore from a Backup File</label>
    <button class="row add" id="ghRe">Change Access Key</button>
    <button class="row add" id="ghOut" style="color:var(--bad)">Disconnect This Phone</button>
  </div></section>`;
}
document.addEventListener("click",e=>{
  if(e.target.closest("#bkSave")) exportBackup();
  if(e.target.closest("#ghRe")) showGate("connect","Paste a new access key for this phone.");
  if(e.target.closest("#ghOut")){ const b=e.target.closest("#ghOut"); if(!b.dataset.armed){ b.dataset.armed="1"; b.textContent="Tap again to disconnect. Your items stay saved on GitHub."; return; } disconnect(); }
});
document.addEventListener("change",e=>{ if(e.target.id==="bkFile"&&e.target.files[0]){ const f=e.target.files[0]; e.target.value=""; importBackup(f); } });
document.addEventListener("keydown",e=>{ if((e.key==="Enter"||e.key===" ")&&e.target.matches?.("label[for=bkFile]")){ e.preventDefault(); $("#bkFile").click(); } });
function denied(err){ if(err?.code==="invalid_argument"){ canWrite=false; render(); } }
function errMsg(err){ return err?.code==="quota_exceeded"?"Storage is full. Delete some saved photos first.":"Couldn’t save. Check your connection and try again."; }
function stripId(x){ const {id,...rest}=x; return rest; }

// ---------- detail view ----------
let openId=null, editM=null, editS=null, cmpVal={};
function openView(id){
  openId=id; editM=null; editS=null; cmpVal={};
  recents=[id,...recents.filter(r=>r!==id)].slice(0,6); ls.set("hm-recent",JSON.stringify(recents));
  drawView(); document.body.style.overflow="hidden";
}
function closeView(){ openId=null; editM=null; editS=null; $("#viewHost").innerHTML=""; document.body.style.overflow=""; render(); }
function refreshView(part){
  if(!openId) return;
  if(!$("#view")) return drawView();
  const s=SP.find(x=>x.id===openId); if(!s) return closeView();
  if($("#vh").textContent!==s.name){ $("#vh").textContent=s.name; $(".navtitle").textContent=s.name; }
  if(part!=="saves"&&!editM){ const cb=$("#cmpBox"); if(cb&&!cb.contains(document.activeElement)){ cb.innerHTML=cmpHtml(s); bindCmp(); } drawMeas(); }
  if(part!=="meas"&&!editS) drawSaveList();
  if(!part){ drawAddForm(); drawSpaceActs(); document.querySelectorAll(".cmp .u").forEach(u=>u.textContent=unit); }
}
function drawView(){
  const s=SP.find(x=>x.id===openId); if(!s) return;
  $("#viewHost").innerHTML=`<div class="scrim" id="scrim"><div class="view" id="view" role="dialog" aria-modal="true" aria-labelledby="vh">
    <div class="nav" id="nav"><button class="navbtn" id="x" aria-label="Back to all spaces">${BACK}<span>${esc(s.room)}</span></button><div class="navtitle">${esc(s.name)}</div><div class="navspacer"></div></div>
    <div class="hero"><div class="crumb">${esc(s.room)}${s.group?" · "+esc(s.group):""}</div><h2 id="vh">${esc(s.name)}</h2></div>
    ${s.view&&!s.custom?`<p class="note">Viewpoint: ${esc(s.view)}</p>`:""}${s.note?`<p class="note">${esc(s.note)}</p>`:""}${s.warn?`<p class="warn"><b>Heads up:</b> ${esc(s.warn)}</p>`:""}
    ${s.shop?`<p class="note">Links and photos for anything you want to buy for the ${esc(s.room)}.</p>`:`
    <div id="cmpBox">${cmpHtml(s)}</div>
    <h3 class="sec">Measurements</h3>
    <div id="measBox"></div>
    <p class="foot-note">≈ means approximate. Tap a measurement to copy it.</p>`}
    <h3 class="sec">${s.shop?"Items":"Saved finds"}</h3>
    <div class="group" id="savesGroup"><div id="addBox"></div><div id="saveList"></div></div>
    <div id="spaceActs"></div>
  </div></div>`;
  $("#x").onclick=closeView;
  $("#scrim").addEventListener("click",e=>{if(e.target.id==="scrim") closeView();});
  $("#view").addEventListener("scroll",e=>$("#nav").classList.toggle("scrolled",e.target.scrollTop>60),{passive:true});
  bindCmp();
  drawMeas(); drawAddForm(); drawSaveList(); drawSpaceActs();
  $("#x").focus({preventScroll:true});
}

// measurements
function measForm(a){
  return `<form class="form" id="mForm">
    <div class="pair"><input id="mLabel" type="text" placeholder="What you measured" value="${esc(a?.label??"")}" autocomplete="off" aria-label="What you measured">
    <input id="mVal" type="text" inputmode="decimal" placeholder="Inches" value="${esc(a?String(a.value??""):"")}" autocomplete="off" aria-label="Inches"></div>
    <label class="chk"><input id="mApprox" type="checkbox" ${a?.approx?"checked":""}> Approximate</label>
    <div class="hint">Inches. Type 34.5, 34 1/2, or 40 x 18.</div>
    <div class="btns"><button class="btn primary" type="submit">${a?"Save":"Add"}</button><button class="btn" type="button" id="mCancel">Cancel</button>${a?`<span class="spacer"></span><button class="btn danger" type="button" id="mDel">Delete</button>`:""}</div>
    <div class="status" id="mSt"></div></form>`;
}
function drawMeas(){
  const box=$("#measBox"); const s=SP.find(x=>x.id===openId); if(!box||!s) return;
  const rows=s.m.map(([l,v,suf,sub,cid],i)=>{
    if(cid&&editM===cid) return measForm(customs.find(c=>c.id===cid));
    const f=fmt(v);
    const copy=(f.na?"":f.plain+(suf?" "+suf:""));
    const dm=rowDims(s,l,v,suf,sub);
    return `<div class="m"${Object.keys(dm).length?` data-dims="${esc(JSON.stringify(dm))}" data-label="${esc(l)}"${s.walk?.[l]?' data-walk="1"':""}`:""}><div class="lbl">${esc(l)}${suf?` <span class="suf">· ${esc(suf)}</span>`:""}</div>
      ${f.na?`<div class="na">${f.html}</div>`:`<button class="valbtn" data-copy="${esc(l+": "+copy)}" aria-label="Copy ${esc(l)} ${esc(copy)}"><span class="val">${f.html}</span>${f.ft?`<span class="ft">${f.ft}</span>`:""}</button>`}
      ${sub?`<div class="foot">${esc(sub)}</div>`:""}<div class="fits" hidden></div>
      ${cid&&canWrite?`<div class="mine">Added by you <button class="link" data-editm="${esc(cid)}">Edit</button></div>`:""}</div>`;
  }).join("");
  const empty=!s.m.length&&editM!=="new"?`<div class="m"><div class="lbl" style="color:var(--muted)">No measurements yet.</div></div>`:"";
  box.innerHTML=`<div class="group">${rows}${empty}${editM==="new"?measForm(null):""}${canWrite&&!editM?`<button class="row add" id="mAdd">Add Measurement</button>`:""}</div>`;
  $("#mAdd")?.addEventListener("click",()=>{editM="new";drawMeas();$("#mLabel")?.focus();});
  box.querySelectorAll("[data-editm]").forEach(b=>b.addEventListener("click",()=>{editM=b.dataset.editm;drawMeas();$("#mLabel")?.focus();}));
  box.querySelectorAll("[data-copy]").forEach(b=>b.addEventListener("click",()=>copyText(b.dataset.copy)));
  updateFit();
  const f=$("#mForm"); if(!f) return;
  $("#mCancel").onclick=()=>{editM=null;drawMeas();};
  f.addEventListener("submit",async e=>{e.preventDefault();
    const label=$("#mLabel").value.trim(), raw=$("#mVal").value.trim(), approx=$("#mApprox").checked;
    if(!label||!raw){ mst("Add what you measured and the inches.",1); return; }
    const value=parseVal(raw); const btn=f.querySelector("[type=submit]"); btn.disabled=true; mst("Saving…");
    try{
      if(editM==="new") await db.collection("custom").add({kind:"measure",space:openId,label,value,approx,created:Date.now()});
      else await db.collection("custom").doc(editM).update({label,value,approx});
      editM=null; drawMeas(); toast("Measurement saved");
    }catch(err){ denied(err); btn.disabled=false; mst(errMsg(err),1); }
  });
  $("#mDel")?.addEventListener("click",async e=>{const b=e.currentTarget; const c=customs.find(x=>x.id===editM); if(!c) return;
    b.disabled=true;
    try{ await db.collection("custom").doc(c.id).delete(); editM=null; drawMeas();
      toast("Measurement deleted",()=>db.collection("custom").doc(c.id).set(stripId(c)).catch(()=>toast("Couldn’t restore it")));
    }catch(_){ b.disabled=false; mst("Couldn’t delete. Try again.",1); }
  });
}
function mst(m,err){const e=$("#mSt"); if(e){e.textContent=m; e.className="status"+(err?" err":"");}}
// Which directions a measurement describes, read from its own label and direction word.
const DIMS=["width","depth","height","length"];
const DIMLBL={width:"Width",depth:"Depth",height:"Height",length:"Length"};
function dimTypes(text){
  const t=String(text).toLowerCase(); const out=[];
  if(/width|wide/.test(t)) out.push("width");
  if(/depth|deep/.test(t)) out.push("depth");
  if(/height|tall|floor to|ceiling/.test(t)) out.push("height");
  if(/length|long/.test(t)) out.push("length");
  return out;
}
function dimsOf(label,v,suf,sub,hint){
  const p=pv(v); if(!p||!p.nums) return {};
  if(p.nums.length===2) return /width × depth/.test(suf||"")?{width:p.nums[0],depth:p.nums[1]}:{};
  let types=hint?[hint]:/depth measurement/i.test(sub||"")?["depth"]:dimTypes(label+" "+(suf||""));
  // No direction word in the notes: checked as a width and labeled as assumed.
  if(!types.length) return {width:p.nums[0],assumed:true};
  const o={}; types.forEach(t=>o[t]=p.nums[0]); return o;
}
function bindCmp(){
  document.querySelectorAll(".cmp input").forEach(i=>i.addEventListener("input",e=>{cmpVal[e.target.dataset.dim]=e.target.value; updateFit();}));
  $("#cmpClear")?.addEventListener("click",()=>{cmpVal={}; document.querySelectorAll(".cmp input").forEach(i=>i.value=""); updateFit();});
}
function rowDims(s,l,v,suf,sub){ return s.checkOnly&&!s.checkOnly.includes(l)?{}:dimsOf(l,v,suf,sub,s.dims?.[l]); }
function cmpHtml(s){
  const present=DIMS.filter(d=>s.m.some(([l,v,suf,sub])=>typeof rowDims(s,l,v,suf,sub)[d]==="number"));
  if(!present.length) return "";
  return `<div class="cmp"><div class="head"><div><b>Will it fit?</b><small>${s.checkIntro?esc(s.checkIntro):`Type the ${present.map(d=>DIMLBL[d].toLowerCase()).join(", ").replace(/, ([^,]*)$/," and $1")} of the furniture you’re looking at. Each measurement below will show whether the furniture fits and how much room is left over.`}</small></div><button class="link" id="cmpClear" type="button">Clear</button></div>
    <div class="dims">${present.map(d=>`<div class="dim"><label for="cmp-${d}">${esc(s.checkLabel?.[d]||"Furniture "+DIMLBL[d].toLowerCase())}</label><div class="box"><input id="cmp-${d}" data-dim="${d}" type="text" inputmode="decimal" placeholder="0" autocomplete="off" value="${esc(cmpVal[d]??"")}"><span class="u">${unit}</span></div></div>`).join("")}</div>
    <div class="verdict" id="verdict" hidden></div></div>`;
}
function updateFit(){
  const item={};
  DIMS.forEach(d=>{ const raw=String(cmpVal[d]??"").trim(); if(!raw) return; const pvv=parseVal(raw); let n=parseFloat(pvv);
    if(!isNaN(n)&&/^\d/.test(pvv)&&!pvv.includes("×")) item[d]=unit==="cm"?n/2.54:n; });
  const show=x=>unit==="cm"?r1(Math.abs(x)*2.54)+" cm":String(+Math.abs(x).toFixed(2))+"″";
  let checked=0, walkMsg=null, walkOnly=true; const tooBig=[];
  document.querySelectorAll("#measBox .m[data-dims]").forEach(row=>{
    const box=row.querySelector(".fits"); if(!box) return;
    const dm=JSON.parse(row.dataset.dims); const parts=[]; const assumed=dm.assumed; delete dm.assumed;
    Object.keys(dm).forEach(d=>{ if(item[d]==null) return;
      const diff=dm[d]-item[d]; const multi=Object.keys(dm).filter(k=>item[k]!=null).length>1;
      const pre=multi?DIMLBL[d]+": ":assumed?"Assumed width: ":"";
      if(row.dataset.walk){
        walkMsg=diff>0.005?`Leaves ${show(diff)} to walk between the console and the bed`:"No room to walk between the console and the bed";
        if(diff>0.005) parts.push(`<span class="fit ok">${pre}${show(diff)} left to walk</span>`);
        else { parts.push(`<span class="fit no">${pre}No room to walk</span>`); tooBig.push(row.dataset.label); }
        checked++; return; }
      walkOnly=false;
      if(Math.abs(diff)<.005) parts.push(`<span class="fit ok">${pre}Exact match</span>`);
      else if(diff>0){
        // Say where the leftover room is: split left and right for widths, above for heights, in front for depths.
        const left=d==="width"?`${show(diff/2)} on each side if centered (${show(diff)} total)`
          :d==="height"?`${show(diff)} of room above it`
          :d==="depth"?`${show(diff)} of room left in front of it`
          :`${show(diff)} of room left over`;
        parts.push(`<span class="fit ok">${pre}Fits · ${left}</span>`);
      }
      else { parts.push(`<span class="fit no">${pre}${show(diff)} too big</span>`); tooBig.push(row.dataset.label+(multi?" ("+DIMLBL[d].toLowerCase()+")":"")); }
      checked++; });
    box.hidden=!parts.length; box.innerHTML=parts.join("");
  });
  const v=$("#verdict"); if(!v) return;
  if(!checked){ v.hidden=true; return; }
  v.hidden=false;
  if(walkOnly&&walkMsg){ v.className="verdict "+(tooBig.length?"no":"ok"); v.textContent=walkMsg; }
  else if(!tooBig.length){ v.className="verdict ok"; v.textContent=checked===1?"It fits":`It fits all ${checked} measurements`; }
  else { v.className="verdict no"; v.innerHTML=`Too big for ${tooBig.length} of ${checked} ${checked===1?"measurement":"measurements"}<span>Doesn’t fit: ${tooBig.map(esc).join(", ")}</span>`; }
}
async function copyText(t){
  try{ await navigator.clipboard.writeText(t); toast("Copied"); }
  catch(_){ toast("Couldn’t copy on this device"); }
}

// saved finds
function drawAddForm(){
  const box=$("#addBox"); if(!box) return;
  if(!db){ box.innerHTML=`<div class="save"><div class="info"><div class="d">Connect this phone to save links and photos.</div></div></div>`; return; }
  if(!canWrite){ box.innerHTML=""; return; }
  if(box.dataset.ready===openId) return;
  box.dataset.ready=openId;
  box.innerHTML=`<form class="form" id="addForm">
      <input id="lnk" type="url" inputmode="url" placeholder="Paste a product link" autocomplete="off" aria-label="Product link">
      <input id="nt" type="text" placeholder="Note: size, price, color" autocomplete="off" aria-label="Note">
      <div class="btns"><button class="btn primary" type="submit" id="saveLink">Save Link</button>
      <label class="btn" for="ph" tabindex="0" ${assets?"":"hidden"}>Add Photo</label><input id="ph" type="file" accept="image/*" multiple hidden></div>
      <div class="status" id="st"></div></form>`;
  $("label[for=ph]")?.addEventListener("keydown",e=>{ if(e.key==="Enter"||e.key===" "){ e.preventDefault(); $("#ph").click(); }});
  $("#addForm").addEventListener("submit",async e=>{e.preventDefault(); const u=cleanUrl($("#lnk").value); const n=$("#nt").value.trim();
    if(!u&&!n){st("Paste a link first.",1);return;}
    $("#saveLink").disabled=true; st("Saving…");
    try{ await db.collection("saves").add({space:openId,url:u||null,note:n||null,created:Date.now()}); $("#lnk").value="";$("#nt").value=""; st(""); toast("Link saved"); }
    catch(err){ denied(err); st(errMsg(err),1); }
    finally{ const b=$("#saveLink"); if(b) b.disabled=false; }
  });
  $("#ph").addEventListener("change",async e=>{const files=[...e.target.files]; e.target.value=""; if(!files.length) return; const n=$("#nt").value.trim(); const sp=openId;
    for(let i=0;i<files.length;i++){ st(`Uploading photo ${i+1} of ${files.length}…`);
      try{ const blob=await shrink(files[i]); const r=await assets.upload(blob,{type:blob.type||"image/jpeg"});
        await db.collection("saves").add({space:sp,asset:r.id,url:null,note:n||null,created:Date.now()}); }
      catch(err){ st(err?.code==="too_large"?"That photo is over 20 MB.":err?.code==="unsupported_type"?"That file type isn’t supported. Use a JPG, PNG or WebP.":"Couldn’t upload that photo. Try again.",1); return; } }
    $("#nt").value=""; st(""); toast(files.length>1?"Photos saved":"Photo saved");
  });
}
function cleanUrl(v){ v=String(v).trim(); if(!v) return ""; const m=v.match(/https?:\/\/\S+/i); if(m) return m[0]; return /^[\w-]+(\.[\w-]+)+/.test(v)?"https://"+v:v; }
function drawSaveList(){
  const box=$("#saveList"); if(!box) return; if(!db){ box.innerHTML=""; return; }
  const mine=saves.filter(x=>x.space===openId);
  box.innerHTML=mine.map(x=>{
    if(editS===x.id) return `<div class="save editing"><form class="form" id="sForm">
      ${x.asset?`<div class="hint">Photo note</div>`:`<input id="eLnk" type="url" inputmode="url" value="${esc(x.url??"")}" placeholder="Product link" aria-label="Product link">`}
      <input id="eNt" type="text" value="${esc(x.note??"")}" placeholder="Note: size, price, color" aria-label="Note">
      <div class="btns"><button class="btn primary" type="submit">Save</button><button class="btn" type="button" id="sCancel">Cancel</button></div>
      <div class="status" id="sSt"></div></form></div>`;
    return saveRow(x,false);
  }).join("")||`<div class="save"><div class="info"><div class="d">${storeReady?"Nothing saved for this space yet.":"Loading saved finds…"}</div></div></div>`;
  box.querySelectorAll(".pic img").forEach(img=>img.addEventListener("error",()=>{img.replaceWith(document.createTextNode("Missing"));}));
  box.querySelectorAll("[data-edits]").forEach(b=>b.addEventListener("click",()=>{editS=b.dataset.edits;drawSaveList();($("#eLnk")||$("#eNt"))?.focus();}));
  box.querySelectorAll("[data-del]").forEach(b=>b.addEventListener("click",async()=>{
    const x=saves.find(s=>s.id===b.dataset.del); if(!x) return; b.disabled=true;
    try{
      await db.collection("saves").doc(x.id).delete();
      let undone=false;
      const isDone=toast(x.asset?"Photo deleted":"Link deleted",()=>{undone=true; db.collection("saves").doc(x.id).set(stripId(x)).catch(()=>toast("Couldn’t restore it"));});
      if(x.asset&&assets) setTimeout(()=>{ if(!undone) assets.delete(x.asset).catch(()=>{}); },6000);
    }catch(_){ b.disabled=false; toast("Couldn’t delete. Try again."); }
  }));
  const f=$("#sForm"); if(!f) return;
  $("#sCancel").onclick=()=>{editS=null;drawSaveList();};
  f.addEventListener("submit",async e=>{e.preventDefault();
    const patch={note:$("#eNt").value.trim()||null}; if($("#eLnk")) patch.url=cleanUrl($("#eLnk").value)||null;
    const btn=f.querySelector("[type=submit]"); btn.disabled=true;
    try{ await db.collection("saves").doc(editS).update(patch); editS=null; drawSaveList(); toast("Changes saved"); }
    catch(err){ denied(err); btn.disabled=false; const s=$("#sSt"); if(s){s.textContent=errMsg(err); s.className="status err";} }
  });
}
function st(msg,err){const e=$("#st"); if(e){e.textContent=msg; e.className="status"+(err?" err":"");}}
async function shrink(file){
  try{
    const bmp=await createImageBitmap(file); const max=1800, k=Math.min(1,max/Math.max(bmp.width,bmp.height));
    const c=document.createElement("canvas"); c.width=Math.round(bmp.width*k); c.height=Math.round(bmp.height*k);
    c.getContext("2d").drawImage(bmp,0,0,c.width,c.height);
    return await new Promise((res,rej)=>c.toBlob(b=>b?res(b):rej(),"image/jpeg",.85));
  }catch(_){ return file; }
}

// spaces added in the app
function drawSpaceActs(){
  const box=$("#spaceActs"); const s=SP.find(x=>x.id===openId); if(!box) return; if(!s?.custom||!canWrite){ box.innerHTML=""; return; }
  box.innerHTML=`<h3 class="sec">This space</h3><div class="group"><button class="row add" id="rename">Rename Space</button><button class="row add" id="delSpace" style="color:var(--bad)">Delete Space</button></div><div class="status" id="spSt" style="margin:6px 16px"></div>`;
  $("#rename").onclick=()=>openSpaceForm(s.room,s);
  $("#delSpace").onclick=async e=>{const b=e.currentTarget;
    if(!b.dataset.armed){ b.dataset.armed="1"; b.textContent="Tap again to delete this space and everything in it"; return; }
    b.disabled=true;
    try{
      for(const c of customs.filter(c=>c.kind==="measure"&&c.space===s.id)) await db.collection("custom").doc(c.id).delete();
      for(const x of saves.filter(x=>x.space===s.id)){ await db.collection("saves").doc(x.id).delete(); if(x.asset&&assets) assets.delete(x.asset).catch(()=>{}); }
      await db.collection("custom").doc(s.docId).delete(); recents=recents.filter(r=>r!==s.id); ls.set("hm-recent",JSON.stringify(recents)); closeView(); toast("Space deleted");
    }catch(_){ b.disabled=false; const t=$("#spSt"); if(t){t.textContent="Couldn’t delete. Try again."; t.className="status err";} }
  };
}
let pendingOpen=null;
function openSpaceForm(rn,existing){
  openId=null; document.body.style.overflow="hidden";
  $("#viewHost").innerHTML=`<div class="scrim" id="scrim"><div class="view" role="dialog" aria-modal="true" aria-labelledby="nsh">
    <div class="nav scrolled"><button class="navbtn" id="x">${BACK}<span>${existing?esc(existing.name):"Back"}</span></button><div class="navtitle">${existing?"Rename Space":"New Space"}</div><div class="navspacer"></div></div>
    <div class="hero"><div class="crumb">${esc(rn)}</div><h2 id="nsh">${existing?"Rename space":"Add a space"}</h2></div>
    <div class="group" style="margin-top:14px"><form class="form" id="spForm">
      <select id="spRoom" aria-label="Room" ${existing?"disabled":""}>${ROOMS.map(r=>`<option ${r===rn?"selected":""}>${esc(r)}</option>`).join("")}</select>
      <input id="spName" type="text" placeholder="Space name, like Laundry Closet" value="${esc(existing?.name??"")}" autocomplete="off" aria-label="Space name">
      <input id="spNote" type="text" placeholder="Note (optional)" value="${esc(existing?.note??"")}" autocomplete="off" aria-label="Note">
      <div class="btns"><button class="btn primary" type="submit" id="spSave">${existing?"Save":"Create Space"}</button></div>
      <div class="status" id="spSt2"></div>
    </form></div></div></div>`;
  const back=()=>{ if(existing) openView(existing.id); else closeView(); };
  $("#x").onclick=back;
  $("#scrim").addEventListener("click",e=>{if(e.target.id==="scrim") back();});
  $("#spName").focus();
  $("#spForm").addEventListener("submit",async e=>{e.preventDefault();
    const name=$("#spName").value.trim(), note=$("#spNote").value.trim(), r=$("#spRoom").value;
    const t=$("#spSt2"); if(!name){ t.textContent="Give the space a name."; t.className="status err"; return; }
    $("#spSave").disabled=true;
    try{
      if(existing){ await db.collection("custom").doc(existing.docId).update({name,note}); openView(existing.id); toast("Space renamed"); }
      else { const ref=await db.collection("custom").add({kind:"space",room:r,name,note,created:Date.now()}); pendingOpen="c-"+ref.id; tryPending(); }
    }catch(err){ denied(err); $("#spSave").disabled=false; t.textContent=errMsg(err); t.className="status err"; }
  });
}
function tryPending(){ if(pendingOpen&&SP.some(s=>s.id===pendingOpen)){ const id=pendingOpen; pendingOpen=null; openView(id); editM="new"; drawMeas(); $("#mLabel")?.focus(); } }

document.addEventListener("keydown",e=>{ if(e.key==="Escape"){ const v=document.querySelector(".viewer"); if(v) v.remove(); else if($("#scrim")) $("#x").click(); }});

{ const r=ls.get("hm-room"); if(r&&ROOMS.includes(r)) room=r; }
// Keep the pinned room headers sitting just under the search header as it grows and shrinks.
function setHdr(){ document.documentElement.style.setProperty("--hdr",$("#top").offsetHeight+"px"); }
setHdr(); try{ new ResizeObserver(setHdr).observe($("#top")); }catch(_){ addEventListener("resize",setHdr); }
units(); chips(); render(); initStore();
</script>

</body>
</html>
