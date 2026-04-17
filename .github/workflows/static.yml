<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Breakform Bidding Manager</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;500;600&family=IBM+Plex+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
:root {
  --bg:#0f0f0f;--bg1:#161616;--bg2:#1e1e1e;--bg3:#252525;
  --border:#2e2e2e;--border2:#3a3a3a;
  --text:#e8e8e8;--text2:#a0a0a0;--text3:#606060;
  --amber:#f0a020;--amber-dim:#9b6510;--amber-bg:#1a1200;--amber-border:#3d2800;
  --green:#4caf50;--green-dim:#2d6e30;--green-bg:#071209;--green-border:#1a3c1b;
  --blue:#4a9eff;--blue-dim:#1e5fa8;--blue-bg:#040d1a;--blue-border:#0e2d52;
  --red:#ff5555;--red-dim:#9b2020;--red-bg:#120404;--red-border:#3d1010;
  --purple:#a78bfa;--purple-bg:#0d0b18;--purple-border:#2d2550;
  --mono:'IBM Plex Mono',monospace;--sans:'IBM Plex Sans',sans-serif;
  --r:4px;--r2:6px;
}
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:var(--sans);background:var(--bg);color:var(--text);height:100vh;overflow:hidden;font-size:13px}

/* TOPBAR */
.topbar{display:flex;align-items:center;gap:12px;padding:0 16px;height:44px;background:var(--bg1);border-bottom:1px solid var(--border);flex-shrink:0;z-index:10;position:relative}
.logo{font-family:var(--mono);font-size:13px;font-weight:600;letter-spacing:.12em;color:var(--text);user-select:none}
.logo span{color:var(--amber)}
.logo-sep{width:1px;height:20px;background:var(--border2);margin:0 4px}
.tabs{display:flex;gap:2px}
.tab{padding:5px 14px;border-radius:var(--r);font-size:12px;font-weight:500;cursor:pointer;border:none;background:transparent;color:var(--text3);transition:all .12s;font-family:var(--sans)}
.tab:hover{color:var(--text2);background:var(--bg2)}
.tab.active{background:var(--bg3);color:var(--amber);border:1px solid var(--border2)}
.topbar-right{margin-left:auto;display:flex;align-items:center;gap:8px}
.tb-badge{font-family:var(--mono);font-size:10px;color:var(--text3);padding:3px 8px;background:var(--bg2);border:1px solid var(--border);border-radius:var(--r)}
.tb-badge span{color:var(--amber)}

/* LAYOUT */
.app{display:flex;flex-direction:column;height:100vh}
.content{flex:1;overflow:hidden;display:flex}
.split{display:flex;flex:1;overflow:hidden}
.list-panel{width:320px;flex-shrink:0;border-right:1px solid var(--border);display:flex;flex-direction:column;background:var(--bg1)}
.list-scroll{flex:1;overflow-y:auto;padding:10px}
.detail-panel{flex:1;overflow-y:auto;background:var(--bg)}

/* SCROLLBAR */
::-webkit-scrollbar{width:4px;height:4px}
::-webkit-scrollbar-track{background:transparent}
::-webkit-scrollbar-thumb{background:var(--border2);border-radius:2px}

/* SEARCH */
.search-wrap{padding:10px 10px 6px;flex-shrink:0}
.search-box{display:flex;align-items:center;gap:8px;background:var(--bg2);border:1px solid var(--border);border-radius:var(--r2);padding:7px 10px;transition:border-color .15s}
.search-box:focus-within{border-color:var(--border2)}
.search-box svg{flex-shrink:0;color:var(--text3)}
.search-box input{background:transparent;border:none;outline:none;font-size:12px;color:var(--text);flex:1;font-family:var(--sans)}
.search-box input::placeholder{color:var(--text3)}

/* FILTER */
.filter-bar{padding:0 10px 8px;display:flex;gap:5px;flex-wrap:wrap;flex-shrink:0}
.chip{font-size:10px;font-family:var(--mono);padding:3px 9px;border-radius:20px;border:1px solid var(--border);cursor:pointer;color:var(--text3);background:var(--bg2);transition:all .1s;white-space:nowrap;user-select:none}
.chip:hover{color:var(--text2);border-color:var(--border2)}
.chip.on{background:var(--amber-bg);border-color:var(--amber-border);color:var(--amber)}
.filter-select{font-size:10px;font-family:var(--mono);padding:3px 6px;border-radius:4px;border:1px solid var(--border);background:var(--bg2);color:var(--text2);cursor:pointer;outline:none;flex:1;min-width:0}
.filter-select:focus{border-color:var(--border2)}

/* SECTION LABEL */
.sec-label{font-family:var(--mono);font-size:9px;font-weight:600;letter-spacing:.1em;color:var(--text3);text-transform:uppercase;padding:0 10px 6px;flex-shrink:0}

/* BADGES */
.badge{font-family:var(--mono);font-size:9px;font-weight:600;padding:2px 7px;border-radius:10px;letter-spacing:.05em;cursor:default}
.badge-hold{background:var(--amber-bg);color:var(--amber);border:1px solid var(--amber-border)}
.badge-lost{background:var(--red-bg);color:var(--red);border:1px solid var(--red-border)}
.badge-active{background:var(--green-bg);color:var(--green);border:1px solid var(--green-border)}
.badge-sent{background:var(--blue-bg);color:var(--blue);border:1px solid var(--blue-border)}
.badge-withdrawn{background:var(--bg2);color:var(--text3);border:1px solid var(--border)}
.badge-new{background:var(--purple-bg);color:var(--purple);border:1px solid var(--purple-border)}
.badge.clickable{cursor:pointer}
.badge.clickable:hover{filter:brightness(1.2)}

/* PROJ CARD */
.proj-card{background:var(--bg1);border:1px solid var(--border);border-radius:var(--r2);padding:10px 11px;margin-bottom:5px;cursor:pointer;transition:border-color .12s,background .12s}
.proj-card:hover{border-color:var(--border2);background:var(--bg2)}
.proj-card.sel{border-color:var(--amber-border);background:var(--amber-bg)}
.proj-name{font-size:12px;font-weight:500;color:var(--text);margin-bottom:5px}
.proj-meta{display:flex;gap:5px;align-items:center;flex-wrap:wrap;margin-bottom:6px}
.meta-chip{font-family:var(--mono);font-size:9px;color:var(--text3)}
.prog-track{height:2px;background:var(--bg3);border-radius:1px;overflow:hidden}
.prog-fill{height:100%;background:var(--amber);border-radius:1px;transition:width .3s}
.prog-fill.done{background:var(--green)}
.prog-text{font-family:var(--mono);font-size:9px;color:var(--text3);margin-top:3px}

/* SUB CARD */
.sub-card{background:var(--bg1);border:1px solid var(--border);border-radius:var(--r2);padding:9px 11px;margin-bottom:4px;cursor:pointer;transition:border-color .12s,background .12s}
.sub-card:hover{border-color:var(--border2);background:var(--bg2)}
.sub-card.sel{border-color:var(--amber-border);background:var(--amber-bg)}
.sub-card.inactive{opacity:.45}
.sub-head{display:flex;align-items:flex-start;gap:6px;margin-bottom:3px}
.sub-name{font-size:12px;font-weight:500;color:var(--text);flex:1;line-height:1.3}
.sub-code{font-family:var(--mono);font-size:9px;color:var(--text3)}
.sub-contact{font-family:var(--mono);font-size:10px;color:var(--text3);margin-top:2px}
.bid-dots{display:flex;gap:3px;flex-wrap:wrap;margin-top:4px;align-items:center}
.bid-dot{width:6px;height:6px;border-radius:50%;background:var(--amber)}
.status-dot{width:7px;height:7px;border-radius:50%;flex-shrink:0;margin-top:3px}
.status-dot.on{background:var(--green);box-shadow:0 0 4px var(--green-dim)}
.status-dot.off{background:var(--red-dim)}

/* DETAIL HEADER */
.d-header{padding:18px 20px 14px;border-bottom:1px solid var(--border);background:var(--bg1);position:sticky;top:0;z-index:5}
.d-title{font-size:16px;font-weight:600;color:var(--text);margin-bottom:6px}
.d-meta{display:flex;gap:6px;flex-wrap:wrap;align-items:center}

/* STATS */
.stats-row{display:flex;gap:8px;padding:12px 20px;border-bottom:1px solid var(--border);background:var(--bg1)}
.stat-box{flex:1;background:var(--bg2);border:1px solid var(--border);border-radius:var(--r2);padding:8px 10px;text-align:center}
.stat-num{font-family:var(--mono);font-size:20px;font-weight:600;color:var(--text)}
.stat-num.blue{color:var(--blue)}
.stat-num.amber{color:var(--amber)}
.stat-num.green{color:var(--green)}
.stat-label{font-family:var(--mono);font-size:9px;color:var(--text3);text-transform:uppercase;margin-top:2px;letter-spacing:.08em}

/* CATEGORIES */
.cats-section{padding:14px 20px}
.sec-heading{font-family:var(--mono);font-size:9px;font-weight:600;letter-spacing:.12em;color:var(--text3);text-transform:uppercase;margin-bottom:8px;margin-top:14px;display:flex;align-items:center;gap:8px}
.sec-heading:first-child{margin-top:0}
.sec-heading::after{content:'';flex:1;height:1px;background:var(--border)}

.cat-row{display:flex;align-items:center;gap:8px;padding:7px 10px;background:var(--bg1);border:1px solid var(--border);border-radius:var(--r);margin-bottom:3px;transition:border-color .1s;position:relative}
.cat-row:hover{border-color:var(--border2)}
.cat-name{font-size:11px;color:var(--text2);flex:1}
.cat-note{font-family:var(--mono);font-size:9px;color:var(--amber);margin-left:4px}

/* TOGGLES */
.tog-group{display:flex;gap:3px}
.tog{height:22px;padding:0 8px;border-radius:var(--r);font-family:var(--mono);font-size:9px;font-weight:600;cursor:pointer;border:1px solid var(--border);background:var(--bg3);color:var(--text3);display:flex;align-items:center;gap:3px;transition:all .1s;white-space:nowrap;user-select:none;min-width:44px;justify-content:center;position:relative}
.tog:hover{border-color:var(--border2);color:var(--text2)}
.tog.set{background:var(--blue-bg);border-color:var(--blue-border);color:var(--blue)}
.tog.sent{background:var(--amber-bg);border-color:var(--amber-border);color:var(--amber)}
.tog.recv{background:var(--green-bg);border-color:var(--green-border);color:var(--green)}
.tog.no{background:var(--red-bg);border-color:var(--red-border);color:var(--red)}
.tog.pend{background:var(--purple-bg);border-color:var(--purple-border);color:var(--purple)}
.tog.has-bids{background:var(--green-bg);border-color:var(--green);color:var(--green);box-shadow:0 0 6px rgba(76,175,80,.3)}

.price-tag{font-family:var(--mono);font-size:11px;color:var(--green);font-weight:600;margin-left:4px;white-space:nowrap}
.price-disc{font-family:var(--mono);font-size:13px;color:var(--green);font-weight:700;margin-left:4px}
.price-orig{font-family:var(--mono);font-size:10px;color:var(--text3);text-decoration:line-through;margin-left:3px}
.price-date{font-family:var(--mono);font-size:9px;color:var(--text3);margin-left:4px}

/* DROPDOWN MENU */
.dropdown-menu{position:absolute;top:calc(100% + 4px);left:0;background:var(--bg2);border:1px solid var(--border2);border-radius:var(--r2);padding:4px;z-index:200;min-width:140px;box-shadow:0 8px 24px rgba(0,0,0,.5);animation:fadeIn .1s ease}
@keyframes fadeIn{from{opacity:0;transform:translateY(-4px)}to{opacity:1;transform:translateY(0)}}
.dd-item{padding:6px 10px;border-radius:var(--r);font-size:11px;cursor:pointer;display:flex;align-items:center;gap:7px;color:var(--text2);font-family:var(--mono);transition:background .1s}
.dd-item:hover{background:var(--bg3);color:var(--text)}
.dd-item.dd-active{color:var(--green)}
.dd-item.dd-sent{color:var(--blue)}
.dd-item.dd-hold{color:var(--amber)}
.dd-item.dd-lost{color:var(--red)}
.dd-item.dd-withdrawn{color:var(--text3)}
.dd-item.dd-na{color:var(--text3)}
.dd-item.dd-set{color:var(--blue)}
.dd-item.dd-unset{color:var(--red)}
.dd-sep{height:1px;background:var(--border);margin:3px 0}

/* N/A TAGS */
.na-wrap{display:flex;flex-wrap:wrap;gap:4px;margin-top:8px}
.na-tag{font-family:var(--mono);font-size:9px;color:var(--text3);background:var(--bg2);border:1px dashed var(--border);padding:3px 9px;border-radius:10px;cursor:pointer;transition:all .15s;user-select:none}
.na-tag:hover{color:var(--amber);border-color:var(--amber-border);background:var(--amber-bg)}

/* SUB DETAIL */
.sub-info-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px;padding:14px 20px}
.info-block{background:var(--bg1);border:1px solid var(--border);border-radius:var(--r2);padding:10px 12px}
.info-label{font-family:var(--mono);font-size:9px;color:var(--text3);text-transform:uppercase;letter-spacing:.08em;margin-bottom:4px}
.info-val{font-size:12px;color:var(--text)}
.info-val a{color:var(--blue);text-decoration:none}
.info-val a:hover{text-decoration:underline}

/* BIDS TABLE */
.bids-section{padding:0 20px 20px}
.proj-bids-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(240px,1fr));gap:8px;margin-top:8px}
.proj-bid-card{background:var(--bg1);border:1px solid var(--border);border-radius:var(--r2);padding:10px 12px;transition:border-color .1s}
.proj-bid-card:hover{border-color:var(--border2)}
.proj-bid-name{font-size:11px;color:var(--text2);margin-bottom:4px;font-weight:500}
.proj-bid-cat{font-family:var(--mono);font-size:9px;color:var(--text3);margin-bottom:4px}
.proj-bid-prices{display:flex;align-items:baseline;gap:6px;margin-bottom:4px}
.proj-bid-price{font-family:var(--mono);font-size:16px;font-weight:700;color:var(--green)}
.proj-bid-price.discounted{color:var(--green)}
.proj-bid-original{font-family:var(--mono);font-size:11px;color:var(--text3);text-decoration:line-through}
.proj-bid-date{font-family:var(--mono);font-size:9px;color:var(--text3);margin-top:2px}
.proj-bid-actions{display:flex;gap:4px;margin-top:7px}

/* BIDS VIEW MODAL */
.bids-view-list{display:flex;flex-direction:column;gap:6px;margin-top:12px;max-height:340px;overflow-y:auto}
.bv-item{display:flex;align-items:center;gap:12px;padding:10px 12px;background:var(--bg2);border:1px solid var(--border);border-radius:var(--r2)}
.bv-sub{flex:1}
.bv-sub-name{font-size:12px;font-weight:500;color:var(--text)}
.bv-sub-code{font-family:var(--mono);font-size:9px;color:var(--text3)}
.bv-prices{text-align:right}
.bv-price{font-family:var(--mono);font-size:16px;font-weight:700;color:var(--green)}
.bv-orig{font-family:var(--mono);font-size:10px;color:var(--text3);text-decoration:line-through}
.bv-date{font-family:var(--mono);font-size:9px;color:var(--text3);margin-top:2px}
.bv-empty{text-align:center;padding:24px;color:var(--text3);font-family:var(--mono);font-size:11px}

/* OVERVIEW */
.overview-panel{padding:28px 40px;max-width:1600px;margin:0 auto}
.overview-stats{display:grid;grid-template-columns:repeat(4,1fr);gap:14px;margin-bottom:32px}
.ov-stat{background:var(--bg1);border:1px solid var(--border);border-radius:var(--r2);padding:22px 24px;min-height:96px;display:flex;flex-direction:column;justify-content:center}
.ov-num{font-family:var(--mono);font-size:32px;font-weight:600;color:var(--text);margin-bottom:6px;line-height:1}
.ov-label{font-family:var(--mono);font-size:10px;color:var(--text3);text-transform:uppercase;letter-spacing:.1em;line-height:1.4}
.ov-projects-grid{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-bottom:32px}
.ov-proj-card{background:var(--bg1);border:1px solid var(--border);border-radius:var(--r2);padding:14px 16px;cursor:pointer;transition:border-color .1s,background .1s;min-height:78px;box-sizing:border-box}
.ov-proj-card:hover{border-color:var(--border2)}
.ov-proj-card.sel{border-color:var(--amber);background:var(--amber-bg)}
@media (max-width: 1200px){ .ov-projects-grid{grid-template-columns:repeat(3,1fr)} }
@media (max-width: 900px){ .ov-projects-grid{grid-template-columns:repeat(2,1fr)} }
.activity-feed{display:flex;flex-direction:column;gap:4px}
.act-item{display:flex;align-items:flex-start;gap:10px;padding:9px 12px;background:var(--bg1);border:1px solid var(--border);border-radius:var(--r);transition:border-color .1s}
.act-item:hover{border-color:var(--border2)}
.act-dot{width:8px;height:8px;border-radius:50%;flex-shrink:0;margin-top:4px}
.act-dot.new{background:var(--green)}
.act-dot.upd{background:var(--amber)}
.act-body{flex:1}
.act-title{font-size:12px;color:var(--text);font-weight:500;margin-bottom:2px}
.act-sub{font-family:var(--mono);font-size:10px;color:var(--text3)}
.act-price{font-family:var(--mono);font-size:13px;font-weight:600;color:var(--green)}
.act-time{font-family:var(--mono);font-size:9px;color:var(--text3);flex-shrink:0;margin-top:4px}

/* MODAL */
.backdrop{position:fixed;top:0;left:0;width:100%;height:100%;background:rgba(0,0,0,.72);display:flex;align-items:center;justify-content:center;z-index:100;backdrop-filter:blur(3px)}
.modal{background:var(--bg1);border:1px solid var(--border2);border-radius:8px;padding:22px;width:400px;animation:slideUp .18s ease}
.modal-wide{width:520px}
@keyframes slideUp{from{transform:translateY(8px);opacity:0}to{transform:translateY(0);opacity:1}}
.modal-title{font-size:14px;font-weight:600;color:var(--text);margin-bottom:4px}
.modal-sub{font-family:var(--mono);font-size:11px;color:var(--text3);margin-bottom:16px}
.modal-label{font-family:var(--mono);font-size:10px;color:var(--text3);text-transform:uppercase;letter-spacing:.08em;margin-bottom:5px}
.modal-input{width:100%;border:1px solid var(--border2);border-radius:var(--r2);padding:9px 12px;font-size:14px;font-family:var(--mono);background:var(--bg2);color:var(--text);outline:none;margin-bottom:14px;transition:border-color .15s}
.modal-input:focus{border-color:var(--amber)}
.minp{width:100%;border:1px solid var(--border2);border-radius:var(--r2);padding:8px 12px;font-size:12px;font-family:var(--sans);background:var(--bg2);color:var(--text);outline:none;margin-bottom:10px;transition:border-color .15s}
.minp:focus{border-color:var(--amber)}
.msel{width:100%;border:1px solid var(--border2);border-radius:var(--r2);padding:8px 12px;font-size:12px;font-family:var(--sans);background:var(--bg2);color:var(--text);outline:none;margin-bottom:10px;cursor:pointer}
.msel:focus{border-color:var(--amber)}
.mrow{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.modal-btns{display:flex;gap:8px;justify-content:flex-end;margin-top:16px}
.btn{padding:8px 16px;border-radius:var(--r2);font-size:12px;font-family:var(--sans);cursor:pointer;border:1px solid var(--border2);font-weight:500;transition:all .1s}
.btn-amber{background:var(--amber);border-color:var(--amber);color:#0a0500}
.btn-amber:hover{background:#e09010}
.btn-ghost{background:transparent;color:var(--text2)}
.btn-ghost:hover{background:var(--bg2);color:var(--text)}
.btn-danger{background:var(--red-bg);border-color:var(--red-border);color:var(--red)}
.btn-danger:hover{background:var(--red-dim);color:white}
.btn-green{background:var(--green-bg);border-color:var(--green-border);color:var(--green)}
.btn-sm{padding:4px 10px;font-size:11px}

/* ADD BTN */
.add-btn{display:flex;align-items:center;gap:6px;padding:7px 12px;margin:0 10px 8px;border:1px dashed var(--border2);border-radius:var(--r2);background:transparent;color:var(--text3);font-family:var(--mono);font-size:10px;cursor:pointer;transition:all .15s;flex-shrink:0;width:calc(100% - 20px)}
.add-btn:hover{border-color:var(--amber-border);color:var(--amber);background:var(--amber-bg)}

/* TOGGLE */
.toggle-wrap{display:flex;align-items:center;gap:10px}
.toggle{position:relative;width:36px;height:20px;cursor:pointer}
.toggle input{opacity:0;width:0;height:0;position:absolute}
.toggle-track{position:absolute;top:0;left:0;right:0;bottom:0;background:var(--bg3);border:1px solid var(--border2);border-radius:10px;transition:all .2s}
.toggle input:checked+.toggle-track{background:var(--green-dim);border-color:var(--green-border)}
.toggle-thumb{position:absolute;top:3px;left:3px;width:12px;height:12px;background:var(--text3);border-radius:50%;transition:all .2s}
.toggle input:checked+.toggle-track+.toggle-thumb{transform:translateX(16px);background:var(--green)}

/* COMMENT BOX */
.comment-box{background:var(--bg2);border:1px solid var(--border);border-radius:var(--r2);padding:10px 12px;font-size:12px;color:var(--text3);line-height:1.5;margin-bottom:12px}
.rfi-box{background:var(--amber-bg);border:1px solid var(--amber-border);border-radius:var(--r2);padding:8px 12px;font-size:12px;color:var(--amber);margin-bottom:12px}

/* EDIT BTN */
.edit-btn{font-family:var(--mono);font-size:9px;padding:3px 8px;border-radius:var(--r);border:1px solid var(--border);background:var(--bg3);color:var(--text3);cursor:pointer;transition:all .1s}
.edit-btn:hover{border-color:var(--amber-border);color:var(--amber);background:var(--amber-bg)}

.empty{text-align:center;padding:60px 20px;color:var(--text3);font-family:var(--mono);font-size:12px;line-height:2}

/* Price section in sub bid */
.price-entry-row{display:grid;grid-template-columns:1fr 1fr 1fr auto;gap:8px;align-items:end;margin-bottom:8px}
.disc-badge{font-family:var(--mono);font-size:9px;padding:2px 7px;border-radius:10px;background:var(--green-bg);color:var(--green);border:1px solid var(--green-border)}
/* PROJ HEADER BOXES */
.proj-boxes{display:flex;gap:6px;padding:8px 20px 0;flex-wrap:wrap}
.proj-box{background:var(--bg2);border:1px solid var(--border);border-radius:var(--r2);padding:6px 10px;flex:1;min-width:140px;transition:border-color .15s;cursor:pointer;min-height:44px;display:flex;flex-direction:column;justify-content:center}
.proj-box:hover{border-color:var(--border2)}
.proj-box.editing{border-color:var(--amber);cursor:default}
.pbox-label{font-family:var(--mono);font-size:8px;color:var(--text3);text-transform:uppercase;letter-spacing:.08em;margin-bottom:3px}
.pbox-val{font-size:12px;font-weight:700;color:var(--text);line-height:1.2}
.pbox-val.dl{color:var(--amber);font-size:15px}
.pbox-val.empty{color:var(--text3);font-size:10px;font-weight:400;font-style:italic}
.bt-chip{display:inline-flex;align-items:center;gap:4px;background:var(--bg3);border:1px solid var(--border2);border-radius:10px;padding:2px 8px;font-size:11px;color:var(--text2);margin:2px 2px 0 0}
.bt-chip button{border:none;background:transparent;color:var(--text3);cursor:pointer;font-size:11px;padding:0 1px;line-height:1}
.bt-chip button:hover{color:var(--red)}
/* Architect Set link row */
.arch-row{padding:8px 20px 0}
.arch-set{display:flex;align-items:center;gap:10px;background:var(--bg2);border:1px solid var(--border);border-radius:var(--r2);padding:10px 14px;transition:all .15s}
.arch-set:hover{border-color:var(--border2)}
.arch-set.has-link{border-color:var(--blue-border);background:var(--blue-bg)}
.arch-set-label{font-family:var(--mono);font-size:9px;color:var(--text3);text-transform:uppercase;letter-spacing:.08em;flex-shrink:0}
.arch-set-link{flex:1;font-size:12px;color:var(--blue);text-decoration:none;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;font-weight:500}
.arch-set-link:hover{text-decoration:underline}
.arch-set-empty{flex:1;font-size:11px;color:var(--text3);font-style:italic}
.arch-set-btn{background:transparent;border:1px solid var(--border2);color:var(--text2);font-size:11px;padding:4px 10px;border-radius:6px;cursor:pointer;font-family:var(--sans)}
.arch-set-btn:hover{border-color:var(--amber);color:var(--amber)}
.arch-set-btn.primary{background:var(--blue);border-color:var(--blue);color:#fff;font-weight:600}
.arch-set-btn.primary:hover{background:var(--blue-dark,#0052cc)}
.arch-set-inp{flex:1;background:var(--bg1);border:1px solid var(--amber);border-radius:6px;padding:6px 10px;font-size:12px;color:var(--text);outline:none;font-family:var(--sans)}
/* Remove spinners on number inputs */
.minp[type="number"]::-webkit-outer-spin-button,
.minp[type="number"]::-webkit-inner-spin-button{-webkit-appearance:none;margin:0}
.minp[type="number"]{-moz-appearance:textfield;appearance:textfield}
input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button{-webkit-appearance:none;margin:0}
input[type="number"]{-moz-appearance:textfield;appearance:textfield}
/* FOLLOW-UP TAB */
.fu-cat-row{display:flex;align-items:center;gap:10px;padding:12px 14px;background:var(--bg1);border:1px solid var(--border);border-radius:var(--r2);margin-bottom:6px;cursor:pointer;transition:border-color .12s}
.fu-cat-row:hover{border-color:var(--border2)}
.fu-cat-name{font-size:13px;font-weight:500;color:var(--text);flex:1}
.fu-cat-meta{font-family:var(--mono);font-size:10px;color:var(--text3);display:flex;gap:10px;align-items:center}
.fu-sent-pill{font-family:var(--mono);font-size:9px;padding:2px 8px;border-radius:10px;background:var(--green-bg);color:var(--green);border:1px solid var(--green-border)}
.fu-followup-pill{font-family:var(--mono);font-size:9px;padding:2px 8px;border-radius:10px;background:var(--amber-bg);color:var(--amber);border:1px solid var(--amber-border)}
.fu-view-btn{background:transparent;border:1px solid var(--border2);color:var(--text2);font-size:11px;padding:4px 10px;border-radius:6px;cursor:pointer;font-family:var(--sans)}
.fu-view-btn:hover{border-color:var(--amber);color:var(--amber)}
.fu-sub-row{display:flex;align-items:center;gap:10px;padding:8px 12px;border-bottom:1px solid var(--border)}
.fu-sub-row:last-child{border-bottom:none}
.fu-sub-info{flex:1;min-width:0}
.fu-sub-name{font-size:13px;font-weight:500;color:var(--text);margin-bottom:2px}
.fu-sub-emails{font-family:var(--mono);font-size:10px;color:var(--text3);word-break:break-all}
.fu-sub-noemail{font-family:var(--mono);font-size:10px;color:var(--red);font-style:italic}
.fu-toggle{background:var(--bg3);border:1px solid var(--border2);color:var(--text3);font-size:10px;padding:4px 12px;border-radius:6px;cursor:pointer;font-family:var(--mono);letter-spacing:.06em;white-space:nowrap}
.fu-toggle:hover{border-color:var(--amber)}
.fu-toggle.on{background:var(--amber-bg);border-color:var(--amber);color:var(--amber)}
.fu-bcc-box{background:var(--bg2);border:1px solid var(--border);border-radius:var(--r2);padding:10px 12px;margin-bottom:10px;font-family:var(--mono);font-size:10px;color:var(--text2);max-height:80px;overflow-y:auto;word-break:break-all;line-height:1.5;user-select:all}
.fu-action-row{display:flex;gap:8px;align-items:center;margin-bottom:12px;flex-wrap:wrap}
.fu-history{font-family:var(--mono);font-size:10px;color:var(--text3);margin-bottom:10px;padding:6px 10px;background:var(--bg2);border-radius:6px}
.fu-view-tabs{display:flex;gap:4px;margin-bottom:10px;border-bottom:1px solid var(--border)}
.fu-view-tab{font-family:var(--mono);font-size:10px;padding:6px 12px;cursor:pointer;color:var(--text3);border-bottom:2px solid transparent;letter-spacing:.06em}
.fu-view-tab.on{color:var(--amber);border-bottom-color:var(--amber)}
.fu-empty-state{text-align:center;padding:24px 12px;color:var(--text3);font-size:12px;font-style:italic}
.fu-project-card{background:var(--bg1);border:1px solid var(--border);border-radius:var(--r2);padding:12px 14px;margin-bottom:6px;cursor:pointer;transition:border-color .12s}
.fu-project-card:hover{border-color:var(--border2)}
.fu-project-card.sel{border-color:var(--amber);background:var(--amber-bg)}
</style>
</head>
<body>
<div class="app" id="app"></div>
<script>
// ============================================================
// BASE DATA
// ============================================================
const PROJECTS_BASE = [
  {id:'p01',name:'52-60 Market St',status:'on-hold',dl:'TBD',sdl:null,est:'Csaba',source:'Breakform',comments:'Wait till the new changes arrive to re bid. Csaba is checking new plans.',rfi:'',builder:'Csaba'},
  {id:'p02',name:'Quadro Vecchio',status:'lost',dl:'PAST DUE',sdl:null,est:null,source:null,comments:'LOST — Csaba is checking new plans.',rfi:'',builder:null},
  {id:'p03',name:'429 Sherman Canal',status:'active',dl:'08/15/25',sdl:null,est:'Sofia',source:'INTERNAL',comments:'',rfi:'',builder:'Tas'},
  {id:'p04',name:'213 OFW Waterfront',status:'active',dl:'08/01/25',sdl:null,est:'Sofia',source:'INTERNAL',comments:'',rfi:'',builder:'Csaba'},
  {id:'p05',name:'723 OFW',status:'active',dl:'08/30/25',sdl:'12/19/25',est:'Sofia',source:null,comments:'',rfi:'',builder:null},
  {id:'p06',name:'15265 W Bestor Blvd',status:'sent',dl:'05/12/25',sdl:null,est:'Tas',source:'Breakform',comments:'Wait for architects to answer. Call Billy.',rfi:'',builder:'Tas'},
  {id:'p07',name:'748 & 750 Palisades Dr',status:'active',dl:'08/30/25',sdl:'02/27/26',est:'Sofia',source:'Breakform',comments:'Monday for site walks.',rfi:'',builder:'Csaba'},
  {id:'p08',name:'478 Wynola St',status:'sent',dl:'09/22/25',sdl:'12/22/25',est:null,source:'Architect',comments:'Take-offs: wood flooring, tiles, gypsum board, stucco.',rfi:'Specify finish on flooring',builder:null},
  {id:'p09',name:'6537 Topanga Canyon',status:'withdrawn',dl:'WITHDRAW',sdl:null,est:null,source:null,comments:'DISREGARD PROJECT',rfi:'',builder:null},
  {id:'p10',name:'17797 Camino De Yatasto',status:'sent',dl:'SENT',sdl:null,est:'Edmund',source:'Architect',comments:'',rfi:'',builder:'Edmund'},
  {id:'p11',name:'865 N Oreo Pl',status:'sent',dl:'11/28/25',sdl:null,est:'Tas',source:'Breakform',comments:'Structural drawings bid updates — Billy Snow.',rfi:'',builder:'Tas'},
  {id:'p12',name:'807 6th Ave',status:'sent',dl:'11/07/25',sdl:null,est:'Edmund',source:'Architect: David Kornmeyer',comments:'',rfi:'',builder:'Edmund'},
  {id:'p13',name:'1080 El Medio Place',status:'sent',dl:'12/04/25',sdl:'12/12/25',est:'Tas',source:'Architect: Bestor',comments:'Take-offs: tiles, wood flooring, wood deck, stone pavers.',rfi:'Grand HVAC contractor asks for site walk.',builder:'Tas'},
  {id:'p14',name:'4565 Dundee Drive',status:'sent',dl:'SENT',sdl:null,est:'Edmund',source:'Architect: RFRMM Collective',comments:'',rfi:'',builder:'Edmund'},
  {id:'p15',name:'1093 Palms Blvd',status:'sent',dl:'12/01/25',sdl:null,est:'Tas',source:'Architect',comments:'Re-send info to AMG Electric.',rfi:'',builder:'Tas'},
  {id:'p16',name:'2429 Eastern Canal',status:'sent',dl:'SENT',sdl:null,est:null,source:'Architect',comments:'Service connections from main house included.',rfi:'',builder:null},
  {id:'p17',name:'16339 Akron',status:'active',dl:'01/09/26',sdl:null,est:null,source:null,comments:'',rfi:'',builder:null},
  {id:'p18',name:'14949 Mc Kendree Ave',status:'sent',dl:'SENT',sdl:null,est:null,source:null,comments:'',rfi:'',builder:null},
  {id:'p19',name:'12979 Blairwood Dr',status:'sent',dl:'SENT',sdl:null,est:null,source:null,comments:'',rfi:'',builder:null},
  {id:'p20',name:'7300 Vista Del Mar',status:'active',dl:'',sdl:null,est:null,source:null,comments:'',rfi:'',builder:null},
  {id:'p21',name:'1134 Iliff St',status:'active',dl:'',sdl:null,est:null,source:null,comments:'',rfi:'',builder:null},
];

const CATS = ['STRUCTURAL CONCRETE','ROUGH CARPENTRY','PLUMBING AND APPLIANCES','HVAC','ELECTRIC ROUGH','INSULATION','WATERPROOFING','DEMOLITION','ROOFING','STRUCTURAL STEEL','MASONRY','ELEVATORS','EXTERIOR WOOD SIDING','METAL SIDING - PANELS','CABINETS','GYPSUM BOARD - DRYWALL','WOOD FLOORING','INSTALLATION TILES','METAL FABRICATION','WINDOWS & DOORS','FIRE SPRINKLERS','STUCCO','RAILING','GLAZING','PLANTING-LANDSCAPING','SWIMING POOL/SPA','FIREPLACE','SHORING / GRADING','SKYLIGHTS','CONCRETE SLAB','ELEVATED ROOF DECKS','SOLAR PANELS'];

const DIV_CODES = {"DIVISION 01": ["014533 Utilities", "015000 Temp  Facilities", "015150 Deputy Inspections", "015220 Temporary Toilet", "015423 Scaffolding", "015620 Temporary Fencing", "017410 Dumpsters", "017423 Final Clean-up"], "DIVISION 02": ["022600 Asbestos", "024000 Demolition", "030630 Concrete Slab", "031113 Shoring", "033100 Structural Concrete", "051200 Structural Steel", "061000 Rough Carpentry", "131100 Swimming Pool/Spa/Fountain", "312300 Excavation & Backfill", "312500 Erosion Controls", "334000 Stormwater management-LID"], "DIVISION 03": ["024000 Demolition", "030630 Concrete Slab", "030650 Finish Concrete", "031113 Shoring", "033100 Structural Concrete", "042200 Concrete Masonry Unit", "061000 Rough Carpentry", "077700 Waterproofing Build. Wrap", "131100 Swimming Pool/Spa/Fountain"], "DIVISION 04": ["042100 Masonry Brick Veneer", "042200 Concrete Masonry Unit", "055200 Metal Railing", "096000 Tile - Material", "103000 Fireplace"], "DIVISION 05": ["051200 Structural Steel", "054000 Cold Form Metal Framing", "055000 Metal Fabricators", "055200 Metal Railing", "058000 Glazing", "064100 Cabinets", "074619 Steel Siding", "076000 Flashing & Sheet Metal", "081001 Exterior Doors & Windows Installation", "092000 Gypsum Board", "093200 Elevated Roof Top Decks", "323100 Fences & Gates"], "DIVISION 06": ["061000 Rough Carpentry", "062000 Finish Carpentry", "064100 Cabinets", "074623 Wood Siding", "077700 Waterproofing Build. Wrap", "081001 Exterior Doors & Windows Installation", "081005- Shower enclosures", "087000 Finish Hardware", "093600 Countertops"], "DIVISION 07": ["071000 Roofing", "071010 Waterproofing", "072100 Insulation", "073313 Green Roof", "074619 Steel Siding", "076000 Flashing & Sheet Metal", "076113 Standing Seam Sheet Metal Roofing", "076413 Standing Seam Sheet Metal Wall Cladding", "077123 Gutters/Downspouts/Water Retention", "077700 Waterproofing Build. Wrap", "103000 Fireplace"], "DIVISION 08": ["058000 Glazing", "061000 Rough Carpentry", "074623 Wood Siding", "074624 Wood Siding - Install", "081000 Exterior Doors & Windows Supply", "081001 Exterior Doors & Windows Installation", "081002 Interior Doors & Frames", "081003 Interior Doors & Frames Installation", "081004 Garage Doors", "081005- Shower enclosures", "086000 Skylights", "087000 Finish Hardware", "224000 Plumbing Fixtures"], "DIVISION 09": ["055000 Metal Fabricators", "062000 Finish Carpentry", "074619 Steel Siding", "074623 Wood Siding", "074624 Wood Siding - Install", "081001 Exterior Doors & Windows Installation", "081002 Interior Doors & Frames", "081004 Garage Doors", "092000 Gypsum Board", "092400 Stucco", "093200 Elevated Roof Top Decks", "095100 Accoustical Ceiling", "096000 Tile - Installation", "096000 Tile - Material", "096100 Flooring", "096400 Wood Flooring", "096600 Terrazzo", "096800 Carpet", "097200 Wall Coverings", "099000 Painting", "099001 Painting Cabinets"], "DIVISION 10": ["102800 Toilet/Bathrom Accessories", "103000 Fireplace", "113000 Residential Equipment", "224000 Plumbing Fixtures", "96801 Carpet"], "DIVISION 11": ["111000 Vehicle Equipment", "112163 Refrigerated Display Equipment", "113000 Residential Equipment", "122000 Window Treatments"], "DIVISION 12": ["122000 Window Treatments"], "DIVISION 13": ["130000 - Pool & Spa Coping", "131100 Swimming Pool/Spa/Fountain", "Sauna"], "DIVISION 14": ["142000 Elevators"], "DIVISION 21": ["211300 Fire Spinklers"], "DIVISION 22": ["102800 Toilet/Bathrom Accessories", "113000 Residential Equipment", "220000 Plumbing Rough & Finish", "223200 Domestic Water Filtration Equipment", "224000 Plumbing Fixtures", "230000 Hvac", "334000 Stormwater management-LID"], "DIVISION 23": ["230000 Hvac"], "DIVISION 26": ["211300 Fire Spinklers", "221000 Radiant Heating", "250000 Home Automation", "250010 Security Systems", "260500 Electric Rough & Finish", "262000 Low Voltage", "269900 Electric Fixtures", "270500 Audio Visual Systems", "481400 Solar Energy Electrical Power Generation Equipment"], "DIVISION 31": ["312300 Excavation & Backfill", "312500 Erosion Controls", "334000 Stormwater management-LID"], "DIVISION 32": ["321300 Ridgid Paving", "323100 Fences & Gates", "329000 Planting, Landscaping"], "DIVISION 33": ["334000 Stormwater management-LID"]};

// Category → substring patterns to match sub codes
const CAT_TO_CODES = {
  'STRUCTURAL CONCRETE': ['033100','structural concrete'],
  'ROUGH CARPENTRY': ['061000','rough carpentry'],
  'PLUMBING AND APPLIANCES': ['220000','223200','224000','113000','102800','plumbing','residential equipment','plumbing fixtures'],
  'HVAC': ['230000','hvac','radiant heating','221000'],
  'ELECTRIC ROUGH': ['260500','262000','269900','270500','250000','250010','electric rough','low voltage','electric fixtures','home automation','security systems'],
  'INSULATION': ['072100','insulation'],
  'WATERPROOFING': ['071010','077700','waterproofing','build. wrap'],
  'DEMOLITION': ['024000','demolition'],
  'ROOFING': ['071000','076113','roofing','green roof','standing seam sheet metal roofing'],
  'STRUCTURAL STEEL': ['051200','054000','structural steel','cold form metal framing'],
  'MASONRY': ['042100','042200','masonry'],
  'ELEVATORS': ['142000','elevator'],
  'EXTERIOR WOOD SIDING': ['074623','074624','wood siding'],
  'METAL SIDING - PANELS': ['074619','076413','steel siding','sheet metal wall cladding'],
  'CABINETS': ['064100','093600','cabinet','countertop'],
  'GYPSUM BOARD - DRYWALL': ['092000','gypsum','drywall'],
  'WOOD FLOORING': ['096400','096100','wood flooring','flooring'],
  'INSTALLATION TILES': ['096000','tile'],
  'METAL FABRICATION': ['055000','076000','metal fabricator','flashing & sheet metal'],
  'WINDOWS & DOORS': ['081000','081001','081002','081003','081004','081005','087000','window','door','hardware','shower enclosure'],
  'FIRE SPRINKLERS': ['211300','fire spinkler','fire sprinkler'],
  'STUCCO': ['092400','stucco'],
  'RAILING': ['055200','railing'],
  'GLAZING': ['058000','glazing'],
  'PLANTING-LANDSCAPING': ['329000','323100','landscap','planting','fence'],
  'SWIMING POOL/SPA': ['131100','130000','pool','spa','fountain'],
  'FIREPLACE': ['103000','fireplace','sauna'],
  'SHORING / GRADING': ['031113','312300','312500','shoring','excavation','erosion','grading'],
  'SKYLIGHTS': ['086000','skylight'],
  'CONCRETE SLAB': ['030630','030650','concrete slab','finish concrete'],
  'ELEVATED ROOF DECKS': ['093200','077123','elevated roof','gutter'],
  'SOLAR PANELS': ['481400','solar']
};

// Return active subs whose codes match the given project category
function getSubsForCategory(cat) {
  const keys = CAT_TO_CODES[cat] || [];
  if (!keys.length) return [];
  const lowered = keys.map(k => k.toLowerCase());
  return allSubs().filter(s => {
    if (!s.active) return false;
    const codesStr = subCodes(s).join(' | ').toLowerCase();
    return lowered.some(k => codesStr.includes(k));
  });
}

// Split email string (which may contain multiple comma-separated addresses) into array
function parseEmails(str) {
  if (!str) return [];
  return str.split(/[,;]+/).map(e => e.trim()).filter(e => e.includes('@'));
}


const CM = {
'STRUCTURAL CONCRETE':    ['YYY','YYY','YYY','---','YYY','YYY','---','YYY','---','YYY','YYY','YYY','YYY','YYY','YYY','YYY','---','---','---','---','---'],
'ROUGH CARPENTRY':        ['YYY','YYY','YYY','---','YYY','YYY','YYY','YYY','---','YYY','YYY','YYY','YYY','YYY','YYY','YYY','---','---','---','---','---'],
'PLUMBING AND APPLIANCES':['YYY','---','---','YYY','P-N','YYY','---','YYY','YYY','YYY','YYY','YYY','YYY','YYN','YYY','YYY','---','---','---','---','---'],
'HVAC':                   ['YYY','YYY','---','YYY','P-N','YYY','---','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','---','---','---','---','---'],
'ELECTRIC ROUGH':         ['YYY','YYY','YYY','YYY','P-N','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','---','---','---','---','---'],
'INSULATION':             ['YYY','YYY','---','YYY','YYY','YYY','YYY','YYY','---','YYY','YYY','YYY','YYY','YYY','YYY','YYY','---','---','---','---','---'],
'WATERPROOFING':          ['YYY','YYY','YYY','YYN','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','---','---','---','---','---'],
'DEMOLITION':             ['YYY','YYY','YYY','---','YYY','---','---','YYY','YYN','---','---','YYY','---','YYN','YYY','YYY','---','---','---','---','---'],
'ROOFING':                ['YYY','YYY','YYY','YYN','---','YYY','YYY','YYY','---','YYY','---','---','YYY','YYY','YYY','YYY','---','---','---','---','---'],
'STRUCTURAL STEEL':       ['YYY','YYY','---','---','---','YYY','---','---','YYY','YYY','YYY','YYY','---','YYY','---','---','---','---','---','---','---'],
'MASONRY':                ['---','YYN','---','YYN','---','---','---','YYY','---','---','---','---','---','---','---','---','---','---','---','---','---'],
'ELEVATORS':              ['---','YYY','---','---','YYY','YYY','---','---','---','---','YYY','YYY','---','---','---','---','---','---','---','---','---'],
'EXTERIOR WOOD SIDING':   ['---','---','---','---','---','YYY','---','---','YYN','YYY','---','---','YYY','---','YYY','---','---','---','---','---','---'],
'METAL SIDING - PANELS':  ['---','---','---','---','---','---','---','---','---','---','---','YYY','---','YYN','---','---','---','---','---','---','---'],
'CABINETS':               ['YYY','YYY','YYY','---','YYY','YYY','YYY','---','---','YYY','YYY','YYY','YYY','YYY','YYY','YYY','---','---','---','---','---'],
'GYPSUM BOARD - DRYWALL': ['---','YYY','YYY','---','YYY','YYY','YYY','YYY','YYN','YYY','YYY','YYY','YYY','YYY','YYY','YYY','---','---','---','---','---'],
'WOOD FLOORING':          ['---','YYY','---','---','---','YYY','---','---','---','YYY','---','YYY','YYY','PPN','---','PPP','---','---','---','---','---'],
'INSTALLATION TILES':     ['YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYN','YYY','YYY','---','---','---','---','---'],
'METAL FABRICATION':      ['YYN','---','---','YYY','---','---','YYY','YYY','---','---','YYY','YYY','---','---','---','---','---','---','---','---','---'],
'WINDOWS & DOORS':        ['YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','YYY','---','---','---','---','---'],
'FIRE SPRINKLERS':        ['YYY','YYY','---','---','YYY','YYY','YYY','---','YYY','YYY','YYY','YYY','YYY','YYY','---','YYY','---','---','---','---','---'],
'STUCCO':                 ['---','YYN','YYY','---','YYY','---','YYY','YYY','YYY','YYY','---','YYY','---','YYY','YYY','YYY','---','---','---','---','---'],
'RAILING':                ['YYY','---','YYY','YYY','YYY','YYY','YYY','YYY','---','YYY','YYY','YYY','---','---','---','---','---','---','---','---','---'],
'GLAZING':                ['---','---','YYY','---','YYY','---','---','---','---','---','---','YYY','---','---','---','---','---','---','---','---','---'],
'PLANTING-LANDSCAPING':   ['YYN','---','---','---','YYY','---','---','---','---','---','---','---','YYN','---','YYN','---','---','---','---','---','---'],
'SWIMING POOL/SPA':       ['---','YYN','---','---','---','YYN','---','---','---','YYY','YYY','YYY','YYY','---','---','---','---','---','---','---','---'],
'FIREPLACE':              ['---','YYY','---','---','---','YYY','YYY','---','---','YYY','YYY','YYY','YYY','---','---','---','---','---','---','---','---'],
'SHORING / GRADING':      ['--Y','YYY','---','---','---','---','---','---','---','---','YYY','YYY','---','---','---','---','---','---','---','---','---'],
'SKYLIGHTS':              ['YYY','---','---','---','---','YYY','---','---','YYN','---','YYY','YYY','---','YYY','YYY','---','---','---','---','---','---'],
'CONCRETE SLAB':          ['---','---','---','YYY','---','---','---','YYY','YYY','---','YYY','---','YYY','---','YYY','---','---','---','---','---','---'],
'ELEVATED ROOF DECKS':    ['---','---','YYY','YYY','---','YYN','YYY','---','---','---','YYY','YYY','---','---','---','---','---','---','---','---','---'],
'SOLAR PANELS':           ['---','YYN','---','---','YYY','---','---','---','---','---','YYY','---','YYY','---','---','---','---','---','---','---','---']
};

const SUBS_BASE = [{"id": "m0000", "div": "DIVISION 09", "divName": "FINISHES", "code": "099000 Painting", "company": "3-B'Z PAINTING CO.", "active": true, "contact": "Ben", "phone": "1 818 752 7613", "cell": "1 818 284 5946", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["099000 Painting", "099001 Painting Cabinets"]}, {"id": "m0001", "div": "DIVISION 03", "divName": "CONCRETE", "code": "033100 Structural Concrete", "company": "3CP, INC.", "active": true, "contact": "John Mideiros", "phone": "1 714 991 6900", "cell": "", "statusNote": "", "comments": "NO RESPONSE", "email": "", "bids": {}, "codes": ["033100 Structural Concrete"]}, {"id": "m0002", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "072100 Insulation", "company": "911 ATTIC INSULATION", "active": true, "contact": "", "phone": "(888) 202-8282", "cell": "", "statusNote": "NEW", "comments": "", "email": "911atticinsulation@gmail.com", "bids": {}, "codes": ["072100 Insulation"]}, {"id": "m0003", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "A & R JUNIOR GLASS INC", "active": true, "contact": "Sauceda Richardo", "phone": "work (323) 777-1344", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0004", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "A&A HVAC", "active": false, "contact": "Hafeez Abbasi", "phone": "424-43-59243", "cell": "", "statusNote": "", "comments": "NO RESPONSE", "email": "hafeezabbasi1973@gmail.com", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0005", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "A&M REFRIDGERATION", "active": true, "contact": "Eugene Manzano", "phone": "2132724968.0", "cell": "2134871131.0", "statusNote": "NEW", "comments": "", "email": "appletreecorp@ymail.com", "bids": {"17797 Camino De Yatasto": {"price": 172000.0, "received": "2026-03-31", "comments": "UPDATED BID"}, "807 6th Ave": {"price": 147300.0, "received": "2026-01-20", "comments": ""}, "15265 W Bestor Blvd": {"price": 133400.0, "received": "2026-01-20", "comments": ""}, "12979 Blairwood Dr": {"price": 164000.0, "received": "2026-03-04", "comments": ""}, "1134 Iliff St": {"price": 29700.0, "received": "2026-04-10", "comments": "2 BID OPTIONS ducted split heat pump system and one for a package unit"}}, "codes": ["230000 Hvac"]}, {"id": "m0006", "div": "DIVISION 21", "divName": "FIRE SUPPRESSION", "code": "211300 Fire Spinklers", "company": "A&S FIRE PROTECTION", "active": true, "contact": "Robert Charbonneau", "phone": "1 805 650 2505", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["211300 Fire Spinklers"]}, {"id": "m0007", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "A-1 CONCRETE READY-MIX, INC.", "active": true, "contact": "Beto Campos", "phone": "1 626 523 5222", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["030630 Concrete Slab"]}, {"id": "m0008", "div": "DIVISION 09", "divName": "FINISHES", "code": "092000 Gypsum Board", "company": "A-1 DRYWALL", "active": true, "contact": "", "phone": "1 805 647 9440", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["092000 Gypsum Board"]}, {"id": "m0009", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "A1 ALL AMERICAN ROOFING", "active": true, "contact": "Matthew Schwartz", "phone": "310.320.0224", "cell": "424.467.1222", "statusNote": "", "comments": "", "email": "matt@a1roofingcorp.com", "bids": {"52-60 Market St": {"price": 49060.62, "received": "2025-08-11", "comments": ""}, "Quadro Vecchio": {"price": 26672.75, "received": "2025-08-04", "comments": "Bid broken it out into two quotes: Flat roof and Sloped roof"}, "748 & 750 Palisades Dr": {"price": 31961.88, "received": "2025-08-07", "comments": ""}, "478 Wynola St": {"price": 21071.3, "received": "2025-09-15", "comments": ""}, "807 6th Ave": {"price": 53207.62, "received": "2025-10-28", "comments": "Discount $22000 with SPF system, the original number its with TPO system"}, "1080 El Medio Place": {"price": 110145.33, "received": "22/10/25", "comments": "Check;"}, "15265 W Bestor Blvd": {"price": 74269.09, "received": "2025-11-19", "comments": ""}, "1093 Palms Blvd": {"price": 32316.52, "received": "2025-11-26", "comments": ""}, "2429 Eastern Canal": {"price": 43308.74, "received": "2025-12-10", "comments": ""}, "16339 Akron": {"price": 69650.0, "received": null, "comments": "Includes waterproofing on roofing"}, "12979 Blairwood Dr": {"price": 185000.0, "received": "2026-03-03", "comments": ""}}, "codes": ["071000 Roofing", "073313 Green Roof"]}, {"id": "m0010", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "A1 TOTAL SERVICE PLUMBING", "active": true, "contact": "", "phone": "833-340-6322", "cell": "", "statusNote": "NEW", "comments": "", "email": "info@a1tsp.com", "bids": {}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0011", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "AAA PLUMBING", "active": true, "contact": "Mike", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "aaaplumbingsolutionsinc@gmail.com", "bids": {"213 OFW Waterfront": {"price": 130050.0, "received": "2025-08-04", "comments": ""}, "478 Wynola St": {"price": 27850.0, "received": "2025-09-12", "comments": "https://links.notification.intuit.com/ls/click?upn=u001.Hu9nToJLxsJSQR8ZHWn8Ib7JikYF6PNXv5VK-2BAfeSpVHPRNy-2BFDtJ-2BhNUfKXTverofrKjvXVKH4ba5KbTX-2BS4Z73Z6LrBxuE9bfDdb5i7Ijam0JtqtVMwWIe-2BgyQTeq9lK7FD2pNUxemg7cLQK3E8Ugyr-2BHf-2BmZrG69V0spfJX9YgzqaPkU-2FHiFBUTf4aBPSh-2BVkJRi02NPWfO0-2BiIkLrvdnS-2F842uIABKxM3Yd4Fki0nwAcaK1uSZl81Q1VwdR8IyrTi4WHxtNfWA20uA1cWA-3D-3DpHLQ_E3jX7UdwUvWW16GmiaKN7IBXUiBK0ekgQE1aiqjb-2BLwDjLmLF1ZY81IHLjZk-2FHMPolH-2BjylXIQFm5uv1Ti6arFaieCT7ceEk7ws2F1QWO0iLDGxQnA3osNVUfuVzxHV1PLM1HIoaxI-2BIFUgbhmhUgpdQi7L3mkfIaaMnmNtvp7bZ3riA0ZeIknudZ-2FvCBSjlfjaiaYeau7JOZgJekve8OmusRdPDJiXHc6hkzYgmeVmuHE8ooGTfO0y8H-2FmZ9zglmSqvDJ5qIHAzV4OfSNTdvL55b0DAaZhScCzdf42d3z-2FjQQTpM0UX2lmDW01UevYc5W9lwTvOOU8P40BMB-2FmdWiwHcYa1a-2Bf1X9D3febUdSPXHXxRNnHhPPov2a-2BhtGm2DEbfdbjepsLcCTzFBKuikE7fRMPcjw5SmOj65ldZ8iwmmgqyyfxX7d9ug21JL-2FYMF-2BKQFllV-2FG6T35imu6S2gDY5IG300OFsO2JbI3sgIokSBkQBl9gEFeohmYWfO2J15qMEnZMmFneYVFz7kIeFWuKLp80M21tVrtb4FH9pkE4UxTZLRGMHR0hPEJ22-2FOuvyKrT58My-2BynGvtiFSZrGM1shPa-2BqGC1RGStRQNfvmm5TRX-2B07oG26jM7gQjSWtEylt2dkMvZPWK7UdpTIsBYetpQUzg33ZOMKcswqThaT3-2BG2r19yf48-2Frb-2BfvyY9M-2BAGmNDq6tNbufhwby0c-2BCeVewaUwQfS2U-2BywyXIX35SCJQUihAOYdChs-2BURZAXBdJ3LNjwvu-2Bq1Koyki01I-2BPED2ohgGIGd7hSGcFKXgtsxt7R6HGweTCVBIFL121553bSN0guCmOGrLfwRLYWlODAhGoyaaw-2Fcg28xb-2FJOb-2BJ1tEEox4KorWFsEZGxBVlDYhwEgVy650Np3om1mupD5IQpP6q8QAUNTeavHa7Bb6AvKJZN0bWZVFbovahbeLh7ncX2ul317AenZ-2Bx7SVuVkuDqdyqynF6OpVBkYzQNeE1d-2Fw2xhEIx7PczE6MuC-2F3VQjEOMnbYRdzIczILODv0HUbjT5CF7WK1gWAK05uwc5CWs1LJV3zU7ocXMv8FLzkOB-2FET-2BBEEd1zQCbsh72zsShPJxyJ1rbM6GexMIEoYwSHD2Jt5XynhYRZSb0VTrc9OEhSyoQcY54pj7Egvx4Zeqdmhm11T5I4Hv1f3ptAgKRiW9s0mrz-2B2tJUws-2BUDFq3dJkTBI9VQyiyeHLHG-2F7LFa3i4xe7uyu-2BbZjSdamcbmVIlAUcFfwCx0-2F8fq5PQczckOdHg3vu6S2aWfzDPaFNHzvLrJLmU0i9UqpV4eL08ngWbliwKVMW-2B2tGvgiezjDa1yn1kRtbkabRldjMPSLNpZzt-2FW-2F5u6MewVEkNxIhpGSbKm8-3D"}, "17797 Camino De Yatasto": {"price": 109700.0, "received": "2026-04-14", "comments": ""}, "12979 Blairwood Dr": {"price": 130400.0, "received": "2026-03-10", "comments": ""}}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0012", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "022600 Asbestos", "company": "ABATEC ENVIRONMENTAL", "active": true, "contact": "Dennis Hanna", "phone": "1 949 380 8995", "cell": "1 949 279 2245", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["022600 Asbestos"]}, {"id": "m0013", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "ABSOLUTE ELECTRIC", "active": true, "contact": "Josh Rodelo", "phone": "1 805 551 2625", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0014", "div": "DIVISION 11", "divName": "EQUIPMENT", "code": "113000 Residential Equipment", "company": "ABT ELECTRONICS", "active": true, "contact": "Appliances", "phone": "847.967.8830", "cell": "847.544.2787", "statusNote": "", "comments": "", "email": "rkhoury@abt.com", "bids": {}, "codes": ["113000 Residential Equipment"]}, {"id": "m0015", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "ACCENT BUILDERS", "active": true, "contact": "Dean LeMar", "phone": "1 818 361 7080", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["030630 Concrete Slab", "131100 Swimming Pool/Spa/Fountain"]}, {"id": "m0016", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081005- Shower enclosures", "company": "ACCESS CUSTOM GARAGE DOORS", "active": true, "contact": "Sarah Sun", "phone": "1 800 994 3643", "cell": "1 818 518 4022", "statusNote": "", "comments": "New email address", "email": "office@accessgaragedoor.com", "bids": {}, "codes": ["081005- Shower enclosures"]}, {"id": "m0017", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "015150 Deputy Inspections", "company": "ACCUTECH INC.", "active": true, "contact": "Jim Feeney", "phone": "1 805 492 3455", "cell": "1 805 479 0656", "statusNote": "", "comments": "", "email": "accutechinc@gmail.com", "bids": {}, "codes": ["015150 Deputy Inspections"]}, {"id": "m0018", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "269900 Electric Fixtures", "company": "ACS CONSTRUCTION", "active": true, "contact": "David Navarro", "phone": "1 805 962 1200", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["269900 Electric Fixtures", "481400 Solar Energy Electrical Power Generation Equipment"]}, {"id": "m0019", "div": "DIVISION 05", "divName": "METALS", "code": "055000 Metal Fabricators", "company": "ACTION COMPANIES", "active": true, "contact": "Eddie Razo", "phone": "1 818 365 3241", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["055000 Metal Fabricators"]}, {"id": "m0020", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "ACTION ROOFING", "active": true, "contact": "Kumar Atterbury", "phone": "1 805 966 3696", "cell": "1 805 896 4067", "statusNote": "", "comments": "", "email": "kumar@aroofing.com", "bids": {}, "codes": ["071000 Roofing"]}, {"id": "m0021", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "ADVANCED CLIMATE SEAL SYSTEMS", "active": true, "contact": "Matt Morrison", "phone": "1 760 777 2570", "cell": "1 760 845 9315", "statusNote": "", "comments": "", "email": "sales@climateseal.com", "bids": {}, "codes": ["030630 Concrete Slab"]}, {"id": "m0022", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "481400 Solar Energy Electrical Power Generation Equipment", "company": "ADVANCED SOLAR ELECTRIC", "active": true, "contact": "", "phone": "1 805 214 9960", "cell": "", "statusNote": "", "comments": "BOUNCED BACK", "email": "info@ase4u.com", "bids": {"12979 Blairwood Dr": {"price": 35413.56, "received": "2026-02-05", "comments": ""}}, "codes": ["481400 Solar Energy Electrical Power Generation Equipment"]}, {"id": "m0023", "div": "DIVISION 12", "divName": "FURNISHINGS", "code": "122000 Window Treatments", "company": "AERO SHADES", "active": true, "contact": "Jack Pitson", "phone": "1 323 655 2411", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["122000 Window Treatments"]}, {"id": "m0024", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "AERODYNAMIX", "active": false, "contact": "Rod Greene", "phone": "1 888 707 HVAC", "cell": "1 310 395 2482", "statusNote": "", "comments": "Mail needs to be updated", "email": "rod@aerodynamixusa.com", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0025", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "022600 Asbestos", "company": "AFG", "active": true, "contact": "Mohammeh Hussain", "phone": "1 818 848 4803", "cell": "1 818 378 6896", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["022600 Asbestos"]}, {"id": "m0026", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "AGB Woodworks", "active": true, "contact": "Albert Borgo", "phone": "310-908-6499", "cell": "", "statusNote": "", "comments": "", "email": "borgooey@gmail.com", "bids": {"723 OFW": {"price": 36177.0, "received": "2025-06-13", "comments": ""}}, "codes": ["064100 Cabinets"]}, {"id": "m0027", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "AIR AL", "active": true, "contact": "Gideon Eliyahu", "phone": "1 323 934 3838", "cell": "", "statusNote": "CALL", "comments": "", "email": "airalinc@aol.com", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0028", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "AIR CREW HEATING & AIR CONDITIONING", "active": true, "contact": "", "phone": "(661)430 6644", "cell": "", "statusNote": "NEW", "comments": "", "email": "aircrewhvac@gmail.com", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0029", "div": "DIVISION 21", "divName": "FIRE SUPPRESSION", "code": "211300 Fire Spinklers", "company": "Aj Fire Protection", "active": false, "contact": "Amado", "phone": "8184485560.0", "cell": "", "statusNote": "", "comments": "", "email": "ajfirepro1@gmail.com", "bids": {"52-60 Market St": {"price": 12750.0, "received": "2025-02-05", "comments": "Bid for 60 Market St"}, "Quadro Vecchio": {"price": 17500.0, "received": "2025-07-26", "comments": "LEFT VM"}, "723 OFW": {"price": 130750.0, "received": "2025-04-11", "comments": ""}}, "codes": ["211300 Fire Spinklers"]}, {"id": "m0030", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "ALEX & ALEX ELECTRICAL SERVICES", "active": true, "contact": "", "phone": "310.905.5050", "cell": "", "statusNote": "", "comments": "NEW", "email": "info@alexelectrician.com", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0031", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "ALEXANDER EXCAVATION - CONCRETE", "active": true, "contact": "3107151451.0", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["024000 Demolition"]}, {"id": "m0032", "div": "DIVISION 10", "divName": "SPECIALTIES", "code": "103000 Fireplace", "company": "ALEXANDER FIREPLACE", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {"Quadro Vecchio": {"price": 18601.0, "received": "2025-07-08", "comments": ""}}, "codes": ["103000 Fireplace"]}, {"id": "m0033", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "ALL PLASTER SYSTEMS", "active": true, "contact": "Mike Gates", "phone": "1 818 642 6329", "cell": "", "statusNote": "", "comments": "", "email": "allplastersystems@gmail.com", "bids": {}, "codes": ["092400 Stucco"]}, {"id": "m0034", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081005- Shower enclosures", "company": "ALL STAR GARAGE DOOR", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["081005- Shower enclosures"]}, {"id": "m0035", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071010 Waterproofing", "company": "ALL STATE WATERPROOFING", "active": false, "contact": "Luis Hernandez", "phone": "1 213 383 1968", "cell": "", "statusNote": "", "comments": "", "email": "luish@allstate-engineering.net", "bids": {}, "codes": ["071010 Waterproofing"]}, {"id": "m0036", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071010 Waterproofing", "company": "ALL WEATHER DECK", "active": true, "contact": "Mike Davoodi", "phone": "(310) 836-0800", "cell": "", "statusNote": "NEW", "comments": "", "email": "allweathercompany@gmail.com", "bids": {"6537 Topanga Canyon": {"price": 69660.0, "received": null, "comments": ""}, "12979 Blairwood Dr": {"price": 79020.0, "received": "2026-02-16", "comments": ""}}, "codes": ["071010 Waterproofing"]}, {"id": "m0037", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "ALL-POWERFULL", "active": true, "contact": "David Woollen", "phone": "1 310 641 9675", "cell": "1 310 265 3398", "statusNote": "CALL", "comments": "", "email": "d_woollen@hotmail.com", "bids": {}, "codes": ["220000 Plumbing Rough & Finish", "223200 Domestic Water Filtration Equipment", "224000 Plumbing Fixtures", "334000 Stormwater management-LID"]}, {"id": "m0038", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "262000 Low Voltage", "company": "ALL-PRO COMMUNICATIONS TECHNOLOGIES", "active": true, "contact": "Gilbert Torres", "phone": "1 909 596 7051", "cell": "1 626 506 5259", "statusNote": "", "comments": "", "email": "gilbertt@allprocti.com", "bids": {}, "codes": ["262000 Low Voltage"]}, {"id": "m0039", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "022600 Asbestos", "company": "ALLIED INDUSTRIES", "active": true, "contact": "Mike Jabbour", "phone": "1 818 781 2490", "cell": "1 805 804 7498", "statusNote": "", "comments": "", "email": "mjabbour@alliedlead.com", "bids": {}, "codes": ["022600 Asbestos"]}, {"id": "m0040", "div": "DIVISION 21", "divName": "FIRE SUPPRESSION", "code": "211300 Fire Spinklers", "company": "ALPHA SYSTEMS", "active": true, "contact": "Jason Pivnik", "phone": "1 323 227 0005", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["211300 Fire Spinklers"]}, {"id": "m0041", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081005- Shower enclosures", "company": "ALPINE DOOR & TRIM", "active": true, "contact": "Noalla Ritzka", "phone": "", "cell": "", "statusNote": "", "comments": "New email address", "email": "info@alpinedoorandtrim.com", "bids": {}, "codes": ["081005- Shower enclosures"]}, {"id": "m0042", "div": "DIVISION 09", "divName": "FINISHES", "code": "096400 Wood Flooring", "company": "ALSI WOOD FLOORS", "active": true, "contact": "Moe Alsi", "phone": "310 204 4000", "cell": "", "statusNote": "", "comments": "", "email": "alsiwoodfloors@gmail.com", "bids": {"429 Sherman Canal": {"price": 24933.0, "received": "2025-04-07", "comments": ""}}, "codes": ["096400 Wood Flooring"]}, {"id": "m0043", "div": "DIVISION 08", "divName": "OPENINGS", "code": "086000 Skylights", "company": "ALUMINEX", "active": true, "contact": "Susan", "phone": "1 951 353 1101", "cell": "", "statusNote": "", "comments": "", "email": "office@aluminexinc.com, marilynp@aluminexinc.com, pm@aluminexinc.com", "bids": {"52-60 Market St": {"price": 3294.0, "received": "2025-05-23", "comments": ""}, "16339 Akron": {"price": 4144.0, "received": null, "comments": "RE-SEND"}}, "codes": ["086000 Skylights"]}, {"id": "m0044", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "AM Cabinets", "active": true, "contact": "Carlos Juarez", "phone": "310-532-1919", "cell": "", "statusNote": "", "comments": "", "email": "carlosj@amcabinets.com", "bids": {}, "codes": ["064100 Cabinets"]}, {"id": "m0045", "div": "DIVISION 03", "divName": "CONCRETE", "code": "033100 Structural Concrete", "company": "AMALFI CONSTRUCTION GROUP", "active": true, "contact": "Pablo Becerra", "phone": "818 974 1114", "cell": "", "statusNote": "", "comments": "", "email": "pablo.becerra@gmail.com", "bids": {}, "codes": ["033100 Structural Concrete"]}, {"id": "m0046", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "022600 Asbestos", "company": "AMERICAN ANALYTICAL", "active": true, "contact": "Matthew Massey", "phone": "1 800 991 LABS", "cell": "1 714 379 0838", "statusNote": "", "comments": "", "email": "mmasseyamericananalytical@msn.com", "bids": {}, "codes": ["022600 Asbestos"]}, {"id": "m0047", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "076000 Flashing & Sheet Metal", "company": "AMERICAN SHEET METAL", "active": true, "contact": "", "phone": "(714) 780-0155", "cell": "(714) 780 - 0155", "statusNote": "", "comments": "", "email": "elic@asmsheetmetal.com", "bids": {}, "codes": ["076000 Flashing & Sheet Metal", "074619 Steel Siding"]}, {"id": "m0048", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "017423 Final Clean-up", "company": "AMERICANFINALCLEAN@YAHOO.COM", "active": true, "contact": "Kristena Bernal", "phone": "(909) 948-8787", "cell": "www.finalclean.com", "statusNote": "", "comments": "", "email": "americanfinalclean@yahoo.com", "bids": {}, "codes": ["017423 Final Clean-up"]}, {"id": "m0049", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "AMG ELECTRIC", "active": true, "contact": "ALEX", "phone": "4242241250.0", "cell": "", "statusNote": "", "comments": "", "email": "alex37mg75@gmail.com", "bids": {"17797 Camino De Yatasto": {"price": 71120.0, "received": "2026-03-26", "comments": ""}, "807 6th Ave": {"price": 54090.0, "received": "2025-12-03", "comments": ""}, "15265 W Bestor Blvd": {"price": 92730.0, "received": "2025-11-17", "comments": ""}, "1093 Palms Blvd": {"price": 30280.0, "received": "2025-11-21", "comments": ""}, "16339 Akron": {"price": 49780.0, "received": "2025-12-28", "comments": ""}}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0050", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "AMP ELECTRICAL", "active": false, "contact": "http://www.amp-ec.com/", "phone": "818-253-5752", "cell": "818-391-3625", "statusNote": "", "comments": "BOUNCED BACK", "email": "info@ampelectricalcontractor.com", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0051", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "AMPAN PARKS MECHANICAL", "active": false, "contact": "Keith Price", "phone": "1 310 427 7023", "cell": "", "statusNote": "EMAIL NEEDS TO BE UPDATED", "comments": "", "email": "keith.price@ampam.com", "bids": {}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0052", "div": "DIVISION 05", "divName": "METALS", "code": "051200 Structural Steel", "company": "ANDERSEN WELDING", "active": false, "contact": "Zach Andersen", "phone": "310-672-0920", "cell": "", "statusNote": "", "comments": "", "email": "zach.a@andersenmp.com", "bids": {}, "codes": ["051200 Structural Steel"]}, {"id": "m0053", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081000 Exterior Doors & Windows Supply", "company": "ANDERSON MOULDING INC.", "active": true, "contact": "Lance Young", "phone": "951 239 2937", "cell": "", "statusNote": "", "comments": "Bid for windows", "email": "lance@andersonmoulding.com", "bids": {"52-60 Market St": {"price": 112256.55, "received": "2025-01-22", "comments": "Bid for windows"}, "Quadro Vecchio": {"price": 131026.14, "received": "2025-08-06", "comments": "Bid for windows"}, "429 Sherman Canal": {"price": 33591.18, "received": "2025-08-12", "comments": ""}, "723 OFW": {"price": 343908.48, "received": "2025-08-12", "comments": ""}, "478 Wynola St": {"price": 43361.13, "received": "2025-09-09", "comments": ""}, "6537 Topanga Canyon": {"price": 68883.49, "received": "2026-02-17", "comments": "Scope adjusted due to fabrication limits and door/transom constraints. Future cost-optimization options noted."}, "865 N Oreo Pl": {"price": 231460.56, "received": "2025-10-03", "comments": ""}, "807 6th Ave": {"price": 283128.66, "received": null, "comments": "+$6,679.39 SKYLIGHTS"}, "1080 El Medio Place": {"price": 223306.13, "received": "2025-10-27", "comments": "Check;Window 03 was too large to build as a single unit (the 3-panel doors are made in their multi-slide series\u2026and I quoted the 2-panel doors ) +$16,777.48 doors +$6,679.39 SKYLIGHTS"}, "15265 W Bestor Blvd": {"price": 139673.34, "received": "2025-11-13", "comments": ""}, "1093 Palms Blvd": {"price": 856.0, "received": "2025-12-05", "comments": ""}, "213 OFW Waterfront": {"price": 11194.5, "received": "2026-06-19", "comments": ""}}, "codes": ["081000 Exterior Doors & Windows Supply", "081002 Interior Doors & Frames", "086000 Skylights", "081001 Exterior Doors & Windows Installation"]}, {"id": "m0054", "div": "DIVISION 09", "divName": "FINISHES", "code": "092000 Gypsum Board", "company": "ANNING-JOHNSON COMPANY", "active": false, "contact": "Anthony Sanchez", "phone": "1 626 369 7131", "cell": "", "statusNote": "", "comments": "NOT RESIDENTIAL", "email": "asanchez@anningjohnson.com", "bids": {}, "codes": ["092000 Gypsum Board"]}, {"id": "m0055", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Material", "company": "ANTONIELLO & SONS", "active": true, "contact": "Tony Antoniello Jr.", "phone": "1 818 458 8530", "cell": "", "statusNote": "", "comments": "", "email": "tonyjr@antoniello.net", "bids": {}, "codes": ["096000 Tile - Material"]}, {"id": "m0056", "div": "DIVISION 05", "divName": "METALS", "code": "051200 Structural Steel", "company": "ANVIL", "active": true, "contact": "Marte Manansala", "phone": "1 310 329 5811", "cell": "", "statusNote": "", "comments": "", "email": "martem@anvilsteel.com", "bids": {"12979 Blairwood Dr": {"price": 31450.0, "received": "2026-03-05", "comments": ""}}, "codes": ["051200 Structural Steel"]}, {"id": "m0057", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "APPLIED", "active": false, "contact": "Oren Prosser/ Brad Jurecka", "phone": "1 818 991 4646", "cell": "1 818 519 4300", "statusNote": "", "comments": "Email needs to be updated", "email": "oren@appliedconcrete.com, brad@appliedconcrete.com", "bids": {}, "codes": ["030630 Concrete Slab", "030650 Finish Concrete", "031113 Shoring", "042200 Concrete Masonry Unit", "033100 Structural Concrete"]}, {"id": "m0058", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "APPTEK INC.", "active": true, "contact": "Scott Lidster", "phone": "310 749 5381", "cell": "858 875 1854", "statusNote": "", "comments": "", "email": "scott@apptekstucco.com", "bids": {"429 Sherman Canal": {"price": 95075.0, "received": "2025-08-03", "comments": ""}, "748 & 750 Palisades Dr": {"price": 132515.0, "received": null, "comments": "Bid by 09/05"}, "6537 Topanga Canyon": {"price": 24255.0, "received": "24/02/2026", "comments": ""}, "17797 Camino De Yatasto": {"price": 113485.0, "received": null, "comments": ""}, "807 6th Ave": {"price": 47835.0, "received": "2025-10-16", "comments": "Discount request acepted $46,195"}, "4565 Dundee Drive": {"price": 39070.0, "received": "2025-11-24", "comments": ""}, "1093 Palms Blvd": {"price": 52825.0, "received": "2025-11-25", "comments": ""}, "2429 Eastern Canal": {"price": 75660.0, "received": "2025-12-04", "comments": ""}, "16339 Akron": {"price": 29545.0, "received": null, "comments": "Building walls & Clean Up and Debris Hauling"}, "1134 Iliff St": {"price": 31710.0, "received": "2026-04-07", "comments": ""}}, "codes": ["092400 Stucco"]}, {"id": "m0059", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "ARACADIA ARCHITECTURAL PRODUCTS, INC.", "active": true, "contact": "Margie Alonso", "phone": "(323) 908-5472", "cell": "", "statusNote": "", "comments": "New email address", "email": "malonso@arcadiainc.com, cbauza@arcadiainc.com", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0060", "div": "DIVISION 09", "divName": "FINISHES", "code": "096600 Terrazzo", "company": "ARCADIAN", "active": true, "contact": "Theodore Lambros", "phone": "1 626 284 1563", "cell": "1 626 284 6957", "statusNote": "", "comments": "", "email": "ted@arcadiandevelopment.com", "bids": {}, "codes": ["096600 Terrazzo"]}, {"id": "m0061", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "ARCHILECTRIC", "active": true, "contact": "Diego Pascarelli", "phone": "310-748-4904", "cell": "", "statusNote": "", "comments": "NEW", "email": "diegopascarelli@archilectric.com", "bids": {"12979 Blairwood Dr": {"price": 114390.0, "received": "2026-03-05", "comments": "$15.50 PER SF"}}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0062", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "ARCHITECTURAL PRODUCTS", "active": true, "contact": "Henry Camilleri", "phone": "310-613-4627", "cell": "", "statusNote": "", "comments": "", "email": "henry@architecturalpro.com", "bids": {"2429 Eastern Canal": {"price": 23468.0, "received": "2025-12-02", "comments": ""}}, "codes": ["064100 Cabinets"]}, {"id": "m0063", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "076000 Flashing & Sheet Metal", "company": "ARCHITECTURAL SHEET METAL", "active": true, "contact": "Johnny Meloni", "phone": "1 805 388 9272", "cell": "", "statusNote": "", "comments": "VOICE MAIL", "email": "johnny@arsheetmetal.com", "bids": {}, "codes": ["076000 Flashing & Sheet Metal"]}, {"id": "m0064", "div": "DIVISION 12", "divName": "FURNISHINGS", "code": "122000 Window Treatments", "company": "ARCHITECTURAL WINDOW SHADES", "active": true, "contact": "Tom Roberson", "phone": "1 626 578 1936", "cell": "", "statusNote": "", "comments": "", "email": "awshades@pacbell.net", "bids": {}, "codes": ["122000 Window Treatments"]}, {"id": "m0065", "div": "DIVISION 03", "divName": "CONCRETE", "code": "033100 Structural Concrete", "company": "ART & SON CONSTRUCTION, INC.", "active": true, "contact": "Concrete/Concrete  Reinforcing", "phone": "818.367.2703", "cell": "", "statusNote": "", "comments": "NO RESPONSE", "email": "artnsonconstruction@gmail.com", "bids": {}, "codes": ["033100 Structural Concrete"]}, {"id": "m0066", "div": "DIVISION 05", "divName": "METALS", "code": "051200 Structural Steel", "company": "ART WILLISON CONSTRUCTION", "active": true, "contact": "", "phone": "1 805 302 5689", "cell": "", "statusNote": "", "comments": "", "email": "awcsteel@msn.com", "bids": {}, "codes": ["051200 Structural Steel"]}, {"id": "m0067", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "077700 Waterproofing Build. Wrap", "company": "ARWP", "active": true, "contact": "Justin", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "cesar.renteria@arwp.com, justin@arwp.com", "bids": {"52-60 Market St": {"price": 35350.0, "received": null, "comments": ""}}, "codes": ["077700 Waterproofing Build. Wrap", "071010 Waterproofing"]}, {"id": "m0068", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081004 Garage Doors", "company": "ASAP GARAGE DOORS & GATES", "active": true, "contact": "", "phone": "(888) 770-7229", "cell": "", "statusNote": "NEW", "comments": "", "email": "asapgaragedoorandgate@gmail.com", "bids": {}, "codes": ["081004 Garage Doors"]}, {"id": "m0069", "div": "DIVISION 03", "divName": "CONCRETE", "code": "033100 Structural Concrete", "company": "ASHER CONSTRUCTION", "active": true, "contact": "John", "phone": "", "cell": "", "statusNote": "Does framing too", "comments": "", "email": "john@asherconstruction.net", "bids": {"807 6th Ave": {"price": 415653.0, "received": "2025-12-17", "comments": ""}, "12979 Blairwood Dr": {"price": 884573.0, "received": "2026-02-06", "comments": ""}, "1134 Iliff St": {"price": 75730.0, "received": "2026-04-13", "comments": ""}}, "codes": ["033100 Structural Concrete", "061000 Rough Carpentry"]}, {"id": "m0070", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "321300 Ridgid Paving", "company": "ASPHALT PROFESSIONALS", "active": true, "contact": "Tom Hodge", "phone": "1 805 375 2753", "cell": "1 805 432 2605", "statusNote": "", "comments": "", "email": "tom@asphaltprofessionals.com", "bids": {}, "codes": ["321300 Ridgid Paving"]}, {"id": "m0071", "div": "DIVISION 03", "divName": "CONCRETE", "code": "031113 Shoring", "company": "AUGUST CONSTRUCTION & SHORING, INC", "active": false, "contact": "", "phone": "(424) 270-0370 ext. 302", "cell": "", "statusNote": "", "comments": "", "email": "jim@geosupport.com", "bids": {}, "codes": ["031113 Shoring", "033100 Structural Concrete"]}, {"id": "m0072", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "AURORA PLASTERING, INC.", "active": true, "contact": "", "phone": "1 818 364 9496", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {"4565 Dundee Drive": {"price": 39070.0, "received": "2025-11-24", "comments": ""}}, "codes": ["092400 Stucco"]}, {"id": "m0073", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "AUTHENTIC WOODWORKS", "active": true, "contact": "Mike Gill", "phone": "818-359-7368", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["064100 Cabinets"]}, {"id": "m0074", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081000 Exterior Doors & Windows Supply", "company": "AVALON DOOR & WINDOW-LA", "active": true, "contact": "Bob Balyzsak", "phone": "", "cell": "", "statusNote": "", "comments": "ONLY RESIDENTIAL", "email": "bob@avalondoor.com", "bids": {"478 Wynola St": {"price": 30897.19, "received": "2025-09-26", "comments": "ONLY WINDOWS"}, "807 6th Ave": {"price": 423432.63, "received": "2025-10-31", "comments": "Discount request declined"}, "1080 El Medio Place": {"price": 343462.78, "received": "2025-10-17", "comments": "check;the contractor comment some detail regarding energy code"}, "15265 W Bestor Blvd": {"price": 221682.0, "received": "2025-11-01", "comments": ""}, "4565 Dundee Drive": {"price": 113259.0, "received": "2025-11-04", "comments": ""}, "2429 Eastern Canal": {"price": 79451.36, "received": "2025-11-26", "comments": ""}, "16339 Akron": {"price": 130000.0, "received": null, "comments": "Bottom line is $146,000, Fleetwood is giving very generous fire discounts on the burn jobs, so deduct $16,000 and call it $130,000."}}, "codes": ["081000 Exterior Doors & Windows Supply", "081005- Shower enclosures"]}, {"id": "m0075", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071010 Waterproofing", "company": "AVM", "active": true, "contact": "Amir Rudyan", "phone": "1 818 888 0050", "cell": "1 818 424 0082", "statusNote": "", "comments": "VOICE MAIL", "email": "amir@avmindustries.com", "bids": {}, "codes": ["071010 Waterproofing"]}, {"id": "m0076", "div": "DIVISION 12", "divName": "FURNISHINGS", "code": "122000 Window Treatments", "company": "AWS", "active": true, "contact": "Nick Tolentino", "phone": "1 626 578 1936", "cell": "", "statusNote": "", "comments": "", "email": "nick@awsshades.com", "bids": {}, "codes": ["122000 Window Treatments"]}, {"id": "m0077", "div": "DIVISION 21", "divName": "FIRE SUPPRESSION", "code": "211300 Fire Spinklers", "company": "AXIS FIRE PROTECTION, INC.", "active": true, "contact": "Viggen Garibian", "phone": "1 818 546 2947", "cell": "", "statusNote": "", "comments": "", "email": "axisfp@aol.com", "bids": {}, "codes": ["211300 Fire Spinklers"]}, {"id": "m0078", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "B RADIANT", "active": true, "contact": "Brad Cote, Ron Rodriguez", "phone": "1 310 937 1800", "cell": "", "statusNote": "CALL", "comments": "", "email": "bradcote@b-radiant.com, ron@b-radiant.com", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0079", "div": "DIVISION 09", "divName": "FINISHES", "code": "074619 Steel Siding", "company": "B&G SHEET METAL", "active": true, "contact": "Bob Ellingsworth", "phone": "626.444.8566", "cell": "", "statusNote": "", "comments": "NO RESIDENTIAL PROJECTS", "email": "estimating@bgsheetmetal.com", "bids": {}, "codes": ["074619 Steel Siding"]}, {"id": "m0080", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "B&M", "active": true, "contact": "Bruce Arikawa", "phone": "1 805 581 5480", "cell": "1 805 432 0297", "statusNote": "", "comments": "NO PICK UP THE PHONE", "email": "bruce@bamconcrete.com", "bids": {}, "codes": ["030630 Concrete Slab", "030650 Finish Concrete", "031113 Shoring", "033100 Structural Concrete", "042200 Concrete Masonry Unit"]}, {"id": "m0081", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "062000 Finish Carpentry", "company": "B. ROBLEY", "active": true, "contact": "Barry Robley", "phone": "1 626 794 5112", "cell": "1 818 625 4683", "statusNote": "CALL", "comments": "", "email": "bsrobley@sbcglobal.net", "bids": {}, "codes": ["062000 Finish Carpentry", "077700 Waterproofing Build. Wrap", "074623 Wood Siding"]}, {"id": "m0082", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "015150 Deputy Inspections", "company": "B.H. COMMUNITY DEVELOPMENT", "active": true, "contact": "Trent Baker", "phone": "1 310 285 1169", "cell": "", "statusNote": "", "comments": "", "email": "tbaker@beverlyhills.org", "bids": {}, "codes": ["015150 Deputy Inspections"]}, {"id": "m0083", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "015150 Deputy Inspections", "company": "B.H. FIRE DEPARTMENT", "active": true, "contact": "Eddie Gamboa", "phone": "1 310 281 2717", "cell": "", "statusNote": "", "comments": "", "email": "egamboa@beverlyhills.org", "bids": {}, "codes": ["015150 Deputy Inspections"]}, {"id": "m0084", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071010 Waterproofing", "company": "BANCROFT", "active": true, "contact": "Matt Bancroft", "phone": "1 818 992 4627", "cell": "1 805 732 9087", "statusNote": "", "comments": "NO RESPONSE", "email": "estimates@bancroftinc.com, bancroftconstruction@hotmail.com", "bids": {"865 N Oreo Pl": {"price": 163064.0, "received": "2025-11-18", "comments": ""}, "15265 W Bestor Blvd": {"price": 187394.0, "received": null, "comments": "Includes all"}, "1093 Palms Blvd": {"price": 112684.0, "received": "2025-12-03", "comments": "Includes doors, windows, deck waterproofing, shower and house wrap"}, "2429 Eastern Canal": {"price": 71208.0, "received": null, "comments": "INCLUDE WATERPROOFING FOR THE WHOLE HOUSE, WINDOWS,DOORS, BATHROOM"}}, "codes": ["071010 Waterproofing", "077700 Waterproofing Build. Wrap", "071000 Roofing", "076000 Flashing & Sheet Metal"]}, {"id": "m0085", "div": "DIVISION 05", "divName": "METALS", "code": "051200 Structural Steel", "company": "BANKS WELDING AND FABRICATION", "active": true, "contact": "DOUG BANKS", "phone": "310.670.7617", "cell": "310.628.8973", "statusNote": "CALL", "comments": "", "email": "bankswelding@sbcglobal.net", "bids": {}, "codes": ["051200 Structural Steel"]}, {"id": "m0086", "div": "DIVISION 10", "divName": "SPECIALTIES", "code": "103000 Fireplace", "company": "BARBEQUES GALORE", "active": true, "contact": "Vince Harling", "phone": "1 310 914 9693", "cell": "", "statusNote": "", "comments": "BBQ  PROVIDOR", "email": "10131sd@bbqgalore.com", "bids": {}, "codes": ["103000 Fireplace"]}, {"id": "m0087", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "BARR COMMERCIAL DOOR", "active": false, "contact": "Tom Sutter", "phone": "1 818 771 0147", "cell": "", "statusNote": "", "comments": "", "email": "tsutter@barrdoor.com", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0088", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "BARRY STRATTON ROBLEY", "active": true, "contact": "Barry Robley", "phone": "1 626 794 5112", "cell": "1 818 625 4683", "statusNote": "", "comments": "NO RESPONSE", "email": "bsrobley@sbcglobal.net", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0089", "div": "DIVISION 12", "divName": "FURNISHINGS", "code": "122000 Window Treatments", "company": "BAY SCREENS & SHADES", "active": true, "contact": "Edgar Sanchez/ Greg Amato", "phone": "1 310 828 7998", "cell": "1 310 488 7836", "statusNote": "", "comments": "", "email": "edgar@bayscreensinc.com", "bids": {}, "codes": ["122000 Window Treatments"]}, {"id": "m0090", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "062000 Finish Carpentry", "company": "BDS CONSTRUCTION", "active": false, "contact": "Brian Sieck", "phone": "1 805 455 4055", "cell": "", "statusNote": "", "comments": "", "email": "bsieck@cox.net", "bids": {}, "codes": ["062000 Finish Carpentry"]}, {"id": "m0091", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071010 Waterproofing", "company": "BEACH CITIES ROOFING", "active": true, "contact": "MIKE DUBY", "phone": "(949) 329-9981", "cell": "", "statusNote": "", "comments": "", "email": "beachcitiesroofing@gmail.com", "bids": {}, "codes": ["071010 Waterproofing", "071000 Roofing"]}, {"id": "m0092", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "077700 Waterproofing Build. Wrap", "company": "Beach City Water Proofing", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "mike@bcrpro.com", "bids": {"429 Sherman Canal": {"price": 27463.0, "received": "2025-07-28", "comments": ""}, "748 & 750 Palisades Dr": {"price": 56943.0, "received": "2025-07-30", "comments": ""}}, "codes": ["077700 Waterproofing Build. Wrap"]}, {"id": "m0093", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "BEESON MASONRY", "active": true, "contact": "www.beesonmasonry.com", "phone": "561.724.1350", "cell": "661.724.1092", "statusNote": "", "comments": "NO PICK UP", "email": "beesonmasonry@gmail.com", "bids": {"Quadro Vecchio": {"price": 11687.5, "received": "2025-08-04", "comments": ""}}, "codes": ["030630 Concrete Slab"]}, {"id": "m0094", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "BELLONIRIS PLUMBING", "active": true, "contact": "Silvestre Bellorinis", "phone": "3104629881.0", "cell": "", "statusNote": "", "comments": "", "email": "bellorinisplumbing@gmail.com", "bids": {"6537 Topanga Canyon": {"price": 61185.0, "received": "2026-02-11", "comments": ""}}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0095", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "BENCHMARK", "active": false, "contact": "Jay Adams", "phone": "1 310 313 7274", "cell": "", "statusNote": "", "comments": "", "email": "jay@thebenchmark.us", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation", "087000 Finish Hardware"]}, {"id": "m0096", "div": "DIVISION 05", "divName": "METALS", "code": "051200 Structural Steel", "company": "BERGER STEEL", "active": true, "contact": "", "phone": "916-640-8778", "cell": "", "statusNote": "NEW", "comments": "", "email": "info@bergersteel.com", "bids": {}, "codes": ["051200 Structural Steel"]}, {"id": "m0097", "div": "DIVISION 31", "divName": "EARTHWORK", "code": "312300 Excavation & Backfill", "company": "BEST", "active": true, "contact": "Raffy Estacio", "phone": "1 818 366 3500", "cell": "1 805 402 2402", "statusNote": "", "comments": "", "email": "restacio7@gmail.com", "bids": {}, "codes": ["312300 Excavation & Backfill", "312500 Erosion Controls", "334000 Stormwater management-LID"]}, {"id": "m0098", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "BEST BUY METALS", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["071000 Roofing"]}, {"id": "m0099", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "BEST DEMO", "active": true, "contact": "Javier Perez", "phone": "81-253-6200", "cell": "", "statusNote": "", "comments": "", "email": "info@bestdemo.org", "bids": {"807 6th Ave": {"price": 19790.0, "received": "2025-10-07", "comments": ""}}, "codes": ["024000 Demolition"]}, {"id": "m0100", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "BEST INC.", "active": false, "contact": "Darrell French", "phone": "1 310 380 6060", "cell": "1 310 345 3934", "statusNote": "", "comments": "", "email": "info@bestcontractingservices.com", "bids": {}, "codes": ["071000 Roofing"]}, {"id": "m0101", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "BH KRUPER", "active": false, "contact": "Eli Shtykan", "phone": "1 818 343 0016", "cell": "", "statusNote": "", "comments": "", "email": "russel@bhkruper.com, eli@bhkruper.com", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation", "058000 Glazing", "087000 Finish Hardware"]}, {"id": "m0102", "div": "DIVISION 09", "divName": "FINISHES", "code": "093200 Elevated Roof Top Decks", "company": "BISON PEDESTAL SYTEM", "active": true, "contact": "JOHNNY KNIGHT", "phone": "818-727-1780", "cell": "818-437-4557", "statusNote": "", "comments": "", "email": "johnny@elevateddecksystems.com, kimberly@elevateddecksystems.com", "bids": {}, "codes": ["093200 Elevated Roof Top Decks"]}, {"id": "m0103", "div": "DIVISION 03", "divName": "CONCRETE", "code": "033100 Structural Concrete", "company": "BLAHA", "active": true, "contact": "Matthew Blaha", "phone": "1 661 799 1618", "cell": "", "statusNote": "", "comments": "EMAIL UPDATED", "email": "office@blahaconcrete.com", "bids": {}, "codes": ["033100 Structural Concrete"]}, {"id": "m0104", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "BOB WARD ELECTRIC INC.", "active": false, "contact": "KEN KAMBA", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "bobwardelectric@earthlink.net", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0105", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "BOOTH", "active": true, "contact": "Roger Booth", "phone": "1 661 269 5503", "cell": "1 661 547 1783", "statusNote": "", "comments": "LOOK EMAIL", "email": "ebdigger@roadrunner.com", "bids": {"Quadro Vecchio": {"price": 161350.0, "received": "2025-07-07", "comments": "Material And labor"}, "807 6th Ave": {"price": 95383.0, "received": null, "comments": ""}, "12979 Blairwood Dr": {"price": 132439.0, "received": "2026-02-18", "comments": ""}}, "codes": ["024000 Demolition", "312300 Excavation & Backfill", "312500 Erosion Controls", "334000 Stormwater management-LID"]}, {"id": "m0106", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Material", "company": "BOULEVARD TILE", "active": true, "contact": "Tony McCauley", "phone": "1 818 781 5900", "cell": "", "statusNote": "", "comments": "", "email": "blvdtile@hotmail.com", "bids": {}, "codes": ["096000 Tile - Material"]}, {"id": "m0107", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "017423 Final Clean-up", "company": "BOYLAN BROS.", "active": true, "contact": "Tom Campbell", "phone": "1 760 322 1495", "cell": "1 760 902 0183", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["017423 Final Clean-up"]}, {"id": "m0108", "div": "DIVISION 13", "divName": "SPECIAL CONSTRUCTION", "code": "Sauna", "company": "Breakform", "active": true, "contact": "Tas Oszkay", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "tas@breakformdesign.com", "bids": {"17797 Camino De Yatasto": {"price": 40000.0, "received": "2025-09-18", "comments": "DRY SAUNA $25.000 // WET SAUNA $15.000"}}, "codes": ["Sauna"]}, {"id": "m0109", "div": "DIVISION 05", "divName": "METALS", "code": "055200 Metal Railing", "company": "BREAKFORM FABRICATION", "active": true, "contact": "GUS", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "gus@breakformdesign.com", "bids": {"Quadro Vecchio": {"price": 57850.0, "received": "2025-07-25", "comments": ""}, "723 OFW": {"price": 291600.0, "received": "2025-09-22", "comments": ""}, "748 & 750 Palisades Dr": {"price": 73174.0, "received": null, "comments": ""}, "478 Wynola St": {"price": 12578.0, "received": "2025-08-22", "comments": ""}, "17797 Camino De Yatasto": {"price": 7102.0, "received": "2025-09-22", "comments": ""}, "865 N Oreo Pl": {"price": 302075.0, "received": "2025-09-24", "comments": ""}, "12979 Blairwood Dr": {"price": 101100.0, "received": "2026-02-13", "comments": ""}}, "codes": ["055200 Metal Railing"]}, {"id": "m0110", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "BRENTWOOD", "active": true, "contact": "Bruce Sobol", "phone": "1 310 477 2944", "cell": "", "statusNote": "", "comments": "", "email": "bsobol@brentwoodelectrical.com", "bids": {}, "codes": ["260500 Electric Rough & Finish", "269900 Electric Fixtures"]}, {"id": "m0111", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "BRIAN ODELL ( AND CASSANDRA)", "active": true, "contact": "Concrete finisher", "phone": "818-419-9850", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["030630 Concrete Slab"]}, {"id": "m0112", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Material", "company": "BRIAN ODELL'S SLAB ART", "active": true, "contact": "", "phone": "1 818 223 9181", "cell": "1 818 419 9850", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["096000 Tile - Material"]}, {"id": "m0113", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "076000 Flashing & Sheet Metal", "company": "BROADWAY SHEET METAL", "active": true, "contact": "", "phone": "1 818 781 1477", "cell": "", "statusNote": "", "comments": "EMAIL UPDATED", "email": "alex@broadwaysm.com", "bids": {}, "codes": ["076000 Flashing & Sheet Metal"]}, {"id": "m0114", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "Brothers Glass & Shower Door", "active": true, "contact": "", "phone": "323 692-0057", "cell": "", "statusNote": "", "comments": "", "email": "brothersglass323@yahoo.com", "bids": {}, "codes": ["058000 Glazing"]}, {"id": "m0115", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "BUDDY KING PLUMBING, HESTING & AC.", "active": true, "contact": "", "phone": "310-390-8606", "cell": "", "statusNote": "CALL", "comments": "", "email": "buddykingphvac@gmail.com", "bids": {"865 N Oreo Pl": {"price": 120000.0, "received": "2025-11-05", "comments": ""}}, "codes": ["220000 Plumbing Rough & Finish", "230000 Hvac"]}, {"id": "m0116", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Installation", "company": "BULLETPROOF TILE AND STONE SERVICE", "active": true, "contact": "", "phone": "818 6981773", "cell": "", "statusNote": "NEW", "comments": "WEB FORM", "email": "", "bids": {}, "codes": ["096000 Tile - Installation"]}, {"id": "m0117", "div": "DIVISION 09", "divName": "FINISHES", "code": "099000 Painting", "company": "C & G PAINT(C&G REMODELING INC)", "active": true, "contact": "Carlos", "phone": "818.201.7701", "cell": "", "statusNote": "", "comments": "", "email": "cgremodelinginc@gmail.com", "bids": {}, "codes": ["099000 Painting"]}, {"id": "m0118", "div": "DIVISION 09", "divName": "FINISHES", "code": "092000 Gypsum Board", "company": "C&H DRYWALL", "active": true, "contact": "Jeff Jay", "phone": "1 805 207 0642", "cell": "805-495-0679", "statusNote": "", "comments": "", "email": "candhframingdrywall@hotmail.com", "bids": {}, "codes": ["092000 Gypsum Board"]}, {"id": "m0119", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "C-ERA CONSTRUCTION", "active": false, "contact": "David Lee", "phone": "1 562 245 7235", "cell": "1 562 219 0799", "statusNote": "", "comments": "NO RESPONSE", "email": "info@c-eraconstruction.com", "bids": {}, "codes": ["030630 Concrete Slab", "033100 Structural Concrete", "042200 Concrete Masonry Unit"]}, {"id": "m0120", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Material", "company": "C.G. TILE", "active": true, "contact": "Adam Hammet", "phone": "1 818 989 3217", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["096000 Tile - Material"]}, {"id": "m0121", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "C.I. PLUMBING", "active": true, "contact": "Damon Premer", "phone": "1 310 656 2400", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0122", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "CABINET & MILLWORK INSTALLERS", "active": false, "contact": "Larry Johnson", "phone": "1 760 772 2208", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["064100 Cabinets"]}, {"id": "m0123", "div": "DIVISION 05", "divName": "METALS", "code": "055000 Metal Fabricators", "company": "CAC FABRICATIONS", "active": false, "contact": "David Agins", "phone": "1 818 882 2626", "cell": "", "statusNote": "", "comments": "", "email": "david@cacfab.com", "bids": {}, "codes": ["055000 Metal Fabricators"]}, {"id": "m0124", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "CACTUS CUSTOM CABINETS INC.", "active": false, "contact": "Matthew Tafoya", "phone": "1 310 644 7615", "cell": "", "statusNote": "", "comments": "They got the invites but ignore now because past quotes had no response.", "email": "cactuscabinets@gmail.com", "bids": {}, "codes": ["064100 Cabinets"]}, {"id": "m0125", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "CALIFORNIA", "active": false, "contact": "Pat Resendiz", "phone": "1 815 342 3450", "cell": "", "statusNote": "", "comments": "", "email": "pat@californiasteelwindows.com", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0126", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "CALIFORNIA AIR", "active": true, "contact": "Harry Irvine", "phone": "(323) 922 4824", "cell": "", "statusNote": "NEW", "comments": "", "email": "harryirvine@californiaac.com", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0127", "div": "DIVISION 14", "divName": "CONVEYING EQUIPMENT", "code": "142000 Elevators", "company": "California Custom Lift", "active": true, "contact": "", "phone": "714-554-1300", "cell": "", "statusNote": "", "comments": "", "email": "office@calcustomliftinc.com", "bids": {"Quadro Vecchio": {"price": 32800.0, "received": "2025-07-09", "comments": ""}, "865 N Oreo Pl": {"price": 32800.0, "received": "2025-10-28", "comments": ""}, "807 6th Ave": {"price": 39800.0, "received": "2025-10-03", "comments": ""}, "15265 W Bestor Blvd": {"price": 34800.0, "received": "2025-10-28", "comments": ""}}, "codes": ["142000 Elevators"]}, {"id": "m0128", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071010 Waterproofing", "company": "CALIFORNIA DECKING & WATERPROOFING", "active": true, "contact": "", "phone": "(800) 482-6334", "cell": "", "statusNote": "NEW", "comments": "", "email": "contact@californiadecking.com", "bids": {}, "codes": ["071010 Waterproofing"]}, {"id": "m0129", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "CALIFORNIA GLASS BENDING", "active": true, "contact": "Dave Mispagel", "phone": "310-549-5255", "cell": "714-240-6868", "statusNote": "", "comments": "", "email": "dave@calglassbending.com", "bids": {}, "codes": ["058000 Glazing"]}, {"id": "m0130", "div": "DIVISION 10", "divName": "SPECIALTIES", "code": "103000 Fireplace", "company": "California Mantel & Fireplace", "active": true, "contact": "Tom", "phone": "714-204-2470", "cell": "", "statusNote": "HIGHLY ACTIVE", "comments": "www.calmantel.com.", "email": "nknox@calmantel.com", "bids": {"17797 Camino De Yatasto": {"price": 14150.0, "received": "2025-11-03", "comments": ""}, "865 N Oreo Pl": {"price": 18735.0, "received": "2025-10-22", "comments": ""}, "1080 El Medio Place": {"price": 43938.0, "received": "2025-10-21", "comments": "Check;new sub"}, "15265 W Bestor Blvd": {"price": 18980.0, "received": "2025-10-29", "comments": ""}}, "codes": ["103000 Fireplace"]}, {"id": "m0131", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "CALIFORNIA PAVING & GRADING, INC.", "active": true, "contact": "", "phone": "818.956.5939", "cell": "323.255.3473", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["030630 Concrete Slab"]}, {"id": "m0132", "div": "DIVISION 09", "divName": "FINISHES", "code": "074619 Steel Siding", "company": "CALIFORNIA PRE STAIN INC.", "active": true, "contact": "SKIP", "phone": "310-326-2403", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["074619 Steel Siding"]}, {"id": "m0133", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "481400 Solar Energy Electrical Power Generation Equipment", "company": "CALIFORNIA SOLAR", "active": true, "contact": "Richard White", "phone": "1 805 419 1051", "cell": "", "statusNote": "", "comments": "", "email": "rick@californiasolar.com, sales@californiasolar.com", "bids": {}, "codes": ["481400 Solar Energy Electrical Power Generation Equipment", "221000 Radiant Heating"]}, {"id": "m0134", "div": "DIVISION 09", "divName": "FINISHES", "code": "097200 Wall Coverings", "company": "CAL\u2010LITE CONCRETE", "active": true, "contact": "Lightweight Concrete", "phone": "208.712.3456", "cell": "Hayden, ID  83835", "statusNote": "", "comments": "", "email": "calliteconcrete@aol.com", "bids": {}, "codes": ["097200 Wall Coverings"]}, {"id": "m0135", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "CAMPBELL CUSTOM GLASS, LLC.", "active": true, "contact": "Tim Campbell", "phone": "1 323 735 1445", "cell": "1 323 735 0021", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["058000 Glazing"]}, {"id": "m0136", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "061000 Rough Carpentry", "company": "CANFIELD", "active": false, "contact": "Jeff Pratt", "phone": "1 805 522 4426", "cell": "", "statusNote": "", "comments": "", "email": "jeff@dalecc.com", "bids": {}, "codes": ["061000 Rough Carpentry"]}, {"id": "m0137", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "076000 Flashing & Sheet Metal", "company": "CANOGA", "active": true, "contact": "Chris/ Greg/ Kevin", "phone": "1 818 340 8720", "cell": "1 818 340 0867", "statusNote": "", "comments": "EMAIL UPDATED", "email": "csmoffice1956@gmail.com", "bids": {}, "codes": ["076000 Flashing & Sheet Metal"]}, {"id": "m0138", "div": "DIVISION 09", "divName": "FINISHES", "code": "074619 Steel Siding", "company": "CANOGA SHEET METAL", "active": true, "contact": "Chris/ Greg/ Kevin", "phone": "1 818 340 8720", "cell": "1 818 340 0867", "statusNote": "", "comments": "", "email": "coppersmith@sprintmail.com", "bids": {}, "codes": ["074619 Steel Siding"]}, {"id": "m0139", "div": "DIVISION 09", "divName": "FINISHES", "code": "096800 Carpet", "company": "CARPET CREATIONS", "active": true, "contact": "Amnon Levy", "phone": "1 818 703 8227", "cell": "", "statusNote": "", "comments": "", "email": "amnon@carpetcreationsgroup.com", "bids": {}, "codes": ["096800 Carpet"]}, {"id": "m0140", "div": "DIVISION 09", "divName": "FINISHES", "code": "096800 Carpet", "company": "CARPET DESIGN", "active": true, "contact": "Robert Rickun", "phone": "1 310 659 5722", "cell": "", "statusNote": "", "comments": "", "email": "robertrickun@sbcglobal.net", "bids": {}, "codes": ["096800 Carpet"]}, {"id": "m0141", "div": "DIVISION 08", "divName": "OPENINGS", "code": "087000 Finish Hardware", "company": "CARTER", "active": true, "contact": "Sheila Carter", "phone": "1 310 657 1940", "cell": "", "statusNote": "", "comments": "", "email": "scarter@carterhardware.com", "bids": {}, "codes": ["087000 Finish Hardware", "224000 Plumbing Fixtures"]}, {"id": "m0142", "div": "DIVISION 05", "divName": "METALS", "code": "055000 Metal Fabricators", "company": "CASA DEL SOL", "active": true, "contact": "Dennis Estrada", "phone": "1 310 456 2395", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["055000 Metal Fabricators"]}, {"id": "m0143", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "061000 Rough Carpentry", "company": "CASTILLO BUILDING", "active": true, "contact": "Ray Castillo", "phone": "1-323-241-8394", "cell": "", "statusNote": "", "comments": "NO RESPONSE", "email": "castillosbuilding@yahoo.com", "bids": {}, "codes": ["061000 Rough Carpentry"]}, {"id": "m0144", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071010 Waterproofing", "company": "CBS CONSTRUCTION", "active": true, "contact": "", "phone": "(714) 840-2000", "cell": "(714) 904-2378", "statusNote": "NEW", "comments": "", "email": "cbsconstructionservices@gmail.com", "bids": {}, "codes": ["071010 Waterproofing"]}, {"id": "m0145", "div": "DIVISION 09", "divName": "FINISHES", "code": "096800 Carpet", "company": "CCG", "active": true, "contact": "Amnon Levy", "phone": "1 818 340 2884", "cell": "1 818 419 2726", "statusNote": "", "comments": "", "email": "alevy@ccgfloors.com", "bids": {}, "codes": ["096800 Carpet"]}, {"id": "m0146", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "CD HVAC", "active": true, "contact": "", "phone": "(310) 770-9246", "cell": "", "statusNote": "NEW", "comments": "", "email": "mail@constructiondistrict.com", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0147", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "CELL-CRETE CORP.", "active": true, "contact": "Marc McClure", "phone": "1 626 357 3500", "cell": "1 626 945 8651", "statusNote": "", "comments": "NO RESPONSE", "email": "mmcclure@cell-crete.com", "bids": {}, "codes": ["030630 Concrete Slab"]}, {"id": "m0148", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "061000 Rough Carpentry", "company": "CENTER CIRCLE CONSTRUCTION CORPORATION", "active": false, "contact": "", "phone": "1-818-368-8240", "cell": "", "statusNote": "", "comments": "", "email": "laserframe@aol.com", "bids": {}, "codes": ["061000 Rough Carpentry"]}, {"id": "m0149", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "CENTRAL RECLAMATION", "active": false, "contact": "", "phone": "phone: (323)263-7400", "cell": "323-263-7400", "statusNote": "", "comments": "NO RESPONSE", "email": "ron@centralreclamation.com", "bids": {}, "codes": ["024000 Demolition", "031113 Shoring"]}, {"id": "m0150", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "CH HEATING & AIR", "active": true, "contact": "Gilbert Chavez", "phone": "8184025109.0", "cell": "8188954935.0", "statusNote": "", "comments": "", "email": "gilbert@chavezac.com", "bids": {"213 OFW Waterfront": {"price": 32963.0, "received": "2025-08-06", "comments": ""}, "1080 El Medio Place": {"price": 76963.0, "received": "2025-10-21", "comments": "Check;"}, "15265 W Bestor Blvd": {"price": 32550.0, "received": "2025-12-01", "comments": ""}, "4565 Dundee Drive": {"price": 28963.0, "received": "2025-12-01", "comments": ""}, "1093 Palms Blvd": {"price": 32550.0, "received": "2025-12-01", "comments": ""}}, "codes": ["230000 Hvac"]}, {"id": "m0151", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "CHAMPION WINDOWS", "active": true, "contact": "Keith Ackerman", "phone": "1 661 510 5716", "cell": "", "statusNote": "", "comments": "", "email": "keith.a@championwindows.biz", "bids": {}, "codes": ["058000 Glazing"]}, {"id": "m0152", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "CHRISTIAN BROTHERS", "active": true, "contact": "", "phone": "404-671-4690", "cell": "", "statusNote": "", "comments": "", "email": "info@cbmech.com", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0153", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Installation", "company": "CITY OF ANGELS STONE INC.", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "ortegaangel404@gmail.com, cityofangelsstone@gmail.com", "bids": {"6537 Topanga Canyon": {"price": 93120.0, "received": "2026-02-05", "comments": ""}, "17797 Camino De Yatasto": {"price": 125779.0, "received": "2025-11-13", "comments": ""}, "1080 El Medio Place": {"price": 21137.7, "received": "2025-12-05", "comments": ""}, "15265 W Bestor Blvd": {"price": 152924.0, "received": "2025-10-28", "comments": ""}, "1093 Palms Blvd": {"price": 40140.0, "received": "2025-10-21", "comments": ""}, "2429 Eastern Canal": {"price": 57243.7, "received": "2025-11-12", "comments": ""}, "16339 Akron": {"price": 52693.2, "received": "2025-12-23", "comments": ""}, "12979 Blairwood Dr": {"price": 98690.0, "received": "2026-02-05", "comments": ""}, "1134 Iliff St": {"price": 25612.0, "received": "2026-04-07", "comments": ""}, "865 N Oreo Pl": {"price": 77137.9, "received": null, "comments": ""}, "807 6th Ave": {"price": 148286.4, "received": null, "comments": "UPDATED PRICE WITH DISCOUNT"}}, "codes": ["096000 Tile - Installation", "096100 Flooring"]}, {"id": "m0154", "div": "DIVISION 09", "divName": "FINISHES", "code": "092000 Gypsum Board", "company": "CITY WALL", "active": true, "contact": "Maria", "phone": "1 818 988 8546", "cell": "", "statusNote": "", "comments": "highly active", "email": "info@lacitywall.com", "bids": {"Quadro Vecchio": {"price": 149888.0, "received": "2025-07-08", "comments": ""}, "723 OFW": {"price": 434010.0, "received": "2025-08-07", "comments": ""}, "748 & 750 Palisades Dr": {"price": 157793.0, "received": "2025-08-04", "comments": ""}, "478 Wynola St": {"price": 39965.0, "received": "2025-09-04", "comments": ""}, "17797 Camino De Yatasto": {"price": 310792.0, "received": "2025-09-15", "comments": ""}, "865 N Oreo Pl": {"price": 127379.0, "received": "2025-11-19", "comments": ""}, "807 6th Ave": {"price": 168483.0, "received": "2025-10-06", "comments": ""}, "1080 El Medio Place": {"price": 144143.0, "received": "2025-10-28", "comments": "Check;"}, "15265 W Bestor Blvd": {"price": 253209.0, "received": "2025-10-30", "comments": ""}, "4565 Dundee Drive": {"price": 43172.0, "received": "2025-11-19", "comments": ""}, "1093 Palms Blvd": {"price": 40140.0, "received": "2025-11-21", "comments": ""}, "2429 Eastern Canal": {"price": 39770.0, "received": "2025-12-02", "comments": ""}, "16339 Akron": {"price": 56010.0, "received": "2026-01-12", "comments": ""}, "12979 Blairwood Dr": {"price": 134255.0, "received": "2026-02-17", "comments": ""}}, "codes": ["092000 Gypsum Board"]}, {"id": "m0155", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "269900 Electric Fixtures", "company": "CLASSIC ELECTRIC", "active": true, "contact": "Ed Williams", "phone": "1 818 889 2831", "cell": "1 818 612 8856", "statusNote": "", "comments": "", "email": "edw@ecbelectric.com", "bids": {}, "codes": ["269900 Electric Fixtures", "260500 Electric Rough & Finish"]}, {"id": "m0156", "div": "DIVISION 04", "divName": "MASONRY", "code": "042100 Masonry Brick Veneer", "company": "CLIVE CHRISTIE", "active": true, "contact": "Clive Christie", "phone": "1 310 455 3596", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["042100 Masonry Brick Veneer"]}, {"id": "m0157", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "CME", "active": true, "contact": "Carla Eubank", "phone": "1 818 434 0725", "cell": "", "statusNote": "", "comments": "", "email": "cme3@att.net, cme8@att.net", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation", "087000 Finish Hardware"]}, {"id": "m0158", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "COAST TO COAST PLASTERING", "active": true, "contact": "", "phone": "(323) 731-4400", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["092400 Stucco"]}, {"id": "m0159", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "COASTAL ELECTRIC SOLUTIONS", "active": true, "contact": "Andy Ernst", "phone": "1 805 233 2816", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0160", "div": "DIVISION 10", "divName": "FINISHES", "code": "96801 Carpet", "company": "COCOTURF", "active": true, "contact": "Oliver Roumy", "phone": "310 957-1900", "cell": "", "statusNote": "", "comments": "", "email": "olivier@cocoturf.com", "bids": {}, "codes": ["96801 Carpet"]}, {"id": "m0161", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "CONSTRUCTION PLUMBING", "active": false, "contact": "Peter Kornbluth", "phone": "1 805 965 7377", "cell": "", "statusNote": "", "comments": "", "email": "constructionplumbing@yahoo.com", "bids": {}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0162", "div": "DIVISION 09", "divName": "FINISHES", "code": "096800 Carpet", "company": "CONTEMPO", "active": true, "contact": "David Haloosim", "phone": "1 310 837 8110", "cell": "", "statusNote": "", "comments": "", "email": "haloo2u@hotmail.com", "bids": {}, "codes": ["096800 Carpet"]}, {"id": "m0163", "div": "DIVISION 09", "divName": "FINISHES", "code": "096400 Wood Flooring", "company": "CONTEMPO FLOOR COVERINGS, INC.", "active": true, "contact": "David Haloossim", "phone": "1 310 837 8110", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["096400 Wood Flooring"]}, {"id": "m0164", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "COOLCOMFORT HVAC", "active": true, "contact": "Sergey Matevosyan", "phone": "(323)546-4822", "cell": "", "statusNote": "", "comments": "ALL MEP", "email": "m.serge@coolcomforthvac.com", "bids": {"6537 Topanga Canyon": {"price": 108322.0, "received": "2026-02-12", "comments": ""}, "17797 Camino De Yatasto": {"price": 67188.0, "received": null, "comments": ""}, "807 6th Ave": {"price": 66120.0, "received": "2025-12-23", "comments": ""}, "15265 W Bestor Blvd": {"price": 80868.0, "received": null, "comments": ""}, "2429 Eastern Canal": {"price": 27270.0, "received": null, "comments": ""}, "16339 Akron": {"price": 27690.0, "received": "2025-01-10", "comments": ""}}, "codes": ["230000 Hvac"]}, {"id": "m0165", "div": "DIVISION 21", "divName": "FIRE SUPPRESSION", "code": "211300 Fire Spinklers", "company": "CORE FIRE PROTECTION", "active": false, "contact": "Uzi Levy", "phone": "1 818 345 7815", "cell": "1 818 335 7656", "statusNote": "closed business", "comments": "", "email": "core33@gmail.com", "bids": {}, "codes": ["211300 Fire Spinklers"]}, {"id": "m0166", "div": "DIVISION 03", "divName": "CONCRETE", "code": "033100 Structural Concrete", "company": "CORONA CONSTRUCTIONS", "active": true, "contact": "Jose Corona", "phone": "310 831-2164", "cell": "310 720-9465", "statusNote": "FRAMING TOO", "comments": "", "email": "jose@coronaframing.com", "bids": {}, "codes": ["033100 Structural Concrete"]}, {"id": "m0167", "div": "DIVISION 03", "divName": "CONCRETE", "code": "031113 Shoring", "company": "COSTAL CONCRETE COMPANY", "active": true, "contact": "", "phone": "800 987-8046", "cell": "", "statusNote": "", "comments": "NO RESPONSE", "email": "info@coastalconcretecompany.com", "bids": {}, "codes": ["031113 Shoring", "033100 Structural Concrete"]}, {"id": "m0168", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "COVELLO PLASTERING CORPORATION", "active": true, "contact": "", "phone": "(818) 346-3153", "cell": "", "statusNote": "", "comments": "", "email": "ccplast@sbcglobal.net", "bids": {}, "codes": ["092400 Stucco"]}, {"id": "m0169", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "COVERALL ELECTRIC, INC.", "active": true, "contact": "Mike Derderian", "phone": "1 310 837 7219", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0170", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "CRYSTAL CLEAR", "active": true, "contact": "Russ Martin", "phone": "1 818 993 4527", "cell": "", "statusNote": "", "comments": "Wants more time for the estimates, 7 days is not enough", "email": "pmestimating@ccglassinc.com, mark@ccglassinc.com, estimatingcrystalclearglass@gmail.com", "bids": {"17797 Camino De Yatasto": {"price": 56096.0, "received": "2025-10-02", "comments": "Bathroom glass"}}, "codes": ["058000 Glazing"]}, {"id": "m0171", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "015423 Scaffolding", "company": "CSI", "active": true, "contact": "John Keefer", "phone": "1 310 324 7004", "cell": "1 310 261 8600", "statusNote": "", "comments": "", "email": "johnk@csiscaffold.com", "bids": {}, "codes": ["015423 Scaffolding"]}, {"id": "m0172", "div": "DIVISION 09", "divName": "FINISHES", "code": "099000 Painting", "company": "Cucufate", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "Didn't saw our emails", "email": "cucufatepainting@gmail.com", "bids": {}, "codes": ["099000 Painting"]}, {"id": "m0173", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "CURRENT ELECTRIC", "active": true, "contact": "", "phone": "1 818 885 5567", "cell": "1 310 828 0567", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0174", "div": "DIVISION 05", "divName": "METALS", "code": "055000 Metal Fabricators", "company": "CUSTOM DESIGN IRONWORKS", "active": true, "contact": "Beverly Schuchmacher", "phone": "1 818 700 9182", "cell": "", "statusNote": "", "comments": "", "email": "beverly@cdiw.com", "bids": {}, "codes": ["055000 Metal Fabricators"]}, {"id": "m0175", "div": "DIVISION 09", "divName": "FINISHES", "code": "097200 Wall Coverings", "company": "CY'S DRAPER SERVICE/WINDOW COVERINGS", "active": true, "contact": "Steve Bergmans", "phone": "310.390.6577", "cell": "", "statusNote": "", "comments": "", "email": "cysdrapery@yahoo.com", "bids": {}, "codes": ["097200 Wall Coverings"]}, {"id": "m0176", "div": "DIVISION 03", "divName": "CONCRETE", "code": "033100 Structural Concrete", "company": "D&L CONSTRUCTION", "active": true, "contact": "Rick Luoma", "phone": "1 626 484 1602", "cell": "", "statusNote": "", "comments": "NO RESPONSE", "email": "", "bids": {}, "codes": ["033100 Structural Concrete"]}, {"id": "m0177", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "D&W ELECTRIC CORP.", "active": true, "contact": "", "phone": "(424)207-0751", "cell": "", "statusNote": "", "comments": "", "email": "dwelectricinfo@gmail.com", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0178", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "061000 Rough Carpentry", "company": "DALE CANFIELD CONSTRUCTION", "active": true, "contact": "Marcus", "phone": "1 805 522 4426", "cell": "", "statusNote": "", "comments": "VOICEMAIL", "email": "marcus@dalecc.com", "bids": {}, "codes": ["061000 Rough Carpentry"]}, {"id": "m0179", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "DAMIAN PLASTERING INC", "active": true, "contact": "", "phone": "(310) 418-4532", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["092400 Stucco"]}, {"id": "m0180", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "DAVE COLEMAN", "active": true, "contact": "Dave Coleman", "phone": "1 323 793 2821", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0181", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "DAVIS", "active": true, "contact": "Jim Posey", "phone": "1 661 255 5382", "cell": "1 805 509 3920", "statusNote": "", "comments": "", "email": "jim@davisplastering.com", "bids": {}, "codes": ["092400 Stucco"]}, {"id": "m0182", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "DAY & NITE DOOR SERVICE INC.", "active": true, "contact": "Mike Monroy", "phone": "1 800 698 7202", "cell": "1 714 448 4116", "statusNote": "CALL", "comments": "", "email": "mikemonroy@sbcglobal.net", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0183", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071010 Waterproofing", "company": "DECKRITE WATERPROOFING CO., INC.", "active": false, "contact": "Waterproofing", "phone": "310.322.0107", "cell": "310.322.1916", "statusNote": "WON'T BID W/OUT GETTING A JOB FIRST", "comments": "", "email": "keith@deckritewaterproofing.com", "bids": {"52-60 Market St": {"price": 46100.0, "received": "2025-05-27", "comments": ""}, "429 Sherman Canal": {"price": 11400.0, "received": "2025-08-04", "comments": "Work for 2dn and 3rd floor decks"}, "213 OFW Waterfront": {"price": 26000.0, "received": "2025-08-04", "comments": ""}, "723 OFW": {"price": 163300.0, "received": "2025-11-04", "comments": ""}, "748 & 750 Palisades Dr": {"price": 19800.0, "received": "2025-08-08", "comments": ""}, "17797 Camino De Yatasto": {"price": 140800.0, "received": "2025-10-21", "comments": ""}, "865 N Oreo Pl": {"price": 186500.0, "received": "2025-11-17", "comments": ""}, "1080 El Medio Place": {"price": 61200.0, "received": "2025-11-10", "comments": "Check;price and scope work lower than competitors"}, "15265 W Bestor Blvd": {"price": 157900.0, "received": null, "comments": "Does not include any waterproofing for Property Line, Site or Planter walls. No Civil plans were available."}, "1093 Palms Blvd": {"price": 22200.0, "received": "2025-11-25", "comments": ""}, "2429 Eastern Canal": {"price": 21200.0, "received": null, "comments": ""}}, "codes": ["071010 Waterproofing"]}, {"id": "m0184", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "DECORE-ATIVE SPECIALTIES", "active": true, "contact": "Caree Reser", "phone": "1 626 254 9191", "cell": "1 805 217 6753", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["064100 Cabinets"]}, {"id": "m0185", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "DEL MAR MECHANICAL", "active": true, "contact": "Ron Rodriguez", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0186", "div": "DIVISION 14", "divName": "CONVEYING EQUIPMENT", "code": "142000 Elevators", "company": "DELTA ELEVATOR", "active": true, "contact": "Elevator", "phone": "562.630.5311", "cell": "562.630.5820", "statusNote": "", "comments": "", "email": "brian@deltaelev.com", "bids": {}, "codes": ["142000 Elevators"]}, {"id": "m0187", "div": "DIVISION 21", "divName": "FIRE SUPPRESSION", "code": "211300 Fire Spinklers", "company": "DELTA FIRE PROTECTION AND EQUIPMENT", "active": true, "contact": "Brett Greene", "phone": "1 818 764 7990", "cell": "", "statusNote": "", "comments": "X", "email": "bgreene@deltafireprotection.com", "bids": {"17797 Camino De Yatasto": {"price": 32300.0, "received": "2025-10-23", "comments": ""}, "1080 El Medio Place": {"price": 19600.0, "received": "2025-11-11", "comments": "Check;"}}, "codes": ["211300 Fire Spinklers"]}, {"id": "m0188", "div": "DIVISION 09", "divName": "FINISHES", "code": "092000 Gypsum Board", "company": "DENKO DRYWALL & PAINTING", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["092000 Gypsum Board", "099000 Painting", "099001 Painting Cabinets"]}, {"id": "m0189", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "DESIGN CONSULTING", "active": true, "contact": "Ed Marchall", "phone": "310-980-8312", "cell": "", "statusNote": "", "comments": "", "email": "marshalled@me.com", "bids": {}, "codes": ["064100 Cabinets"]}, {"id": "m0190", "div": "DIVISION 09", "divName": "FINISHES", "code": "096400 Wood Flooring", "company": "DFS FLOORING (COMMERCIAL FLOORING)", "active": true, "contact": "http://www.dfsflooring.com", "phone": "818-374-5200", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["096400 Wood Flooring"]}, {"id": "m0191", "div": "DIVISION 14", "divName": "CONVEYING EQUIPMENT", "code": "142000 Elevators", "company": "Diamond Elevator Inc", "active": true, "contact": "Mike Peterson", "phone": "(323) 919-0029", "cell": "", "statusNote": "", "comments": "", "email": "michaelp@diamondhe.com", "bids": {"865 N Oreo Pl": {"price": 59825.0, "received": "2025-10-27", "comments": ""}, "15265 W Bestor Blvd": {"price": 69610.0, "received": "2025-10-28", "comments": ""}}, "codes": ["142000 Elevators"]}, {"id": "m0192", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "015150 Deputy Inspections", "company": "DICK NIGRA INSPECTIONS", "active": true, "contact": "Richard Nigra", "phone": "1 818 624 9373", "cell": "1 818 957 2759", "statusNote": "", "comments": "", "email": "richardjr@dn-inspections.com", "bids": {"865 N Oreo Pl": {"price": 20350.0, "received": "2025-10-31", "comments": ""}}, "codes": ["015150 Deputy Inspections"]}, {"id": "m0193", "div": "DIVISION 21", "divName": "FIRE SUPPRESSION", "code": "211300 Fire Spinklers", "company": "DIGIFIER INC.", "active": true, "contact": "Wolfgang Ehrgott", "phone": "818-649-9884", "cell": "747-609-5159", "statusNote": "", "comments": "", "email": "sales.la@digifier.com", "bids": {}, "codes": ["211300 Fire Spinklers"]}, {"id": "m0194", "div": "DIVISION 09", "divName": "FINISHES", "code": "092000 Gypsum Board", "company": "DIRECT CONSTRUCTION", "active": true, "contact": "", "phone": "1 310 523 2088", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["092000 Gypsum Board", "092400 Stucco"]}, {"id": "m0195", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "DJ SCHEFFLER", "active": true, "contact": "Dale Scheffler/ Mark Nye", "phone": "1 909 595 2924", "cell": "", "statusNote": "HIGHLY ACTIVE", "comments": "Morris", "email": "dale@djscheffler.com, mark@djscheffler.com", "bids": {"865 N Oreo Pl": {"price": 116655.0, "received": null, "comments": "$165.00 per linear foot will be added for additional length"}, "12979 Blairwood Dr": {"price": 146860.0, "received": "2026-02-13", "comments": "BID just for Cast-in-Drilled Hole Piles"}}, "codes": ["030630 Concrete Slab", "030650 Finish Concrete", "031113 Shoring", "033100 Structural Concrete", "042200 Concrete Masonry Unit"]}, {"id": "m0196", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071010 Waterproofing", "company": "DLX WATERPROOFING", "active": true, "contact": "", "phone": "818 8065114", "cell": "", "statusNote": "NEW", "comments": "", "email": "decks@dlxwaterproofing.com", "bids": {}, "codes": ["071010 Waterproofing"]}, {"id": "m0197", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "DMC PLUMBING", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "dave@dmcplumbing.org, patsy@dmcplumbing.org", "bids": {"6537 Topanga Canyon": {"price": 162825.0, "received": "2026-02-13", "comments": ""}, "17797 Camino De Yatasto": {"price": 257100.0, "received": "2026-04-15", "comments": ""}, "807 6th Ave": {"price": 277500.0, "received": "2026-04-06", "comments": "UPDATED PRICE"}, "1080 El Medio Place": {"price": 194900.0, "received": "2025-10-23", "comments": "Check;"}}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0198", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "323100 Fences & Gates", "company": "DORLAND", "active": true, "contact": "Tim Dorland", "phone": "1 818 888 8850", "cell": "1 310 850 2294", "statusNote": "", "comments": "", "email": "dasiinc@aol.com", "bids": {}, "codes": ["323100 Fences & Gates"]}, {"id": "m0199", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "DOUBLE GREEN LANDSCAPE", "active": true, "contact": "Ethan Rice", "phone": "1 310 448 4220", "cell": "", "statusNote": "", "comments": "will answer the phone", "email": "ethan@dglandscapes.com", "bids": {}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0200", "div": "DIVISION 09", "divName": "FINISHES", "code": "092000 Gypsum Board", "company": "DRAPER DRYWALL", "active": true, "contact": "", "phone": "1 949 305 8100", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["092000 Gypsum Board"]}, {"id": "m0201", "div": "DIVISION 09", "divName": "FINISHES", "code": "092000 Gypsum Board", "company": "DRYTECH ENTERPRISE INC", "active": false, "contact": "Tamir Hochmano", "phone": "818-376-0016", "cell": "", "statusNote": "", "comments": "", "email": "office@drytechenterprise.com", "bids": {}, "codes": ["092000 Gypsum Board", "092400 Stucco"]}, {"id": "m0202", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "262000 Low Voltage", "company": "DSI ENTERTAINMENT SYSTEMS, INC.", "active": true, "contact": "Michael Fehmers", "phone": "1 866 MYAVGUY", "cell": "1 310 432 2381", "statusNote": "", "comments": "", "email": "mfehmers@dsientertainment.com", "bids": {}, "codes": ["262000 Low Voltage"]}, {"id": "m0203", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Installation", "company": "DTLA Tile and Stone, Inc.", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "bill@dtlatile.com", "bids": {}, "codes": ["096000 Tile - Installation"]}, {"id": "m0204", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "015150 Deputy Inspections", "company": "DTS ENVIRONMENTAL CONSULTING", "active": true, "contact": "Donald Short", "phone": "1 626 844 1841", "cell": "1 323 459 6823", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["015150 Deputy Inspections"]}, {"id": "m0205", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "061000 Rough Carpentry", "company": "DURST BUILDERS", "active": true, "contact": "John Durst", "phone": "818-631-9577", "cell": "", "statusNote": "", "comments": "NO RESPONSE", "email": "johnd@durstbuilders.com", "bids": {"748 & 750 Palisades Dr": {"price": 367750.0, "received": "2025-08-18", "comments": ""}, "15265 W Bestor Blvd": {"price": 166000.0, "received": "2025-11-24", "comments": ""}}, "codes": ["061000 Rough Carpentry"]}, {"id": "m0206", "div": "DIVISION 09", "divName": "FINISHES", "code": "092000 Gypsum Board", "company": "Dylan Drywall:", "active": true, "contact": "Juan Fernandez", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "juanfr2224@gmail.com", "bids": {}, "codes": ["092000 Gypsum Board"]}, {"id": "m0207", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "E&D PLUMBING", "active": true, "contact": "Karolan Palacios", "phone": "310-426-4316", "cell": "", "statusNote": "NEW", "comments": "", "email": "edplumbing@icloud.com, info@eands-plumbing.com", "bids": {"6537 Topanga Canyon": {"price": 82950.0, "received": "2026-02-07", "comments": ""}, "807 6th Ave": {"price": 123350.0, "received": "2026-01-13", "comments": ""}, "15265 W Bestor Blvd": {"price": 135600.0, "received": "2026-01-13", "comments": ""}}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0208", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "EAGLE ROOFING PRODUCTS", "active": false, "contact": "Jim McGeehan", "phone": "1 800 300 3245", "cell": "1 818 482 0019", "statusNote": "", "comments": "", "email": "jimm@eagleroofing.com", "bids": {}, "codes": ["071000 Roofing"]}, {"id": "m0209", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "EAGON", "active": true, "contact": "Inho Sohn", "phone": "1-916-770-7614", "cell": "", "statusNote": "", "comments": "", "email": "insohn@gmail.com", "bids": {"1080 El Medio Place": {"price": 518343.0, "received": "2025-10-24", "comments": "Check; Correct elements"}, "1093 Palms Blvd": {"price": 116092.5, "received": "2025-11-26", "comments": ""}}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0210", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "EARTH CONCEPTS", "active": true, "contact": "Sammy Castro", "phone": "1 760 534 1000", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0211", "div": "DIVISION 10", "divName": "SPECIALTIES", "code": "103000 Fireplace", "company": "EARTHCORE INDUSTRIES, INC.", "active": true, "contact": "Rick Ertel", "phone": "1 805 484 7350", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["103000 Fireplace"]}, {"id": "m0212", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "EAST WEST ELECTRIC", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "NEW", "email": "eastwestelec@gmail.com", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0213", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "073313 Green Roof", "company": "EBERHARD ROOFING", "active": true, "contact": "Rick Boyce", "phone": "1 818 782 4604", "cell": "", "statusNote": "", "comments": "", "email": "rboyce@eberhardcom.com", "bids": {}, "codes": ["073313 Green Roof", "071000 Roofing"]}, {"id": "m0214", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "EBERHARD SMC", "active": true, "contact": "Russ Olinger", "phone": "818.782.4604", "cell": "", "statusNote": "", "comments": "", "email": "hamparo@eberhardco.com", "bids": {}, "codes": ["071000 Roofing", "074619 Steel Siding"]}, {"id": "m0215", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "ECB", "active": true, "contact": "Ed Williams", "phone": "1 818 889 2831", "cell": "1 818 612 8856", "statusNote": "", "comments": "", "email": "info@ecbelectric.com, edw@ecbelectric.com", "bids": {}, "codes": ["260500 Electric Rough & Finish", "269900 Electric Fixtures"]}, {"id": "m0216", "div": "DIVISION 09", "divName": "FINISHES", "code": "096400 Wood Flooring", "company": "EDDIE EGAN AND ASSOCIATES", "active": true, "contact": "", "phone": "1 310 559 4341", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["096400 Wood Flooring"]}, {"id": "m0217", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "EDGAR", "active": true, "contact": "Alu. Slider doors", "phone": "818-300-2239", "cell": "", "statusNote": "", "comments": "NO RESPONSE", "email": "edgardoeuceda01@yahoo.com", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0218", "div": "DIVISION 21", "divName": "FIRE SUPPRESSION", "code": "211300 Fire Spinklers", "company": "EDISON FIRE", "active": true, "contact": "Rick Hawa", "phone": "1 323 259 9999", "cell": "", "statusNote": "", "comments": "X", "email": "rick@edison-fire.com", "bids": {}, "codes": ["211300 Fire Spinklers"]}, {"id": "m0219", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "Eggersmann Usa", "active": true, "contact": "James McCabe", "phone": "323-420-7322", "cell": "", "statusNote": "", "comments": "", "email": "alexi.knight@eggersmannusa.com", "bids": {"429 Sherman Canal": {"price": 120438.6, "received": "2025-08-05", "comments": ""}, "865 N Oreo Pl": {"price": 423020.0, "received": null, "comments": ""}, "1080 El Medio Place": {"price": 275500.0, "received": "2025-12-04", "comments": ""}, "4565 Dundee Drive": {"price": 176000.0, "received": "2025-12-04", "comments": "ROUGH NUMBER"}}, "codes": ["064100 Cabinets"]}, {"id": "m0220", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "ELECTRIC BROTHERS", "active": true, "contact": "", "phone": "(562) 354-8900", "cell": "", "statusNote": "", "comments": "NEW", "email": "info@electricbro.com", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0221", "div": "DIVISION 14", "divName": "CONVEYING EQUIPMENT", "code": "142000 Elevators", "company": "Elevator Boutique", "active": true, "contact": "Zeke Poulton", "phone": "(855) 326-8847", "cell": "", "statusNote": "", "comments": "", "email": "zeke@elevatorboutique.com", "bids": {"865 N Oreo Pl": {"price": 58290.0, "received": "2025-10-24", "comments": ""}, "807 6th Ave": {"price": 2859.63, "received": "2025-11-30", "comments": ""}, "15265 W Bestor Blvd": {"price": 65855.5, "received": "2025-10-28", "comments": ""}}, "codes": ["142000 Elevators"]}, {"id": "m0222", "div": "DIVISION 14", "divName": "CONVEYING EQUIPMENT", "code": "142000 Elevators", "company": "ELEVATTO BOUTIQUE", "active": true, "contact": "John F. Mielke", "phone": "909-625-2299", "cell": "909-238-3313", "statusNote": "", "comments": "", "email": "johnmielke686@aol.com", "bids": {"807 6th Ave": {"price": 82092.43, "received": null, "comments": ""}}, "codes": ["142000 Elevators"]}, {"id": "m0223", "div": "DIVISION 05", "divName": "METALS", "code": "051200 Structural Steel", "company": "ELI INDUSTRIES", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["051200 Structural Steel"]}, {"id": "m0224", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "ELITE ENGINEER", "active": true, "contact": "Omar Vinas", "phone": "(562) 277-6201", "cell": "", "statusNote": "EMAIL UPDATED", "comments": "", "email": "omar@eliteengineering.net", "bids": {"807 6th Ave": {"price": 29955.0, "received": "2025-10-09", "comments": ""}}, "codes": ["024000 Demolition", "033100 Structural Concrete", "131100 Swimming Pool/Spa/Fountain"]}, {"id": "m0225", "div": "DIVISION 03", "divName": "CONCRETE", "code": "031113 Shoring", "company": "ELITE ENGINEERING", "active": true, "contact": "Omar Vinas", "phone": "(562) 277-6201", "cell": "", "statusNote": "EMAIL UPDATED", "comments": "VOICE MAIL", "email": "omar@eliteengineering.net", "bids": {"865 N Oreo Pl": {"price": 153270.0, "received": null, "comments": "Includes pool piles"}}, "codes": ["031113 Shoring"]}, {"id": "m0226", "div": "DIVISION 09", "divName": "FINISHES", "code": "096400 Wood Flooring", "company": "ELITE FLOOR COVERING", "active": true, "contact": "Hardwood Floors", "phone": "310.231.5111", "cell": "310.902 2780", "statusNote": "", "comments": "", "email": "info@eliteflooringsolutions.com", "bids": {"1134 Iliff St": {"price": 26618.08, "received": "2026-04-06", "comments": ""}}, "codes": ["096400 Wood Flooring"]}, {"id": "m0227", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "323100 Fences & Gates", "company": "ELITE GATES", "active": true, "contact": "Ron Albert", "phone": "1 310 456 2500", "cell": "", "statusNote": "", "comments": "", "email": "service@elitegates.net", "bids": {}, "codes": ["323100 Fences & Gates"]}, {"id": "m0228", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "017423 Final Clean-up", "company": "ELITE SERVICES", "active": true, "contact": "Sage Teke", "phone": "1 323 924 5330", "cell": "", "statusNote": "", "comments": "", "email": "sales@elitemaidsla.com", "bids": {}, "codes": ["017423 Final Clean-up"]}, {"id": "m0229", "div": "DIVISION 03", "divName": "CONCRETE", "code": "031113 Shoring", "company": "ELLIOTT DRILLING", "active": true, "contact": "Mark Elliott", "phone": "760-421-9840", "cell": "", "statusNote": "", "comments": "NO PICK UP THE PHONE", "email": "mark.elliott@elliottdrilling.com", "bids": {}, "codes": ["031113 Shoring"]}, {"id": "m0230", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "ELLIOTT DRILLING SERVICES, INC.", "active": false, "contact": "Mark Elliott", "phone": "760.722.1400", "cell": "760.421.9640", "statusNote": "", "comments": "", "email": "mark.elliott@elliottdrilling.com", "bids": {}, "codes": ["024000 Demolition"]}, {"id": "m0231", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "072100 Insulation", "company": "ELM INSULATION", "active": true, "contact": "", "phone": "(818) 798-9723", "cell": "", "statusNote": "NEW", "comments": "", "email": "info@elminsulation.com", "bids": {}, "codes": ["072100 Insulation"]}, {"id": "m0232", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081004 Garage Doors", "company": "EM GARAGE DOORS AND GATE SERVICE", "active": true, "contact": "", "phone": "818-919-0785", "cell": "", "statusNote": "NEW", "comments": "", "email": "emgaragedoorsandgates@gmail.com", "bids": {}, "codes": ["081004 Garage Doors"]}, {"id": "m0233", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "EMC HVAC", "active": true, "contact": "Esvin Morales", "phone": "", "cell": "", "statusNote": "NEW", "comments": "", "email": "emc15hvac@gmail.com", "bids": {"1134 Iliff St": {"price": 59600.0, "received": "2026-04-13", "comments": ""}}, "codes": ["230000 Hvac"]}, {"id": "m0234", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "EMMONS", "active": false, "contact": "Jeff Dillingham", "phone": "1 626 820 0909", "cell": "emmonsroof@gmail.com", "statusNote": "", "comments": "NO RESIDENTIAL PROJECTS", "email": "jeff@emmonsroof.com", "bids": {}, "codes": ["071000 Roofing"]}, {"id": "m0235", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "481400 Solar Energy Electrical Power Generation Equipment", "company": "ENERGY OPTIONS", "active": true, "contact": "Scott Meyer", "phone": "1 661 209 7987", "cell": "1 818 730 4900", "statusNote": "", "comments": "", "email": "scott.m@energyoptions-wind.com", "bids": {}, "codes": ["481400 Solar Energy Electrical Power Generation Equipment"]}, {"id": "m0236", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "EPCO PLUMBING", "active": true, "contact": "Eric Poquette", "phone": "1 714 898 3039", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["220000 Plumbing Rough & Finish", "334000 Stormwater management-LID"]}, {"id": "m0237", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "022600 Asbestos", "company": "ERC ENVIROMENTAL ( REMOVAL)", "active": true, "contact": "Francisco Arcila", "phone": "714-232-2278", "cell": "", "statusNote": "", "comments": "", "email": "arcila@erc-removal.com", "bids": {}, "codes": ["022600 Asbestos"]}, {"id": "m0238", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "250010 Security Systems", "company": "ESS SYSTEMS", "active": true, "contact": "Anthony Marino", "phone": "1 818 541 1091", "cell": "", "statusNote": "", "comments": "", "email": "tony@esssystems.com, vince@esssystems.com", "bids": {}, "codes": ["250010 Security Systems"]}, {"id": "m0239", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "ETIVISTA CONCRETE", "active": false, "contact": "Marco Dicarlo", "phone": "1 909 899 1796", "cell": "mike@etivista.com", "statusNote": "", "comments": "", "email": "marco@etivista.com, mario@etivista.com", "bids": {}, "codes": ["030630 Concrete Slab", "033100 Structural Concrete", "042200 Concrete Masonry Unit"]}, {"id": "m0240", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "ETO DOORS", "active": true, "contact": "", "phone": "1 213 622 2003", "cell": "", "statusNote": "CALL", "comments": "REPEATED", "email": "sales@etodoors.com", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0241", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "062000 Finish Carpentry", "company": "EUROTECH", "active": false, "contact": "Steve Davies", "phone": "1 310 497 2079", "cell": "1 310 430 1715", "statusNote": "", "comments": "Mail needs to be updated", "email": "steve@eurotechconstruction.com", "bids": {}, "codes": ["062000 Finish Carpentry", "077700 Waterproofing Build. Wrap", "074623 Wood Siding"]}, {"id": "m0242", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "062000 Finish Carpentry", "company": "EUROTECH CONSTRUCTION", "active": false, "contact": "", "phone": "310-476-8699", "cell": "2 310 430 1715", "statusNote": "", "comments": "Mail needs to be updated", "email": "steve@eurotechconstruction.com", "bids": {}, "codes": ["062000 Finish Carpentry"]}, {"id": "m0243", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "072100 Insulation", "company": "EVERGUARD INSULATION", "active": true, "contact": "", "phone": "818.348.1460", "cell": "310.274.5644", "statusNote": "NEW", "comments": "", "email": "steve@everguardinsulation.com", "bids": {}, "codes": ["072100 Insulation"]}, {"id": "m0244", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "EXCLUSIVELY ELECTRIC, INC.", "active": false, "contact": "Clayton Reed", "phone": "(714) 307-6194", "cell": "1 661 857 3628", "statusNote": "", "comments": "", "email": "kyle@exclusiveelectric.com", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0245", "div": "DIVISION 04", "divName": "MASONRY", "code": "042100 Masonry Brick Veneer", "company": "EXECUTIVE STONE", "active": true, "contact": "Noah Tal", "phone": "1 818 765 0900", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["042100 Masonry Brick Veneer", "096000 Tile - Material"]}, {"id": "m0246", "div": "DIVISION 22", "divName": "PLUMBING", "code": "223200 Domestic Water Filtration Equipment", "company": "EXPERT", "active": true, "contact": "Marcos Uriate", "phone": "1 562 529 8537", "cell": "1 310 600 0073", "statusNote": "", "comments": "", "email": "mauriarte@expertplumbinginc.com", "bids": {}, "codes": ["223200 Domestic Water Filtration Equipment", "224000 Plumbing Fixtures", "334000 Stormwater management-LID"]}, {"id": "m0247", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "EXPERT Plumbing", "active": true, "contact": "Marcos Uriate", "phone": "1 562 529 8537", "cell": "1 310 600 0073", "statusNote": "", "comments": "", "email": "mauriarte@expertplumbinginc.com", "bids": {"52-60 Market St": {"price": 479872.0, "received": "2025-06-12", "comments": ""}}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0248", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "EXPRESS", "active": true, "contact": "", "phone": "(310) 625-7305", "cell": "", "statusNote": "NEW", "comments": "", "email": "service@expressac.com", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0249", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "EXPRESS GLASS & MIRROR", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "Says he hasn't seen the previous invitations", "email": "expressglassmirror@gmail.com", "bids": {}, "codes": ["058000 Glazing"]}, {"id": "m0250", "div": "DIVISION 09", "divName": "FINISHES", "code": "096400 Wood Flooring", "company": "FAME HARDWOOD", "active": true, "contact": "Siobhan Angli", "phone": "1 855 666 3263", "cell": "", "statusNote": "", "comments": "", "email": "siobhan@famehardwood.com", "bids": {"17797 Camino De Yatasto": {"price": 219842.39, "received": "2025-11-01", "comments": ""}, "865 N Oreo Pl": {"price": 63098.65, "received": "2025-11-08", "comments": ""}, "807 6th Ave": {"price": 89473.64, "received": "2025-10-03", "comments": "5K discount for floor called Fire Oak that is on sale and is similar in look"}, "1080 El Medio Place": {"price": 63090.65, "received": "2025-11-08", "comments": "Check;"}, "15265 W Bestor Blvd": {"price": 167602.96, "received": "2025-10-28", "comments": ""}, "12979 Blairwood Dr": {"price": 123823.37, "received": "2026-02-07", "comments": ""}}, "codes": ["096400 Wood Flooring"]}, {"id": "m0251", "div": "DIVISION 31", "divName": "EARTHWORK", "code": "312300 Excavation & Backfill", "company": "FARENBAUGH", "active": true, "contact": "Mike Farenbaugh", "phone": "1 818 367 7271", "cell": "1 818 402 2329", "statusNote": "", "comments": "", "email": "jfarenbaugh@roadrunner.com", "bids": {}, "codes": ["312300 Excavation & Backfill", "312500 Erosion Controls", "334000 Stormwater management-LID"]}, {"id": "m0252", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "FENCESCREEN, INC.", "active": true, "contact": "Fence Banners", "phone": "27002 Vista Terrace", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0253", "div": "DIVISION 22", "divName": "PLUMBING", "code": "224000 Plumbing Fixtures", "company": "FERGUSON", "active": true, "contact": "Matthew Sasldana", "phone": "1 310 829 3371", "cell": "", "statusNote": "HIGHLY ACTIVE", "comments": "POSSIBLE NEGOCIATION", "email": "matthew.saldana@ferguson.com, christian.lua-lopez@ferguson.com, mattew.saldana@ferguson.com, katie.grachen@ferguson.com", "bids": {"1080 El Medio Place": {"price": 32528.61, "received": "2025-10-24", "comments": "Check;"}, "15265 W Bestor Blvd": {"price": 60324.33, "received": "2025-10-31", "comments": "Appliances for $73,326.09"}, "2429 Eastern Canal": {"price": 29221.6, "received": "2025-11-26", "comments": ""}, "16339 Akron": {"price": 20934.95, "received": null, "comments": "Also sent appliances"}, "4565 Dundee Drive": {"price": 11591.19, "received": "2025-11-25", "comments": ""}, "1093 Palms Blvd": {"price": 11382.0, "received": "2025-11-24", "comments": ""}}, "codes": ["224000 Plumbing Fixtures", "113000 Residential Equipment", "102800 Toilet/Bathrom Accessories"]}, {"id": "m0254", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "FERNANDO DAVILA & SONS", "active": true, "contact": "Fernando Davila", "phone": "1 310 329 7493", "cell": "1 310 938 3905", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["024000 Demolition"]}, {"id": "m0255", "div": "DIVISION 12", "divName": "FURNISHINGS", "code": "122000 Window Treatments", "company": "FINE DRAPERIES", "active": true, "contact": "Mark Horwitz", "phone": "1 818 989 5567", "cell": "", "statusNote": "", "comments": "", "email": "mark@finedrapes.com", "bids": {}, "codes": ["122000 Window Treatments"]}, {"id": "m0256", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "062000 Finish Carpentry", "company": "FINELINE", "active": true, "contact": "Marc Butman", "phone": "1 714 345 7718", "cell": "", "statusNote": "", "comments": "", "email": "marc@finelinewood.com", "bids": {"429 Sherman Canal": {"price": 125531.0, "received": "2025-08-01", "comments": ""}}, "codes": ["062000 Finish Carpentry", "074623 Wood Siding"]}, {"id": "m0257", "div": "DIVISION 10", "divName": "SPECIALTIES", "code": "103000 Fireplace", "company": "FIREPLACE GUYS", "active": true, "contact": "", "phone": "(310)320-2785", "cell": "", "statusNote": "", "comments": "", "email": "lori.fireplaceguys@sbcglobal.net", "bids": {}, "codes": ["103000 Fireplace"]}, {"id": "m0258", "div": "DIVISION 10", "divName": "SPECIALTIES", "code": "103000 Fireplace", "company": "FIREPLACE GUYS, INC.", "active": true, "contact": "Brad Angeleri", "phone": "1 310 320 2785", "cell": "1 310 529 7132", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["103000 Fireplace"]}, {"id": "m0259", "div": "DIVISION 21", "divName": "FIRE SUPPRESSION", "code": "211300 Fire Spinklers", "company": "FIRESAFE GROUP", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "REPEATED", "comments": "X", "email": "joseph@firesafesystems.com", "bids": {"52-60 Market St": {"price": 51800.0, "received": "2025-01-22", "comments": ""}}, "codes": ["211300 Fire Spinklers"]}, {"id": "m0260", "div": "DIVISION 10", "divName": "SPECIALTIES", "code": "103000 Fireplace", "company": "FIRESIDE EXPERTS", "active": true, "contact": "Benjamin Thompson", "phone": "(818) 764-3366", "cell": "", "statusNote": "", "comments": "", "email": "bthompson@ohdfiresideexperts.com", "bids": {}, "codes": ["103000 Fireplace"]}, {"id": "m0261", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "323100 Fences & Gates", "company": "FIRST ACCESS CONTROL", "active": true, "contact": "Don", "phone": "8059559230.0", "cell": "8184621567.0", "statusNote": "", "comments": "", "email": "don.1stclassaccesscontrol@gmail.com", "bids": {}, "codes": ["323100 Fences & Gates"]}, {"id": "m0262", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "062000 Finish Carpentry", "company": "FIRST CLASS", "active": true, "contact": "Scott Kindseth", "phone": "1 818 888 0590", "cell": "1 818 266 0650", "statusNote": "", "comments": "", "email": "scottkindseth@gmail.com", "bids": {}, "codes": ["062000 Finish Carpentry", "074623 Wood Siding"]}, {"id": "m0263", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "FIRST RATE REMODELING", "active": true, "contact": "Robert Cline", "phone": "714 922-0014", "cell": "", "statusNote": "", "comments": "NEW-SUB", "email": "robert@firstrateremodeling.com", "bids": {"478 Wynola St": {"price": 45088.28, "received": "2025-09-26", "comments": "Only windows & glass door"}}, "codes": ["081001 Exterior Doors & Windows Installation", "074623 Wood Siding"]}, {"id": "m0264", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "323100 Fences & Gates", "company": "FIVE STAR", "active": true, "contact": "Romuald Hardy", "phone": "1 818 890 0500", "cell": "1 818 426 0283", "statusNote": "", "comments": "", "email": "rhardy@fivestarfences.com", "bids": {}, "codes": ["323100 Fences & Gates"]}, {"id": "m0265", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "FLOOD BROTHERS", "active": true, "contact": "", "phone": "1 855 840 7800", "cell": "", "statusNote": "NEW", "comments": "", "email": "support@floodbrothersplumbing.com", "bids": {}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0266", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Installation", "company": "Flooring Los Angeles", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "estimate@flooringlosangeles.com", "bids": {"478 Wynola St": {"price": 17720.0, "received": "2025-09-02", "comments": ""}, "16339 Akron": {"price": 37825.0, "received": null, "comments": ""}}, "codes": ["096000 Tile - Installation"]}, {"id": "m0267", "div": "DIVISION 09", "divName": "FINISHES", "code": "096800 Carpet", "company": "FLOORS PLUS", "active": true, "contact": "Glen Allen", "phone": "1 805 651 9650", "cell": "", "statusNote": "", "comments": "", "email": "floorsplusnow@gmail.com", "bids": {}, "codes": ["096800 Carpet"]}, {"id": "m0268", "div": "DIVISION 21", "divName": "FIRE SUPPRESSION", "code": "211300 Fire Spinklers", "company": "FORERUNNER FIRE PREVENTION, INC.", "active": true, "contact": "Nicholas De Sio", "phone": "1 818 842 6911", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["211300 Fire Spinklers"]}, {"id": "m0269", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "FORTUNY AIR", "active": true, "contact": "", "phone": "323-578-4334", "cell": "", "statusNote": "", "comments": "", "email": "info@fortuny-air.com", "bids": {"Quadro Vecchio": {"price": 45800.0, "received": "2025-07-29", "comments": "WILL PROVIDE BY 07/14/25"}, "478 Wynola St": {"price": 17800.0, "received": "2025-09-11", "comments": ""}, "865 N Oreo Pl": {"price": 66150.0, "received": "2025-10-24", "comments": ""}, "4565 Dundee Drive": {"price": 51800.0, "received": "2025-12-03", "comments": ""}, "1093 Palms Blvd": {"price": 15699.0, "received": "2026-02-03", "comments": ""}, "16339 Akron": {"price": 65846.0, "received": "2026-01-05", "comments": ""}}, "codes": ["230000 Hvac"]}, {"id": "m0270", "div": "DIVISION 05", "divName": "METALS", "code": "051200 Structural Steel", "company": "FOUGHT & COMPANY", "active": true, "contact": "Katie Williams", "phone": "(503) 639-3141", "cell": "", "statusNote": "NEW", "comments": "", "email": "kwilliams@foughtsteel.com", "bids": {}, "codes": ["051200 Structural Steel"]}, {"id": "m0271", "div": "DIVISION 04", "divName": "MASONRY", "code": "042100 Masonry Brick Veneer", "company": "FOUNDATION BUILDING MATERIALS", "active": true, "contact": "Bldg. Materials", "phone": "818.579.4910", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["042100 Masonry Brick Veneer"]}, {"id": "m0272", "div": "DIVISION 03", "divName": "CONCRETE", "code": "031113 Shoring", "company": "FOUS BUILDERS INC.", "active": true, "contact": "Norman Salter", "phone": "(310) 820-0550", "cell": "(310) 261-2092", "statusNote": "", "comments": "NO BID, NO TIME", "email": "nsalter@focusbuildersinc.com", "bids": {}, "codes": ["031113 Shoring"]}, {"id": "m0273", "div": "DIVISION 09", "divName": "FINISHES", "code": "099000 Painting", "company": "FRESHCO PAINTERS", "active": true, "contact": "", "phone": "(626) 600-6448", "cell": "", "statusNote": "", "comments": "", "email": "angel@freshcopainters.com", "bids": {}, "codes": ["099000 Painting"]}, {"id": "m0274", "div": "DIVISION 21", "divName": "FIRE SUPPRESSION", "code": "211300 Fire Spinklers", "company": "FRONTLINE WILD FIRE", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "NEW", "comments": "", "email": "", "bids": {}, "codes": ["211300 Fire Spinklers"]}, {"id": "m0275", "div": "DIVISION 09", "divName": "FINISHES", "code": "096400 Wood Flooring", "company": "FUHRMANN FLOORS, INC.", "active": true, "contact": "Warren Hogge", "phone": "1 818 886 3198", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["096400 Wood Flooring"]}, {"id": "m0276", "div": "DIVISION 09", "divName": "FINISHES", "code": "099000 Painting", "company": "FULL SPECTRUM CUSTOM PAINTING", "active": true, "contact": "Keith Helgeson", "phone": "1 909 986 2264", "cell": "", "statusNote": "", "comments": "", "email": "fullspectrumptg@hotmail.com", "bids": {}, "codes": ["099000 Painting"]}, {"id": "m0277", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "FUNTIME CABINET FACTORY", "active": true, "contact": "Shawn Belschner", "phone": "818-882-2281", "cell": "818-259-0942", "statusNote": "", "comments": "", "email": "shawn@funtimecabinetfactory.com", "bids": {"52-60 Market St": {"price": 37735.76, "received": "2025-05-21", "comments": ""}, "Quadro Vecchio": {"price": 135208.86, "received": "2025-07-15", "comments": ""}, "723 OFW": {"price": 153636.89, "received": "2025-07-24", "comments": ""}, "748 & 750 Palisades Dr": {"price": 85555.11, "received": "2025-08-02", "comments": ""}, "865 N Oreo Pl": {"price": 267562.28, "received": "2025-11-13", "comments": ""}, "807 6th Ave": {"price": 55844.62, "received": "2025-10-04", "comments": "Discount request declined"}, "4565 Dundee Drive": {"price": 267562.28, "received": "2025-11-12", "comments": "include all, rooms, bathrooms, kitchen"}}, "codes": ["064100 Cabinets"]}, {"id": "m0278", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "G.Leon Landscaping", "active": true, "contact": "Chris", "phone": "", "cell": "", "statusNote": "", "comments": "will sen", "email": "chris@gleonlandscape.com", "bids": {"723 OFW": {"price": 56354.0, "received": "2025-08-14", "comments": ""}}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0279", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "014533 Utilities", "company": "GATES ENTERPRISES", "active": true, "contact": "Dirt Hauling", "phone": "714.382.6707", "cell": "714.382.6708", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["014533 Utilities"]}, {"id": "m0280", "div": "DIVISION 05", "divName": "METALS", "code": "055000 Metal Fabricators", "company": "GENERAL PLATING CO. & BRITE PLATING INC.", "active": true, "contact": "Adrian Toledo", "phone": "1 323 234 9201 (Gen)  1 323 263 7593 (Brite)", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["055000 Metal Fabricators"]}, {"id": "m0281", "div": "DIVISION 22", "divName": "PLUMBING", "code": "224000 Plumbing Fixtures", "company": "GEORGE'S PIPE & PLUMBING", "active": true, "contact": "Bob Arnold", "phone": "1 626 792 5547", "cell": "", "statusNote": "", "comments": "", "email": "boba@georgesshowroom.com", "bids": {}, "codes": ["224000 Plumbing Fixtures"]}, {"id": "m0282", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "GIBIN CUSTOM STAIRS & MILLWORK", "active": false, "contact": "Patrick", "phone": "951-746-4719", "cell": "", "statusNote": "", "comments": "", "email": "hi@gibinremodeling.com", "bids": {"429 Sherman Canal": {"price": 207155.0, "received": "2025-07-11", "comments": ""}, "748 & 750 Palisades Dr": {"price": 66795.0, "received": "2025-08-06", "comments": ""}, "865 N Oreo Pl": {"price": 141926.44, "received": "2025-11-20", "comments": ""}, "1080 El Medio Place": {"price": 115335.16, "received": "2025-11-17", "comments": ""}, "4565 Dundee Drive": {"price": 38654.9, "received": "2025-11-20", "comments": ""}, "1093 Palms Blvd": {"price": 38654.9, "received": "2025-11-20", "comments": ""}, "2429 Eastern Canal": {"price": 29457.52, "received": "2025-12-04", "comments": ""}, "16339 Akron": {"price": 95399.77, "received": null, "comments": "Includes all the house cabinets and installation"}}, "codes": ["064100 Cabinets"]}, {"id": "m0283", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071010 Waterproofing", "company": "GNO WATERPROOFING", "active": true, "contact": "", "phone": "(323)-230-3006", "cell": "", "statusNote": "NEW", "comments": "", "email": "estimate@gnowaterproofing.com", "bids": {}, "codes": ["071010 Waterproofing"]}, {"id": "m0284", "div": "DIVISION 09", "divName": "FINISHES", "code": "099000 Painting", "company": "GPS", "active": true, "contact": "Hugo Camacho", "phone": "1 714 730 8904", "cell": "1 949 254 4228", "statusNote": "", "comments": "", "email": "hcamacho@gpspainting.com", "bids": {}, "codes": ["099000 Painting"]}, {"id": "m0285", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "GRAND HVAC", "active": true, "contact": "Jessy Perets", "phone": "1 323 870 2923", "cell": "", "statusNote": "CALL", "comments": "", "email": "grandhtg01@sbcglobal.net, office@grandhvac.com", "bids": {"213 OFW Waterfront": {"price": 28900.0, "received": "2025-07-30", "comments": ""}, "17797 Camino De Yatasto": {"price": 175000.0, "received": "2025-11-05", "comments": "BUDGET"}, "807 6th Ave": {"price": 158000.0, "received": "2025-11-05", "comments": ""}, "15265 W Bestor Blvd": {"price": 105000.0, "received": "2025-12-19", "comments": ""}}, "codes": ["230000 Hvac"]}, {"id": "m0286", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "GREAT WESTERN", "active": true, "contact": "Abel Luna", "phone": "1 818 891 4586", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0287", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081004 Garage Doors", "company": "GREEN GARAGE DOOR & REPAIR", "active": true, "contact": "", "phone": "(818) 392 5110", "cell": "", "statusNote": "NEW", "comments": "", "email": "localgaragedoors5@gmail.com", "bids": {}, "codes": ["081004 Garage Doors"]}, {"id": "m0288", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "GREEN TREE LANDSCAPING, INC.", "active": true, "contact": "Michael Baer", "phone": "1 323 468 9740", "cell": "", "statusNote": "", "comments": "email was wrong", "email": "jmbaer@greentreela.com, info@greentreela.com", "bids": {}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0289", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "GROUND UP CONSTRUCTION", "active": true, "contact": "Nelson Erazo", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "erazo13nelson@gmail.com", "bids": {"807 6th Ave": {"price": 24000.0, "received": "2025-10-10", "comments": ""}, "16339 Akron": {"price": 28000.0, "received": "2026-01-07", "comments": ""}}, "codes": ["092400 Stucco"]}, {"id": "m0290", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "GROUNDTECH", "active": true, "contact": "", "phone": "310-327-1740", "cell": "310-988-2891", "statusNote": "Email needs to be updated", "comments": "NO RESPONSE", "email": "jim@geosupport.com", "bids": {}, "codes": ["024000 Demolition", "031113 Shoring", "033100 Structural Concrete"]}, {"id": "m0291", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "073313 Green Roof", "company": "GSKY", "active": true, "contact": "Doug Veith", "phone": "1 917 804 3597", "cell": "", "statusNote": "", "comments": "", "email": "doug@g-sky.com", "bids": {}, "codes": ["073313 Green Roof"]}, {"id": "m0292", "div": "DIVISION 09", "divName": "FINISHES", "code": "092000 Gypsum Board", "company": "GUBUCE BROTHERS, INC.", "active": false, "contact": "Karla Salguero", "phone": "1 310 645 6405", "cell": "1 310 721 1004", "statusNote": "", "comments": "BOUNCED BACK", "email": "karla@gubucebrothers.com", "bids": {}, "codes": ["092000 Gypsum Board"]}, {"id": "m0293", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "077123 Gutters/Downspouts/Water Retention", "company": "GUTTER DEPOT", "active": true, "contact": "", "phone": "888-488-8383", "cell": "", "statusNote": "", "comments": "", "email": "gutterdepot@aol.com", "bids": {}, "codes": ["077123 Gutters/Downspouts/Water Retention"]}, {"id": "m0294", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Installation", "company": "HALL TILE", "active": true, "contact": "Joshua Hall", "phone": "760-265-5918", "cell": "", "statusNote": "", "comments": "Price for 52 Market St // 60 Market St", "email": "joshua77hall@gmail.com", "bids": {"Quadro Vecchio": {"price": 8786.98, "received": "2025-07-28", "comments": ""}, "748 & 750 Palisades Dr": {"price": 29498.0, "received": "2025-08-07", "comments": ""}, "478 Wynola St": {"price": 14904.8, "received": "2025-09-02", "comments": ""}, "6537 Topanga Canyon": {"price": 20300.0, "received": "2026-02-18", "comments": ""}, "12979 Blairwood Dr": {"price": 24000.0, "received": "2026-02-18", "comments": ""}}, "codes": ["096000 Tile - Installation"]}, {"id": "m0295", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "061000 Rough Carpentry", "company": "HAMMERHEAD", "active": false, "contact": "Lance Wyatt", "phone": "1 805 289 1588", "cell": "1 310 463 6757", "statusNote": "", "comments": "New Email address", "email": "info.hammerheadbuilders@gmail.com", "bids": {}, "codes": ["061000 Rough Carpentry"]}, {"id": "m0296", "div": "DIVISION 05", "divName": "METALS", "code": "051200 Structural Steel", "company": "HANLEY'S WELDING", "active": true, "contact": "Tony", "phone": "310-8920616", "cell": "", "statusNote": "", "comments": "", "email": "hwelding@earthlink.net", "bids": {}, "codes": ["051200 Structural Steel"]}, {"id": "m0297", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "061000 Rough Carpentry", "company": "HANOVER BUILDERS", "active": false, "contact": "Scott Silverman", "phone": "1 805 374 8684", "cell": "1 818 519 1375", "statusNote": "", "comments": "EMAIL UPDATED;NO RESPONSE ON CALL 10/16/25", "email": "office@hanoverbuildersinc.com", "bids": {}, "codes": ["061000 Rough Carpentry"]}, {"id": "m0298", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "HARO'S TREE SERVICE", "active": true, "contact": "", "phone": "323-993-1070", "cell": "818-970-8399", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0299", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "HAROLD JONES LANDSCAPE", "active": true, "contact": "Jason Sanders", "phone": "1 805 582 7443", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0300", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "HEATING & AIR LIONS", "active": true, "contact": "", "phone": "(866) 430-3950", "cell": "", "statusNote": "NEW", "comments": "", "email": "info@lionshvac.com", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0301", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "HECTOR'S ROOFING", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "hectorsroofingservice@gmail.com", "bids": {}, "codes": ["071000 Roofing"]}, {"id": "m0302", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "HERITAGE CABINET CO., INC.", "active": false, "contact": "Lisette Tuohy", "phone": "1 818 786 4900", "cell": "", "statusNote": "out of zone", "comments": "New email address", "email": "heritagecabinetco@gmail.com", "bids": {}, "codes": ["064100 Cabinets"]}, {"id": "m0303", "div": "DIVISION 09", "divName": "FINISHES", "code": "096600 Terrazzo", "company": "HERMOSA", "active": true, "contact": "Marv Raupp", "phone": "1 310 951 2075", "cell": "", "statusNote": "", "comments": "", "email": "marv@ilterrasinicorp.com", "bids": {}, "codes": ["096600 Terrazzo"]}, {"id": "m0304", "div": "DIVISION 09", "divName": "FINISHES", "code": "092000 Gypsum Board", "company": "HERRERA CONSTRUCTION", "active": true, "contact": "Adolfo Herrera", "phone": "1 818 391 3133", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["092000 Gypsum Board"]}, {"id": "m0305", "div": "DIVISION 09", "divName": "FINISHES", "code": "092000 Gypsum Board", "company": "HH DRYWALL", "active": true, "contact": "", "phone": "3103465934.0", "cell": "", "statusNote": "", "comments": "", "email": "accounting@hh-drywall.com", "bids": {}, "codes": ["092000 Gypsum Board"]}, {"id": "m0306", "div": "DIVISION 05", "divName": "METALS", "code": "051200 Structural Steel", "company": "HIGH RISE STEEL", "active": true, "contact": "", "phone": "323 5480707", "cell": "", "statusNote": "NEW", "comments": "", "email": "info@highrisesteel.co, highrisesteelca@gmail.com", "bids": {}, "codes": ["051200 Structural Steel"]}, {"id": "m0307", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "HIGHPIONT ROOFING CO.", "active": true, "contact": "Derrick Maldonado", "phone": "323-945-4083", "cell": "909-600-7745", "statusNote": "", "comments": "", "email": "highpointroofing@hotmail.com", "bids": {}, "codes": ["071000 Roofing"]}, {"id": "m0308", "div": "DIVISION 05", "divName": "METALS", "code": "051200 Structural Steel", "company": "HILO ERECTORS", "active": false, "contact": "", "phone": "530 7510354", "cell": "", "statusNote": "", "comments": "", "email": "hilo@hiloerectors.com", "bids": {}, "codes": ["051200 Structural Steel"]}, {"id": "m0309", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "HITECH ROOTER", "active": true, "contact": "Andre Setian", "phone": "818.558.7070", "cell": "818.968.8995", "statusNote": "", "comments": "", "email": "andresetian@hotmail.com", "bids": {}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0310", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "HOLLYWOOD", "active": true, "contact": "Irwin Tuchfeld/ Aaron", "phone": "1 323 661 7774", "cell": "", "statusNote": "", "comments": "They\u2019ve received bid requests but don\u2019t know the company; prefer a meeting before bidding; available after 11am in his office", "email": "hollywoodglass@sbcglobal.net", "bids": {}, "codes": ["058000 Glazing"]}, {"id": "m0311", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "262000 Low Voltage", "company": "HOME CONTROL", "active": true, "contact": "Joe Anderson", "phone": "1 310 578 2006", "cell": "", "statusNote": "", "comments": "", "email": "joe@myhomecontrol.com", "bids": {}, "codes": ["262000 Low Voltage"]}, {"id": "m0312", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "HOPE'S", "active": false, "contact": "Ryne Johnson", "phone": "1 716 665 5124 x260", "cell": "1 716 485 1135", "statusNote": "", "comments": "", "email": "rjohnson@hopeswindows.com", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0313", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "HUGHES A TO Z", "active": true, "contact": "", "phone": "1 310 397 2110", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0314", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "HY GLOBAL LLC/Cabinets& Countertops", "active": true, "contact": "Celine Sleem", "phone": "(818) 669-9923", "cell": "(310) 272-3145", "statusNote": "HIGHLY ACTIVE", "comments": "", "email": "celine@hygloballlc.com, bryce@hygloballlc.com", "bids": {"723 OFW": {"price": 44914.63, "received": "2025-08-11", "comments": ""}, "17797 Camino De Yatasto": {"price": 38116.53, "received": "2025-11-13", "comments": ""}, "865 N Oreo Pl": {"price": 17190.71, "received": "2025-11-26", "comments": ""}, "12979 Blairwood Dr": {"price": 31838.19, "received": "2026-02-13", "comments": ""}, "1134 Iliff St": {"price": 11953.44, "received": "2026-04-14", "comments": ""}}, "codes": ["064100 Cabinets", "093600 Countertops"]}, {"id": "m0315", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "IKDUSA", "active": true, "contact": "Mina Park", "phone": "424-333-4511", "cell": "", "statusNote": "HIGHLY ACTIVE", "comments": "", "email": "marta@ikdusa.com, mina@ikdusa.com", "bids": {"429 Sherman Canal": {"price": 71000.0, "received": "27/06/2025", "comments": ""}, "17797 Camino De Yatasto": {"price": 320000.0, "received": "2025-11-13", "comments": ""}, "865 N Oreo Pl": {"price": 163600.0, "received": "2025-11-18", "comments": ""}, "1080 El Medio Place": {"price": 115500.0, "received": "2025-11-19", "comments": "Check;"}, "15265 W Bestor Blvd": {"price": 241000.0, "received": "2025-11-22", "comments": ""}, "4565 Dundee Drive": {"price": 41400.0, "received": "2025-11-23", "comments": ""}, "1093 Palms Blvd": {"price": 55000.0, "received": "2025-11-21", "comments": ""}, "2429 Eastern Canal": {"price": 49400.0, "received": "2025-12-03", "comments": ""}}, "codes": ["064100 Cabinets"]}, {"id": "m0316", "div": "DIVISION 22", "divName": "PLUMBING", "code": "224000 Plumbing Fixtures", "company": "IN-EX", "active": true, "contact": "Ali Alam", "phone": "1 310 358 0500", "cell": "", "statusNote": "", "comments": "", "email": "ali.alam@inexsite.com", "bids": {}, "codes": ["224000 Plumbing Fixtures"]}, {"id": "m0317", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "INDEPENDENT CONCRETE CUTTING,  INC.", "active": true, "contact": "", "phone": "1 800 350 0409", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["030630 Concrete Slab"]}, {"id": "m0318", "div": "DIVISION 08", "divName": "OPENINGS", "code": "086000 Skylights", "company": "INDUSTRIAL", "active": true, "contact": "John Buell", "phone": "1 760 434 6001", "cell": "1 760 822 6001", "statusNote": "", "comments": "", "email": "johnb@industrialskylights.com, brandon@industrialskylights.com, liz@industrialskylights.com", "bids": {"865 N Oreo Pl": {"price": 60596.32, "received": "2025-10-20", "comments": "WORKING ON BID"}}, "codes": ["086000 Skylights"]}, {"id": "m0319", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "INSTANT JUNGLE INT", "active": true, "contact": "Andy Blanton", "phone": "1 714 267 0154", "cell": "", "statusNote": "", "comments": "voicemail", "email": "andy@instantjungle.com", "bids": {}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0320", "div": "DIVISION 08", "divName": "OPENINGS", "code": "086000 Skylights", "company": "INTER-SKY", "active": false, "contact": "David Klaess", "phone": "1 800 972 9112", "cell": "", "statusNote": "", "comments": "", "email": "dklaess@inter-sky.com", "bids": {}, "codes": ["086000 Skylights"]}, {"id": "m0321", "div": "DIVISION 12", "divName": "FURNISHINGS", "code": "122000 Window Treatments", "company": "INTERIOR SERVICES", "active": true, "contact": "Josh Brown", "phone": "1 626 358 4411", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["122000 Window Treatments"]}, {"id": "m0322", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "250000 Home Automation", "company": "INTERIOR SYSTEMS DESIGN, INC.", "active": true, "contact": "Yves Richarz", "phone": "1 818 767 3162", "cell": "1 818 284 0351", "statusNote": "", "comments": "BOUNCED BACK", "email": "yvesr@interiorsystems.net", "bids": {}, "codes": ["250000 Home Automation", "262000 Low Voltage", "270500 Audio Visual Systems"]}, {"id": "m0323", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "Interium Cabinets", "active": true, "contact": "212 767-1727", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "info@interiumcabinets.com", "bids": {"15265 W Bestor Blvd": {"price": 275194.8, "received": null, "comments": ""}, "16339 Akron": {"price": 40358.0, "received": "2025-12-23", "comments": "3 BID OPTIONS ($40,358 / $45,667 / $51,453)"}, "12979 Blairwood Dr": {"price": 102740.0, "received": "2026-02-06", "comments": "Provide more options with more expensive numbers"}, "1134 Iliff St": {"price": 37205.25, "received": "2026-04-07", "comments": "LOWER END BID: $30126.38 - HIGHER END BID: $42319.60 PRICE FOR INSTALLATION IS 15% OF THE PRODUCT PRICE"}}, "codes": ["064100 Cabinets"]}, {"id": "m0324", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "IRS", "active": false, "contact": "Richard Ludt", "phone": "1 323 357 6900", "cell": "", "statusNote": "", "comments": "", "email": "richard@irsdemo.com", "bids": {}, "codes": ["024000 Demolition"]}, {"id": "m0325", "div": "DIVISION 03", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "IRS DEMOLITION", "active": true, "contact": "Arlene Medina", "phone": "(323) 357\u20116900", "cell": "", "statusNote": "Send mail again", "comments": "", "email": "amedina@irsdemo.com", "bids": {}, "codes": ["024000 Demolition"]}, {"id": "m0326", "div": "DIVISION 10", "divName": "SPECIALTIES", "code": "103000 Fireplace", "company": "ISOKERN", "active": true, "contact": "Rick Ertel", "phone": "1 805 484 7350", "cell": "1 805 469 7233", "statusNote": "", "comments": "", "email": "rick.ertel@iso-cal.com", "bids": {}, "codes": ["103000 Fireplace"]}, {"id": "m0327", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "061000 Rough Carpentry", "company": "IWF BUILDERS, INC.", "active": false, "contact": "Josh", "phone": "818.599.2984", "cell": "", "statusNote": "", "comments": "", "email": "office@iwfbuildersinc.com", "bids": {}, "codes": ["061000 Rough Carpentry"]}, {"id": "m0328", "div": "DIVISION 05", "divName": "METALS", "code": "051200 Structural Steel", "company": "J&R STEEL AND WELDING", "active": true, "contact": "", "phone": "818 6099700", "cell": "818 3352529", "statusNote": "NEW", "comments": "", "email": "jandrsteelinc@gmail.com, coby@jandrsteel.com", "bids": {}, "codes": ["051200 Structural Steel"]}, {"id": "m0329", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "J.R.H. ELECTRIC", "active": true, "contact": "Electrical", "phone": "818.366.8497", "cell": "818.368.7849", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0330", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "JACK FARENBAUGH & SONS", "active": false, "contact": "Mike Farenbaugh", "phone": "1 818 367 7271", "cell": "1 818 402 2329", "statusNote": "", "comments": "", "email": "jfarenbaugh@roadrunner.com", "bids": {}, "codes": ["024000 Demolition"]}, {"id": "m0331", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "JACOME'S HAULING", "active": true, "contact": "Javier", "phone": "1 323 200 5346", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["024000 Demolition"]}, {"id": "m0332", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "JAMES COWAN & ASSOCIATES", "active": true, "contact": "Peter Ashley", "phone": "1 310 457 2574", "cell": "", "statusNote": "", "comments": "no answer", "email": "pashley@jhcowan.com", "bids": {}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0333", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "JBW CONCRETE CONSTRUCTION, INC.", "active": true, "contact": "", "phone": "818 402 2242", "cell": "", "statusNote": "", "comments": "Will bid in the future", "email": "jbwccinc@gmail.com", "bids": {"1134 Iliff St": {"price": 73500.0, "received": "2026-04-13", "comments": "BID FOR FOUNDATIONS & CONCRETE SLAB"}}, "codes": ["030630 Concrete Slab", "033100 Structural Concrete", "042200 Concrete Masonry Unit"]}, {"id": "m0334", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "Jesse Bautista", "active": true, "contact": "", "phone": "3107048058.0", "cell": "", "statusNote": "", "comments": "", "email": "jessebautista2@gmail.com", "bids": {}, "codes": ["092400 Stucco"]}, {"id": "m0335", "div": "DIVISION 09", "divName": "FINISHES", "code": "099000 Painting", "company": "Jesse Valdez", "active": true, "contact": "Jesse Valdez", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "valdez.jesse22@yahoo.com", "bids": {}, "codes": ["099000 Painting"]}, {"id": "m0336", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "JG Solar Inc", "active": true, "contact": "Justin", "phone": "9513861505.0", "cell": "", "statusNote": "", "comments": "SEND BY TAS", "email": "justin.g@jgpowercompany.com", "bids": {"17797 Camino De Yatasto": {"price": 275353.06, "received": "2026-04-07", "comments": ""}}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0337", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "JGJ Electrical", "active": true, "contact": "Genaro Catalan", "phone": "310 597-7592", "cell": "", "statusNote": "", "comments": "NEW SUB", "email": "jgj.genaro@yahoo.com", "bids": {"6537 Topanga Canyon": {"price": 182960.0, "received": "2026-02-18", "comments": ""}, "15265 W Bestor Blvd": {"price": 193450.0, "received": "2025-11-21", "comments": ""}, "4565 Dundee Drive": {"price": 22630.0, "received": "2025-11-06", "comments": ""}, "1093 Palms Blvd": {"price": 33550.0, "received": "2025-11-26", "comments": ""}, "2429 Eastern Canal": {"price": 29250.0, "received": null, "comments": ""}, "16339 Akron": {"price": 77140.0, "received": "2025-12-26", "comments": ""}, "12979 Blairwood Dr": {"price": 135000.0, "received": "2026-03-05", "comments": ""}}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0338", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "JH PLUMBING", "active": true, "contact": "John Slavens", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "jhplumbing1@yahoo.com", "bids": {}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0339", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "JIMENEZ DEMILITION", "active": true, "contact": "Rey Jimenez", "phone": "(323) 550-1153", "cell": "", "statusNote": "they will send on friday 10/24", "comments": "", "email": "contact@jimenezdemolition.com", "bids": {"723 OFW": {"price": 39800.0, "received": "2025-08-18", "comments": "soil export"}, "478 Wynola St": {"price": 9800.0, "received": "2025-09-30", "comments": ""}, "17797 Camino De Yatasto": {"price": 98700.0, "received": null, "comments": ""}, "807 6th Ave": {"price": 24300.0, "received": null, "comments": ""}, "1093 Palms Blvd": {"price": 6400.0, "received": "2025-12-02", "comments": "$3800 separate price for planting removal"}, "2429 Eastern Canal": {"price": 19900.0, "received": "2025-12-29", "comments": ""}, "12979 Blairwood Dr": {"price": 98600.0, "received": "2026-02-10", "comments": ""}}, "codes": ["024000 Demolition"]}, {"id": "m0340", "div": "DIVISION 09", "divName": "FINISHES", "code": "099001 Painting Cabinets", "company": "JODY TOOLE'S PROFESSIONAL FINISHES", "active": true, "contact": "Jody Toole", "phone": "1 818 621 6120", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["099001 Painting Cabinets"]}, {"id": "m0341", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "JOHN THE PLUMBER", "active": true, "contact": "", "phone": "310-347-5322", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0342", "div": "DIVISION 31", "divName": "EARTHWORK", "code": "312300 Excavation & Backfill", "company": "JON WATSON EXCAVATING", "active": true, "contact": "", "phone": "1 818 248 0132", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["312300 Excavation & Backfill"]}, {"id": "m0343", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Installation", "company": "Joseph & Sons Mosaic & Tile", "active": false, "contact": "Joseph cohen", "phone": "", "cell": "", "statusNote": "ONLY MOSAICS NO GENERAL TILES", "comments": "", "email": "josephandsonsmosaic@yahoo.com", "bids": {"213 OFW Waterfront": {"price": 20850.0, "received": "2025-07-11", "comments": ""}, "723 OFW": {"price": 34675.0, "received": "2025-05-10", "comments": ""}}, "codes": ["096000 Tile - Installation"]}, {"id": "m0344", "div": "DIVISION 09", "divName": "FINISHES", "code": "096100 Flooring", "company": "Jos\u00e9", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "gilvertocalderon1992@icloud.com", "bids": {}, "codes": ["096100 Flooring"]}, {"id": "m0345", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "062000 Finish Carpentry", "company": "JRM CONSTRUCTION", "active": true, "contact": "Chris Kritt", "phone": "818-714-4890", "cell": "", "statusNote": "", "comments": "", "email": "ckrittinstallations@gmail.com", "bids": {}, "codes": ["062000 Finish Carpentry", "081005- Shower enclosures"]}, {"id": "m0346", "div": "DIVISION 09", "divName": "FINISHES", "code": "092000 Gypsum Board", "company": "JUAN -DRYWALL", "active": true, "contact": "", "phone": "3236361818.0", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["092000 Gypsum Board"]}, {"id": "m0347", "div": "DIVISION 31", "divName": "EARTHWORK", "code": "312300 Excavation & Backfill", "company": "K SUE CORPORATION", "active": true, "contact": "Chris Carter", "phone": "1 435 259 2333", "cell": "1 435 260 2660", "statusNote": "", "comments": "", "email": "ksuecorp@frontier.net", "bids": {}, "codes": ["312300 Excavation & Backfill"]}, {"id": "m0348", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071010 Waterproofing", "company": "KAZEMI", "active": true, "contact": "Ron Kazemi", "phone": "1 310 312 1254", "cell": "", "statusNote": "", "comments": "They want RFPs sent to their email and ask to be notified of specific jobs (last one was Market St).", "email": "info@kazemiwaterproofing.com", "bids": {"723 OFW": {"price": 743680.0, "received": "2025-11-05", "comments": ""}, "17797 Camino De Yatasto": {"price": 708100.0, "received": "2025-11-13", "comments": ""}, "865 N Oreo Pl": {"price": 498380.0, "received": "2025-11-17", "comments": ""}, "807 6th Ave": {"price": 64700.0, "received": "2025-10-10", "comments": ""}, "1080 El Medio Place": {"price": 370525.0, "received": "2025-11-19", "comments": "Check"}, "4565 Dundee Drive": {"price": 38900.0, "received": "2025-11-13", "comments": ""}}, "codes": ["071010 Waterproofing", "077700 Waterproofing Build. Wrap", "071000 Roofing"]}, {"id": "m0349", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "073313 Green Roof", "company": "KAZEMI WATERPROOFING", "active": true, "contact": "Ron Kazemi", "phone": "1 310 312 1254", "cell": "", "statusNote": "", "comments": "", "email": "info@kazemiwaterproofing.com", "bids": {"4565 Dundee Drive": {"price": 21600.0, "received": "2025-11-25", "comments": ""}}, "codes": ["073313 Green Roof"]}, {"id": "m0350", "div": "DIVISION 09", "divName": "FINISHES", "code": "096400 Wood Flooring", "company": "KELLEY FLOORING", "active": false, "contact": "David Abramson", "phone": "310-926-3955", "cell": "", "statusNote": "", "comments": "", "email": "kelleyflooring@gmail.com", "bids": {}, "codes": ["096400 Wood Flooring"]}, {"id": "m0351", "div": "DIVISION 03", "divName": "CONCRETE", "code": "033100 Structural Concrete", "company": "KG MULLEN", "active": true, "contact": "Kevin Mullen", "phone": "1 310 237 1223", "cell": "310-237-1223", "statusNote": "HIGHLY ACTIVE", "comments": "", "email": "kevin@kgmullen.com, don@kgmullen.com", "bids": {"478 Wynola St": {"price": 24000.0, "received": "2025-09-22", "comments": ""}, "1093 Palms Blvd": {"price": 41835.0, "received": "2025-11-26", "comments": ""}, "213 OFW Waterfront": {"price": 37825.0, "received": "2025-07-14", "comments": ""}}, "codes": ["033100 Structural Concrete", "077700 Waterproofing Build. Wrap", "030630 Concrete Slab", "042200 Concrete Masonry Unit"]}, {"id": "m0352", "div": "DIVISION 03", "divName": "CONCRETE", "code": "033100 Structural Concrete", "company": "KIA - STRUCTURAL CONCRETE & SHORTCRETE SPECIALIST", "active": true, "contact": "Erik Orozco", "phone": "1 818 429-8238", "cell": "", "statusNote": "", "comments": "NO RESPONSE", "email": "contact@kiacontractors.com, estimating@kiacontractors.com", "bids": {"52-60 Market St": {"price": 98500.0, "received": "2025-03-06", "comments": ""}, "17797 Camino De Yatasto": {"price": 499000.0, "received": "2025-11-27", "comments": ""}, "807 6th Ave": {"price": 850000.0, "received": "2025-10-07", "comments": "Working on discount request"}, "15265 W Bestor Blvd": {"price": 499000.0, "received": "2025-11-27", "comments": "FOUNDATION"}, "16339 Akron": {"price": 104000.0, "received": "2026-01-09", "comments": "Slab on grade $ 49,000.00Foundation $ 55,000.00"}}, "codes": ["033100 Structural Concrete"]}, {"id": "m0353", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "323100 Fences & Gates", "company": "KING FENCE", "active": true, "contact": "Jerome Sanders", "phone": "1 310 677 5588", "cell": "", "statusNote": "", "comments": "", "email": "jwsfence@yahoo.com", "bids": {}, "codes": ["323100 Fences & Gates"]}, {"id": "m0354", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "KINSLO GLASS WALL SYSTEMS", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "kinslosales@gmail.com", "bids": {}, "codes": ["058000 Glazing"]}, {"id": "m0355", "div": "DIVISION 03", "divName": "CONCRETE", "code": "031113 Shoring", "company": "KLM ENGINEERING", "active": true, "contact": "", "phone": "Phone: (310) 379-6762", "cell": "", "statusNote": "", "comments": "WRONG NUMBER", "email": "info@klm-engineering.com", "bids": {}, "codes": ["031113 Shoring"]}, {"id": "m0356", "div": "DIVISION 03", "divName": "CONCRETE", "code": "033100 Structural Concrete", "company": "KREIK CONSTRUCTION", "active": false, "contact": "Rafic Kreik", "phone": "1 310 391 0736", "cell": "", "statusNote": "", "comments": "", "email": "rkreik@earthlink.net", "bids": {}, "codes": ["033100 Structural Concrete"]}, {"id": "m0357", "div": "DIVISION 05", "divName": "METALS", "code": "051200 Structural Steel", "company": "KWIRON", "active": true, "contact": "Bashar Witwit", "phone": "8189616399.0", "cell": "8188868406.0", "statusNote": "", "comments": "", "email": "info@kwiron.com", "bids": {"Quadro Vecchio": {"price": 38500.0, "received": "2025-07-09", "comments": ""}, "6537 Topanga Canyon": {"price": 15000.0, "received": "2026-02-12", "comments": ""}, "4565 Dundee Drive": {"price": 75900.0, "received": "2025-11-28", "comments": ""}}, "codes": ["051200 Structural Steel"]}, {"id": "m0358", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Installation", "company": "KZ TILE & STONE", "active": true, "contact": "", "phone": "323 6027965", "cell": "", "statusNote": "NEW", "comments": "", "email": "kztile2020@gmail.com", "bids": {"1134 Iliff St": {"price": 13320.0, "received": "2026-04-13", "comments": ""}}, "codes": ["096000 Tile - Installation"]}, {"id": "m0359", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Installation", "company": "LA CUSTOM TILE", "active": true, "contact": "", "phone": "310 3977411", "cell": "310 5691080", "statusNote": "NEW", "comments": "", "email": "lacustomtile@aol.com", "bids": {}, "codes": ["096000 Tile - Installation"]}, {"id": "m0360", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "LA ELECTRICIANS", "active": true, "contact": "", "phone": "(424) 238-3889", "cell": "", "statusNote": "", "comments": "NEW", "email": "marketing@electricians-la.com", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0361", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "LA GALAXY PLUMBING", "active": true, "contact": "Uzi Shefer", "phone": "310-704-2907", "cell": "", "statusNote": "", "comments": "", "email": "uzishefer@gmail.com", "bids": {"1134 Iliff St": {"price": 34650.0, "received": "2026-04-14", "comments": ""}}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0362", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "015423 Scaffolding", "company": "La Loma Scaffolding", "active": true, "contact": "Dacia", "phone": "424 313 4187", "cell": "", "statusNote": "", "comments": "", "email": "admin@llscaffolding.com", "bids": {}, "codes": ["015423 Scaffolding"]}, {"id": "m0363", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081005- Shower enclosures", "company": "LA OVERHEAD GARAGE DOOR", "active": true, "contact": "", "phone": "1 310 441 2088", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["081005- Shower enclosures"]}, {"id": "m0364", "div": "DIVISION 05", "divName": "METALS", "code": "055200 Metal Railing", "company": "LA RAILINGS", "active": true, "contact": "Clayton Arghiropol", "phone": "323-393-0391", "cell": "", "statusNote": "", "comments": "", "email": "clay@larailings.com", "bids": {"429 Sherman Canal": {"price": 28954.13, "received": "2025-07-09", "comments": ""}, "478 Wynola St": {"price": 18173.0, "received": "2025-08-22", "comments": "Considering glass railings: https://www.skynova.com/uxw6-83ol-m3ej.est Considering cable railings: https://www.skynova.com/ozar-ahyu-b55w.est"}, "17797 Camino De Yatasto": {"price": 72654.9, "received": "2025-09-17", "comments": "https://www.skynova.com/vrn5-19ik-kbb2.est"}, "865 N Oreo Pl": {"price": 98544.26, "received": "2025-09-30", "comments": "\"standard\" installation with regular tempered glass  $86590.52 -     Sentryglas technology   $98,544.26"}, "807 6th Ave": {"price": 69990.9, "received": "2025-10-09", "comments": ""}, "15265 W Bestor Blvd": {"price": 14313.52, "received": "2025-10-28", "comments": ""}}, "codes": ["055200 Metal Railing"]}, {"id": "m0365", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "481400 Solar Energy Electrical Power Generation Equipment", "company": "LA SOLAR SYSTEMS, INC.", "active": false, "contact": "Shawn Alvandi", "phone": "1 866 744 3374", "cell": "1 818 667 6633", "statusNote": "WRONG NUMBER", "comments": "Greg M", "email": "shawn@lasolarsystemsinc.com", "bids": {"Quadro Vecchio": {"price": 18733.0, "received": "13/10/2025", "comments": ""}}, "codes": ["481400 Solar Energy Electrical Power Generation Equipment"]}, {"id": "m0366", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "LA STUCCO INC", "active": true, "contact": "", "phone": "(424) 270-0412", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["092400 Stucco"]}, {"id": "m0367", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "LA TOP ROOFING", "active": true, "contact": "", "phone": "1-877-353-6688", "cell": "", "statusNote": "", "comments": "", "email": "toproofing1@gmail.com", "bids": {}, "codes": ["071000 Roofing"]}, {"id": "m0368", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "LANA", "active": true, "contact": "Claudio Lana/ Jose", "phone": "1 858 552 8746", "cell": "1 858 243 3866", "statusNote": "", "comments": "", "email": "lanaconstruction@sbcglobal.net", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0369", "div": "DIVISION 08", "divName": "OPENINGS", "code": "087000 Finish Hardware", "company": "LANA/ BELLISIMA", "active": true, "contact": "Claudio Lana/ Jose", "phone": "1 858 552 8746", "cell": "1 858 243 3866", "statusNote": "", "comments": "", "email": "lanaconstruction@sbcglobal.net", "bids": {}, "codes": ["087000 Finish Hardware"]}, {"id": "m0370", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "LANE PLUMBING, INC.", "active": true, "contact": "Donald Lane", "phone": "1 323 478 0108", "cell": "1 818 640 6461", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0371", "div": "DIVISION 09", "divName": "FINISHES", "code": "099000 Painting", "company": "LAST TOUCH UP", "active": true, "contact": "Angelo Gamboa", "phone": "1 818 909 7791", "cell": "1 818 469 8003", "statusNote": "", "comments": "", "email": "thelasttouchup@aol.com", "bids": {}, "codes": ["099000 Painting"]}, {"id": "m0372", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "LAZCANO'S MASONRY & CONCRETE", "active": true, "contact": "Juan Lazcano", "phone": "1 805 981 9328", "cell": "1 805 896 2156", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["030630 Concrete Slab"]}, {"id": "m0373", "div": "DIVISION 13", "divName": "SPECIAL CONSTRUCTION", "code": "131100 Swimming Pool/Spa/Fountain", "company": "LC POOLS", "active": true, "contact": "Jhon", "phone": "1 818 991 2700", "cell": "1 818 519 0402", "statusNote": "", "comments": "DONT PICK UP", "email": "tipre4@aol.com", "bids": {"865 N Oreo Pl": {"price": 329700.0, "received": "2025-10-28", "comments": ""}, "1080 El Medio Place": {"price": 75374.0, "received": "2025-11-26", "comments": ""}}, "codes": ["131100 Swimming Pool/Spa/Fountain"]}, {"id": "m0374", "div": "DIVISION 09", "divName": "FINISHES", "code": "099000 Painting", "company": "LCI PAINT", "active": true, "contact": "Ray Sponsler", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "ray@lcipaint.com", "bids": {}, "codes": ["099000 Painting"]}, {"id": "m0375", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "LDI MECHANICAL", "active": false, "contact": "Steve Hall", "phone": "1 909 721 2844", "cell": "", "statusNote": "CALL", "comments": "NOT RESIDENTIAL PROJECTS", "email": "steve.hall@ldimechanical.com", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0376", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "262000 Low Voltage", "company": "LEGATO", "active": true, "contact": "Mark Niven", "phone": "1 310 399 6632", "cell": "1 310 429 8053", "statusNote": "", "comments": "", "email": "mark@legatohometheater.com", "bids": {}, "codes": ["262000 Low Voltage"]}, {"id": "m0377", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "250000 Home Automation", "company": "LEGATO ENTERPRISES", "active": true, "contact": "Mark Niven", "phone": "1 310 399 6632", "cell": "1 310 429 8053", "statusNote": "", "comments": "", "email": "mark@legatohometheater.com", "bids": {}, "codes": ["250000 Home Automation", "270500 Audio Visual Systems"]}, {"id": "m0378", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "LEON & SON\u2019S PLUMBING, INC.", "active": true, "contact": "David", "phone": "661 298-4417", "cell": "", "statusNote": "", "comments": "", "email": "leonandsonsplumbing@yahoo.com", "bids": {"52-60 Market St": {"price": 337000.0, "received": null, "comments": ""}, "Quadro Vecchio": {"price": 133975.0, "received": "2025-07-28", "comments": "Bid to be provided by 07/15/25"}}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0379", "div": "DIVISION 03", "divName": "CONCRETE", "code": "031113 Shoring", "company": "LEON KROUS DRILLING", "active": false, "contact": "Leon Krous", "phone": "1 818 833 4654", "cell": "1 818 968 3778", "statusNote": "Email needs to be updated", "comments": "", "email": "leonkrousdrilling@verizon.net", "bids": {}, "codes": ["031113 Shoring"]}, {"id": "m0380", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "LEONARD ROOFING, INC.", "active": false, "contact": "Marshall Howen", "phone": "1 951 506 3811", "cell": "1 805 895 2466", "statusNote": "", "comments": "", "email": "marshall@leonardroofing.com", "bids": {}, "codes": ["071000 Roofing"]}, {"id": "m0381", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "Liberty Glass Fabrication,Inc.", "active": false, "contact": "Vick Jayakumar", "phone": "951-808-9140; 378", "cell": "951-690-1559", "statusNote": "", "comments": "", "email": "vick@libertyglassfabricators.com", "bids": {}, "codes": ["058000 Glazing"]}, {"id": "m0382", "div": "DIVISION 21", "divName": "FIRE SUPPRESSION", "code": "211300 Fire Spinklers", "company": "LIFETIME FIRE PROTECTION", "active": true, "contact": "Jerzon Garcia; MelissaQuijada", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "admin@lifetimefire.com, estimating@lifetimefire.com", "bids": {"865 N Oreo Pl": {"price": 19350.0, "received": "2025-10-28", "comments": ""}, "1080 El Medio Place": {"price": 13400.0, "received": "2025-11-11", "comments": "Check;"}, "16339 Akron": {"price": 12800.0, "received": "2025-12-23", "comments": ""}, "1134 Iliff St": {"price": 8400.0, "received": "2026-04-07", "comments": ""}}, "codes": ["211300 Fire Spinklers"]}, {"id": "m0383", "div": "DIVISION 11", "divName": "EQUIPMENT", "code": "113000 Residential Equipment", "company": "LITEN", "active": true, "contact": "Light Fixtures", "phone": "310.826.7777", "cell": "310.882.6412", "statusNote": "", "comments": "", "email": "info@liteninc.com", "bids": {}, "codes": ["113000 Residential Equipment"]}, {"id": "m0384", "div": "DIVISION 09", "divName": "FINISHES", "code": "099000 Painting", "company": "LIVING COLORS", "active": true, "contact": "Ray Sponsler", "phone": "1 818 893 5068", "cell": "1 818 652 3367", "statusNote": "", "comments": "", "email": "rsponsler@livingcolorsinc.com", "bids": {}, "codes": ["099000 Painting", "099001 Painting Cabinets"]}, {"id": "m0385", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "LK PLUMBING", "active": true, "contact": "Eddie Klein", "phone": "3236535085.0", "cell": "", "statusNote": "", "comments": "", "email": "eddie@lkplumbing.com", "bids": {}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0386", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "LOMELLI ROOFING", "active": true, "contact": "", "phone": "1-310-795-7616", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["071000 Roofing"]}, {"id": "m0387", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "LORDS OF PLUMBING", "active": true, "contact": "", "phone": "(310) 845-6027", "cell": "", "statusNote": "NEW", "comments": "", "email": "admin@lordsofplumbing.com", "bids": {}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0388", "div": "DIVISION 10", "divName": "SPECIALTIES", "code": "103000 Fireplace", "company": "LUCKY CHIMNEY SWEEP, INC.", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["103000 Fireplace"]}, {"id": "m0389", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081000 Exterior Doors & Windows Supply", "company": "LUCKY GLASS", "active": true, "contact": "Jeff Ettley", "phone": "(310) 263-4100", "cell": "", "statusNote": "ONLY GLASS", "comments": "", "email": "jeff@luckysglass.com", "bids": {}, "codes": ["081000 Exterior Doors & Windows Supply"]}, {"id": "m0390", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "Luis", "active": true, "contact": "Luis", "phone": "3232202669.0", "cell": "", "statusNote": "", "comments": "", "email": "katakacalvo@gmail.com", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0391", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "LUSSO", "active": true, "contact": "Jake Pohl", "phone": "1 858 531 4930", "cell": "", "statusNote": "", "comments": "NO RESPONSE", "email": "jakepohl@gmail.com", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0392", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "262000 Low Voltage", "company": "M&C LOW VOLTAGE", "active": true, "contact": "Marcio Herrera", "phone": "1 877 642 7321", "cell": "1 818 266 6704", "statusNote": "", "comments": "", "email": "marcio@mandclv.com", "bids": {}, "codes": ["262000 Low Voltage"]}, {"id": "m0393", "div": "DIVISION 04", "divName": "MASONRY", "code": "042100 Masonry Brick Veneer", "company": "M&R MASONRY", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["042100 Masonry Brick Veneer", "103000 Fireplace"]}, {"id": "m0394", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "076413 Standing Seam Sheet Metal Wall Cladding", "company": "MACIAS SHEET METAL", "active": true, "contact": "Leticia Macias", "phone": "213 577-5233", "cell": "", "statusNote": "", "comments": "", "email": "leticia@maciassheetmetal.com", "bids": {}, "codes": ["076413 Standing Seam Sheet Metal Wall Cladding"]}, {"id": "m0395", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "MADISON ELECTRIC", "active": true, "contact": "Nathan Clarke", "phone": "310-514-6114", "cell": "", "statusNote": "", "comments": "", "email": "madisonelectric@gmail.com", "bids": {"429 Sherman Canal": {"price": 14210.0, "received": "2025-07-13", "comments": ""}}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0396", "div": "DIVISION 10", "divName": "SPECIALTIES", "code": "103000 Fireplace", "company": "MAGID MASONRY", "active": true, "contact": "Ilya Magid", "phone": "1 805 899 2720", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["103000 Fireplace"]}, {"id": "m0397", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "MAGNUM LAND CLEARING, INC.", "active": true, "contact": "RENTAL ONLY", "phone": "(818) 887-9222", "cell": "", "statusNote": "", "comments": "Wants to BID in the future", "email": "michael.turner@landclearing.net", "bids": {}, "codes": ["024000 Demolition"]}, {"id": "m0398", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "MAJESTIC ELECTRIC", "active": true, "contact": "Sheldon Sugarman", "phone": "818-519-2600", "cell": "", "statusNote": "", "comments": "", "email": "majesticelectric@socal.rr.com", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0399", "div": "DIVISION 21", "divName": "FIRE SUPPRESSION", "code": "211300 Fire Spinklers", "company": "MAJESTIC FIRE PROTECTION (KORD)", "active": true, "contact": "Burton Pederson", "phone": "1 800 918 8978", "cell": "1 213 422 6716", "statusNote": "", "comments": "X", "email": "burton@majesticfire.com", "bids": {"723 OFW": {"price": 122550.0, "received": "2025-04-07", "comments": ""}, "748 & 750 Palisades Dr": {"price": 31920.0, "received": null, "comments": "WORKING ON BID"}, "865 N Oreo Pl": {"price": 21950.0, "received": "2025-10-27", "comments": ""}, "807 6th Ave": {"price": 48775.0, "received": "2025-09-30", "comments": ""}, "1080 El Medio Place": {"price": 22575.0, "received": "2025-11-15", "comments": "Check;"}, "15265 W Bestor Blvd": {"price": 23550.0, "received": "2025-11-06", "comments": ""}, "2429 Eastern Canal": {"price": 9775.0, "received": "2025-12-01", "comments": ""}, "16339 Akron": {"price": 14900.0, "received": "2025-12-25", "comments": "INSTALL COST AUTOMATIC SYSTEM $9,775"}, "1134 Iliff St": {"price": 4900.0, "received": "2026-04-09", "comments": ""}}, "codes": ["211300 Fire Spinklers"]}, {"id": "m0400", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "MALIBU GLASS & MIRROR INC.", "active": true, "contact": "Adeline Freedman", "phone": "1 310 456 1844", "cell": "310-456 2594", "statusNote": "", "comments": "", "email": "adelinef@malibuglass.com", "bids": {"429 Sherman Canal": {"price": 11295.0, "received": "2025-06-27", "comments": ""}, "723 OFW": {"price": 119987.65, "received": "2025-09-17", "comments": ""}, "17797 Camino De Yatasto": {"price": 233633.5, "received": null, "comments": "Glass railing prices"}, "6537 Topanga Canyon": {"price": 105587.17, "received": "2026-02-13", "comments": ""}}, "codes": ["058000 Glazing", "081001 Exterior Doors & Windows Installation"]}, {"id": "m0401", "div": "DIVISION 13", "divName": "SPECIAL CONSTRUCTION", "code": "131100 Swimming Pool/Spa/Fountain", "company": "MALIBU POOL & SPA", "active": true, "contact": "Gary Humecke ;Darin Marten", "phone": "1 818 228 0535", "cell": "", "statusNote": "", "comments": "DONT PICK UP", "email": "garyshouse@sbcglobal.net", "bids": {"1080 El Medio Place": {"price": 31600.0, "received": "2025-11-11", "comments": ""}}, "codes": ["131100 Swimming Pool/Spa/Fountain"]}, {"id": "m0402", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "MANNY'S HEATING & AIR CONDITION", "active": true, "contact": "", "phone": "(323) 774-4032 ; (626) 388-4821", "cell": "", "statusNote": "NEW", "comments": "", "email": "mannyhvac@yahoo.com", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0403", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Material", "company": "MARBLE UNLIMITED", "active": true, "contact": "", "phone": "818-988-0100", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["096000 Tile - Material"]}, {"id": "m0404", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "Marino Sanchez", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "sanchezmarino135@gmail.com", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation", "081003 Interior Doors & Frames Installation", "081004 Garage Doors", "074624 Wood Siding - Install"]}, {"id": "m0405", "div": "DIVISION 09", "divName": "FINISHES", "code": "095100 Accoustical Ceiling", "company": "MARK FLANDERS COUSTIC-GLO", "active": true, "contact": "Mark Flanders", "phone": "1 897 6760", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["095100 Accoustical Ceiling"]}, {"id": "m0406", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "MARSHALL DESIGN CONSTRUCTION", "active": true, "contact": "", "phone": "310-980-8312", "cell": "", "statusNote": "", "comments": "", "email": "designconsulting@mac.com", "bids": {"4565 Dundee Drive": {"price": 176000.0, "received": "2025-12-04", "comments": ""}}, "codes": ["064100 Cabinets"]}, {"id": "m0407", "div": "DIVISION 05", "divName": "METALS", "code": "054000 Cold Form Metal Framing", "company": "MARTIN BROTHERS MARCOWALL", "active": true, "contact": "", "phone": "1 310 532 5335", "cell": "1 310 897 6760", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["054000 Cold Form Metal Framing", "092000 Gypsum Board"]}, {"id": "m0408", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "MASCO CONSTRACTOR SERVICES", "active": true, "contact": "Sean Peace", "phone": "1 661 295 9855", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["058000 Glazing"]}, {"id": "m0409", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081005- Shower enclosures", "company": "MASCO CONTRACTOR SERVICES", "active": true, "contact": "Josh Negrin", "phone": "1 805 965 4962", "cell": "1 858 518 4012", "statusNote": "", "comments": "", "email": "josh.negrin@truteam.com", "bids": {}, "codes": ["081005- Shower enclosures"]}, {"id": "m0410", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "077123 Gutters/Downspouts/Water Retention", "company": "MASCO CONTRACTOR SERVICES OF CA.", "active": true, "contact": "Mike Stone", "phone": "661 295-9855", "cell": "661 383-3452", "statusNote": "", "comments": "", "email": "mike.stone@truteam.com", "bids": {"748 & 750 Palisades Dr": {"price": 2750.0, "received": "2025-08-16", "comments": ""}, "Quadro Vecchio": {"price": 15975.0, "received": "2025-07-15", "comments": ""}, "478 Wynola St": {"price": 2600.0, "received": "2025-09-09", "comments": "Also sent proposal for gutters"}}, "codes": ["077123 Gutters/Downspouts/Water Retention", "072100 Insulation"]}, {"id": "m0411", "div": "DIVISION 10", "divName": "SPECIALTIES", "code": "103000 Fireplace", "company": "MASCO CONTRACTORS SERVICES", "active": true, "contact": "Sean Peace", "phone": "1 661 295 9855", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["103000 Fireplace"]}, {"id": "m0412", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "MASTER DEMOLITION INC.", "active": true, "contact": "Jeremy", "phone": "1-888-666-8808", "cell": "2135960330.0", "statusNote": "DOESNT PICK UP", "comments": "", "email": "estimates.masterdemolitioninc@gmail.com", "bids": {}, "codes": ["024000 Demolition"]}, {"id": "m0413", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "MAX'S CUSTOM CABINETS", "active": true, "contact": "", "phone": "310 827 2878", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["064100 Cabinets"]}, {"id": "m0414", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Installation", "company": "MC TILE & STONE", "active": true, "contact": "", "phone": "(310) 397-4210", "cell": "", "statusNote": "NEW", "comments": "", "email": "mctilemarble@live.com", "bids": {}, "codes": ["096000 Tile - Installation"]}, {"id": "m0415", "div": "DIVISION 05", "divName": "METALS", "code": "055000 Metal Fabricators", "company": "MCCOY CONSTRUCTION", "active": true, "contact": "Kyle Weekes", "phone": "435 554-9347", "cell": "", "statusNote": "", "comments": "", "email": "kyle@mcllusa.com", "bids": {}, "codes": ["055000 Metal Fabricators"]}, {"id": "m0416", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Material", "company": "MCGOWAN'S", "active": true, "contact": "Ernie McGowan/ Wanda", "phone": "1 805 527 9021", "cell": "1 818 694 2609", "statusNote": "", "comments": "", "email": "mcgowansmarble@sbcglobal.net", "bids": {}, "codes": ["096000 Tile - Material"]}, {"id": "m0417", "div": "DIVISION 14", "divName": "CONVEYING EQUIPMENT", "code": "142000 Elevators", "company": "MCKINLEY ELEVATOR CORPORATION", "active": true, "contact": "", "phone": "(949) 381-1309 (California)", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["142000 Elevators"]}, {"id": "m0418", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "MCLOUD DEMOLITION INC.", "active": false, "contact": "John Rigdon", "phone": "1 818 291 9940", "cell": "1 818 968 9728", "statusNote": "RETIRED", "comments": "NO RESPONSE", "email": "mclouds@pacbell.net", "bids": {}, "codes": ["024000 Demolition"]}, {"id": "m0419", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "MEGA ELECTRIC", "active": true, "contact": "Ben Gil", "phone": "(818)426-5208", "cell": "", "statusNote": "", "comments": "", "email": "megaelectric1@aol.com", "bids": {"52-60 Market St": {"price": 474000.0, "received": "2025-05-23", "comments": ""}, "Quadro Vecchio": {"price": 197000.0, "received": "2025-07-15", "comments": "WILL PROVIDE BY 07/14/25"}, "429 Sherman Canal": {"price": 67000.0, "received": "2025-08-11", "comments": ""}, "213 OFW Waterfront": {"price": 114000.0, "received": "2025-07-31", "comments": ""}, "748 & 750 Palisades Dr": {"price": 244000.0, "received": "2025-08-13", "comments": ""}, "478 Wynola St": {"price": 41275.0, "received": "2025-09-13", "comments": ""}, "17797 Camino De Yatasto": {"price": 268000.0, "received": null, "comments": "NO LIGHTING PACKAGE INCLUDED"}, "807 6th Ave": {"price": 297000.0, "received": "2025-10-28", "comments": "Working on discount request"}, "15265 W Bestor Blvd": {"price": 285000.0, "received": "2025-11-17", "comments": ""}, "4565 Dundee Drive": {"price": 79000.0, "received": "2025-11-10", "comments": ""}, "1093 Palms Blvd": {"price": 49700.0, "received": "2025-11-30", "comments": ""}}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0420", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "MEGA PLASTERING SYSTEMS INC", "active": true, "contact": "", "phone": "(562) 863-9100", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["092400 Stucco"]}, {"id": "m0421", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Material", "company": "MEGA TILE", "active": true, "contact": "Harry San Luis", "phone": "1 818 593 9141", "cell": "", "statusNote": "", "comments": "", "email": "mega.estimate@gmail.com", "bids": {}, "codes": ["096000 Tile - Material"]}, {"id": "m0422", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "015423 Scaffolding", "company": "MEMO SCAFFOLDING INC.", "active": true, "contact": "Yoland Rodriguez", "phone": "1 562 404 8600", "cell": "", "statusNote": "", "comments": "", "email": "contact@memoscaffolding.com", "bids": {}, "codes": ["015423 Scaffolding"]}, {"id": "m0423", "div": "DIVISION 05", "divName": "METALS", "code": "055200 Metal Railing", "company": "MG CONSTRUCTION & DECKS", "active": true, "contact": "Jenny", "phone": "323 849-3944", "cell": "", "statusNote": "", "comments": "", "email": "office@mgcdecks.com", "bids": {"748 & 750 Palisades Dr": {"price": 42081.0, "received": "2025-08-21", "comments": ""}, "12979 Blairwood Dr": {"price": 29165.0, "received": "2026-02-18", "comments": "$250 linear ft"}, "213 OFW Waterfront": {"price": 35658.0, "received": "2025-06-19", "comments": "$42 / SF"}}, "codes": ["055200 Metal Railing", "093200 Elevated Roof Top Decks"]}, {"id": "m0424", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Material", "company": "MICHELI MARBLE & TILE, INC.", "active": true, "contact": "Nathan Micheli", "phone": "1 310 301 1990", "cell": "", "statusNote": "", "comments": "EMAIL NEED TO BE UPDATED", "email": "nathan@michelimarble.com", "bids": {}, "codes": ["096000 Tile - Material"]}, {"id": "m0425", "div": "DIVISION 21", "divName": "FIRE SUPPRESSION", "code": "211300 Fire Spinklers", "company": "MILLENIUM", "active": true, "contact": "Drew Smith", "phone": "1 805 389 3056", "cell": "", "statusNote": "", "comments": "", "email": "drew@firesprinklersdoneright.com", "bids": {}, "codes": ["211300 Fire Spinklers"]}, {"id": "m0426", "div": "DIVISION 09", "divName": "FINISHES", "code": "099000 Painting", "company": "MILMARK PAINTING, INC.", "active": true, "contact": "Keith Burleigh", "phone": "(858) 432-4316", "cell": "", "statusNote": "", "comments": "", "email": "dwilliams@dcccc.net", "bids": {}, "codes": ["099000 Painting"]}, {"id": "m0427", "div": "DIVISION 03", "divName": "CONCRETE", "code": "033100 Structural Concrete", "company": "MINTZ CONCRETE INC.", "active": true, "contact": "Brian Mintz", "phone": "818-932-1978", "cell": "818-968-1217", "statusNote": "HIGHLY ACTIVE", "comments": "NO BID, NO TIME", "email": "brian@mintzconcrete.com", "bids": {"52-60 Market St": {"price": 52669.0, "received": "2025-05-21", "comments": ""}, "Quadro Vecchio": {"price": 122354.0, "received": "2025-10-02", "comments": ""}, "807 6th Ave": {"price": 611180.0, "received": "2025-10-16", "comments": ""}, "15265 W Bestor Blvd": {"price": 440241.0, "received": "2025-11-06", "comments": "FOUNDATION"}, "4565 Dundee Drive": {"price": 52338.0, "received": "2025-11-06", "comments": ""}, "1093 Palms Blvd": {"price": 48622.0, "received": null, "comments": ""}, "16339 Akron": {"price": 93276.0, "received": "2026-01-05", "comments": ""}, "12979 Blairwood Dr": {"price": 590144.0, "received": "2026-02-10", "comments": ""}, "7300 Vista Del Mar": {"price": 546625.0, "received": "2026-04-02", "comments": ""}, "1134 Iliff St": {"price": 56538.0, "received": "2026-04-07", "comments": "Slab & Footings"}, "429 Sherman Canal": {"price": 53363.0, "received": "24/06/2025", "comments": ""}, "723 OFW": {"price": 1272236.0, "received": "28/04/2025", "comments": ""}, "478 Wynola St": {"price": 27784.0, "received": "2025-08-25", "comments": ""}, "1080 El Medio Place": {"price": 204952.0, "received": "2025-10-17", "comments": "Check;"}, "2429 Eastern Canal": {"price": 59575.0, "received": "2025-11-25", "comments": ""}}, "codes": ["033100 Structural Concrete"]}, {"id": "m0428", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Material", "company": "MISSION TILE WEST", "active": true, "contact": "Chris Campos", "phone": "1 310 434 9697", "cell": "", "statusNote": "", "comments": "", "email": "chris@missiontilewest.com", "bids": {}, "codes": ["096000 Tile - Material"]}, {"id": "m0429", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "MITCHELL INVIROMENTAL CONCRETE", "active": true, "contact": "", "phone": "818-767-2988", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["030630 Concrete Slab"]}, {"id": "m0430", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "262000 Low Voltage", "company": "MJM COMMUNICATIONS & FIRE, INC.-LOW VOLTAGE/FIRE ALARM", "active": true, "contact": "", "phone": "818.224.4880", "cell": "", "statusNote": "", "comments": "", "email": "mark@mjmprotection.com", "bids": {}, "codes": ["262000 Low Voltage"]}, {"id": "m0431", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Material", "company": "MODUL MARBLE & GRANITE", "active": true, "contact": "Vahe \"Vinny\" Akpulat", "phone": "1 818 767 4528", "cell": "", "statusNote": "", "comments": "EMAIL NEED TO BE UPDATED", "email": "vinny@modulmarble.com", "bids": {}, "codes": ["096000 Tile - Material"]}, {"id": "m0432", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "MONKEY MAN TREE SERVICE", "active": true, "contact": "John Lamberston", "phone": "1 310 396 8768", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0433", "div": "DIVISION 09", "divName": "FINISHES", "code": "097200 Wall Coverings", "company": "MONTE ALLEN", "active": true, "contact": "Esa Yla-Soininmaki", "phone": "1 310 380 4640", "cell": "", "statusNote": "", "comments": "", "email": "esa@monteallen.com", "bids": {}, "codes": ["097200 Wall Coverings"]}, {"id": "m0434", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "MONTELONGO", "active": true, "contact": "Michael Montelongo", "phone": "3107489616.0", "cell": "3105409122.0", "statusNote": "", "comments": "", "email": "montelongoinc@verizon.net", "bids": {"1093 Palms Blvd": {"price": 40250.0, "received": "2025-11-24", "comments": ""}, "12979 Blairwood Dr": {"price": 186887.0, "received": "2026-03-05", "comments": ""}}, "codes": ["092400 Stucco"]}, {"id": "m0435", "div": "DIVISION 03", "divName": "CONCRETE", "code": "031113 Shoring", "company": "MOORE FOUNDATIONS", "active": true, "contact": "Ryan Moore", "phone": "818-698-4783", "cell": "818-698-4737", "statusNote": "", "comments": "NO PICK UP THE PHONE", "email": "ryan@moorefoundationsinc.com", "bids": {}, "codes": ["031113 Shoring"]}, {"id": "m0436", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "MOORE'S PLUMBING", "active": true, "contact": "Mitch Moore", "phone": "6266277573.0", "cell": "", "statusNote": "", "comments": "", "email": "mitch@mooresplumbinginc.com", "bids": {"17797 Camino De Yatasto": {"price": 212450.0, "received": "2025-12-22", "comments": ""}, "807 6th Ave": {"price": 209400.0, "received": "2026-01-13", "comments": "includes deck drains and roof drains"}, "1080 El Medio Place": {"price": 147850.0, "received": "2025-12-22", "comments": ""}}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0437", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "MR CH ELECTRIC", "active": true, "contact": "Wilmer Cruz", "phone": "323-928-8880", "cell": "", "statusNote": "", "comments": "NEW SUB", "email": "wilmer@mrchetoelectric.com", "bids": {"6537 Topanga Canyon": {"price": 99800.0, "received": "2026-02-13", "comments": ""}, "865 N Oreo Pl": {"price": 138500.0, "received": "2025-10-31", "comments": ""}, "1093 Palms Blvd": {"price": 37000.0, "received": "2025-11-21", "comments": ""}, "2429 Eastern Canal": {"price": 37000.0, "received": "2025-11-21", "comments": ""}, "16339 Akron": {"price": 38500.0, "received": "2025-12-26", "comments": ""}}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0438", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "061000 Rough Carpentry", "company": "MRB CONSTRUCTION INC", "active": true, "contact": "Crisol Perez", "phone": "(747) 529-4890", "cell": "", "statusNote": "", "comments": "EMAIL UPDATED", "email": "marvin@mrbconstruction.net", "bids": {"429 Sherman Canal": {"price": 162590.0, "received": "2025-07-09", "comments": ""}, "723 OFW": {"price": 1701956.0, "received": "2025-08-21", "comments": ""}, "748 & 750 Palisades Dr": {"price": 552384.0, "received": "2025-08-08", "comments": ""}, "478 Wynola St": {"price": 71538.0, "received": "2025-08-22", "comments": ""}, "17797 Camino De Yatasto": {"price": 1030133.0, "received": "2025-11-06", "comments": ""}, "807 6th Ave": {"price": 645515.0, "received": "2025-10-10", "comments": "Discount request declined"}, "1080 El Medio Place": {"price": 386866.0, "received": "2025-10-21", "comments": "Check;"}, "15265 W Bestor Blvd": {"price": 581793.0, "received": "2025-12-19", "comments": ""}, "4565 Dundee Drive": {"price": 226140.0, "received": "2025-11-06", "comments": ""}, "1093 Palms Blvd": {"price": 85335.0, "received": null, "comments": ""}, "2429 Eastern Canal": {"price": 170128.0, "received": "2025-11-24", "comments": ""}, "16339 Akron": {"price": 158802.0, "received": "2025-12-26", "comments": ""}, "12979 Blairwood Dr": {"price": 626975.0, "received": "2026-02-06", "comments": ""}, "7300 Vista Del Mar": {"price": 418130.0, "received": "2026-04-06", "comments": ""}, "1134 Iliff St": {"price": 97274.0, "received": "04/07 /202", "comments": ""}}, "codes": ["061000 Rough Carpentry"]}, {"id": "m0439", "div": "DIVISION 05", "divName": "METALS", "code": "055000 Metal Fabricators", "company": "MRP", "active": false, "contact": "Dave Aylesworth", "phone": "1 310 826 6222", "cell": "1 310 678 7660", "statusNote": "", "comments": "New email address", "email": "aylesworthd@marmol-radziner.com, todd@marmol-radziner.com", "bids": {}, "codes": ["055000 Metal Fabricators", "076000 Flashing & Sheet Metal", "081001 Exterior Doors & Windows Installation", "064100 Cabinets"]}, {"id": "m0440", "div": "DIVISION 09", "divName": "FINISHES", "code": "099001 Painting Cabinets", "company": "MRP CABINET SHOP", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["099001 Painting Cabinets"]}, {"id": "m0441", "div": "DIVISION 09", "divName": "FINISHES", "code": "074619 Steel Siding", "company": "MRP METAL SHOP", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["074619 Steel Siding"]}, {"id": "m0442", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "014533 Utilities", "company": "MULTIFAMILY UTILITY COMPANY, INC.", "active": true, "contact": "Water Meters", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["014533 Utilities"]}, {"id": "m0443", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Material", "company": "MVA MARBLE & GRANITE", "active": true, "contact": "", "phone": "1 818 504 9199", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["096000 Tile - Material"]}, {"id": "m0444", "div": "DIVISION 03", "divName": "CONCRETE", "code": "033100 Structural Concrete", "company": "MVM", "active": true, "contact": "Francisco Sorto", "phone": "8183701254.0", "cell": "", "statusNote": "", "comments": "NO RESPONSE", "email": "mvmconcreteinc@gmail.com", "bids": {}, "codes": ["033100 Structural Concrete"]}, {"id": "m0445", "div": "DIVISION 01", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "015000 Temp  Facilities", "company": "NATIONAL CONSTRUCTION RENTALS", "active": true, "contact": "Leticia Lopez", "phone": "1 323 838 1800", "cell": "", "statusNote": "", "comments": "", "email": "llopez@rentnational.com", "bids": {}, "codes": ["015000 Temp  Facilities", "015220 Temporary Toilet", "015620 Temporary Fencing"]}, {"id": "m0446", "div": "DIVISION 14", "divName": "CONVEYING EQUIPMENT", "code": "142000 Elevators", "company": "Nationwide Lifts", "active": true, "contact": "Barry Singer", "phone": "818-359-7863", "cell": "", "statusNote": "", "comments": "", "email": "barry@nwlifts.com", "bids": {"865 N Oreo Pl": {"price": 53950.0, "received": "2025-10-30", "comments": ""}, "807 6th Ave": {"price": 58900.0, "received": "2025-10-03", "comments": ""}, "15265 W Bestor Blvd": {"price": 63500.0, "received": null, "comments": ""}}, "codes": ["142000 Elevators"]}, {"id": "m0447", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081004 Garage Doors", "company": "NEIGHBORLY GARAGE DOOR PROS", "active": true, "contact": "", "phone": "(818) 450-5312", "cell": "", "statusNote": "NEW", "comments": "", "email": "info@neighborlypro.com", "bids": {}, "codes": ["081004 Garage Doors"]}, {"id": "m0448", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Material", "company": "NEW HORIZONS STONE & TILE", "active": true, "contact": "Claude Brunkow Sr", "phone": "310 985-4762", "cell": "", "statusNote": "NEW", "comments": "", "email": "cbrunkow@nhstoneandtile.com", "bids": {"12979 Blairwood Dr": {"price": 102540.75, "received": "2026-02-19", "comments": ""}}, "codes": ["096000 Tile - Material", "096000 Tile - Installation"]}, {"id": "m0449", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "NEW IMAGE ROOFING, INC.", "active": true, "contact": "Julio Benitez", "phone": "1 818 833 6833", "cell": "1 818 326 9756", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["071000 Roofing"]}, {"id": "m0450", "div": "DIVISION 05", "divName": "METALS", "code": "055000 Metal Fabricators", "company": "NEXUSMETALWERX", "active": false, "contact": "Matt", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "info@nexusmetalwerx.com", "bids": {}, "codes": ["055000 Metal Fabricators"]}, {"id": "m0451", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "Nobel Cabinets ( Vietnam)", "active": true, "contact": "", "phone": "(908) 566-5999", "cell": "", "statusNote": "", "comments": "NO RESPONSE", "email": "sales@nobelcabinetsusa.com", "bids": {}, "codes": ["064100 Cabinets"]}, {"id": "m0452", "div": "DIVISION 03", "divName": "CONCRETE", "code": "033100 Structural Concrete", "company": "NORMAN SALTER", "active": true, "contact": "", "phone": "(310) 820-0550", "cell": "(310) 820-0990", "statusNote": "", "comments": "VOICEMAIL", "email": "nsalter@focusbuildersinc.com", "bids": {}, "codes": ["033100 Structural Concrete"]}, {"id": "m0453", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "NORTHERN AIR", "active": true, "contact": "Kevin Chernenkoff", "phone": "1 818 342 9414", "cell": "315 415 4061", "statusNote": "", "comments": "ONLY COMERCIAL USES NOT RESIDENTIAL", "email": "k.chernenkoff@northernairtech.com", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0454", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "481400 Solar Energy Electrical Power Generation Equipment", "company": "NRG CLEAN POWER", "active": true, "contact": "Frankie Gutierrez", "phone": "888-650-4750", "cell": "747-293-3060", "statusNote": "", "comments": "", "email": "frankie.g@nrgcleanpower.com", "bids": {"723 OFW": {"price": 49642.0, "received": "2025-08-25", "comments": ""}, "865 N Oreo Pl": {"price": 14374.8, "received": "2025-09-28", "comments": "NO BATTERIES"}, "1080 El Medio Place": {"price": 12936.0, "received": "2025-11-25", "comments": ""}}, "codes": ["481400 Solar Energy Electrical Power Generation Equipment"]}, {"id": "m0455", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "O'BRIEN SCREEN & GLASS", "active": true, "contact": "Ron Gaxiola", "phone": "1 310 676 0454", "cell": "1 310 387 6945", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["058000 Glazing"]}, {"id": "m0456", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "O2COMPOST (COMPOST SYSTEMS & TRAINING)", "active": true, "contact": "Derrick Santos", "phone": "1 360 568 8085", "cell": "", "statusNote": "", "comments": "Email is wrong, voicemail", "email": "sherri@o2compost.com", "bids": {}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0457", "div": "DIVISION 09", "divName": "FINISHES", "code": "096400 Wood Flooring", "company": "OFF THE WALL", "active": true, "contact": "Mike Dwyer", "phone": "1 818 363 1254", "cell": "1 818 216 6490", "statusNote": "", "comments": "", "email": "mike@offthewallfloors.com", "bids": {}, "codes": ["096400 Wood Flooring", "099000 Painting"]}, {"id": "m0458", "div": "DIVISION 09", "divName": "FINISHES", "code": "092000 Gypsum Board", "company": "OGDEN DRYWALL COMPANY", "active": true, "contact": "", "phone": "1 702 353 1232", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["092000 Gypsum Board"]}, {"id": "m0459", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "072100 Insulation", "company": "OJ Fireplaces", "active": true, "contact": "Trevor Wells", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "twells@ojinc.com", "bids": {"Quadro Vecchio": {"price": 10565.0, "received": "2025-07-31", "comments": ""}, "748 & 750 Palisades Dr": {"price": 12632.0, "received": "2025-08-04", "comments": ""}, "478 Wynola St": {"price": 1771.0, "received": "2025-08-21", "comments": ""}, "865 N Oreo Pl": {"price": 11698.0, "received": "2025-11-18", "comments": ""}, "1080 El Medio Place": {"price": 16621.0, "received": "2025-10-20", "comments": "Check;"}, "4565 Dundee Drive": {"price": 6871.0, "received": "2025-11-10", "comments": ""}, "1093 Palms Blvd": {"price": 8786.0, "received": "2025-11-21", "comments": ""}, "2429 Eastern Canal": {"price": 7142.0, "received": "2025-12-03", "comments": ""}, "16339 Akron": {"price": 6898.0, "received": "2025-12-30", "comments": ""}, "1134 Iliff St": {"price": 5685.0, "received": "2026-04-10", "comments": ""}, "17797 Camino De Yatasto": {"price": 15319.0, "received": "2025-11-03", "comments": ""}, "15265 W Bestor Blvd": {"price": 8585.0, "received": "2025-10-29", "comments": ""}}, "codes": ["072100 Insulation", "103000 Fireplace"]}, {"id": "m0460", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "OLD ENGLISH PLASTERING", "active": false, "contact": "Mike Gates", "phone": "818-768-2345", "cell": "1 818 389 3722", "statusNote": "", "comments": "", "email": "mgates@oldenglishplastering.com", "bids": {}, "codes": ["092400 Stucco"]}, {"id": "m0461", "div": "DIVISION 14", "divName": "CONVEYING EQUIPMENT", "code": "142000 Elevators", "company": "OTIS ELEVATORS", "active": true, "contact": "Andrea Thomas", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "andrea.thomas@otis.com", "bids": {"723 OFW": {"price": 162862.0, "received": "2025-08-22", "comments": ""}}, "codes": ["142000 Elevators"]}, {"id": "m0462", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "P&M CUSTOM PLASTERING INC", "active": true, "contact": "", "phone": "(818) 991-4072", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["092400 Stucco"]}, {"id": "m0463", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "PACIFIC", "active": false, "contact": "Warren Brevelri", "phone": "1 818 765 5758", "cell": "1 818 426 8628", "statusNote": "", "comments": "RETIRED", "email": "warren@pacificlightinginc.com", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0464", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "PACIFIC & SANTA MONICA AIR DUCT", "active": true, "contact": "Charles Gigliotti", "phone": "1 310 451 3749", "cell": "1 323 462 8557", "statusNote": "", "comments": "", "email": "cgiglio148@aol.com", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0465", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "PACIFIC GLASS WORKS INC.", "active": true, "contact": "", "phone": "310/444-9191", "cell": "", "statusNote": "", "comments": "Received too many bid proposals, they don't have time to do all those bids", "email": "ronnie@pacificglassworksinc.com", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0466", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "PACIFIC OCEAN PARK", "active": true, "contact": "Jim Gentry", "phone": "310.801.7932", "cell": "", "statusNote": "", "comments": "", "email": "popconst1@gmail.com", "bids": {"52-60 Market St": {"price": 150400.0, "received": "2025-09-01", "comments": "Bid for 52 & 60 Market St"}, "Quadro Vecchio": {"price": 47250.0, "received": "2025-07-27", "comments": "SOFIA - RESEND TO CORRECTED EMAIL"}, "213 OFW Waterfront": {"price": 17800.0, "received": "2025-08-03", "comments": ""}, "15265 W Bestor Blvd": {"price": 135600.0, "received": "2025-11-23", "comments": ""}, "4565 Dundee Drive": {"price": 29600.0, "received": "2025-11-30", "comments": ""}, "1093 Palms Blvd": {"price": 27900.0, "received": "2025-11-24", "comments": ""}, "2429 Eastern Canal": {"price": 45200.0, "received": "2025-11-24", "comments": ""}, "16339 Akron": {"price": 26900.0, "received": "2025-12-29", "comments": ""}}, "codes": ["230000 Hvac"]}, {"id": "m0467", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Material", "company": "PACIFIC STONE DESIGN", "active": true, "contact": "Zack Kazanchyan/ Tim Weatherton", "phone": "1 323 869 9764", "cell": "", "statusNote": "", "comments": "", "email": "zack@pacificstonedesigns.com", "bids": {}, "codes": ["096000 Tile - Material"]}, {"id": "m0468", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "PAN PACIFIC METALS, INC.", "active": true, "contact": "MICHAEL SANDFORD", "phone": "", "cell": "", "statusNote": "CALL", "comments": "", "email": "pacific44@att.net", "bids": {}, "codes": ["071000 Roofing", "074619 Steel Siding"]}, {"id": "m0469", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "PELLA WINDOW AND DOOR SHOWROOM OF ENCINO", "active": true, "contact": "", "phone": "1-818-729-4824", "cell": "1-818-728-9500", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0470", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081005- Shower enclosures", "company": "PELLA WINDOWS & DOORS", "active": true, "contact": "Tami Paulson", "phone": "310-633-1987", "cell": "", "statusNote": "", "comments": "", "email": "paulsonta@pella.com", "bids": {}, "codes": ["081005- Shower enclosures"]}, {"id": "m0471", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "PERALTA", "active": true, "contact": "Enrique Peralta", "phone": "1 323 256 4495", "cell": "1 213 458 4194", "statusNote": "DOESNT PICK UP", "comments": "NO RESPONSE", "email": "fastrdenu@gmail.com", "bids": {}, "codes": ["024000 Demolition", "312300 Excavation & Backfill", "312500 Erosion Controls"]}, {"id": "m0472", "div": "DIVISION 09", "divName": "FINISHES", "code": "099001 Painting Cabinets", "company": "PETE\u2019S HOUSE PAINTING", "active": true, "contact": "Pedro Silva", "phone": "818 63 27392", "cell": "", "statusNote": "", "comments": "", "email": "pedrohsilva@sbcglobal.net", "bids": {"52-60 Market St": {"price": 93000.0, "received": "2025-05-21", "comments": ""}}, "codes": ["099001 Painting Cabinets"]}, {"id": "m0473", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "PIERRE SPRINKLER & LANDSCAPE", "active": true, "contact": "Joe Lowden", "phone": "1 626 239 3927", "cell": "1 626 831 7939", "statusNote": "", "comments": "voicemail", "email": "info@pierrelandscape.com", "bids": {}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0474", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "PIONEERS HEATING & AIR", "active": true, "contact": "", "phone": "(626) 217-0559", "cell": "", "statusNote": "NEW", "comments": "", "email": "support@pioneersheatingandair.com", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0475", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "PLANTASIA", "active": true, "contact": "Alex Colovic", "phone": "1 310 375 0387", "cell": "", "statusNote": "", "comments": "", "email": "goplantasia@aol.com", "bids": {}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0476", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "PLANTER SOLUTIONS-LANDSCAPING PLANTERS", "active": false, "contact": "Ryan Risse", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "ryan@planter\u2010solutions.com", "bids": {}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0477", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "PLASTIC DEPOT", "active": false, "contact": "Bill Larkins", "phone": "1 310 217 7080", "cell": "", "statusNote": "", "comments": "", "email": "bill@plasticdepots.com", "bids": {}, "codes": ["064100 Cabinets"]}, {"id": "m0478", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "269900 Electric Fixtures", "company": "PLAZA WHOLESALE ELECTRIC", "active": true, "contact": "Electric Materials", "phone": "5879 W. Pico Blvd.", "cell": "323.938.1800", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["269900 Electric Fixtures"]}, {"id": "m0479", "div": "DIVISION 13", "divName": "SPECIAL CONSTRUCTION", "code": "130000 - Pool & Spa Coping", "company": "PORTER SANDBLASTING CO.", "active": true, "contact": "Ismael Felix", "phone": "1 818 842 1626", "cell": "", "statusNote": "", "comments": "DONT PICK UP", "email": "portersandblast@gmail.com", "bids": {}, "codes": ["130000 - Pool & Spa Coping"]}, {"id": "m0480", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "Power by Spark", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "powerbyspark@gmail.com", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0481", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "015000 Temp  Facilities", "company": "POWER PLUS!", "active": true, "contact": "Jose Munguia", "phone": "1 818 504 4974", "cell": "1 818 581 9349", "statusNote": "", "comments": "", "email": "j_munguia@powerplusutility.com", "bids": {}, "codes": ["015000 Temp  Facilities"]}, {"id": "m0482", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "PPC", "active": true, "contact": "Bill Collins", "phone": "1 714 952 2001", "cell": "", "statusNote": "", "comments": "", "email": "bill@1ppc.com", "bids": {}, "codes": ["220000 Plumbing Rough & Finish", "230000 Hvac"]}, {"id": "m0483", "div": "DIVISION 09", "divName": "FINISHES", "code": "096800 Carpet", "company": "PREMIER CARPET", "active": true, "contact": "Alan Comins", "phone": "1 310 657 4200", "cell": "1 310 701 6777", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["096800 Carpet"]}, {"id": "m0484", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "PRIME AIR", "active": true, "contact": "Steve Yantzer", "phone": "1 818 865 2310", "cell": "1 818 269 0272", "statusNote": "", "comments": "", "email": "syantzer@covad.net", "bids": {"807 6th Ave": {"price": 269390.0, "received": "2025-10-21", "comments": ""}}, "codes": ["230000 Hvac"]}, {"id": "m0485", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "PROGRESSIVE", "active": true, "contact": "Phil Nowaski", "phone": "1 818 709 0988", "cell": "1 805 444 8162", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0486", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "072100 Insulation", "company": "PROGRESSIVE INSULATION", "active": true, "contact": "Phil Nowaski", "phone": "1 818 709 0988", "cell": "1 805 444 8162", "statusNote": "CALL", "comments": "", "email": "", "bids": {}, "codes": ["072100 Insulation"]}, {"id": "m0487", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "072100 Insulation", "company": "PROGRESSIVE INSULATION & WINDOWS", "active": true, "contact": "Kyle Melerski", "phone": "818.709.0988", "cell": "818-201-4100", "statusNote": "", "comments": "", "email": "kmelerski@proiw.com", "bids": {}, "codes": ["072100 Insulation"]}, {"id": "m0488", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Installation", "company": "PROSLIT TILE & STONE", "active": true, "contact": "Irakli Khizanishvili", "phone": "818 9192233", "cell": "", "statusNote": "NEW", "comments": "WEB FORM", "email": "irakli@proslit.com", "bids": {}, "codes": ["096000 Tile - Installation"]}, {"id": "m0489", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "250010 Security Systems", "company": "PROTECH", "active": true, "contact": "Paul Ott", "phone": "1 805 522 1659", "cell": "1 818 887 1369", "statusNote": "", "comments": "X", "email": "paulott@pro-techsystems.com, protechfire@yahoo.com", "bids": {"748 & 750 Palisades Dr": {"price": 50000.0, "received": null, "comments": ""}, "17797 Camino De Yatasto": {"price": 27000.0, "received": "2025-10-23", "comments": ""}, "807 6th Ave": {"price": 16800.0, "received": "2026-01-26", "comments": "original price 17,800 (1k discount)"}, "1080 El Medio Place": {"price": 23000.0, "received": "2025-11-11", "comments": "Check;"}, "15265 W Bestor Blvd": {"price": 21600.0, "received": "2025-10-28", "comments": ""}, "2429 Eastern Canal": {"price": 10700.0, "received": "2025-12-01", "comments": ""}, "16339 Akron": {"price": 10700.0, "received": "2026-01-05", "comments": ""}, "1134 Iliff St": {"price": 9000.0, "received": "2026-04-08", "comments": ""}}, "codes": ["250010 Security Systems", "211300 Fire Spinklers"]}, {"id": "m0490", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "PYRAMID PLASTERING", "active": true, "contact": "Raquel De La Mora", "phone": "1 818 897 9805", "cell": "", "statusNote": "", "comments": "", "email": "office@pyramidplastercorp.com", "bids": {}, "codes": ["092400 Stucco"]}, {"id": "m0491", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "Quilt", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "CALL", "comments": "", "email": "partnersuccess@quilt.com", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0492", "div": "DIVISION 11", "divName": "EQUIPMENT", "code": "111000 Vehicle Equipment", "company": "QUINN RENTAL SERVICES", "active": true, "contact": "Crane Rental", "phone": "562.463.4050", "cell": "562.692.9249", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["111000 Vehicle Equipment"]}, {"id": "m0493", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "R&R PLASTERING INC", "active": true, "contact": "", "phone": "(323) 376-9892", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["092400 Stucco"]}, {"id": "m0494", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "072100 Insulation", "company": "R.B.H. INSULATION", "active": true, "contact": "Oscar Perez", "phone": "1 310 322 8883", "cell": "", "statusNote": "", "comments": "", "email": "oscar@rbhinsulation.com", "bids": {"Quadro Vecchio": {"price": 22305.0, "received": "2025-07-14", "comments": ""}, "213 OFW Waterfront": {"price": 6405.0, "received": "2025-07-31", "comments": ""}, "723 OFW": {"price": 95770.0, "received": "2025-07-22", "comments": ""}, "748 & 750 Palisades Dr": {"price": 21494.0, "received": "2025-08-11", "comments": ""}, "17797 Camino De Yatasto": {"price": 46804.0, "received": "2025-09-17", "comments": "https://login.jobprotech.com/JP_MVC/esign/698205e1-a4b7-4ae2-a706-b7f1db103a9f"}, "807 6th Ave": {"price": 30105.0, "received": "2025-10-01", "comments": "LINK TO SELECT"}, "1093 Palms Blvd": {"price": 8786.0, "received": "2025-11-21", "comments": ""}, "2429 Eastern Canal": {"price": 11164.0, "received": null, "comments": ""}, "16339 Akron": {"price": 11472.0, "received": null, "comments": "https://login.jobprotech.com/JP_MVC/esign/815b70fb-301e-4d1d-bac4-4cdbc2e3d479"}, "12979 Blairwood Dr": {"price": 20939.0, "received": "2026-02-17", "comments": ""}, "1134 Iliff St": {"price": 10117.0, "received": "2026-04-10", "comments": ""}}, "codes": ["072100 Insulation"]}, {"id": "m0495", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "R.E. MCCOY COMPANY", "active": true, "contact": "Concrete floor grinding", "phone": "818-7642101", "cell": "", "statusNote": "", "comments": "VOICE MAIL", "email": "remccoycompany@twc.com", "bids": {}, "codes": ["030630 Concrete Slab"]}, {"id": "m0496", "div": "DIVISION 11", "divName": "EQUIPMENT", "code": "113000 Residential Equipment", "company": "RA APPLIANCES", "active": true, "contact": "Roman Biller", "phone": "1 818 855 9555", "cell": "", "statusNote": "", "comments": "", "email": "service@tofix.net", "bids": {}, "codes": ["113000 Residential Equipment"]}, {"id": "m0497", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "RAY LACK", "active": true, "contact": "Ray Lack", "phone": "1 310 869 6711", "cell": "", "statusNote": "", "comments": "NO PICK UP", "email": "raymondjlack@yahoo.com", "bids": {}, "codes": ["030630 Concrete Slab"]}, {"id": "m0498", "div": "DIVISION 04", "divName": "MASONRY", "code": "042200 Concrete Masonry Unit", "company": "RCA CONCRETE", "active": true, "contact": "Alvaro Rivera", "phone": "818-903-8068", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {"478 Wynola St": {"price": 6400.0, "received": null, "comments": ""}}, "codes": ["042200 Concrete Masonry Unit"]}, {"id": "m0499", "div": "DIVISION 09", "divName": "FINISHES", "code": "099000 Painting", "company": "RED'S CUSTOM PAINTING & WALLPAPER", "active": true, "contact": "Red Reddington", "phone": "1 818 348 1391", "cell": "1 310 770 0900", "statusNote": "", "comments": "", "email": "donerightp@gmail.com", "bids": {}, "codes": ["099000 Painting", "099001 Painting Cabinets"]}, {"id": "m0500", "div": "DIVISION 21", "divName": "FIRE SUPPRESSION", "code": "211300 Fire Spinklers", "company": "REGENCY", "active": false, "contact": "Chaim Jeraffi", "phone": "1 818 982 0126", "cell": "1 818 571 6947", "statusNote": "", "comments": "", "email": "office@regencyfireservices.com", "bids": {}, "codes": ["211300 Fire Spinklers"]}, {"id": "m0501", "div": "DIVISION 05", "divName": "METALS", "code": "051200 Structural Steel", "company": "REMO STEEL", "active": true, "contact": "Ally Cazian", "phone": "1 818 4146610", "cell": "", "statusNote": "NEW", "comments": "", "email": "ally@remosteel.com", "bids": {}, "codes": ["051200 Structural Steel"]}, {"id": "m0502", "div": "DIVISION 05", "divName": "METALS", "code": "051200 Structural Steel", "company": "RENO IRON WORKS", "active": true, "contact": "", "phone": "(775) 329-1111", "cell": "", "statusNote": "NEW", "comments": "", "email": "sales@renoironworks.com", "bids": {}, "codes": ["051200 Structural Steel"]}, {"id": "m0503", "div": "DIVISION 05", "divName": "METALS", "code": "055000 Metal Fabricators", "company": "REPUBLIC", "active": true, "contact": "Jared Medlinsky", "phone": "1 818 341 5323", "cell": "1 310 386 8590", "statusNote": "", "comments": "", "email": "jmedlinsky.rfc@gmail.com", "bids": {}, "codes": ["055000 Metal Fabricators", "323100 Fences & Gates"]}, {"id": "m0504", "div": "DIVISION 14", "divName": "CONVEYING EQUIPMENT", "code": "142000 Elevators", "company": "RESIDENTIAL ELEVATORS", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "sales@residentialelevators.com", "bids": {}, "codes": ["142000 Elevators"]}, {"id": "m0505", "div": "DIVISION 11", "divName": "EQUIPMENT", "code": "112163 Refrigerated Display Equipment", "company": "RESTAURANT DEPOT", "active": true, "contact": "MANNY MACIAS", "phone": "323 964 1200", "cell": "", "statusNote": "", "comments": "", "email": "smware.043@jetrord.com", "bids": {}, "codes": ["112163 Refrigerated Display Equipment"]}, {"id": "m0506", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "RICHARD SMITH CUSTOM CONCRETE", "active": true, "contact": "Larry Ross", "phone": "1 818 710 6615", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["030630 Concrete Slab"]}, {"id": "m0507", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "061000 Rough Carpentry", "company": "RICHARDS", "active": false, "contact": "Myles Richards", "phone": "1 805 845 3133", "cell": "1 805 679 1333", "statusNote": "Mail needs to be updated", "comments": "NO RESPONSE", "email": "myles@arc-sb.com", "bids": {}, "codes": ["061000 Rough Carpentry"]}, {"id": "m0508", "div": "DIVISION 08", "divName": "OPENINGS", "code": "087000 Finish Hardware", "company": "RICK'S HARDWARE", "active": true, "contact": "Sheri Pistone", "phone": "1 818 509 7948", "cell": "1 818 402 2117", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["087000 Finish Hardware"]}, {"id": "m0509", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "Right price rooter & plumbing", "active": true, "contact": "", "phone": "866-766-8374", "cell": "", "statusNote": "NEW", "comments": "", "email": "rightpricerooter@gmail.com", "bids": {}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0510", "div": "DIVISION 05", "divName": "METALS", "code": "055000 Metal Fabricators", "company": "RIGIDIZED METALS", "active": true, "contact": "David Miske", "phone": "1 716 849 4703", "cell": "", "statusNote": "", "comments": "", "email": "davemiske@rigidized.com", "bids": {}, "codes": ["055000 Metal Fabricators"]}, {"id": "m0511", "div": "DIVISION 13", "divName": "SPECIAL CONSTRUCTION", "code": "131100 Swimming Pool/Spa/Fountain", "company": "RIVIERA POOL AND SPA", "active": true, "contact": "Stephen Stubbs", "phone": "1 310 437 4290", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["131100 Swimming Pool/Spa/Fountain"]}, {"id": "m0512", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "ROBERT C. WORTH, INC.", "active": true, "contact": "Cabinets", "phone": "661.942.6601", "cell": "661.942.6911", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["064100 Cabinets"]}, {"id": "m0513", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "250000 Home Automation", "company": "ROBERTS", "active": true, "contact": "Leif Pehrson", "phone": "1 310 276 3955", "cell": "1 310 780 8826", "statusNote": "", "comments": "", "email": "leif@robertshomeav.com", "bids": {}, "codes": ["250000 Home Automation", "262000 Low Voltage"]}, {"id": "m0514", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "061000 Rough Carpentry", "company": "ROGMA CONSTRUCTION SERVICES, INC.", "active": true, "contact": "Tony Herrera", "phone": "1 213 620 1144", "cell": "1 323 974 2074", "statusNote": "", "comments": "EMAIL UPDATED; they only do demolitions", "email": "bids@rogmainc.com, robert@rogmainc.com", "bids": {}, "codes": ["061000 Rough Carpentry"]}, {"id": "m0515", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "015423 Scaffolding", "company": "ROLLS SCAFFOLD INC.", "active": true, "contact": "", "phone": "1 800 523 4775", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["015423 Scaffolding"]}, {"id": "m0516", "div": "DIVISION 11", "divName": "EQUIPMENT", "code": "113000 Residential Equipment", "company": "ROMAN RAYGOZA DESIGN STUDIO", "active": true, "contact": "Roman Raygoza", "phone": "1 323 933 3921", "cell": "", "statusNote": "", "comments": "", "email": "roman@romanraygoza.com", "bids": {}, "codes": ["113000 Residential Equipment", "122000 Window Treatments"]}, {"id": "m0517", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "ROMANOSKI", "active": true, "contact": "David Gerred", "phone": "1 818 559 3644", "cell": "1 818 331 3089", "statusNote": "CALL", "comments": "", "email": "klund@romanoskiglass.com, psmith@romanoskiglass.com", "bids": {}, "codes": ["058000 Glazing"]}, {"id": "m0518", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "ROOF MASTERS", "active": true, "contact": "", "phone": "323-590-8490", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["071000 Roofing"]}, {"id": "m0519", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "ROOFING STANDARDS, INC.", "active": true, "contact": "Roof", "phone": "714.993.9715", "cell": "714.993.9743", "statusNote": "CALL", "comments": "", "email": "info@roofingstandards.com", "bids": {}, "codes": ["071000 Roofing"]}, {"id": "m0520", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "061000 Rough Carpentry", "company": "ROSSMOYNE, INC.", "active": true, "contact": "Laura Verduzco", "phone": "1 818 249 8397", "cell": "1 818 402 1192", "statusNote": "", "comments": "EMAIL UPDATED", "email": "lverduzco@rossmoyneinc.com", "bids": {}, "codes": ["061000 Rough Carpentry"]}, {"id": "m0521", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "ROY E. SMITH PLUMBING CO., INC.", "active": true, "contact": "Ken Smith", "phone": "1 310 398 8855", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0522", "div": "DIVISION 33", "divName": "UTILITIES", "code": "334000 Stormwater management-LID", "company": "ROYAL GARDENS", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["334000 Stormwater management-LID"]}, {"id": "m0523", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "ROYAL PLYWOOD CO", "active": false, "contact": "Dave Mahony", "phone": "1 949 429 9428", "cell": "", "statusNote": "", "comments": "", "email": "davem@royalplywood.com", "bids": {}, "codes": ["064100 Cabinets"]}, {"id": "m0524", "div": "DIVISION 11", "divName": "EQUIPMENT", "code": "111000 Vehicle Equipment", "company": "RSC EQUIPMENT RENTAL", "active": true, "contact": "Steve Roberts", "phone": "1 818 504 4333", "cell": "1 818 822 9548", "statusNote": "", "comments": "", "email": "steve.roberts@rscrental.com", "bids": {}, "codes": ["111000 Vehicle Equipment"]}, {"id": "m0525", "div": "DIVISION 05", "divName": "METALS", "code": "051200 Structural Steel", "company": "RSR", "active": true, "contact": "Hector/ Edgar Grijalba", "phone": "1 760 244 2210", "cell": "", "statusNote": "", "comments": "", "email": "rsrsteel@aol.com", "bids": {"52-60 Market St": {"price": 79900.0, "received": "2025-01-28", "comments": ""}, "Quadro Vecchio": {"price": 42800.0, "received": "2025-07-11", "comments": ""}, "6537 Topanga Canyon": {"price": 20900.0, "received": "2026-02-12", "comments": ""}, "12979 Blairwood Dr": {"price": 42300.0, "received": "2026-03-03", "comments": ""}}, "codes": ["051200 Structural Steel"]}, {"id": "m0526", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "RTR ROOFING", "active": true, "contact": "Richard", "phone": "310-383-3063", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["071000 Roofing"]}, {"id": "m0527", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "RUBENS GLASS & MIRRORS", "active": true, "contact": "Glass & Glazing", "phone": "616 S. La Brea Ave.", "cell": "323.937.7519", "statusNote": "", "comments": "", "email": "ruben.glass@me.com", "bids": {"723 OFW": {"price": 279687.0, "received": "2025-09-23", "comments": ""}}, "codes": ["058000 Glazing"]}, {"id": "m0528", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "270500 Audio Visual Systems", "company": "RUTHERFORD DESIGN", "active": true, "contact": "Scott Blackwell", "phone": "1 818 312 5262", "cell": "", "statusNote": "", "comments": "", "email": "data@rutherforddesign.com", "bids": {}, "codes": ["270500 Audio Visual Systems"]}, {"id": "m0529", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "RW ELECTRIC", "active": true, "contact": "Rick White", "phone": "1 714 767 0389", "cell": "", "statusNote": "", "comments": "", "email": "richard@rw-electric.com", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0530", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071010 Waterproofing", "company": "S&S", "active": false, "contact": "Shane Satey", "phone": "1 818 981 3225", "cell": "1 818 497 0047", "statusNote": "", "comments": "", "email": "sandswaterproofing@gmail.com", "bids": {}, "codes": ["071010 Waterproofing", "077700 Waterproofing Build. Wrap"]}, {"id": "m0531", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "077700 Waterproofing Build. Wrap", "company": "S&W", "active": true, "contact": "Jason", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {"52-60 Market St": {"price": 48940.0, "received": "2025-02-21", "comments": ""}, "Quadro Vecchio": {"price": 34201.0, "received": "2025-06-24", "comments": ""}}, "codes": ["077700 Waterproofing Build. Wrap"]}, {"id": "m0532", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "015423 Scaffolding", "company": "SAFE-T SCAFFOLDING", "active": true, "contact": "Joe Connor", "phone": "1 310 715 6364", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["015423 Scaffolding"]}, {"id": "m0533", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "SAHARA HEATING & AIR", "active": true, "contact": "", "phone": "(818) 437-5165", "cell": "", "statusNote": "NEW", "comments": "", "email": "saharaheatandairdesk@gmail.com", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0534", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "061000 Rough Carpentry", "company": "SAL-OYA CONSTRUCTION CO,INC", "active": true, "contact": "Alberto Salinas", "phone": "1 661 209 2243", "cell": "", "statusNote": "", "comments": "", "email": "albert2salinas@gmail.com", "bids": {"1080 El Medio Place": {"price": 356820.0, "received": "2025-10-23", "comments": "Check;Framing and materials"}, "2429 Eastern Canal": {"price": 142000.0, "received": "2025-12-01", "comments": ""}, "16339 Akron": {"price": 129400.0, "received": "2026-01-02", "comments": ""}, "12979 Blairwood Dr": {"price": 475000.0, "received": "2026-02-12", "comments": ""}, "1134 Iliff St": {"price": 111500.0, "received": "2026-04-11", "comments": ""}}, "codes": ["061000 Rough Carpentry"]}, {"id": "m0535", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "061000 Rough Carpentry", "company": "SAL-OYA CONSTRUCTION COMPANY, INC.", "active": false, "contact": "Alberto Salinas", "phone": "661-209-2243", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {"1080 El Medio Place": {"price": 356820.0, "received": "2025-10-24", "comments": ""}}, "codes": ["061000 Rough Carpentry"]}, {"id": "m0536", "div": "DIVISION 09", "divName": "FINISHES", "code": "074624 Wood Siding - Install", "company": "SALVADOR ROMERO", "active": true, "contact": "Salvador Romero", "phone": "562-324-1589", "cell": "", "statusNote": "HIGHLY ACTIVE", "comments": "", "email": "romerochava78@gmail.com", "bids": {"429 Sherman Canal": {"price": 14368.0, "received": "2025-07-07", "comments": ""}, "865 N Oreo Pl": {"price": 22170.0, "received": "2025-09-26", "comments": ""}, "807 6th Ave": {"price": 23600.0, "received": "2025-10-09", "comments": ""}, "52-60 Market St": {"price": 35600.0, "received": "2025-01-28", "comments": ""}, "748 & 750 Palisades Dr": {"price": 26670.0, "received": "2025-08-06", "comments": ""}, "723 OFW": {"price": 17070.0, "received": "2025-07-22", "comments": ""}}, "codes": ["074624 Wood Siding - Install", "093200 Elevated Roof Top Decks", "062000 Finish Carpentry", "081001 Exterior Doors & Windows Installation", "081002 Interior Doors & Frames", "081004 Garage Doors", "096100 Flooring"]}, {"id": "m0537", "div": "DIVISION 03", "divName": "CONCRETE", "code": "033100 Structural Concrete", "company": "SAM VAN CONSTRUCTION", "active": true, "contact": "Sam", "phone": "1 310 420 9060", "cell": "", "statusNote": "EMAIL UPDATED", "comments": "", "email": "samvanconstruction@hotmail.com", "bids": {}, "codes": ["033100 Structural Concrete", "030630 Concrete Slab", "042200 Concrete Masonry Unit"]}, {"id": "m0538", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "SAMSONS CONCRETE", "active": true, "contact": "", "phone": "1 805 527 0622", "cell": "", "statusNote": "", "comments": "", "email": "samsons01@yahoo.com", "bids": {}, "codes": ["030630 Concrete Slab"]}, {"id": "m0539", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "061000 Rough Carpentry", "company": "SCHARFF", "active": false, "contact": "John Scharff", "phone": "1 310 391 4464", "cell": "1 310 940 1303", "statusNote": "", "comments": "", "email": "john@scharffconstruction.com", "bids": {}, "codes": ["061000 Rough Carpentry"]}, {"id": "m0540", "div": "DIVISION 14", "divName": "CONVEYING EQUIPMENT", "code": "142000 Elevators", "company": "SCHINDLER ELEVATORS & ESCALATORS", "active": true, "contact": "Monte Lukov", "phone": "818-336-3000", "cell": "", "statusNote": "", "comments": "", "email": "monte.lukov@schindler.com", "bids": {"723 OFW": {"price": 190500.0, "received": "2025-10-06", "comments": ""}}, "codes": ["142000 Elevators"]}, {"id": "m0541", "div": "DIVISION 05", "divName": "METALS", "code": "055000 Metal Fabricators", "company": "SECURE SHEET METAL", "active": true, "contact": "Robert Riepe", "phone": "1 818 341 8100", "cell": "", "statusNote": "", "comments": "asked for remove him from list", "email": "bob@securesheetmetal.com, forrest@securesheetmetal.com", "bids": {}, "codes": ["055000 Metal Fabricators", "076000 Flashing & Sheet Metal", "074619 Steel Siding"]}, {"id": "m0542", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "076113 Standing Seam Sheet Metal Roofing", "company": "Secure Sheet Metal Inc.", "active": true, "contact": "Robert Riepe", "phone": "818 3418100", "cell": "", "statusNote": "", "comments": "", "email": "bob@securesheetmetal.com", "bids": {}, "codes": ["076113 Standing Seam Sheet Metal Roofing"]}, {"id": "m0543", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "017410 Dumpsters", "company": "SEGOVIA ROLL OFF", "active": true, "contact": "Silvia Alvarez", "phone": "1 818 896 4367", "cell": "", "statusNote": "", "comments": "", "email": "segoviarolloffinc@live.com", "bids": {}, "codes": ["017410 Dumpsters"]}, {"id": "m0544", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "SENNA TREE COMPANY", "active": true, "contact": "Mike McShane", "phone": "1 818 957 5755", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0545", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "017423 Final Clean-up", "company": "SERVPRO", "active": true, "contact": "Tim Lawler", "phone": "1 818 842 1400", "cell": "", "statusNote": "", "comments": "", "email": "servpro2720@servproburbank.com", "bids": {}, "codes": ["017423 Final Clean-up"]}, {"id": "m0546", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Installation", "company": "Sevak @ Firenze tile", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "sevak@firenzetile.com", "bids": {}, "codes": ["096000 Tile - Installation"]}, {"id": "m0547", "div": "DIVISION 09", "divName": "FINISHES", "code": "096400 Wood Flooring", "company": "SFC HARDWOOD & CARPET, INC.", "active": false, "contact": "Shane Broumand", "phone": "1 818 578 6019", "cell": "1 818 292 2457", "statusNote": "", "comments": "BOUNCED BACK", "email": "shane@sfchardwoodandcarpet.com", "bids": {}, "codes": ["096400 Wood Flooring", "096800 Carpet"]}, {"id": "m0548", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "076000 Flashing & Sheet Metal", "company": "SHEET METAL GUY: LEE", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "sheetmetalmaniac@hotmail.com", "bids": {}, "codes": ["076000 Flashing & Sheet Metal"]}, {"id": "m0549", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "SHOCK ELECTRIC", "active": true, "contact": "", "phone": "(800)311-9695", "cell": "", "statusNote": "", "comments": "NEW", "email": "shokelectric@yahoo.com", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0550", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "SILVERMAN ROOFING", "active": true, "contact": "Richard Silverman", "phone": "1 310 399 0888", "cell": "", "statusNote": "", "comments": "", "email": "rtrroofer@aol.com", "bids": {}, "codes": ["071000 Roofing"]}, {"id": "m0551", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "SIMICH CONSTRUCTION", "active": true, "contact": "John Simich", "phone": "1 310 519 8203", "cell": "", "statusNote": "EMAIL UPDATED", "comments": "", "email": "john@simich.com", "bids": {}, "codes": ["030630 Concrete Slab", "033100 Structural Concrete"]}, {"id": "m0552", "div": "DIVISION 21", "divName": "FIRE SUPPRESSION", "code": "211300 Fire Spinklers", "company": "SINGLETON", "active": true, "contact": "Carla Sanchez", "phone": "1 818 252 5744", "cell": "", "statusNote": "", "comments": "X", "email": "msingletonfire@sbcglobal.net", "bids": {"6537 Topanga Canyon": {"price": 34925.0, "received": "2026-02-11", "comments": "12K for installation"}, "17797 Camino De Yatasto": {"price": 31950.0, "received": "2025-10-24", "comments": ""}, "807 6th Ave": {"price": 22100.0, "received": "2025-10-06", "comments": "Pricing adjustment completed"}, "1080 El Medio Place": {"price": 18950.0, "received": "2025-11-17", "comments": ""}, "16339 Akron": {"price": 12950.0, "received": "2025-12-23", "comments": ""}}, "codes": ["211300 Fire Spinklers"]}, {"id": "m0553", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "262000 Low Voltage", "company": "SKYLINE COMMUNICATIONS", "active": true, "contact": "Louis Hurlburt", "phone": "1 310 680 7960", "cell": "", "statusNote": "", "comments": "", "email": "louis@skyline-communications.com", "bids": {}, "codes": ["262000 Low Voltage"]}, {"id": "m0554", "div": "DIVISION 05", "divName": "METALS", "code": "051200 Structural Steel", "company": "SKYLINE FABRICATOR", "active": true, "contact": "Henry Mora", "phone": "310-901-0117", "cell": "", "statusNote": "", "comments": "", "email": "h.mora@skylinefabrication.com", "bids": {"6537 Topanga Canyon": {"price": 38821.0, "received": "2026-02-13", "comments": "BID FOR CANOPY AND OPENINGS"}, "865 N Oreo Pl": {"price": 101588.27, "received": "2025-10-02", "comments": ""}, "807 6th Ave": {"price": 183449.56, "received": "2025-10-07", "comments": "With discount: $180,679.43"}, "15265 W Bestor Blvd": {"price": 69410.13, "received": "2025-12-22", "comments": ""}}, "codes": ["051200 Structural Steel"]}, {"id": "m0555", "div": "DIVISION 09", "divName": "FINISHES", "code": "092000 Gypsum Board", "company": "SLABACK", "active": false, "contact": "Ray Poje", "phone": "1 310 306 7808", "cell": "1 310 345 4856", "statusNote": "", "comments": "Says that he has bid over 10 projects but didn't get any and he was paying to his estimator, so he couldn't lose more money", "email": "slabackconstruction@yahoo.com", "bids": {}, "codes": ["092000 Gypsum Board"]}, {"id": "m0556", "div": "DIVISION 04", "divName": "MASONRY", "code": "042100 Masonry Brick Veneer", "company": "SMG STONE COMPANY INC.", "active": true, "contact": "Doug McKay", "phone": "1 818 767 0000", "cell": "1 818 804 1454", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["042100 Masonry Brick Veneer", "096000 Tile - Material"]}, {"id": "m0557", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "062000 Finish Carpentry", "company": "SMITH BROS.", "active": false, "contact": "Aaron Foster", "phone": "1 805 449 2841", "cell": "", "statusNote": "", "comments": "", "email": "aaron@smith-bros.net", "bids": {}, "codes": ["062000 Finish Carpentry", "077700 Waterproofing Build. Wrap", "081001 Exterior Doors & Windows Installation", "087000 Finish Hardware", "074623 Wood Siding"]}, {"id": "m0558", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "SMITH BROS., INC.", "active": false, "contact": "Aaron Foster", "phone": "1 805 449 2841", "cell": "", "statusNote": "", "comments": "", "email": "aaron@smith-bros.net", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation", "086000 Skylights"]}, {"id": "m0559", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "SNOW CONSTRUCTION", "active": true, "contact": "Billy snow", "phone": "310-926-9993", "cell": "", "statusNote": "HIGHLY ACTIVE", "comments": "", "email": "snownewprojects@gmail.com", "bids": {"Quadro Vecchio": {"price": 210000.0, "received": "2025-07-21", "comments": "60K DEMO // 150K GRADING"}, "429 Sherman Canal": {"price": 50000.0, "received": "2025-07-22", "comments": ""}, "478 Wynola St": {"price": 15000.0, "received": "2025-09-02", "comments": ""}, "17797 Camino De Yatasto": {"price": 102000.0, "received": null, "comments": ""}, "4565 Dundee Drive": {"price": 25000.0, "received": "2025-11-17", "comments": "rough number"}, "865 N Oreo Pl": {"price": 320000.0, "received": "2025-09-28", "comments": ""}, "807 6th Ave": {"price": 500000.0, "received": null, "comments": "Shoring $193,000 + $36,000 excavation"}, "16339 Akron": {"price": 80000.0, "received": "2026-01-07", "comments": ""}, "14949 Mc Kendree Ave": {"price": 210000.0, "received": "2026-01-28", "comments": "FOUNDATION EXCAVATION ($36K) GRAVEL & WATERPROOFING (25K) SIDE YARD (22K) STEPS DRIVEWAY TO PATIO (25K)"}, "12979 Blairwood Dr": {"price": 500000.0, "received": "2026-02-05", "comments": ""}}, "codes": ["024000 Demolition", "033100 Structural Concrete", "061000 Rough Carpentry", "051200 Structural Steel"]}, {"id": "m0560", "div": "DIVISION 10", "divName": "SPECIALTIES", "code": "102800 Toilet/Bathrom Accessories", "company": "SNYDER DIAMOND", "active": true, "contact": "Perry Stewart", "phone": "1 310 450 1000", "cell": "1 818 674 8299", "statusNote": "", "comments": "", "email": "pstewart@snyderdiamond.com", "bids": {}, "codes": ["102800 Toilet/Bathrom Accessories", "113000 Residential Equipment", "224000 Plumbing Fixtures"]}, {"id": "m0561", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "SOCAL AIR CONDITION & HEATING", "active": true, "contact": "Talin Mardirossian", "phone": "818 471 6022", "cell": "", "statusNote": "NEW", "comments": "", "email": "hello@socalair.co, menooa@socalair.co, talin@socalair.co", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0562", "div": "DIVISION 03", "divName": "CONCRETE", "code": "033100 Structural Concrete", "company": "SoCal Concrete", "active": true, "contact": "Joe Arriaga", "phone": "818-402-9483", "cell": "949-402-6083", "statusNote": "", "comments": "VOICEMAIL", "email": "socalconcrete1@gmail.com, jim.scconcrete@gmail.com", "bids": {"478 Wynola St": {"price": 36650.0, "received": "2025-09-17", "comments": ""}}, "codes": ["033100 Structural Concrete"]}, {"id": "m0563", "div": "DIVISION 04", "divName": "METALS", "code": "055200 Metal Railing", "company": "SOCAL STAIRS", "active": true, "contact": "Dan Calton", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "calton@socalstairs.com", "bids": {"213 OFW Waterfront": {"price": 32000.0, "received": "25/06/2025", "comments": "Depending on exact measurements"}, "723 OFW": {"price": 285957.0, "received": "2025-09-03", "comments": "WORKING ON BID"}, "748 & 750 Palisades Dr": {"price": 4225.0, "received": null, "comments": ""}, "478 Wynola St": {"price": 18494.0, "received": "2025-09-02", "comments": ""}}, "codes": ["055200 Metal Railing"]}, {"id": "m0564", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "SOLE AIRE", "active": true, "contact": "Dan", "phone": "1 818 365 3161", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0565", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "SOLIDO CONSTRUCTION", "active": true, "contact": "Carlos", "phone": "818.201.7701", "cell": "", "statusNote": "", "comments": "NO RESPONSE;Doesn't pick up the phone 10/16/25", "email": "solidoconstruction1@gmail.com", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation", "061000 Rough Carpentry"]}, {"id": "m0566", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "250010 Security Systems", "company": "SONARGUARD POOL SECURITY SYSTEM", "active": false, "contact": "Derek Trowbridge", "phone": "1 949 727 9399", "cell": "1 949 632 3489", "statusNote": "", "comments": "", "email": "dt@sonarguard.com", "bids": {}, "codes": ["250010 Security Systems"]}, {"id": "m0567", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "015423 Scaffolding", "company": "SOUTH BAY SCAFFOLD & LADDER CO., INC.", "active": true, "contact": "Michael Martinez", "phone": "1 310 965 9565", "cell": "", "statusNote": "", "comments": "", "email": "sbscaffold@sbcglobal.net", "bids": {}, "codes": ["015423 Scaffolding"]}, {"id": "m0568", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "SOUTHERN CALIFORNIA REPIPING & PLUMBNIG REPAIRS", "active": true, "contact": "Richard Otto", "phone": "1 310 541 7610", "cell": "1 310 809 9180", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0569", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "SOUTHLAND HEATING AND AIR", "active": true, "contact": "David Molina", "phone": "1 818 652 4265", "cell": "", "statusNote": "", "comments": "", "email": "davemolina@southlandac.com", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0570", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "SOUTHSIDE STUCCO", "active": true, "contact": "John De La Cruz", "phone": "310 714-1394", "cell": "", "statusNote": "", "comments": "", "email": "john@southsidestucco.com", "bids": {"723 OFW": {"price": 29820.0, "received": "2025-08-28", "comments": ""}, "4565 Dundee Drive": {"price": 22920.0, "received": "2025-11-30", "comments": ""}, "1093 Palms Blvd": {"price": 21898.0, "received": "2025-11-30", "comments": ""}, "2429 Eastern Canal": {"price": 41457.0, "received": "2025-12-03", "comments": ""}, "16339 Akron": {"price": 19998.0, "received": "2026-01-04", "comments": ""}}, "codes": ["092400 Stucco"]}, {"id": "m0571", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "SPECTRA COMPANY", "active": false, "contact": "Heather La Fave", "phone": "1 909 599 0760", "cell": "1 909 599 6862", "statusNote": "", "comments": "", "email": "hlafave@spectracompany.com", "bids": {}, "codes": ["071000 Roofing", "071010 Waterproofing"]}, {"id": "m0572", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "323100 Fences & Gates", "company": "SQUARE CUT CONSTRUCTION, INC.", "active": true, "contact": "Fred Farnham", "phone": "1 310 990 4790", "cell": "", "statusNote": "", "comments": "", "email": "sales@squarecutfencing.com", "bids": {}, "codes": ["323100 Fences & Gates"]}, {"id": "m0573", "div": "DIVISION 01", "divName": "GENERAL REQUIREMENTS", "code": "017423 Final Clean-up", "company": "SQUEAKY CLEAN CO.", "active": true, "contact": "Zeke Torres", "phone": "1 310 457 7777", "cell": "", "statusNote": "", "comments": "", "email": "zekedances@yahoo.com", "bids": {}, "codes": ["017423 Final Clean-up"]}, {"id": "m0574", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "STATE PLASTERING, INC.", "active": true, "contact": "Lath & Plaster", "phone": "661.298.2848", "cell": "661.298.2947", "statusNote": "", "comments": "", "email": "stateplasteringinc@yahoo.com", "bids": {}, "codes": ["092400 Stucco"]}, {"id": "m0575", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "STEEL CITY GLASS, INC.", "active": true, "contact": "John Colosimo", "phone": "1 714 755 1000", "cell": "1 714 915 0368", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["058000 Glazing"]}, {"id": "m0576", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "STEVE HANSON LANDSCAPING", "active": false, "contact": "Steve Hanson", "phone": "1 805 563 3429", "cell": "1 805 896 6422", "statusNote": "", "comments": "dont serve pacific, only santa barbara", "email": "steve@stevehansonlandscaping.com", "bids": {}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0577", "div": "DIVISION 10", "divName": "SPECIALTIES", "code": "103000 Fireplace", "company": "STILLSON FIREPLACE", "active": true, "contact": "Bruce Medeck", "phone": "1 951 788 2828", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["103000 Fireplace"]}, {"id": "m0578", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "STOCK WINDOW AND DOOR", "active": true, "contact": "ALEX CACERES", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "acaceres@westsidedoor.com", "bids": {"15265 W Bestor Blvd": {"price": 131982.0, "received": "2026-12-02", "comments": "Includes delivery"}}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0579", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Material", "company": "STONECRAFTERS", "active": true, "contact": "Ramin Bagherzadeh", "phone": "1 310 680 7070", "cell": "mail@demolink.org", "statusNote": "", "comments": "", "email": "raminbagher@aol.com", "bids": {}, "codes": ["096000 Tile - Material"]}, {"id": "m0580", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "STORREY BUILDERS", "active": true, "contact": "Steve Richeson", "phone": "1 818 491 5219", "cell": "1 818 720 9414", "statusNote": "ANY OF THE NUMBERS IS IN USE", "comments": "NO ANSWER", "email": "steve@storreybuilding.com", "bids": {}, "codes": ["030630 Concrete Slab", "061000 Rough Carpentry", "033100 Structural Concrete", "077700 Waterproofing Build. Wrap"]}, {"id": "m0581", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "STRUCTURAL MATERIALS CO.", "active": true, "contact": "Dave Westcott", "phone": "1 323 728 7115", "cell": "1 323 974 2233", "statusNote": "CALL", "comments": "", "email": "dave.westcott@structuralmaterials.com", "bids": {}, "codes": ["071000 Roofing"]}, {"id": "m0582", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "STUBBINSPAINTING", "active": true, "contact": "Mike Aliyev", "phone": "", "cell": "", "statusNote": "NEW", "comments": "", "email": "info@stubbinspainting.com", "bids": {"478 Wynola St": {"price": 3200.0, "received": null, "comments": ""}}, "codes": ["092400 Stucco"]}, {"id": "m0583", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "SUBURFACE IMAGING, INC.", "active": true, "contact": "Jamie Davis", "phone": "1 310 781 9405", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["030630 Concrete Slab"]}, {"id": "m0584", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "SUH GLASS", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "suhglass@gmail.com", "bids": {}, "codes": ["058000 Glazing"]}, {"id": "m0585", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "269900 Electric Fixtures", "company": "SUN", "active": true, "contact": "Hans Christensen", "phone": "1 818 345 8344", "cell": "1 818 632 4811", "statusNote": "", "comments": "", "email": "sunelectricco@aol.com", "bids": {}, "codes": ["269900 Electric Fixtures"]}, {"id": "m0586", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "SUN ELECTRIC", "active": false, "contact": "Hans Christensen", "phone": "1 818 345 8344", "cell": "1 818 632 4811", "statusNote": "", "comments": "", "email": "sunelectricco@aol.com", "bids": {"478 Wynola St": {"price": 54540.0, "received": "2025-08-21", "comments": ""}, "17797 Camino De Yatasto": {"price": 534300.0, "received": "2025-10-27", "comments": ""}, "1080 El Medio Place": {"price": 231800.0, "received": "2025-10-24", "comments": "Check;"}, "15265 W Bestor Blvd": {"price": 255800.0, "received": "2025-11-18", "comments": ""}, "1093 Palms Blvd": {"price": 65000.0, "received": "2025-11-21", "comments": ""}, "2429 Eastern Canal": {"price": 65000.0, "received": "2025-11-21", "comments": ""}}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0587", "div": "DIVISION 09", "divName": "FINISHES", "code": "099000 Painting", "company": "SUN MI PAINTING CO.", "active": true, "contact": "John Shin", "phone": "1 213 384 0899", "cell": "1 213 595 9249", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["099000 Painting"]}, {"id": "m0588", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "SUN-LITE", "active": false, "contact": "Sammy Morales, Jr.", "phone": "1 323 728 7399", "cell": "1 323 309 3916", "statusNote": "", "comments": "", "email": "samjr@sun-litedemo.com", "bids": {}, "codes": ["024000 Demolition"]}, {"id": "m0589", "div": "DIVISION 08", "divName": "OPENINGS", "code": "086000 Skylights", "company": "SUNSATIONAL SKYLIGHTS", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["086000 Skylights"]}, {"id": "m0590", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "072100 Insulation", "company": "SUPERGREEN INSULATION", "active": true, "contact": "", "phone": "888 2782902", "cell": "", "statusNote": "NEW", "comments": "", "email": "supergreenattic@gmail.com", "bids": {}, "codes": ["072100 Insulation"]}, {"id": "m0591", "div": "DIVISION 12", "divName": "FURNISHINGS", "code": "122000 Window Treatments", "company": "SUPERIOR AWNING", "active": true, "contact": "Don Barnett", "phone": "1 800 780 0201", "cell": "1 805 947 9018", "statusNote": "", "comments": "", "email": "info@superiorawning.com", "bids": {}, "codes": ["122000 Window Treatments"]}, {"id": "m0592", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "SURE LIGHT ELECTRIC", "active": false, "contact": "Dave Trumbull", "phone": "1 323 810 1708", "cell": "", "statusNote": "", "comments": "", "email": "surelightelectric@hotmail.com", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0593", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071010 Waterproofing", "company": "SW WATERPROOFING", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "swwaterproofing@att.net", "bids": {"Quadro Vecchio": {"price": 34201.0, "received": "2024-06-24", "comments": ""}, "478 Wynola St": {"price": 3740.0, "received": "2025-09-04", "comments": "https://links.notification.intuit.com/ls/click?upn=u001.Hu9nToJLxsJSQR8ZHWn8Ib7JikYF6PNXv5VK-2BAfeSpVHPRNy-2BFDtJ-2BhNUfKXTverofrKjvXVKH4ba5KbTX-2BS4eGw4PMhAF-2Fff6NcQw0jmOddHXEDPPlVLXvqO0PAFHlaXpfFAYRxA7bv7KAqJsiO7GHe-2ByF32LHGfujCXXSyZai7dYDAtyMcBNGjsYX4cUAgEg9L6YqS4R-2FYQmI6yqr57QJS3Fhxw-2FUB4j6255t8cZg-2F-2BVnXuXMC1u03IvIjhEwsisKSnsdhn6Vg6dp95iR8ug-3D-3DMr_I_m62Kq-2BZVlqTCB7tW71uBl1KmDGOT7iBnPn-2F0vXZnl6qIO-2BP7tTuT7MAQNOTDHC4V8W-2F0YEstHgMb7RFIQbTR1IoXCORVrzpBK6WT0Urz-2FVt8mVyuLEpNGxx6-2BiSHJA9x5iCZT-2FQMm93ebmKNqe8d2vBYg5p4T96-2F9vQjiQaKk0mxbvML2y6RK0hKvf2WdMp8XmzCDC9xsUn3lBBfruJase0zfm2dYj1NhQvyMmDtyoBMU3qHiDZDdIF4wauMiql54dW6pUF7nLI8UtHqLEgVUvCuloo3qP1xEqIIgJ9yhQXEppLHdQTCGmh0FzSQ8tWCwDwSpzjEARH74CsACTObAZheWLXH73gGBveHU5MiBCeH-2FvI7ftUixptdV658UsOVaqhN8UIUih5mAMk6eyplTYwisKcm6U3CIcwTKZa6inzLkIXI78AWnOuZRQqzG4Bhe6lkWuIjEmnvBwEPavXw4gNtu1wtKG40eDu8ZaWgh-2FWt7YlqW66BQf-2BtIhRH0n57tHOC7XV5Q4LBbEKhvIqB9h93j5DMwEyAo8kyoZVuGc0fLi06nYoE4H3kjy1p86fH0RNGokPGW6zEXJDynJy8AvuA-2FoNTVyf1fF-2Fl8d-2F4XQzwj1wenLEiRR6c-2FlQQJD3I5m9-2FlpW71GdKsGx-2FBjZXSp-2FmsRkw4oXDZF2pVsEJURzWzDeBXRFV0YKQnRCZ-2Bb779Mzs8t96ZG1bdXzmoTm-2BMpjOE5mnK9z-2FjdqNwp4A-2F-2Fpzi6UM2rVn96iPoCjnxfyNBtKx2HOpP9AGM1M9D6-2BL-2FjKhRTg4OkM-2BS3eXn-2FJri-2Fl0SdVmPgDVU6EU9nlBD1QaVQa4-2FDMHIhgGzN2U-2Fk0bXeQDg2L-2Bpvk1qBdyWrYsXwT13-2FwgliN8r6YwqRAkpPtb5JgP6zxJQYaWhuE5yTOC50ynzfADf5nfmRwRkCopVvDCdtIUe0WXwe4oSarZnuxomHtgBIN-2BCQlidais1Mrp-2B-2FpTrtt5Mi4HEtcPFlxMM3tKv2co5SoB5iXZ6bAgp7aycJaoH9w8j3g9fTt9kp2sAhGBv8ov5DjNCXStm30c5kQXCQkcJ3SaHmsVWkaxmCbww5DjxM0BE9kiFJJENSdcy10sWk9GuKNSJttKeQdDu6fCLVrtvkzFbYnQJjW-2B-2BaGCEJh000hlh4gwxzEhNZu6yKP5n5Vt-2Ft1QDq5DfjMkrFqkvRB9tWCaLfYy1ZaVea0JwDIzVb9He3JWtGKotfiTVvG49bN8Iz-2FU5ixO-2B7w6YulgA2IW8TJSz1Y8e-2BuRAsJrfYLjn67y-2FM5G3oNBywJC5PJ-2BM9ymeOCLFAQrgKOV0l9OaQ72Bf8Od2MtGQ2-2BJ9IqN4mi3TaZfwxqg4iclF0hkQ-3D-3D"}, "17797 Camino De Yatasto": {"price": 57911.0, "received": "2025-10-30", "comments": ""}}, "codes": ["071010 Waterproofing"]}, {"id": "m0594", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "SWISS WOODWORKING", "active": true, "contact": "Nicola Ganzoni", "phone": "310 7710622", "cell": "3106595200.0", "statusNote": "", "comments": "", "email": "nick@swisswoodworking.com", "bids": {}, "codes": ["064100 Cabinets"]}, {"id": "m0595", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "061000 Rough Carpentry", "company": "T.R. WURSTER", "active": true, "contact": "Jonathan Wurster", "phone": "1 818 349 1090", "cell": "1 818 391 4208", "statusNote": "", "comments": "", "email": "jon@trwurster.com", "bids": {"17797 Camino De Yatasto": {"price": 1390000.0, "received": null, "comments": "Payment to be made as follows: 1. $ 348,000 retainer prior to commencement 2. $ weekly T&M progress draws net 7 3. $ refundable retainer applied toward final invoice(s)"}, "1080 El Medio Place": {"price": 576000.0, "received": "2025-10-17", "comments": "Check;"}, "15265 W Bestor Blvd": {"price": 1119000.0, "received": "2025-12-19", "comments": "Includes all"}, "4565 Dundee Drive": {"price": 410000.0, "received": null, "comments": "BID FOR FOUNDATION - STRUCTURAL STEEL - ROUGH CARPENTRY"}, "1093 Palms Blvd": {"price": 76000.0, "received": "2025-11-24", "comments": ""}, "2429 Eastern Canal": {"price": 210000.0, "received": "2025-11-24", "comments": ""}, "16339 Akron": {"price": 125000.0, "received": "2025-12-23", "comments": ""}}, "codes": ["061000 Rough Carpentry"]}, {"id": "m0596", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "TASHMANS", "active": true, "contact": "Tashman Kenny", "phone": "work (323) 656-7028", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0597", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "TAYLOR ELECTRIC", "active": false, "contact": "Matt Taylor", "phone": "1 805 897 3333", "cell": "1 805 448 8846", "statusNote": "", "comments": "", "email": "matt@taylorelectricsb.com", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0598", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "TEAM ROOTER", "active": true, "contact": "", "phone": "(844) 247-9874", "cell": "", "statusNote": "NEW", "comments": "", "email": "info@teamrooter.com", "bids": {}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0599", "div": "DIVISION 09", "divName": "FINISHES", "code": "092400 Stucco", "company": "TEX STON", "active": false, "contact": "Raul Reyes", "phone": "1 310 866 7006", "cell": "raul.r@meodedpaint.com", "statusNote": "", "comments": "", "email": "raul@wallsandsurfaces.com", "bids": {}, "codes": ["092400 Stucco"]}, {"id": "m0600", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "TH CONSTRUCTION INC.", "active": true, "contact": "Tom", "phone": "1 310 370 8701", "cell": "", "statusNote": "ANY OF THE NUMBERS IS IN USE", "comments": "", "email": "tom@th-constructioninc.com", "bids": {}, "codes": ["030630 Concrete Slab", "033100 Structural Concrete"]}, {"id": "m0601", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "THE BANCHMARK", "active": true, "contact": "Cowles Sandra", "phone": "(310) 313-7274", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0602", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "THE BEST DEMO & GRADING", "active": true, "contact": "Jesus Astorga", "phone": "1 818 366 3500", "cell": "818-253-6598", "statusNote": "they will send on friday 10/24", "comments": "", "email": "bestdemo1994@yahoo.com", "bids": {"52-60 Market St": {"price": 102000.0, "received": "2025-02-05", "comments": ""}, "Quadro Vecchio": {"price": 51100.0, "received": "2025-05-02", "comments": ""}, "478 Wynola St": {"price": 17935.0, "received": "2025-09-16", "comments": ""}}, "codes": ["024000 Demolition", "334000 Stormwater management-LID"]}, {"id": "m0603", "div": "DIVISION 05", "divName": "METALS", "code": "051200 Structural Steel", "company": "THE BEST STRUCTURAL WELDING", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "rafael.aguilera71@hotmail.com", "bids": {"865 N Oreo Pl": {"price": 114704.0, "received": null, "comments": ""}, "807 6th Ave": {"price": 146190.0, "received": "2025-10-05", "comments": ""}}, "codes": ["051200 Structural Steel"]}, {"id": "m0604", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "THE COLD CLOUD", "active": true, "contact": "", "phone": "(747) 298-8580", "cell": "", "statusNote": "NEW", "comments": "", "email": "info@thecoldcloud.com", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0605", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "THE KNAPP SERVICE COMPANY", "active": true, "contact": "", "phone": "1 760 771 0181", "cell": "", "statusNote": "", "comments": "", "email": "benjaminknappland@hotmail.com", "bids": {}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0606", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "THE PRODUCT SOURCE", "active": true, "contact": "TARA JAZDZYK", "phone": "1 770 592 3145", "cell": "", "statusNote": "", "comments": "", "email": "tarajazdzyk@tpsgranite.com", "bids": {}, "codes": ["064100 Cabinets"]}, {"id": "m0607", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "THE ROOF DOCTOR", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["071000 Roofing"]}, {"id": "m0608", "div": "DIVISION 09", "divName": "FINISHES", "code": "096600 Terrazzo", "company": "THE VERDE TERRAZZO CORP.", "active": true, "contact": "Jose Elvira", "phone": "1 909 225 4591", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["096600 Terrazzo"]}, {"id": "m0609", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071010 Waterproofing", "company": "THOME WATERPROOFING", "active": true, "contact": "", "phone": "(818) 899-1234", "cell": "", "statusNote": "NEW", "comments": "", "email": "info@thomewaterproofing.com", "bids": {}, "codes": ["071010 Waterproofing"]}, {"id": "m0610", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "THRIFTY TREE SERVICE", "active": true, "contact": "Dave Aviram", "phone": "1 818 996 4577", "cell": "1 310 652 7723", "statusNote": "specialized in trees", "comments": "wrong mail, different scope", "email": "dave@thriftytreeservice.com", "bids": {}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0611", "div": "DIVISION 09", "divName": "FINISHES", "code": "074619 Steel Siding", "company": "TINCO SHEET METAL", "active": true, "contact": "Tony Argueta", "phone": "323.263.0511", "cell": "", "statusNote": "", "comments": "", "email": "estimating@tincosheetmetal.com", "bids": {}, "codes": ["074619 Steel Siding"]}, {"id": "m0612", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "TINKER GLASS (COMMERCIAL GLASS AND STOREFRONT)", "active": true, "contact": "http://tinkerglass.com/contact.html", "phone": "(909) 477-2651", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["058000 Glazing"]}, {"id": "m0613", "div": "DIVISION 09", "divName": "FINISHES", "code": "099000 Painting", "company": "TINT FACTORY", "active": true, "contact": "Frank Garrido", "phone": "1 310 815 1013", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["099000 Painting"]}, {"id": "m0614", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "072100 Insulation", "company": "TITAN INSULATION", "active": true, "contact": "", "phone": "(818) 647-9475", "cell": "", "statusNote": "NEW", "comments": "", "email": "gotitaninsulation@gmail.com", "bids": {}, "codes": ["072100 Insulation"]}, {"id": "m0615", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081000 Exterior Doors & Windows Supply", "company": "Titoni Window Systems Los Angeles", "active": true, "contact": "Niklas Neumann", "phone": "310.844.1199", "cell": "", "statusNote": "", "comments": "REPEATED", "email": "inquire@titoniwindows.com, niklas@titoniwindows.com", "bids": {"6537 Topanga Canyon": {"price": 50510.78, "received": "2026-02-10", "comments": ""}, "807 6th Ave": {"price": 262843.24, "received": "2025-10-15", "comments": "discount applied"}, "1080 El Medio Place": {"price": 277973.32, "received": "2025-10-22", "comments": "Check;"}, "1093 Palms Blvd": {"price": 67630.61, "received": "2025-12-01", "comments": ""}, "2429 Eastern Canal": {"price": 69983.19, "received": "2025-12-01", "comments": ""}, "16339 Akron": {"price": 108149.37, "received": "2025-12-30", "comments": "Supply"}}, "codes": ["081000 Exterior Doors & Windows Supply", "081001 Exterior Doors & Windows Installation"]}, {"id": "m0616", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "TJ BANNING CO., INC.", "active": true, "contact": "Kevin Uyemura", "phone": "1 310 831 2549", "cell": "1 310 800 5429", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["024000 Demolition", "030630 Concrete Slab"]}, {"id": "m0617", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "TORRANCE/ TRI-CITY", "active": true, "contact": "Ramon Martinez", "phone": "1 310 830 2410", "cell": "", "statusNote": "", "comments": "", "email": "ramonm@tricityglass.net", "bids": {"52-60 Market St": {"price": 32000.0, "received": "2025-05-28", "comments": ""}, "213 OFW Waterfront": {"price": 24064.0, "received": "2025-06-18", "comments": ""}, "748 & 750 Palisades Dr": {"price": 236850.0, "received": "2025-08-08", "comments": "SUPPLY AND INSTALL"}}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0618", "div": "DIVISION 05", "divName": "METALS", "code": "051200 Structural Steel", "company": "TORRES IRON WORKS", "active": true, "contact": "Noe Torres", "phone": "1 818 686 8908", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["051200 Structural Steel"]}, {"id": "m0619", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "329000 Planting, Landscaping", "company": "TREE PRESERVATION, INC.", "active": false, "contact": "David Sims", "phone": "1 626 441 4555", "cell": "1 818 416 6662", "statusNote": "", "comments": "", "email": "preservetrees@earthlink.net", "bids": {}, "codes": ["329000 Planting, Landscaping"]}, {"id": "m0620", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "TRI-CITY", "active": true, "contact": "Ramon Martinez", "phone": "1 310 830 2410", "cell": "", "statusNote": "", "comments": "", "email": "steveh@tricityglass.net, johnd@tricityglass.net", "bids": {}, "codes": ["058000 Glazing"]}, {"id": "m0621", "div": "DIVISION 03", "divName": "CONCRETE", "code": "031113 Shoring", "company": "TROYCO COX", "active": true, "contact": "admin@troyco.com", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "troy@troyco.com", "bids": {"807 6th Ave": {"price": 268434.0, "received": "2025-10-15", "comments": ""}}, "codes": ["031113 Shoring"]}, {"id": "m0622", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "072100 Insulation", "company": "Tru Team", "active": true, "contact": "Mike stone", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "mike.stone@truteam.com", "bids": {"17797 Camino De Yatasto": {"price": 18975.0, "received": "2025-09-22", "comments": ""}, "2429 Eastern Canal": {"price": 6975.0, "received": "2025-12-23", "comments": "CONTRACTOR SENT A BID FOR RAINGUTTER FOR $1.100"}, "16339 Akron": {"price": 4350.0, "received": "2025-12-30", "comments": "ADDITIONAL $2,650 BID FOR RAIN GUTTER"}, "12979 Blairwood Dr": {"price": 11975.0, "received": "2026-02-28", "comments": ""}}, "codes": ["072100 Insulation"]}, {"id": "m0623", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "TUDOR STONE & BRICKWORK", "active": true, "contact": "Paul King", "phone": "1 310 829 9733", "cell": "1 310 780 8780", "statusNote": "", "comments": "VOICE MAIL", "email": "info@tudorstoneandbrick.com", "bids": {}, "codes": ["030630 Concrete Slab"]}, {"id": "m0624", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081004 Garage Doors", "company": "TWO BROTHERS GARAGE DOOR & GATES", "active": true, "contact": "", "phone": "(818) 288-0853", "cell": "", "statusNote": "NEW", "comments": "", "email": "info@tbgaragedoor.com", "bids": {}, "codes": ["081004 Garage Doors"]}, {"id": "m0625", "div": "DIVISION 21", "divName": "FIRE SUPPRESSION", "code": "211300 Fire Spinklers", "company": "TYCO FIRE & SECURITY", "active": true, "contact": "Lois St. Bernard", "phone": "1 310 619 2131", "cell": "1 310 619 2209", "statusNote": "", "comments": "X", "email": "lstbernard@adt.com", "bids": {}, "codes": ["211300 Fire Spinklers"]}, {"id": "m0626", "div": "DIVISION 21", "divName": "FIRE SUPPRESSION", "code": "211300 Fire Spinklers", "company": "TYCOSIMPLEXGRINNELL", "active": true, "contact": "", "phone": "(562) 405-3800", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["211300 Fire Spinklers"]}, {"id": "m0627", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "T\u20109 ENTERPRISES", "active": true, "contact": "Demo/Grading/Earthwork", "phone": "909.392.0880", "cell": "909.392.0438", "statusNote": "DOESNT PICK UP", "comments": "", "email": "info@t9inc.com", "bids": {}, "codes": ["024000 Demolition"]}, {"id": "m0628", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "ULTIMATE", "active": true, "contact": "Fermin Miranda", "phone": "1 818 341 1061", "cell": "1 818 402 8785", "statusNote": "CALL", "comments": "", "email": "ultimatefermin@att.net", "bids": {}, "codes": ["220000 Plumbing Rough & Finish", "223200 Domestic Water Filtration Equipment", "334000 Stormwater management-LID"]}, {"id": "m0629", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "UNITED GLASS AND MIRROR", "active": true, "contact": "", "phone": "310318-0810", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["058000 Glazing"]}, {"id": "m0630", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "UNIVERSAL DEMOLITION", "active": true, "contact": "Jose Jimenez", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "jjudsinc@gmail.com", "bids": {}, "codes": ["024000 Demolition"]}, {"id": "m0631", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "VAN ZANDT ROOFING, INC.", "active": false, "contact": "Keith Van Zandt", "phone": "1 818 885 ROOF", "cell": "", "statusNote": "", "comments": "", "email": "vzroof@gmail.com", "bids": {}, "codes": ["071000 Roofing"]}, {"id": "m0632", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "262000 Low Voltage", "company": "VERTACORE", "active": true, "contact": "Dan Ryan", "phone": "1 310 698 0996", "cell": "1 310 910 8382", "statusNote": "", "comments": "", "email": "dan@vertacore.net", "bids": {}, "codes": ["262000 Low Voltage"]}, {"id": "m0633", "div": "DIVISION 09", "divName": "FINISHES", "code": "099000 Painting", "company": "VIA COLOR", "active": true, "contact": "Joe Hrebien", "phone": "1 562 695 9496", "cell": "1 562 818 2592", "statusNote": "", "comments": "", "email": "viacolor@dslextreme.com", "bids": {}, "codes": ["099000 Painting"]}, {"id": "m0634", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "Viewlux Windows & Doors", "active": true, "contact": "Liran Zorella", "phone": "323-818-1818", "cell": "", "statusNote": "", "comments": "NEW SUB", "email": "liran@viewluxwindows.com", "bids": {"748 & 750 Palisades Dr": {"price": 73282.33, "received": "2025-08-12", "comments": "Metal Railing with glass"}, "478 Wynola St": {"price": 28859.1, "received": "2025-08-22", "comments": ""}, "807 6th Ave": {"price": 168440.0, "received": "2025-10-10", "comments": ""}, "2429 Eastern Canal": {"price": 27709.09, "received": "2025-11-27", "comments": ""}, "1134 Iliff St": {"price": 47781.92, "received": "2026-04-07", "comments": "BID FOR EXTERIOR DOORS & WINDOWS"}}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0635", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "072100 Insulation", "company": "VIKING", "active": true, "contact": "Usama Amdad", "phone": "1 323 849 5991", "cell": "", "statusNote": "CALL", "comments": "", "email": "usama.amdad@vikinginsulation.com", "bids": {}, "codes": ["072100 Insulation"]}, {"id": "m0636", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "VIKING DEMOLITION CONTRACTORS", "active": true, "contact": "Phil Ayala", "phone": "1 818 500 9447", "cell": "", "statusNote": "Voice message", "comments": "New email address", "email": "vikingdemoinfo@gmail.com", "bids": {}, "codes": ["024000 Demolition"]}, {"id": "m0637", "div": "DIVISION 13", "divName": "SPECIAL CONSTRUCTION", "code": "131100 Swimming Pool/Spa/Fountain", "company": "VILLAGE POOLS", "active": false, "contact": "Duane Hanna", "phone": "1 805 969 0211", "cell": "", "statusNote": "", "comments": "", "email": "duane@villagepoolbuilders.com", "bids": {}, "codes": ["131100 Swimming Pool/Spa/Fountain"]}, {"id": "m0638", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "022600 Asbestos", "company": "VM3 ENVIROMENTAL(TESTING)", "active": true, "contact": "Udo Steinberger", "phone": "310-295-1099", "cell": "", "statusNote": "", "comments": "", "email": "udo@vm3enviro.com", "bids": {}, "codes": ["022600 Asbestos"]}, {"id": "m0639", "div": "DIVISION 09", "divName": "FINISHES", "code": "074619 Steel Siding", "company": "VMZINC", "active": false, "contact": "Bryan Ninnerman", "phone": "1 919 874 7173", "cell": "1 919 3492176", "statusNote": "", "comments": "BOUNCED BACK", "email": "bryan.ninnerman@am.umicore.com, bryan.ninneman@am.umicore.com", "bids": {}, "codes": ["074619 Steel Siding", "055000 Metal Fabricators"]}, {"id": "m0640", "div": "DIVISION 03", "divName": "CONCRETE", "code": "033100 Structural Concrete", "company": "WACONAH CONSTRUCTION", "active": true, "contact": "Chris Mulhern", "phone": "310 617-3563", "cell": "", "statusNote": "", "comments": "WON'T BID", "email": "chris@waconahconstruction.com", "bids": {"52-60 Market St": {"price": 98500.0, "received": "2025-04-06", "comments": ""}, "723 OFW": {"price": 1035575.0, "received": "28/05/2025", "comments": ""}, "1080 El Medio Place": {"price": 204750.0, "received": "2025-10-28", "comments": "Check;"}}, "codes": ["033100 Structural Concrete"]}, {"id": "m0641", "div": "DIVISION 13", "divName": "SPECIAL CONSTRUCTION", "code": "131100 Swimming Pool/Spa/Fountain", "company": "WALKER POOLS, INC.", "active": true, "contact": "Steve Walker", "phone": "1 805 520 0826", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["131100 Swimming Pool/Spa/Fountain"]}, {"id": "m0642", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "WALLOCK & MAGGIO, INC.", "active": false, "contact": "Chris Wallock", "phone": "1 805 499 5960", "cell": "1 805 432 0998", "statusNote": "", "comments": "", "email": "cwallock@wallockandmaggio.com", "bids": {}, "codes": ["030630 Concrete Slab"]}, {"id": "m0643", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "269900 Electric Fixtures", "company": "WALTERS (WHOLESALE ELECTRIC)", "active": true, "contact": "Jim Darling", "phone": "1 310 342 5730", "cell": "1 310 988 9881", "statusNote": "", "comments": "", "email": "jim.darling@walterswholesale.com", "bids": {}, "codes": ["269900 Electric Fixtures"]}, {"id": "m0644", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "WE POUR MUD", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "NO RESPONSE", "email": "wepourmud@sbcglobal.net", "bids": {}, "codes": ["030630 Concrete Slab"]}, {"id": "m0645", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "077700 Waterproofing Build. Wrap", "company": "WEATHER MASTERS", "active": true, "contact": "Ben Moghaddam", "phone": "1 310 312 1700", "cell": "1 818 788 7806", "statusNote": "WON'T BID WITH US ANYMORE", "comments": "They decline bidding now due to past unsuccessful proposals but appreciate the opportunity and hope to work together in the future.", "email": "ben@weathermasters.org", "bids": {}, "codes": ["077700 Waterproofing Build. Wrap", "071010 Waterproofing", "073313 Green Roof"]}, {"id": "m0646", "div": "DIVISION 02", "divName": "EXISTING CONDITIONS/SITE WORK", "code": "024000 Demolition", "company": "WEBER MADGWICK", "active": true, "contact": "Saul Oros", "phone": "1 661 775 1900", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["024000 Demolition", "312300 Excavation & Backfill", "334000 Stormwater management-LID"]}, {"id": "m0647", "div": "DIVISION 32", "divName": "EXTERIOR IMPROVEMENTS", "code": "323100 Fences & Gates", "company": "WEST COAST GATE", "active": true, "contact": "Gary Ovsiowitz", "phone": "1 310 445 5067", "cell": "1 310 210 4105", "statusNote": "", "comments": "", "email": "garyovs@gmail.com", "bids": {}, "codes": ["323100 Fences & Gates"]}, {"id": "m0648", "div": "DIVISION 03", "divName": "CONCRETE", "code": "030630 Concrete Slab", "company": "WEST COAST SAND & GRAVEL, INC.", "active": true, "contact": "Concrete/Concrete  Reinforcing", "phone": "800.522.0282", "cell": "714.522.4524", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["030630 Concrete Slab"]}, {"id": "m0649", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "262000 Low Voltage", "company": "WEST COAST TELECOM SERVICE", "active": true, "contact": "Louie Ruiz", "phone": "1 323 492 0045", "cell": "", "statusNote": "", "comments": "", "email": "louie.ruiz@wctservice.com", "bids": {}, "codes": ["262000 Low Voltage"]}, {"id": "m0650", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "260500 Electric Rough & Finish", "company": "WESTCO ELETRICAL CONTRACTORS", "active": true, "contact": "Jack Goldberg", "phone": "1 800 2 WESTCO", "cell": "", "statusNote": "", "comments": "", "email": "westco@westcoelectrical.com", "bids": {}, "codes": ["260500 Electric Rough & Finish"]}, {"id": "m0651", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "076000 Flashing & Sheet Metal", "company": "WESTECH CONTRACTORS, INC.", "active": true, "contact": "Ryan Hession", "phone": "1 805 569 1191", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["076000 Flashing & Sheet Metal"]}, {"id": "m0652", "div": "DIVISION 07", "divName": "THERMAL AND MOISTURE PROTECTION", "code": "071000 Roofing", "company": "WESTERN STATES", "active": true, "contact": "Shawn Reeves/ Gary", "phone": "1 818 718 0770", "cell": "1 818 416 0706", "statusNote": "", "comments": "", "email": "aroofguy1@gmail.com", "bids": {"748 & 750 Palisades Dr": {"price": 36500.0, "received": "2025-08-13", "comments": ""}, "478 Wynola St": {"price": 19335.0, "received": "2025-08-28", "comments": ""}}, "codes": ["071000 Roofing"]}, {"id": "m0653", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "WESTERN WINDOW SYSTEMS", "active": true, "contact": "Todd Hayhurst", "phone": "1 602 268 1300", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0654", "div": "DIVISION 10", "divName": "SPECIALTIES", "code": "103000 Fireplace", "company": "WESTFIRE - THE FIREPLACE PROS", "active": true, "contact": "Rod Thomas", "phone": "1 949 355 9590", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["103000 Fireplace"]}, {"id": "m0655", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "WESTSIDE DOOR & MOULDING", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "ONLY WINDOWS", "comments": "", "email": "", "bids": {"478 Wynola St": {"price": 48179.72, "received": null, "comments": "Only Windows"}}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0656", "div": "DIVISION 13", "divName": "SPECIAL CONSTRUCTION", "code": "131100 Swimming Pool/Spa/Fountain", "company": "WILLIAM BURKE", "active": true, "contact": "WILLIAM BURKE", "phone": "9163379620.0", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["131100 Swimming Pool/Spa/Fountain"]}, {"id": "m0657", "div": "DIVISION 10", "divName": "SPECIALTIES", "code": "103000 Fireplace", "company": "WILSHIRE FIREPLACE SHOPS", "active": true, "contact": "Michael Di Giorgio", "phone": "1 310 454 4444", "cell": "", "statusNote": "", "comments": "", "email": "wilshirefireplace@verizon.net", "bids": {}, "codes": ["103000 Fireplace"]}, {"id": "m0658", "div": "DIVISION 09", "divName": "FINISHES", "code": "096000 Tile - Installation", "company": "WILSHIRE TILE", "active": true, "contact": "", "phone": "323 9351269", "cell": "", "statusNote": "NEW", "comments": "WEB FORM", "email": "", "bids": {}, "codes": ["096000 Tile - Installation"]}, {"id": "m0659", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "WINDOW WORLD", "active": true, "contact": "Gene Bryan", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "gene@wwsocal.com", "bids": {"478 Wynola St": {"price": 5889.47, "received": "2025-08-26", "comments": ""}, "17797 Camino De Yatasto": {"price": 48238.69, "received": "2025-09-26", "comments": "(DOOR INST $12057.43) AND (WINDOW INST $36181.26)"}, "1080 El Medio Place": {"price": 370119.41, "received": "2025-10-24", "comments": "Check;"}, "1093 Palms Blvd": {"price": 69285.61, "received": "2025-11-25", "comments": ""}, "748 & 750 Palisades Dr": {"price": 63068.28, "received": "2025-08-12", "comments": ""}, "865 N Oreo Pl": {"price": 368436.88, "received": "2025-09-30", "comments": ""}, "807 6th Ave": {"price": 380709.96, "received": "2025-10-13", "comments": "garage: $15,163.30"}, "16339 Akron": {"price": 11955.53, "received": "2026-01-27", "comments": ""}}, "codes": ["081001 Exterior Doors & Windows Installation", "081000 Exterior Doors & Windows Supply", "081004 Garage Doors"]}, {"id": "m0660", "div": "DIVISION 08", "divName": "OPENINGS", "code": "081001 Exterior Doors & Windows Installation", "company": "WINDOWS + THINGS", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["081001 Exterior Doors & Windows Installation"]}, {"id": "m0661", "div": "DIVISION 09", "divName": "FINISHES", "code": "074623 Wood Siding", "company": "WJE SIDING", "active": true, "contact": "", "phone": "1 818 748 2324", "cell": "", "statusNote": "", "comments": "NEW SUB-INTERNET", "email": "wjesiding@gmail.com", "bids": {"17797 Camino De Yatasto": {"price": 46332.0, "received": "2025-11-18", "comments": ""}, "1080 El Medio Place": {"price": 296889.0, "received": "2025-11-20", "comments": "Check;"}, "15265 W Bestor Blvd": {"price": 183532.0, "received": "2025-11-18", "comments": ""}, "1093 Palms Blvd": {"price": 16896.0, "received": "2025-11-26", "comments": ""}}, "codes": ["074623 Wood Siding"]}, {"id": "m0662", "div": "DIVISION 05", "divName": "METALS", "code": "058000 Glazing", "company": "Wolf Glass", "active": false, "contact": "Moses", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "moe@wolfglassandmetals.com", "bids": {}, "codes": ["058000 Glazing"]}, {"id": "m0663", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "061000 Rough Carpentry", "company": "Wonk Construction Inc.", "active": true, "contact": "Sean Chi", "phone": "213-700-8660", "cell": "", "statusNote": "", "comments": "NO RESPONSE", "email": "sean@wonkconstruction.com", "bids": {}, "codes": ["061000 Rough Carpentry"]}, {"id": "m0664", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "WOODWORK AND WHATNOT", "active": true, "contact": "Jim Dowdell", "phone": "1 310 390 3698", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["064100 Cabinets"]}, {"id": "m0665", "div": "DIVISION 26", "divName": "ELECTRIC", "code": "250010 Security Systems", "company": "X-TECH", "active": true, "contact": "Tony Wakelin", "phone": "1 310 225 2614", "cell": "1 310 422 7778", "statusNote": "", "comments": "", "email": "awakelin@xtechsecurity.com", "bids": {}, "codes": ["250010 Security Systems"]}, {"id": "m0666", "div": "DIVISION 23", "divName": "HVAC", "code": "230000 Hvac", "company": "YANTZER BROTHERS AIR, INC.", "active": true, "contact": "Steve Yantzer", "phone": "1 818 865 2310", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["230000 Hvac"]}, {"id": "m0667", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "061000 Rough Carpentry", "company": "YORK CONSTRUCTION", "active": false, "contact": "", "phone": "1-805-520-1605", "cell": "", "statusNote": "", "comments": "", "email": "nyork@yorkconst.com", "bids": {}, "codes": ["061000 Rough Carpentry"]}, {"id": "m0668", "div": "DIVISION 09", "divName": "FINISHES", "code": "092000 Gypsum Board", "company": "ZAMORA DRYWALL", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "zamoradrywall@yahoo.com", "bids": {}, "codes": ["092000 Gypsum Board"]}, {"id": "m0669", "div": "DIVISION 22", "divName": "PLUMBING", "code": "220000 Plumbing Rough & Finish", "company": "ZION PLUMBING & ROOTING", "active": true, "contact": "Enrique Zion", "phone": "1 818 581 1148", "cell": "", "statusNote": "", "comments": "", "email": "", "bids": {}, "codes": ["220000 Plumbing Rough & Finish"]}, {"id": "m0670", "div": "DIVISION 06", "divName": "WOOD, PLASTICS, COMPOSITES", "code": "064100 Cabinets", "company": "ZORN PRODUCTIONS: MILLWORK/ CASEWORK/ COUNTERS", "active": true, "contact": "", "phone": "", "cell": "", "statusNote": "", "comments": "", "email": "info@zornpro.com", "bids": {}, "codes": ["064100 Cabinets"]}];
</script>
<script>
// ============================================================
// STATE
// ============================================================
let ST = {
  tab: 'projects',
  selProj: null, selSub: null,
  projQ: '', subQ: '', subCatF: '',
  subActiveOnly: false,
  projStatusFilter: 'all',
  overrides: {},     // {pid: {_status, _projName, [cat]: {set,sent,received,price,priceDate,comments,_na,_active}}}
  subOverrides: {},  // {sid: {active,statusNote,comments,bids:{key:{price,discPrice,date,comments,cat}}}}
  addedSubs: [],
  addedProjects: [],
  activityLog: [],
  // UI ephemeral
  dropdown: null,    // {type:'status'|'set', pid, cat?, x, y}
  bidsModal: null,   // {pid, cat}
  addProjModal: false,
  addSubModal: false,
  editSubModal: null,
  ovSelProj: null,      // selected project in overview
  editComments: null,   // {pid} currently editing
  editProjBox: null,    // {pid, box: 'received'|'due'|'bt'}
  editArchSet: null,    // pid currently editing architect set link
  editSubCodes: null,   // codes array during edit
  editSubDivFilter: '', // division filter in edit modal
  addSubDivFilter: '',  // division filter in add modal
  addSubSelCodes: [],   // selected codes in add modal
  followUp: {},         // {pid: {cat: {sentDates:[iso], followUps:{sid:true}}}}
  followUpSel: null,    // pid selected in follow-up tab
  followUpModal: null,  // {pid, cat} category detail modal
  followUpView: 'all',  // 'all' | 'followup'
};

// ============================================================
// STORAGE
// ============================================================
async function loadSt() {
  try {
    const r = await window.storage?.get('bf-v4-main');
    if (r?.value) {
      const d = JSON.parse(r.value);
      ST.overrides = d.overrides || {};
      ST.subOverrides = d.subOverrides || {};
      ST.addedSubs = d.addedSubs || [];
      ST.addedProjects = d.addedProjects || [];
      ST.activityLog = d.activityLog || [];
      ST.followUp = d.followUp || {};
    }
  } catch(e) {}
  render();
}

async function saveSt() {
  try {
    await window.storage?.set('bf-v4-main', JSON.stringify({
      overrides: ST.overrides,
      subOverrides: ST.subOverrides,
      addedSubs: ST.addedSubs,
      addedProjects: ST.addedProjects,
      activityLog: ST.activityLog,
      followUp: ST.followUp
    }));
  } catch(e) {}
}

// ============================================================
// HELPERS
// ============================================================
function fmt$(n) {
  if (!n && n !== 0) return '—';
  return '$' + Number(n).toLocaleString('en-US', {minimumFractionDigits:0,maximumFractionDigits:0});
}
function fmtDate(d) {
  if (!d) return '—';
  const dt = new Date(d);
  if (isNaN(dt)) return String(d);
  return dt.toLocaleDateString('en-US', {month:'short',day:'numeric',year:'2-digit'});
}
function nowISO() { return new Date().toISOString(); }
function esc(s) {
  if (!s) return '';
  return String(s).replace(/&/g,'&amp;').replace(/\x3c/g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;').replace(/'/g,'&#39;');
}

function allProjects() {
  return [
    ...PROJECTS_BASE.map(p => ({
      ...p,
      status: ST.overrides[p.id]?._status || p.status,
      name: ST.overrides[p.id]?._projName || p.name
    })),
    ...ST.addedProjects
  ];
}

function parseCell(s) {
  if (!s || s.length < 3) return {set:'-',sent:'-',received:'-'};
  return {set:s[0]==='P'?'P':s[0], sent:s[1]==='P'?'P':s[1], received:s[2]==='P'?'P':s[2]};
}

function isCatActive(pid, cat) {
  const ov = ST.overrides[pid]?.[cat] || {};
  if (ov._na) return false;
  if (ov._active) return true;
  const pidx = allProjects().findIndex(p => p.id === pid);
  if (pidx < 0) return false;
  const cell = CM[cat]?.[pidx] || '---';
  return cell !== '---';
}

function getCatSt(pid, cat) {
  const pidx = allProjects().findIndex(p => p.id === pid);
  if (pidx < 0) return {set:'-',sent:'-',received:'-'};
  const base = CM[cat] ? parseCell(CM[cat][pidx] || '---') : {set:'-',sent:'-',received:'-'};
  const ov = ST.overrides[pid]?.[cat] || {};
  return {
    set: ov.set !== undefined ? ov.set : base.set,
    sent: ov.sent !== undefined ? ov.sent : base.sent,
    received: ov.received !== undefined ? ov.received : base.received,
    price: ov.price, priceDate: ov.priceDate, comments: ov.comments
  };
}

function setProjOv(pid, cat, field, val) {
  if (!ST.overrides[pid]) ST.overrides[pid] = {};
  if (!ST.overrides[pid][cat]) ST.overrides[pid][cat] = {};
  ST.overrides[pid][cat][field] = val;
  saveSt();
}

function calcProjStats(pid) {
  let set=0,sent=0,rec=0,total=0,totalVal=0;
  CATS.forEach(cat => {
    if (!isCatActive(pid, cat)) return;
    const cs = getCatSt(pid, cat);
    total++;
    if (cs.set==='Y') set++;
    if (cs.sent==='Y') sent++;
    if (cs.received==='Y') { rec++; if (cs.price) totalVal+=Number(cs.price); }
  });
  return {set,sent,rec,total,totalVal};
}

function badgeHtml(status, pid) {
  const map = {
    'on-hold': ['badge-hold','ON HOLD'],
    'lost': ['badge-lost','LOST'],
    'active': ['badge-active','ACTIVE'],
    'sent': ['badge-sent','SENT'],
    'withdrawn': ['badge-withdrawn','WITHDRAWN'],
    'new': ['badge-new','NEW'],
  };
  const [cls, label] = map[status] || ['badge-hold', status.toUpperCase()];
  const click = pid ? `onclick="openStatusDD(event,'${pid}')"` : '';
  return `<span class="badge ${cls}${pid?' clickable':''}" ${click} title="${pid?'Click to change status':''}">${label}${pid?' ▾':''}</span>`;
}

function togClass(val, type) {
  if (val==='Y') { if (type==='set') return 'tog set'; if (type==='sent') return 'tog sent'; return 'tog recv'; }
  if (val==='N') return 'tog no';
  if (val==='P') return 'tog pend';
  return 'tog';
}
function togLabel(val, type) {
  const base = type==='set'?'SET':type==='sent'?'SENT':'RECV';
  const ico = val==='Y'?'✓ ':val==='N'?'✗ ':val==='P'?'~ ':'';
  return ico+base;
}

function allSubs() {
  const merge = s => {
    const ov = ST.subOverrides[s.id] || {};
    return {...s,
      company: ov.company !== undefined ? ov.company : s.company,
      contact: ov.contact !== undefined ? ov.contact : s.contact,
      phone: ov.phone !== undefined ? ov.phone : s.phone,
      cell: ov.cell !== undefined ? ov.cell : s.cell,
      email: ov.email !== undefined ? ov.email : s.email,
      active: ov.active !== undefined ? ov.active : s.active,
      statusNote: ov.statusNote !== undefined ? ov.statusNote : s.statusNote,
      comments: ov.comments !== undefined ? ov.comments : s.comments,
      codes: ov.codes !== undefined ? ov.codes : (s.codes || (s.code ? [s.code] : [])),
      bids: {...(s.bids||{}), ...(ov.bids||{})}
    };
  };
  return [
    ...SUBS_BASE.map(merge),
    ...ST.addedSubs.map(merge)
  ];
}

// Helper: get all codes for a sub as array
function subCodes(s) {
  return s.codes || (s.code ? [s.code] : []);
}

// Get bids for a specific project+category across all subs
// key format in subOverrides.bids: "projName|catName"
function getBidsForProjCat(projName, cat) {
  const subs = allSubs();
  const results = [];
  subs.forEach(s => {
    const ov = ST.subOverrides[s.id]?.bids || {};
    const key = `${projName}|${cat}`;
    const bid = ov[key];
    if (bid?.price) {
      results.push({sub: s, bid});
    }
  });
  return results;
}

function addActivity(type, sub, proj, cat, price, oldPrice) {
  ST.activityLog.unshift({ts:nowISO(),type,sub,proj,cat,price:price?Number(price):null,oldPrice:oldPrice?Number(oldPrice):null});
  if (ST.activityLog.length > 500) ST.activityLog.pop();
}

// ============================================================
// RENDER
// ============================================================
function render() {
  document.getElementById('app').innerHTML = buildApp();
}

function buildApp() {
  const totalBids = ST.activityLog.filter(a=>a.type==='price').length;
  const recentBids = ST.activityLog.filter(a=>a.type==='price' && (Date.now()-new Date(a.ts))<86400000).length;
  return `
    <div class="app" onclick="handleOutsideClick(event)">
      <div class="topbar">
        <div class="logo">BREAK<span>FORM</span></div>
        <div class="logo-sep"></div>
        <span style="font-family:var(--mono);font-size:10px;color:var(--text3);letter-spacing:.06em">BIDDING MANAGER</span>
        <div class="tabs">
          <button class="tab${ST.tab==='projects'?' active':''}" onclick="setTab('projects')">Projects</button>
          <button class="tab${ST.tab==='subs'?' active':''}" onclick="setTab('subs')">Subcontractors</button>
          <button class="tab${ST.tab==='followup'?' active':''}" onclick="setTab('followup')">Follow-Up</button>
          <button class="tab${ST.tab==='overview'?' active':''}" onclick="setTab('overview')">Overview</button>
        </div>
        <div class="topbar-right">
          <div class="tb-badge">Bids today: <span>${recentBids}</span></div>
          <div class="tb-badge">Total: <span>${totalBids}</span></div>
        </div>
      </div>
      <div class="content">
        ${ST.tab==='projects' ? buildProjectsTab() :
          ST.tab==='subs' ? buildSubsTab() :
          ST.tab==='followup' ? buildFollowUpTab() :
          buildOverviewTab()}
      </div>
      ${ST.dropdown ? buildDropdown() : ''}
      ${ST.bidsModal ? buildBidsModal() : ''}
      ${ST.addProjModal ? buildAddProjModal() : ''}
      ${ST.addSubModal ? buildAddSubModal() : ''}
      ${ST.editSubModal ? buildEditSubModal() : ''}
      ${ST.followUpModal ? buildFollowUpModal() : ''}
    </div>`;
}

// ============================================================
// PROJECTS TAB
// ============================================================
function buildProjectsTab() {
  const q = ST.projQ.toLowerCase();
  const pf = ST.projStatusFilter;
  const projs = allProjects();
  const filtered = projs.filter(p =>
    p.name.toLowerCase().includes(q) &&
    (pf==='all' || p.status===pf)
  );
  return `
    <div class="split">
      <div class="list-panel">
        <div class="search-wrap">
          <div class="search-box">
            <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/></svg>
            <input placeholder="Search project..." value="${esc(ST.projQ)}" oninput="ST.projQ=this.value;render()">
          </div>
        </div>
        <div class="filter-bar">
          ${['all','active','sent','on-hold','lost','withdrawn'].map(f =>
            `<div class="chip${ST.projStatusFilter===f?' on':''}" onclick="ST.projStatusFilter='${f}';render()">${f==='all'?'All':f.toUpperCase()}</div>`
          ).join('')}
        </div>
        <button class="add-btn" onclick="ST.addProjModal=true;render()">
          <svg width="11" height="11" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M12 5v14M5 12h14"/></svg>
          Add new project
        </button>
        <div class="sec-label">Projects (${filtered.length})</div>
        <div class="list-scroll">
          ${filtered.map(p => {
            const s = calcProjStats(p.id);
            const pct = s.total>0 ? Math.round(s.rec/s.total*100) : 0;
            return `<div class="proj-card${ST.selProj===p.id?' sel':''}" onclick="ST.selProj='${p.id}';render()">
              <div class="proj-name">${esc(p.name)}</div>
              <div class="proj-meta">
                ${badgeHtml(p.status)}
                ${p.dl?`<span class="meta-chip">DL: ${p.dl}</span>`:''}
                ${p.est?`<span class="meta-chip">${p.est}</span>`:''}
              </div>
              <div class="prog-track"><div class="prog-fill${pct===100?' done':''}" style="width:${pct}%"></div></div>
              <div class="prog-text">${s.rec}/${s.total} received • ${pct}%${s.totalVal>0?' • '+fmt$(s.totalVal):''}</div>
            </div>`;
          }).join('')}
        </div>
      </div>
      <div class="detail-panel">
        ${ST.selProj ? buildProjectDetail(allProjects().find(p=>p.id===ST.selProj)) : '<div class="empty">← Select a project</div>'}
      </div>
    </div>`;
}

function getLowestBidForCat(projName, cat) {
  // Returns {lowestEff, lowestOrig, lowestDisc, count} across all subs for this proj+cat
  const bids = getBidsForProjCat(projName, cat);
  if (!bids.length) return null;
  let lowestEff = Infinity, lowestOrig = null, lowestDisc = null;
  bids.forEach(({bid}) => {
    const eff = bid.discPrice && bid.discPrice < bid.price ? Number(bid.discPrice) : Number(bid.price);
    if (eff < lowestEff) {
      lowestEff = eff;
      lowestOrig = Number(bid.price);
      lowestDisc = bid.discPrice ? Number(bid.discPrice) : null;
    }
  });
  return {lowestEff, lowestOrig, lowestDisc, count: bids.length};
}

function getComments(p) {
  // Returns comments from overrides or base project
  return ST.overrides[p.id]?._comments !== undefined ? ST.overrides[p.id]._comments : (p.comments||'');
}
function getRfi(p) {
  return ST.overrides[p.id]?._rfi !== undefined ? ST.overrides[p.id]._rfi : (p.rfi||'');
}

function buildProjectDetail(p) {
  if (!p) return '<div class="empty">Project not found</div>';
  const s = calcProjStats(p.id);
  const pct = s.total>0 ? Math.round(s.rec/s.total*100) : 0;
  const activeCats = CATS.filter(cat => isCatActive(p.id, cat));
  const naCats = CATS.filter(cat => !isCatActive(p.id, cat));
  const comments = getComments(p);
  const rfi = getRfi(p);
  const isEditingComm = ST.editComments === p.id;

  // Calculate lowest-bid total
  let lowestTotal = 0;
  activeCats.forEach(cat => {
    const lb = getLowestBidForCat(p.name, cat);
    if (lb) lowestTotal += lb.lowestEff;
  });

  return `
    <div class="d-header">
      <div class="d-title">${esc(p.name)}</div>
      <div class="d-meta">
        ${badgeHtml(p.status, p.id)}
        ${p.dl?`<span class="meta-chip">Deadline: ${p.dl}</span>`:''}
        ${p.sdl?`<span class="meta-chip">Submittal: ${p.sdl}</span>`:''}
        ${p.est?`<span class="meta-chip">Estimator: ${p.est}</span>`:''}
        ${p.source?`<span class="meta-chip">${esc(p.source)}</span>`:''}
        ${p.builder?`<span class="meta-chip">Builder: ${p.builder}</span>`:''}
      </div>
    </div>
    <div class="stats-row">
      <div class="stat-box"><div class="stat-num blue">${s.set}</div><div class="stat-label">Set</div></div>
      <div class="stat-box"><div class="stat-num amber">${s.sent}</div><div class="stat-label">Sent</div></div>
      <div class="stat-box"><div class="stat-num green">${s.rec}</div><div class="stat-label">Received</div></div>
      <div class="stat-box"><div class="stat-num">${pct}%</div><div class="stat-label">Complete</div></div>
      ${lowestTotal>0?`<div class="stat-box" style="flex:2"><div class="stat-num green" style="font-size:14px">${fmt$(lowestTotal)}</div><div class="stat-label">Lowest Total</div></div>`:''}
    </div>

    ${buildArchSet(p)}

    ${buildProjBoxes(p)}

    <div style="padding:12px 20px 0;display:flex;gap:8px;align-items:center;flex-wrap:wrap">
      ${isEditingComm ? `
        <div style="flex:1;min-width:200px">
          <div style="font-family:var(--mono);font-size:9px;color:var(--text3);margin-bottom:4px">NOTES / COMMENTS</div>
          <textarea id="comm-inp" rows="2" style="width:100%;background:var(--bg2);border:1px solid var(--amber);border-radius:var(--r2);padding:7px 10px;font-size:12px;color:var(--text);resize:vertical;font-family:var(--sans);outline:none">${esc(comments)}</textarea>
        </div>
        <div style="flex:1;min-width:160px">
          <div style="font-family:var(--mono);font-size:9px;color:var(--text3);margin-bottom:4px">RFI</div>
          <input type="text" id="rfi-inp" value="${esc(rfi)}" style="width:100%;background:var(--bg2);border:1px solid var(--amber);border-radius:var(--r2);padding:7px 10px;font-size:12px;color:var(--text);font-family:var(--sans);outline:none">
        </div>
        <div style="display:flex;gap:6px;align-self:flex-end;padding-bottom:2px">
          <button class="btn btn-amber btn-sm" onclick="saveComments('${p.id}')">Save</button>
          <button class="btn btn-ghost btn-sm" onclick="ST.editComments=null;render()">Cancel</button>
        </div>
      ` : `
        <div style="flex:1">
          ${rfi?`<div class="rfi-box" style="margin-bottom:6px">⚑ RFI: ${esc(rfi)}</div>`:''}
          ${comments?`<div class="comment-box" style="margin-bottom:0">${esc(comments)}</div>`:
            `<div style="font-size:11px;color:var(--text3)">No notes yet</div>`}
        </div>
        <button class="edit-btn" onclick="ST.editComments='${p.id}';render()" style="align-self:flex-start">✎ Edit notes</button>
      `}
    </div>

    <div class="cats-section">
      <div class="sec-heading">Active Categories (${activeCats.length})</div>
      ${activeCats.map(cat => buildCatRow(p.id, p.name, cat)).join('')}
      ${naCats.length?`
        <div class="sec-heading" style="margin-top:16px">N/A — Click to activate (${naCats.length})</div>
        <div class="na-wrap">
          ${naCats.map(cat=>`<span class="na-tag" onclick="activateCat('${p.id}','${esc(cat)}')" title="Click to add to active categories">+ ${esc(cat)}</span>`).join('')}
        </div>`:''}
    </div>`;
}

function buildArchSet(p) {
  const ov = ST.overrides[p.id] || {};
  const link = ov._archSet || '';
  const editing = ST.editArchSet === p.id;
  // normalize link for display (strip https:// if present)
  const displayLink = link.replace(/^https?:\/\//,'').replace(/^www\./,'');
  const fullLink = link.match(/^https?:\/\//) ? link : (link ? 'https://'+link : '');

  if (editing) {
    return `<div class="arch-row">
      <div class="arch-set" style="border-color:var(--amber)">
        <div class="arch-set-label">🗂 Architect Set</div>
        <input type="url" class="arch-set-inp" id="arch-set-inp" value="${esc(link)}"
          placeholder="Paste Google Drive URL (or any link)..." autofocus
          onkeydown="if(event.key==='Enter')saveArchSet('${p.id}');if(event.key==='Escape'){ST.editArchSet=null;render()}">
        <button class="arch-set-btn primary" onclick="saveArchSet('${p.id}')">Save</button>
        <button class="arch-set-btn" onclick="ST.editArchSet=null;render()">✕</button>
      </div>
    </div>`;
  }

  if (link) {
    return `<div class="arch-row">
      <div class="arch-set has-link">
        <div class="arch-set-label">🗂 Architect Set</div>
        <a class="arch-set-link" href="${esc(fullLink)}" target="_blank" rel="noopener noreferrer" title="${esc(fullLink)}">${esc(displayLink)}</a>
        <button class="arch-set-btn primary" onclick="window.open('${esc(fullLink).replace(/'/g,"\\'")}','_blank','noopener')">Open →</button>
        <button class="arch-set-btn" onclick="ST.editArchSet='${p.id}';render()">✎ Edit</button>
      </div>
    </div>`;
  }

  return `<div class="arch-row">
    <div class="arch-set">
      <div class="arch-set-label">🗂 Architect Set</div>
      <div class="arch-set-empty">No link yet — add the Google Drive folder with plans</div>
      <button class="arch-set-btn" onclick="ST.editArchSet='${p.id}';render()">+ Add link</button>
    </div>
  </div>`;
}

function saveArchSet(pid) {
  const inp = document.getElementById('arch-set-inp');
  if (!inp) return;
  if (!ST.overrides[pid]) ST.overrides[pid] = {};
  const val = inp.value.trim();
  ST.overrides[pid]._archSet = val;
  saveSt();
  ST.editArchSet = null;
  render();
}

function buildProjBoxes(p) {
  const ov = ST.overrides[p.id] || {};
  const receivedDate = ov._receivedDate || '';
  const dueDate = ov._dueDate || p.dl || '';
  const btPeople = ov._btPeople || [];
  const editBox = ST.editProjBox; // {pid, box: 'received'|'due'|'bt'}
  const editing = editBox?.pid === p.id;

  const recvEditing = editing && editBox.box === 'received';
  const dueEditing  = editing && editBox.box === 'due';
  const btEditing   = editing && editBox.box === 'bt';

  return `<div class="proj-boxes">
    <!-- BOX 1: Received Date -->
    <div class="proj-box${recvEditing?' editing':''}" onclick="${recvEditing?'':'openProjBox(event,\''+p.id+'\',\'received\')'}">
      <div class="pbox-label">Received Date</div>
      ${recvEditing ? `
        <input type="text" id="pbox-recv" class="minp" value="${esc(receivedDate)}" placeholder="e.g. Apr 30, 25" style="margin:0;font-size:12px;padding:5px 8px" onkeydown="if(event.key==='Enter')saveProjBox('${p.id}','received')" autofocus>
        <div style="display:flex;gap:4px;margin-top:6px">
          <button class="btn btn-amber btn-sm" onclick="saveProjBox('${p.id}','received')">Save</button>
          <button class="btn btn-ghost btn-sm" onclick="ST.editProjBox=null;render()">✕</button>
        </div>` :
        `<div class="pbox-val${!receivedDate?' empty':''}">${receivedDate || 'Click to set'}</div>`
      }
    </div>

    <!-- BOX 2: Due Date (highlighted) -->
    <div class="proj-box${dueEditing?' editing':''}" style="${dueEditing?'':'border-color:var(--amber-border);background:var(--amber-bg)'}" onclick="${dueEditing?'':'openProjBox(event,\''+p.id+'\',\'due\')'}">
      <div class="pbox-label" style="color:var(--amber)">Due Date</div>
      ${dueEditing ? `
        <input type="text" id="pbox-due" class="minp" value="${esc(dueDate)}" placeholder="e.g. 08/30/25" style="margin:0;font-size:13px;padding:5px 8px;border-color:var(--amber)" onkeydown="if(event.key==='Enter')saveProjBox('${p.id}','due')" autofocus>
        <div style="display:flex;gap:4px;margin-top:6px">
          <button class="btn btn-amber btn-sm" onclick="saveProjBox('${p.id}','due')">Save</button>
          <button class="btn btn-ghost btn-sm" onclick="ST.editProjBox=null;render()">✕</button>
        </div>` :
        `<div class="pbox-val dl${!dueDate?' empty':''}">${dueDate || 'Click to set'}</div>`
      }
    </div>

    <!-- BOX 3: Buildertrend people -->
    <div class="proj-box${btEditing?' editing':''}" onclick="${btEditing?'':'openProjBox(event,\''+p.id+'\',\'bt\')'}">
      <div class="pbox-label">Buildertrend</div>
      ${btPeople.length>0 ? `<div style="margin-bottom:4px;flex-wrap:wrap;display:flex">${btPeople.map((name,i)=>`<span class="bt-chip">${esc(name)}<button onclick="event.stopPropagation();removeBTPerson('${p.id}',${i})" title="Remove">✕</button></span>`).join('')}</div>` : ''}
      ${btEditing ? `
        <div onclick="event.stopPropagation()">
          <input type="text" id="pbox-bt" class="minp" placeholder="Add person name..." style="margin:0;font-size:12px;padding:5px 8px" onkeydown="if(event.key==='Enter')addBTPerson('${p.id}')" autofocus>
          <div style="display:flex;gap:4px;margin-top:6px">
            <button class="btn btn-amber btn-sm" onclick="event.stopPropagation();addBTPerson('${p.id}')">+ Add</button>
            <button class="btn btn-ghost btn-sm" onclick="event.stopPropagation();ST.editProjBox=null;render()">Done</button>
          </div>
        </div>` :
        `<div class="pbox-val${!btPeople.length?' empty':''}">${btPeople.length ? '' : 'Click to add people'}</div>`
      }
    </div>
  </div>`;
}


function buildCatRow(pid, projName, cat) {
  const cs = getCatSt(pid, cat);
  const bidsForCat = getBidsForProjCat(projName, cat);
  const hasBids = bidsForCat.length > 0;
  // Lowest effective price
  const lb = getLowestBidForCat(projName, cat);
  const recvClass = hasBids ? 'tog has-bids' : togClass(cs.received,'received');
  const recvLabel = hasBids ? `👁 RECV (${bidsForCat.length})` : togLabel(cs.received,'received');

  return `<div class="cat-row">
    <div class="cat-name">${esc(cat)}</div>
    <div class="tog-group">
      <div class="${togClass(cs.set,'set')} tog-set-btn" data-pid="${pid}" data-cat="${esc(cat)}"
           onclick="openSetDD(event,'${pid}','${esc(cat)}')" title="Click for options">
        ${togLabel(cs.set,'set')} ▾
      </div>
      <div class="${togClass(cs.sent,'sent')}" onclick="togCat('${pid}','${esc(cat)}','sent')">${togLabel(cs.sent,'sent')}</div>
      <div class="${recvClass}" onclick="openBidsModal('${pid}','${esc(projName)}','${esc(cat)}')" title="View submitted bids">${recvLabel}</div>
    </div>
    ${lb ? buildLowestBidTag(lb) : (cs.price ? `<span class="price-tag">${fmt$(cs.price)}</span>` : '')}
  </div>`;
}

function buildLowestBidTag(lb) {
  const hasDisc = lb.lowestDisc && lb.lowestDisc < lb.lowestOrig;
  return `<span style="display:flex;align-items:baseline;gap:4px;margin-left:4px">
    <span style="font-family:var(--mono);font-size:12px;font-weight:700;color:var(--green)">${fmt$(lb.lowestEff)}</span>
    ${hasDisc?`<span style="font-family:var(--mono);font-size:9px;color:var(--text3);text-decoration:line-through">${fmt$(lb.lowestOrig)}</span>`:''}
    ${lb.count>1?`<span style="font-family:var(--mono);font-size:9px;color:var(--text3)">(${lb.count})</span>`:''}
  </span>`;
}

// ============================================================
// SUBS TAB
// ============================================================
function buildSubsTab() {
  const q = ST.subQ.toLowerCase();
  const cf = ST.subCatF;
  const subs = allSubs();
  const filtered = subs.filter(s => {
    const codes = subCodes(s);
    const matchQ = !q || s.company.toLowerCase().includes(q) ||
      codes.some(c=>c.toLowerCase().includes(q)) || (s.contact||'').toLowerCase().includes(q);
    const matchCat = !cf || codes.some(c=>c.toLowerCase().includes(cf.toLowerCase()));
    const matchActive = !ST.subActiveOnly || s.active;
    return matchQ && matchCat && matchActive;
  });
  const uniqueCodes = [...new Set(subs.flatMap(s=>subCodes(s)).filter(Boolean))].sort();

  return `
    <div class="split">
      <div class="list-panel">
        <div class="search-wrap">
          <div class="search-box">
            <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/></svg>
            <input placeholder="Company, category, contact..." value="${esc(ST.subQ)}" oninput="ST.subQ=this.value;render()">
          </div>
        </div>
        <div class="filter-bar">
          <div class="chip${ST.subActiveOnly?' on':''}" onclick="ST.subActiveOnly=!ST.subActiveOnly;render()">Active only</div>
          <select class="filter-select" onchange="ST.subCatF=this.value;render()">
            <option value="">All categories</option>
            ${uniqueCodes.map(c=>`<option value="${esc(c)}"${ST.subCatF===c?' selected':''}>${esc(c)}</option>`).join('')}
          </select>
        </div>
        <button class="add-btn" onclick="ST.addSubModal=true;render()">
          <svg width="11" height="11" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><path d="M12 5v14M5 12h14"/></svg>
          Add subcontractor
        </button>
        <div class="sec-label">Subcontractors (${filtered.length})</div>
        <div class="list-scroll">
          ${filtered.map(s => {
            const codes = subCodes(s);
            const ov = ST.subOverrides[s.id]?.bids || {};
            const bidCount = Object.keys(ov).filter(k=>ov[k]?.price).length + Object.keys(s.bids||{}).filter(k=>(s.bids||{})[k]?.price && !ov[k]).length;
            return `<div class="sub-card${ST.selSub===s.id?' sel':''}${!s.active?' inactive':''}" onclick="ST.selSub='${s.id}';render()">
              <div class="sub-head">
                <div class="status-dot ${s.active?'on':'off'}"></div>
                <div class="sub-name">${esc(s.company)}</div>
              </div>
              <div class="sub-code">${esc(codes.slice(0,2).join(' · '))}${codes.length>2?` +${codes.length-2}`:''}</div>
              ${s.contact?`<div class="sub-contact">${esc(s.contact)}</div>`:''}
              ${s.statusNote?`<div style="font-family:var(--mono);font-size:9px;color:var(--amber);margin-top:2px">${esc(s.statusNote)}</div>`:''}
              ${bidCount>0?`<div class="bid-dots">${Array(Math.min(bidCount,8)).fill('<div class="bid-dot"></div>').join('')}<span style="font-family:var(--mono);font-size:9px;color:var(--amber);margin-left:3px">${bidCount} bid${bidCount>1?'s':''}</span></div>`:''}
            </div>`;
          }).join('')}
          ${filtered.length===0?'<div class="empty">No results</div>':''}
        </div>
      </div>
      <div class="detail-panel">
        ${ST.selSub ? buildSubDetail(allSubs().find(s=>s.id===ST.selSub)) : '<div class="empty">← Select a subcontractor</div>'}
      </div>
    </div>`;
}

function buildSubDetail(sub) {
  if (!sub) return '<div class="empty">Not found</div>';
  const ov = ST.subOverrides[sub.id]?.bids || {};
  const bidEntries = Object.entries(ov).filter(([k,v])=>v?.price).sort((a,b)=> new Date(b[1].date||0)-new Date(a[1].date||0));
  const projs = allProjects();

  return `
    <div class="d-header">
      <div style="display:flex;align-items:flex-start;gap:12px">
        <div style="width:38px;height:38px;border-radius:50%;background:var(--bg3);border:1px solid var(--border2);display:flex;align-items:center;justify-content:center;font-family:var(--mono);font-size:14px;font-weight:600;color:var(--amber);flex-shrink:0">${sub.company.charAt(0)}</div>
        <div style="flex:1">
          <div class="d-title">${esc(sub.company)}</div>
          <div class="d-meta">
            ${sub.active?`<span class="badge badge-active">ACTIVE</span>`:`<span class="badge badge-lost">INACTIVE</span>`}
          </div>
        </div>
        <button class="edit-btn" onclick="ST.editSubModal='${sub.id}';render()">✎ Edit</button>
      </div>
      <!-- All divisions this company appears in -->
      <div style="display:flex;flex-wrap:wrap;gap:4px;margin-top:8px">
        ${subCodes(sub).map((c,i)=>`
          <span style="font-family:var(--mono);font-size:9px;background:var(--bg2);border:1px solid var(--border);padding:2px 8px;border-radius:10px;color:${i===0?'var(--amber)':'var(--text3)'}">${esc(c)}</span>
        `).join('')}
      </div>
    </div>
    ${sub.statusNote?`<div style="padding:10px 20px 0"><div style="background:var(--amber-bg);border:1px solid var(--amber-border);border-radius:var(--r2);padding:7px 12px;font-family:var(--mono);font-size:11px;color:var(--amber)">${esc(sub.statusNote)}</div></div>`:''}
    ${sub.comments?`<div style="padding:10px 20px 0"><div class="comment-box">${esc(sub.comments)}</div></div>`:''}
    <div class="sub-info-grid">
      ${sub.contact?`<div class="info-block"><div class="info-label">Contact</div><div class="info-val">${esc(sub.contact)}</div></div>`:''}
      ${sub.email?`<div class="info-block"><div class="info-label">Email</div><div class="info-val"><a href="mailto:${sub.email}">${esc(sub.email)}</a></div></div>`:''}
      ${sub.phone?`<div class="info-block"><div class="info-label">Phone</div><div class="info-val"><a href="tel:${sub.phone}">${esc(sub.phone)}</a></div></div>`:''}
      ${sub.cell?`<div class="info-block"><div class="info-label">Cell</div><div class="info-val"><a href="tel:${sub.cell}">${esc(sub.cell)}</a></div></div>`:''}
    </div>

    <div class="bids-section">
      <div style="font-family:var(--mono);font-size:9px;font-weight:600;letter-spacing:.12em;color:var(--text3);text-transform:uppercase;margin-bottom:12px">Bids History (${bidEntries.length})</div>
      ${bidEntries.length>0?`
        <div class="proj-bids-grid">
          ${bidEntries.map(([key, bid]) => {
            const [projName, catName] = key.split('|');
            const hasDisc = bid.discPrice && Number(bid.discPrice) < Number(bid.price);
            return `<div class="proj-bid-card">
              <div class="proj-bid-name">${esc(projName||key)}</div>
              ${catName?`<div class="proj-bid-cat">${esc(catName)}</div>`:''}
              <div class="proj-bid-prices">
                <span class="proj-bid-price">${fmt$(hasDisc ? bid.discPrice : bid.price)}</span>
                ${hasDisc?`<span class="proj-bid-original">${fmt$(bid.price)}</span><span class="disc-badge">-${Math.round((1-bid.discPrice/bid.price)*100)}%</span>`:''}
              </div>
              <div class="proj-bid-date">Updated: ${fmtDate(bid.date)}</div>
              ${bid.comments?`<div style="font-size:11px;color:var(--text3);margin-top:4px">${esc(bid.comments)}</div>`:''}
              <div class="proj-bid-actions">
                <button class="edit-btn" onclick="editSubBid('${sub.id}','${esc(key)}')">✎ Edit</button>
                <button class="edit-btn" style="color:var(--red);border-color:var(--red-border)" onclick="deleteSubBid('${sub.id}','${esc(key)}')">✕</button>
              </div>
            </div>`;
          }).join('')}
        </div>
      `:`<div style="color:var(--text3);font-family:var(--mono);font-size:11px;padding:8px 0 16px">No bids recorded yet</div>`}

      <div style="font-family:var(--mono);font-size:9px;font-weight:600;letter-spacing:.12em;color:var(--text3);text-transform:uppercase;margin:16px 0 10px">Add New Bid</div>
      <div style="background:var(--bg1);border:1px solid var(--border);border-radius:var(--r2);padding:14px">
        <div class="mrow" style="margin-bottom:0">
          <div>
            <div class="modal-label">Project (Active only) *</div>
            <select class="msel" id="bid-proj-sel" style="margin-bottom:8px">
              <option value="">Select project...</option>
              ${projs.filter(p=>p.status==='active').map(p=>`<option value="${esc(p.name)}">${esc(p.name)}</option>`).join('')}
            </select>
          </div>
          <div>
            <div class="modal-label">Category *</div>
            <select class="msel" id="bid-cat-sel" style="margin-bottom:8px">
              <option value="">Select category...</option>
              ${CATS.map(c=>`<option value="${esc(c)}">${esc(c)}</option>`).join('')}
            </select>
          </div>
        </div>
        <div class="mrow">
          <div>
            <div class="modal-label">Original Price ($) *</div>
            <input type="number" class="minp" id="bid-price-inp" placeholder="e.g. 45000" style="margin-bottom:8px">
          </div>
          <div>
            <div class="modal-label">Discounted Price ($) <span style="color:var(--green)">optional</span></div>
            <input type="number" class="minp" id="bid-disc-inp" placeholder="e.g. 39000" style="margin-bottom:8px">
          </div>
        </div>
        <div class="modal-label">Comments</div>
        <input type="text" class="minp" id="bid-comm-inp" placeholder="e.g. includes materials, labor only..." style="margin-bottom:10px">
        <button class="btn btn-amber btn-sm" onclick="addSubBid('${sub.id}')">+ Add Bid</button>
      </div>

      <div style="font-family:var(--mono);font-size:9px;font-weight:600;letter-spacing:.12em;color:var(--text3);text-transform:uppercase;margin:20px 0 8px">Activity Log</div>
      ${buildSubActivityLog(sub.company)}
    </div>`;
}

function buildSubActivityLog(company) {
  const acts = ST.activityLog.filter(a=>a.sub===company).slice(0,15);
  if (!acts.length) return `<div style="color:var(--text3);font-family:var(--mono);font-size:11px">No activity recorded</div>`;
  return `<div class="activity-feed">
    ${acts.map(a=>`
      <div class="act-item">
        <div class="act-dot ${a.oldPrice?'upd':'new'}"></div>
        <div class="act-body">
          <div class="act-title">${esc(a.proj||'')} ${a.cat?'→ '+esc(a.cat):''}</div>
          <div class="act-sub">${a.oldPrice?`Updated: ${fmt$(a.oldPrice)} → ${fmt$(a.price)}`:`New bid: ${fmt$(a.price)}`}</div>
        </div>
        <div class="act-time">${fmtDate(a.ts)}</div>
        <div class="act-price">${fmt$(a.price)}</div>
      </div>`).join('')}
  </div>`;
}

// ============================================================
// ============================================================
// FOLLOW-UP TAB
// ============================================================
function buildFollowUpTab() {
  const activeProjects = allProjects().filter(p => p.status === 'active');
  const selPid = ST.followUpSel;
  const selProj = activeProjects.find(p => p.id === selPid) || null;

  return `
    <div class="split">
      <div class="list-panel" style="width:320px">
        <div style="padding:0 14px 6px">
          <div style="font-family:var(--mono);font-size:10px;color:var(--text3);text-transform:uppercase;letter-spacing:.08em;padding:10px 0 8px">Active Projects (${activeProjects.length})</div>
          ${activeProjects.length === 0 ? `<div class="fu-empty-state">No active projects</div>` :
            activeProjects.map(p => {
              const fuData = ST.followUp[p.id] || {};
              const totalSent = Object.values(fuData).reduce((n,c) => n + (c.sentDates?.length || 0), 0);
              const totalFu = Object.values(fuData).reduce((n,c) => n + Object.keys(c.followUps||{}).filter(k => c.followUps[k]).length, 0);
              return `<div class="fu-project-card${selPid===p.id?' sel':''}" onclick="ST.followUpSel='${p.id}';render()">
                <div style="font-size:13px;font-weight:500;color:${selPid===p.id?'var(--amber)':'var(--text)'};margin-bottom:4px">${esc(p.name)}</div>
                <div style="font-family:var(--mono);font-size:10px;color:var(--text3);display:flex;gap:8px">
                  ${totalSent > 0 ? `<span class="fu-sent-pill">${totalSent} sent</span>` : `<span>No emails sent</span>`}
                  ${totalFu > 0 ? `<span class="fu-followup-pill">${totalFu} follow-up</span>` : ''}
                </div>
              </div>`;
            }).join('')}
        </div>
      </div>
      <div class="detail-panel" style="padding:20px 24px">
        ${selProj ? buildFollowUpProjectDetail(selProj) : `
          <div class="fu-empty-state" style="padding:60px 20px;font-size:13px">
            ← Select an active project to view its categories
          </div>`}
      </div>
    </div>`;
}

function buildFollowUpProjectDetail(p) {
  const activeCats = CATS.filter(c => {
    const cs = getCatSt(p.id, c);
    return !(cs.set==='-' && cs.sent==='-' && cs.received==='-');
  });
  const fuData = ST.followUp[p.id] || {};

  return `
    <div style="margin-bottom:18px;padding-bottom:14px;border-bottom:1px solid var(--border)">
      <div style="font-size:17px;font-weight:600;color:var(--text);margin-bottom:4px">${esc(p.name)}</div>
      <div style="font-family:var(--mono);font-size:10px;color:var(--text3);letter-spacing:.04em">Follow-up tracking · ${activeCats.length} active ${activeCats.length===1?'category':'categories'}</div>
    </div>

    ${activeCats.length === 0 ? `<div class="fu-empty-state">No categories activated for this project yet. Go to Projects tab to set them up.</div>` : ''}

    ${activeCats.map(cat => {
      const d = fuData[cat] || {};
      const sentDates = d.sentDates || [];
      const followUps = d.followUps || {};
      const followUpCount = Object.keys(followUps).filter(k => followUps[k]).length;
      const subs = getSubsForCategory(cat);
      const lastSent = sentDates.length ? sentDates[sentDates.length - 1] : null;
      return `<div class="fu-cat-row" onclick="openFollowUpModal('${p.id}','${esc(cat).replace(/'/g,"\\'")}')">
        <div class="fu-cat-name">${esc(cat)}</div>
        <div class="fu-cat-meta">
          <span>${subs.length} sub${subs.length===1?'':'s'}</span>
          ${sentDates.length ? `<span class="fu-sent-pill">${sentDates.length} sent · ${fmtDate(lastSent)}</span>` : `<span style="color:var(--text3)">Not sent</span>`}
          ${followUpCount > 0 ? `<span class="fu-followup-pill">${followUpCount} follow-up</span>` : ''}
          <button class="fu-view-btn" onclick="event.stopPropagation();openFollowUpModal('${p.id}','${esc(cat).replace(/'/g,"\\'")}')">View →</button>
        </div>
      </div>`;
    }).join('')}
  `;
}

function buildFollowUpModal() {
  const {pid, cat} = ST.followUpModal;
  const p = allProjects().find(x => x.id === pid);
  if (!p) return '';
  const fu = (ST.followUp[pid] && ST.followUp[pid][cat]) || {sentDates:[], followUps:{}};
  const subs = getSubsForCategory(cat);
  const view = ST.followUpView || 'all';

  // Filter subs based on view
  const filteredSubs = view === 'followup'
    ? subs.filter(s => fu.followUps && fu.followUps[s.id])
    : subs;

  // Collect all emails from filtered (or all with emails if "all" view) for BCC copy
  const subsForBcc = view === 'followup' ? filteredSubs : subs;
  const allEmails = subsForBcc
    .flatMap(s => parseEmails(s.email))
    .filter((e,i,a) => a.indexOf(e) === i);
  const bccText = allEmails.join(', ');

  const followUpCount = Object.keys(fu.followUps || {}).filter(k => fu.followUps[k]).length;

  return `<div class="backdrop" onclick="if(event.target===this)closeFollowUpModal()">
    <div class="modal modal-wide" style="max-width:720px;max-height:90vh;overflow-y:auto">
      <div style="display:flex;justify-content:space-between;align-items:flex-start;margin-bottom:6px">
        <div>
          <div class="modal-title">${esc(cat)}</div>
          <div class="modal-sub">${esc(p.name)}</div>
        </div>
        <button class="btn btn-ghost" style="padding:4px 10px" onclick="closeFollowUpModal()">✕</button>
      </div>

      ${fu.sentDates && fu.sentDates.length ? `
        <div class="fu-history">
          <strong>${fu.sentDates.length}</strong> email${fu.sentDates.length>1?'s':''} sent · last on <strong>${fmtDate(fu.sentDates[fu.sentDates.length-1])}</strong>
          ${fu.sentDates.length > 1 ? ` · history: ${fu.sentDates.map(d => fmtDate(d)).join(' · ')}` : ''}
        </div>
      ` : `<div class="fu-history" style="color:var(--text3)">No emails sent yet</div>`}

      <div style="font-family:var(--mono);font-size:10px;color:var(--text3);text-transform:uppercase;letter-spacing:.08em;margin-bottom:6px">BCC (${allEmails.length} email${allEmails.length===1?'':'s'}) — click to select, then copy</div>
      <div class="fu-bcc-box" onclick="selectBccText(this)">${allEmails.length ? esc(bccText) : '<span style="color:var(--text3);font-style:italic">No emails available in this view</span>'}</div>

      <div class="fu-action-row">
        <button class="btn btn-amber" onclick="copyFollowUpEmails('${pid}','${esc(cat).replace(/'/g,"\\'")}')" ${!allEmails.length?'disabled style="opacity:.4;cursor:not-allowed"':''}>📋 Copy ${allEmails.length} Email${allEmails.length===1?'':'s'}</button>
        <button class="btn" style="background:var(--green-bg);border:1px solid var(--green-border);color:var(--green);font-weight:600" onclick="markFollowUpSent('${pid}','${esc(cat).replace(/'/g,"\\'")}')">✉ Mark Email Sent — ${fmtDate(new Date().toISOString())}</button>
      </div>

      <div class="fu-view-tabs">
        <div class="fu-view-tab${view==='all'?' on':''}" onclick="ST.followUpView='all';render()">ALL SUBS (${subs.length})</div>
        <div class="fu-view-tab${view==='followup'?' on':''}" onclick="ST.followUpView='followup';render()">FOLLOW-UP ONLY (${followUpCount})</div>
      </div>

      ${filteredSubs.length === 0 ? `<div class="fu-empty-state">${view==='followup'?'No subs flagged for follow-up yet':'No subcontractors match this category'}</div>` :
        filteredSubs.map(s => {
          const isFu = !!(fu.followUps && fu.followUps[s.id]);
          const emails = parseEmails(s.email);
          return `<div class="fu-sub-row">
            <div class="fu-sub-info">
              <div class="fu-sub-name">${esc(s.company)}</div>
              ${emails.length ? `<div class="fu-sub-emails">${emails.map(e=>esc(e)).join(', ')}</div>` : `<div class="fu-sub-noemail">⚠ No email on file</div>`}
            </div>
            <button class="fu-toggle${isFu?' on':''}" onclick="toggleFollowUp('${pid}','${esc(cat).replace(/'/g,"\\'")}','${s.id}')">
              ${isFu ? '✓ FOLLOW-UP' : 'FOLLOW-UP'}
            </button>
          </div>`;
        }).join('')
      }
    </div>
  </div>`;
}

function openFollowUpModal(pid, cat) {
  ST.followUpModal = {pid, cat};
  ST.followUpView = 'all';
  render();
}

function closeFollowUpModal() {
  ST.followUpModal = null;
  render();
}

function ensureFollowUpPath(pid, cat) {
  if (!ST.followUp[pid]) ST.followUp[pid] = {};
  if (!ST.followUp[pid][cat]) ST.followUp[pid][cat] = {sentDates:[], followUps:{}};
}

function markFollowUpSent(pid, cat) {
  ensureFollowUpPath(pid, cat);
  ST.followUp[pid][cat].sentDates.push(new Date().toISOString());
  saveSt();
  render();
}

function toggleFollowUp(pid, cat, sid) {
  ensureFollowUpPath(pid, cat);
  const f = ST.followUp[pid][cat].followUps;
  if (f[sid]) delete f[sid];
  else f[sid] = true;
  saveSt();
  render();
}

async function copyFollowUpEmails(pid, cat) {
  const subs = getSubsForCategory(cat);
  const view = ST.followUpView || 'all';
  const fu = (ST.followUp[pid] && ST.followUp[pid][cat]) || {followUps:{}};
  const subsToInclude = view === 'followup'
    ? subs.filter(s => fu.followUps && fu.followUps[s.id])
    : subs;
  const emails = subsToInclude
    .flatMap(s => parseEmails(s.email))
    .filter((e,i,a) => a.indexOf(e) === i);
  const text = emails.join(', ');
  try {
    await navigator.clipboard.writeText(text);
    // Brief visual feedback
    const btn = event?.target;
    if (btn) {
      const orig = btn.innerHTML;
      btn.innerHTML = '✓ Copied!';
      setTimeout(() => { btn.innerHTML = orig; }, 1500);
    }
  } catch(e) {
    alert('Copy failed. Manually select the BCC box and copy.');
  }
}

function selectBccText(el) {
  const range = document.createRange();
  range.selectNodeContents(el);
  const sel = window.getSelection();
  sel.removeAllRanges();
  sel.addRange(range);
}

// ============================================================
// OVERVIEW TAB
// ============================================================
function buildOverviewTab() {
  const subs = allSubs();
  const totalSubs = subs.length;
  const activeSubs = subs.filter(s=>s.active).length;
  const recent = ST.activityLog.slice(0,60);
  const selProjId = ST.ovSelProj;
  const selProj = selProjId ? allProjects().find(p=>p.id===selProjId) : null;

  // Compute bids/total for selected project
  let projBidsLogged = null, projLowestTotal = null, projBidDetails = [];
  if (selProj) {
    const activeCats = CATS.filter(cat => isCatActive(selProj.id, cat));
    projLowestTotal = 0;
    activeCats.forEach(cat => {
      const bids = getBidsForProjCat(selProj.name, cat);
      if (bids.length) {
        projBidsLogged = (projBidsLogged||0) + bids.length;
        const lb = getLowestBidForCat(selProj.name, cat);
        if (lb) { projLowestTotal += lb.lowestEff; projBidDetails.push({cat, lb, bids}); }
      }
    });
    if (!projBidsLogged) projBidsLogged = 0;
  }

  return `
    <div class="overview-panel">
      <div style="font-family:var(--mono);font-size:10px;font-weight:600;letter-spacing:.12em;color:var(--text3);text-transform:uppercase;margin-bottom:14px">Summary</div>
      <div class="overview-stats">
        <div class="ov-stat"><div class="ov-num" style="color:var(--green)">${activeSubs}</div><div class="ov-label">Active Subcontractors</div></div>
        <div class="ov-stat"><div class="ov-num" style="color:var(--blue)">${selProj ? (projBidsLogged||'0') : '—'}</div><div class="ov-label">Bids Logged${selProj?` · ${esc(selProj.name)}`:'  · select a project'}</div></div>
        <div class="ov-stat" style="grid-column:span 2"><div class="ov-num" style="color:var(--green);font-size:28px">${selProj && projLowestTotal ? fmt$(projLowestTotal) : '—'}</div><div class="ov-label">Lowest Total${selProj?' (sum of lowest bid per category)':' · click a project below'}</div></div>
      </div>

      ${selProj && projBidDetails.length ? `
        <div style="font-family:var(--mono);font-size:10px;font-weight:600;letter-spacing:.12em;color:var(--text3);text-transform:uppercase;margin-bottom:10px">${esc(selProj.name)} — Bid Breakdown</div>
        <div style="background:var(--bg1);border:1px solid var(--border);border-radius:var(--r2);overflow:hidden;margin-bottom:28px">
          <table style="width:100%;border-collapse:collapse">
            <thead><tr>
              <th style="text-align:left;font-family:var(--mono);font-size:10px;color:var(--text3);padding:12px 18px;border-bottom:1px solid var(--border);background:var(--bg2);letter-spacing:.08em">CATEGORY</th>
              <th style="text-align:right;font-family:var(--mono);font-size:10px;color:var(--text3);padding:12px 18px;border-bottom:1px solid var(--border);background:var(--bg2)">LOWEST BID</th>
              <th style="text-align:right;font-family:var(--mono);font-size:10px;color:var(--text3);padding:12px 18px;border-bottom:1px solid var(--border);background:var(--bg2)"># BIDS</th>
            </tr></thead>
            <tbody>
              ${projBidDetails.map(({cat,lb,bids})=>`
                <tr style="border-bottom:1px solid var(--border)">
                  <td style="font-size:13px;color:var(--text2);padding:10px 18px">${esc(cat)}<br><span style="font-family:var(--mono);font-size:10px;color:var(--text3)">${bids[0]?.sub?.company?esc(bids[0].sub.company):''}</span></td>
                  <td style="text-align:right;font-family:var(--mono);font-size:14px;font-weight:600;color:var(--green);padding:10px 18px">${fmt$(lb.lowestEff)}${lb.lowestDisc&&lb.lowestDisc<lb.lowestOrig?`<br><span style="font-size:10px;color:var(--text3);text-decoration:line-through">${fmt$(lb.lowestOrig)}</span>`:''}</td>
                  <td style="text-align:right;font-family:var(--mono);font-size:12px;color:var(--text3);padding:10px 18px">${bids.length}</td>
                </tr>`).join('')}
              <tr style="background:var(--bg2)">
                <td style="font-size:13px;font-weight:600;color:var(--text);padding:12px 18px">TOTAL</td>
                <td style="text-align:right;font-family:var(--mono);font-size:16px;font-weight:700;color:var(--green);padding:12px 18px">${fmt$(projLowestTotal)}</td>
                <td></td>
              </tr>
              ${selProj.comments||ST.overrides[selProj.id]?._comments ? `
                <tr><td colspan="3" style="padding:10px 18px;font-size:12px;color:var(--text3);border-top:1px solid var(--border)">${esc(getComments(selProj))}</td></tr>
              `:``}
            </tbody>
          </table>
        </div>
      `:selProj?`<div style="font-size:13px;color:var(--text3);margin-bottom:28px;font-family:var(--mono)">No bids entered yet for ${esc(selProj.name)}</div>`:''}

      <div style="font-family:var(--mono);font-size:10px;font-weight:600;letter-spacing:.12em;color:var(--text3);text-transform:uppercase;margin-bottom:12px">Projects — Click to see bids</div>
      <div class="ov-projects-grid">
        ${allProjects().map(p=>{
          const s = calcProjStats(p.id);
          const pct = s.total>0?Math.round(s.rec/s.total*100):0;
          const isSel = selProjId === p.id;
          return `<div class="ov-proj-card${isSel?' sel':''}" onclick="ST.ovSelProj='${p.id}';render()">
            <div style="display:flex;align-items:center;gap:8px;margin-bottom:8px">
              ${badgeHtml(p.status)}
              <span style="font-size:13px;font-weight:500;color:${isSel?'var(--amber)':'var(--text)'}">${esc(p.name)}</span>
            </div>
            <div class="prog-track" style="height:4px"><div class="prog-fill${pct===100?' done':''}" style="width:${pct}%"></div></div>
            <div style="font-family:var(--mono);font-size:10px;color:var(--text3);margin-top:6px">${s.rec}/${s.total} received • ${pct}%</div>
          </div>`;
        }).join('')}
      </div>
      <div style="font-family:var(--mono);font-size:10px;font-weight:600;letter-spacing:.12em;color:var(--text3);text-transform:uppercase;margin-bottom:12px">Recent Activity</div>
      ${recent.length?`
        <div class="activity-feed">
          ${recent.map(a=>`
            <div class="act-item">
              <div class="act-dot ${a.oldPrice?'upd':'new'}"></div>
              <div class="act-body">
                <div class="act-title">${esc(a.sub||'')} ${a.proj?'→ '+esc(a.proj):''}</div>
                <div class="act-sub">${esc(a.cat||'')} ${a.oldPrice?`· Updated ${fmt$(a.oldPrice)} → ${fmt$(a.price)}`:`· New bid: ${fmt$(a.price)}`}</div>
              </div>
              <div class="act-time">${fmtDate(a.ts)}</div>
              <div class="act-price">${fmt$(a.price)}</div>
            </div>`).join('')}
        </div>`:`<div class="empty">No activity recorded yet</div>`}
    </div>`;
}

// ============================================================
// DROPDOWN MENUS
// ============================================================
function buildDropdown() {
  const dd = ST.dropdown;
  if (dd.type === 'status') {
    const statuses = [
      {val:'active',label:'Active',cls:'dd-active'},
      {val:'sent',label:'Sent',cls:'dd-sent'},
      {val:'on-hold',label:'On Hold',cls:'dd-hold'},
      {val:'lost',label:'Lost',cls:'dd-lost'},
      {val:'withdrawn',label:'Withdrawn',cls:'dd-withdrawn'},
    ];
    return `<div class="dropdown-menu" id="dd-menu" style="position:fixed;top:${dd.y}px;left:${dd.x}px;z-index:300" onclick="event.stopPropagation()">
      <div style="font-family:var(--mono);font-size:9px;color:var(--text3);padding:4px 10px 6px;letter-spacing:.08em">CHANGE STATUS</div>
      ${statuses.map(s=>`<div class="dd-item ${s.cls}" onclick="setProjStatus('${dd.pid}','${s.val}')">
        <span>${s.label}</span>
      </div>`).join('')}
    </div>`;
  }
  if (dd.type === 'set') {
    const cs = getCatSt(dd.pid, dd.cat);
    return `<div class="dropdown-menu" id="dd-menu" style="position:fixed;top:${dd.y}px;left:${dd.x}px;z-index:300" onclick="event.stopPropagation()">
      <div style="font-family:var(--mono);font-size:9px;color:var(--text3);padding:4px 10px 6px;letter-spacing:.08em">SET OPTIONS</div>
      <div class="dd-item dd-set" onclick="setSetValue('${dd.pid}','${esc(dd.cat)}','Y')">✓ Marked as SET</div>
      <div class="dd-item dd-unset" onclick="setSetValue('${dd.pid}','${esc(dd.cat)}','N')">✗ Not Set</div>
      <div class="dd-item" onclick="setSetValue('${dd.pid}','${esc(dd.cat)}','-')">— Reset to default</div>
      <div class="dd-sep"></div>
      <div class="dd-item dd-na" onclick="moveCatToNA('${dd.pid}','${esc(dd.cat)}')">→ Move to N/A</div>
    </div>`;
  }
  return '';
}

// ============================================================
// BIDS VIEW MODAL
// ============================================================
function buildBidsModal() {
  const {pid, projName, cat} = ST.bidsModal;
  const bids = getBidsForProjCat(projName, cat);
  const cs = getCatSt(pid, cat);

  return `<div class="backdrop" onclick="if(event.target===this){ST.bidsModal=null;render()}">
    <div class="modal modal-wide">
      <div class="modal-title">${esc(cat)}</div>
      <div class="modal-sub">${esc(projName)} — ${bids.length} bid${bids.length!==1?'s':''} received</div>
      ${bids.length>0?`
        <div class="bids-view-list">
          ${bids.map(({sub,bid}) => {
            const hasDisc = bid.discPrice && Number(bid.discPrice) < Number(bid.price);
            const effPrice = hasDisc ? Number(bid.discPrice) : Number(bid.price);
            return `<div class="bv-item">
              <div class="bv-sub">
                <div class="bv-sub-name">${esc(sub.company)}</div>
                <div class="bv-sub-code">${esc(sub.code)}${sub.contact?' · '+esc(sub.contact):''}</div>
                ${bid.comments?`<div style="font-size:11px;color:var(--text3);margin-top:3px">${esc(bid.comments)}</div>`:''}
              </div>
              <div class="bv-prices">
                <div class="bv-price">${fmt$(effPrice)}</div>
                ${hasDisc?`<div class="bv-orig">${fmt$(bid.price)}</div>`:''}
                <div class="bv-date">${fmtDate(bid.date)}</div>
              </div>
            </div>`;
          }).join('')}
        </div>
        <div style="margin-top:12px;padding:10px 12px;background:var(--bg2);border-radius:var(--r2);border:1px solid var(--border)">
          <div style="font-family:var(--mono);font-size:9px;color:var(--text3);margin-bottom:4px">LOWEST BID</div>
          <div style="font-family:var(--mono);font-size:18px;font-weight:700;color:var(--green)">
            ${fmt$(Math.min(...bids.map(({bid})=>bid.discPrice||bid.price)))}
          </div>
        </div>`
      :`<div class="bv-empty">No bids for this category yet.<br>Add bids from the Subcontractors tab.</div>`}
      <div class="modal-btns">
        ${cs.received==='Y'?`<button class="btn btn-ghost" style="color:var(--red)" onclick="clearRecv('${pid}','${esc(cat)}')">Clear Received</button>`:''}
        ${bids.length>0?`<button class="btn btn-green btn-sm" onclick="markCatReceived('${pid}','${esc(cat)}')">✓ Mark Received</button>`:''}
        <button class="btn btn-ghost" onclick="ST.bidsModal=null;render()">Close</button>
      </div>
    </div>
  </div>`;
}

// ============================================================
// ADD PROJECT MODAL
// ============================================================
function buildAddProjModal() {
  return `<div class="backdrop" onclick="if(event.target===this){ST.addProjModal=false;render()}">
    <div class="modal">
      <div class="modal-title">Add New Project</div>
      <div class="modal-sub">Enter the project name — categories can be activated after</div>
      <div class="modal-label">Project Name *</div>
      <input type="text" class="modal-input" id="np-name" placeholder="e.g. 1234 Ocean Ave" autofocus
        onkeydown="if(event.key==='Enter')confirmAddProj()">
      <div class="modal-label">Status</div>
      <select class="msel" id="np-status">
        <option value="active">Active</option>
        <option value="sent">Sent</option>
        <option value="on-hold">On Hold</option>
        <option value="new">New</option>
      </select>
      <div class="modal-label">Deadline (optional)</div>
      <input type="text" class="minp" id="np-dl" placeholder="e.g. 08/30/25 or TBD">
      <div class="modal-btns">
        <button class="btn btn-ghost" onclick="ST.addProjModal=false;render()">Cancel</button>
        <button class="btn btn-amber" onclick="confirmAddProj()">Add Project</button>
      </div>
    </div>
  </div>`;
}

// ============================================================
// ADD/EDIT SUB MODALS
// ============================================================
function buildAddSubModal() {
  const selectedDiv = ST.addSubDivFilter || '';
  const codesForDiv = selectedDiv ? (DIV_CODES[selectedDiv] || []) : [];
  const selectedCodes = ST.addSubSelCodes || [];
  return `<div class="backdrop" onclick="if(event.target===this){ST.addSubModal=false;ST.addSubDivFilter='';ST.addSubSelCodes=[];render()}">
    <div class="modal modal-wide">
      <div class="modal-title">Add Subcontractor</div>
      <div class="modal-sub">New contractor to the database</div>
      <div class="mrow">
        <div><div class="modal-label">Company *</div><input type="text" class="minp" id="ns-company" placeholder="Company name"></div>
        <div><div class="modal-label">Contact</div><input type="text" class="minp" id="ns-contact" placeholder="Contact name"></div>
      </div>
      <div class="mrow">
        <div><div class="modal-label">Phone</div><input type="text" class="minp" id="ns-phone" placeholder="310-555-0000"></div>
        <div><div class="modal-label">Cell</div><input type="text" class="minp" id="ns-cell" placeholder="310-555-0000"></div>
      </div>
      <div class="modal-label">Email</div>
      <input type="email" class="minp" id="ns-email" placeholder="email@company.com">

      <!-- Cascading Division → Categories -->
      <div class="modal-label" style="margin-top:12px">Division → Categories</div>
      <div class="mrow" style="margin-bottom:8px">
        <div>
          <select class="msel" id="ns-div" onchange="ST.addSubDivFilter=this.value;render()">
            <option value="">Select Division...</option>
            ${Object.keys(DIV_CODES).sort().map(d=>`<option value="${d}"${d===selectedDiv?' selected':''}>${d}</option>`).join('')}
          </select>
        </div>
        <div>
          <select class="msel" id="ns-code-picker" ${!selectedDiv?'disabled':''} onchange="addSubSelectCode(this.value);this.value=''">
            <option value="">${selectedDiv?'Add category from '+selectedDiv+'...':'Select Division first'}</option>
            ${codesForDiv.filter(c=>!selectedCodes.includes(c)).map(c=>`<option value="${esc(c)}">${esc(c)}</option>`).join('')}
          </select>
        </div>
      </div>
      ${selectedCodes.length ? `<div style="display:flex;flex-wrap:wrap;gap:4px;margin-bottom:10px">
        ${selectedCodes.map(c=>`<span class="bt-chip" style="background:var(--amber-bg);color:var(--amber);border-color:var(--amber-border)">${esc(c)} <button onclick="addSubRemoveCode('${esc(c)}')">✕</button></span>`).join('')}
      </div>` : `<div style="font-size:11px;color:var(--text3);margin-bottom:10px;font-style:italic">Select a Division, then pick categories from the second dropdown</div>`}

      <div class="modal-label">Status Note</div>
      <select class="msel" id="ns-status" style="margin-bottom:10px">
        <option value="">— None —</option>
        ${['HIGHLY ACTIVE','NEW','CALL','WRONG PHONE','EMAIL UPDATED','DOESNT PICK UP','FRAMING TOO','ONLY WINDOWS','ONLY GLASS','ONLY MOSAICS','WON\'T BID','specialized in trees'].map(opt =>
          `<option value="${esc(opt)}">${esc(opt)}</option>`
        ).join('')}
      </select>

      <div class="modal-label">Comments</div>
      <input type="text" class="minp" id="ns-comments" placeholder="Additional notes">

      <div style="display:flex;align-items:center;gap:10px;margin:10px 0 14px">
        <label class="toggle">
          <input type="checkbox" id="ns-active" checked>
          <div class="toggle-track"></div>
          <div class="toggle-thumb"></div>
        </label>
        <span style="font-size:12px;color:var(--text2)" id="ns-active-lbl">Active</span>
      </div>

      <div class="modal-btns">
        <button class="btn btn-ghost" onclick="ST.addSubModal=false;ST.addSubDivFilter='';ST.addSubSelCodes=[];render()">Cancel</button>
        <button class="btn btn-amber" onclick="confirmAddSub()">Add Subcontractor</button>
      </div>
    </div>
  </div>`;
}

function addSubSelectCode(code) {
  if (!code) return;
  if (!ST.addSubSelCodes) ST.addSubSelCodes = [];
  if (!ST.addSubSelCodes.includes(code)) ST.addSubSelCodes.push(code);
  // Preserve typed values before re-render
  ST._nsCache = {
    company: document.getElementById('ns-company')?.value || '',
    contact: document.getElementById('ns-contact')?.value || '',
    phone: document.getElementById('ns-phone')?.value || '',
    cell: document.getElementById('ns-cell')?.value || '',
    email: document.getElementById('ns-email')?.value || '',
    status: document.getElementById('ns-status')?.value || '',
    comments: document.getElementById('ns-comments')?.value || '',
    active: document.getElementById('ns-active')?.checked ?? true,
  };
  render();
  setTimeout(restoreNSCache, 10);
}
function addSubRemoveCode(code) {
  ST.addSubSelCodes = (ST.addSubSelCodes||[]).filter(c=>c!==code);
  ST._nsCache = {
    company: document.getElementById('ns-company')?.value || '',
    contact: document.getElementById('ns-contact')?.value || '',
    phone: document.getElementById('ns-phone')?.value || '',
    cell: document.getElementById('ns-cell')?.value || '',
    email: document.getElementById('ns-email')?.value || '',
    status: document.getElementById('ns-status')?.value || '',
    comments: document.getElementById('ns-comments')?.value || '',
    active: document.getElementById('ns-active')?.checked ?? true,
  };
  render();
  setTimeout(restoreNSCache, 10);
}
function restoreNSCache() {
  if (!ST._nsCache) return;
  const c = ST._nsCache;
  const set = (id, val) => { const el = document.getElementById(id); if (el) el.value = val; };
  set('ns-company', c.company); set('ns-contact', c.contact);
  set('ns-phone', c.phone); set('ns-cell', c.cell); set('ns-email', c.email);
  set('ns-status', c.status); set('ns-comments', c.comments);
  const a = document.getElementById('ns-active'); if (a) a.checked = c.active;
  ST._nsCache = null;
}

function buildEditSubModal() {
  const sub = allSubs().find(s=>s.id===ST.editSubModal);
  if (!sub) return '';
  const currentCodes = (ST.editSubCodes !== null && ST.editSubCodes !== undefined)
    ? ST.editSubCodes
    : subCodes(sub);
  const selectedDiv = ST.editSubDivFilter || sub.div || '';
  const availableCodes = selectedDiv ? (DIV_CODES[selectedDiv] || []) : [];

  const predefinedNotes = ['HIGHLY ACTIVE','NEW','CALL','WRONG PHONE','EMAIL UPDATED','DOESNT PICK UP','FRAMING TOO','ONLY WINDOWS','ONLY GLASS','ONLY MOSAICS',"WON'T BID",'specialized in trees'];

  return `<div class="backdrop" onclick="if(event.target===this){ST.editSubModal=null;ST.editSubCodes=null;ST.editSubDivFilter='';render()}">
    <div class="modal modal-wide">
      <div class="modal-title">Edit: ${esc(sub.company)}</div>
      <div class="modal-sub">Update subcontractor details</div>
      <div class="mrow">
        <div><div class="modal-label">Company</div><input type="text" class="minp" id="es-company" value="${esc(sub.company)}"></div>
        <div><div class="modal-label">Contact</div><input type="text" class="minp" id="es-contact" value="${esc(sub.contact||'')}"></div>
      </div>
      <div class="mrow">
        <div><div class="modal-label">Phone</div><input type="text" class="minp" id="es-phone" value="${esc(sub.phone||'')}"></div>
        <div><div class="modal-label">Cell</div><input type="text" class="minp" id="es-cell" value="${esc(sub.cell||'')}"></div>
      </div>
      <div class="modal-label">Email</div>
      <input type="email" class="minp" id="es-email" value="${esc(sub.email||'')}">

      <!-- Cascading Division → Categories -->
      <div class="modal-label" style="margin-top:12px">Divisions & Categories</div>
      <div class="mrow" style="margin-bottom:8px">
        <div>
          <select class="msel" onchange="ST.editSubDivFilter=this.value;editSubCacheFields('${sub.id}');render()">
            <option value="">Select Division...</option>
            ${Object.keys(DIV_CODES).sort().map(d=>`<option value="${d}"${d===selectedDiv?' selected':''}>${d}</option>`).join('')}
          </select>
        </div>
        <div>
          <select class="msel" ${!selectedDiv?'disabled':''} onchange="editSubAddCode('${sub.id}',this.value);this.value=''">
            <option value="">${selectedDiv?'Add category from '+selectedDiv+'...':'Select Division first'}</option>
            ${availableCodes.filter(c=>!currentCodes.includes(c)).map(c=>`<option value="${esc(c)}">${esc(c)}</option>`).join('')}
          </select>
        </div>
      </div>
      <div style="display:flex;flex-wrap:wrap;gap:4px;margin-bottom:10px;min-height:24px">
        ${currentCodes.length?currentCodes.map(c=>`<span class="bt-chip" data-sub-code="${esc(c)}" style="background:var(--amber-bg);color:var(--amber);border-color:var(--amber-border)">${esc(c)} <button onclick="editSubRemoveCode('${sub.id}','${esc(c)}')">✕</button></span>`).join(''):`<span style="font-size:11px;color:var(--text3);font-style:italic">No categories assigned</span>`}
      </div>

      <div class="modal-label">Status Note</div>
      <select class="msel" id="es-status" style="margin-bottom:10px">
        <option value=""${!sub.statusNote?' selected':''}>— None —</option>
        ${predefinedNotes.map(opt =>
          `<option value="${esc(opt)}"${sub.statusNote===opt?' selected':''}>${esc(opt)}</option>`
        ).join('')}
        ${sub.statusNote && !predefinedNotes.includes(sub.statusNote) ?
          `<option value="${esc(sub.statusNote)}" selected>${esc(sub.statusNote)}</option>` : ''}
      </select>
      <div class="modal-label">Comments</div>
      <input type="text" class="minp" id="es-comments" value="${esc(sub.comments||'')}">
      <div style="display:flex;align-items:center;gap:10px;margin-bottom:14px">
        <label class="toggle">
          <input type="checkbox" id="es-active" ${sub.active?'checked':''}>
          <div class="toggle-track"></div>
          <div class="toggle-thumb"></div>
        </label>
        <span style="font-size:12px;color:var(--text2)">${sub.active?'Active':'Inactive'} — Toggle status</span>
      </div>
      <div class="modal-btns">
        <button class="btn btn-ghost" onclick="ST.editSubModal=null;ST.editSubCodes=null;ST.editSubDivFilter='';render()">Cancel</button>
        <button class="btn btn-amber" onclick="confirmEditSub('${sub.id}')">Save Changes</button>
      </div>
    </div>
  </div>`;
}

function editSubCacheFields(sid) {
  ST._esCache = {
    company: document.getElementById('es-company')?.value,
    contact: document.getElementById('es-contact')?.value,
    phone:   document.getElementById('es-phone')?.value,
    cell:    document.getElementById('es-cell')?.value,
    email:   document.getElementById('es-email')?.value,
    status:  document.getElementById('es-status')?.value,
    comments:document.getElementById('es-comments')?.value,
    active:  document.getElementById('es-active')?.checked,
  };
}
function editSubRestoreCache() {
  if (!ST._esCache) return;
  const c = ST._esCache;
  const set = (id,v)=>{const e=document.getElementById(id); if(e && v!==undefined) e.value=v;};
  set('es-company',c.company); set('es-contact',c.contact);
  set('es-phone',c.phone); set('es-cell',c.cell); set('es-email',c.email);
  set('es-status',c.status); set('es-comments',c.comments);
  const a=document.getElementById('es-active'); if(a && c.active!==undefined) a.checked=c.active;
  ST._esCache = null;
}
function editSubAddCode(sid, code) {
  if (!code) return;
  const sub = allSubs().find(s=>s.id===sid);
  const current = (ST.editSubCodes !== null && ST.editSubCodes !== undefined)
    ? ST.editSubCodes : subCodes(sub);
  if (!current.includes(code)) {
    ST.editSubCodes = [...current, code];
  }
  editSubCacheFields(sid);
  render();
  setTimeout(editSubRestoreCache, 10);
}
function editSubRemoveCode(sid, code) {
  const sub = allSubs().find(s=>s.id===sid);
  const current = (ST.editSubCodes !== null && ST.editSubCodes !== undefined)
    ? ST.editSubCodes : subCodes(sub);
  ST.editSubCodes = current.filter(c=>c!==code);
  editSubCacheFields(sid);
  render();
  setTimeout(editSubRestoreCache, 10);
}

// ============================================================
// ACTIONS
// ============================================================
const BOX_ID_MAP = {received:'recv', due:'due', bt:'bt'};
function openProjBox(e, pid, box) {
  e.stopPropagation();
  ST.editProjBox = {pid, box};
  render();
  setTimeout(()=>{ document.getElementById('pbox-'+BOX_ID_MAP[box])?.focus(); }, 30);
}

function saveProjBox(pid, box) {
  if (!ST.overrides[pid]) ST.overrides[pid] = {};
  const inp = document.getElementById('pbox-' + BOX_ID_MAP[box]);
  if (!inp) return;
  const key = box === 'received' ? '_receivedDate' : '_dueDate';
  ST.overrides[pid][key] = inp.value.trim();
  saveSt();
  ST.editProjBox = null;
  render();
}

function addBTPerson(pid) {
  const inp = document.getElementById('pbox-bt');
  const name = inp?.value?.trim();
  if (!name) return;
  if (!ST.overrides[pid]) ST.overrides[pid] = {};
  if (!ST.overrides[pid]._btPeople) ST.overrides[pid]._btPeople = [];
  if (!ST.overrides[pid]._btPeople.includes(name)) {
    ST.overrides[pid]._btPeople.push(name);
  }
  saveSt();
  if (inp) inp.value = '';
  render();
  setTimeout(()=>{ document.getElementById('pbox-bt')?.focus(); }, 30);
}

function removeBTPerson(pid, idx) {
  if (!ST.overrides[pid]?._btPeople) return;
  ST.overrides[pid]._btPeople.splice(idx, 1);
  saveSt();
  render();
}


function saveComments(pid) {
  if (!ST.overrides[pid]) ST.overrides[pid] = {};
  ST.overrides[pid]._rfi = document.getElementById('rfi-inp')?.value || '';
  saveSt();
  ST.editComments = null;
  render();
}

function setTab(t) { ST.dropdown=null; ST.tab=t; render(); }

function openStatusDD(e, pid) {
  e.stopPropagation();
  const rect = e.target.getBoundingClientRect();
  ST.dropdown = {type:'status', pid, x: rect.left, y: rect.bottom+4};
  render();
}

function openSetDD(e, pid, cat) {
  e.stopPropagation();
  const rect = e.target.getBoundingClientRect();
  ST.dropdown = {type:'set', pid, cat, x: rect.left, y: rect.bottom+4};
  render();
}

function setProjStatus(pid, status) {
  if (!ST.overrides[pid]) ST.overrides[pid] = {};
  ST.overrides[pid]._status = status;
  saveSt();
  ST.dropdown = null;
  render();
}

function setSetValue(pid, cat, val) {
  if (!ST.overrides[pid]) ST.overrides[pid] = {};
  if (!ST.overrides[pid][cat]) ST.overrides[pid][cat] = {};
  if (val === '-') {
    delete ST.overrides[pid][cat].set;
  } else {
    ST.overrides[pid][cat].set = val;
  }
  saveSt();
  ST.dropdown = null;
  render();
}

function moveCatToNA(pid, cat) {
  if (!ST.overrides[pid]) ST.overrides[pid] = {};
  if (!ST.overrides[pid][cat]) ST.overrides[pid][cat] = {};
  ST.overrides[pid][cat]._na = true;
  delete ST.overrides[pid][cat]._active;
  saveSt();
  ST.dropdown = null;
  render();
}

function activateCat(pid, cat) {
  if (!ST.overrides[pid]) ST.overrides[pid] = {};
  if (!ST.overrides[pid][cat]) ST.overrides[pid][cat] = {};
  ST.overrides[pid][cat]._active = true;
  delete ST.overrides[pid][cat]._na;
  // Set initial state
  if (!ST.overrides[pid][cat].set) ST.overrides[pid][cat].set = 'Y';
  saveSt();
  render();
}

function togCat(pid, cat, field) {
  const cs = getCatSt(pid, cat);
  const cur = cs[field];
  const next = cur==='Y'?'N':'Y';
  setProjOv(pid, cat, field, next);
  render();
}

function openBidsModal(pid, projName, cat) {
  ST.bidsModal = {pid, projName, cat};
  render();
}

function markCatReceived(pid, cat) {
  setProjOv(pid, cat, 'received', 'Y');
  ST.bidsModal = null;
  render();
}

function clearRecv(pid, cat) {
  setProjOv(pid, cat, 'received', 'N');
  ST.bidsModal = null;
  render();
}

function handleOutsideClick(e) {
  if (ST.dropdown && !e.target.closest('#dd-menu') && !e.target.closest('.tog-set-btn') && !e.target.closest('.badge.clickable')) {
    ST.dropdown = null;
    render();
  }
}

function confirmAddProj() {
  const name = document.getElementById('np-name')?.value?.trim();
  if (!name) return;
  const id = 'cp-' + Date.now();
  ST.addedProjects.push({
    id, name,
    status: document.getElementById('np-status')?.value || 'active',
    dl: document.getElementById('np-dl')?.value?.trim() || '',
    sdl: null, est: null, source: null, comments: '', rfi: '', builder: null
  });
  ST.selProj = id;
  saveSt();
  ST.addProjModal = false;
  render();
}

function confirmAddSub() {
  const company = document.getElementById('ns-company')?.value?.trim();
  if (!company) { alert('Enter company name'); return; }
  const codes = (ST.addSubSelCodes && ST.addSubSelCodes.length) ? ST.addSubSelCodes.slice() : [];
  const newSub = {
    id: 'cs-'+Date.now(),
    div: ST.addSubDivFilter || '',
    divName: '',
    code: codes[0] || '',
    codes,
    company,
    active: document.getElementById('ns-active')?.checked ?? true,
    contact: document.getElementById('ns-contact')?.value?.trim()||'',
    phone: document.getElementById('ns-phone')?.value?.trim()||'',
    cell: document.getElementById('ns-cell')?.value?.trim()||'',
    email: document.getElementById('ns-email')?.value?.trim()||'',
    statusNote: document.getElementById('ns-status')?.value?.trim()||'',
    comments: document.getElementById('ns-comments')?.value?.trim()||'',
    bids: {}
  };
  ST.addedSubs.push(newSub);
  ST.selSub = newSub.id;
  ST.addSubModal = false;
  ST.addSubDivFilter = '';
  ST.addSubSelCodes = [];
  saveSt();
  render();
}

function confirmEditSub(sid) {
  if (!ST.subOverrides[sid]) ST.subOverrides[sid] = {};
  const ov = ST.subOverrides[sid];
  const getVal = id => {
    const el = document.getElementById(id);
    return el ? el.value : '';
  };
  ov.company = getVal('es-company').trim();
  ov.contact = getVal('es-contact').trim();
  ov.phone   = getVal('es-phone').trim();
  ov.cell    = getVal('es-cell').trim();
  ov.email   = getVal('es-email').trim();
  ov.statusNote = getVal('es-status').trim(); // empty string clears the note
  ov.comments = getVal('es-comments').trim();
  ov.active = document.getElementById('es-active')?.checked ?? true;
  if (ST.editSubCodes !== null && ST.editSubCodes !== undefined) {
    ov.codes = ST.editSubCodes.slice();
  }
  saveSt();
  ST.editSubModal = null;
  ST.editSubCodes = null;
  ST.editSubDivFilter = '';
  render();
}

function addSubBid(sid) {
  const proj = document.getElementById('bid-proj-sel')?.value;
  const cat = document.getElementById('bid-cat-sel')?.value;
  const price = document.getElementById('bid-price-inp')?.value;
  const disc = document.getElementById('bid-disc-inp')?.value;
  const comm = document.getElementById('bid-comm-inp')?.value||'';
  if (!proj) { alert('Select a project'); return; }
  if (!price || Number(price)<=0) { alert('Enter a valid price'); return; }
  if (disc && Number(disc) >= Number(price)) { alert('Discounted price must be lower than original'); return; }

  if (!ST.subOverrides[sid]) ST.subOverrides[sid]={};
  if (!ST.subOverrides[sid].bids) ST.subOverrides[sid].bids={};

  // Key: projName|catName (cat optional for backward compat)
  const key = cat ? `${proj}|${cat}` : proj;
  const oldBid = ST.subOverrides[sid].bids[key];
  ST.subOverrides[sid].bids[key] = {
    price: Number(price),
    discPrice: disc && Number(disc)>0 ? Number(disc) : null,
    date: nowISO(),
    comments: comm,
    cat: cat||''
  };

  const sub = allSubs().find(s=>s.id===sid);
  addActivity('price', sub?.company||sid, proj, cat||'', Number(disc||price), oldBid?.price);
  saveSt();
  render();
}

function editSubBid(sid, key) {
  const ov = ST.subOverrides[sid]?.bids?.[key];
  if (!ov) return;
  const decodedKey = key;
  const [projName, catName] = decodedKey.split('|');
  const newPrice = prompt(`Edit price for:\n${decodedKey}\n\nOriginal: ${fmt$(ov.price)}\nDiscounted: ${ov.discPrice?fmt$(ov.discPrice):'none'}\n\nNew original price:`, ov.price);
  if (newPrice===null) return;
  const np = Number(newPrice);
  if (!np||np<=0) { alert('Invalid price'); return; }
  const newDisc = prompt(`Discounted price (leave blank for none):`, ov.discPrice||'');
  const nd = newDisc && Number(newDisc)>0 ? Number(newDisc) : null;
  if (nd && nd>=np) { alert('Discounted price must be lower than original'); return; }

  const oldPrice = ov.discPrice||ov.price;
  ST.subOverrides[sid].bids[key] = {...ov, price:np, discPrice:nd, date:nowISO()};

  const sub = allSubs().find(s=>s.id===sid);
  addActivity('price', sub?.company||sid, projName||key, catName||'', nd||np, oldPrice);
  saveSt();
  render();
}

function deleteSubBid(sid, key) {
  if (!confirm('Delete this bid?')) return;
  delete ST.subOverrides[sid]?.bids?.[key];
  saveSt();
  render();
}

loadSt();
</script>
</body>
</html>
