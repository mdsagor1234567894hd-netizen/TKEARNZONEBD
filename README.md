<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>TK EARN ZONE BD </title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700;800&family=Rajdhani:wght@600;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
<!-- Firebase -->
<script src="https://www.gstatic.com/firebasejs/10.12.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.0/firebase-auth-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore-compat.js"></script>
<style>
:root {
  --primary: #FF6B00;
  --primary-dark: #e05e00;
  --primary-light: #ff8c35;
  --bg: #f4f6fb;
  --card: #ffffff;
  --text: #1a1a2e;
  --text-muted: #6b7280;
  --border: #e8ecf4;
  --success: #22c55e;
  --danger: #ef4444;
  --warning: #f59e0b;
  --shadow: 0 4px 24px rgba(255,107,0,0.10);
  --shadow-card: 0 2px 12px rgba(0,0,0,0.07);
  --radius: 16px;
  --radius-sm: 10px;
}

* { margin:0; padding:0; box-sizing:border-box; -webkit-tap-highlight-color:transparent; }

body {
  font-family: 'Poppins', sans-serif;
  background: var(--bg);
  color: var(--text);
  min-height: 100vh;
  max-width: 480px;
  margin: 0 auto;
  position: relative;
  overflow-x: hidden;
}

/* ===== TOPBAR ===== */
.topbar {
  background: linear-gradient(135deg, var(--primary) 0%, var(--primary-light) 100%);
  padding: 14px 18px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: sticky;
  top: 0;
  z-index: 100;
  box-shadow: 0 4px 20px rgba(255,107,0,0.3);
}
.topbar-logo {
  font-family: 'Rajdhani', sans-serif;
  font-size: 22px;
  font-weight: 700;
  color: #fff;
  letter-spacing: 1.5px;
  display: flex;
  align-items: center;
  gap: 8px;
}
.topbar-logo .logo-icon {
  width: 32px; height: 32px;
  background: rgba(255,255,255,0.2);
  border-radius: 8px;
  display: flex; align-items: center; justify-content: center;
  font-size: 16px;
  color: #fff;
}
.topbar-btn {
  width: 38px; height: 38px;
  background: rgba(255,255,255,0.2);
  border: none; border-radius: 10px;
  color: #fff; font-size: 16px;
  cursor: pointer;
  display: flex; align-items: center; justify-content: center;
  transition: all 0.2s;
}
.topbar-btn:hover { background: rgba(255,255,255,0.3); }

/* ===== PAGES ===== */
.page { display: none; padding-bottom: 80px; }
.page.active { display: block; animation: fadeIn 0.3s ease; }
@keyframes fadeIn { from{opacity:0;transform:translateY(8px)} to{opacity:1;transform:translateY(0)} }

/* ===== BOTTOM NAV ===== */
.bottom-nav {
  position: fixed; bottom: 0; left: 50%; transform: translateX(-50%);
  width: 100%; max-width: 480px;
  background: #fff;
  border-top: 1px solid var(--border);
  display: flex; justify-content: space-around; align-items: center;
  padding: 8px 0 12px;
  z-index: 100;
  box-shadow: 0 -4px 20px rgba(0,0,0,0.08);
}
.nav-item {
  display: flex; flex-direction: column; align-items: center; gap: 3px;
  cursor: pointer; padding: 4px 12px; border-radius: 12px;
  transition: all 0.2s;
  background: none; border: none;
}
.nav-item .nav-icon {
  width: 28px; height: 28px;
  display: flex; align-items: center; justify-content: center;
  border-radius: 8px; font-size: 16px;
  color: var(--text-muted);
  transition: all 0.2s;
}
.nav-item span { font-size: 10px; font-weight: 600; color: var(--text-muted); transition: all 0.2s; }
.nav-item.active .nav-icon { color: var(--primary); background: rgba(255,107,0,0.1); }
.nav-item.active span { color: var(--primary); }

/* ===== HERO CARD ===== */
.hero-card {
  margin: 16px;
  background: linear-gradient(135deg, var(--primary) 0%, var(--primary-light) 100%);
  border-radius: 20px;
  padding: 20px;
  color: #fff;
  position: relative;
  overflow: hidden;
  box-shadow: 0 8px 30px rgba(255,107,0,0.35);
}
.hero-card::before {
  content:'';
  position: absolute; top:-40px; right:-40px;
  width: 160px; height: 160px;
  background: rgba(255,255,255,0.08);
  border-radius: 50%;
}
.hero-card::after {
  content:'';
  position: absolute; bottom:-30px; right:30px;
  width: 100px; height: 100px;
  background: rgba(255,255,255,0.05);
  border-radius: 50%;
}
.hero-user { display: flex; align-items: center; gap: 14px; margin-bottom: 16px; }
.hero-avatar {
  width: 56px; height: 56px; border-radius: 50%;
  background: rgba(255,255,255,0.25);
  display: flex; align-items: center; justify-content: center;
  font-size: 22px; border: 3px solid rgba(255,255,255,0.4);
  overflow: hidden; flex-shrink: 0;
}
.hero-avatar img { width:100%; height:100%; object-fit:cover; }
.hero-info h3 { font-size: 17px; font-weight: 700; }
.hero-meta { display: flex; gap: 10px; margin-top: 4px; flex-wrap: wrap; }
.hero-badge {
  font-size: 11px; font-weight: 500;
  background: rgba(255,255,255,0.2);
  padding: 2px 10px; border-radius: 20px;
  display: flex; align-items: center; gap: 4px;
}
.status-dot {
  width: 6px; height: 6px; border-radius: 50%;
  background: #4ade80;
  animation: pulse 1.5s infinite;
}
@keyframes pulse { 0%,100%{opacity:1} 50%{opacity:0.4} }
.hero-balance { display: flex; justify-content: space-between; align-items: center; }
.balance-label { font-size: 12px; opacity: 0.85; font-weight: 500; }
.balance-amount { font-family: 'Rajdhani', sans-serif; font-size: 28px; font-weight: 700; }

/* ===== NOTICE ===== */
.notice-bar {
  margin: 0 16px 16px;
  background: #fff3e8;
  border: 1px solid #ffd9b3;
  border-radius: 12px;
  padding: 10px 14px;
  display: flex; align-items: center; gap: 10px;
  font-size: 13px; color: var(--primary-dark);
}
.notice-bar .notice-label {
  background: var(--primary);
  color: #fff; font-size: 11px; font-weight: 700;
  padding: 3px 10px; border-radius: 20px; white-space: nowrap;
  display: flex; align-items: center; gap: 5px;
}
.notice-text { overflow: hidden; white-space: nowrap; text-overflow: ellipsis; }

