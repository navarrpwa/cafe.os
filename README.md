[cafe-manager (3).html](https://github.com/user-attachments/files/27452751/cafe-manager.3.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<meta name="theme-color" content="#f4f4f0"/>
<title>CaféOS — Café Management System</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:wght@400;500&family=Lato:wght@300;400;700&display=swap" rel="stylesheet"/>
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#f4f4f0;--surface:#ffffff;--surface2:#f0efe9;--surface3:#e8e7e0;
  --border:#e0ddd4;--border2:#ccc9be;
  --accent:#c47d1a;--accent2:#a8621a;--accent3:#e09930;
  --green:#2a9d4e;--red:#d94040;--blue:#2472c8;--purple:#6d4fc4;--pink:#c4306e;
  --text:#1a1714;--text2:#5a5448;--text3:#8c8474;
  --r:12px;--r2:8px;
  --shadow:0 2px 12px rgba(0,0,0,0.08);
  --shadow-lg:0 8px 32px rgba(0,0,0,0.12);
  --glow:0 0 20px rgba(196,125,26,0.15);
}
html,body{height:100%;overflow:hidden;background:var(--bg);color:var(--text);font-family:'Lato',sans-serif}
button{cursor:pointer;border:none;background:none;font-family:inherit;color:inherit}
input,select,textarea{font-family:inherit;color:inherit}
::-webkit-scrollbar{width:5px;height:5px}
::-webkit-scrollbar-track{background:transparent}
::-webkit-scrollbar-thumb{background:var(--border2);border-radius:3px}
::-webkit-scrollbar-track{background:var(--surface2)}
a{color:inherit;text-decoration:none}

/* ── Layout ──────────────────────────────────────────────── */
.app{display:flex;height:100vh;overflow:hidden}
.sidebar{width:220px;flex-shrink:0;background:var(--surface);border-right:1px solid var(--border);display:flex;flex-direction:column;overflow-y:auto}
.main{flex:1;display:flex;flex-direction:column;overflow:hidden}
.topbar{height:56px;flex-shrink:0;background:var(--surface);border-bottom:1px solid var(--border);display:flex;align-items:center;padding:0 24px;gap:16px}
.content{flex:1;overflow-y:auto;padding:24px}

/* ── Sidebar ─────────────────────────────────────────────── */
.sidebar-logo{padding:20px 16px 16px;border-bottom:1px solid var(--border)}
.logo-mark{font-family:'Syne',sans-serif;font-size:18px;font-weight:800;color:var(--accent);letter-spacing:-0.5px}
.logo-sub{font-size:11px;color:var(--text3);letter-spacing:2px;text-transform:uppercase;margin-top:2px}
.nav-section{padding:12px 8px 4px}
.nav-label{font-size:10px;font-weight:700;letter-spacing:2px;text-transform:uppercase;color:var(--text3);padding:0 8px;margin-bottom:4px}
.nav-item{display:flex;align-items:center;gap:10px;padding:9px 12px;border-radius:var(--r2);font-size:13px;font-weight:600;color:var(--text2);cursor:pointer;transition:all 0.15s;margin-bottom:1px;position:relative}
.nav-item:hover{background:var(--surface2);color:var(--text)}
.nav-item.active{background:rgba(196,125,26,0.10);color:var(--accent)}
.nav-item.active::before{content:'';position:absolute;left:0;top:50%;transform:translateY(-50%);width:3px;height:60%;background:var(--accent);border-radius:0 3px 3px 0}
.nav-icon{font-size:16px;width:20px;text-align:center;flex-shrink:0}
.nav-badge{margin-left:auto;background:var(--red);color:white;font-size:10px;font-weight:700;padding:2px 6px;border-radius:50px;min-width:18px;text-align:center}
.sidebar-bottom{margin-top:auto;padding:16px;border-top:1px solid var(--border)}
.cafe-name{font-family:'Syne',sans-serif;font-size:13px;font-weight:700;color:var(--text);margin-bottom:2px}
.cafe-sub{font-size:11px;color:var(--text3)}

/* ── Topbar ──────────────────────────────────────────────── */
.page-title{font-family:'Syne',sans-serif;font-size:18px;font-weight:700;flex:1}
.topbar-actions{display:flex;align-items:center;gap:8px}
.tb-btn{padding:7px 14px;border-radius:var(--r2);font-size:13px;font-weight:600;transition:all 0.15s}
.tb-btn.primary{background:var(--accent);color:#ffffff}
.tb-btn.primary:hover{background:var(--accent2)}
.tb-btn.ghost{border:1px solid var(--border2);color:var(--text2)}
.tb-btn.ghost:hover{border-color:var(--border2);background:var(--surface2);color:var(--text)}
.clock{font-family:'DM Mono',monospace;font-size:13px;color:var(--text2);background:var(--surface2);padding:6px 12px;border-radius:var(--r2)}

/* ── Cards ───────────────────────────────────────────────── */
.card{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);padding:20px}
.card-sm{padding:16px}
.kpi{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);padding:20px 24px;position:relative;overflow:hidden;transition:border-color 0.2s}
.kpi:hover{border-color:var(--border2)}
.kpi-glow{position:absolute;top:-30px;right:-30px;width:100px;height:100px;border-radius:50%;opacity:0.08;filter:blur(20px)}
.kpi-label{font-size:11px;font-weight:700;letter-spacing:1.5px;text-transform:uppercase;color:var(--text3);margin-bottom:10px}
.kpi-val{font-family:'Syne',sans-serif;font-size:28px;font-weight:800;color:var(--text);line-height:1}
.kpi-sub{font-size:12px;color:var(--text3);margin-top:6px}
.kpi-change{display:inline-flex;align-items:center;gap:4px;font-size:12px;font-weight:700;padding:2px 8px;border-radius:50px;margin-top:8px}
.kpi-up{background:rgba(42,157,78,0.10);color:var(--green)}
.kpi-down{background:rgba(217,64,64,0.10);color:var(--red)}

/* ── Grid helpers ────────────────────────────────────────── */
.grid2{display:grid;grid-template-columns:1fr 1fr;gap:16px}
.grid3{display:grid;grid-template-columns:repeat(3,1fr);gap:16px}
.grid4{display:grid;grid-template-columns:repeat(4,1fr);gap:16px}
.flex{display:flex}
.gap{gap:16px}
.gap-sm{gap:8px}
.between{justify-content:space-between;align-items:center}
.col{flex-direction:column}
.mt{margin-top:16px}
.mt2{margin-top:24px}
.mt-sm{margin-top:8px}
.mb{margin-bottom:16px}

/* ── Section header ──────────────────────────────────────── */
.sh{display:flex;align-items:center;justify-content:space-between;margin-bottom:16px}
.sh-title{font-family:'Syne',sans-serif;font-size:15px;font-weight:700;color:var(--text)}
.sh-action{font-size:12px;font-weight:600;color:var(--accent);cursor:pointer;padding:4px 10px;border-radius:var(--r2);transition:background 0.15s}
.sh-action:hover{background:rgba(245,166,35,0.1)}

/* ── Table ───────────────────────────────────────────────── */
.tbl{width:100%;border-collapse:collapse}
.tbl th{padding:10px 14px;text-align:left;font-size:10px;font-weight:700;letter-spacing:1.5px;text-transform:uppercase;color:var(--text3);border-bottom:1px solid var(--border);white-space:nowrap}
.tbl td{padding:12px 14px;font-size:13px;border-bottom:1px solid var(--border);vertical-align:middle}
.tbl tr:last-child td{border-bottom:none}
.tbl tr:hover td{background:rgba(255,255,255,0.02)}
.tbl-wrap{overflow-x:auto;border-radius:var(--r);border:1px solid var(--border);background:var(--surface)}

/* ── Badge / pill ────────────────────────────────────────── */
.badge{display:inline-flex;align-items:center;padding:3px 10px;border-radius:50px;font-size:11px;font-weight:700;letter-spacing:0.3px}
.badge-green{background:rgba(42,157,78,0.12);color:var(--green)}
.badge-red{background:rgba(217,64,64,0.12);color:var(--red)}
.badge-orange{background:rgba(196,125,26,0.12);color:var(--accent)}
.badge-blue{background:rgba(36,114,200,0.12);color:var(--blue)}
.badge-purple{background:rgba(109,79,196,0.12);color:var(--purple)}

/* ── Form elements ───────────────────────────────────────── */
.form-row{display:grid;gap:12px;margin-bottom:12px}
.form-row.cols2{grid-template-columns:1fr 1fr}
.form-row.cols3{grid-template-columns:1fr 1fr 1fr}
.form-group{display:flex;flex-direction:column;gap:6px}
.form-label{font-size:11px;font-weight:700;letter-spacing:1px;text-transform:uppercase;color:var(--text3)}
.form-input{background:var(--surface2);border:1px solid var(--border);border-radius:var(--r2);padding:9px 12px;font-size:13px;color:var(--text);outline:none;transition:border-color 0.15s;width:100%}
.form-input:focus{border-color:var(--accent)}
.form-input::placeholder{color:var(--text3)}
select.form-input option{background:var(--surface2)}
textarea.form-input{resize:vertical;min-height:80px}

