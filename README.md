# ATTENDANCE-MONITORING-SYSTEM
group project
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1.0"/>
<title>ICCT Attendance Monitoring System</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --navy:#0a1f44;--navy2:#112358;--gold:#f5c518;
  --blue:#1565c0;--blue2:#1976d2;
  --green:#15803d;--green2:#16a34a;
  --orange:#c2410c;--orange2:#ea580c;
  --red:#dc2626;--light:#f4f6fb;--white:#fff;
  --gray:#64748b;--lgray:#e2e8f0;--dgray:#334155;
  --shadow:0 2px 12px rgba(10,31,68,.13);
}
body{font-family:'Segoe UI',sans-serif;background:var(--light);min-height:100vh;color:var(--dgray)}
.hidden{display:none!important}
 
/* HEADER */
.header{background:linear-gradient(135deg,var(--navy) 0%,var(--navy2) 100%);color:#fff;padding:0 2rem;display:flex;align-items:center;justify-content:space-between;box-shadow:0 2px 8px rgba(0,0,0,.25);position:sticky;top:0;z-index:100;min-height:64px}
.hbrand{display:flex;align-items:center;gap:12px}
.logo-circle{width:44px;height:44px;background:var(--gold);border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:800;font-size:14px;color:var(--navy);flex-shrink:0}
.brand-text h1{font-size:15px;font-weight:700;letter-spacing:.4px}
.brand-text p{font-size:11px;opacity:.7;letter-spacing:.3px}
.huser{display:flex;align-items:center;gap:10px}
.ubadge{background:rgba(255,255,255,.12);border:1px solid rgba(255,255,255,.2);border-radius:8px;padding:6px 14px;display:flex;align-items:center;gap:8px}
.role-tag{font-size:10px;font-weight:700;padding:2px 7px;border-radius:4px;text-transform:uppercase;letter-spacing:.5px}
.rt-student{background:var(--gold);color:var(--navy)}
.rt-staff{background:#4ade80;color:#14532d}
.rt-professor{background:#fb923c;color:#431407}
.btn-logout{background:rgba(220,38,38,.75);border:none;color:#fff;padding:7px 16px;border-radius:7px;font-size:12px;font-weight:600;cursor:pointer;transition:.15s}
.btn-logout:hover{background:var(--red)}
 
/* ROLE PAGE */
.role-page{min-height:100vh;display:flex;flex-direction:column;align-items:center;justify-content:center;background:linear-gradient(160deg,var(--navy) 0%,#1e3a6e 55%,#1565c0 100%);padding:2rem}
.role-hero{text-align:center;margin-bottom:2.5rem}
.logo-big{width:80px;height:80px;background:var(--gold);border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:900;font-size:24px;color:var(--navy);margin:0 auto 1rem;box-shadow:0 4px 20px rgba(245,197,24,.3)}
.role-hero h2{color:#fff;font-size:26px;font-weight:700;margin-bottom:4px}
.role-hero p{color:rgba(255,255,255,.6);font-size:14px}
.role-cards{display:grid;grid-template-columns:repeat(3,1fr);gap:1.25rem;max-width:780px;width:100%}
.role-card{background:rgba(255,255,255,.08);border:1.5px solid rgba(255,255,255,.18);border-radius:16px;padding:2rem 1.5rem;text-align:center;cursor:pointer;transition:.2s;color:#fff;position:relative}
.role-card:hover{background:rgba(255,255,255,.15);border-color:var(--gold);transform:translateY(-3px)}
.rc-icon{width:56px;height:56px;border-radius:14px;margin:0 auto 1rem;display:flex;align-items:center;justify-content:center;font-size:26px}
.rc-s .rc-icon{background:rgba(21,101,192,.4)}
.rc-st .rc-icon{background:rgba(22,163,74,.3)}
.rc-p .rc-icon{background:rgba(234,88,12,.3)}
.role-card h3{font-size:16px;font-weight:700;margin-bottom:6px}
.role-card p{font-size:12px;opacity:.6}
.lock-badge{position:absolute;top:12px;right:12px;background:rgba(255,255,255,.15);border:1px solid rgba(255,255,255,.25);border-radius:6px;padding:3px 8px;font-size:10px;font-weight:700;letter-spacing:.4px;color:rgba(255,255,255,.7)}
.staff-notice{margin-top:.6rem;font-size:11px;color:rgba(255,255,255,.5);font-style:italic}
 
/* PIN GATE */
.pin-overlay{min-height:100vh;display:flex;align-items:center;justify-content:center;background:linear-gradient(160deg,#1e1e2e 0%,#0f172a 100%);padding:2rem}
.pin-card{background:#1e293b;border:1px solid rgba(255,255,255,.1);border-radius:20px;padding:2.5rem 2rem;max-width:380px;width:100%;text-align:center}
.pin-lock-icon{width:64px;height:64px;border-radius:16px;margin:0 auto 1.25rem;display:flex;align-items:center;justify-content:center;font-size:28px}
.pli-staff{background:rgba(22,163,74,.25)}
.pli-prof{background:rgba(234,88,12,.25)}
.pin-card h3{color:#f1f5f9;font-size:20px;font-weight:700;margin-bottom:6px}
.pin-card p{color:#94a3b8;font-size:13px;margin-bottom:1.75rem}
.pin-dots{display:flex;gap:10px;justify-content:center;margin-bottom:1.5rem}
.pin-dot{width:14px;height:14px;border-radius:50%;border:2px solid #475569;background:transparent;transition:.15s}
.pin-dot.filled{background:#f1f5f9;border-color:#f1f5f9}
.pin-numpad{display:grid;grid-template-columns:repeat(3,1fr);gap:.6rem;margin-bottom:1.25rem}
.pin-btn{background:#334155;border:none;color:#f1f5f9;border-radius:10px;padding:14px;font-size:20px;font-weight:700;cursor:pointer;transition:.15s}
.pin-btn:hover{background:#475569}
.pin-btn:active{transform:scale(.95)}
.pin-del{background:#3f2020;color:#fca5a5}
.pin-del:hover{background:#7f1d1d}
.pin-error{color:#f87171;font-size:13px;font-weight:600;margin-top:.25rem;min-height:20px}
.pin-hint{color:#64748b;font-size:11px;margin-top:.75rem}
.pin-back{margin-top:.75rem;color:#475569;font-size:12px;cursor:pointer;text-decoration:underline}
.pin-back:hover{color:#94a3b8}
 
/* CHECK-IN */
.checkin-page{max-width:560px;margin:2.5rem auto;padding:0 1rem}
.checkin-card{background:var(--white);border-radius:16px;box-shadow:var(--shadow);overflow:hidden}
.checkin-banner{padding:1.75rem 2rem;color:#fff;display:flex;align-items:center;gap:14px}
.cb-s{background:linear-gradient(135deg,var(--navy),var(--navy2))}
.cb-st{background:linear-gradient(135deg,#14532d,#15803d)}
.cb-p{background:linear-gradient(135deg,#431407,#c2410c)}
.logo-sm{width:48px;height:48px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-weight:900;font-size:15px;flex-shrink:0}
.ls-s{background:var(--gold);color:var(--navy)}
.ls-st{background:#4ade80;color:#14532d}
.ls-p{background:#fb923c;color:#431407}
.checkin-banner h2{font-size:18px;font-weight:700}
.checkin-banner p{font-size:12px;opacity:.7;margin-top:2px}
.checkin-form{padding:2rem}
.form-row{display:grid;grid-template-columns:1fr 1fr;gap:1rem}
.fg{margin-bottom:1.1rem}
.fg label{display:block;font-size:11px;font-weight:700;color:var(--gray);margin-bottom:5px;text-transform:uppercase;letter-spacing:.4px}
.fg input,.fg select{width:100%;padding:10px 14px;border:1.5px solid var(--lgray);border-radius:8px;font-size:14px;color:var(--dgray);background:#fff;transition:.15s;font-family:inherit}
.fg input:focus,.fg select:focus{outline:none;border-color:var(--blue);box-shadow:0 0 0 3px rgba(21,101,192,.1)}
.btn-ci{width:100%;padding:13px;color:#fff;border:none;border-radius:10px;font-size:15px;font-weight:700;cursor:pointer;transition:.2s;margin-top:.5rem}
.bcs{background:linear-gradient(135deg,var(--blue),var(--blue2))}
.bcst{background:linear-gradient(135deg,#14532d,#16a34a)}
.bcp{background:linear-gradient(135deg,#431407,#ea580c)}
.btn-ci:hover{filter:brightness(1.08);transform:translateY(-1px)}
.role-pill{display:inline-flex;align-items:center;gap:6px;background:var(--light);border:1px solid var(--lgray);border-radius:6px;padding:5px 12px;font-size:12px;font-weight:600;color:var(--gray);margin-bottom:1rem}
.dot{width:8px;height:8px;border-radius:50%}
.ds{background:var(--blue)}.dst{background:var(--green)}.dp{background:var(--orange)}
.back-link{text-align:center;margin-top:1rem;font-size:13px;color:var(--gray)}
.back-link span{color:var(--blue);cursor:pointer;font-weight:600}
.back-link span:hover{text-decoration:underline}
.conf-bar{font-size:11px;font-weight:600;letter-spacing:.5px;text-align:center;padding:7px;display:flex;align-items:center;justify-content:center;gap:6px;border-bottom:1px solid #1e293b}
.conf-bar-staff{background:#0f2710;color:#4ade80}
.conf-bar-prof{background:#2a0e00;color:#fb923c}
 
/* QR */
.qr-section{background:var(--light);border-top:1px solid var(--lgray);padding:1.5rem 2rem;text-align:center}
.qr-label{font-size:12px;font-weight:700;color:var(--gray);text-transform:uppercase;letter-spacing:.5px;margin-bottom:.75rem}
.qr-box{display:inline-block;background:#fff;border:2px solid var(--lgray);border-radius:12px;padding:14px;margin-bottom:.75rem;position:relative}
.qr-exp{position:absolute;inset:0;background:rgba(255,255,255,.93);border-radius:10px;display:flex;flex-direction:column;align-items:center;justify-content:center;font-size:13px;font-weight:700;color:var(--red)}
.qr-timer{font-size:22px;font-weight:800;color:var(--navy);margin-bottom:4px;font-variant-numeric:tabular-nums}
.qr-timer.warn{color:#ea580c}.qr-timer.exp{color:var(--red)}
.qr-hint{font-size:11px;color:var(--gray)}
.btn-regen{margin-top:.5rem;padding:7px 18px;background:var(--navy);color:#fff;border:none;border-radius:7px;font-size:12px;font-weight:600;cursor:pointer}
 
/* DASHBOARD */
.dashboard{max-width:1100px;margin:0 auto;padding:2rem 1.5rem}
.dash-hd{display:flex;align-items:center;justify-content:space-between;margin-bottom:1.5rem;flex-wrap:wrap;gap:1rem}
.dash-title h2{font-size:22px;font-weight:700;color:var(--navy)}
.dash-title p{font-size:13px;color:var(--gray)}
.dash-tabs{display:flex;gap:.4rem;background:var(--white);border:1px solid var(--lgray);border-radius:10px;padding:4px}
.tab-btn{padding:7px 16px;border:none;background:transparent;border-radius:7px;font-size:13px;font-weight:600;cursor:pointer;color:var(--gray);transition:.15s}
.tab-btn.active{background:var(--navy);color:#fff}
.scope-chip{display:inline-flex;align-items:center;gap:6px;border-radius:8px;padding:6px 14px;font-size:12px;font-weight:600;margin-bottom:1rem}
.scope-self{background:#fef9c3;color:#78350f;border:1px solid #fde68a}
.scope-own{background:#dbeafe;color:#1e40af;border:1px solid #bfdbfe}
.scope-full{background:#dcfce7;color:#14532d;border:1px solid #bbf7d0}
.stats-row{display:grid;grid-template-columns:repeat(4,1fr);gap:1rem;margin-bottom:1.5rem}
.stat-card{background:var(--white);border-radius:12px;padding:1.1rem 1.25rem;box-shadow:var(--shadow);border-left:4px solid transparent}
.sc-t{border-color:var(--blue)}.sc-d{border-color:var(--green)}.sc-w{border-color:var(--gold)}.sc-r{border-color:var(--orange)}
.stat-label{font-size:11px;font-weight:700;color:var(--gray);text-transform:uppercase;letter-spacing:.4px;margin-bottom:4px}
.stat-val{font-size:28px;font-weight:800;color:var(--navy)}
.stat-sub{font-size:11px;color:var(--gray);margin-top:2px}
.table-card{background:var(--white);border-radius:12px;box-shadow:var(--shadow);overflow:hidden}
.ttbar{padding:1rem 1.5rem;display:flex;align-items:center;justify-content:space-between;border-bottom:1px solid var(--lgray);flex-wrap:wrap;gap:.75rem}
.ttbar h3{font-size:15px;font-weight:700;color:var(--navy)}
.tright{display:flex;gap:.5rem;align-items:center;flex-wrap:wrap}
.sbox{padding:7px 13px;border:1.5px solid var(--lgray);border-radius:7px;font-size:13px;width:180px;font-family:inherit}
.sbox:focus{outline:none;border-color:var(--blue)}
.fsel{padding:7px 10px;border:1.5px solid var(--lgray);border-radius:7px;font-size:12px;font-family:inherit;background:#fff;color:var(--dgray)}
.fsel:focus{outline:none;border-color:var(--blue)}
.btn-exp{padding:7px 14px;background:var(--navy);color:#fff;border:none;border-radius:7px;font-size:12px;font-weight:600;cursor:pointer}
.twrap{overflow-x:auto}
table{width:100%;border-collapse:collapse}
th{padding:10px 14px;font-size:11px;font-weight:700;color:var(--gray);text-transform:uppercase;letter-spacing:.4px;background:var(--light);border-bottom:1px solid var(--lgray);text-align:left;white-space:nowrap}
td{padding:10px 14px;font-size:13px;border-bottom:.5px solid var(--lgray);color:var(--dgray)}
tr:last-child td{border-bottom:none}
tr:hover td{background:#f8fafd}
.badge{display:inline-block;padding:3px 9px;border-radius:5px;font-size:11px;font-weight:700}
.bp{background:#dcfce7;color:#15803d}.ba{background:#fee2e2;color:#b91c1c}.bl{background:#fef9c3;color:#92400e}
.brs{background:#dbeafe;color:#1e40af}.brst{background:#dcfce7;color:#166534}.brp{background:#ffedd5;color:#9a3412}
.mbtn{padding:4px 9px;border:1.5px solid var(--lgray);border-radius:5px;font-size:11px;font-weight:600;cursor:pointer;background:#fff;color:var(--dgray);margin-right:3px;transition:.15s}
.mbtn:hover{background:var(--light);border-color:var(--blue);color:var(--blue)}
.norec{text-align:center;padding:3rem;color:var(--gray);font-size:14px}
.toast{position:fixed;bottom:2rem;right:2rem;background:var(--green);color:#fff;padding:12px 22px;border-radius:10px;font-size:14px;font-weight:600;box-shadow:0 4px 16px rgba(0,0,0,.2);z-index:9999;transform:translateY(100px);opacity:0;transition:.35s cubic-bezier(.34,1.56,.64,1)}
.toast.show{transform:translateY(0);opacity:1}
.toast.err{background:var(--red)}
@media(max-width:680px){
  .role-cards{grid-template-columns:1fr}
  .stats-row{grid-template-columns:1fr 1fr}
  .form-row{grid-template-columns:1fr}
  .header{padding:0 1rem}
  .dashboard{padding:1rem}
}
</style>
</head>
<body>
 
<div class="toast" id="toast"></div>
 
<!-- ═══════════════════════════════════════
     HEADER (shown after login)
════════════════════════════════════════ -->
<div class="header hidden" id="appHeader">
  <div class="hbrand">
    <div class="logo-circle">ICCT</div>
    <div class="brand-text">
      <h1>ICCT Colleges — Attendance System</h1>
      <p>Computer Studies Department</p>
    </div>
  </div>
  <div class="huser">
    <div class="ubadge">
      <span class="role-tag" id="hRoleTag">—</span>
      <span id="hUserName" style="font-weight:600;font-size:13px">—</span>
    </div>
    <button class="btn-logout" onclick="logout()">⏏ Logout</button>
  </div>
</div>
 
<!-- ═══════════════════════════════════════
     ROLE SELECTION
════════════════════════════════════════ -->
<div id="rolePage">
  <div class="role-page">
    <div class="role-hero">
      <div class="logo-big">ICCT</div>
      <h2>Attendance Monitoring System</h2>
      <p>Computer Studies Department &nbsp;·&nbsp; Select your role to continue</p>
    </div>
    <div class="role-cards">
      <div class="role-card rc-s" onclick="showCheckin('student')">
        <div class="rc-icon">🎓</div>
        <h3>Student</h3>
        <p>Log your class attendance and view your own records</p>
      </div>
      <div class="role-card rc-st" onclick="showPinGate('staff')">
        <span class="lock-badge">🔒 Restricted</span>
        <div class="rc-icon">🗂️</div>
        <h3>Staff</h3>
        <p>Authorized personnel only</p>
        <div class="staff-notice">PIN required to access</div>
      </div>
      <div class="role-card rc-p" onclick="showPinGate('professor')">
        <span class="lock-badge">🔒 Restricted</span>
        <div class="rc-icon">👩‍🏫</div>
        <h3>Professor</h3>
        <p>Authorized faculty only</p>
        <div class="staff-notice">PIN required to access</div>
      </div>
    </div>
  </div>
</div>
 
<!-- ═══════════════════════════════════════
     PIN GATE
════════════════════════════════════════ -->
<div id="pinGate" class="hidden">
  <div class="pin-overlay">
    <div class="pin-card">
      <div class="pin-lock-icon" id="pinIcon">🔐</div>
      <h3 id="pinTitle">Restricted Access</h3>
      <p id="pinDesc">Enter your 4-digit PIN to continue.</p>
      <div class="pin-dots" id="pinDots">
        <div class="pin-dot" id="pd0"></div>
        <div class="pin-dot" id="pd1"></div>
        <div class="pin-dot" id="pd2"></div>
        <div class="pin-dot" id="pd3"></div>
      </div>
      <div class="pin-numpad" id="pinNumpad"></div>
      <div class="pin-error" id="pinError"></div>
      <div class="pin-hint" id="pinHint"></div>
      <div class="pin-back" onclick="goRole()">← Back to role selection</div>
    </div>
  </div>
</div>
 
<!-- ═══════════════════════════════════════
     STUDENT CHECK-IN
════════════════════════════════════════ -->
<div id="studentCheckin" class="hidden">
  <div class="checkin-page">
    <div class="checkin-card">
      <div class="checkin-banner cb-s">
        <div class="logo-sm ls-s">ICCT</div>
        <div><h2>Student Check-In</h2><p>Computer Studies Department</p></div>
      </div>
      <div class="checkin-form">
        <div class="role-pill"><span class="dot ds"></span>Student Portal</div>
        <div class="form-row">
          <div class="fg"><label>Full Name *</label><input type="text" id="s-name" placeholder="e.g. Juan dela Cruz"/></div>
          <div class="fg"><label>Student Number *</label><input type="text" id="s-snum" placeholder="e.g. 2024-00123"/></div>
        </div>
        <div class="form-row">
          <div class="fg"><label>Section *</label><input type="text" id="s-sec" placeholder="e.g. BSIT-3A"/></div>
          <div class="fg"><label>Date *</label><input type="date" id="s-date"/></div>
        </div>
        <div class="fg">
          <label>Subject *</label>
          <select id="s-subj">
            <option value="">— Select Subject —</option>
            <option>Programming Languages</option>
            <option>Data Structures &amp; Algorithms</option>
            <option>Database Management Systems</option>
            <option>Web Development</option>
            <option>Computer Networks</option>
            <option>Software Engineering</option>
            <option>Operating Systems</option>
            <option>Artificial Intelligence</option>
            <option>Information Security</option>
            <option>Systems Analysis &amp; Design</option>
            <option>Capstone Project</option>
            <option>Other</option>
          </select>
        </div>
        <button class="btn-ci bcs" onclick="submitCheckin('student')">✅ Check In Now</button>
      </div>
      <div class="qr-section">
        <div class="qr-label">📱 Quick QR Check-In Code</div>
        <div class="qr-box">
          <div id="s-qr"></div>
          <div class="qr-exp hidden" id="s-qr-exp">⛔ Expired<br><small>Click Refresh</small></div>
        </div>
        <div class="qr-timer" id="s-timer">30:00</div>
        <div class="qr-hint">Code expires in 30 minutes</div>
        <br><button class="btn-regen" onclick="regenQR('student')">🔄 Refresh QR</button>
      </div>
    </div>
    <div class="back-link"><span onclick="goRole()">← Back to Role Selection</span></div>
  </div>
</div>
 
<!-- ═══════════════════════════════════════
     STAFF CHECK-IN
════════════════════════════════════════ -->
<div id="staffCheckin" class="hidden">
  <div class="conf-bar conf-bar-staff">🔒 &nbsp;CONFIDENTIAL — AUTHORIZED STAFF ONLY&nbsp; 🔒</div>
  <div class="checkin-page">
    <div class="checkin-card">
      <div class="checkin-banner cb-st">
        <div class="logo-sm ls-st">ICCT</div>
        <div><h2>Staff Check-In</h2><p>Confidential — Computer Studies Department</p></div>
      </div>
      <div class="checkin-form">
        <div class="role-pill"><span class="dot dst"></span>Staff Portal — Restricted</div>
        <div class="form-row">
          <div class="fg"><label>Full Name *</label><input type="text" id="st-name" placeholder="e.g. Maria Santos"/></div>
          <div class="fg"><label>Staff ID *</label><input type="text" id="st-id" placeholder="e.g. STAFF-2024-001"/></div>
        </div>
        <div class="form-row">
          <div class="fg"><label>Department / Section *</label><input type="text" id="st-sec" placeholder="e.g. Admin Office"/></div>
          <div class="fg"><label>Date *</label><input type="date" id="st-date"/></div>
        </div>
        <div class="fg">
          <label>Work Task / Assignment *</label>
          <select id="st-task">
            <option value="">— Select Task —</option>
            <option>Office Administration</option>
            <option>Records Management</option>
            <option>IT Support / Helpdesk</option>
            <option>Laboratory Maintenance</option>
            <option>Student Services</option>
            <option>Finance &amp; Accounting</option>
            <option>Facilities Management</option>
            <option>Library Services</option>
            <option>Enrollment Processing</option>
            <option>General Staff Duty</option>
            <option>Department Coordination</option>
            <option>Other</option>
          </select>
        </div>
        <button class="btn-ci bcst" onclick="submitCheckin('staff')">✅ Check In Now</button>
      </div>
      <div class="qr-section">
        <div class="qr-label">📱 Staff QR Code (Confidential)</div>
        <div class="qr-box">
          <div id="st-qr"></div>
          <div class="qr-exp hidden" id="st-qr-exp">⛔ Expired<br><small>Click Refresh</small></div>
        </div>
        <div class="qr-timer" id="st-timer">30:00</div>
        <div class="qr-hint">Code expires in 30 minutes</div>
        <br><button class="btn-regen" onclick="regenQR('staff')">🔄 Refresh QR</button>
      </div>
    </div>
    <div class="back-link"><span onclick="goRole()">← Logout / Back</span></div>
  </div>
</div>