/* ===== GRID MENU ===== */
.section-title { padding: 0 16px 10px; font-size: 13px; font-weight: 700; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.8px; }
.menu-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; padding: 0 16px 20px; }
.menu-item {
  background: #fff;
  border-radius: var(--radius);
  padding: 18px 10px 14px;
  display: flex; flex-direction: column; align-items: center; gap: 10px;
  cursor: pointer;
  box-shadow: var(--shadow-card);
  border: 1.5px solid transparent;
  transition: all 0.2s;
}
.menu-item:hover, .menu-item:active {
  border-color: var(--primary);
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(255,107,0,0.15);
}
.menu-icon {
  width: 46px; height: 46px;
  background: linear-gradient(135deg, #fff5ee, #ffe4cc);
  border-radius: 13px;
  display: flex; align-items: center; justify-content: center;
  font-size: 20px;
  color: var(--primary);
  transition: all 0.2s;
}
.menu-item:hover .menu-icon { background: linear-gradient(135deg, var(--primary), var(--primary-light)); color: #fff; }
.menu-label { font-size: 11.5px; font-weight: 600; text-align: center; color: var(--text); }

/* ===== CARDS ===== */
.card {
  background: #fff;
  border-radius: var(--radius);
  padding: 18px;
  margin: 0 16px 16px;
  box-shadow: var(--shadow-card);
}
.card-title {
  font-size: 15px; font-weight: 700; margin-bottom: 14px;
  display: flex; align-items: center; gap: 8px;
  color: var(--text);
}
.card-title .icon { color: var(--primary); }

/* ===== PAGE HEADER ===== */
.page-header {
  padding: 18px 16px 10px;
  display: flex; align-items: center; gap: 12px;
}
.page-header h2 {
  font-size: 18px; font-weight: 700; color: var(--text);
  display: flex; align-items: center; gap: 8px;
}
.page-header h2 .ph-icon { color: var(--primary); }

/* ===== BUTTONS ===== */
.btn {
  display: inline-flex; align-items: center; justify-content: center; gap: 8px;
  padding: 12px 20px; border-radius: 12px; border: none;
  font-family: 'Poppins', sans-serif; font-size: 14px; font-weight: 600;
  cursor: pointer; transition: all 0.2s; width: 100%;
}
.btn-primary { background: linear-gradient(135deg, var(--primary), var(--primary-light)); color: #fff; box-shadow: 0 4px 15px rgba(255,107,0,0.35); }
.btn-primary:hover { transform: translateY(-1px); box-shadow: 0 6px 20px rgba(255,107,0,0.45); }
.btn-outline { background: transparent; color: var(--primary); border: 2px solid var(--primary); }
.btn-outline:hover { background: rgba(255,107,0,0.05); }
.btn-danger { background: linear-gradient(135deg, #ef4444, #f87171); color: #fff; }

/* ===== FORMS ===== */
.form-group { margin-bottom: 14px; }
.form-label { font-size: 12px; font-weight: 600; color: var(--text-muted); margin-bottom: 6px; display: block; text-transform: uppercase; letter-spacing: 0.5px; }
.form-control {
  width: 100%; padding: 12px 14px; border: 1.5px solid var(--border);
  border-radius: 12px; font-family: 'Poppins', sans-serif; font-size: 14px;
  background: #fafbff; color: var(--text);
  outline: none; transition: all 0.2s;
}
.form-control:focus { border-color: var(--primary); background: #fff; box-shadow: 0 0 0 3px rgba(255,107,0,0.08); }
select.form-control { appearance: none; background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8' viewBox='0 0 12 8'%3E%3Cpath fill='%23666' d='M6 8L0 0h12z'/%3E%3C/svg%3E"); background-repeat: no-repeat; background-position: right 14px center; padding-right: 36px; }

/* ===== WITHDRAW ===== */
.balance-tabs { display: flex; gap: 10px; margin-bottom: 14px; }
.balance-tab {
  flex: 1; padding: 14px; border-radius: 14px;
  border: 2px solid var(--border); background: #fff;
  cursor: pointer; text-align: center; transition: all 0.2s;
}
.balance-tab.active { border-color: var(--primary); background: #fff8f3; }
.balance-tab .tab-label { font-size: 11px; font-weight: 600; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.5px; }
.balance-tab .tab-amount { font-family: 'Rajdhani', sans-serif; font-size: 22px; font-weight: 700; color: var(--text); margin-top: 4px; }
.balance-tab.active .tab-amount { color: var(--primary); }
.balance-display {
  background: linear-gradient(135deg, var(--primary), var(--primary-light));
  color: #fff; border-radius: 14px; padding: 16px; text-align: center; margin-bottom: 16px;
}
.balance-display .bd-label { font-size: 13px; opacity: 0.85; }
.balance-display .bd-amount { font-family: 'Rajdhani', sans-serif; font-size: 32px; font-weight: 700; }
.withdraw-amounts { display: grid; grid-template-columns: repeat(3,1fr); gap: 8px; margin-bottom: 16px; }
.withdraw-amount-btn {
  background: #fff; border: 1.5px solid var(--border);
  border-radius: 12px; padding: 10px 6px; text-align: center;
  cursor: pointer; transition: all 0.2s;
}
.withdraw-amount-btn:hover, .withdraw-amount-btn.selected { border-color: var(--primary); background: #fff8f3; }
.wa-main { font-size: 15px; font-weight: 700; color: var(--text); }
.wa-charge { font-size: 10px; color: var(--danger); font-weight: 600; margin-top: 2px; }

/* ===== JOB TASKS ===== */
.stats-row {
  background: linear-gradient(135deg, var(--primary), var(--primary-light));
  margin: 16px; border-radius: 16px; padding: 16px 20px;
  display: flex; gap: 0; color: #fff;
  box-shadow: 0 6px 20px rgba(255,107,0,0.3);
}
.stat-item { flex:1; text-align: center; }
.stat-item + .stat-item { border-left: 1px solid rgba(255,255,255,0.25); }
.stat-num { font-family: 'Rajdhani', sans-serif; font-size: 26px; font-weight: 700; }
.stat-lbl { font-size: 11px; opacity: 0.85; font-weight: 500; }
.task-card {
  background: #fff; border-radius: var(--radius); margin: 0 16px 10px;
  padding: 16px; box-shadow: var(--shadow-card);
  border: 1.5px solid transparent; transition: all 0.2s;
}
.task-card:hover { border-color: var(--primary); }
.task-title { font-size: 15px; font-weight: 700; margin-bottom: 8px; }
.task-meta { display: flex; align-items: center; justify-content: space-between; margin-bottom: 12px; }
.task-reward {
  background: #dcfce7; color: #16a34a; font-size: 13px; font-weight: 700;
  padding: 4px 12px; border-radius: 20px; display: flex; align-items: center; gap: 4px;
}
.task-time { font-size: 12px; color: var(--text-muted); display: flex; align-items: center; gap: 4px; }

/* ===== SELL FORM ===== */
.important-box {
  background: #fffbeb; border: 1.5px solid #fcd34d;
  border-radius: 12px; padding: 12px 14px; margin-bottom: 16px;
}
.important-box .ib-title { font-size: 12px; font-weight: 700; color: #92400e; margin-bottom: 6px; display: flex; align-items: center; gap: 6px; }
.password-copy {
  background: #fff; border: 1.5px solid var(--border);
  border-radius: 10px; padding: 10px 12px;
  display: flex; align-items: center; justify-content: space-between;
  margin-top: 8px;
}
.pw-text { font-size: 14px; font-weight: 600; color: var(--primary); }
.copy-btn {
  background: var(--text); color: #fff; border: none;
  padding: 6px 14px; border-radius: 8px; font-size: 12px; font-weight: 600;
  cursor: pointer; display: flex; align-items: center; gap: 5px; transition: all 0.2s;
}
.copy-btn:hover { background: var(--primary); }
.reward-badge {
  background: linear-gradient(135deg, var(--primary), var(--primary-light));
  color: #fff; font-weight: 700; font-size: 14px;
  padding: 5px 14px; border-radius: 20px;
}

/* ===== PROFILE ===== */
.profile-hero {
  background: linear-gradient(135deg, var(--primary), var(--primary-light));
  padding: 28px 20px 20px; text-align: center; color: #fff;
}
.profile-avatar {
  width: 72px; height: 72px; border-radius: 50%;
  background: rgba(255,255,255,0.25);
  display: flex; align-items: center; justify-content: center;
  font-size: 28px; border: 3px solid rgba(255,255,255,0.5);
  margin: 0 auto 12px; overflow: hidden;
}
.profile-name { font-size: 18px; font-weight: 700; }
.profile-badges { display: flex; justify-content: center; gap: 8px; margin-top: 8px; flex-wrap: wrap; }
.profile-badge {
  font-size: 11px; font-weight: 600;
  background: rgba(255,255,255,0.2); padding: 3px 12px; border-radius: 20px;
  display: flex; align-items: center; gap: 4px;
}
.profile-stats { display: flex; margin-top: 16px; }
.profile-stat { flex:1; text-align: center; }
.profile-stat + .profile-stat { border-left: 1px solid rgba(255,255,255,0.25); }
.ps-val { font-family: 'Rajdhani', sans-serif; font-size: 20px; font-weight: 700; }
.ps-lbl { font-size: 10px; opacity: 0.85; font-weight: 500; text-transform: uppercase; letter-spacing: 0.5px; }

/* ===== MENU LIST ===== */
.menu-list { padding: 8px 16px; }
.menu-section-title { font-size: 11px; font-weight: 700; color: var(--primary); text-transform: uppercase; letter-spacing: 1px; padding: 12px 0 6px; }
.menu-list-item {
  background: #fff; border-radius: 12px; padding: 14px 16px;
  margin-bottom: 6px; display: flex; align-items: center; gap: 12px;
  cursor: pointer; box-shadow: var(--shadow-card); transition: all 0.2s;
  border: 1.5px solid transparent;
}
.menu-list-item:hover { border-color: var(--primary); transform: translateX(3px); }
.mli-icon { width: 36px; height: 36px; border-radius: 10px; display: flex; align-items: center; justify-content: center; font-size: 16px; flex-shrink: 0; }
.mli-icon.orange { background: #fff3e8; color: var(--primary); }
.mli-icon.blue { background: #eff6ff; color: #3b82f6; }
.mli-icon.green { background: #f0fdf4; color: #22c55e; }
.mli-icon.red { background: #fef2f2; color: #ef4444; }
.mli-icon.purple { background: #faf5ff; color: #a855f7; }
.mli-text { font-size: 14px; font-weight: 600; color: var(--text); flex: 1; }
.mli-arrow { color: var(--text-muted); font-size: 12px; }
.premium-item { background: linear-gradient(135deg, #fff8f3, #fff0e0) !important; border: 1.5px solid #ffd4a3 !important; }
.premium-item .mli-text { color: var(--primary); }

/* ===== WALLET ===== */
.wallet-card {
  background: linear-gradient(135deg, var(--primary), var(--primary-light));
  margin: 16px; border-radius: 20px; padding: 22px;
  color: #fff; text-align: center;
  box-shadow: 0 8px 30px rgba(255,107,0,0.35);
  position: relative; overflow: hidden;
}
.wallet-card::before { content:''; position:absolute; top:-30px; right:-30px; width:120px; height:120px; background:rgba(255,255,255,0.08); border-radius:50%; }
.wc-label { font-size: 13px; opacity: 0.85; font-weight: 500; }
.wc-amount { font-family: 'Rajdhani', sans-serif; font-size: 38px; font-weight: 700; margin: 6px 0; }
.wc-sub { font-size: 12px; opacity: 0.75; }
.wallet-actions { display: flex; gap: 10px; margin: 0 16px 16px; }
.wallet-action-btn {
  flex:1; background: #fff; border: none; border-radius: 14px;
  padding: 14px; display: flex; flex-direction: column; align-items: center; gap: 6px;
  cursor: pointer; box-shadow: var(--shadow-card); transition: all 0.2s;
}
.wallet-action-btn:hover { transform: translateY(-2px); box-shadow: 0 6px 20px rgba(0,0,0,0.1); }
.wa-btn-icon { width:40px; height:40px; border-radius:12px; display:flex; align-items:center; justify-content:center; font-size:18px; }
.wa-btn-icon.orange { background: #fff3e8; color: var(--primary); }
.wa-btn-icon.green { background: #f0fdf4; color: var(--success); }
.wa-btn-label { font-size: 12px; font-weight: 600; color: var(--text); }
.history-item {
  display: flex; align-items: center; gap: 12px;
  padding: 12px 0; border-bottom: 1px solid var(--border);
}
.history-item:last-child { border-bottom: none; }
.hi-icon { width:38px; height:38px; border-radius:12px; display:flex; align-items:center; justify-content:center; font-size:16px; flex-shrink:0; }
.hi-info { flex:1; }
.hi-title { font-size: 14px; font-weight: 600; }
.hi-date { font-size: 11px; color: var(--text-muted); margin-top: 2px; }
.hi-amount { font-family: 'Rajdhani', sans-serif; font-size: 17px; font-weight: 700; }
.hi-amount.positive { color: var(--success); }
.hi-amount.negative { color: var(--danger); }

/* ===== TEAM ===== */
.referral-box {
  background: linear-gradient(135deg, #667eea22, #764ba222);
  border: 1.5px solid #c7d2fe;
  border-radius: 16px; padding: 16px; margin: 0 16px 16px;
}
.ref-link {
  background: #fff; border: 1.5px solid var(--border);
  border-radius: 10px; padding: 10px 12px;
  display: flex; align-items: center; justify-content: space-between;
  margin-top: 10px;
}
.ref-url { font-size: 12px; color: var(--text-muted); overflow: hidden; text-overflow: ellipsis; white-space: nowrap; max-width: 200px; }
.team-stats { display: grid; grid-template-columns: repeat(2,1fr); gap: 10px; margin: 0 16px 16px; }
.team-stat {
  background: #fff; border-radius: 14px; padding: 16px;
  box-shadow: var(--shadow-card); text-align: center;
}
.ts-num { font-family: 'Rajdhani', sans-serif; font-size: 26px; font-weight: 700; color: var(--primary); }
.ts-label { font-size: 11px; color: var(--text-muted); font-weight: 600; }
.member-item {
  display: flex; align-items: center; gap: 12px;
  padding: 12px 0; border-bottom: 1px solid var(--border);
}
.member-item:last-child { border-bottom: none; }
.member-avatar { width:40px; height:40px; border-radius:12px; background: linear-gradient(135deg, var(--primary), var(--primary-light)); display:flex; align-items:center; justify-content:center; color:#fff; font-weight:700; font-size:15px; flex-shrink:0; }
.member-name { font-size: 14px; font-weight: 600; }
.member-joined { font-size: 11px; color: var(--text-muted); margin-top: 2px; }
.member-reward { font-size: 13px; font-weight: 700; color: var(--success); }

/* ===== SIDEBAR OVERLAY ===== */
.sidebar-overlay {
  position: fixed; top:0; left:0; right:0; bottom:0;
  background: rgba(0,0,0,0.5); z-index: 200;
  display: none; align-items: flex-start;
  animation: fadeOverlay 0.25s ease;
}
.sidebar-overlay.open { display: flex; }
@keyframes fadeOverlay { from{opacity:0} to{opacity:1} }
.sidebar {
  width: 280px; background: #fff; height: 100vh;
  animation: slideIn 0.3s ease;
  overflow-y: auto; flex-shrink: 0;
}
@keyframes slideIn { from{transform:translateX(-100%)} to{transform:translateX(0)} }
.sidebar-header {
  background: linear-gradient(135deg, var(--primary), var(--primary-light));
  padding: 28px 20px 20px; color: #fff;
}
.sidebar-avatar {
  width: 64px; height: 64px; border-radius: 50%;
  background: rgba(255,255,255,0.25);
  display: flex; align-items: center; justify-content: center;
  font-size: 24px; border: 3px solid rgba(255,255,255,0.4);
  margin-bottom: 10px; overflow: hidden;
}
.sidebar-name { font-size: 16px; font-weight: 700; }
.sidebar-id { font-size: 12px; opacity: 0.8; margin-top: 3px; }

/* ===== TOAST ===== */
.toast {
  position: fixed; top: 70px; left: 50%; transform: translateX(-50%) translateY(-20px);
  background: #1a1a2e; color: #fff;
  padding: 10px 20px; border-radius: 30px; font-size: 13px; font-weight: 600;
  z-index: 9999; opacity: 0; transition: all 0.3s; white-space: normal; text-align:center;
  pointer-events: none; width: 90%; max-width: 400px;
}
.toast.show { opacity: 1; transform: translateX(-50%) translateY(0); }
.toast.success { background: var(--success); }
.toast.error { background: var(--danger); }

/* ===== MODAL ===== */
.modal-overlay {
  position: fixed; top:0; left:0; right:0; bottom:0;
  background: rgba(0,0,0,0.5); z-index: 300;
  display: none; align-items: flex-end; justify-content: center;
}
.modal-overlay.open { display: flex; }
.modal {
  background: #fff; border-radius: 20px 20px 0 0; width: 100%; max-width: 480px;
  padding: 24px 20px; max-height: 85vh; overflow-y: auto;
  animation: slideUp 0.35s cubic-bezier(0.34,1.56,0.64,1);
}
@keyframes slideUp { from{transform:translateY(100%)} to{transform:translateY(0)} }
.modal-title { font-size: 17px; font-weight: 700; margin-bottom: 16px; display: flex; align-items: center; justify-content: space-between; }
.modal-close { background:none; border:none; font-size:18px; cursor:pointer; color:var(--text-muted); }

/* ===== LEADERBOARD ===== */
.lb-item {
  display: flex; align-items: center; gap: 12px;
  padding: 12px 0; border-bottom: 1px solid var(--border);
}
.lb-rank { font-family: 'Rajdhani', sans-serif; font-size: 18px; font-weight: 700; width: 24px; text-align: center; color: var(--text-muted); }
.lb-rank.gold { color: #f59e0b; }
.lb-rank.silver { color: #9ca3af; }
.lb-rank.bronze { color: #cd7c2f; }
.lb-avatar { width:38px; height:38px; border-radius:12px; background:linear-gradient(135deg,var(--primary),var(--primary-light)); display:flex; align-items:center; justify-content:center; color:#fff; font-weight:700; font-size:14px; }
.lb-name { flex:1; font-size:14px; font-weight:600; }
.lb-amount { font-family:'Rajdhani',sans-serif; font-size:16px; font-weight:700; color:var(--primary); }

/* SCROLLBAR */
::-webkit-scrollbar { width: 4px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb { background: var(--border); border-radius: 10px; }

/* UTIL */
.divider { height:1px; background:var(--border); margin:0 16px 16px; }
.text-muted { color: var(--text-muted); font-size: 13px; }
.mt-8 { margin-top: 8px; }
.empty-state { text-align:center; padding:40px 20px; color:var(--text-muted); }
.empty-state i { font-size:40px; margin-bottom:12px; opacity:0.3; display:block; }

/* ===== AUTH PAGE ===== */
#authPage {
  position: fixed; top:0; left:0; right:0; bottom:0;
  background: linear-gradient(160deg, #FF6B00 0%, #ff8c35 40%, #fff5ee 100%);
  z-index: 9999; display: none; flex-direction: column;
  align-items: center; justify-content: center;
  padding: 24px; overflow-y: auto;
}
.auth-logo {
  font-family: 'Rajdhani', sans-serif; font-size: 36px; font-weight: 700;
  color: #fff; letter-spacing: 3px; margin-bottom: 6px;
  display: flex; align-items: center; gap: 10px;
}
.auth-logo-icon {
  width: 48px; height: 48px; background: rgba(255,255,255,0.25);
  border-radius: 14px; display: flex; align-items: center; justify-content: center;
  font-size: 22px;
}
.auth-tagline { color: rgba(255,255,255,0.85); font-size: 14px; margin-bottom: 32px; text-align: center; }
.auth-card {
  background: #fff; border-radius: 24px; padding: 28px 24px;
  width: 100%; max-width: 400px;
  box-shadow: 0 20px 60px rgba(0,0,0,0.15);
}
.auth-tabs { display: flex; background: #f4f6fb; border-radius: 12px; padding: 4px; margin-bottom: 24px; }
.auth-tab {
  flex: 1; padding: 10px; border: none; border-radius: 10px;
  font-family: 'Poppins', sans-serif; font-size: 14px; font-weight: 600;
  cursor: pointer; transition: all 0.2s; background: transparent; color: var(--text-muted);
}
.auth-tab.active { background: #fff; color: var(--primary); box-shadow: 0 2px 8px rgba(0,0,0,0.1); }
.auth-form { display: none; }
.auth-form.active { display: block; }
.auth-title { font-size: 20px; font-weight: 700; margin-bottom: 4px; }
.auth-subtitle { font-size: 13px; color: var(--text-muted); margin-bottom: 20px; }
.photo-preview-wrap { display: flex; align-items: center; gap: 14px; margin-bottom: 16px; }
.photo-preview {
  width: 60px; height: 60px; border-radius: 50%;
  background: linear-gradient(135deg, var(--primary), var(--primary-light));
  display: flex; align-items: center; justify-content: center;
  font-size: 24px; color: #fff; border: 3px solid rgba(255,107,0,0.2);
  overflow: hidden; flex-shrink: 0;
}
.photo-preview img { width: 100%; height: 100%; object-fit: cover; }
.photo-preview-info { flex: 1; font-size: 12px; color: var(--text-muted); line-height: 1.5; }
.auth-loading { display:none; text-align:center; padding:20px; }
.auth-loading i { font-size:28px; color:var(--primary); animation:spin 1s linear infinite; }
@keyframes spin { to{transform:rotate(360deg)} }
.auth-divider { text-align:center; font-size:12px; color:var(--text-muted); margin:16px 0; }
.forgot-link { text-align:right; margin-top:-8px; margin-bottom:14px; }
.forgot-link a { font-size:12px; color:var(--primary); font-weight:600; cursor:pointer; text-decoration:none; }

/* ===== ACCOUNT ACTIVATION PAGE ===== */
#activationPage {
  position: fixed; top:0; left:0; right:0; bottom:0;
  background: var(--bg);
  z-index: 9998; display: none; flex-direction: column;
  align-items: center; justify-content: flex-start;
  padding: 24px 16px; overflow-y: auto;
}
.activation-card {
  background: #fff; border-radius: 20px; padding: 24px 20px;
  width: 100%; max-width: 440px;
  box-shadow: var(--shadow-card); margin-top: 20px;
  border: 2px solid var(--border);
}
.act-header { text-align:center; margin-bottom: 20px; }
.act-icon { font-size: 48px; color: var(--primary); margin-bottom: 10px; }
.act-title { font-size: 18px; font-weight: 700; }
.act-subtitle { font-size: 12.5px; color: var(--text-muted); margin-top: 4px; }
.payment-nums { background: #fff3e8; border: 1.5px dashed var(--primary-light); border-radius: 12px; padding: 12px; margin-bottom: 16px; }
.num-row { display:flex; align-items:center; justify-content:space-between; padding: 4px 0; font-size:13px; font-weight:600; }

</style>
</head>
<body>

<!-- ==================== AUTH PAGE ==================== -->
<div id="authPage">
  <div class="auth-logo">
    <div class="auth-logo-icon"><i class="fas fa-coins"></i></div>
    TK EARN
  </div>
  <p class="auth-tagline">কাজ করুন, আয় করুন — প্রতিদিন!</p>

  <div class="auth-card">
    <div class="auth-tabs">
      <button class="auth-tab active" onclick="switchAuthTab('login')">Login</button>
      <button class="auth-tab" onclick="switchAuthTab('register')">Register</button>
    </div>

    <!-- LOGIN FORM -->
    <div class="auth-form active" id="loginForm">
      <div class="auth-title">স্বাগতম! 👋</div>
      <div class="auth-subtitle">আপনার অ্যাকাউন্টে প্রবেশ করুন</div>
      <div class="form-group">
        <label class="form-label">Email Address</label>
        <input type="email" class="form-control" id="loginEmail" placeholder="example@gmail.com">
      </div>
      <div class="form-group">
        <label class="form-label">Password</label>
        <input type="password" class="form-control" id="loginPassword" placeholder="আপনার পাসওয়ার্ড">
      </div>
      <div class="forgot-link"><a onclick="forgotPassword()"><i class="fas fa-key"></i> পাসওয়ার্ড ভুলে গেছেন?</a></div>
      <button class="btn btn-primary" onclick="doLogin()"><i class="fas fa-sign-in-alt"></i> Login করুন</button>
      <div class="auth-divider">অ্যাকাউন্ট নেই? <span onclick="switchAuthTab('register')" style="color:var(--primary);font-weight:600;cursor:pointer">Register করুন</span></div>
    </div>

    <!-- REGISTER FORM -->
    <div class="auth-form" id="registerForm">
      <div class="auth-title">নতুন অ্যাকাউন্ট</div>
      <div class="auth-subtitle">ফ্রিতে রেজিস্টার করে আয় শুরু করুন</div>

      <!-- Photo Preview -->
      <div class="photo-preview-wrap">
        <div class="photo-preview" id="regPhotoPreview"><i class="fas fa-user"></i></div>
        <div class="photo-preview-info">
          <strong>প্রোফাইল ছবি (ঐচ্ছিক)</strong><br>
          নিচে ছবির URL লিখুন। না দিলেও রেজিস্টার হবে।
        </div>
      </div>

      <div class="form-group">
        <label class="form-label">Photo URL (ঐচ্ছিক)</label>
        <input type="url" class="form-control" id="regPhotoUrl" placeholder="https://example.com/photo.jpg" oninput="previewRegPhoto(this.value)">
      </div>
      <div class="form-group">
        <label class="form-label">Full Name</label>
        <input type="text" class="form-control" id="regName" placeholder="আপনার পুরো নাম">
      </div>
      <div class="form-group">
        <label class="form-label">Phone Number</label>
        <input type="tel" class="form-control" id="regPhone" placeholder="01">
      </div>
      <div class="form-group">
        <label class="form-label">Email Address</label>
        <input type="email" class="form-control" id="regEmail" placeholder="example@gmail.com">
      </div>
      <div class="form-group">
        <label class="form-label">Password (কমপক্ষে ৬ অক্ষর)</label>
        <input type="password" class="form-control" id="regPassword" placeholder="পাসওয়ার্ড তৈরি করুন">
      </div>
      <div class="form-group">
        <label class="form-label">Referral Code (ঐচ্ছিক)</label>
        <input type="text" class="form-control" id="regRef" placeholder="রেফারেল কোড">
      </div>
      <button class="btn btn-primary" onclick="doRegister()"><i class="fas fa-user-plus"></i> Register করুন</button>
      <div class="auth-divider">ইতিমধ্যে অ্যাকাউন্ট আছে? <span onclick="switchAuthTab('login')" style="color:var(--primary);font-weight:600;cursor:pointer">Login করুন</span></div>
    </div>

    <!-- LOADING -->
    <div class="auth-loading" id="authLoading">
      <i class="fas fa-circle-notch"></i>
      <p style="margin-top:10px;color:var(--text-muted);font-size:13px">অপেক্ষা করুন...</p>
    </div>
  </div>
</div>

<!-- ==================== ACCOUNT ACTIVATION PAGE ==================== -->
<div id="activationPage" style="display:none">
  <div class="auth-logo" style="color: var(--primary); margin-top:20px">
    <div class="auth-logo-icon" style="background: rgba(255,107,0,0.15); color:var(--primary)"><i class="fas fa-coins"></i></div>
    TK EARN
  </div>
  
  <div class="activation-card">
    <div class="act-header">
      <div class="act-icon"><i class="fas fa-shield-alt"></i></div>
      <div class="act-title">অ্যাকাউন্ট একটিভ করুন 🛡️</div>
      <p class="act-subtitle">প্রতিদিন ইনকাম করার জন্য <strong id="act-charge-amount" style="color:var(--primary)">৳২০</strong> দিয়ে অ্যাকাউন্ট একটিভ করুন।</p>
    </div>

    <!-- Option 1: Balance Activation -->
    <div style="background:linear-gradient(135deg,#fff8f3,#fff3e8);border:1.5px solid #fcd9b6;border-radius:14px;padding:14px;margin-bottom:14px">
      <div style="display:flex;align-items:center;gap:8px;margin-bottom:10px">
        <div style="width:32px;height:32px;background:var(--primary);border-radius:9px;display:flex;align-items:center;justify-content:center;color:#fff;font-size:14px"><i class="fas fa-wallet"></i></div>
        <div style="font-size:13px;font-weight:700">প্রধান ব্যালেন্স দিয়ে একটিভ করুন</div>
      </div>
      <div style="font-size:12px;color:var(--text-muted);margin-bottom:10px">বর্তমান ব্যালেন্স: <strong id="actMainBal" style="color:var(--text)">৳0.00</strong> &nbsp;|&nbsp; প্রয়োজন: <strong id="act-bal-required" style="color:var(--primary)">৳২০</strong></div>
      <button class="btn btn-primary" style="width:100%;padding:10px;font-size:12.5px" onclick="activateWithBalance()">
        <i class="fas fa-check-circle"></i> ব্যালেন্স থেকে কেটে একটিভ করুন
      </button>
    </div>

    <!-- Divider -->
    <div style="display:flex;align-items:center;gap:10px;margin:6px 0 14px">
      <div style="flex:1;height:1px;background:var(--border)"></div>
      <span style="font-size:11px;font-weight:700;color:var(--text-muted);background:#fff;padding:2px 10px;border-radius:20px;border:1px solid var(--border)">অথবা ডিপোজিট করুন</span>
      <div style="flex:1;height:1px;background:var(--border)"></div>
    </div>

    <!-- Option 2: Mobile Banking -->
    <div style="background:#f8fafc;border:1.5px solid var(--border);border-radius:14px;padding:14px;margin-bottom:14px">
      <div style="display:flex;align-items:center;gap:8px;margin-bottom:12px">
        <div style="width:32px;height:32px;background:#3b82f6;border-radius:9px;display:flex;align-items:center;justify-content:center;color:#fff;font-size:14px"><i class="fas fa-university"></i></div>
        <div>
          <div style="font-size:13px;font-weight:700">মোবাইল ব্যাংকিং দিয়ে ডিপোজিট করুন</div>
          <div style="font-size:11px;color:var(--text-muted)">নিচের নম্বরে Send Money করুন</div>
        </div>
      </div>

      <!-- Payment Number Cards -->
      <div style="display:flex;flex-direction:column;gap:8px;margin-bottom:14px">

        <!-- bKash -->
        <div id="card-bkash" style="background:#fff0f6;border:1.5px solid #fce7f3;border-radius:12px;padding:10px 12px;display:flex;align-items:center;justify-content:space-between">
          <div style="display:flex;align-items:center;gap:10px">
            <div style="width:34px;height:34px;background:#e91e8c;border-radius:9px;display:flex;align-items:center;justify-content:center;color:#fff;font-size:15px;font-weight:800;flex-shrink:0">b</div>
            <div>
              <div style="font-size:10px;font-weight:700;color:#c2185b;text-transform:uppercase;letter-spacing:0.5px">bKash</div>
              <div id="actBkash" style="font-size:15px;font-weight:700;color:#1a1a2e;font-family:'Rajdhani',sans-serif;letter-spacing:0.5px">01727271390</div>
            </div>
          </div>
          <button onclick="copyNum('actBkash','bKash')" style="background:#e91e8c;color:#fff;border:none;border-radius:8px;padding:6px 10px;font-size:11px;font-weight:700;cursor:pointer;font-family:'Poppins',sans-serif;flex-shrink:0">
            <i class="fas fa-copy"></i> কপি
          </button>
        </div>

        <!-- Nagad -->
        <div id="card-nagad" style="background:#fff8f0;border:1.5px solid #fed7aa;border-radius:12px;padding:10px 12px;display:flex;align-items:center;justify-content:space-between">
          <div style="display:flex;align-items:center;gap:10px">
            <div style="width:34px;height:34px;background:#f97316;border-radius:9px;display:flex;align-items:center;justify-content:center;color:#fff;font-size:15px;font-weight:800;flex-shrink:0">N</div>
            <div>
              <div style="font-size:10px;font-weight:700;color:#c2410c;text-transform:uppercase;letter-spacing:0.5px">Nagad</div>
              <div id="actNagad" style="font-size:15px;font-weight:700;color:#1a1a2e;font-family:'Rajdhani',sans-serif;letter-spacing:0.5px">01727271390</div>
            </div>
          </div>
          <button onclick="copyNum('actNagad','Nagad')" style="background:#f97316;color:#fff;border:none;border-radius:8px;padding:6px 10px;font-size:11px;font-weight:700;cursor:pointer;font-family:'Poppins',sans-serif;flex-shrink:0">
            <i class="fas fa-copy"></i> কপি
          </button>
        </div>

        <!-- Rocket -->
        <div id="card-rocket" style="background:#f5f0ff;border:1.5px solid #ddd6fe;border-radius:12px;padding:10px 12px;display:flex;align-items:center;justify-content:space-between">
          <div style="display:flex;align-items:center;gap:10px">
            <div style="width:34px;height:34px;background:#7c3aed;border-radius:9px;display:flex;align-items:center;justify-content:center;color:#fff;font-size:15px;font-weight:800;flex-shrink:0">R</div>
            <div>
              <div style="font-size:10px;font-weight:700;color:#6d28d9;text-transform:uppercase;letter-spacing:0.5px">Rocket</div>
              <div id="actRocket" style="font-size:15px;font-weight:700;color:#1a1a2e;font-family:'Rajdhani',sans-serif;letter-spacing:0.5px">লোড হচ্ছে...</div>
            </div>
          </div>
          <button onclick="copyNum('actRocket','Rocket')" style="background:#7c3aed;color:#fff;border:none;border-radius:8px;padding:6px 10px;font-size:11px;font-weight:700;cursor:pointer;font-family:'Poppins',sans-serif;flex-shrink:0">
            <i class="fas fa-copy"></i> কপি
          </button>
        </div>

      </div>

      <!-- Info note -->
      <div style="background:#eff6ff;border:1px solid #bfdbfe;border-radius:10px;padding:9px 12px;margin-bottom:14px;font-size:11.5px;color:#1e40af;line-height:1.6">
        <i class="fas fa-info-circle"></i> উপরের যেকোনো নম্বরে <strong>Send Money</strong> করুন। তারপর নিচে মেথড ও TrxID দিয়ে রিকোয়েস্ট পাঠান।
      </div>

      <div class="form-group" style="margin-bottom:10px">
        <label class="form-label" style="font-size:10px">পেমেন্ট মেথড সিলেক্ট করুন</label>
        <select class="form-control" id="actMethod" style="padding:10px;font-size:13px">
          <option value="">-- মেথড সিলেক্ট করুন --</option>
          <option value="bkash">🩷 bKash</option>
          <option value="nagad">🟠 Nagad</option>
          <option value="rocket">💜 Rocket</option>
        </select>
      </div>

      <div class="form-group" style="margin-bottom:10px">
        <label class="form-label" style="font-size:10px">সেন্ডার মোবাইল নম্বর</label>
        <input type="tel" class="form-control" id="actSender" placeholder="01XXXXXXXXX" style="padding:10px;font-size:13px">
      </div>

      <div class="form-group" style="margin-bottom:12px">
        <label class="form-label" style="font-size:10px">ট্রানজেকশন আইডি (TrxID)</label>
        <input type="text" class="form-control" id="actTrx" placeholder="ট্রানজেকশন আইডি দিন" style="padding:10px;font-size:13px">
      </div>

      <button class="btn btn-primary" style="width:100%;padding:11px;font-size:12.5px;background:linear-gradient(135deg,#10b981,#22c55e)" onclick="submitActivationRequest()">
        <i class="fas fa-paper-plane"></i> রিকোয়েস্ট পাঠান
      </button>
    </div>

    <button class="btn btn-outline" style="width:100%;border-radius:12px;padding:10px;font-size:12px" onclick="logout()">
      <i class="fas fa-sign-out-alt"></i> লগআউট করুন
    </button>
  </div>
</div>
<!-- TOPBAR -->
<div class="topbar">
  <button class="topbar-btn" onclick="openSidebar()"><i class="fas fa-bars"></i></button>
  <div class="topbar-logo">
    <div class="logo-icon"><i class="fas fa-coins"></i></div>
    TK EARN
  </div>
  <button class="topbar-btn" onclick="showPage('profile')"><i class="fas fa-user-circle"></i></button>
</div>

<!-- SIDEBAR OVERLAY -->
<div class="sidebar-overlay" id="sidebarOverlay" onclick="closeSidebar()">
  <div class="sidebar" onclick="event.stopPropagation()">
    <div class="sidebar-header">
      <div class="sidebar-avatar" id="sidebarAvatar"><i class="fas fa-user"></i></div>
      <div class="sidebar-name" id="sidebarName"></div>
      <div class="sidebar-id">ID: 974 &bull; Joined: 16 Mar 2026</div>
    </div>
    <div class="menu-list">
      <div class="menu-section-title">HOME SELECTION</div>
      <div class="menu-list-item" onclick="closeSidebar();showPage('home')">
        <div class="mli-icon orange"><i class="fas fa-home"></i></div>
        <span class="mli-text">Dashboard</span>
        <i class="fas fa-chevron-right mli-arrow"></i>
      </div>
      <div class="menu-list-item" onclick="closeSidebar();showPage('leaderboard')">
        <div class="mli-icon orange"><i class="fas fa-trophy"></i></div>
        <span class="mli-text">Top Leaderboard</span>
        <i class="fas fa-chevron-right mli-arrow"></i>
      </div>
      <div class="menu-list-item" onclick="closeSidebar();showPage('profileUpdate')">
        <div class="mli-icon blue"><i class="fas fa-user-edit"></i></div>
        <span class="mli-text">Profile Update</span>
        <i class="fas fa-chevron-right mli-arrow"></i>
      </div>

      <div class="menu-section-title">WORKING SELECTION</div>
      <div class="menu-list-item" onclick="closeSidebar();showPage('dailyJob')">
        <div class="mli-icon orange"><i class="fas fa-briefcase"></i></div>
        <span class="mli-text">My Job (Regular)</span>
        <i class="fas fa-chevron-right mli-arrow"></i>
      </div>
      <div class="menu-list-item" onclick="closeSidebar();showPage('visitingJob')">
        <div class="mli-icon blue"><i class="fas fa-map-marker-alt"></i></div>
        <span class="mli-text">Visiting Job</span>
        <i class="fas fa-chevron-right mli-arrow"></i>
      </div>
      <div class="menu-list-item" onclick="closeSidebar();showPage('postWork')">
        <div class="mli-icon green"><i class="fas fa-upload"></i></div>
        <span class="mli-text">Post Work</span>
        <i class="fas fa-chevron-right mli-arrow"></i>
      </div>
      <div class="menu-list-item" onclick="closeSidebar();showPage('jobHistory')">
        <div class="mli-icon purple"><i class="fas fa-history"></i></div>
        <span class="mli-text">My Job History</span>
        <i class="fas fa-chevron-right mli-arrow"></i>
      </div>
      <div class="menu-list-item" onclick="closeSidebar();showPage('giftCode')">
        <div class="mli-icon orange"><i class="fas fa-gift"></i></div>
        <span class="mli-text">Ref Gift Code</span>
        <i class="fas fa-chevron-right mli-arrow"></i>
      </div>

      <div class="menu-section-title">SELL SERVICE</div>
      <div class="menu-list-item" onclick="closeSidebar();showPage('facebookSell')">
        <div class="mli-icon blue"><i class="fab fa-facebook-f"></i></div>
        <span class="mli-text">Facebook ID Sell</span>
        <i class="fas fa-chevron-right mli-arrow"></i>
      </div>
      <div class="menu-list-item" onclick="closeSidebar();showPage('gmailSell')">
        <div class="mli-icon red"><i class="fas fa-envelope"></i></div>
        <span class="mli-text">Gmail Sell</span>
        <i class="fas fa-chevron-right mli-arrow"></i>
      </div>
      <div class="menu-list-item" onclick="closeSidebar();showPage('instagramSell')">
        <div class="mli-icon purple"><i class="fab fa-instagram"></i></div>
        <span class="mli-text">Instagram ID Sell</span>
        <i class="fas fa-chevron-right mli-arrow"></i>
      </div>

      <div class="menu-section-title">PREMIUM ZONE</div>
      <div class="menu-list-item premium-item" onclick="closeSidebar();showPage('membership')">
        <div class="mli-icon orange"><i class="fas fa-gem"></i></div>
        <span class="mli-text">Upgrade Membership</span>
        <i class="fas fa-chevron-right mli-arrow"></i>
      </div>

      <div class="menu-list-item" onclick="closeSidebar();logout()" style="margin-top:8px;">
        <div class="mli-icon red"><i class="fas fa-sign-out-alt"></i></div>
        <span class="mli-text" style="color:#ef4444;">Logout</span>
        <i class="fas fa-chevron-right mli-arrow"></i>
      </div>
    </div>
  </div>
</div>

<!-- TOAST -->
<div class="toast" id="toast"></div>

<!-- ==================== HOME PAGE ==================== -->
<div class="page active" id="page-home">
  <div class="hero-card">
    <div class="hero-user">
      <div class="hero-avatar" id="heroAvatar"><i class="fas fa-user" style="font-size:22px;color:#fff"></i></div>
      <div class="hero-info">
        <h3 id="heroName"> </>
        <div class="hero-meta">
          <div class="hero-badge"><i class="fas fa-id-badge"></i> ID: 974</div>
          <div class="hero-badge"><i class="fas fa-calendar"></i> 16 Mar 2026</div>
        </div>
        <div class="hero-meta" style="margin-top:4px">
          <div class="hero-badge" id="heroStatusBadge"><div class="status-dot"></div> Active</div>
        </div>
      </div>
    </div>
    <div class="hero-balance">
      <span class="balance-label">Main Balance</span>
      <span class="balance-amount" id="homeBalance">৳ 0.00</span>
    </div>
  </div>

  <div class="notice-bar">
    <div class="notice-label"><i class="fas fa-bullhorn"></i> Notice</div>
    <div class="notice-text" id="noticeText">Daily job tasks updated! Complete all tasks to earn rewards. Welcome to TK Earn platform!</div>
  </div>

  <!-- ACTIVATION BANNER — inactive users এর জন্য -->
  <div id="activationBanner" style="display:none;margin:0 16px 14px;background:linear-gradient(135deg,#FF6B00,#ff8c35);border-radius:16px;padding:16px;box-shadow:0 4px 20px rgba(255,107,0,0.35)">
    <div style="display:flex;align-items:center;gap:10px;margin-bottom:10px">
      <div style="width:40px;height:40px;background:rgba(255,255,255,0.25);border-radius:12px;display:flex;align-items:center;justify-content:center;font-size:18px">🔒</div>
      <div>
        <div style="color:#fff;font-weight:700;font-size:14px">অ্যাকাউন্ট একটিভ করুন</div>
        <div style="color:rgba(255,255,255,0.85);font-size:11px">মাত্র ৳২০ দিয়ে সব ফিচার আনলক করুন</div>
      </div>
    </div>
    <button onclick="document.getElementById('activationPage').style.display='flex'" style="width:100%;padding:11px;background:#fff;color:var(--primary);border:none;border-radius:12px;font-weight:700;font-size:13px;cursor:pointer;font-family:'Poppins',sans-serif">
      <i class="fas fa-unlock-alt"></i> এখনই একটিভ করুন →
    </button>
  </div>

  <div class="section-title">Quick Actions</div>
  <div class="menu-grid">
    <div class="menu-item" onclick="showPage('dailyJob')">
      <div class="menu-icon"><i class="fas fa-briefcase"></i></div>
      <span class="menu-label">Daily Job</span>
    </div>
    <div class="menu-item" onclick="showPage('giftCode')">
      <div class="menu-icon"><i class="fas fa-gift"></i></div>
      <span class="menu-label">Gift Code</span>
    </div>
    <div class="menu-item" onclick="showPage('withdraw')">
      <div class="menu-icon"><i class="fas fa-money-bill-wave"></i></div>
      <span class="menu-label">Withdraw</span>
    </div>
    <div class="menu-item" onclick="showPage('facebookSell')">
      <div class="menu-icon"><i class="fab fa-facebook-f"></i></div>
      <span class="menu-label">Facebook Sell</span>
    </div>
    <div class="menu-item" onclick="showPage('instagramSell')">
      <div class="menu-icon"><i class="fab fa-instagram"></i></div>
      <span class="menu-label">Instagram Sell</span>
    </div>
    <div class="menu-item" onclick="showPage('gmailSell')">
      <div class="menu-icon"><i class="fas fa-envelope"></i></div>
      <span class="menu-label">Gmail Sell</span>
    </div>
    <div class="menu-item" onclick="showPage('visitingJob')">
      <div class="menu-icon"><i class="fas fa-globe"></i></div>
      <span class="menu-label">Visit Job</span>
    </div>
    <div class="menu-item" onclick="showPage('team')">
      <div class="menu-icon"><i class="fas fa-users"></i></div>
      <span class="menu-label">Refer Team</span>
    </div>
    <div class="menu-item" onclick="showPage('leaderboard')">
      <div class="menu-icon"><i class="fas fa-trophy"></i></div>
      <span class="menu-label">Leaderboard</span>
    </div>
  </div>
</div>

<!-- ==================== DAILY JOB PAGE ==================== -->
<div class="page" id="page-dailyJob">
  <div class="page-header"><h2><i class="fas fa-briefcase ph-icon"></i> Daily Job</h2></div>
  <div class="stats-row">
    <div class="stat-item"><div class="stat-num" id="totalTasks">5</div><div class="stat-lbl">Total Available</div></div>
    <div class="stat-item"><div class="stat-num" id="completedTasks">0</div><div class="stat-lbl">Completed</div></div>
  </div>
  <div id="dailyJobList"></div>
</div>

<!-- ==================== VISITING JOB ==================== -->
<div class="page" id="page-visitingJob">
  <div class="page-header"><h2><i class="fas fa-globe ph-icon"></i> Visiting Job</h2></div>
  <div class="stats-row">
    <div class="stat-item"><div class="stat-num">3</div><div class="stat-lbl">Total Available</div></div>
    <div class="stat-item"><div class="stat-num" id="visitCompleted">0</div><div class="stat-lbl">Completed</div></div>
  </div>
  <p class="section-title">WEBSITE VISITING TASKS</p>
  <div id="visitingJobList"></div>
</div>

<!-- ==================== POST WORK ==================== -->
<div class="page" id="page-postWork">
  <div class="page-header"><h2><i class="fas fa-upload ph-icon"></i> Post Work</h2></div>
  <div class="card">
    <div class="card-title"><i class="fas fa-info-circle icon"></i> Submit Your Work</div>
    <div class="form-group">
      <label class="form-label">Work Type</label>
      <select class="form-control" id="pwType">
        <option value="">-- Select Work Type --</option>
        <option>Facebook Post</option>
        <option>Instagram Post</option>
        <option>YouTube Comment</option>
        <option>Website Visit</option>
        <option>App Download</option>
      </select>
    </div>
    <div class="form-group">
      <label class="form-label">Work Screenshot Link</label>
      <input type="url" class="form-control" id="pwScreenshot" placeholder="https://...">
    </div>
    <div class="form-group">
      <label class="form-label">Work Description</label>
      <textarea class="form-control" id="pwDesc" rows="3" placeholder="Describe your work..."></textarea>
    </div>
    <button class="btn btn-primary" onclick="submitWork()"><i class="fas fa-paper-plane"></i> Submit Work</button>
  </div>
</div>

<!-- ==================== JOB HISTORY ==================== -->
<div class="page" id="page-jobHistory">
  <div class="page-header"><h2><i class="fas fa-history ph-icon"></i> Job History</h2></div>
  <div class="card">
    <div id="jobHistoryList">
      <div class="empty-state"><i class="fas fa-folder-open"></i><p>No job history yet</p></div>
    </div>
  </div>
</div>

<!-- ==================== GIFT CODE ==================== -->
<div class="page" id="page-giftCode">
  <div class="page-header"><h2><i class="fas fa-gift ph-icon"></i> Gift Code</h2></div>
  <div class="card">
    <div class="card-title"><i class="fas fa-ticket-alt icon"></i> Redeem Gift Code</div>
    <div class="form-group">
      <label class="form-label">Enter Gift Code</label>
      <input type="text" class="form-control" id="giftCodeInput" placeholder="Enter your gift code here" style="text-transform:uppercase">
    </div>
    <button class="btn btn-primary" onclick="redeemGiftCode()"><i class="fas fa-check-circle"></i> Redeem Now</button>
  </div>
  <div class="card" style="margin-top:0">
    <div class="card-title"><i class="fas fa-history icon"></i> Redemption History</div>
    <div id="giftHistory">
      <div class="empty-state"><i class="fas fa-gift"></i><p>No codes redeemed yet</p></div>
    </div>
  </div>
</div>

<!-- ==================== WITHDRAW ==================== -->
<div class="page" id="page-withdraw">
  <div class="page-header"><h2><i class="fas fa-money-bill-wave ph-icon"></i> Withdraw Funds</h2></div>
  <div style="padding:0 16px 16px">
    <div class="balance-tabs">
      <div class="balance-tab active" onclick="selectBalanceTab(this,'main')">
        <div class="tab-label">Main Balance</div>
        <div class="tab-amount" id="wdMainBal">৳ 0.00</div>
      </div>
      <div class="balance-tab" onclick="selectBalanceTab(this,'refer')">
        <div class="tab-label">Refer Balance</div>
        <div class="tab-amount" id="wdReferBal">৳ 0.00</div>
      </div>
    </div>
    <div class="balance-display">
      <div class="bd-label">Your Main Balance</div>
      <div class="bd-amount" id="wdDisplayBal">৳ 0.00</div>
    </div>
    <div class="form-group">
      <label class="form-label">Select Method</label>
      <select class="form-control" id="withdrawMethod">
        <option value="">-- Choose method --</option>
        <option value="bkash">bKash</option>
        <option value="nagad">Nagad</option>
        <option value="rocket">Rocket</option>
        <option value="bank">Bank Transfer</option>
      </select>
    </div>
    <div class="form-group">
      <label class="form-label">Account Number</label>
      <input type="text" class="form-control" id="withdrawAccount" placeholder="Enter your account number">
    </div>
    <p class="form-label" style="margin-bottom:10px">SELECT AMOUNT</p>
    <div class="withdraw-amounts" id="withdrawAmounts">
      <div class="withdraw-amount-btn" onclick="selectAmount(this,60,5)"><div class="wa-main">৳60</div><div class="wa-charge">charge ৳5</div></div>
      <div class="withdraw-amount-btn" onclick="selectAmount(this,110,10)"><div class="wa-main">৳110</div><div class="wa-charge">charge ৳10</div></div>
      <div class="withdraw-amount-btn" onclick="selectAmount(this,220,20)"><div class="wa-main">৳220</div><div class="wa-charge">charge ৳20</div></div>
      <div class="withdraw-amount-btn" onclick="selectAmount(this,330,30)"><div class="wa-main">৳330</div><div class="wa-charge">charge ৳30</div></div>
      <div class="withdraw-amount-btn" onclick="selectAmount(this,440,40)"><div class="wa-main">৳440</div><div class="wa-charge">charge ৳40</div></div>
      <div class="withdraw-amount-btn" onclick="selectAmount(this,550,50)"><div class="wa-main">৳550</div><div class="wa-charge">charge ৳50</div></div>
    </div>
    <button class="btn btn-primary" onclick="processWithdraw()"><i class="fas fa-paper-plane"></i> Submit Withdrawal</button>
  </div>
</div>

<!-- ==================== FACEBOOK SELL ==================== -->
<div class="page" id="page-facebookSell">
  <div class="page-header"><h2><i class="fab fa-facebook-f ph-icon"></i> Facebook ID Sell</h2></div>
  <div class="card">
    <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:14px">
      <div class="card-title" style="margin-bottom:0"><i class="fas fa-upload icon"></i> Submit Your ID</div>
      <div class="reward-badge">৳ OFF</div>
    </div>
    <div class="important-box">
      <div class="ib-title"><i class="fas fa-exclamation-circle" style="color:#f59e0b"></i> Important</div>
      <p style="font-size:12px;color:#92400e">Must provide today's password, otherwise it will be rejected.</p>
      <div class="password-copy">
        <span class="pw-text" id="fbPassword">moneyjobsite@07</span>
        <button class="copy-btn" onclick="copyText('fbPassword')"><i class="fas fa-copy"></i> Copy</button>
      </div>
    </div>
    <div class="form-group">
      <label class="form-label">UID / Profile Link</label>
      <input type="text" class="form-control" id="fbUID" placeholder="e.g., 1000123456789 or profile link">
    </div>
    <div class="form-group">
      <label class="form-label">Phone Number (optional)</label>
      <input type="tel" class="form-control" id="fbPhone" placeholder="Login phone">
    </div>
    <div class="form-group">
      <label class="form-label">Password</label>
      <input type="password" class="form-control" id="fbPass" placeholder="Account password">
    </div>
    <div class="form-group">
      <label class="form-label">Cookies (optional)</label>
      <textarea class="form-control" id="fbCookies" rows="3" placeholder="Paste cookies here..."></textarea>
    </div>
    <button class="btn btn-primary" onclick="submitSell('facebook')"><i class="fas fa-paper-plane"></i> Submit Now</button>
  </div>
</div>

<!-- ==================== GMAIL SELL ==================== -->
<div class="page" id="page-gmailSell">
  <div class="page-header"><h2><i class="fas fa-envelope ph-icon"></i> Gmail Sell</h2></div>
  <div class="card">
    <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:14px">
      <div class="card-title" style="margin-bottom:0"><i class="fas fa-upload icon"></i> Submit Gmail</div>
      <div class="reward-badge">৳ 12.00</div>
    </div>
    <div class="important-box">
      <div class="ib-title"><i class="fas fa-exclamation-circle" style="color:#f59e0b"></i> Important</div>
      <p style="font-size:12px;color:#92400e">Gmail must be active and recovery email set.</p>
      <div class="password-copy">
        <span class="pw-text" id="gmailPassword">gmailsite@2026</span>
        <button class="copy-btn" onclick="copyText('gmailPassword')"><i class="fas fa-copy"></i> Copy</button>
      </div>
    </div>
    <div class="form-group">
      <label class="form-label">Gmail Address</label>
      <input type="email" class="form-control" id="gmEmail" placeholder="example@gmail.com">
    </div>
    <div class="form-group">
      <label class="form-label">Password</label>
      <input type="password" class="form-control" id="gmPass" placeholder="Gmail password">
    </div>
    <div class="form-group">
      <label class="form-label">Recovery Email (optional)</label>
      <input type="email" class="form-control" id="gmRecovery" placeholder="Recovery email">
    </div>
    <button class="btn btn-primary" onclick="submitSell('gmail')"><i class="fas fa-paper-plane"></i> Submit Now</button>
  </div>
</div>

<!-- ==================== INSTAGRAM SELL ==================== -->
<div class="page" id="page-instagramSell">
  <div class="page-header"><h2><i class="fab fa-instagram ph-icon"></i> Instagram ID Sell</h2></div>
  <div class="card">
    <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:14px">
      <div class="card-title" style="margin-bottom:0"><i class="fas fa-upload icon"></i> Submit Your ID</div>
      <div class="reward-badge">৳ OFF </div>
    </div>
    <div class="important-box">
      <div class="ib-title"><i class="fas fa-exclamation-circle" style="color:#f59e0b"></i> Important</div>
      <p style="font-size:12px;color:#92400e">Account must have minimum 100 followers.</p>
      <div class="password-copy">
        <span class="pw-text" id="igPassword">instasite@2026</span>
        <button class="copy-btn" onclick="copyText('igPassword')"><i class="fas fa-copy"></i> Copy</button>
      </div>
    </div>
    <div class="form-group">
      <label class="form-label">Username / Profile Link</label>
      <input type="text" class="form-control" id="igUser" placeholder="@username or profile URL">
    </div>
    <div class="form-group">
      <label class="form-label">Password</label>
      <input type="password" class="form-control" id="igPass" placeholder="Account password">
    </div>
    <div class="form-group">
      <label class="form-label">Backup Code (optional)</label>
      <input type="text" class="form-control" id="igBackup" placeholder="2FA backup code">
    </div>
    <button class="btn btn-primary" onclick="submitSell('instagram')"><i class="fas fa-paper-plane"></i> Submit Now</button>
  </div>
</div>

<!-- ==================== WALLET ==================== -->
<div class="page" id="page-wallet">
  <div class="wallet-card">
    <div class="wc-label">Total Balance</div>
    <div class="wc-amount" id="walletBalance">৳ 0.00</div>
    <div class="wc-sub">Main + Refer Balance</div>
  </div>
  <div class="wallet-actions">
    <div class="wallet-action-btn" onclick="showPage('withdraw')">
      <div class="wa-btn-icon orange"><i class="fas fa-arrow-up"></i></div>
      <span class="wa-btn-label">Withdraw</span>
    </div>
    <div class="wallet-action-btn" onclick="showModal('transferModal')">
      <div class="wa-btn-icon green"><i class="fas fa-exchange-alt"></i></div>
      <span class="wa-btn-label">Transfer</span>
    </div>
    <div class="wallet-action-btn" onclick="showPage('team')">
      <div class="wa-btn-icon orange"><i class="fas fa-users"></i></div>
      <span class="wa-btn-label">Earn More</span>
    </div>
  </div>
  <div class="card">
    <div class="card-title"><i class="fas fa-clock icon"></i> Recent Transactions</div>
    <div id="transactionHistory">
      <div class="empty-state"><i class="fas fa-receipt"></i><p>No transactions yet</p></div>
    </div>
  </div>
</div>

<!-- ==================== TEAM ==================== -->
<div class="page" id="page-team">
  <div class="page-header"><h2><i class="fas fa-users ph-icon"></i> My Team</h2></div>
  <div class="card" style="margin-bottom:10px">
    <div class="card-title"><i class="fas fa-share-alt icon"></i> Your Referral Link</div>
    <div style="background:#f8faff;border:1.5px solid var(--border);border-radius:12px;padding:12px 14px;margin-bottom:12px">
      <div style="font-size:11px;color:var(--text-muted);font-weight:600;text-transform:uppercase;letter-spacing:0.5px;margin-bottom:6px">আপনার ইউনিক Referral Link</div>
      <div id="refLink" style="font-size:12px;color:var(--primary);font-weight:600;word-break:break-all;line-height:1.6">লোড হচ্ছে...</div>
    </div>
    <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px">
      <button class="copy-btn" onclick="copyRef()" style="padding:10px;border-radius:10px;font-size:13px;justify-content:center"><i class="fas fa-copy"></i> Copy Link</button>
      <button class="btn btn-primary" onclick="shareRef()" style="padding:10px;font-size:13px"><i class="fas fa-share-alt"></i> Share</button>
    </div>
  </div>
  <div class="team-stats">
    <div class="team-stat"><div class="ts-num" id="totalReferrals">0</div><div class="ts-label">Total Referrals</div></div>
    <div class="team-stat"><div class="ts-num" id="referBalance">৳0.00</div><div class="ts-label">Refer Earnings</div></div>
  </div>
  <div class="card">
    <div class="card-title"><i class="fas fa-user-friends icon"></i> Team Members</div>
    <div id="teamMembers">
      <div class="empty-state"><i class="fas fa-users"></i><p>No team members yet. Share your referral link!</p></div>
    </div>
  </div>
</div>

<!-- ==================== PROFILE ==================== -->
<div class="page" id="page-profile">
  <div class="profile-hero">
    <div class="profile-avatar" id="profileAvatarEl"><i class="fas fa-user" style="font-size:28px;color:#fff"></i></div>
    <div class="profile-name" id="profileName"></>
    <div class="profile-badges">
      <div class="profile-badge"><i class="fas fa-id-badge"></i> ID: 974</div>
      <div class="profile-badge" id="profileStatusBadge" style="background:rgba(74,222,128,0.25)"><div class="status-dot"></div> Active</div>
    </div>
    <div class="profile-stats">
      <div class="profile-stat"><div class="ps-val" id="profileBalance">৳0.00</div><div class="ps-lbl">Balance</div></div>
      <div class="profile-stat"><div class="ps-val">16 Mar</div><div class="ps-lbl">Joined</div></div>
      <div class="profile-stat"><div class="ps-val" id="profileReferrals">0</div><div class="ps-lbl">Referrals</div></div>
    </div>
  </div>
  <div class="menu-list">
    <div class="menu-section-title">HOME SELECTION</div>
    <div class="menu-list-item" onclick="showPage('home')">
      <div class="mli-icon orange"><i class="fas fa-home"></i></div>
      <span class="mli-text">Dashboard</span><i class="fas fa-chevron-right mli-arrow"></i>
    </div>
    <div class="menu-list-item" onclick="showPage('leaderboard')">
      <div class="mli-icon orange"><i class="fas fa-trophy"></i></div>
      <span class="mli-text">Top Leaderboard</span><i class="fas fa-chevron-right mli-arrow"></i>
    </div>
    <div class="menu-list-item" onclick="showPage('profileUpdate')">
      <div class="mli-icon blue"><i class="fas fa-user-edit"></i></div>
      <span class="mli-text">Profile Update</span><i class="fas fa-chevron-right mli-arrow"></i>
    </div>
    <div class="menu-section-title">PREMIUM ZONE</div>
    <div class="menu-list-item premium-item" onclick="showPage('membership')">
      <div class="mli-icon orange"><i class="fas fa-gem"></i></div>
      <span class="mli-text">Upgrade Membership</span><i class="fas fa-chevron-right mli-arrow"></i>
    </div>
    <div class="menu-list-item" onclick="logout()" style="margin-top:8px">
      <div class="mli-icon red"><i class="fas fa-sign-out-alt"></i></div>
      <span class="mli-text" style="color:#ef4444">Logout</span><i class="fas fa-chevron-right mli-arrow"></i>
    </div>
  </div>
</div>

<!-- ==================== PROFILE UPDATE ==================== -->
<div class="page" id="page-profileUpdate">
  <div class="page-header"><h2><i class="fas fa-user-edit ph-icon"></i> Profile Update</h2></div>
  <div class="card">
    <!-- Photo preview in profile update -->
    <div class="photo-preview-wrap" style="margin-bottom:18px">
      <div class="photo-preview" id="updatePhotoPreview"><i class="fas fa-user"></i></div>
      <div class="photo-preview-info">
        <strong>প্রোফাইল ছবি</strong><br>
        ছবির URL দিন। পরিবর্তন করলে Save করুন।
      </div>
    </div>
    <div class="form-group">
      <label class="form-label">Photo URL (ঐচ্ছিক)</label>
      <input type="url" class="form-control" id="updatePhotoUrl" placeholder="https://example.com/photo.jpg" oninput="previewUpdatePhoto(this.value)">
    </div>
    <div class="form-group">
      <label class="form-label">Full Name</label>
      <input type="text" class="form-control" id="updateName" placeholder="Your full name">
    </div>
    <div class="form-group">
      <label class="form-label">Phone Number</label>
      <input type="tel" class="form-control" id="updatePhone" placeholder="01XXXXXXX">
    </div>
    <div class="form-group">
      <label class="form-label">bKash Number</label>
      <input type="tel" class="form-control" id="updateBkash" placeholder="bKash account number">
    </div>
    <div class="form-group">
      <label class="form-label">Nagad Number</label>
      <input type="tel" class="form-control" id="updateNagad" placeholder="Nagad account number">
    </div>
    <button class="btn btn-primary" onclick="updateProfile()"><i class="fas fa-save"></i> Save Changes</button>
  </div>
  <div class="card">
    <div class="card-title"><i class="fas fa-lock icon"></i> Change Password</div>
    <div class="form-group">
      <label class="form-label">New Password (কমপক্ষে ৬ অক্ষর)</label>
      <input type="password" class="form-control" id="newPassword" placeholder="নতুন পাসওয়ার্ড">
    </div>
    <div class="form-group">
      <label class="form-label">Confirm Password</label>
      <input type="password" class="form-control" id="confirmPassword" placeholder="পাসওয়ার্ড নিশ্চিত করুন">
    </div>
    <button class="btn btn-outline" onclick="changePassword()"><i class="fas fa-key"></i> Change Password</button>
  </div>
</div>

<!-- ==================== LEADERBOARD ==================== -->
<div class="page" id="page-leaderboard">
  <div class="page-header"><h2><i class="fas fa-trophy ph-icon"></i> Top Leaderboard</h2></div>
  <div class="card">
    <div class="card-title"><i class="fas fa-medal icon"></i> Top Earners This Month</div>
    <div id="leaderboardList"></div>
  </div>
</div>

<!-- ==================== MEMBERSHIP ==================== -->
<div class="page" id="page-membership">
  <div class="page-header"><h2><i class="fas fa-gem ph-icon"></i> Upgrade Membership</h2></div>
  <div id="membershipPlans"></div>
</div>

<!-- ==================== BOTTOM NAV ==================== -->
<nav class="bottom-nav">
  <button class="nav-item active" onclick="showPage('home')" id="nav-home">
    <div class="nav-icon"><i class="fas fa-home"></i></div>
    <span>Home</span>
  </button>
  <button class="nav-item" onclick="showPage('visitingJob')" id="nav-visitingJob">
    <div class="nav-icon"><i class="fas fa-headset"></i></div>
    <span>Help</span>
  </button>
  <button class="nav-item" onclick="showPage('wallet')" id="nav-wallet">
    <div class="nav-icon"><i class="fas fa-wallet"></i></div>
    <span>Wallet</span>
  </button>
  <button class="nav-item" onclick="showPage('team')" id="nav-team">
    <div class="nav-icon"><i class="fas fa-users"></i></div>
    <span>Team</span>
  </button>
  <button class="nav-item" onclick="showPage('profile')" id="nav-profile">
    <div class="nav-icon"><i class="fas fa-user"></i></div>
    <span>Profile</span>
  </button>
</nav>

<!-- TRANSFER MODAL -->
<div class="modal-overlay" id="transferModal">
  <div class="modal">
    <div class="modal-title">Transfer Balance <button class="modal-close" onclick="closeModal('transferModal')"><i class="fas fa-times"></i></button></div>
    <div class="form-group">
      <label class="form-label">Recipient ID</label>
      <input type="text" class="form-control" placeholder="Enter user ID">
    </div>
    <div class="form-group">
      <label class="form-label">Amount (৳)</label>
      <input type="number" class="form-control" placeholder="Enter amount">
    </div>
    <button class="btn btn-primary" onclick="processTransfer()"><i class="fas fa-paper-plane"></i> Transfer Now</button>
  </div>
</div>

<script>
// ============ FIREBASE CONFIG ============
const firebaseConfig = {
  apiKey: "AIzaSyCD9sx-jXdUoW3_dYGribl3IKw7Blz_Zbk",
  authDomain: "khelofreefir.firebaseapp.com",
  databaseURL: "https://khelofreefir-default-rtdb.firebaseio.com",
  projectId: "khelofreefir",
  storageBucket: "khelofreefir.firebasestorage.app",
  messagingSenderId: "990986344662",
  appId: "1:990986344662:web:355748a0c8a7672dc01177",
  measurementId: "G-0FQXPGF6VQ"
};
firebase.initializeApp(firebaseConfig);
const auth = firebase.auth();
const db = firebase.firestore();

// ============ AUTH FUNCTIONS ============
function switchAuthTab(tab) {
  document.querySelectorAll('.auth-tab').forEach((t,i) => {
    t.classList.toggle('active', (tab==='login'&&i===0)||(tab==='register'&&i===1));
  });
  const loginForm = document.getElementById('loginForm');
  const registerForm = document.getElementById('registerForm');
  const loading = document.getElementById('authLoading');
  // loading hide করো — নইলে form দেখা যায় না
  if(loading) loading.style.display = 'none';
  loginForm.classList.toggle('active', tab==='login');
  registerForm.classList.toggle('active', tab==='register');
  loginForm.style.display = tab === 'login' ? 'block' : 'none';
  registerForm.style.display = tab === 'register' ? 'block' : 'none';
}

function showAuthLoading(show) {
  const loading = document.getElementById('authLoading');
  const loginForm = document.getElementById('loginForm');
  const registerForm = document.getElementById('registerForm');
  loading.style.display = show ? 'block' : 'none';
  if(show) { loginForm.style.display='none'; registerForm.style.display='none'; }
  else {
    loginForm.style.display = loginForm.classList.contains('active') ? 'block' : 'none';
    registerForm.style.display = registerForm.classList.contains('active') ? 'block' : 'none';
  }
}

function previewRegPhoto(url) {
  const prev = document.getElementById('regPhotoPreview');
  if(url && url.startsWith('http')) {
    prev.innerHTML = `<img src="${url}" onerror="this.parentElement.innerHTML='<i class=\\'fas fa-user\\'></i>'" alt="Photo">`;
  } else {
    prev.innerHTML = '<i class="fas fa-user"></i>';
  }
}

async function doRegister() {
  const name = document.getElementById('regName').value.trim();
  const phone = document.getElementById('regPhone').value.trim();
  const email = document.getElementById('regEmail').value.trim();
  const password = document.getElementById('regPassword').value;
  const photoUrl = document.getElementById('regPhotoUrl').value.trim();
  const refCode = document.getElementById('regRef').value.trim();

  if(!name) { showAuthToast('নাম দিন', 'error'); return; }
  if(!phone) { showAuthToast('ফোন নম্বর দিন', 'error'); return; }
  if(!email) { showAuthToast('Email দিন', 'error'); return; }
  if(password.length < 6) { showAuthToast('পাসওয়ার্ড কমপক্ষে ৬ অক্ষর', 'error'); return; }

  showAuthLoading(true);
  try {
    const cred = await auth.createUserWithEmailAndPassword(email, password);
    const uid = cred.user.uid;

    const counterRef = db.collection('meta').doc('userCounter');
    const userIdNum = await db.runTransaction(async t => {
      const doc = await t.get(counterRef);
      const next = (doc.exists ? doc.data().count : 1000) + 1;
      t.set(counterRef, { count: next });
      return next;
    });

    // Handle referral bonus
    if(refCode) {
      try {
        let refDocRef = db.collection('users').doc(refCode);
        let refDoc = await refDocRef.get();

        if(!refDoc.exists) {
          const refSnap = await db.collection('users').where('referCode', '==', refCode).limit(1).get();
          if(!refSnap.empty) refDocRef = refSnap.docs[0].ref;
          refDoc = refSnap.empty ? null : refSnap.docs[0];
        }

        if(refDoc && refDoc.exists) {
          const settings = await getAppSettings();
          const refBonus = settings.refBonus || 10;
          await refDocRef.update({
            referBalance: firebase.firestore.FieldValue.increment(refBonus),
          });
          await refDocRef.collection('transactions').add({
            title: `Referral Bonus — ${name}`, amount: refBonus, positive: true,
            createdAt: firebase.firestore.FieldValue.serverTimestamp(),
          });
        }
      } catch(refErr) { console.warn('Ref bonus error:', refErr); }
    }

    const joinDate = new Date().toLocaleDateString('en-GB', { day:'2-digit', month:'short', year:'numeric' });
    const settings = await getAppSettings();
    const signupBonus = settings.signupBonus || 0;

    const myReferCode = uid;

    const userData = {
      name, phone, email, photoUrl: photoUrl || '',
      userId: userIdNum, joined: joinDate,
      balance: signupBonus, referBalance: 0,
      referCode: myReferCode,
      referredBy: refCode || '',
      status: 'inactive', // রেজিস্ট্রেশনের শুরুতে অ্যাকাউন্ট নিষ্ক্রিয় বা ইন-একটিভ থাকবে
      createdAt: firebase.firestore.FieldValue.serverTimestamp()
    };
    await db.collection('users').doc(uid).set(userData);
    await cred.user.updateProfile({ displayName: name, photoURL: photoUrl || null });
    showAuthToast('রেজিস্টার সফল হয়েছে! 🎉', 'success');
  } catch(e) {
    showAuthLoading(false);
    const msgs = {
      'auth/email-already-in-use': 'এই Email ইতিমধ্যে ব্যবহৃত',
      'auth/invalid-email': 'সঠিক Email দিন',
      'auth/weak-password': 'পাসওয়ার্ড দুর্বল'
    };
    showAuthToast(msgs[e.code] || e.message, 'error');
  }
}

async function doLogin() {
  const email = document.getElementById('loginEmail').value.trim();
  const password = document.getElementById('loginPassword').value;
  if(!email || !password) { showAuthToast('Email ও পাসওয়ার্ড দিন', 'error'); return; }
  showAuthLoading(true);
  try {
    await auth.signInWithEmailAndPassword(email, password);
  } catch(e) {
    showAuthLoading(false);
    const msgs = {
      'auth/user-not-found': 'অ্যাকাউন্ট পাওয়া যায়নি',
      'auth/wrong-password': 'পাসওয়ার্ড ভুল',
      'auth/invalid-credential': 'Email বা পাসওয়ার্ড ভুল',
      'auth/too-many-requests': 'অনেকবার চেষ্টা হয়েছে, পরে আবার চেষ্টা করুন'
    };
    showAuthToast(msgs[e.code] || e.message, 'error');
  }
}

async function forgotPassword() {
  const email = document.getElementById('loginEmail').value.trim();
  if(!email) { showAuthToast('আগে Email দিন', 'error'); return; }
  try {
    await auth.sendPasswordResetEmail(email);
    showAuthToast('পাসওয়ার্ড রিসেট ইমেইল পাঠানো হয়েছে ✉️', 'success');
  } catch(e) {
    showAuthToast('Email পাওয়া যায়নি', 'error');
  }
}

function showAuthToast(msg, type='') {
  const t = document.getElementById('toast');
  if(t) {
    t.textContent = msg;
    t.className = 'toast show ' + type;
    setTimeout(() => t.className = 'toast', 3000);
  }
}

// ============ APP SETTINGS LOADER ============
let appSettings = { minWithdraw: 60, charge: 8, refBonus: 10, signupBonus: 5, activationCharge: 100 };
async function getAppSettings() {
  try {
    const doc = await db.collection('app_config').doc('settings').get();
    if(doc.exists) {
      appSettings = { ...appSettings, ...doc.data() };
      // ডাইনামিক ডিপোজিট বিকাশ/নগদ নম্বর রেন্ডারিং
      // bKash number
      const bkEl = document.getElementById('actBkash');
      const bkCard = document.getElementById('card-bkash');
      if(appSettings.bkashNum) {
        if(bkEl) bkEl.textContent = appSettings.bkashNum;
        if(bkCard) bkCard.style.display = 'flex';
      } else {
        if(bkCard) bkCard.style.display = 'none';
      }
      // Nagad number
      const ngEl = document.getElementById('actNagad');
      const ngCard = document.getElementById('card-nagad');
      if(appSettings.nagadNum) {
        if(ngEl) ngEl.textContent = appSettings.nagadNum;
        if(ngCard) ngCard.style.display = 'flex';
      } else {
        if(ngCard) ngCard.style.display = 'none';
      }
      // Rocket number
      const rkEl = document.getElementById('actRocket');
      const rkCard = document.getElementById('card-rocket');
      if(appSettings.rocketNum) {
        if(rkEl) rkEl.textContent = appSettings.rocketNum;
        if(rkCard) rkCard.style.display = 'flex';
      } else {
        if(rkCard) rkCard.style.display = 'none';
      }
      // একটিভেশন চার্জ ডাইনামিক আপডেট
      const ac = appSettings.activationCharge || 100;
      const actChargeEl = document.getElementById('act-charge-amount');
      if(actChargeEl) actChargeEl.textContent = '৳' + ac;
      const actBalReq = document.getElementById('act-bal-required');
      if(actBalReq) actBalReq.textContent = '৳' + ac;
    }
  } catch(e) {}
  return appSettings;
}

// ============ COPY NUMBER HELPER ============
function copyNum(elId, label) {
  const el = document.getElementById(elId);
  if(!el) return;
  const num = el.textContent.trim();
  if(!num || num === 'লোড হচ্ছে...') return;
  navigator.clipboard.writeText(num).then(() => {
    showToast('✅ ' + label + ' নম্বর কপি হয়েছে: ' + num, 'success');
  }).catch(() => {
    // fallback for older browsers
    const ta = document.createElement('textarea');
    ta.value = num; ta.style.position='fixed'; ta.style.opacity='0';
    document.body.appendChild(ta); ta.select();
    document.execCommand('copy');
    document.body.removeChild(ta);
    showToast('✅ ' + label + ' নম্বর কপি হয়েছে!', 'success');
  });
}

// ============ STATE ============
const state = {
  user: { name: '', id: '', joined: '', status: 'inactive', uid: null },
  balance: { main: 0, refer: 0 },
  completedTasks: new Set(),
  visitCompleted: new Set(),
  appGiftCodes: {},      
  redeemedCodes: [],
  transactions: [],
  selectedWithdrawAmount: null,
  selectedWithdrawCharge: null,
  activeWithdrawTab: 'main',
  members: [],
  jobHistory: [],
  dailyTasks: [],   
  visitTasks: [],   
  selfAction: false,  
  lastTxId: null,     
};

// ============ AUTH STATE & REAL-TIME LISTENERS ============
let previousBalance = null;

auth.onAuthStateChanged(async user => {
  if(user) {
    // ১. ইউজার ডাটার রিয়েল-টাইম লিসেনার (ব্যান চেক, একটিভ চেক ও ব্যালেন্স মনিটর)
    db.collection('users').doc(user.uid).onSnapshot(doc => {
      if(!doc.exists) return;
      const data = doc.data();

      // ব্যানড ইউজার চেক
      if(data.status === 'banned') {
        auth.signOut();
        showAuthToast('⛔ আপনার অ্যাকাউন্ট Banned করা হয়েছে!', 'error');
        document.getElementById('authPage').style.display = 'flex';
        document.getElementById('activationPage').style.display = 'none';
    const ab = document.getElementById('activationBanner');
    if(ab) ab.style.display = 'none';
        showBannedMessage();
        return;
      }

      // ইন-একটিভ চেক — activation page full screen দেখাবে না
      // শুধু home page এ banner দেখাবে
      document.getElementById('activationPage').style.display = 'none';
      document.getElementById('authPage').style.display = 'none';
      document.getElementById('actMainBal').textContent = '৳' + (data.balance || 0).toFixed(2);
      // banner control: inactive হলে দেখাও, active হলে লুকাও
      const ab = document.getElementById('activationBanner');
      if(ab) ab.style.display = (data.status === 'inactive') ? 'block' : 'none';

      // রিয়েল-টাইম ব্যালেন্স বৃদ্ধি পর্যবেক্ষণ
      if (previousBalance !== null && data.balance > previousBalance) {
        if (state.selfAction) {
          state.selfAction = false; 
        } else {
          const diff = data.balance - previousBalance;
          showToast(`🎉 এডমিন আপনার অ্যাকাউন্টে ৳${diff.toFixed(2)} পাঠিয়েছেন!`, 'success');
        }
      }
      previousBalance = data.balance;

      loadUserIntoApp(data, user.uid);
    });

    // ২. ট্রানজেকশন হিস্ট্রি ও রিয়েল-টাইম লিসেনার
    db.collection('users').doc(user.uid).collection('transactions')
      .orderBy('createdAt','desc').limit(20).onSnapshot(snap => {
        if(snap && !snap.empty) {
          const txList = snap.docs.map(d => ({
            id: d.id,
            title: d.data().title,
            amount: d.data().amount,
            positive: d.data().positive,
            date: d.data().createdAt ? new Date(d.data().createdAt.toDate()).toLocaleString() : '',
          }));

          const latestTx = txList[0];
          if (state.lastTxId && state.lastTxId !== latestTx.id) {
            const icon = latestTx.positive ? '🎉' : '🔔';
            showToast(`${icon} ${latestTx.title}: ৳${latestTx.amount.toFixed(2)}`, latestTx.positive ? 'success' : 'error');
          }
          state.lastTxId = latestTx.id;

          state.transactions = txList;
          renderTransactions();
        }
      });

    // ৩. ওয়ান-টাইম ডাটা লোডার
    loadCompletedTasks(user.uid);
    loadVisitedTasks(user.uid);
    loadRedeemedCodes(user.uid);

    // ৪. অ্যাপ কনফিগ ও নোটিশবোর্ড রিয়েল-টাইম লিসেনার
    db.collection('app_config').doc('main').onSnapshot(doc => {
      if(!doc.exists) return;
      const d = doc.data();
      if(d.notice) {
        const nb = document.getElementById('noticeText');
        if(nb) nb.textContent = d.notice;
      }
      if(d.dailyTasks) { state.dailyTasks = d.dailyTasks; renderDailyJobs(); }
      if(d.visitTasks) { state.visitTasks = d.visitTasks; renderVisitingJobs(); }
      if(d.giftCodes) { state.appGiftCodes = d.giftCodes; }
    });

    getAppSettings();
    loadTeamMembers(user.uid);
    loadLeaderboard();
    loadJobHistory(user.uid);

  } else {
    document.getElementById('authPage').style.display = 'flex';
    document.getElementById('activationPage').style.display = 'none';
    const ab = document.getElementById('activationBanner');
    if(ab) ab.style.display = 'none';
    showAuthLoading(false);
  }
});

// ============ ACCOUNT ACTIVATION FUNCTIONS ============
async function activateWithBalance() {
  const user = auth.currentUser;
  if(!user) return;
  const actAmt = appSettings.activationCharge || 100;
  if(state.balance.main < actAmt) {
    showToast('আপনার অ্যাকাউন্টে পর্যাপ্ত ব্যালেন্স নেই (কমপক্ষে ৳' + actAmt + ' প্রয়োজন)', 'error');
    return;
  }
  
  if(!confirm('আপনি কি আপনার ব্যালেন্স থেকে ৳' + actAmt + ' কেটে অ্যাকাউন্ট একটিভ করতে চান?')) return;

  try {
    state.selfAction = true;
    const newBal = state.balance.main - actAmt;
    
    await db.collection('users').doc(user.uid).update({
      balance: newBal,
      status: 'active'
    });
    
    await db.collection('users').doc(user.uid).collection('transactions').add({
      title: 'Account Activated (Balance)',
      amount: actAmt,
      positive: false,
      createdAt: firebase.firestore.FieldValue.serverTimestamp()
    });
    
    state.balance.main = newBal;
    updateBalanceUI();
    showToast('আপনার অ্যাকাউন্ট সফলভাবে একটিভ হয়েছে! 🎉', 'success');
    document.getElementById('activationPage').style.display = 'none';
  } catch(e) {
    showToast('Error: ' + e.message, 'error');
  }
}

// ── Activation Prompt ──────────────────────────────────
function showActivationPrompt() {
  // Small toast + scroll to activation banner
  showToast('🔒 আগে অ্যাকাউন্ট একটিভ করুন!', 'error');
  // Show activation page
  setTimeout(() => {
    document.getElementById('activationPage').style.display = 'flex';
  }, 600);
}

async function submitActivationRequest() {
  const user = auth.currentUser;
  if(!user) return;
  
  const method = document.getElementById('actMethod').value;
  const sender = document.getElementById('actSender').value.trim();
  const trxid = document.getElementById('actTrx').value.trim();
  
  if(!method) { showToast('সেন্ড মানি করার মাধ্যম সিলেক্ট করুন', 'error'); return; }
  if(!sender) { showToast('সেন্ডার মোবাইল নম্বর দিন', 'error'); return; }
  if(!trxid) { showToast('TrxID বা ট্রানজেকশন আইডি দিন', 'error'); return; }
  
  try {
    // অ্যাক্টিভেশন রিকোয়েস্ট সেভ
    await db.collection('activation_requests').add({
      uid: user.uid,
      userId: String(state.user.id),
      name: state.user.name,
      method: method,
      senderNumber: sender,
      trxId: trxid,
      amount: appSettings.activationCharge || 100,
      status: 'pending',
      createdAt: firebase.firestore.FieldValue.serverTimestamp()
    });
    
    showToast('আপনার রিকোয়েস্ট জমা হয়েছে! অ্যাডমিন ভেরিফাই করে অ্যাকাউন্ট একটিভ করে দেবে। ⏳', 'success');
    
    // রিসেট ইনপুট
    document.getElementById('actMethod').value = '';
    document.getElementById('actSender').value = '';
    document.getElementById('actTrx').value = '';
  } catch(e) {
    showToast('Error: ' + e.message, 'error');
  }
}

function showBannedMessage() {
  const authCard = document.querySelector('.auth-card');
  if(authCard) {
    authCard.innerHTML = `
      <div style="text-align:center;padding:20px">
        <div style="font-size:48px;margin-bottom:16px">🚫</div>
        <div style="font-size:18px;font-weight:700;color:#ef4444;margin-bottom:8px">অ্যাকাউন্ট Banned</div>
        <div style="font-size:13px;color:var(--text-muted)">আপনার অ্যাকাউন্ট Admin কর্তৃক Banned করা হয়েছে। সহায়তার জন্য যোগাযোগ করুন।</div>
      </div>
    `;
  }
}

function loadUserIntoApp(data, uid) {
  // Activation banner control
  const _ab = document.getElementById('activationBanner');
  if(_ab) _ab.style.display = (data.status === 'inactive') ? 'block' : 'none';
  state.user.name = data.name || 'User';
  state.user.id = data.userId || '---';
  state.user.joined = data.joined || '';
  state.user.uid = uid;
  state.user.photoUrl = data.photoUrl || '';
  state.balance.main = data.balance || 0;
  state.balance.refer = data.referBalance || 0;

  const name = data.name || 'User';
  const userId = data.userId || '---';
  const joined = data.joined || '';
  const photoUrl = data.photoUrl || '';

  setElText('heroName', name);
  setElText('profileName', name);
  setElText('sidebarName', name);

  document.querySelectorAll('.hero-badge').forEach((el, i) => {
    if(i === 0) el.innerHTML = `<i class="fas fa-id-badge"></i> ID: ${userId}`;
    if(i === 1) el.innerHTML = `<i class="fas fa-calendar"></i> ${joined}`;
  });
  const sidId = document.querySelector('.sidebar-id');
  if(sidId) sidId.textContent = `ID: ${userId} • Joined: ${joined}`;
  document.querySelectorAll('.profile-badge').forEach((el,i) => {
    if(i===0) el.innerHTML = `<i class="fas fa-id-badge"></i> ID: ${userId}`;
  });

  const refEl = document.getElementById('refLink');
  if(refEl) {
    const myRefCode = data.referCode || uid;
    const base = window.location.origin + window.location.pathname;
    const fullRefLink = base + '?ref=' + myRefCode;
    refEl.textContent = fullRefLink;
    refEl.dataset.fullLink = fullRefLink;
  }

  // Status badge update
  const isActive = data.status !== 'inactive';
  state.user.status = data.status || 'inactive';
  const heroBadge = document.getElementById('heroStatusBadge');
  if(heroBadge) {
    if(isActive) {
      heroBadge.style.background = 'rgba(74,222,128,0.2)';
      heroBadge.style.color = '#16a34a';
      heroBadge.innerHTML = '<div class="status-dot" style="background:#22c55e"></div> Active';
    } else {
      heroBadge.style.background = 'rgba(239,68,68,0.15)';
      heroBadge.style.color = '#dc2626';
      heroBadge.innerHTML = '<i class="fas fa-lock" style="font-size:9px"></i> Inactive';
    }
  }
  const profBadge = document.getElementById('profileStatusBadge');
  if(profBadge) {
    if(isActive) {
      profBadge.style.background = 'rgba(74,222,128,0.25)';
      profBadge.style.color = '';
      profBadge.innerHTML = '<div class="status-dot"></div> Active';
    } else {
      profBadge.style.background = 'rgba(239,68,68,0.15)';
      profBadge.style.color = '#dc2626';
      profBadge.innerHTML = '<i class="fas fa-lock" style="font-size:9px;margin-right:3px"></i> Inactive';
    }
  }

  setAvatars(photoUrl, name);
  updateBalanceUI();
  const wdRef = document.getElementById('wdReferBal');
  if(wdRef) wdRef.textContent = '৳ ' + (data.referBalance||0).toFixed(2);

  const updateName = document.getElementById('updateName');
  const updatePhotoUrl = document.getElementById('updatePhotoUrl');
  const updatePhone = document.getElementById('updatePhone');
  const updateBkash = document.getElementById('updateBkash');
  const updateNagad = document.getElementById('updateNagad');
  if(updateName) updateName.value = name;
  if(updatePhotoUrl) updatePhotoUrl.value = photoUrl;
  if(updatePhone) updatePhone.value = data.phone || '';
  if(updateBkash) updateBkash.value = data.bkash || '';
  if(updateNagad) updateNagad.value = data.nagad || '';
}

function setElText(id, val) {
  const el = document.getElementById(id);
  if(el) el.textContent = val;
}

function setAvatars(photoUrl, name) {
  ['heroAvatar','sidebarAvatar','profileAvatarEl'].forEach(id => {
    const el = document.getElementById(id);
    if(!el) return;
    if(photoUrl) {
      el.innerHTML = `<img src="${photoUrl}" onerror="this.parentElement.innerHTML='<i class=\\'fas fa-user\\'></i>'" alt="Photo" style="width:100%;height:100%;object-fit:cover;border-radius:50%">`;
    } else {
      el.innerHTML = `<i class="fas fa-user" style="color:#fff"></i>`;
    }
  });
}

const leaderboardData = [];
const membershipPlans = [
  { name:'Silver', price:99, dailyEarn:20, badge:'fas fa-shield-alt', color:'#9ca3af' },
  { name:'Gold', price:199, dailyEarn:45, badge:'fas fa-crown', color:'#f59e0b' },
  { name:'Platinum', price:399, dailyEarn:100, badge:'fas fa-gem', color:'#8b5cf6' },
];

// ============ PAGE NAVIGATION ============
const pageMap = {
  home: 'nav-home', wallet: 'nav-wallet', team: 'nav-team', profile: 'nav-profile',
};

function showPage(id) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  const el = document.getElementById('page-' + id);
  if(el) { el.classList.add('active'); window.scrollTo(0,0); }

  document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
  if(pageMap[id]) { const nav = document.getElementById(pageMap[id]); if(nav) nav.classList.add('active'); }

  if(id === 'dailyJob') renderDailyJobs();
  if(id === 'visitingJob') renderVisitingJobs();
  if(id === 'leaderboard') loadLeaderboard();
  if(id === 'membership') renderMembership();
  if(id === 'wallet') updateWalletUI();
  if(id === 'jobHistory') renderJobHistory();
}

// ============ SIDEBAR ============
function openSidebar() { document.getElementById('sidebarOverlay').classList.add('open'); }
function closeSidebar() { document.getElementById('sidebarOverlay').classList.remove('open'); }

// ============ TOAST ============
function showToast(msg, type='') {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.className = 'toast show ' + type;
  setTimeout(() => t.className = 'toast', 3000);
}

// ============ MODAL ============
function showModal(id) { document.getElementById(id).classList.add('open'); }
function closeModal(id) { document.getElementById(id).classList.remove('open'); }

// ============ BALANCE ============
function updateBalanceUI() {
  const fmt = '৳ ' + state.balance.main.toFixed(2);
  ['homeBalance','wdMainBal','wdDisplayBal','profileBalance'].forEach(id => {
    const el = document.getElementById(id); if(el) el.textContent = fmt;
  });
  const wb = document.getElementById('walletBalance');
  if(wb) wb.textContent = '৳ ' + (state.balance.main + state.balance.refer).toFixed(2);
}

function updateBalance(amount) {
  state.balance.main += amount;
  if(state.balance.main < 0) state.balance.main = 0;
  updateBalanceUI();
}

async function saveBalanceToFirestore(newMain, newRefer) {
  const user = auth.currentUser;
  if(!user) return;
  try {
    const updates = {};
    if(newMain !== undefined) updates.balance = newMain;
    if(newRefer !== undefined) updates.referBalance = newRefer;
    await db.collection('users').doc(user.uid).update(updates);
  } catch(e) { console.error('Balance save error:', e); }
}

async function addTransaction(title, amount, positive) {
  const user = auth.currentUser;
  if(user) {
    try {
      await db.collection('users').doc(user.uid).collection('transactions').add({
        title, amount, positive,
        createdAt: firebase.firestore.FieldValue.serverTimestamp(),
      });
    } catch(e) {}
  }
}

function renderTransactions() {
  const el = document.getElementById('transactionHistory');
  if(!state.transactions.length) { el.innerHTML = '<div class="empty-state"><i class="fas fa-receipt"></i><p>No transactions yet</p></div>'; return; }
  el.innerHTML = state.transactions.slice(0,20).map(t => `
    <div class="history-item">
      <div class="hi-icon" style="background:${t.positive?'#f0fdf4':'#fef2f2'}">
        <i class="fas ${t.positive?'fa-arrow-down':'fa-arrow-up'}" style="color:${t.positive?'#22c55e':'#ef4444'}"></i>
      </div>
      <div class="hi-info">
        <div class="hi-title">${t.title}</div>
        <div class="hi-date">${t.date}</div>
      </div>
      <div class="hi-amount ${t.positive?'positive':'negative'}">${t.positive?'+':'-'}৳${Math.abs(t.amount).toFixed(2)}</div>
    </div>
  `).join('');
}

// ============ DAILY JOBS ============
function renderDailyJobs() {
  const el = document.getElementById('dailyJobList');
  if(!el) return;
  const jobs = state.dailyTasks.length ? state.dailyTasks : [];
  const completed = state.completedTasks.size;
  const countEl = document.getElementById('completedTasks');
  if(countEl) countEl.textContent = completed;

  if(!jobs.length) {
    el.innerHTML = '<div class="empty-state"><i class="fas fa-briefcase"></i><p>কোনো task নেই</p></div>';
    return;
  }

  el.innerHTML = jobs.map(j => {
    const done = state.completedTasks.has(j.id);
    const waitSec = parseInt(j.time) || 20; 
    const link = j.link || '';
    return `
    <div class="task-card" style="${done?'opacity:0.65':''}">
      <div class="task-title">${j.title}</div>
      <div class="task-meta">
        <div class="task-reward"><i class="fas fa-coins"></i> ৳${j.reward}.00</div>
        <div class="task-time"><i class="fas fa-clock"></i> ${j.time || '20s'}</div>
      </div>
      ${done
        ? `<button class="btn" style="background:#f0fdf4;color:#22c55e;border:2px solid #bbf7d0" disabled><i class="fas fa-check-circle"></i> Completed</button>`
        : `<button class="btn btn-primary" onclick="startDailyJob(${j.id}, ${j.reward}, '${j.title.replace(/'/g,"\\'")}', '${link}', ${waitSec}, event)"><i class="fas fa-play"></i> Start Task</button>`
      }
    </div>`;
  }).join('');
}

async function startDailyJob(id, reward, title, link, waitSec, ev) {
  const user = auth.currentUser;
  if(!user || state.completedTasks.has(id)) return;
  // Inactive check
  if(state.user.status === 'inactive') {
    showActivationPrompt();
    return;
  }

  const btn = ev.currentTarget;
  btn.disabled = true;

  if(link && link.startsWith('http')) {
    window.open(link, '_blank');
  } else {
    showToast('টাস্ক শুরু হচ্ছে...', 'success');
  }

  let sec = waitSec || 20;
  const countdown = setInterval(() => {
    btn.innerHTML = `<i class="fas fa-spinner fa-spin"></i> অপেক্ষা করুন... ${sec}s`;
    sec--;
    if(sec < 0) {
      clearInterval(countdown);
      completeJob(id, reward, title);
    }
  }, 1000);
}

async function completeJob(id, reward, title) {
  const user = auth.currentUser;
  if(!user) return;
  if(state.completedTasks.has(id)) return;

  state.selfAction = true; 
  state.completedTasks.add(id);
  const newBal = state.balance.main + reward;
  state.balance.main = newBal;
  updateBalanceUI();

  state.jobHistory.unshift({ title, reward, date: new Date().toLocaleString(), status: 'Approved' });
  renderDailyJobs();
  showToast(`+৳${reward} earned!`, 'success');

  try {
    await db.collection('users').doc(user.uid).update({
      balance: firebase.firestore.FieldValue.increment(reward),
    });
    await db.collection('users').doc(user.uid).collection('transactions').add({
      title, amount: reward, positive: true,
      createdAt: firebase.firestore.FieldValue.serverTimestamp(),
    });
    await db.collection('users').doc(user.uid).collection('completedTasks').doc(String(id)).set({
      completedAt: firebase.firestore.FieldValue.serverTimestamp(),
    });
  } catch(e) { console.error(e); }
}

async function loadCompletedTasks(uid) {
  try {
    const snap = await db.collection('users').doc(uid).collection('completedTasks').get();
    snap.docs.forEach(d => state.completedTasks.add(Number(d.id) || d.id));
    renderDailyJobs();
  } catch(e) {}
}

// ============ VISITING JOBS ============
function renderVisitingJobs() {
  const el = document.getElementById('visitingJobList');
  if(!el) return;
  const jobs = state.visitTasks.length ? state.visitTasks : [];
  const countEl = document.getElementById('visitCompleted');
  if(countEl) countEl.textContent = state.visitCompleted.size;

  if(!jobs.length) {
    el.innerHTML = '<div class="empty-state"><i class="fas fa-globe"></i><p>কোনো visit task নেই</p></div>';
    return;
  }

  el.innerHTML = jobs.map(j => {
    const done = state.visitCompleted.has(j.id);
    return `
    <div class="task-card" style="${done?'opacity:0.65':''}">
      <div class="task-title">${j.title}</div>
      <div class="task-meta">
        <div class="task-reward"><i class="fas fa-coins"></i> ৳${j.reward}.00</div>
        <div class="task-time"><i class="fas fa-clock"></i> ${j.wait||20}s</div>
      </div>
      ${done
        ? `<button class="btn" style="background:#f0fdf4;color:#22c55e;border:2px solid #bbf7d0" disabled><i class="fas fa-check-circle"></i> Completed</button>`
        : `<button class="btn btn-primary" onclick="startVisit(${j.id}, ${j.reward}, '${j.title.replace(/'/g,"\\'")}', '${j.link||''}', ${j.wait||20}, event)"><i class="fas fa-external-link-alt"></i> Visit Now</button>`
      }
    </div>`;
  }).join('');
}

async function startVisit(id, reward, title, link, waitSec, ev) {
  const user = auth.currentUser;
  if(!user || state.visitCompleted.has(id)) return;

  const btn = ev.currentTarget; 
  btn.disabled = true;

  if(link && link.startsWith('http')) {
    window.open(link, '_blank');
  } else {
    showToast('টাস্ক শুরু হচ্ছে...', 'success');
  }

  let sec = waitSec || 20;
  const countdown = setInterval(() => {
    btn.innerHTML = `<i class="fas fa-spinner fa-spin"></i> অপেক্ষা করুন... ${sec}s`;
    sec--;
    if(sec < 0) {
      clearInterval(countdown);
      completeVisitJob(id, reward, title);
    }
  }, 1000);
}

async function completeVisitJob(id, reward, title) {
  const user = auth.currentUser;
  if(!user) return;
  state.selfAction = true; 
  state.visitCompleted.add(id);
  state.balance.main += reward;
  updateBalanceUI();
  renderVisitingJobs();
  showToast(`+৳${reward} earned!`, 'success');

  try {
    await db.collection('users').doc(user.uid).update({
      balance: firebase.firestore.FieldValue.increment(reward),
    });
    await db.collection('users').doc(user.uid).collection('transactions').add({
      title, amount: reward, positive: true,
      createdAt: firebase.firestore.FieldValue.serverTimestamp(),
    });
    await db.collection('users').doc(user.uid).collection('visitedTasks').doc(String(id)).set({
      completedAt: firebase.firestore.FieldValue.serverTimestamp(),
    });
  } catch(e) {}
}

async function loadVisitedTasks(uid) {
  try {
    const snap = await db.collection('users').doc(uid).collection('visitedTasks').get();
    snap.docs.forEach(d => state.visitCompleted.add(Number(d.id) || d.id));
    renderVisitingJobs();
  } catch(e) {}
}

// ============ GIFT CODE SYSTEM ============
async function redeemGiftCode() {
  const user = auth.currentUser;
  if(!user) return;
  const input = document.getElementById('giftCodeInput');
  const code = input.value.trim().toUpperCase();
  if(!code) { showToast('Please enter a gift code', 'error'); return; }

  try {
    const usedDoc = await db.collection('users').doc(user.uid).collection('redeemedCodes').doc(code).get();
    if(usedDoc.exists) { showToast('Code already redeemed!', 'error'); return; }

    const configDoc = await db.collection('app_config').doc('main').get();
    const giftCodes = configDoc.exists ? (configDoc.data().giftCodes || {}) : state.appGiftCodes;

    if(!giftCodes[code]) { showToast('Invalid gift code!', 'error'); return; }

    const amt = giftCodes[code];
    state.selfAction = true; 
    const newBal = state.balance.main + amt;

    await db.collection('users').doc(user.uid).update({
      balance: firebase.firestore.FieldValue.increment(amt),
    });
    await db.collection('users').doc(user.uid).collection('redeemedCodes').doc(code).set({
      amount: amt, redeemedAt: firebase.firestore.FieldValue.serverTimestamp(),
    });
    await db.collection('users').doc(user.uid).collection('transactions').add({
      title: 'Gift Code: ' + code, amount: amt, positive: true,
      createdAt: firebase.firestore.FieldValue.serverTimestamp(),
    });

    state.balance.main = newBal;
    state.redeemedCodes.push(code);
    state.appGiftCodes = giftCodes;
    updateBalanceUI();
    input.value = '';
    renderGiftHistory();
    showToast(`+৳${amt} redeemed! 🎁`, 'success');
  } catch(e) {
    showToast('Error: ' + e.message, 'error');
  }
}

function renderGiftHistory() {
  const el = document.getElementById('giftHistory');
  if(!el) return;
  if(!state.redeemedCodes.length) {
    el.innerHTML = '<div class="empty-state"><i class="fas fa-gift"></i><p>No codes redeemed yet</p></div>';
    return;
  }
  el.innerHTML = state.redeemedCodes.map(c => `
    <div class="history-item">
      <div class="hi-icon" style="background:#f0fdf4"><i class="fas fa-gift" style="color:#22c55e"></i></div>
      <div class="hi-info"><div class="hi-title">Code: ${c}</div><div class="hi-date">Redeemed</div></div>
      <div class="hi-amount positive">+৳${state.appGiftCodes[c]||'?'}</div>
    </div>
  `).join('');
}

async function loadRedeemedCodes(uid) {
  try {
    const snap = await db.collection('users').doc(uid).collection('redeemedCodes').get();
    state.redeemedCodes = snap.docs.map(d => d.id);
    renderGiftHistory();
  } catch(e) {}
}

// ============ WITHDRAW ============
function selectBalanceTab(el, type) {
  document.querySelectorAll('.balance-tab').forEach(t => t.classList.remove('active'));
  el.classList.add('active');
  state.activeWithdrawTab = type;
  const bal = type === 'main' ? state.balance.main : state.balance.refer;
  const wdDisp = document.getElementById('wdDisplayBal');
  if(wdDisp) wdDisp.textContent = '৳ ' + bal.toFixed(2);
}

function selectAmount(el, amount, charge) {
  document.querySelectorAll('.withdraw-amount-btn').forEach(b => b.classList.remove('selected'));
  el.classList.add('selected');
  state.selectedWithdrawAmount = amount;
  state.selectedWithdrawCharge = charge;
}

async function processWithdraw() {
  const user = auth.currentUser;
  if(!user) return;
  const method = document.getElementById('withdrawMethod').value;
  const account = document.getElementById('withdrawAccount').value.trim();
  if(!method) { showToast('Please select a method', 'error'); return; }
  if(!account) { showToast('Please enter account number', 'error'); return; }
  if(!state.selectedWithdrawAmount) { showToast('Please select an amount', 'error'); return; }

  const bal = state.activeWithdrawTab === 'main' ? state.balance.main : state.balance.refer;
  const minWithdraw = appSettings.minWithdraw || 60;

  if(state.selectedWithdrawAmount < minWithdraw) {
    showToast(`Minimum withdrawal ৳${minWithdraw}!`, 'error'); return;
  }
  if(bal < state.selectedWithdrawAmount) {
    showToast('Insufficient balance!', 'error'); return;
  }

  try {
    const charge = state.selectedWithdrawCharge || 0;
    state.selfAction = true; 
    const newBal = bal - state.selectedWithdrawAmount;
    if(state.activeWithdrawTab === 'main') {
      await db.collection('users').doc(user.uid).update({ balance: newBal });
      state.balance.main = newBal;
    } else {
      await db.collection('users').doc(user.uid).update({ referBalance: newBal });
      state.balance.refer = newBal;
    }
    updateBalanceUI();

    await db.collection('withdrawals').add({
      userId: String(state.user.id),
      uid: user.uid,
      name: state.user.name,
      method, account,
      amount: state.selectedWithdrawAmount,
      charge,
      balanceType: state.activeWithdrawTab,
      status: 'pending',
      createdAt: firebase.firestore.FieldValue.serverTimestamp(),
    });

    await db.collection('users').doc(user.uid).collection('transactions').add({
      title: `Withdraw via ${method} — Pending`,
      amount: state.selectedWithdrawAmount, positive: false,
      createdAt: firebase.firestore.FieldValue.serverTimestamp(),
    });

    showToast('Withdrawal request submitted! ✅', 'success');
    document.querySelectorAll('.withdraw-amount-btn').forEach(b => b.classList.remove('selected'));
    state.selectedWithdrawAmount = null;
  } catch(e) {
    showToast('Error: ' + e.message, 'error');
  }
}

// ============ SELL INTEGRATED SUBMISSIONS ============
async function submitSell(type) {
  const user = auth.currentUser;
  if(!user) return;
  // Inactive check
  if(state.user.status === 'inactive') {
    showActivationPrompt();
    return;
  }
  
  let dataObj = {
    uid: user.uid,
    name: state.user.name,
    type: type,
    status: 'pending',
    createdAt: firebase.firestore.FieldValue.serverTimestamp()
  };

  if(type === 'facebook') {
    const fbUID = document.getElementById('fbUID').value.trim();
    const fbPhone = document.getElementById('fbPhone').value.trim();
    const fbPass = document.getElementById('fbPass').value.trim();
    const fbCookies = document.getElementById('fbCookies').value.trim();

    if(!fbUID) { showToast('UID বা প্রোফাইল লিংক দিন', 'error'); return; }
    if(!fbPass) { showToast('পাসওয়ার্ড দিন', 'error'); return; }

    dataObj.fbUID = fbUID;
    dataObj.fbPhone = fbPhone;
    dataObj.fbPass = fbPass;
    dataObj.fbCookies = fbCookies;
  }
  
  else if(type === 'gmail') {
    const gmailAddress = document.getElementById('gmEmail').value.trim();
    const gmailPassword = document.getElementById('gmPass').value.trim();
    const recoveryEmail = document.getElementById('gmRecovery').value.trim();

    if(!gmailAddress) { showToast('Gmail ঠিকানা দিন', 'error'); return; }
    if(!gmailPassword) { showToast('পাসওয়ার্ড দিন', 'error'); return; }

    dataObj.gmailAddress = gmailAddress;
    dataObj.gmailPassword = gmailPassword;
    dataObj.recoveryEmail = recoveryEmail;
  }
  
  else if(type === 'instagram') {
    const username = document.getElementById('igUser').value.trim();
    const password = document.getElementById('igPass').value.trim();
    const backupCode = document.getElementById('igBackup').value.trim();

    if(!username) { showToast('Username বা লিংক দিন', 'error'); return; }
    if(!password) { showToast('পাসওয়ার্ড দিন', 'error'); return; }

    dataObj.username = username;
    dataObj.password = password;
    dataObj.backupCode = backupCode;
  }

  showToast('সাবমিশনটি পর্যালোচনার জন্য পাঠানো হয়েছে!', 'success');
  
  try {
    await db.collection('submissions').add(dataObj);
    if(type === 'facebook') {
      document.getElementById('fbUID').value = '';
      document.getElementById('fbPhone').value = '';
      document.getElementById('fbPass').value = '';
      document.getElementById('fbCookies').value = '';
    } else if(type === 'gmail') {
      document.getElementById('gmEmail').value = '';
      document.getElementById('gmPass').value = '';
      document.getElementById('gmRecovery').value = '';
    } else if(type === 'instagram') {
      document.getElementById('igUser').value = '';
      document.getElementById('igPass').value = '';
      document.getElementById('igBackup').value = '';
    }
  } catch(e) {
    showToast('Error: ' + e.message, 'error');
  }
}

// ============ POST WORK ============
async function submitWork() {
  const user = auth.currentUser;
  if(!user) return;
  
  const type = document.getElementById('pwType').value;
  const screenshot = document.getElementById('pwScreenshot').value.trim();
  const desc = document.getElementById('pwDesc').value.trim();

  if(!type) { showToast('কাজের ধরন নির্বাচন করুন', 'error'); return; }
  if(!screenshot) { showToast('কাজের স্ক্রিনশট লিংক দিন', 'error'); return; }

  showToast('Work submitted for review!', 'success');
  try {
    await db.collection('postWork').add({
      uid: user.uid,
      name: state.user.name,
      workType: type,
      screenshotLink: screenshot,
      description: desc,
      status: 'pending',
      createdAt: firebase.firestore.FieldValue.serverTimestamp(),
    });
    document.getElementById('pwType').value = '';
    document.getElementById('pwScreenshot').value = '';
    document.getElementById('pwDesc').value = '';
  } catch(e) {
    showToast('Error: ' + e.message, 'error');
  }
}

// ============ WALLET ============
function updateWalletUI() {
  const wb = document.getElementById('walletBalance');
  if(wb) wb.textContent = '৳ ' + (state.balance.main + state.balance.refer).toFixed(2);
}

// ============ JOB HISTORY ============
async function loadJobHistory(uid) {
  try {
    db.collection('users').doc(uid).collection('transactions')
      .where('positive','==',true).orderBy('createdAt','desc').limit(30).onSnapshot(snap => {
        if (snap) {
          state.jobHistory = snap.docs.map(d => ({
            title: d.data().title,
            reward: d.data().amount,
            date: d.data().createdAt ? new Date(d.data().createdAt.toDate()).toLocaleString() : '',
            status: 'Approved',
          }));
          renderJobHistory();
        }
      });
  } catch(e) {}
}

function renderJobHistory() {
  const el = document.getElementById('jobHistoryList');
  if(!el) return;
  if(!state.jobHistory.length) {
    el.innerHTML = '<div class="empty-state"><i class="fas fa-folder-open"></i><p>No job history yet</p></div>';
    return;
  }
  el.innerHTML = state.jobHistory.map(j => `
    <div class="history-item">
      <div class="hi-icon" style="background:#f0fdf4"><i class="fas fa-check" style="color:#22c55e"></i></div>
      <div class="hi-info"><div class="hi-title">${j.title}</div><div class="hi-date">${j.date}</div></div>
      <div class="hi-amount positive">+৳${j.reward}</div>
    </div>
  `).join('');
}

// ============ LEADERBOARD ============
async function loadLeaderboard() {
  const el = document.getElementById('leaderboardList');
  if(!el) return;
  try {
    const snap = await db.collection('users').orderBy('balance','desc').limit(10).get();
    const rankClass = r => r===1?'gold':r===2?'silver':r===3?'bronze':'';
    el.innerHTML = snap.docs.map((d,i) => `
      <div class="lb-item">
        <div class="lb-rank ${rankClass(i+1)}">${i+1}</div>
        <div class="lb-avatar">${(d.data().name||'U').charAt(0)}</div>
        <div class="lb-name">${d.data().name||'User'}</div>
        <div class="lb-amount">৳${(d.data().balance||0).toFixed(0)}</div>
      </div>
    `).join('');
  } catch(e) {
    if(el) el.innerHTML = '<div class="empty-state"><i class="fas fa-trophy"></i><p>Leaderboard loading...</p></div>';
  }
}

// ============ TEAM ============
async function loadTeamMembers(uid) {
  try {
    const userDoc = await db.collection('users').doc(uid).get();
    const myRefCode = userDoc.data()?.referCode || uid;

    const snap = await db.collection('users').where('referredBy','==',myRefCode).get();
    state.members = snap.docs.map(d => ({
      name: d.data().name || 'User',
      joined: d.data().joined || '',
      balance: d.data().balance || 0,
    }));

    const totalRef = document.getElementById('totalReferrals');
    const refBal = document.getElementById('referBalance');
    const profileRef = document.getElementById('profileReferrals');
    if(totalRef) totalRef.textContent = state.members.length;
    if(refBal) refBal.textContent = '৳' + (userDoc.data()?.referBalance || 0).toFixed(2);
    if(profileRef) profileRef.textContent = state.members.length;

    const el = document.getElementById('teamMembers');
    if(!el) return;
    if(!state.members.length) {
      el.innerHTML = '<div class="empty-state"><i class="fas fa-users"></i><p>এখনো কেউ join করেনি</p></div>';
      return;
    }
    el.innerHTML = state.members.map(m => `
      <div class="member-item">
        <div class="member-avatar">${m.name.charAt(0).toUpperCase()}</div>
        <div>
          <div class="member-name">${m.name}</div>
          <div class="member-joined">${m.joined}</div>
        </div>
        <div class="member-reward">৳${m.balance}</div>
      </div>
    `).join('');
  } catch(e) { console.error('Team load error:', e); }
}

// ============ MEMBERSHIP ============
function renderMembership() {
  const el = document.getElementById('membershipPlans');
  if(!el) return;
  el.innerHTML = membershipPlans.map(p => `
    <div class="card" style="border:2px solid ${p.color}22">
      <div style="display:flex;align-items:center;gap:12px;margin-bottom:14px">
        <div style="width:48px;height:48px;border-radius:14px;background:${p.color}22;display:flex;align-items:center;justify-content:center;font-size:22px;color:${p.color}">
          <i class="${p.badge}"></i>
        </div>
        <div>
          <div style="font-size:17px;font-weight:700;color:${p.color}">${p.name} Member</div>
          <div style="font-size:12px;color:var(--text-muted)">Daily Earn: ৳${p.dailyEarn}</div>
        </div>
        <div style="margin-left:auto;font-family:'Rajdhani',sans-serif;font-size:22px;font-weight:700;color:var(--primary)">৳${p.price}</div>
      </div>
      <ul style="list-style:none;margin-bottom:14px">
        <li style="font-size:13px;padding:4px 0;color:var(--text-muted)"><i class="fas fa-check" style="color:${p.color};margin-right:8px"></i>Daily ৳${p.dailyEarn} earning bonus</li>
        <li style="font-size:13px;padding:4px 0;color:var(--text-muted)"><i class="fas fa-check" style="color:${p.color};margin-right:8px"></i>Priority withdrawal</li>
        <li style="font-size:13px;padding:4px 0;color:var(--text-muted)"><i class="fas fa-check" style="color:${p.color};margin-right:8px"></i>Special ${p.name} badge</li>
        <li style="font-size:13px;padding:4px 0;color:var(--text-muted)"><i class="fas fa-check" style="color:${p.color};margin-right:8px"></i>Exclusive tasks access</li>
      </ul>
      <button class="btn btn-primary" onclick="buyMembership('${p.name}',${p.price})" style="background:linear-gradient(135deg,${p.color},${p.color}cc)"><i class="fas fa-crown"></i> Activate ${p.name}</button>
    </div>
  `).join('');
}

async function buyMembership(name, price) {
  const user = auth.currentUser;
  if(!user) return;
  if(state.balance.main < price) { showToast('Insufficient balance!', 'error'); return; }
  state.selfAction = true; 
  const newBal = state.balance.main - price;
  try {
    await db.collection('users').doc(user.uid).update({
      balance: newBal, membership: name,
    });
    await db.collection('users').doc(user.uid).collection('transactions').add({
      title: `${name} Membership Activated`, amount: price, positive: false,
      createdAt: firebase.firestore.FieldValue.serverTimestamp(),
    });
    state.balance.main = newBal;
    updateBalanceUI();
    showToast(`${name} membership activated! 🎉`, 'success');
  } catch(e) { showToast('Error: ' + e.message, 'error'); }
}

// ============ PROFILE UPDATE ============
function previewUpdatePhoto(url) {
  const prev = document.getElementById('updatePhotoPreview');
  if(!prev) return;
  if(url && url.startsWith('http')) {
    prev.innerHTML = `<img src="${url}" onerror="this.parentElement.innerHTML='<i class=\\'fas fa-user\\'></i>'" style="width:100%;height:100%;object-fit:cover;border-radius:50%">`;
  } else {
    prev.innerHTML = '<i class="fas fa-user"></i>';
  }
}

async function updateProfile() {
  const user = auth.currentUser;
  if(!user) return;
  const name = document.getElementById('updateName').value.trim();
  const phone = document.getElementById('updatePhone').value.trim();
  const bkash = document.getElementById('updateBkash').value.trim();
  const nagad = document.getElementById('updateNagad').value.trim();
  const photoUrl = document.getElementById('updatePhotoUrl').value.trim();
  if(!name) { showToast('নাম দিন', 'error'); return; }
  try {
    await db.collection('users').doc(user.uid).update({ name, phone, bkash, nagad, photoUrl });
    await user.updateProfile({ displayName: name, photoURL: photoUrl || null });
    state.user.name = name;
    state.user.photoUrl = photoUrl;
    setElText('heroName', name);
    setElText('profileName', name);
    setElText('sidebarName', name);
    setAvatars(photoUrl, name);
    showToast('প্রোফাইল আপডেট হয়েছে! ✅', 'success');
  } catch(e) { showToast('Error: ' + e.message, 'error'); }
}

async function changePassword() {
  const user = auth.currentUser;
  if(!user) return;
  const newPass = document.getElementById('newPassword').value;
  const confirmPass = document.getElementById('confirmPassword').value;
  if(newPass.length < 6) { showToast('পাসওয়ার্ড কমপক্ষে ৬ অক্ষর', 'error'); return; }
  if(newPass !== confirmPass) { showToast('পাসওয়ার্ড মিলছে না', 'error'); return; }
  try {
    await user.updatePassword(newPass);
    document.getElementById('newPassword').value = '';
    document.getElementById('confirmPassword').value = '';
    showToast('পাসওয়ার্ড পরিবর্তন হয়েছে! 🔐', 'success');
  } catch(e) {
    if(e.code === 'auth/requires-recent-login') {
      showToast('আবার Login করুন তারপর চেষ্টা করুন', 'error');
    } else { showToast('Error: ' + e.message, 'error'); }
  }
}

// ============ COPY & SHARE ============
function copyRef() {
  const refEl = document.getElementById('refLink');
  const link = refEl?.dataset?.fullLink || refEl?.textContent || '';
  navigator.clipboard.writeText(link).then(() => {
    showToast('✅ Referral link copied!', 'success');
  }).catch(() => {
    const ta = document.createElement('textarea');
    ta.value = link;
    document.body.appendChild(ta);
    ta.select();
    document.execCommand('copy');
    document.body.removeChild(ta);
    showToast('✅ Referral link copied!', 'success');
  });
}
function shareRef() {
  const refEl = document.getElementById('refLink');
  const link = refEl?.dataset?.fullLink || refEl?.textContent || '';
  if(navigator.share) {
    navigator.share({
      title: 'TK Earn — টাকা আয় করুন',
      text: '🎉 TK Earn এ join করুন এবং প্রতিদিন টাকা আয় করুন!',
      url: link
    });
  } else {
    copyRef();
  }
}

function copyText(id) {
  const text = document.getElementById(id).textContent;
  navigator.clipboard.writeText(text).catch(()=>{});
  showToast('Copied!', 'success');
}

async function processTransfer() {
  const user = auth.currentUser;
  if(!user) return;
  showToast('Transfer submitted!', 'success');
  closeModal('transferModal');
}

// ============ LOGOUT ============
function logout() {
  if(confirm('Are you sure you want to logout?')) {
    auth.signOut().then(() => {
      showToast('Logged out successfully');
      setTimeout(() => location.reload(), 800);
    });
  }
}

// ============ AUTO-DETECT REFERRAL FROM URL ============
(function autoFillRef() {
  try {
    const params = new URLSearchParams(window.location.search);
    const refParam = params.get('ref');
    if(refParam) {
      const regRefEl = document.getElementById('regRef');
      if(regRefEl) regRefEl.value = refParam;
      switchAuthTab && switchAuthTab('register');
    }
  } catch(e) {}
})();
</script>
</body>
</html>