/* ── Buttons ─────────────────────────────────────────────── */
.btn{padding:9px 18px;border-radius:var(--r2);font-size:13px;font-weight:700;transition:all 0.15s;cursor:pointer;border:none;display:inline-flex;align-items:center;gap:6px}
.btn-primary{background:var(--accent);color:#ffffff}
.btn-primary:hover{background:var(--accent2);transform:translateY(-1px)}
.btn-danger{background:var(--red);color:white}
.btn-danger:hover{opacity:0.85}
.btn-ghost{background:var(--surface2);color:var(--text2);border:1px solid var(--border)}
.btn-ghost:hover{background:var(--surface3);color:var(--text)}
.btn-green{background:var(--green);color:#ffffff}
.btn-green:hover{opacity:0.85}
.btn-sm{padding:6px 12px;font-size:12px}
.btn-xs{padding:4px 8px;font-size:11px}
.btn-icon{width:32px;height:32px;padding:0;justify-content:center;border-radius:var(--r2);font-size:14px}

/* ── Modal ───────────────────────────────────────────────── */
.overlay{position:fixed;inset:0;background:rgba(0,0,0,0.7);z-index:100;display:flex;align-items:center;justify-content:center;padding:20px;backdrop-filter:blur(4px)}
.modal{background:var(--surface);border:1px solid var(--border2);border-radius:16px;width:100%;max-width:520px;max-height:90vh;overflow-y:auto;box-shadow:var(--shadow-lg)}
.modal-head{padding:20px 24px 0;display:flex;align-items:center;justify-content:space-between}
.modal-title{font-family:'Syne',sans-serif;font-size:17px;font-weight:700}
.modal-body{padding:20px 24px}
.modal-foot{padding:0 24px 20px;display:flex;gap:10px;justify-content:flex-end}

/* ── Progress bar ────────────────────────────────────────── */
.progress-wrap{background:var(--surface2);border-radius:50px;height:6px;overflow:hidden}
.progress-bar{height:100%;border-radius:50px;transition:width 0.4s ease}

/* ── POS specific ────────────────────────────────────────── */
.pos-layout{display:grid;grid-template-columns:1fr 360px;gap:0;height:calc(100vh - 56px);overflow:hidden}
.pos-menu{overflow-y:auto;padding:16px}
.pos-cart{background:var(--surface);border-left:1px solid var(--border);display:flex;flex-direction:column}
.cat-tabs{display:flex;gap:8px;overflow-x:auto;padding-bottom:4px;margin-bottom:16px;scrollbar-width:none}
.cat-tabs::-webkit-scrollbar{display:none}
.cat-tab{padding:7px 16px;border-radius:50px;font-size:12px;font-weight:700;cursor:pointer;transition:all 0.15s;white-space:nowrap;border:1px solid var(--border);color:var(--text2)}
.cat-tab:hover{border-color:var(--border2);color:var(--text)}
.cat-tab.active{background:var(--accent);color:#1a1008;border-color:var(--accent)}
.menu-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(140px,1fr));gap:12px}
.menu-item{background:var(--surface2);border:1px solid var(--border);border-radius:var(--r);padding:14px 12px;cursor:pointer;transition:all 0.15s;text-align:center;position:relative}
.menu-item:hover{border-color:var(--accent);transform:translateY(-2px);box-shadow:0 4px 16px rgba(196,125,26,0.15)}
.menu-item.out{opacity:0.4;pointer-events:none}
.item-emoji{font-size:32px;display:block;margin-bottom:8px}
.item-name{font-size:12px;font-weight:700;color:var(--text);margin-bottom:4px;line-height:1.3}
.item-price{font-family:'DM Mono',monospace;font-size:13px;color:var(--accent);font-weight:500}
.item-cat-dot{position:absolute;top:8px;right:8px;width:6px;height:6px;border-radius:50%}
.cart-head{padding:16px;border-bottom:1px solid var(--border)}
.cart-title{font-family:'Syne',sans-serif;font-size:15px;font-weight:700}
.cart-items{flex:1;overflow-y:auto;padding:8px}
.cart-item{display:flex;align-items:center;gap:10px;padding:10px;border-radius:var(--r2);transition:background 0.15s}
.cart-item:hover{background:var(--surface2)}
.ci-emoji{font-size:22px;width:36px;height:36px;display:flex;align-items:center;justify-content:center;background:var(--surface2);border-radius:var(--r2);flex-shrink:0}
.ci-info{flex:1;min-width:0}
.ci-name{font-size:13px;font-weight:600;color:var(--text);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.ci-price{font-size:12px;color:var(--text3);font-family:'DM Mono',monospace}
.ci-qty{display:flex;align-items:center;gap:6px;flex-shrink:0}
.qty-btn{width:24px;height:24px;border-radius:50%;background:var(--surface3);color:var(--text);font-size:14px;font-weight:700;display:flex;align-items:center;justify-content:center;transition:all 0.15s}
.qty-btn:hover{background:var(--accent);color:#1a1008}
.qty-val{font-size:13px;font-weight:700;min-width:16px;text-align:center}
.cart-foot{padding:16px;border-top:1px solid var(--border)}
.cart-row{display:flex;justify-content:space-between;font-size:13px;margin-bottom:6px}
.cart-row.total{font-family:'Syne',sans-serif;font-size:17px;font-weight:800;margin-top:10px;padding-top:10px;border-top:1px solid var(--border);margin-bottom:0}
.cart-empty{display:flex;flex-direction:column;align-items:center;justify-content:center;height:100%;color:var(--text3);gap:10px;padding:24px}
.ce-icon{font-size:48px;opacity:0.4}

/* ── Inventory specific ──────────────────────────────────── */
.stock-bar-wrap{display:flex;align-items:center;gap:8px}
.stock-bar{flex:1;background:var(--surface2);border-radius:3px;height:5px;overflow:hidden}
.stock-fill{height:100%;border-radius:3px}

/* ── Chart (pure CSS bar chart) ─────────────────────────── */
.chart-wrap{display:flex;align-items:flex-end;gap:6px;height:120px;padding:0 4px}
.chart-bar-wrap{flex:1;display:flex;flex-direction:column;align-items:center;gap:4px}
.chart-bar{width:100%;border-radius:4px 4px 0 0;transition:height 0.4s ease;min-height:2px;cursor:pointer;position:relative}
.chart-bar:hover::after{content:attr(data-val);position:absolute;top:-22px;left:50%;transform:translateX(-50%);background:var(--surface3);color:var(--text);font-size:10px;padding:2px 6px;border-radius:4px;white-space:nowrap;font-family:'DM Mono',monospace}
.chart-label{font-size:10px;color:var(--text3);text-align:center;white-space:nowrap}

/* ── Notification toast ──────────────────────────────────── */
.toast-wrap{position:fixed;bottom:20px;right:20px;z-index:999;display:flex;flex-direction:column;gap:8px}
.toast{background:var(--surface);border:1px solid var(--border2);border-radius:var(--r);padding:12px 16px;font-size:13px;font-weight:600;display:flex;align-items:center;gap:10px;box-shadow:var(--shadow);animation:slideUp 0.3s ease;max-width:280px}
.toast-success{border-color:var(--green);background:rgba(42,157,78,0.06)}
.toast-error{border-color:var(--red);background:rgba(217,64,64,0.06)}
.toast-info{border-color:var(--blue);background:rgba(36,114,200,0.06)}
@keyframes slideUp{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}
@keyframes fadeIn{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}
.page{animation:fadeIn 0.25s ease}

/* ── Stat row ────────────────────────────────────────────── */
.stat-row{display:flex;align-items:center;justify-content:space-between;padding:10px 0;border-bottom:1px solid var(--border)}
.stat-row:last-child{border-bottom:none}
.stat-label{font-size:13px;color:var(--text2)}
.stat-val{font-family:'DM Mono',monospace;font-size:13px;font-weight:500;color:var(--text)}

/* ── Alert ───────────────────────────────────────────────── */
.alert{border-radius:var(--r2);padding:12px 16px;font-size:13px;display:flex;align-items:flex-start;gap:10px;margin-bottom:8px}
.alert-warn{background:rgba(196,125,26,0.08);border:1px solid rgba(196,125,26,0.35);color:var(--accent2)}
.alert-danger{background:rgba(217,64,64,0.08);border:1px solid rgba(217,64,64,0.35);color:var(--red)}
.alert-success{background:rgba(42,157,78,0.08);border:1px solid rgba(42,157,78,0.35);color:var(--green)}

/* ── Staff card ──────────────────────────────────────────── */
.staff-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);padding:16px;display:flex;align-items:center;gap:14px;transition:border-color 0.2s}
.staff-card:hover{border-color:var(--border2)}
.staff-avatar{width:44px;height:44px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-family:'Syne',sans-serif;font-size:16px;font-weight:800;flex-shrink:0}
.staff-info{flex:1;min-width:0}
.staff-name{font-weight:700;font-size:14px;color:var(--text)}
.staff-role{font-size:12px;color:var(--text3);margin-top:1px}
.staff-hours{font-family:'DM Mono',monospace;font-size:12px;color:var(--text2)}

/* ── Scrollable page ─────────────────────────────────────── */
.page-scroll{height:calc(100vh - 56px);overflow-y:auto;padding:24px}

/* ── Expense cat icon ────────────────────────────────────── */
.exp-icon{width:36px;height:36px;border-radius:var(--r2);display:flex;align-items:center;justify-content:center;font-size:16px;flex-shrink:0}

/* ── Search ──────────────────────────────────────────────── */
.search-wrap{position:relative;flex:1;max-width:280px}
.search-icon{position:absolute;left:10px;top:50%;transform:translateY(-50%);color:var(--text3);font-size:13px}
.search-input{width:100%;background:var(--surface2);border:1px solid var(--border);border-radius:var(--r2);padding:8px 12px 8px 30px;font-size:13px;color:var(--text);outline:none;transition:border-color 0.15s}
.search-input:focus{border-color:var(--accent)}
.search-input::placeholder{color:var(--text3)}

/* ── Responsive ──────────────────────────────────────────── */
@media(max-width:768px){
  .sidebar{width:52px}
  .sidebar-logo,.nav-item span,.sidebar-bottom .cafe-name,.sidebar-bottom .cafe-sub,.nav-label{display:none}
  .nav-item{justify-content:center;padding:10px}
  .nav-icon{width:auto}
  .pos-layout{grid-template-columns:1fr}
  .pos-cart{display:none}
  .grid4,.grid3{grid-template-columns:1fr 1fr}
  .grid2{grid-template-columns:1fr}
}

/* ── Login Screen ─────────────────────────────────────────── */
.login-screen{
  position:fixed;inset:0;z-index:9999;
  background:linear-gradient(135deg,#2c1a0e 0%,#4a2c10 45%,#6b3d15 100%);
  display:flex;align-items:center;justify-content:center;padding:20px;
  font-family:'Lato',sans-serif;
}
.login-bg-pattern{
  position:absolute;inset:0;opacity:0.04;
  background-image:radial-gradient(circle at 2px 2px,#fff 1px,transparent 0);
  background-size:28px 28px;
}
.login-card{
  background:#fff;border-radius:20px;padding:40px;width:100%;max-width:420px;
  box-shadow:0 24px 80px rgba(0,0,0,0.4);position:relative;z-index:1;
  animation:loginFadeIn 0.5s ease;
}
@keyframes loginFadeIn{
  from{opacity:0;transform:translateY(24px) scale(0.97)}
  to{opacity:1;transform:translateY(0) scale(1)}
}
.login-logo{text-align:center;margin-bottom:28px}
.login-logo-icon{font-size:52px;display:block;margin-bottom:10px}
.login-logo-name{font-family:'Syne',sans-serif;font-size:26px;font-weight:800;color:#2c1a0e;letter-spacing:-0.5px}
.login-logo-sub{font-size:12px;color:#8c8474;letter-spacing:2px;text-transform:uppercase;margin-top:3px}
.login-divider{height:1px;background:#e8e7e0;margin:20px 0}
.login-field{margin-bottom:16px}
.login-label{display:block;font-size:11px;font-weight:700;letter-spacing:1.2px;text-transform:uppercase;color:#8c8474;margin-bottom:7px}
.login-input{
  width:100%;padding:11px 14px;border-radius:10px;
  border:1.5px solid #e0ddd4;background:#f8f7f4;
  font-size:14px;color:#1a1714;outline:none;transition:all 0.2s;
}
.login-input:focus{border-color:#c47d1a;background:#fff;box-shadow:0 0 0 3px rgba(196,125,26,0.1)}
.login-input.error{border-color:#d94040;background:#fff8f8}
.login-input-wrap{position:relative}
.login-eye{
  position:absolute;right:12px;top:50%;transform:translateY(-50%);
  cursor:pointer;font-size:16px;color:#8c8474;transition:color 0.2s;background:none;border:none;
}
.login-eye:hover{color:#c47d1a}
.login-btn{
  width:100%;padding:13px;border-radius:10px;background:#c47d1a;color:#fff;
  font-family:'Syne',sans-serif;font-size:15px;font-weight:700;border:none;cursor:pointer;
  transition:all 0.2s;margin-top:6px;letter-spacing:0.3px;
}
.login-btn:hover{background:#a8621a;transform:translateY(-1px);box-shadow:0 4px 16px rgba(196,125,26,0.35)}
.login-btn:active{transform:translateY(0)}
.login-btn:disabled{opacity:0.6;pointer-events:none}
.login-error{
  background:#fff0f0;border:1px solid #f5c2c2;border-radius:8px;
  padding:10px 14px;font-size:13px;color:#d94040;font-weight:600;
  display:none;margin-top:12px;align-items:center;gap:8px;
}
.login-error.show{display:flex}
.login-users-hint{margin-top:20px;border-top:1px solid #e8e7e0;padding-top:16px}
.login-hint-title{font-size:11px;font-weight:700;letter-spacing:1px;text-transform:uppercase;color:#8c8474;margin-bottom:10px}
.login-user-chip{
  display:flex;align-items:center;gap:10px;padding:8px 12px;border-radius:8px;
  background:#f8f7f4;border:1px solid #e8e7e0;cursor:pointer;transition:all 0.15s;margin-bottom:6px;
}
.login-user-chip:hover{border-color:#c47d1a;background:#fdf6ec}
.login-chip-avatar{
  width:30px;height:30px;border-radius:50%;display:flex;align-items:center;
  justify-content:center;font-size:12px;font-weight:800;flex-shrink:0;
}
.login-chip-name{font-size:13px;font-weight:700;color:#1a1714}
.login-chip-role{font-size:11px;color:#8c8474;margin-left:auto}
.login-chip-pw{font-size:11px;color:#c47d1a;font-family:'DM Mono',monospace}
.login-footer{text-align:center;margin-top:16px;font-size:11px;color:#8c8474}
/* Topbar user pill */
.user-pill{
  display:flex;align-items:center;gap:8px;padding:4px 12px 4px 4px;
  border-radius:50px;background:var(--surface2);border:1px solid var(--border);cursor:pointer;transition:all 0.15s;
}
.user-pill:hover{border-color:var(--border2)}
.up-avatar{
  width:28px;height:28px;border-radius:50%;display:flex;align-items:center;
  justify-content:center;font-size:11px;font-weight:800;flex-shrink:0;
}
.up-name{font-size:12px;font-weight:700;color:var(--text)}
.up-role{font-size:11px;color:var(--text3)}
</style>
</head>
<body>

<!-- ═══════════════════════════════════════════════════════════
     LOGIN SCREEN
════════════════════════════════════════════════════════════ -->
<div id="login-screen" class="login-screen">
  <div class="login-bg-pattern"></div>
  <div class="login-card">
    <div class="login-logo">
      <span class="login-logo-icon">☕</span>
      <div class="login-logo-name">CaféOS</div>
      <div class="login-logo-sub">Management System</div>
    </div>

    <div class="login-field">
      <label class="login-label">Username</label>
      <input class="login-input" id="login-username" type="text" placeholder="Enter your username" autocomplete="username" autocapitalize="none"/>
    </div>

    <div class="login-field">
      <label class="login-label">Password</label>
      <div class="login-input-wrap">
        <input class="login-input" id="login-password" type="password" placeholder="Enter your password" autocomplete="current-password"
          onkeydown="if(event.key==='Enter')doLogin()"/>
        <button class="login-eye" id="login-eye-btn" onclick="toggleLoginPw()" title="Show/hide password">👁</button>
      </div>
    </div>

    <div class="login-error" id="login-error">
      <span>⚠</span><span id="login-error-msg">Incorrect username or password.</span>
    </div>

    <button class="login-btn" id="login-btn" onclick="doLogin()">Sign In →</button>

    <!-- Quick-login chips -->
    <div class="login-users-hint">
      <div class="login-hint-title">Quick Login — tap to fill</div>
      <div id="login-chips"></div>
    </div>

    <div class="login-footer">☕ All data stored locally on this device</div>
  </div>
</div>
<div class="app" id="app">
  <!-- SIDEBAR -->
  <aside class="sidebar" id="sidebar">
    <div class="sidebar-logo">
      <div class="logo-mark">☕ CaféOS</div>
      <div class="logo-sub">Management System</div>
    </div>

    <div class="nav-section">
      <div class="nav-label">Operations</div>
      <div class="nav-item active" data-page="dashboard" onclick="nav('dashboard')">
        <span class="nav-icon">⚡</span><span>Dashboard</span>
      </div>
      <div class="nav-item" data-page="pos" onclick="nav('pos')">
        <span class="nav-icon">🧾</span><span>Point of Sale</span>
      </div>
      <div class="nav-item" data-page="orders" onclick="nav('orders')">
        <span class="nav-icon">📋</span><span>Orders</span>
        <span class="nav-badge" id="pending-badge">0</span>
      </div>
    </div>

    <div class="nav-section">
      <div class="nav-label">Management</div>
      <div class="nav-item" data-page="menu" onclick="nav('menu')">
        <span class="nav-icon">🍽️</span><span>Menu Items</span>
      </div>
      <div class="nav-item" data-page="inventory" onclick="nav('inventory')">
        <span class="nav-icon">📦</span><span>Inventory</span>
        <span class="nav-badge" id="low-badge" style="display:none">!</span>
      </div>
      <div class="nav-item" data-page="expenses" onclick="nav('expenses')">
        <span class="nav-icon">💸</span><span>Expenses</span>
      </div>
      <div class="nav-item" data-page="staff" onclick="nav('staff')">
        <span class="nav-icon">👥</span><span>Staff</span>
      </div>
    </div>

    <div class="nav-section">
      <div class="nav-label">Analytics</div>
      <div class="nav-item" data-page="reports" onclick="nav('reports')">
        <span class="nav-icon">📊</span><span>Reports</span>
      </div>
    </div>

    <div class="sidebar-bottom">
      <div class="cafe-name" id="cafe-name-display">My Café</div>
      <div class="cafe-sub">v2.0 — Local Mode</div>
    </div>
  </aside>

  <!-- MAIN -->
  <div class="main">
    <div class="topbar">
      <div class="page-title" id="page-title">Dashboard</div>
      <div class="topbar-actions">
        <div class="clock" id="clock">--:--:--</div>
        <div class="user-pill" id="topbar-user" onclick="confirmLogout()" title="Click to sign out">
          <div class="up-avatar" id="topbar-avatar"></div>
          <div>
            <div class="up-name" id="topbar-uname">—</div>
            <div class="up-role" id="topbar-urole">—</div>
          </div>
        </div>
        <button class="tb-btn ghost" onclick="openSettings()">⚙ Settings</button>
        <button class="tb-btn primary" id="topbar-action" onclick="topbarAction()">+ New Order</button>
      </div>
    </div>
    <div id="page-content" style="flex:1;overflow:hidden"></div>
  </div>
</div>

<!-- Toast container -->
<div class="toast-wrap" id="toasts"></div>

<!-- Settings Modal -->
<div class="overlay" id="settings-modal" style="display:none">
  <div class="modal">
    <div class="modal-head">
      <div class="modal-title">⚙ Settings</div>
      <button class="btn btn-ghost btn-sm" onclick="closeModal('settings-modal')">✕</button>
    </div>
    <div class="modal-body">
      <div class="form-group mb">
        <label class="form-label">Café Name</label>
        <input class="form-input" id="setting-cafe-name" placeholder="My Café"/>
      </div>
      <div class="form-row cols2">
        <div class="form-group">
          <label class="form-label">Currency Symbol</label>
          <input class="form-input" id="setting-currency" placeholder="QR "/>
        </div>
        <div class="form-group">
          <label class="form-label">Tax Rate (%)</label>
          <input class="form-input" type="number" id="setting-tax" placeholder="0"/>
        </div>
      </div>
      <div class="form-group">
        <label class="form-label">Receipt Footer Message</label>
        <textarea class="form-input" id="setting-receipt" placeholder="Thank you for visiting!"></textarea>
      </div>
    </div>
    <div class="modal-foot">
      <button class="btn btn-ghost" onclick="closeModal('settings-modal')">Cancel</button>
      <button class="btn btn-primary" onclick="saveSettings()">Save Settings</button>
    </div>
  </div>
</div>

<script>
// ═══════════════════════════════════════════════════════════════
// STATE — All data stored in localStorage
// ═══════════════════════════════════════════════════════════════
// Reset currency to QR if still set to old $ default
(function(){
  try{
    const s = JSON.parse(localStorage.getItem('cafeOS_settings'))
    if(s && s.currency==='$'){ s.currency='QR '; localStorage.setItem('cafeOS_settings',JSON.stringify(s)) }
  }catch(e){}
})()
const DB = {
  load(k, def){ try{return JSON.parse(localStorage.getItem('cafeOS_'+k))||def}catch{return def} },
  save(k,v){ localStorage.setItem('cafeOS_'+k, JSON.stringify(v)) }
}

let state = {
  settings: DB.load('settings', { name:'My Café', currency:'QR ', tax:0, receipt:'Thank you! Come again ☕' }),
  menuItems: DB.load('menu', [
    {id:1,name:'Espresso',cat:'Coffee',price:9,cost:2,emoji:'☕',available:true},
    {id:2,name:'Cappuccino',cat:'Coffee',price:14,cost:3.50,emoji:'☕',available:true},
    {id:3,name:'Latte',cat:'Coffee',price:15,cost:4.50,emoji:'🥛',available:true},
    {id:4,name:'Cold Brew',cat:'Coffee',price:16,cost:4,emoji:'🧊',available:true},
    {id:5,name:'Matcha Latte',cat:'Tea',price:17,cost:5,emoji:'🍵',available:true},
    {id:6,name:'Chai Tea',cat:'Tea',price:13,cost:3,emoji:'🫖',available:true},
    {id:7,name:'Green Tea',cat:'Tea',price:10,cost:1.50,emoji:'🍃',available:true},
    {id:8,name:'Croissant',cat:'Food',price:12,cost:3.50,emoji:'🥐',available:true},
    {id:9,name:'Blueberry Muffin',cat:'Food',price:13,cost:3.50,emoji:'🫐',available:true},
    {id:10,name:'Avocado Toast',cat:'Food',price:28,cost:9,emoji:'🥑',available:true},
    {id:11,name:'Club Sandwich',cat:'Food',price:32,cost:11,emoji:'🥪',available:true},
    {id:12,name:'Cheesecake',cat:'Desserts',price:20,cost:6.50,emoji:'🍰',available:true},
    {id:13,name:'Chocolate Brownie',cat:'Desserts',price:15,cost:4.50,emoji:'🍫',available:true},
    {id:14,name:'Fresh OJ',cat:'Drinks',price:16,cost:5.50,emoji:'🍊',available:true},
    {id:15,name:'Sparkling Water',cat:'Drinks',price:7,cost:1,emoji:'💧',available:true},
  ]),
  inventory: DB.load('inventory', [
    {id:1,name:'Coffee Beans',unit:'kg',qty:5.2,min:2,cost:65,supplier:'Bean Bros'},
    {id:2,name:'Whole Milk',unit:'L',qty:12,min:5,cost:5.50,supplier:'Dairy Co'},
    {id:3,name:'Oat Milk',unit:'L',qty:6,min:3,cost:10,supplier:'Dairy Co'},
    {id:4,name:'Sugar',unit:'kg',qty:8,min:2,cost:3.50,supplier:'Local Market'},
    {id:5,name:'Matcha Powder',unit:'kg',qty:0.8,min:0.5,cost:165,supplier:'Tea Direct'},
    {id:6,name:'Chai Mix',unit:'kg',qty:1.2,min:0.5,cost:80,supplier:'Tea Direct'},
    {id:7,name:'Flour',unit:'kg',qty:15,min:5,cost:4.50,supplier:'Bakery Supply'},
    {id:8,name:'Butter',unit:'kg',qty:3,min:1,cost:29,supplier:'Dairy Co'},
    {id:9,name:'Croissants (pre-made)',unit:'pcs',qty:24,min:10,cost:3.50,supplier:'Bakery Supply'},
    {id:10,name:'Avocados',unit:'pcs',qty:8,min:5,cost:4.50,supplier:'Fresh Produce'},
    {id:11,name:'Coffee Cups (S)',unit:'pcs',qty:200,min:50,cost:0.20,supplier:'Supplies Inc'},
    {id:12,name:'Coffee Cups (L)',unit:'pcs',qty:150,min:50,cost:0.25,supplier:'Supplies Inc'},
  ]),
  expenses: DB.load('expenses', [
    {id:1,desc:'Electricity Bill',cat:'Utilities',amount:650,date:'2024-01-01',recurring:true},
    {id:2,desc:'Coffee Bean Restock',cat:'Supplies',amount:1200,date:'2024-01-03',recurring:false},
    {id:3,desc:'Staff Wages - Week 1',cat:'Wages',amount:4400,date:'2024-01-07',recurring:true},
    {id:4,desc:'Milk & Dairy',cat:'Supplies',amount:350,date:'2024-01-08',recurring:false},
    {id:5,desc:'Internet & Phone',cat:'Utilities',amount:240,date:'2024-01-10',recurring:true},
    {id:6,desc:'Cleaning Supplies',cat:'Maintenance',amount:165,date:'2024-01-12',recurring:false},
    {id:7,desc:'Rent',cat:'Rent',amount:8000,date:'2024-01-01',recurring:true},
    {id:8,desc:'Staff Wages - Week 2',cat:'Wages',amount:4400,date:'2024-01-14',recurring:true},
  ]),
  staff: DB.load('staff', [
    {id:1,name:'Alex Rivera',role:'Head Barista',hourlyRate:60,hoursThisWeek:38,color:'#f5a623',phone:'+974 5000-0101'},
    {id:2,name:'Sam Chen',role:'Barista',hourlyRate:48,hoursThisWeek:32,color:'#4da6ff',phone:'+974 5000-0102'},
    {id:3,name:'Jordan Lee',role:'Cashier',hourlyRate:45,hoursThisWeek:36,color:'#4ecb71',phone:'+974 5000-0103'},
    {id:4,name:'Morgan Blake',role:'Kitchen',hourlyRate:48,hoursThisWeek:30,color:'#a78bfa',phone:'+974 5000-0104'},
    {id:5,name:'Casey Park',role:'Server',hourlyRate:42,hoursThisWeek:28,color:'#f472b6',phone:'+974 5000-0105'},
  ]),
  orders: DB.load('orders', []),
  cart: [],
  currentPage: 'dashboard',
  orderCounter: DB.load('orderCounter', 1000),
  filterCat: 'All',
}

function saveAll(){
  DB.save('menu', state.menuItems)
  DB.save('inventory', state.inventory)
  DB.save('expenses', state.expenses)
  DB.save('staff', state.staff)
  DB.save('orders', state.orders)
  DB.save('settings', state.settings)
  DB.save('orderCounter', state.orderCounter)
}

// ═══════════════════════════════════════════════════════════════
// HELPERS
// ═══════════════════════════════════════════════════════════════
const cur = (v) => state.settings.currency + parseFloat(v||0).toFixed(2)
const today = () => new Date().toISOString().split('T')[0]
const fmtDate = (d) => new Date(d).toLocaleDateString('en-US',{month:'short',day:'numeric',year:'numeric'})
const fmtTime = (d) => new Date(d).toLocaleTimeString('en-US',{hour:'2-digit',minute:'2-digit'})

function toast(msg, type='info'){
  const c = document.getElementById('toasts')
  const el = document.createElement('div')
  el.className = `toast toast-${type}`
  const icons = {success:'✓',error:'✕',info:'ℹ'}
  el.innerHTML = `<span>${icons[type]||'ℹ'}</span> ${msg}`
  c.appendChild(el)
  setTimeout(()=>{el.style.opacity='0';el.style.transform='translateY(8px)';el.style.transition='all 0.3s';setTimeout(()=>el.remove(),300)}, 2800)
}

function openModal(id){ document.getElementById(id).style.display='flex' }
function closeModal(id){ document.getElementById(id).style.display='none' }

// ═══════════════════════════════════════════════════════════════
// NAVIGATION
// ═══════════════════════════════════════════════════════════════
const pageTitles = {
  dashboard:'⚡ Dashboard', pos:'🧾 Point of Sale', orders:'📋 Orders',
  menu:'🍽️ Menu Items', inventory:'📦 Inventory', expenses:'💸 Expenses',
  staff:'👥 Staff', reports:'📊 Reports'
}
const topbarActions = {
  dashboard:'+ New Order', pos:'Clear Cart', orders:'+ New Order',
  menu:'+ Add Item', inventory:'+ Restock', expenses:'+ Add Expense',
  staff:'+ Add Staff', reports:'Export PDF'
}

function nav(page){
  state.currentPage = page
  document.getElementById('page-title').textContent = pageTitles[page]||page
  document.getElementById('topbar-action').textContent = topbarActions[page]||'Action'
  document.querySelectorAll('.nav-item').forEach(el=>{
    el.classList.toggle('active', el.dataset.page===page)
  })
  render()
}

function topbarAction(){
  const a = { dashboard:()=>nav('pos'), pos:()=>clearCart(),
    orders:()=>nav('pos'), menu:()=>openAddItem(),
    inventory:()=>openRestock(), expenses:()=>openAddExpense(),
    staff:()=>openAddStaff(), reports:()=>toast('Export coming soon','info') }
  ;(a[state.currentPage]||(() =>{}))()
}

// ═══════════════════════════════════════════════════════════════
// CLOCK
// ═══════════════════════════════════════════════════════════════
function updateClock(){
  const now = new Date()
  document.getElementById('clock').textContent =
    now.toLocaleTimeString('en-US',{hour:'2-digit',minute:'2-digit',second:'2-digit'})
}
setInterval(updateClock, 1000); updateClock()

// ═══════════════════════════════════════════════════════════════
// RENDER ROUTER
// ═══════════════════════════════════════════════════════════════
function render(){
  const pc = document.getElementById('page-content')
  const pages = {
    dashboard: renderDashboard, pos: renderPOS, orders: renderOrders,
    menu: renderMenu, inventory: renderInventory, expenses: renderExpenses,
    staff: renderStaff, reports: renderReports
  }
  pc.innerHTML = (pages[state.currentPage]||renderDashboard)()
  // Update badges
  const pending = state.orders.filter(o=>o.status==='pending').length
  const pb = document.getElementById('pending-badge')
  pb.textContent = pending; pb.style.display = pending>0?'':'none'
  const lowStock = state.inventory.filter(i=>i.qty<=i.min).length
  const lb = document.getElementById('low-badge')
  lb.style.display = lowStock>0?'':'none'
  document.getElementById('cafe-name-display').textContent = state.settings.name
}

// ═══════════════════════════════════════════════════════════════
// DASHBOARD
// ═══════════════════════════════════════════════════════════════
function renderDashboard(){
  const todayOrders = state.orders.filter(o=>o.date?.startsWith(today()))
  const todayRevenue = todayOrders.reduce((s,o)=>s+o.total,0)
  const todayCOGS = todayOrders.reduce((s,o)=>s+(o.cost||0),0)
  const todayProfit = todayRevenue - todayCOGS
  const todayCount = todayOrders.length
  const avgOrder = todayCount ? todayRevenue/todayCount : 0
  const totalExpenses = state.expenses.reduce((s,e)=>s+e.amount,0)
  const lowStock = state.inventory.filter(i=>i.qty<=i.min)
  const pendingOrders = state.orders.filter(o=>o.status==='pending')

  // Last 7 days revenue
  const days = []
  for(let i=6;i>=0;i--){
    const d = new Date(); d.setDate(d.getDate()-i)
    const ds = d.toISOString().split('T')[0]
    const rev = state.orders.filter(o=>o.date?.startsWith(ds)).reduce((s,o)=>s+o.total,0)
    days.push({label:d.toLocaleDateString('en-US',{weekday:'short'}),rev})
  }
  const maxRev = Math.max(...days.map(d=>d.rev),1)

  // Top items
  const itemSales = {}
  state.orders.forEach(o=>{
    (o.items||[]).forEach(i=>{
      itemSales[i.name] = (itemSales[i.name]||0)+i.qty
    })
  })
  const topItems = Object.entries(itemSales).sort((a,b)=>b[1]-a[1]).slice(0,5)

  return `<div class="page-scroll page">
  <div class="grid4 mb">
    <div class="kpi">
      <div class="kpi-glow" style="background:var(--accent)"></div>
      <div class="kpi-label">Today's Revenue</div>
      <div class="kpi-val">${cur(todayRevenue)}</div>
      <div class="kpi-sub">${todayCount} orders today</div>
    </div>
    <div class="kpi">
      <div class="kpi-glow" style="background:var(--green)"></div>
      <div class="kpi-label">Today's Profit</div>
      <div class="kpi-val" style="color:var(--green)">${cur(todayProfit)}</div>
      <div class="kpi-sub">Margin: ${todayRevenue?((todayProfit/todayRevenue)*100).toFixed(1):0}%</div>
    </div>
    <div class="kpi">
      <div class="kpi-glow" style="background:var(--blue)"></div>
      <div class="kpi-label">Avg Order Value</div>
      <div class="kpi-val" style="color:var(--blue)">${cur(avgOrder)}</div>
      <div class="kpi-sub">Per transaction</div>
    </div>
    <div class="kpi">
      <div class="kpi-glow" style="background:var(--red)"></div>
      <div class="kpi-label">Total Expenses</div>
      <div class="kpi-val" style="color:var(--red)">${cur(totalExpenses)}</div>
      <div class="kpi-sub">All time logged</div>
    </div>
  </div>

  <div class="grid2 gap mb">
    <div class="card">
      <div class="sh"><div class="sh-title">📈 Revenue — Last 7 Days</div></div>
      <div class="chart-wrap">
        ${days.map(d=>`
          <div class="chart-bar-wrap">
            <div class="chart-bar" data-val="${cur(d.rev)}"
              style="height:${Math.max(4,(d.rev/maxRev)*110)}px;background:linear-gradient(180deg,var(--accent),var(--accent2))">
            </div>
            <div class="chart-label">${d.label}</div>
          </div>`).join('')}
      </div>
    </div>
    <div class="card">
      <div class="sh"><div class="sh-title">🏆 Top Selling Items</div></div>
      ${topItems.length?topItems.map(([name,qty],i)=>`
        <div class="stat-row">
          <div class="flex gap-sm" style="align-items:center">
            <span style="font-family:'Syne',sans-serif;font-size:12px;font-weight:800;color:var(--text3);width:16px">#${i+1}</span>
            <span class="stat-label">${name}</span>
          </div>
          <span class="badge badge-orange">${qty} sold</span>
        </div>`).join(''):`<div style="color:var(--text3);font-size:13px;padding:12px 0">No sales recorded yet. Start taking orders! 🚀</div>`}
    </div>
  </div>

  <div class="grid3 gap">
    <div class="card">
      <div class="sh">
        <div class="sh-title">⏳ Pending Orders</div>
        <span class="sh-action" onclick="nav('orders')">View all →</span>
      </div>
      ${pendingOrders.length?pendingOrders.slice(0,4).map(o=>`
        <div class="stat-row">
          <div>
            <div style="font-weight:700;font-size:13px;color:var(--text)">#${o.id}</div>
            <div style="font-size:11px;color:var(--text3)">${(o.items||[]).length} items · ${fmtTime(o.date)}</div>
          </div>
          <div class="flex gap-sm" style="align-items:center">
            <span style="font-family:'DM Mono',monospace;font-size:12px;color:var(--accent)">${cur(o.total)}</span>
            <button class="btn btn-green btn-xs" onclick="completeOrder(${o.id})">Done</button>
          </div>
        </div>`).join(''):`<div style="color:var(--text3);font-size:13px;padding:8px 0">🎉 All orders complete!</div>`}
    </div>

    <div class="card">
      <div class="sh">
        <div class="sh-title">⚠️ Low Stock Alerts</div>
        <span class="sh-action" onclick="nav('inventory')">Manage →</span>
      </div>
      ${lowStock.length?lowStock.slice(0,5).map(i=>`
        <div class="alert alert-${i.qty===0?'danger':'warn'} mt-sm" style="padding:8px 12px;margin-bottom:4px">
          <span>${i.qty===0?'🚨':'⚠️'}</span>
          <div style="flex:1">
            <div style="font-weight:700;font-size:12px">${i.name}</div>
            <div style="font-size:11px;opacity:0.8">${i.qty} ${i.unit} remaining (min: ${i.min})</div>
          </div>
        </div>`).join(''):`<div class="alert alert-success"><span>✅</span><div>All stock levels OK!</div></div>`}
    </div>

    <div class="card">
      <div class="sh">
        <div class="sh-title">👥 Staff on Shift</div>
        <span class="sh-action" onclick="nav('staff')">Manage →</span>
      </div>
      ${state.staff.slice(0,4).map(s=>`
        <div class="flex gap-sm mt-sm" style="align-items:center">
          <div style="width:32px;height:32px;border-radius:50%;background:${s.color}22;color:${s.color};display:flex;align-items:center;justify-content:center;font-weight:800;font-size:13px;flex-shrink:0">${s.name[0]}</div>
          <div style="flex:1">
            <div style="font-size:13px;font-weight:600;color:var(--text)">${s.name}</div>
            <div style="font-size:11px;color:var(--text3)">${s.role}</div>
          </div>
          <span class="badge badge-green">${s.hoursThisWeek}h</span>
        </div>`).join('')}
    </div>
  </div>
</div>`
}

// ═══════════════════════════════════════════════════════════════
// POINT OF SALE
// ═══════════════════════════════════════════════════════════════
function renderPOS(){
  const cats = ['All', ...new Set(state.menuItems.map(m=>m.cat))]
  const filtered = state.currentPage==='pos' && state.filterCat && state.filterCat!=='All'
    ? state.menuItems.filter(m=>m.cat===state.filterCat)
    : state.menuItems

  const subtotal = state.cart.reduce((s,i)=>s+i.price*i.qty,0)
  const tax = subtotal * (state.settings.tax/100)
  const total = subtotal + tax

  const catColors = {'Coffee':'#f5a623','Tea':'#4ecb71','Food':'#4da6ff','Drinks':'#a78bfa','Desserts':'#f472b6'}

  return `<div class="pos-layout page">
  <div class="pos-menu">
    <div class="cat-tabs">
      ${cats.map(c=>`<div class="cat-tab ${state.filterCat===c?'active':''}" onclick="setCat('${c}')">${c}</div>`).join('')}
    </div>
    <div class="menu-grid">
      ${filtered.map(item=>`
        <div class="menu-item ${!item.available?'out':''}" onclick="addToCart(${item.id})">
          <div class="item-cat-dot" style="background:${catColors[item.cat]||'var(--accent)'}"></div>
          <span class="item-emoji">${item.emoji}</span>
          <div class="item-name">${item.name}</div>
          <div class="item-price">${cur(item.price)}</div>
        </div>`).join('')}
    </div>
  </div>

  <div class="pos-cart">
    <div class="cart-head">
      <div class="flex between">
        <div class="cart-title">🛒 Current Order</div>
        ${state.cart.length?`<button class="btn btn-ghost btn-xs" onclick="clearCart()">Clear</button>`:''}
      </div>
      <div style="font-size:11px;color:var(--text3);margin-top:4px">${new Date().toLocaleDateString('en-US',{weekday:'long',month:'long',day:'numeric'})}</div>
    </div>

    <div class="cart-items">
      ${state.cart.length===0?`
        <div class="cart-empty">
          <div class="ce-icon">🛒</div>
          <div style="font-weight:600;font-size:14px">Cart is Empty</div>
          <div style="font-size:12px;text-align:center">Tap a menu item to add it to the order</div>
        </div>`
      :state.cart.map(item=>`
        <div class="cart-item">
          <div class="ci-emoji">${item.emoji}</div>
          <div class="ci-info">
            <div class="ci-name">${item.name}</div>
            <div class="ci-price">${cur(item.price)} ea · ${cur(item.price*item.qty)}</div>
          </div>
          <div class="ci-qty">
            <button class="qty-btn" onclick="changeQty(${item.id},-1)">−</button>
            <span class="qty-val">${item.qty}</span>
            <button class="qty-btn" onclick="changeQty(${item.id},1)">+</button>
          </div>
        </div>`).join('')}
    </div>

    ${state.cart.length?`
    <div class="cart-foot">
      <div class="cart-row"><span style="color:var(--text2)">Subtotal</span><span style="font-family:'DM Mono',monospace">${cur(subtotal)}</span></div>
      ${state.settings.tax>0?`<div class="cart-row"><span style="color:var(--text2)">Tax (${state.settings.tax}%)</span><span style="font-family:'DM Mono',monospace">${cur(tax)}</span></div>`:''}
      <div class="cart-row total"><span>TOTAL</span><span style="color:var(--accent)">${cur(total)}</span></div>
      <div style="display:flex;gap:8px;margin-top:12px">
        <select class="form-input" id="order-type" style="flex:1;padding:8px 10px">
          <option value="Dine In">🪑 Dine In</option>
          <option value="Takeaway">🥡 Takeaway</option>
          <option value="Delivery">🚴 Delivery</option>
        </select>
      </div>
      <button class="btn btn-primary" style="width:100%;margin-top:10px;padding:12px;font-size:15px;justify-content:center" onclick="placeOrder()">
        ✓ Place Order · ${cur(total)}
      </button>
    </div>`:''}
  </div>
</div>`
}

function setCat(cat){
  state.filterCat = cat
  render()
}

function addToCart(id){
  const item = state.menuItems.find(m=>m.id===id)
  if(!item||!item.available) return
  const existing = state.cart.find(c=>c.id===id)
  if(existing) existing.qty++
  else state.cart.push({...item, qty:1})
  render()
}

function changeQty(id, delta){
  const idx = state.cart.findIndex(c=>c.id===id)
  if(idx<0) return
  state.cart[idx].qty += delta
  if(state.cart[idx].qty<=0) state.cart.splice(idx,1)
  render()
}

function clearCart(){
  state.cart = []
  render()
}

function placeOrder(){
  if(!state.cart.length){toast('Cart is empty!','error');return}
  const subtotal = state.cart.reduce((s,i)=>s+i.price*i.qty,0)
  const tax = subtotal*(state.settings.tax/100)
  const cost = state.cart.reduce((s,i)=>s+(i.cost||0)*i.qty,0)
  const typeEl = document.getElementById('order-type')
  const type = typeEl?typeEl.value:'Dine In'
  const order = {
    id: ++state.orderCounter,
    items: state.cart.map(i=>({...i})),
    subtotal, tax, total: subtotal+tax, cost,
    type, status:'pending',
    date: new Date().toISOString()
  }
  state.orders.unshift(order)
  state.cart = []
  saveAll()
  toast(`Order #${order.id} placed!`,'success')
  render()
}

function completeOrder(id){
  const o = state.orders.find(o=>o.id===id)
  if(o) o.status='completed'
  saveAll()
  toast(`Order #${id} completed!`,'success')
  render()
}

// ═══════════════════════════════════════════════════════════════
// ORDERS
// ═══════════════════════════════════════════════════════════════
function renderOrders(){
  const statusColors = {pending:'orange',completed:'green',cancelled:'red'}
  const recentOrders = state.orders.slice(0,50)
  return `<div class="page-scroll page">
  <div class="flex between mb">
    <div class="flex gap-sm">
      ${['All','pending','completed','cancelled'].map(s=>`
        <button class="btn btn-ghost btn-sm" onclick="filterOrders('${s}')">${s==='All'?'All':s.charAt(0).toUpperCase()+s.slice(1)}</button>`).join('')}
    </div>
    <div style="font-size:13px;color:var(--text3)">${state.orders.length} total orders</div>
  </div>
  ${recentOrders.length===0?`<div class="card" style="text-align:center;padding:48px">
    <div style="font-size:48px;margin-bottom:12px">📋</div>
    <div style="font-family:'Syne',sans-serif;font-size:18px;font-weight:700;margin-bottom:8px">No Orders Yet</div>
    <div style="color:var(--text3);font-size:14px;margin-bottom:16px">Head to Point of Sale to take your first order</div>
    <button class="btn btn-primary" onclick="nav('pos')">Open POS →</button>
  </div>`:`
  <div class="tbl-wrap">
    <table class="tbl">
      <thead><tr>
        <th>Order #</th><th>Time</th><th>Type</th><th>Items</th><th>Subtotal</th><th>Total</th><th>Status</th><th>Actions</th>
      </tr></thead>
      <tbody>
        ${recentOrders.map(o=>`<tr>
          <td><span style="font-family:'DM Mono',monospace;font-weight:600;color:var(--accent)">#${o.id}</span></td>
          <td style="color:var(--text2)">${fmtTime(o.date)}<br><span style="font-size:11px;color:var(--text3)">${fmtDate(o.date)}</span></td>
          <td><span class="badge badge-blue">${o.type||'Dine In'}</span></td>
          <td style="max-width:200px">
            <div style="font-size:12px;color:var(--text2)">${(o.items||[]).map(i=>`${i.name}×${i.qty}`).join(', ')}</div>
          </td>
          <td style="font-family:'DM Mono',monospace">${cur(o.subtotal)}</td>
          <td style="font-family:'DM Mono',monospace;font-weight:700;color:var(--accent)">${cur(o.total)}</td>
          <td><span class="badge badge-${statusColors[o.status]||'blue'}">${o.status}</span></td>
          <td>
            <div class="flex gap-sm">
              ${o.status==='pending'?`<button class="btn btn-green btn-xs" onclick="completeOrder(${o.id})">✓ Done</button>`:''}
              ${o.status==='pending'?`<button class="btn btn-ghost btn-xs" onclick="cancelOrder(${o.id})">✕</button>`:''}
            </div>
          </td>
        </tr>`).join('')}
      </tbody>
    </table>
  </div>`}
</div>`
}

function cancelOrder(id){
  const o = state.orders.find(o=>o.id===id)
  if(o){o.status='cancelled';saveAll();toast(`Order #${id} cancelled`,'info');render()}
}

// ═══════════════════════════════════════════════════════════════
// MENU MANAGEMENT
// ═══════════════════════════════════════════════════════════════
function renderMenu(){
  const cats = ['All', ...new Set(state.menuItems.map(m=>m.cat))]
  const fc = state.filterCat||'All'
  const filtered = fc==='All'?state.menuItems:state.menuItems.filter(m=>m.cat===fc)
  return `<div class="page-scroll page">
  <div class="flex between mb" style="flex-wrap:wrap;gap:10px">
    <div class="cat-tabs" style="flex:1">
      ${cats.map(c=>`<div class="cat-tab ${fc===c?'active':''}" onclick="setMenuCat('${c}')">${c}</div>`).join('')}
    </div>
  </div>
  <div class="tbl-wrap">
    <table class="tbl">
      <thead><tr><th>Item</th><th>Category</th><th>Price</th><th>Cost</th><th>Margin</th><th>Status</th><th>Actions</th></tr></thead>
      <tbody>
        ${filtered.map(item=>{
          const margin = item.price>0?((item.price-item.cost)/item.price*100):0
          return `<tr>
            <td>
              <div class="flex gap-sm" style="align-items:center">
                <span style="font-size:22px">${item.emoji}</span>
                <span style="font-weight:600;font-size:14px">${item.name}</span>
              </div>
            </td>
            <td><span class="badge badge-purple">${item.cat}</span></td>
            <td style="font-family:'DM Mono',monospace;color:var(--accent)">${cur(item.price)}</td>
            <td style="font-family:'DM Mono',monospace;color:var(--text2)">${cur(item.cost)}</td>
            <td>
              <div class="flex gap-sm" style="align-items:center">
                <div class="progress-wrap" style="width:60px">
                  <div class="progress-bar" style="width:${margin}%;background:${margin>50?'var(--green)':margin>30?'var(--accent)':'var(--red)'}"></div>
                </div>
                <span style="font-size:12px;color:${margin>50?'var(--green)':margin>30?'var(--accent)':'var(--red)'}">${margin.toFixed(0)}%</span>
              </div>
            </td>
            <td><span class="badge ${item.available?'badge-green':'badge-red'}">${item.available?'Active':'Inactive'}</span></td>
            <td>
              <div class="flex gap-sm">
                <button class="btn btn-ghost btn-xs" onclick="editItem(${item.id})">✏ Edit</button>
                <button class="btn btn-ghost btn-xs" onclick="toggleItem(${item.id})">${item.available?'Disable':'Enable'}</button>
                <button class="btn btn-danger btn-xs" onclick="deleteItem(${item.id})">✕</button>
              </div>
            </td>
          </tr>`}).join('')}
      </tbody>
    </table>
  </div>

  <div class="overlay" id="item-modal" style="display:none">
    <div class="modal">
      <div class="modal-head">
        <div class="modal-title" id="item-modal-title">Add Menu Item</div>
        <button class="btn btn-ghost btn-sm" onclick="closeModal('item-modal')">✕</button>
      </div>
      <div class="modal-body">
        <input type="hidden" id="item-id"/>
        <div class="form-row cols2">
          <div class="form-group">
            <label class="form-label">Item Name</label>
            <input class="form-input" id="item-name" placeholder="Cappuccino"/>
          </div>
          <div class="form-group">
            <label class="form-label">Emoji</label>
            <input class="form-input" id="item-emoji" placeholder="☕"/>
          </div>
        </div>
        <div class="form-row cols3">
          <div class="form-group">
            <label class="form-label">Category</label>
            <select class="form-input" id="item-cat">
              <option>Coffee</option><option>Tea</option><option>Food</option><option>Drinks</option><option>Desserts</option>
            </select>
          </div>
          <div class="form-group">
            <label class="form-label">Selling Price</label>
            <input class="form-input" type="number" id="item-price" step="0.01" placeholder="4.50"/>
          </div>
          <div class="form-group">
            <label class="form-label">Cost Price</label>
            <input class="form-input" type="number" id="item-cost" step="0.01" placeholder="1.20"/>
          </div>
        </div>
      </div>
      <div class="modal-foot">
        <button class="btn btn-ghost" onclick="closeModal('item-modal')">Cancel</button>
        <button class="btn btn-primary" onclick="saveItem()">Save Item</button>
      </div>
    </div>
  </div>
</div>`
}

function setMenuCat(c){ state.filterCat=c; render() }
function openAddItem(){ 
  document.getElementById('item-id').value=''
  document.getElementById('item-name').value=''
  document.getElementById('item-emoji').value=''
  document.getElementById('item-price').value=''
  document.getElementById('item-cost').value=''
  document.getElementById('item-modal-title').textContent='Add Menu Item'
  openModal('item-modal')
}
function editItem(id){
  const item=state.menuItems.find(m=>m.id===id); if(!item)return
  document.getElementById('item-id').value=id
  document.getElementById('item-name').value=item.name
  document.getElementById('item-emoji').value=item.emoji
  document.getElementById('item-cat').value=item.cat
  document.getElementById('item-price').value=item.price
  document.getElementById('item-cost').value=item.cost
  document.getElementById('item-modal-title').textContent='Edit Menu Item'
  openModal('item-modal')
}
function saveItem(){
  const id=parseInt(document.getElementById('item-id').value)||null
  const item={
    name:document.getElementById('item-name').value,
    emoji:document.getElementById('item-emoji').value||'☕',
    cat:document.getElementById('item-cat').value,
    price:parseFloat(document.getElementById('item-price').value)||0,
    cost:parseFloat(document.getElementById('item-cost').value)||0,
    available:true
  }
  if(!item.name){toast('Name required','error');return}
  if(id){const idx=state.menuItems.findIndex(m=>m.id===id);if(idx>=0)state.menuItems[idx]={...state.menuItems[idx],...item}}
  else{state.menuItems.push({...item,id:Date.now()})}
  closeModal('item-modal');saveAll();toast(id?'Item updated!':'Item added!','success');render()
}
function toggleItem(id){
  const item=state.menuItems.find(m=>m.id===id); if(item){item.available=!item.available;saveAll();render()}
}
function deleteItem(id){
  if(!confirm('Delete this item?'))return
  state.menuItems=state.menuItems.filter(m=>m.id!==id);saveAll();toast('Item deleted','info');render()
}

// ═══════════════════════════════════════════════════════════════
// INVENTORY
// ═══════════════════════════════════════════════════════════════
function renderInventory(){
  const totalValue = state.inventory.reduce((s,i)=>s+i.qty*i.cost,0)
  const lowItems = state.inventory.filter(i=>i.qty<=i.min)
  return `<div class="page-scroll page">
  ${lowItems.length?`<div class="alert alert-warn mb">${lowItems.length} item(s) below minimum stock level. <strong>${lowItems.map(i=>i.name).join(', ')}</strong></div>`:''}
  
  <div class="grid3 mb">
    <div class="kpi">
      <div class="kpi-label">Total Stock Value</div>
      <div class="kpi-val">${cur(totalValue)}</div>
    </div>
    <div class="kpi">
      <div class="kpi-label">Items Tracked</div>
      <div class="kpi-val">${state.inventory.length}</div>
    </div>
    <div class="kpi">
      <div class="kpi-label">Low Stock Alerts</div>
      <div class="kpi-val" style="color:${lowItems.length?'var(--red)':'var(--green)'}">${lowItems.length}</div>
    </div>
  </div>

  <div class="tbl-wrap">
    <table class="tbl">
      <thead><tr><th>Item</th><th>Supplier</th><th>In Stock</th><th>Min Level</th><th>Stock Level</th><th>Unit Cost</th><th>Total Value</th><th>Actions</th></tr></thead>
      <tbody>
        ${state.inventory.map(item=>{
          const pct = Math.min(100,(item.qty/Math.max(item.min*2,1))*100)
          const color = item.qty===0?'var(--red)':item.qty<=item.min?'var(--accent)':'var(--green)'
          return `<tr>
            <td><span style="font-weight:600;font-size:14px">${item.name}</span></td>
            <td style="color:var(--text2);font-size:12px">${item.supplier}</td>
            <td>
              <span style="font-family:'DM Mono',monospace;font-weight:700;color:${color}">${item.qty}</span>
              <span style="color:var(--text3);font-size:12px"> ${item.unit}</span>
            </td>
            <td style="color:var(--text3);font-family:'DM Mono',monospace">${item.min} ${item.unit}</td>
            <td style="min-width:120px">
              <div class="stock-bar-wrap">
                <div class="stock-bar"><div class="stock-fill" style="width:${pct}%;background:${color}"></div></div>
                <span style="font-size:11px;color:${color};min-width:30px">${pct.toFixed(0)}%</span>
              </div>
            </td>
            <td style="font-family:'DM Mono',monospace;color:var(--text2)">${cur(item.cost)}</td>
            <td style="font-family:'DM Mono',monospace;font-weight:600">${cur(item.qty*item.cost)}</td>
            <td>
              <div class="flex gap-sm">
                <button class="btn btn-ghost btn-xs" onclick="restockItem(${item.id})">+ Restock</button>
                <button class="btn btn-ghost btn-xs" onclick="editInventory(${item.id})">✏</button>
                <button class="btn btn-danger btn-xs" onclick="deleteInventory(${item.id})">✕</button>
              </div>
            </td>
          </tr>`}).join('')}
      </tbody>
    </table>
  </div>

  <div class="overlay" id="inv-modal" style="display:none">
    <div class="modal">
      <div class="modal-head">
        <div class="modal-title" id="inv-modal-title">Add Inventory Item</div>
        <button class="btn btn-ghost btn-sm" onclick="closeModal('inv-modal')">✕</button>
      </div>
      <div class="modal-body">
        <input type="hidden" id="inv-id"/>
        <div class="form-row cols2">
          <div class="form-group">
            <label class="form-label">Item Name</label>
            <input class="form-input" id="inv-name" placeholder="Coffee Beans"/>
          </div>
          <div class="form-group">
            <label class="form-label">Unit (kg, L, pcs…)</label>
            <input class="form-input" id="inv-unit" placeholder="kg"/>
          </div>
        </div>
        <div class="form-row cols3">
          <div class="form-group">
            <label class="form-label">Current Qty</label>
            <input class="form-input" type="number" id="inv-qty" step="0.1" placeholder="10"/>
          </div>
          <div class="form-group">
            <label class="form-label">Min Level</label>
            <input class="form-input" type="number" id="inv-min" step="0.1" placeholder="2"/>
          </div>
          <div class="form-group">
            <label class="form-label">Cost per Unit</label>
            <input class="form-input" type="number" id="inv-cost" step="0.01" placeholder="18.00"/>
          </div>
        </div>
        <div class="form-group">
          <label class="form-label">Supplier</label>
          <input class="form-input" id="inv-supplier" placeholder="Supplier name"/>
        </div>
      </div>
      <div class="modal-foot">
        <button class="btn btn-ghost" onclick="closeModal('inv-modal')">Cancel</button>
        <button class="btn btn-primary" onclick="saveInventory()">Save</button>
      </div>
    </div>
  </div>

  <div class="overlay" id="restock-modal" style="display:none">
    <div class="modal" style="max-width:380px">
      <div class="modal-head">
        <div class="modal-title" id="restock-title">Restock Item</div>
        <button class="btn btn-ghost btn-sm" onclick="closeModal('restock-modal')">✕</button>
      </div>
      <div class="modal-body">
        <input type="hidden" id="restock-id"/>
        <div class="form-group">
          <label class="form-label">Add Quantity</label>
          <input class="form-input" type="number" id="restock-qty" step="0.1" placeholder="Enter amount to add"/>
        </div>
        <div class="form-group">
          <label class="form-label">Supplier Invoice / Note (optional)</label>
          <input class="form-input" id="restock-note" placeholder="e.g. Invoice #1234"/>
        </div>
      </div>
      <div class="modal-foot">
        <button class="btn btn-ghost" onclick="closeModal('restock-modal')">Cancel</button>
        <button class="btn btn-primary" onclick="confirmRestock()">✓ Add Stock</button>
      </div>
    </div>
  </div>
</div>`
}

function openRestock(){ 
  document.getElementById('inv-id').value=''
  document.getElementById('inv-modal-title').textContent='Add Inventory Item'
  openModal('inv-modal')
}
function editInventory(id){
  const i=state.inventory.find(x=>x.id===id); if(!i)return
  document.getElementById('inv-id').value=id
  document.getElementById('inv-name').value=i.name
  document.getElementById('inv-unit').value=i.unit
  document.getElementById('inv-qty').value=i.qty
  document.getElementById('inv-min').value=i.min
  document.getElementById('inv-cost').value=i.cost
  document.getElementById('inv-supplier').value=i.supplier
  document.getElementById('inv-modal-title').textContent='Edit Item'
  openModal('inv-modal')
}
function saveInventory(){
  const id=parseInt(document.getElementById('inv-id').value)||null
  const item={
    name:document.getElementById('inv-name').value,
    unit:document.getElementById('inv-unit').value||'pcs',
    qty:parseFloat(document.getElementById('inv-qty').value)||0,
    min:parseFloat(document.getElementById('inv-min').value)||0,
    cost:parseFloat(document.getElementById('inv-cost').value)||0,
    supplier:document.getElementById('inv-supplier').value||'—'
  }
  if(!item.name){toast('Name required','error');return}
  if(id){const idx=state.inventory.findIndex(i=>i.id===id);if(idx>=0)state.inventory[idx]={...state.inventory[idx],...item}}
  else state.inventory.push({...item,id:Date.now()})
  closeModal('inv-modal');saveAll();toast('Saved!','success');render()
}
function restockItem(id){
  const i=state.inventory.find(x=>x.id===id); if(!i)return
  document.getElementById('restock-id').value=id
  document.getElementById('restock-title').textContent=`Restock: ${i.name}`
  document.getElementById('restock-qty').value=''
  openModal('restock-modal')
}
function confirmRestock(){
  const id=parseInt(document.getElementById('restock-id').value)
  const qty=parseFloat(document.getElementById('restock-qty').value)
  if(!qty||qty<=0){toast('Enter a valid quantity','error');return}
  const item=state.inventory.find(i=>i.id===id); if(!item)return
  item.qty=parseFloat((item.qty+qty).toFixed(2))
  closeModal('restock-modal');saveAll();toast(`${item.name} restocked +${qty} ${item.unit}`,'success');render()
}
function deleteInventory(id){
  if(!confirm('Remove this item?'))return
  state.inventory=state.inventory.filter(i=>i.id!==id);saveAll();render()
}

// ═══════════════════════════════════════════════════════════════
// EXPENSES
// ═══════════════════════════════════════════════════════════════
const expCats = ['Supplies','Wages','Rent','Utilities','Maintenance','Marketing','Equipment','Other']
const expIcons = {Supplies:'🛒',Wages:'👷',Rent:'🏠',Utilities:'⚡',Maintenance:'🔧',Marketing:'📣',Equipment:'🖥️',Other:'📌'}
const expColors = {Supplies:'var(--blue)',Wages:'var(--purple)',Rent:'var(--red)',Utilities:'var(--accent)',Maintenance:'var(--green)',Marketing:'var(--pink)',Equipment:'var(--text2)',Other:'var(--text3)'}

function renderExpenses(){
  const total = state.expenses.reduce((s,e)=>s+e.amount,0)
  const bycat = {}
  state.expenses.forEach(e=>{ bycat[e.cat]=(bycat[e.cat]||0)+e.amount })
  const maxCat = Math.max(...Object.values(bycat),1)

  return `<div class="page-scroll page">
  <div class="grid4 mb">
    <div class="kpi" style="grid-column:span 1">
      <div class="kpi-label">Total Expenses</div>
      <div class="kpi-val" style="color:var(--red)">${cur(total)}</div>
    </div>
    ${Object.entries(bycat).slice(0,3).map(([cat,amt])=>`
      <div class="kpi">
        <div class="kpi-label">${cat}</div>
        <div class="kpi-val" style="font-size:22px">${cur(amt)}</div>
        <div style="margin-top:8px"><div class="progress-wrap"><div class="progress-bar" style="width:${(amt/total*100).toFixed(0)}%;background:${expColors[cat]||'var(--accent)'}"></div></div></div>
      </div>`).join('')}
  </div>

  <div class="grid2 gap mb">
    <div class="card">
      <div class="sh"><div class="sh-title">📊 By Category</div></div>
      ${Object.entries(bycat).sort((a,b)=>b[1]-a[1]).map(([cat,amt])=>`
        <div class="stat-row">
          <div class="flex gap-sm" style="align-items:center">
            <div class="exp-icon" style="background:${expColors[cat]||'var(--surface2)'}22;color:${expColors[cat]||'var(--text2)'}">
              ${expIcons[cat]||'📌'}
            </div>
            <span class="stat-label">${cat}</span>
          </div>
          <div class="flex gap-sm" style="align-items:center">
            <div class="progress-wrap" style="width:80px"><div class="progress-bar" style="width:${(amt/maxCat*100).toFixed(0)}%;background:${expColors[cat]||'var(--accent)'}"></div></div>
            <span style="font-family:'DM Mono',monospace;font-size:13px;min-width:70px;text-align:right">${cur(amt)}</span>
          </div>
        </div>`).join('')}
    </div>

    <div class="card">
      <div class="sh">
        <div class="sh-title">🔄 Recurring Expenses</div>
        <span class="sh-action" onclick="openAddExpense()">+ Add</span>
      </div>
      ${state.expenses.filter(e=>e.recurring).map(e=>`
        <div class="stat-row">
          <div>
            <div style="font-size:13px;font-weight:600;color:var(--text)">${e.desc}</div>
            <div style="font-size:11px;color:var(--text3)">${e.cat}</div>
          </div>
          <span style="font-family:'DM Mono',monospace;color:var(--red)">${cur(e.amount)}/mo</span>
        </div>`).join('')}
    </div>
  </div>

  <div class="sh"><div class="sh-title">All Expense Records</div></div>
  <div class="tbl-wrap">
    <table class="tbl">
      <thead><tr><th>Description</th><th>Category</th><th>Date</th><th>Recurring</th><th>Amount</th><th>Actions</th></tr></thead>
      <tbody>
        ${state.expenses.map(e=>`<tr>
          <td>
            <div class="flex gap-sm" style="align-items:center">
              <div class="exp-icon" style="background:${expColors[e.cat]||'var(--surface2)'}22;font-size:14px">${expIcons[e.cat]||'📌'}</div>
              <span style="font-weight:600;font-size:13px">${e.desc}</span>
            </div>
          </td>
          <td><span class="badge" style="background:${expColors[e.cat]||'var(--surface2)'}22;color:${expColors[e.cat]||'var(--text2)'}">${e.cat}</span></td>
          <td style="color:var(--text2);font-size:12px">${fmtDate(e.date)}</td>
          <td>${e.recurring?'<span class="badge badge-blue">🔄 Monthly</span>':'<span style="color:var(--text3);font-size:12px">One-time</span>'}</td>
          <td style="font-family:'DM Mono',monospace;font-weight:700;color:var(--red)">${cur(e.amount)}</td>
          <td>
            <div class="flex gap-sm">
              <button class="btn btn-ghost btn-xs" onclick="editExpense(${e.id})">✏</button>
              <button class="btn btn-danger btn-xs" onclick="deleteExpense(${e.id})">✕</button>
            </div>
          </td>
        </tr>`).join('')}
      </tbody>
    </table>
  </div>

  <div class="overlay" id="exp-modal" style="display:none">
    <div class="modal">
      <div class="modal-head">
        <div class="modal-title" id="exp-modal-title">Add Expense</div>
        <button class="btn btn-ghost btn-sm" onclick="closeModal('exp-modal')">✕</button>
      </div>
      <div class="modal-body">
        <input type="hidden" id="exp-id"/>
        <div class="form-group mb">
          <label class="form-label">Description</label>
          <input class="form-input" id="exp-desc" placeholder="e.g. Coffee Bean Restock"/>
        </div>
        <div class="form-row cols2">
          <div class="form-group">
            <label class="form-label">Category</label>
            <select class="form-input" id="exp-cat">
              ${expCats.map(c=>`<option>${c}</option>`).join('')}
            </select>
          </div>
          <div class="form-group">
            <label class="form-label">Amount</label>
            <input class="form-input" type="number" id="exp-amount" step="0.01" placeholder="0.00"/>
          </div>
        </div>
        <div class="form-row cols2">
          <div class="form-group">
            <label class="form-label">Date</label>
            <input class="form-input" type="date" id="exp-date"/>
          </div>
          <div class="form-group" style="justify-content:flex-end">
            <label class="form-label">Recurring Monthly?</label>
            <select class="form-input" id="exp-recurring">
              <option value="false">One-time</option>
              <option value="true">🔄 Yes, monthly</option>
            </select>
          </div>
        </div>
      </div>
      <div class="modal-foot">
        <button class="btn btn-ghost" onclick="closeModal('exp-modal')">Cancel</button>
        <button class="btn btn-primary" onclick="saveExpense()">Save Expense</button>
      </div>
    </div>
  </div>
</div>`
}

function openAddExpense(){
  document.getElementById('exp-id').value=''
  document.getElementById('exp-desc').value=''
  document.getElementById('exp-amount').value=''
  document.getElementById('exp-date').value=today()
  document.getElementById('exp-recurring').value='false'
  document.getElementById('exp-modal-title').textContent='Add Expense'
  openModal('exp-modal')
}
function editExpense(id){
  const e=state.expenses.find(x=>x.id===id); if(!e)return
  document.getElementById('exp-id').value=id
  document.getElementById('exp-desc').value=e.desc
  document.getElementById('exp-cat').value=e.cat
  document.getElementById('exp-amount').value=e.amount
  document.getElementById('exp-date').value=e.date
  document.getElementById('exp-recurring').value=e.recurring?'true':'false'
  document.getElementById('exp-modal-title').textContent='Edit Expense'
  openModal('exp-modal')
}
function saveExpense(){
  const id=parseInt(document.getElementById('exp-id').value)||null
  const item={
    desc:document.getElementById('exp-desc').value,
    cat:document.getElementById('exp-cat').value,
    amount:parseFloat(document.getElementById('exp-amount').value)||0,
    date:document.getElementById('exp-date').value||today(),
    recurring:document.getElementById('exp-recurring').value==='true'
  }
  if(!item.desc){toast('Description required','error');return}
  if(id){const idx=state.expenses.findIndex(e=>e.id===id);if(idx>=0)state.expenses[idx]={...state.expenses[idx],...item}}
  else state.expenses.push({...item,id:Date.now()})
  closeModal('exp-modal');saveAll();toast(id?'Expense updated!':'Expense added!','success');render()
}
function deleteExpense(id){
  if(!confirm('Delete this expense?'))return
  state.expenses=state.expenses.filter(e=>e.id!==id);saveAll();toast('Deleted','info');render()
}

// ═══════════════════════════════════════════════════════════════
// STAFF
// ═══════════════════════════════════════════════════════════════

// Helper: calculate a staff member's effective weekly pay
function staffWeeklyPay(s){
  if(s.salaryType==='monthly') return (s.monthlySalary||0)/4.33
  if(s.salaryType==='fixed_weekly') return s.weeklyRate||0
  return (s.hourlyRate||0)*(s.hoursThisWeek||0)
}
function staffMonthlyCost(s){
  if(s.salaryType==='monthly') return s.monthlySalary||0
  if(s.salaryType==='fixed_weekly') return (s.weeklyRate||0)*4.33
  return (s.hourlyRate||0)*(s.hoursThisWeek||0)*4.33
}

function renderStaff(){
  const totalWeekly   = state.staff.reduce((sum,s)=>sum+staffWeeklyPay(s),0)
  const totalMonthly  = state.staff.reduce((sum,s)=>sum+staffMonthlyCost(s),0)
  const avgHours      = state.staff.length ? (state.staff.reduce((s,x)=>s+(x.hoursThisWeek||0),0)/state.staff.length).toFixed(1) : 0

  return `<div class="page-scroll page">

  <!-- KPI row -->
  <div class="grid4 mb">
    <div class="kpi">
      <div class="kpi-label">Total Staff</div>
      <div class="kpi-val">${state.staff.length}</div>
    </div>
    <div class="kpi">
      <div class="kpi-label">Weekly Wage Bill</div>
      <div class="kpi-val" style="color:var(--red)">${cur(totalWeekly)}</div>
    </div>
    <div class="kpi">
      <div class="kpi-label">Monthly Wage Bill</div>
      <div class="kpi-val" style="color:var(--red)">${cur(totalMonthly)}</div>
    </div>
    <div class="kpi">
      <div class="kpi-label">Avg Hours / Week</div>
      <div class="kpi-val">${avgHours}h</div>
    </div>
  </div>

  <!-- Staff cards -->
  <div class="grid2 gap mb">
    ${state.staff.map(s=>{
      const weekly = staffWeeklyPay(s)
      const monthly = staffMonthlyCost(s)
      const salLabel = s.salaryType==='monthly'
        ? `${cur(s.monthlySalary||0)}/mo`
        : s.salaryType==='fixed_weekly'
        ? `${cur(s.weeklyRate||0)}/wk`
        : `${cur(s.hourlyRate||0)}/hr`
      const salIcon = s.salaryType==='monthly' ? '📅' : s.salaryType==='fixed_weekly' ? '🗓️' : '⏱️'
      return `
      <div class="staff-card">
        <div class="staff-avatar" style="background:${s.color}22;color:${s.color}">
          ${s.name.split(' ').map(n=>n[0]).join('')}
        </div>
        <div class="staff-info">
          <div class="staff-name">${s.name}</div>
          <div class="staff-role">${s.role} · ${s.phone||'—'}</div>
          <div class="flex gap-sm mt-sm" style="align-items:center;flex-wrap:wrap">
            <span class="badge badge-green">${s.hoursThisWeek||0}h this week</span>
            <span class="badge badge-purple">${salIcon} ${salLabel}</span>
            <span class="badge badge-orange">~${cur(weekly)} this week</span>
          </div>
          ${s.notes?`<div style="font-size:11px;color:var(--text3);margin-top:6px;font-style:italic">📝 ${s.notes}</div>`:''}
        </div>
        <div class="flex col gap-sm">
          <button class="btn btn-ghost btn-xs" onclick="editStaff(${s.id})">✏ Edit</button>
          <button class="btn btn-primary btn-xs" onclick="openSalaryModal(${s.id})">💰 Salary</button>
          <button class="btn btn-ghost btn-xs" onclick="logHours(${s.id})">⏱ Hours</button>
          <button class="btn btn-danger btn-xs" onclick="deleteStaff(${s.id})">✕</button>
        </div>
      </div>`}).join('')}
  </div>

  <!-- Salary table -->
  <div class="sh mt"><div class="sh-title">💰 Salary & Wages Overview</div></div>
  <div class="tbl-wrap mt-sm">
    <table class="tbl">
      <thead><tr>
        <th>Name</th><th>Role</th><th>Salary Type</th><th>Rate</th>
        <th>Hours/Week</th><th>Weekly Pay</th><th>Monthly Cost</th><th>Actions</th>
      </tr></thead>
      <tbody>
        ${state.staff.map(s=>{
          const weekly  = staffWeeklyPay(s)
          const monthly = staffMonthlyCost(s)
          const typeLabel = s.salaryType==='monthly' ? '📅 Monthly' : s.salaryType==='fixed_weekly' ? '🗓️ Fixed Weekly' : '⏱️ Hourly'
          const rateStr   = s.salaryType==='monthly'
            ? cur(s.monthlySalary||0)+'/mo'
            : s.salaryType==='fixed_weekly'
            ? cur(s.weeklyRate||0)+'/wk'
            : cur(s.hourlyRate||0)+'/hr'
          return `<tr>
            <td>
              <div class="flex gap-sm" style="align-items:center">
                <div style="width:34px;height:34px;border-radius:50%;background:${s.color}22;color:${s.color};display:flex;align-items:center;justify-content:center;font-weight:800;font-size:12px;flex-shrink:0">
                  ${s.name.split(' ').map(n=>n[0]).join('')}
                </div>
                <div>
                  <div style="font-weight:700;font-size:13px">${s.name}</div>
                  <div style="font-size:11px;color:var(--text3)">${s.phone||'—'}</div>
                </div>
              </div>
            </td>
            <td><span class="badge badge-blue">${s.role}</span></td>
            <td><span class="badge badge-purple">${typeLabel}</span></td>
            <td style="font-family:'DM Mono',monospace;font-weight:600;color:var(--accent)">${rateStr}</td>
            <td>
              <div class="flex gap-sm" style="align-items:center">
                <div class="progress-wrap" style="width:64px">
                  <div class="progress-bar" style="width:${Math.min(100,((s.hoursThisWeek||0)/48)*100).toFixed(0)}%;background:var(--green)"></div>
                </div>
                <span style="font-family:'DM Mono',monospace;font-size:12px">${s.hoursThisWeek||0}h</span>
              </div>
            </td>
            <td style="font-family:'DM Mono',monospace;font-weight:700;color:var(--accent)">${cur(weekly)}</td>
            <td style="font-family:'DM Mono',monospace;font-weight:700;color:var(--red)">${cur(monthly)}</td>
            <td>
              <div class="flex gap-sm">
                <button class="btn btn-primary btn-xs" onclick="openSalaryModal(${s.id})">💰 Edit Salary</button>
                <button class="btn btn-ghost btn-xs" onclick="logHours(${s.id})">⏱ Hours</button>
              </div>
            </td>
          </tr>`}).join('')}
        <tr style="background:var(--surface2)">
          <td colspan="5" style="font-weight:700;text-align:right;padding-right:16px;font-size:13px">Totals:</td>
          <td style="font-family:'DM Mono',monospace;font-weight:800;color:var(--accent)">${cur(totalWeekly)}</td>
          <td style="font-family:'DM Mono',monospace;font-weight:800;color:var(--red)">${cur(totalMonthly)}</td>
          <td></td>
        </tr>
      </tbody>
    </table>
  </div>

  <!-- ── ADD / EDIT STAFF MODAL ─────────────────────────── -->
  <div class="overlay" id="staff-modal" style="display:none">
    <div class="modal">
      <div class="modal-head">
        <div class="modal-title" id="staff-modal-title">Add Staff Member</div>
        <button class="btn btn-ghost btn-sm" onclick="closeModal('staff-modal')">✕</button>
      </div>
      <div class="modal-body">
        <input type="hidden" id="staff-id"/>
        <div class="form-row cols2">
          <div class="form-group">
            <label class="form-label">Full Name</label>
            <input class="form-input" id="staff-name" placeholder="Alex Rivera"/>
          </div>
          <div class="form-group">
            <label class="form-label">Role</label>
            <select class="form-input" id="staff-role">
              <option>Head Barista</option><option>Barista</option><option>Cashier</option>
              <option>Kitchen</option><option>Server</option><option>Manager</option><option>Cleaner</option>
            </select>
          </div>
        </div>
        <div class="form-row cols2">
          <div class="form-group">
            <label class="form-label">Phone</label>
            <input class="form-input" id="staff-phone" placeholder="+974 5000-0100"/>
          </div>
          <div class="form-group">
            <label class="form-label">Hours This Week</label>
            <input class="form-input" type="number" id="staff-hours" placeholder="0" step="0.5"/>
          </div>
        </div>
        <div class="form-group">
          <label class="form-label">Notes (optional)</label>
          <input class="form-input" id="staff-notes" placeholder="e.g. Part-time, morning shift only"/>
        </div>
      </div>
      <div class="modal-foot">
        <button class="btn btn-ghost" onclick="closeModal('staff-modal')">Cancel</button>
        <button class="btn btn-primary" onclick="saveStaff()">Save Member</button>
      </div>
    </div>
  </div>

  <!-- ── SALARY EDIT MODAL ──────────────────────────────── -->
  <div class="overlay" id="salary-modal" style="display:none">
    <div class="modal" style="max-width:480px">
      <div class="modal-head">
        <div class="modal-title" id="salary-modal-title">💰 Edit Salary</div>
        <button class="btn btn-ghost btn-sm" onclick="closeModal('salary-modal')">✕</button>
      </div>
      <div class="modal-body">
        <input type="hidden" id="salary-staff-id"/>

        <!-- staff summary strip -->
        <div id="salary-staff-info" style="background:var(--surface2);border-radius:var(--r2);padding:12px 14px;margin-bottom:18px;display:flex;align-items:center;gap:12px">
          <div id="salary-avatar" style="width:40px;height:40px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:800;font-size:14px;flex-shrink:0"></div>
          <div>
            <div id="salary-name" style="font-weight:700;font-size:14px"></div>
            <div id="salary-role" style="font-size:12px;color:var(--text3)"></div>
          </div>
        </div>

        <div class="form-group mb">
          <label class="form-label">Salary / Payment Type</label>
          <select class="form-input" id="salary-type" onchange="toggleSalaryFields()">
            <option value="hourly">⏱️ Hourly Rate</option>
            <option value="monthly">📅 Fixed Monthly Salary</option>
            <option value="fixed_weekly">🗓️ Fixed Weekly Rate</option>
          </select>
        </div>

        <!-- Hourly fields -->
        <div id="salary-hourly-fields">
          <div class="form-row cols2">
            <div class="form-group">
              <label class="form-label">Hourly Rate (QR)</label>
              <input class="form-input" type="number" id="salary-hourly-rate" step="0.5" placeholder="50"/>
            </div>
            <div class="form-group">
              <label class="form-label">Expected Hours / Week</label>
              <input class="form-input" type="number" id="salary-expected-hours" step="0.5" placeholder="40"/>
            </div>
          </div>
          <div id="salary-hourly-preview" style="background:var(--surface2);border-radius:var(--r2);padding:12px 14px;font-size:13px;color:var(--text2)">
            Enter rate and hours to see preview
          </div>
        </div>

        <!-- Monthly fields -->
        <div id="salary-monthly-fields" style="display:none">
          <div class="form-group">
            <label class="form-label">Monthly Salary (QR)</label>
            <input class="form-input" type="number" id="salary-monthly-val" step="50" placeholder="3000"
              oninput="updateMonthlyPreview()"/>
          </div>
          <div id="salary-monthly-preview" style="background:var(--surface2);border-radius:var(--r2);padding:12px 14px;font-size:13px;color:var(--text2)">
            Enter salary to see breakdown
          </div>
        </div>

        <!-- Fixed weekly fields -->
        <div id="salary-weekly-fields" style="display:none">
          <div class="form-group">
            <label class="form-label">Fixed Weekly Rate (QR)</label>
            <input class="form-input" type="number" id="salary-weekly-val" step="25" placeholder="700"
              oninput="updateWeeklyPreview()"/>
          </div>
          <div id="salary-weekly-preview" style="background:var(--surface2);border-radius:var(--r2);padding:12px 14px;font-size:13px;color:var(--text2)">
            Enter weekly rate to see breakdown
          </div>
        </div>

        <div class="form-group mt" style="margin-top:14px">
          <label class="form-label">Salary Notes (optional)</label>
          <input class="form-input" id="salary-notes-field" placeholder="e.g. Includes housing allowance"/>
        </div>
      </div>
      <div class="modal-foot">
        <button class="btn btn-ghost" onclick="closeModal('salary-modal')">Cancel</button>
        <button class="btn btn-primary" onclick="saveSalary()">💾 Save Salary</button>
      </div>
    </div>
  </div>

  <!-- ── LOG HOURS MODAL ────────────────────────────────── -->
  <div class="overlay" id="hours-modal" style="display:none">
    <div class="modal" style="max-width:360px">
      <div class="modal-head">
        <div class="modal-title" id="hours-title">⏱ Log Hours</div>
        <button class="btn btn-ghost btn-sm" onclick="closeModal('hours-modal')">✕</button>
      </div>
      <div class="modal-body">
        <input type="hidden" id="hours-staff-id"/>
        <div class="form-group">
          <label class="form-label">Hours Worked This Week</label>
          <input class="form-input" type="number" id="hours-val" step="0.5" placeholder="0"/>
        </div>
        <div id="hours-pay-preview" style="background:var(--surface2);border-radius:var(--r2);padding:12px 14px;font-size:13px;color:var(--text2);margin-top:8px"></div>
      </div>
      <div class="modal-foot">
        <button class="btn btn-ghost" onclick="closeModal('hours-modal')">Cancel</button>
        <button class="btn btn-primary" onclick="saveHours()">Update Hours</button>
      </div>
    </div>
  </div>

</div>`
}

// ── Salary modal helpers ─────────────────────────────────────
function toggleSalaryFields(){
  const type = document.getElementById('salary-type').value
  document.getElementById('salary-hourly-fields').style.display  = type==='hourly'       ?'block':'none'
  document.getElementById('salary-monthly-fields').style.display = type==='monthly'      ?'block':'none'
  document.getElementById('salary-weekly-fields').style.display  = type==='fixed_weekly' ?'block':'none'
}

function updateHourlyPreview(){
  const rate  = parseFloat(document.getElementById('salary-hourly-rate').value)||0
  const hours = parseFloat(document.getElementById('salary-expected-hours').value)||0
  const weekly  = rate*hours
  const monthly = weekly*4.33
  const el = document.getElementById('salary-hourly-preview')
  if(!rate||!hours){ el.textContent='Enter rate and hours to see preview'; return }
  el.innerHTML = `<div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px;text-align:center">
    <div><div style="font-size:10px;text-transform:uppercase;letter-spacing:1px;color:var(--text3);margin-bottom:4px">Per Hour</div>
      <div style="font-family:'DM Mono',monospace;font-weight:700;font-size:15px;color:var(--accent)">QR ${rate.toFixed(2)}</div></div>
    <div><div style="font-size:10px;text-transform:uppercase;letter-spacing:1px;color:var(--text3);margin-bottom:4px">Per Week</div>
      <div style="font-family:'DM Mono',monospace;font-weight:700;font-size:15px;color:var(--blue)">QR ${weekly.toFixed(2)}</div></div>
    <div><div style="font-size:10px;text-transform:uppercase;letter-spacing:1px;color:var(--text3);margin-bottom:4px">Per Month</div>
      <div style="font-family:'DM Mono',monospace;font-weight:700;font-size:15px;color:var(--red)">QR ${monthly.toFixed(2)}</div></div>
  </div>`
}

function updateMonthlyPreview(){
  const monthly = parseFloat(document.getElementById('salary-monthly-val').value)||0
  const weekly  = monthly/4.33
  const daily   = monthly/30
  const el = document.getElementById('salary-monthly-preview')
  if(!monthly){ el.textContent='Enter salary to see breakdown'; return }
  el.innerHTML = `<div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px;text-align:center">
    <div><div style="font-size:10px;text-transform:uppercase;letter-spacing:1px;color:var(--text3);margin-bottom:4px">Per Day</div>
      <div style="font-family:'DM Mono',monospace;font-weight:700;font-size:15px;color:var(--green)">QR ${daily.toFixed(2)}</div></div>
    <div><div style="font-size:10px;text-transform:uppercase;letter-spacing:1px;color:var(--text3);margin-bottom:4px">Per Week</div>
      <div style="font-family:'DM Mono',monospace;font-weight:700;font-size:15px;color:var(--blue)">QR ${weekly.toFixed(2)}</div></div>
    <div><div style="font-size:10px;text-transform:uppercase;letter-spacing:1px;color:var(--text3);margin-bottom:4px">Per Month</div>
      <div style="font-family:'DM Mono',monospace;font-weight:700;font-size:15px;color:var(--red)">QR ${monthly.toFixed(2)}</div></div>
  </div>`
}

function updateWeeklyPreview(){
  const weekly  = parseFloat(document.getElementById('salary-weekly-val').value)||0
  const monthly = weekly*4.33
  const daily   = weekly/7
  const el = document.getElementById('salary-weekly-preview')
  if(!weekly){ el.textContent='Enter weekly rate to see breakdown'; return }
  el.innerHTML = `<div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:12px;text-align:center">
    <div><div style="font-size:10px;text-transform:uppercase;letter-spacing:1px;color:var(--text3);margin-bottom:4px">Per Day</div>
      <div style="font-family:'DM Mono',monospace;font-weight:700;font-size:15px;color:var(--green)">QR ${daily.toFixed(2)}</div></div>
    <div><div style="font-size:10px;text-transform:uppercase;letter-spacing:1px;color:var(--text3);margin-bottom:4px">Per Week</div>
      <div style="font-family:'DM Mono',monospace;font-weight:700;font-size:15px;color:var(--blue)">QR ${weekly.toFixed(2)}</div></div>
    <div><div style="font-size:10px;text-transform:uppercase;letter-spacing:1px;color:var(--text3);margin-bottom:4px">Per Month</div>
      <div style="font-family:'DM Mono',monospace;font-weight:700;font-size:15px;color:var(--red)">QR ${monthly.toFixed(2)}</div></div>
  </div>`
}

// ── Open Salary Modal ────────────────────────────────────────
function openSalaryModal(id){
  const s = state.staff.find(x=>x.id===id); if(!s)return
  document.getElementById('salary-staff-id').value = id
  document.getElementById('salary-modal-title').textContent = `💰 Salary — ${s.name}`
  document.getElementById('salary-name').textContent = s.name
  document.getElementById('salary-role').textContent = s.role
  const av = document.getElementById('salary-avatar')
  av.textContent = s.name.split(' ').map(n=>n[0]).join('')
  av.style.background = s.color+'22'
  av.style.color = s.color
  // Pre-fill
  const type = s.salaryType||'hourly'
  document.getElementById('salary-type').value = type
  document.getElementById('salary-hourly-rate').value  = s.hourlyRate||''
  document.getElementById('salary-expected-hours').value = s.hoursThisWeek||''
  document.getElementById('salary-monthly-val').value  = s.monthlySalary||''
  document.getElementById('salary-weekly-val').value   = s.weeklyRate||''
  document.getElementById('salary-notes-field').value  = s.salaryNotes||''
  toggleSalaryFields()
  // wire up live preview for hourly
  setTimeout(()=>{
    const rateEl  = document.getElementById('salary-hourly-rate')
    const hoursEl = document.getElementById('salary-expected-hours')
    if(rateEl)  rateEl.addEventListener('input', updateHourlyPreview)
    if(hoursEl) hoursEl.addEventListener('input', updateHourlyPreview)
    updateHourlyPreview()
    updateMonthlyPreview()
    updateWeeklyPreview()
  }, 50)
  openModal('salary-modal')
}

function saveSalary(){
  const id   = parseInt(document.getElementById('salary-staff-id').value)
  const type = document.getElementById('salary-type').value
  const s    = state.staff.find(x=>x.id===id); if(!s)return
  s.salaryType   = type
  s.salaryNotes  = document.getElementById('salary-notes-field').value
  if(type==='hourly'){
    s.hourlyRate  = parseFloat(document.getElementById('salary-hourly-rate').value)||0
    s.hoursThisWeek = parseFloat(document.getElementById('salary-expected-hours').value)||s.hoursThisWeek
    s.monthlySalary = null; s.weeklyRate = null
  } else if(type==='monthly'){
    s.monthlySalary = parseFloat(document.getElementById('salary-monthly-val').value)||0
    s.hourlyRate = null; s.weeklyRate = null
  } else {
    s.weeklyRate   = parseFloat(document.getElementById('salary-weekly-val').value)||0
    s.hourlyRate = null; s.monthlySalary = null
  }
  saveAll(); closeModal('salary-modal')
  toast(`${s.name}'s salary updated!`, 'success')
  render()
}

// ── Staff CRUD ───────────────────────────────────────────────
function openAddStaff(){
  ['staff-id','staff-name','staff-phone','staff-hours','staff-notes'].forEach(id=>{
    const el=document.getElementById(id); if(el) el.value=''
  })
  document.getElementById('staff-modal-title').textContent='Add Staff Member'
  openModal('staff-modal')
}
function editStaff(id){
  const s=state.staff.find(x=>x.id===id); if(!s)return
  document.getElementById('staff-id').value    = id
  document.getElementById('staff-name').value  = s.name
  document.getElementById('staff-role').value  = s.role
  document.getElementById('staff-phone').value = s.phone||''
  document.getElementById('staff-hours').value = s.hoursThisWeek||0
  document.getElementById('staff-notes').value = s.notes||''
  document.getElementById('staff-modal-title').textContent='Edit Staff Member'
  openModal('staff-modal')
}
function saveStaff(){
  const id = parseInt(document.getElementById('staff-id').value)||null
  const data = {
    name:  document.getElementById('staff-name').value.trim(),
    role:  document.getElementById('staff-role').value,
    phone: document.getElementById('staff-phone').value||'—',
    hoursThisWeek: parseFloat(document.getElementById('staff-hours').value)||0,
    notes: document.getElementById('staff-notes').value,
  }
  if(!data.name){ toast('Name is required','error'); return }
  if(id){
    const idx=state.staff.findIndex(x=>x.id===id)
    if(idx>=0) state.staff[idx]={...state.staff[idx],...data}
  } else {
    state.staff.push({
      ...data, id:Date.now(),
      salaryType:'hourly', hourlyRate:45,
      color:['#c47d1a','#2472c8','#2a9d4e','#6d4fc4','#c4306e','#d94040'][Math.floor(Math.random()*6)]
    })
  }
  closeModal('staff-modal'); saveAll()
  toast(id?'Staff member updated!':'Staff member added!','success')
  render()
}

function logHours(id){
  const s=state.staff.find(x=>x.id===id); if(!s)return
  document.getElementById('hours-staff-id').value = id
  document.getElementById('hours-val').value       = s.hoursThisWeek||0
  document.getElementById('hours-title').textContent = `⏱ Hours — ${s.name}`
  // Show pay preview
  const rate = s.hourlyRate||0
  const prev = document.getElementById('hours-pay-preview')
  if(s.salaryType==='monthly'){
    prev.innerHTML = `<span style="color:var(--text3)">Monthly salary — hours for attendance only</span>`
  } else if(s.salaryType==='fixed_weekly'){
    prev.innerHTML = `<span style="color:var(--text3)">Fixed weekly rate — hours for attendance only</span>`
  } else {
    prev.innerHTML = `Rate: <strong>QR ${rate}/hr</strong> — update hours to recalculate pay`
    document.getElementById('hours-val').addEventListener('input',function(){
      const h=parseFloat(this.value)||0
      prev.innerHTML = `Rate: <strong>QR ${rate}/hr</strong> · <strong>${h}h</strong> = <strong style="color:var(--accent)">QR ${(rate*h).toFixed(2)}</strong> this week`
    })
  }
  openModal('hours-modal')
}
function saveHours(){
  const id = parseInt(document.getElementById('hours-staff-id').value)
  const h  = parseFloat(document.getElementById('hours-val').value)||0
  const s  = state.staff.find(x=>x.id===id)
  if(s){ s.hoursThisWeek=h; saveAll(); toast('Hours updated!','success'); closeModal('hours-modal'); render() }
}
function deleteStaff(id){
  if(!confirm('Remove this staff member?')) return
  state.staff=state.staff.filter(s=>s.id!==id); saveAll(); render()
}

// ═══════════════════════════════════════════════════════════════
// REPORTS
// ═══════════════════════════════════════════════════════════════
function renderReports(){
  const totalRevenue = state.orders.filter(o=>o.status!=='cancelled').reduce((s,o)=>s+o.total,0)
  const totalCOGS = state.orders.filter(o=>o.status!=='cancelled').reduce((s,o)=>s+(o.cost||0),0)
  const totalExpenses = state.expenses.reduce((s,e)=>s+e.amount,0)
  const totalWages = state.staff.reduce((s,st)=>s+st.hourlyRate*st.hoursThisWeek,0)
  const grossProfit = totalRevenue - totalCOGS
  const netProfit = grossProfit - totalExpenses
  const margin = totalRevenue>0?(netProfit/totalRevenue*100):0

  const itemSales = {}
  state.orders.filter(o=>o.status!=='cancelled').forEach(o=>{
    (o.items||[]).forEach(i=>{
      if(!itemSales[i.name]) itemSales[i.name]={qty:0,revenue:0,cost:0,emoji:i.emoji}
      itemSales[i.name].qty+=i.qty
      itemSales[i.name].revenue+=i.price*i.qty
      itemSales[i.name].cost+=(i.cost||0)*i.qty
    })
  })
  const topItems = Object.entries(itemSales).sort((a,b)=>b[1].revenue-a[1].revenue).slice(0,8)

  const ordersByType = {}
  state.orders.forEach(o=>{ ordersByType[o.type||'Dine In']=(ordersByType[o.type||'Dine In']||0)+1 })

  return `<div class="page-scroll page">
  <div class="grid4 mb">
    <div class="kpi">
      <div class="kpi-glow" style="background:var(--accent)"></div>
      <div class="kpi-label">Total Revenue</div>
      <div class="kpi-val">${cur(totalRevenue)}</div>
      <div class="kpi-sub">${state.orders.filter(o=>o.status!=='cancelled').length} completed orders</div>
    </div>
    <div class="kpi">
      <div class="kpi-glow" style="background:var(--red)"></div>
      <div class="kpi-label">Total Expenses</div>
      <div class="kpi-val" style="color:var(--red)">${cur(totalExpenses)}</div>
      <div class="kpi-sub">All logged expenses</div>
    </div>
    <div class="kpi">
      <div class="kpi-glow" style="background:var(--green)"></div>
      <div class="kpi-label">Net Profit</div>
      <div class="kpi-val" style="color:${netProfit>=0?'var(--green)':'var(--red)'}">${cur(netProfit)}</div>
      <div class="kpi-sub">After all expenses</div>
    </div>
    <div class="kpi">
      <div class="kpi-glow" style="background:var(--blue)"></div>
      <div class="kpi-label">Profit Margin</div>
      <div class="kpi-val" style="color:${margin>20?'var(--green)':margin>0?'var(--accent)':'var(--red)'}">${margin.toFixed(1)}%</div>
      <div class="kpi-sub">Net / Revenue</div>
    </div>
  </div>

  <div class="grid2 gap mb">
    <div class="card">
      <div class="sh"><div class="sh-title">💰 Profit & Loss Summary</div></div>
      <div class="stat-row"><span class="stat-label">Total Revenue</span><span class="stat-val" style="color:var(--green)">${cur(totalRevenue)}</span></div>
      <div class="stat-row"><span class="stat-label">Cost of Goods Sold</span><span class="stat-val" style="color:var(--red)">−${cur(totalCOGS)}</span></div>
      <div class="stat-row" style="font-weight:700"><span class="stat-label">Gross Profit</span><span class="stat-val" style="color:var(--accent)">${cur(grossProfit)}</span></div>
      <div class="stat-row"><span class="stat-label">Operating Expenses</span><span class="stat-val" style="color:var(--red)">−${cur(totalExpenses)}</span></div>
      <div class="stat-row"><span class="stat-label">Staff Wages (this week)</span><span class="stat-val" style="color:var(--red)">−${cur(totalWages)}</span></div>
      <div class="stat-row" style="border-top:2px solid var(--border2);padding-top:14px;margin-top:4px">
        <span style="font-family:'Syne',sans-serif;font-weight:700;font-size:15px">Net Profit</span>
        <span style="font-family:'DM Mono',monospace;font-size:17px;font-weight:700;color:${netProfit>=0?'var(--green)':'var(--red)'}">${cur(netProfit)}</span>
      </div>
    </div>

    <div class="card">
      <div class="sh"><div class="sh-title">🥧 Orders by Type</div></div>
      ${Object.entries(ordersByType).map(([type,count])=>`
        <div class="stat-row">
          <div class="flex gap-sm" style="align-items:center">
            <span>${type==='Dine In'?'🪑':type==='Takeaway'?'🥡':'🚴'}</span>
            <span class="stat-label">${type}</span>
          </div>
          <div class="flex gap-sm" style="align-items:center">
            <div class="progress-wrap" style="width:80px"><div class="progress-bar" style="width:${(count/state.orders.length*100).toFixed(0)}%;background:var(--blue)"></div></div>
            <span style="font-family:'DM Mono',monospace">${count}</span>
          </div>
        </div>`).join('')||'<div style="color:var(--text3);font-size:13px">No orders yet</div>'}
      <div class="stat-row mt">
        <span class="stat-label">Avg Order Value</span>
        <span class="stat-val">${cur(state.orders.length?totalRevenue/state.orders.filter(o=>o.status!=='cancelled').length:0)}</span>
      </div>
    </div>
  </div>

  <div class="sh"><div class="sh-title">🏆 Menu Item Performance</div></div>
  <div class="tbl-wrap">
    <table class="tbl">
      <thead><tr><th>Item</th><th>Units Sold</th><th>Revenue</th><th>COGS</th><th>Gross Profit</th><th>Margin</th></tr></thead>
      <tbody>
        ${topItems.length?topItems.map(([name,d])=>{
          const profit=d.revenue-d.cost
          const m=d.revenue>0?(profit/d.revenue*100):0
          return `<tr>
            <td><div class="flex gap-sm" style="align-items:center"><span style="font-size:18px">${d.emoji||'☕'}</span><span style="font-weight:600">${name}</span></div></td>
            <td style="font-family:'DM Mono',monospace">${d.qty}</td>
            <td style="font-family:'DM Mono',monospace;color:var(--green)">${cur(d.revenue)}</td>
            <td style="font-family:'DM Mono',monospace;color:var(--red)">${cur(d.cost)}</td>
            <td style="font-family:'DM Mono',monospace;font-weight:700;color:var(--accent)">${cur(profit)}</td>
            <td>
              <div class="flex gap-sm" style="align-items:center">
                <div class="progress-wrap" style="width:60px"><div class="progress-bar" style="width:${m}%;background:${m>50?'var(--green)':m>30?'var(--accent)':'var(--red)'}"></div></div>
                <span style="font-size:12px;color:${m>50?'var(--green)':m>30?'var(--accent)':'var(--red)'}">${m.toFixed(0)}%</span>
              </div>
            </td>
          </tr>`}).join(''):`<tr><td colspan="6" style="text-align:center;color:var(--text3);padding:24px">No sales data yet. Start taking orders to see performance data.</td></tr>`}
      </tbody>
    </table>
  </div>
</div>`
}

// ═══════════════════════════════════════════════════════════════
// SETTINGS
// ═══════════════════════════════════════════════════════════════
function openSettings(){
  document.getElementById('setting-cafe-name').value = state.settings.name
  document.getElementById('setting-currency').value = state.settings.currency
  document.getElementById('setting-tax').value = state.settings.tax
  document.getElementById('setting-receipt').value = state.settings.receipt
  openModal('settings-modal')
}
function saveSettings(){
  state.settings.name = document.getElementById('setting-cafe-name').value||'My Café'
  state.settings.currency = document.getElementById('setting-currency').value||'QR '
  state.settings.tax = parseFloat(document.getElementById('setting-tax').value)||0
  state.settings.receipt = document.getElementById('setting-receipt').value
  saveAll()
  closeModal('settings-modal')
  toast('Settings saved!','success')
  render()
}

// ═══════════════════════════════════════════════════════════════
// AUTH — Login / Session
// ═══════════════════════════════════════════════════════════════

// Built-in users list (saved in localStorage so admin can manage)
const DEFAULT_USERS = [
  { id:1, username:'admin',   password:'admin123',  name:'Admin',        role:'Owner / Admin',  color:'#c47d1a', canAccess:'all' },
  { id:2, username:'manager', password:'manager1',  name:'Manager',      role:'Manager',        color:'#2472c8', canAccess:'all' },
  { id:3, username:'barista', password:'barista1',  name:'Barista',      role:'Barista',        color:'#2a9d4e', canAccess:'pos,orders' },
  { id:4, username:'cashier', password:'cashier1',  name:'Cashier',      role:'Cashier',        color:'#6d4fc4', canAccess:'pos,orders' },
]

function getUsers(){
  return DB.load('users', DEFAULT_USERS)
}

let currentUser = null

// ── Render login chips ────────────────────────────────────────
function renderLoginChips(){
  const users = getUsers()
  const container = document.getElementById('login-chips')
  if(!container) return
  container.innerHTML = users.map(u=>`
    <div class="login-user-chip" onclick="fillLogin('${u.username}','${u.password}')">
      <div class="login-chip-avatar" style="background:${u.color}22;color:${u.color}">${u.name[0]}</div>
      <div>
        <div class="login-chip-name">${u.name}</div>
        <span class="login-chip-role">${u.role}</span>
      </div>
      <span class="login-chip-pw">pw: ${u.password}</span>
    </div>`).join('')
}

function fillLogin(username, password){
  document.getElementById('login-username').value = username
  document.getElementById('login-password').value = password
  document.getElementById('login-username').classList.remove('error')
  document.getElementById('login-password').classList.remove('error')
  document.getElementById('login-error').classList.remove('show')
  document.getElementById('login-password').focus()
}

function toggleLoginPw(){
  const inp = document.getElementById('login-password')
  const btn = document.getElementById('login-eye-btn')
  if(inp.type==='password'){ inp.type='text'; btn.textContent='🙈' }
  else { inp.type='password'; btn.textContent='👁' }
}

// ── Attempt login ─────────────────────────────────────────────
function doLogin(){
  const username = document.getElementById('login-username').value.trim().toLowerCase()
  const password = document.getElementById('login-password').value
  const errEl    = document.getElementById('login-error')
  const errMsg   = document.getElementById('login-error-msg')
  const btn      = document.getElementById('login-btn')

  // Clear previous errors
  errEl.classList.remove('show')
  document.getElementById('login-username').classList.remove('error')
  document.getElementById('login-password').classList.remove('error')

  if(!username){ showLoginError('Please enter your username.'); document.getElementById('login-username').classList.add('error'); return }
  if(!password){ showLoginError('Please enter your password.');  document.getElementById('login-password').classList.add('error'); return }

  btn.textContent = 'Signing in…'
  btn.disabled = true

  setTimeout(()=>{
    const users = getUsers()
    const user  = users.find(u => u.username.toLowerCase()===username && u.password===password)

    if(!user){
      btn.textContent = 'Sign In →'
      btn.disabled = false
      document.getElementById('login-username').classList.add('error')
      document.getElementById('login-password').classList.add('error')
      showLoginError('Incorrect username or password. Please try again.')
      document.getElementById('login-password').value = ''
      document.getElementById('login-password').focus()
      return
    }

    // Success — store session
    currentUser = user
    DB.save('session', { userId: user.id, loginTime: Date.now() })
    mountApp(user)
  }, 600)
}

function showLoginError(msg){
  const el = document.getElementById('login-error-msg')
  const wrap = document.getElementById('login-error')
  if(el) el.textContent = msg
  if(wrap) wrap.classList.add('show')
}

// ── Mount app after login ─────────────────────────────────────
function mountApp(user){
  // Hide login screen with fade
  const ls = document.getElementById('login-screen')
  ls.style.transition = 'opacity 0.4s ease'
  ls.style.opacity = '0'
  setTimeout(()=>{ ls.style.display='none' }, 400)

  // Update topbar user pill
  const avatar = document.getElementById('topbar-avatar')
  if(avatar){
    avatar.textContent = user.name[0]
    avatar.style.background = user.color+'22'
    avatar.style.color = user.color
  }
  document.getElementById('topbar-uname').textContent = user.name
  document.getElementById('topbar-urole').textContent = user.role

  toast(`Welcome back, ${user.name}! ☕`, 'success')
  render()
}

// ── Logout ────────────────────────────────────────────────────
function confirmLogout(){
  if(!confirm(`Sign out as ${currentUser?.name}?`)) return
  doLogout()
}

function doLogout(){
  currentUser = null
  DB.save('session', null)
  // Reset login form
  document.getElementById('login-username').value = ''
  document.getElementById('login-password').value = ''
  document.getElementById('login-password').type = 'password'
  document.getElementById('login-eye-btn').textContent = '👁'
  document.getElementById('login-error').classList.remove('show')
  document.getElementById('login-username').classList.remove('error')
  document.getElementById('login-password').classList.remove('error')
  // Show login screen
  const ls = document.getElementById('login-screen')
  ls.style.display = 'flex'
  ls.style.opacity = '0'
  setTimeout(()=>{ ls.style.transition='opacity 0.35s ease'; ls.style.opacity='1' }, 10)
  toast('Signed out. See you soon! 👋', 'info')
}

// ── Check for existing session on load ───────────────────────
function checkSession(){
  const session = DB.load('session', null)
  if(!session || !session.userId) return false
  // Auto-expire after 12 hours
  if(Date.now() - session.loginTime > 12 * 60 * 60 * 1000){
    DB.save('session', null)
    return false
  }
  const users = getUsers()
  const user  = users.find(u=>u.id===session.userId)
  if(!user) return false
  currentUser = user
  return true
}

// ═══════════════════════════════════════════════════════════════
// INIT
// ═══════════════════════════════════════════════════════════════
renderLoginChips()

if(checkSession()){
  // Already logged in — skip login screen
  document.getElementById('login-screen').style.display = 'none'
  const avatar = document.getElementById('topbar-avatar')
  if(avatar){
    avatar.textContent = currentUser.name[0]
    avatar.style.background = currentUser.color+'22'
    avatar.style.color = currentUser.color
  }
  document.getElementById('topbar-uname').textContent = currentUser.name
  document.getElementById('topbar-urole').textContent = currentUser.role
  render()
} else {
  // Show login — hide main app until logged in
  document.getElementById('app').style.display = 'none'
  // Reveal app when login succeeds (handled in mountApp)
  const _origMountApp = mountApp
  window.mountApp = function(user){
    document.getElementById('app').style.display = 'flex'
    _origMountApp(user)
  }
  // Focus username field
  setTimeout(()=>{ const el=document.getElementById('login-username'); if(el) el.focus() }, 100)
}
</script>
</body>
</html>
