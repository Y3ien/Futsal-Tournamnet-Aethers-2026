<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover" />
  <title>Aethers Futsal – Player Registration</title>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg:        #f5ede3;
      --surface:   #fdf7f1;
      --card:      #fffcf8;
      --border:    #e2cdb8;
      --accent:    #8b5e3c;
      --accent-dk: #5c3d24;
      --accent-lt: #c9956a;
      --text:      #2e1a0e;
      --muted:     #9c7a62;
      --err:       #c0392b;
    }

    body {
      font-family: 'Inter', system-ui, -apple-system, sans-serif;
      background: var(--bg);
      min-height: 100vh;
      -webkit-text-size-adjust: 100%;
    }

    /* ── HEADER ── */
    .header {
      background: var(--accent-dk);
      padding: 36px 24px 30px;
      text-align: center;
    }
    .header-eyebrow {
      display: inline-block;
      background: var(--accent-lt);
      color: #fff;
      font-weight: 700;
      font-size: 11px;
      letter-spacing: 0.14em;
      text-transform: uppercase;
      padding: 4px 12px;
      border-radius: 4px;
      margin-bottom: 12px;
    }
    .header h1 {
      font-weight: 900;
      font-size: clamp(1.7rem, 6vw, 2.8rem);
      color: #fff;
      line-height: 1.1;
      text-transform: uppercase;
      letter-spacing: 0.02em;
    }

    /* ── TABS ── */
    .tabs {
      display: flex;
      justify-content: center;
      background: var(--accent-dk);
      border-top: 1px solid rgba(255,255,255,.1);
    }
    .tab-btn {
      flex: 1;
      max-width: 200px;
      padding: 12px 20px;
      background: transparent;
      border: none;
      border-bottom: 3px solid transparent;
      color: rgba(255,255,255,.55);
      font-family: inherit;
      font-size: 13px;
      font-weight: 600;
      letter-spacing: 0.04em;
      text-transform: uppercase;
      cursor: pointer;
    }
    .tab-btn.active { color: #fff; border-bottom-color: var(--accent-lt); }

    /* ── PANEL ── */
    .panel {
      max-width: 620px;
      margin: 32px auto 0;
      padding: 0 16px;
    }

    /* ── CARD ── */
    .card {
      background: var(--card);
      border-radius: 10px;
      border: 1px solid var(--border);
      box-shadow: 0 2px 14px rgba(90,50,20,.08);
      padding: 28px 24px;
    }

    /* ── FIELD ── */
    .field { margin-bottom: 18px; }
    .field label {
      display: block;
      font-size: 11px;
      font-weight: 700;
      letter-spacing: 0.07em;
      text-transform: uppercase;
      color: var(--accent-dk);
      margin-bottom: 6px;
    }
    .field label .opt {
      font-size: 11px;
      color: var(--muted);
      font-weight: 400;
      margin-left: 6px;
      text-transform: none;
      letter-spacing: 0;
    }
    .field label .req { color: var(--err); margin-left: 2px; }
    .field .err-msg { font-size: 12px; color: var(--err); margin-top: 5px; }

    /* ── INPUTS ── */
    input[type=text], input[type=tel], input[type=password], select {
      width: 100%;
      padding: 10px 14px;
      border: 1.5px solid var(--border);
      border-radius: 7px;
      font-family: inherit;
      font-size: 16px;
      color: var(--text);
      background: var(--card);
      outline: none;
      appearance: none;
      -webkit-appearance: none;
    }
    input.has-err, select.has-err {
      border-color: var(--err);
      box-shadow: 0 0 0 3px rgba(192,57,43,.1);
    }
    input:focus, select:focus { border-color: var(--accent); }

    /* ── UPLOAD ── */
    .upload-zone {
      border: 2px dashed var(--border);
      border-radius: 8px;
      padding: 24px 16px;
      text-align: center;
      background: var(--surface);
    }
    .upload-zone .uz-title { font-weight: 600; font-size: 13px; color: var(--text); margin-bottom: 4px; }
    .upload-zone .uz-sub   { font-size: 12px; color: var(--muted); margin-bottom: 14px; }
    .upload-btns { display: flex; gap: 10px; justify-content: center; flex-wrap: wrap; }
    .btn-take   { background: var(--accent-dk); color: #fff; border: none; border-radius: 6px;
                  padding: 10px 20px; font-family: inherit; font-size: 13px; font-weight: 600; cursor: pointer; }
    .btn-choose { background: transparent; color: var(--accent); border: 1.5px solid var(--border);
                  border-radius: 6px; padding: 10px 20px; font-family: inherit; font-size: 13px; font-weight: 600; cursor: pointer; }
    .preview-row {
      display: flex; align-items: center; gap: 12px; padding: 12px;
      border: 1.5px solid var(--border); border-radius: 8px; background: var(--surface);
    }
    .preview-row img { width: 72px; height: 72px; border-radius: 8px; object-fit: cover;
                       border: 1.5px solid var(--border); flex-shrink: 0; }
    .preview-info { min-width: 0; }
    .preview-info .p-name { font-size: 13px; font-weight: 600; word-break: break-all; color: var(--text); }
    .preview-info .p-size { font-size: 11px; color: var(--muted); margin-top: 2px; }
    .preview-info .p-links { display: flex; gap: 12px; margin-top: 8px; }
    .preview-info .p-links a { font-size: 12px; color: var(--accent); text-decoration: underline; cursor: pointer; }

    /* ── BUTTONS ── */
    .btn-primary {
      width: 100%; padding: 14px;
      background: var(--accent); color: #fff;
      border: none; border-radius: 8px;
      font-family: inherit; font-weight: 700; font-size: 15px; cursor: pointer;
      text-transform: uppercase; letter-spacing: 0.05em;
      margin-top: 4px;
      -webkit-tap-highlight-color: transparent;
    }
    .btn-primary:disabled { opacity: .6; cursor: not-allowed; }
    .btn-danger {
      background: #fdf1f0; color: var(--err); border: 1.5px solid #f5b0a8;
      border-radius: 8px; padding: 10px 22px; font-family: inherit;
      font-weight: 700; font-size: 13px; cursor: pointer; margin-top: 20px;
    }
    .btn-outline {
      background: transparent; color: var(--accent); border: 1.5px solid var(--accent);
      border-radius: 8px; padding: 7px 16px; font-family: inherit;
      font-weight: 700; font-size: 12px; cursor: pointer;
      text-transform: uppercase; letter-spacing: 0.04em;
    }
    .btn-card-view {
      background: var(--surface); color: var(--accent); border: 1.5px solid var(--border);
      border-radius: 7px; padding: 6px 12px; font-family: inherit; font-weight: 600; font-size: 12px; cursor: pointer;
    }
    .btn-card-remove {
      background: #fdf1f0; color: var(--err); border: 1.5px solid #f5b0a8;
      border-radius: 7px; padding: 6px 12px; font-family: inherit; font-weight: 600; font-size: 12px; cursor: pointer;
    }

    /* ── SUCCESS / REMOVED ── */
    .success-card {
      background: var(--card); border-radius: 10px; border: 1.5px solid var(--border);
      padding: 36px 28px; text-align: center; box-shadow: 0 2px 14px rgba(90,50,20,.08);
    }
    .success-card.removed { background: #fdecea; border-color: #f5b0a8; }
    .success-card h2 {
      font-weight: 900; font-size: 24px; color: var(--accent-dk);
      margin-bottom: 8px; text-transform: uppercase;
    }
    .success-card.removed h2 { color: var(--err); }
    .success-card p { font-size: 14px; color: var(--muted); line-height: 1.6; margin-bottom: 8px; }
    .success-card.removed p { color: var(--text); margin-bottom: 20px; }
    .timer-badge {
      display: inline-block; background: var(--surface); border: 1px solid var(--border);
      border-radius: 20px; padding: 6px 16px; font-size: 13px; font-weight: 600;
      color: var(--accent); margin: 12px 0 4px;
    }
    .timer-sub { font-size: 12px; color: var(--muted); margin-top: 4px; }

    /* ── ADMIN LIST ── */
    .admin-header {
      display: flex; justify-content: space-between; align-items: center;
      margin-bottom: 24px; flex-wrap: wrap; gap: 10px;
    }
    .admin-header h2 { font-weight: 800; font-size: 20px; color: var(--accent-dk); }
    .admin-header .right { display: flex; gap: 10px; align-items: center; }
    .count-badge {
      background: var(--accent); color: #fff; border-radius: 20px;
      padding: 3px 12px; font-size: 12px; font-weight: 600;
    }
    .pos-section { margin-bottom: 28px; }
    .pos-header {
      display: flex; align-items: center; gap: 8px; margin-bottom: 10px;
      padding-bottom: 8px; border-bottom: 2px solid var(--border);
    }
    .pos-header span { font-weight: 700; font-size: 13px; color: var(--accent-dk);
      text-transform: uppercase; letter-spacing: 0.06em; }
    .pos-count {
      margin-left: auto; background: var(--accent); color: #fff;
      border-radius: 20px; padding: 2px 10px; font-size: 12px; font-weight: 700;
    }
    .player-card {
      display: flex; gap: 14px; align-items: center; padding: 14px 16px;
      background: var(--card); border-radius: 9px; border: 1.5px solid var(--border);
      margin-bottom: 10px; box-shadow: 0 1px 6px rgba(90,50,20,.06);
    }
    .player-card img { width: 52px; height: 52px; border-radius: 8px; object-fit: cover;
      border: 1.5px solid var(--border); flex-shrink: 0; }
    .player-card .info { flex: 1; min-width: 0; }
    .player-card .info .pname { font-weight: 700; font-size: 15px; color: var(--text); margin-bottom: 4px; }
    .player-card .info .pdate { font-size: 11px; color: var(--muted); margin-top: 5px; }
    .player-card .actions { display: flex; gap: 8px; align-self: center; flex-shrink: 0; }

    /* ── PILLS ── */
    .pills { display: flex; gap: 6px; flex-wrap: wrap; }
    .pill {
      font-size: 11px; font-weight: 700; letter-spacing: 0.05em; text-transform: uppercase;
      padding: 3px 8px; border-radius: 4px; color: var(--accent-dk);
    }
    .pill-cls  { background: #f0e6d8; border: 1px solid #d4b08a; }
    .pill-pos  { background: #fff3e0; border: 1px solid #f5c97a; }

    /* ── MODAL ── */
    .modal-bg {
      display: none; position: fixed; inset: 0;
      background: rgba(30,15,5,.6); z-index: 9000;
      align-items: center; justify-content: center; padding: 20px; overflow-y: auto;
    }
    .modal-bg.open { display: flex; }
    .modal {
      background: var(--card); border-radius: 14px; border: 1.5px solid var(--border);
      padding: 28px 24px; width: 100%; max-width: 420px; position: relative;
      box-shadow: 0 8px 32px rgba(30,15,5,.25); max-height: 90vh; overflow-y: auto;
    }
    .modal-close {
      position: absolute; top: 14px; right: 16px; background: transparent;
      border: none; font-size: 18px; cursor: pointer; color: var(--muted); font-weight: 700;
    }
    .modal-photo { width: 80px; height: 80px; border-radius: 10px; object-fit: cover;
      border: 2px solid var(--border); flex-shrink: 0; }
    .modal-top { display: flex; gap: 16px; align-items: flex-start; margin-bottom: 20px; }
    .modal-name { font-weight: 800; font-size: 20px; color: var(--accent-dk); margin-bottom: 8px; }
    .info-row { display: flex; gap: 8px; margin-bottom: 10px; align-items: flex-start; }
    .info-label { font-size: 10px; font-weight: 700; color: var(--muted);
      text-transform: uppercase; letter-spacing: 0.06em; }
    .info-value { font-size: 13px; color: var(--text); font-weight: 500; }
    .info-value a { color: var(--accent); font-weight: 600; }

    /* ── FOOTER ── */
    .footer { max-width: 620px; margin: 28px auto 0; padding: 20px 16px 40px; text-align: center; }
    .footer p { font-size: 12px; color: var(--muted); line-height: 1.6; margin-bottom: 4px; }
    .footer strong { font-size: 12px; color: var(--accent-dk); letter-spacing: 0.04em; }

    /* ── EMPTY STATE ── */
    .empty { text-align: center; padding: 48px 0; color: var(--muted); font-size: 14px; }

    /* ── LOADING ── */
    .loading { text-align: center; padding: 48px 0; color: var(--muted); font-size: 14px; }
    .spinner {
      display: inline-block; width: 24px; height: 24px;
      border: 3px solid var(--border); border-top-color: var(--accent);
      border-radius: 50%; animation: spin 0.7s linear infinite; margin-bottom: 10px;
    }
    @keyframes spin { to { transform: rotate(360deg); } }

    button { -webkit-tap-highlight-color: transparent; }
  </style>
</head>
<body>

<!-- HEADER -->
<div class="header">
  <div class="header-eyebrow">Player Registration</div>
  <h1>Aethers Futsal<br>Tournament</h1>
</div>

<!-- TABS -->
<div class="tabs">
  <button class="tab-btn active" id="tab-register" onclick="switchTab('register')">Register</button>
  <button class="tab-btn"        id="tab-admin"    onclick="switchTab('admin')">Host View</button>
</div>

<!-- HIDDEN FILE INPUTS -->
<input type="file" id="camera-input"  accept="image/*" capture="user" style="display:none">
<input type="file" id="gallery-input" accept="image/*"                style="display:none">

<!-- PANELS -->
<div class="panel">

  <!-- ── REGISTER PANEL ── -->
  <div id="panel-register">

    <!-- Removed notice -->
    <div id="removed-notice" class="success-card removed" style="display:none">
      <h2>Registration Removed</h2>
      <p>The host has removed your registration. Contact the organiser if this was a mistake, or submit again below.</p>
      <button class="btn-primary" onclick="showForm()">Submit Again</button>
    </div>

    <!-- Registered notice -->
    <div id="registered-notice" class="success-card" style="display:none">
      <h2>You're Registered</h2>
      <p>Your registration is submitted. The coaching staff will review your details and contact you if selected.</p>
      <div id="timer-badge" class="timer-badge"></div>
      <div id="timer-sub"   class="timer-sub"></div>
      <button id="withdraw-btn" class="btn-danger" onclick="withdraw()" style="display:none">
        Withdraw My Registration
      </button>
    </div>

    <!-- Registration form -->
    <div id="reg-form" class="card">

      <div class="field">
        <label>Full Name <span class="req">*</span></label>
        <input type="text" id="f-name" placeholder="Your full name" autocomplete="name">
        <div class="err-msg" id="err-name" style="display:none"></div>
      </div>

      <div class="field">
        <label>Class <span class="req">*</span></label>
        <select id="f-cls">
          <option value="">Select your class</option>
          <option value="6">Class 6</option>
          <option value="7">Class 7</option>
          <option value="8">Class 8</option>
        </select>
        <div class="err-msg" id="err-cls" style="display:none"></div>
      </div>

      <div class="field">
        <label>Position <span class="req">*</span></label>
        <select id="f-pos">
          <option value="">Select your position</option>
          <option>Attacker</option>
          <option>Midfielder</option>
          <option>Defender</option>
          <option>Goalkeeper</option>
        </select>
        <div class="err-msg" id="err-pos" style="display:none"></div>
      </div>

      <div class="field">
        <label>WhatsApp Number <span class="req">*</span></label>
        <input type="tel" id="f-wa" placeholder="+880 1712 345678" autocomplete="tel">
        <div class="err-msg" id="err-wa" style="display:none"></div>
      </div>

      <div class="field">
        <label>Instagram <span class="opt">(optional)</span></label>
        <input type="text" id="f-ig" placeholder="@yourhandle" autocomplete="off">
      </div>

      <div class="field">
        <label>Your Photo <span class="req">*</span></label>
        <div id="upload-zone" class="upload-zone">
          <div class="uz-title">Upload your photo</div>
          <div class="uz-sub">JPG or PNG — selfie or portrait</div>
          <div class="upload-btns">
            <button type="button" class="btn-take"   onclick="document.getElementById('camera-input').click()">Take Photo</button>
            <button type="button" class="btn-choose" onclick="document.getElementById('gallery-input').click()">Choose from Library</button>
          </div>
        </div>
        <div id="photo-preview" class="preview-row" style="display:none">
          <img id="preview-img" src="" alt="preview">
          <div class="preview-info">
            <div class="p-name" id="preview-name"></div>
            <div class="p-size" id="preview-size"></div>
            <div class="p-links">
              <a onclick="document.getElementById('camera-input').click()">Retake</a>
              <a onclick="document.getElementById('gallery-input').click()">Change</a>
            </div>
          </div>
        </div>
        <div class="err-msg" id="err-photo" style="display:none"></div>
      </div>

      <button class="btn-primary" id="submit-btn" onclick="submitForm()">Submit Registration</button>
    </div>
  </div>

  <!-- ── ADMIN PANEL ── -->
  <div id="panel-admin" style="display:none">

    <!-- Login -->
    <div id="admin-login" style="max-width:360px; margin:0 auto;">
      <div class="card">
        <h2 style="font-weight:800;font-size:20px;color:var(--accent-dk);margin-bottom:20px;text-align:center;">Host Access</h2>
        <div class="field">
          <label>Password <span class="req">*</span></label>
          <input type="password" id="admin-pass" placeholder="Enter access code"
            onkeydown="if(event.key==='Enter')adminLogin()">
          <div class="err-msg" id="err-admin" style="display:none">Incorrect password</div>
        </div>
        <button class="btn-primary" style="margin-top:8px" onclick="adminLogin()">View Submissions</button>
      </div>
    </div>

    <!-- Dashboard -->
    <div id="admin-dashboard" style="display:none">
      <div class="admin-header">
        <h2>All Registrations</h2>
        <div class="right">
          <span class="count-badge" id="total-count"></span>
          <button class="btn-outline" onclick="adminLogout()">Log Out</button>
        </div>
      </div>
      <div id="players-list"></div>
    </div>
  </div>

</div><!-- /panel -->

<!-- FOOTER -->
<div class="footer">
  <p>Your information is kept private. If selected, you will be contacted directly.</p>
  <strong>Organized by Team Aethers</strong>
</div>

<!-- PLAYER MODAL -->
<div class="modal-bg" id="player-modal" onclick="closeModal()">
  <div class="modal" onclick="event.stopPropagation()">
    <button class="modal-close" onclick="closeModal()">×</button>
    <div class="modal-top">
      <img class="modal-photo" id="modal-photo" src="" alt="">
      <div>
        <div class="modal-name" id="modal-name"></div>
        <div class="pills" id="modal-pills"></div>
      </div>
    </div>
    <div id="modal-body"></div>
  </div>
</div>

<script>
// ── SUPABASE CONFIG ──
const SUPABASE_URL  = "https://tkumgwhytoqokjiwwfvs.supabase.co";
const SUPABASE_ANON = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InRrdW1nd2h5dG9xb2tqaXd3ZnZzIiwicm9sZSI6ImFub24iLCJpYXQiOjE3ODEzNjQxMTEsImV4cCI6MjA5Njk0MDExMX0.W3Diqlsu408NQ7nhBQ971KE0VARFlFcJa9MBMT4P9aY";
const DB_TABLE      = "submissions";
const BUCKET        = "player-photos";

// ── LOCAL STATE (just for this device's own registration) ──
const MY_KEY      = "aethers_my_v1";
const REMOVED_KEY = "aethers_removed_v1";
const ADMIN_PASS  = "19805";
const POSITIONS   = ["Attacker","Midfielder","Defender","Goalkeeper"];

function getMy()         { try { return JSON.parse(localStorage.getItem(MY_KEY)); } catch { return null; } }
function saveMy(s)       { localStorage.setItem(MY_KEY, JSON.stringify(s)); }
function clearMy()       { localStorage.removeItem(MY_KEY); }
function getRemovedIds() { try { return JSON.parse(localStorage.getItem(REMOVED_KEY)) || []; } catch { return []; } }
function addRemovedId(id){ const ids = getRemovedIds(); if(!ids.includes(id)){ ids.push(id); localStorage.setItem(REMOVED_KEY, JSON.stringify(ids)); } }
function fmtSize(b)      { return b<1048576 ? (b/1024).toFixed(0)+" KB" : (b/1048576).toFixed(1)+" MB"; }

// ── SUPABASE HELPERS ──
async function sbFetch(path, opts = {}) {
  const url = `${SUPABASE_URL}/rest/v1/${path}`;
  const res = await fetch(url, {
    ...opts,
    headers: {
      "apikey": SUPABASE_ANON,
      "Authorization": `Bearer ${SUPABASE_ANON}`,
      "Content-Type": "application/json",
      "Prefer": "return=representation",
      ...(opts.headers || {})
    }
  });
  if (!res.ok) {
    const err = await res.text();
    throw new Error(`Supabase error ${res.status}: ${err}`);
  }
  const text = await res.text();
  return text ? JSON.parse(text) : null;
}

async function uploadPhoto(base64DataUrl, filename) {
  // Convert base64 data URL to blob
  const [meta, b64] = base64DataUrl.split(",");
  const mime = meta.match(/:(.*?);/)[1];
  const binary = atob(b64);
  const bytes = new Uint8Array(binary.length);
  for (let i = 0; i < binary.length; i++) bytes[i] = binary.charCodeAt(i);
  const blob = new Blob([bytes], { type: mime });

  const path = `${Date.now()}_${filename}`;
  const url = `${SUPABASE_URL}/storage/v1/object/${BUCKET}/${path}`;
  const res = await fetch(url, {
    method: "POST",
    headers: {
      "apikey": SUPABASE_ANON,
      "Authorization": `Bearer ${SUPABASE_ANON}`,
      "Content-Type": mime,
    },
    body: blob
  });
  if (!res.ok) {
    const err = await res.text();
    throw new Error(`Photo upload failed: ${err}`);
  }
  // Return public URL
  return `${SUPABASE_URL}/storage/v1/object/public/${BUCKET}/${path}`;
}

async function getAllSubs() {
  return await sbFetch(`${DB_TABLE}?order=submitted_to.desc&select=*&removed=neq.true`) || [];
}

async function insertSub(sub) {
  const result = await sbFetch(DB_TABLE, {
    method: "POST",
    body: JSON.stringify(sub)
  });
  return Array.isArray(result) ? result[0] : result;
}

async function markRemoved(playerId) {
  await sbFetch(`${DB_TABLE}?player_id=eq.${encodeURIComponent(playerId)}`, {
    method: "PATCH",
    body: JSON.stringify({ removed: true })
  });
}

async function deleteSub(playerId) {
  // We use the removed flag so the player gets notified, not a hard delete
  await markRemoved(playerId);
}

// ── IMAGE RESIZE ──
function resizeImage(file, maxW=800) {
  return new Promise((res, rej) => {
    const img = new Image();
    const url = URL.createObjectURL(file);
    img.onload = () => {
      URL.revokeObjectURL(url);
      const scale = Math.min(1, maxW / img.width);
      const canvas = document.createElement("canvas");
      canvas.width  = Math.round(img.width  * scale);
      canvas.height = Math.round(img.height * scale);
      canvas.getContext("2d").drawImage(img, 0, 0, canvas.width, canvas.height);
      canvas.toBlob(blob => {
        if (!blob) { rej(new Error("toBlob failed")); return; }
        const out = new File([blob], file.name.replace(/\.\w+$/,".jpg"), { type:"image/jpeg" });
        const reader = new FileReader();
        reader.onload = ev => res({ src: ev.target.result, name: out.name, size: out.size });
        reader.onerror = rej;
        reader.readAsDataURL(out);
      }, "image/jpeg", 0.82);
    };
    img.onerror = rej;
    img.src = url;
  });
}

// ── STATE ──
let photoData = null;
let timerInterval = null;

// ── INIT ──
window.addEventListener("DOMContentLoaded", async () => {
  document.getElementById("camera-input").addEventListener("change", e => handleFileSelect(e.target.files[0]));
  document.getElementById("gallery-input").addEventListener("change", e => handleFileSelect(e.target.files[0]));

  const my = getMy();
  if (my) {
    // Check if this registration still exists in Supabase
    try {
      const rows = await sbFetch(`${DB_TABLE}?player_id=eq.${encodeURIComponent(my.player_id)}&select=player_id,removed`);
      if (!rows || rows.length === 0 || rows[0].removed === true) {
        // Removed by host
        clearMy();
        addRemovedId(my.player_id);
        showRemoved();
      } else {
        showRegistered(my);
      }
    } catch {
      // Network error — show registered optimistically
      showRegistered(my);
    }
  }
});

async function handleFileSelect(file) {
  if (!file) return;
  try {
    photoData = await resizeImage(file);
  } catch {
    const reader = new FileReader();
    reader.onload = e => { photoData = { src: e.target.result, name: file.name, size: file.size }; };
    reader.readAsDataURL(file);
    return;
  }
  document.getElementById("upload-zone").style.display = "none";
  const prev = document.getElementById("photo-preview");
  prev.style.display = "flex";
  document.getElementById("preview-img").src  = photoData.src;
  document.getElementById("preview-name").textContent = photoData.name;
  document.getElementById("preview-size").textContent = fmtSize(photoData.size);
  clearErr("photo");
  document.getElementById("camera-input").value  = "";
  document.getElementById("gallery-input").value = "";
}

// ── TAB SWITCH ──
function switchTab(tab) {
  document.getElementById("panel-register").style.display = tab==="register" ? "" : "none";
  document.getElementById("panel-admin").style.display    = tab==="admin"    ? "" : "none";
  document.getElementById("tab-register").classList.toggle("active", tab==="register");
  document.getElementById("tab-admin").classList.toggle("active",    tab==="admin");
}

// ── FORM VIEWS ──
function showForm()     {
  document.getElementById("reg-form").style.display="";
  document.getElementById("removed-notice").style.display="none";
  document.getElementById("registered-notice").style.display="none";
}
function showRemoved()  {
  document.getElementById("reg-form").style.display="none";
  document.getElementById("removed-notice").style.display="";
  document.getElementById("registered-notice").style.display="none";
}
function showRegistered(sub) {
  document.getElementById("reg-form").style.display="none";
  document.getElementById("removed-notice").style.display="none";
  document.getElementById("registered-notice").style.display="";
  startTimer(sub.submittedAt || new Date(sub.submitted_to).getTime());
}

// ── COUNTDOWN ──
function startTimer(submittedAt) {
  if (timerInterval) clearInterval(timerInterval);
  const deadline = submittedAt + 24*3600*1000;
  const badge = document.getElementById("timer-badge");
  const sub   = document.getElementById("timer-sub");
  const wbtn  = document.getElementById("withdraw-btn");
  function tick() {
    const left = deadline - Date.now();
    if (left <= 0) {
      badge.textContent = "Withdrawal period ended";
      sub.textContent   = "";
      wbtn.style.display = "none";
      clearInterval(timerInterval);
      return;
    }
    const h = Math.floor(left/3600000);
    const m = Math.floor((left%3600000)/60000);
    const s = Math.floor((left%60000)/1000);
    badge.textContent = `Withdraw within ${h}h ${m}m`;
    sub.textContent   = `Time left: ${h}h ${m}m ${s}s`;
    wbtn.style.display = "";
  }
  tick();
  timerInterval = setInterval(tick, 1000);
}

// ── VALIDATION ──
function setErr(id, msg) {
  const el=document.getElementById("err-"+id);
  el.textContent=msg; el.style.display="";
  const inp=document.getElementById("f-"+id);
  if(inp) inp.classList.add("has-err");
}
function clearErr(id) {
  const el=document.getElementById("err-"+id);
  if(el) el.style.display="none";
  const inp=document.getElementById("f-"+id);
  if(inp) inp.classList.remove("has-err");
}

function validate() {
  let ok = true;
  ["name","cls","pos","wa","photo"].forEach(k => clearErr(k));
  const name = document.getElementById("f-name").value.trim();
  const cls  = document.getElementById("f-cls").value;
  const pos  = document.getElementById("f-pos").value;
  const wa   = document.getElementById("f-wa").value.trim();
  if (!name)    { setErr("name","Enter your full name");      ok=false; }
  if (!cls)     { setErr("cls","Select your class");          ok=false; }
  if (!pos)     { setErr("pos","Select your position");       ok=false; }
  if (!wa)      { setErr("wa","Enter your WhatsApp number");  ok=false; }
  if (!photoData){ setErr("photo","Upload your photo");       ok=false; }
  return ok;
}

// ── SUBMIT ──
async function submitForm() {
  if (!validate()) return;
  const btn = document.getElementById("submit-btn");
  btn.disabled = true;
  btn.textContent = "Uploading photo…";

  try {
    // 1. Upload photo to Supabase Storage
    let photoUrl;
    try {
      photoUrl = await uploadPhoto(photoData.src, photoData.name);
    } catch (uploadErr) {
      // If storage bucket isn't set up, fall back to storing base64 directly
      console.warn("Storage upload failed, storing base64:", uploadErr.message);
      photoUrl = photoData.src;
    }

    btn.textContent = "Saving registration…";

    // 2. Insert row into Supabase
    const now = Date.now();
    const playerId = crypto.randomUUID();
    const sub = {
      player_id:    playerId,
      name:         document.getElementById("f-name").value.trim(),
      cls:          document.getElementById("f-cls").value,
      position:     document.getElementById("f-pos").value,
      whatsapp:     document.getElementById("f-wa").value.trim(),
      instagram:    document.getElementById("f-ig").value.trim() || null,
      photo:        photoUrl,
      removed:      false,
      submitted_to: new Date(now).toISOString(),
    };

    const inserted = await insertSub(sub);
    const localSub = { ...inserted, submittedAt: now };
    saveMy(localSub);
    showRegistered(localSub);

  } catch(e) {
    alert("Something went wrong: " + e.message + "\n\nCheck your Supabase table and RLS settings.");
  }

  btn.disabled = false;
  btn.textContent = "Submit Registration";
}

// ── WITHDRAW ──
async function withdraw() {
  if (!confirm("Withdraw your registration? You can re-submit anytime.")) return;
  const my = getMy();
  if (my) {
    try {
      await deleteSub(my.player_id);
    } catch(e) {
      alert("Could not withdraw: " + e.message);
      return;
    }
    clearMy();
  }
  if (timerInterval) clearInterval(timerInterval);
  photoData = null;
  document.getElementById("f-name").value="";
  document.getElementById("f-cls").value="";
  document.getElementById("f-pos").value="";
  document.getElementById("f-wa").value="";
  document.getElementById("f-ig").value="";
  document.getElementById("upload-zone").style.display="";
  document.getElementById("photo-preview").style.display="none";
  showForm();
}

// ── ADMIN ──
function adminLogin() {
  const pass = document.getElementById("admin-pass").value;
  if (pass === ADMIN_PASS) {
    document.getElementById("err-admin").style.display="none";
    document.getElementById("admin-login").style.display="none";
    document.getElementById("admin-dashboard").style.display="";
    renderPlayers();
  } else {
    document.getElementById("err-admin").style.display="";
    document.getElementById("admin-pass").classList.add("has-err");
  }
}

function adminLogout() {
  document.getElementById("admin-login").style.display="";
  document.getElementById("admin-dashboard").style.display="none";
  document.getElementById("admin-pass").value="";
  document.getElementById("err-admin").style.display="none";
  document.getElementById("admin-pass").classList.remove("has-err");
}

async function renderPlayers() {
  const list = document.getElementById("players-list");
  list.innerHTML = '<div class="loading"><div class="spinner"></div><br>Loading registrations…</div>';

  let subs;
  try {
    subs = await getAllSubs();
  } catch(e) {
    list.innerHTML = `<div class="empty">Failed to load: ${e.message}</div>`;
    return;
  }

  document.getElementById("total-count").textContent = subs.length+" player"+(subs.length!==1?"s":"");
  list.innerHTML="";

  if (!subs.length) {
    list.innerHTML='<div class="empty">No registrations yet.</div>';
    return;
  }

  POSITIONS.forEach(pos => {
    const group = subs.filter(s => s.position===pos);
    if (!group.length) return;
    const sec = document.createElement("div"); sec.className="pos-section";
    sec.innerHTML=`<div class="pos-header"><span>${pos}s</span><span class="pos-count">${group.length}</span></div>`;
    group.forEach(sub => {
      const card = document.createElement("div"); card.className="player-card";
      const dateStr = new Date(sub.submitted_to || sub.submittedAt).toLocaleDateString();
      const safeId = String(sub.player_id).replace(/'/g, "");
      card.innerHTML=`
        <img src="${sub.photo}" alt="${sub.name}" onerror="this.src='data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 width=%2252%22 height=%2252%22><rect width=%2252%22 height=%2252%22 fill=%22%23e2cdb8%22/></svg>'">
        <div class="info">
          <div class="pname">${sub.name}</div>
          <div class="pills">
            <span class="pill pill-cls">Class ${sub.cls}</span>
            <span class="pill pill-pos">${sub.position}</span>
          </div>
          <div class="pdate">${dateStr}</div>
        </div>
        <div class="actions">
          <button class="btn-card-view"   onclick="openModal('${safeId}', allSubs)">View</button>
          <button class="btn-card-remove" onclick="removePlayer('${safeId}')">Remove</button>
        </div>`;
      sec.appendChild(card);
    });
    list.appendChild(sec);
  });

  // Store for modal lookups
  window.allSubs = subs;
}

async function removePlayer(id) {
  const subs = window.allSubs || [];
  const sub = subs.find(s => String(s.player_id) === String(id));
  if (!sub) return;
  if (!confirm(`Remove ${sub.name}'s registration? They will be notified next time they visit.`)) return;
  try {
    await markRemoved(id);
    addRemovedId(String(id));
    closeModal();
    renderPlayers();
  } catch(e) {
    alert("Could not remove: " + e.message);
  }
}

// ── MODAL ──
function openModal(id, subs) {
  const sub = (subs || window.allSubs || []).find(s => String(s.player_id) === String(id));
  if (!sub) return;
  document.getElementById("modal-photo").src = sub.photo;
  document.getElementById("modal-name").textContent = sub.name;
  document.getElementById("modal-pills").innerHTML =
    `<span class="pill pill-cls">Class ${sub.cls}</span><span class="pill pill-pos">${sub.position}</span>`;
  const dateStr = new Date(sub.submitted_to || sub.submittedAt).toLocaleString();
  document.getElementById("modal-body").innerHTML=`
    <div class="info-row"><div><div class="info-label">Submitted</div><div class="info-value">${dateStr}</div></div></div>
    <div class="info-row"><div><div class="info-label">WhatsApp</div><div class="info-value"><a href="https://wa.me/${(sub.whatsapp||"").replace(/[^0-9]/g,"")}" target="_blank">${sub.whatsapp}</a></div></div></div>
    ${sub.instagram ? `<div class="info-row"><div><div class="info-label">Instagram</div><div class="info-value">${sub.instagram}</div></div></div>` : ""}
  `;
  document.getElementById("player-modal").classList.add("open");
}

function closeModal() {
  document.getElementById("player-modal").classList.remove("open");
}
</script>
</body>
</html>
