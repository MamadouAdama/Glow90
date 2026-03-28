<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<title>Glow Up 90 Jours</title>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }
  body { background: #080808; color: #e0d8cc; font-family: Georgia, serif; min-height: 100vh; padding-bottom: 60px; }
  button { font-family: Georgia, serif; cursor: pointer; }
  .header { background: #0d0d0d; border-bottom: 1px solid #1a1a1a; padding: 24px 20px 0; text-align: center; position: sticky; top: 0; z-index: 10; }
  .eyebrow { font-size: 10px; letter-spacing: 6px; color: #c8a84b; text-transform: uppercase; margin-bottom: 5px; }
  .title { font-size: 21px; font-weight: normal; color: #f0e8d8; text-transform: capitalize; margin-bottom: 2px; }
  .scores { display: flex; justify-content: center; gap: 28px; margin: 16px 0 0; }
  .score-label { font-size: 9px; color: #555; letter-spacing: 2px; text-transform: uppercase; margin-top: 2px; }
  .tabs { display: flex; margin-top: 18px; }
  .tab { flex: 1; padding: 12px; background: transparent; border: none; border-bottom: 2px solid transparent; color: #555; font-size: 12px; letter-spacing: 2px; }
  .tab.active { border-bottom-color: #c8a84b; color: #c8a84b; }
  .subtabs { display: flex; border-bottom: 1px solid #1a1a1a; }
  .subtab { flex: 1; padding: 11px; background: transparent; border: none; border-bottom: 2px solid transparent; color: #555; font-size: 11px; letter-spacing: 3px; text-transform: uppercase; }
  .subtab.active { border-bottom-color: #c8a84b; color: #c8a84b; }
  .content { max-width: 480px; margin: 0 auto; padding: 18px 16px; }
  .task-row { display: flex; align-items: center; gap: 12px; padding: 13px 15px; margin-bottom: 7px; border-radius: 10px; cursor: pointer; transition: all 0.2s; }
  .task-row.done { background: #0f1a0f; border: 1px solid #1e3a1e; opacity: 0.72; }
  .task-row.undone { background: #111; border: 1px solid #1a1a1a; }
  .task-time { font-size: 11px; color: #555; min-width: 38px; font-variant-numeric: tabular-nums; }
  .task-icon { font-size: 18px; }
  .task-text { flex: 1; font-size: 13px; }
  .task-text.done { color: #6a8a6a; text-decoration: line-through; }
  .task-text.undone { color: #c0b8a8; }
  .check { width: 20px; height: 20px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 11px; color: #fff; flex-shrink: 0; transition: all 0.2s; }
  .check.done { border: 2px solid #4a8a4a; background: #4a8a4a; }
  .check.undone { border: 2px solid #2a2a2a; background: transparent; }
  .goal-row { display: flex; align-items: center; gap: 16px; padding: 18px 20px; margin-bottom: 10px; border-radius: 14px; cursor: pointer; transition: all 0.25s; }
  .goal-row.done { background: #111a11; border: 1px solid #2a4a2a; }
  .goal-row.undone { background: #111; border: 1px solid #1a1a1a; }
  .goal-icon { font-size: 24px; }
  .goal-label { flex: 1; font-size: 14px; }
  .goal-label.done { color: #80b080; }
  .goal-label.undone { color: #998; }
  .goal-check { width: 26px; height: 26px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 13px; color: #000; transition: all 0.2s; }
  .goal-check.done { border: 2px solid #c8a84b; background: #c8a84b; }
  .goal-check.undone { border: 2px solid #2a2a2a; background: transparent; }
  .perfect { text-align: center; margin-top: 20px; color: #c8a84b; font-size: 12px; letter-spacing: 4px; }
  .week-picker { display: flex; gap: 5px; flex-wrap: wrap; justify-content: center; margin-bottom: 20px; }
  .week-btn { padding: 5px 9px; border-radius: 6px; background: transparent; border: 1px solid #1e1e1e; color: #555; font-size: 10px; }
  .week-btn.active { background: #1a1a1a; }
  .week-info { text-align: center; margin-bottom: 20px; }
  .week-title { font-size: 15px; color: #c8a84b; }
  .week-sub { font-size: 11px; color: #555; margin-top: 3px; }
  .week-score { font-size: 11px; color: #666; margin-top: 6px; }
  .goal-grid-row { margin-bottom: 14px; }
  .goal-grid-header { display: flex; align-items: center; gap: 10px; margin-bottom: 7px; }
  .goal-grid-label { font-size: 13px; color: #a09080; flex: 1; }
  .goal-grid-count { font-size: 11px; color: #555; }
  .day-grid { display: grid; grid-template-columns: repeat(7, 1fr); gap: 5px; }
  .day-cell { aspect-ratio: 1; border-radius: 6px; cursor: pointer; display: flex; flex-direction: column; align-items: center; justify-content: center; transition: all 0.15s; }
  .day-cell.checked { background: #c8a84b; border: 1px solid #c8a84b; }
  .day-cell.unchecked { background: #151515; border: 1px solid #222; }
  .day-letter { font-size: 8px; margin-bottom: 1px; }
  .day-letter.checked { color: #5a3a00; }
  .day-letter.unchecked { color: #444; }
  .day-tick { font-size: 10px; color: #5a3a00; }
  .overview-row { cursor: pointer; margin-bottom: 14px; }
  .overview-header { display: flex; justify-content: space-between; font-size: 11px; margin-bottom: 4px; }
  .overview-bar-bg { height: 7px; background: #151515; border-radius: 4px; overflow: hidden; }
  .overview-bar { height: 100%; border-radius: 4px; transition: width 0.5s ease; }
  .mini-dots { display: flex; gap: 3px; margin-top: 4px; }
  .mini-dot { flex: 1; height: 4px; border-radius: 2px; }
  .legend { display: flex; justify-content: center; gap: 16px; margin-top: 24px; }
  .legend-item { display: flex; align-items: center; gap: 5px; font-size: 10px; color: #555; }
  .legend-dot { width: 10px; height: 10px; border-radius: 2px; }
  .hint { font-size: 10px; color: #444; text-align: center; margin-top: 12px; letter-spacing: 2px; }
</style>
</head>
<body>

<div class="header">
  <div class="eyebrow">Glow Up · 90 Jours</div>
  <h1 class="title" id="dateStr"></h1>
  <div class="scores">
    <div>
      <svg width="54" height="54" id="svg-reussites"></svg>
      <div class="score-label">Réussites</div>
    </div>
    <div>
      <svg width="54" height="54" id="svg-taches"></svg>
      <div class="score-label">Tâches</div>
    </div>
    <div>
      <svg width="54" height="54" id="svg-global"></svg>
      <div class="score-label">90j global</div>
    </div>
  </div>
  <div class="tabs">
    <button class="tab active" id="tab-daily" onclick="switchView('daily')">📅 Journalier</button>
    <button class="tab" id="tab-weekly" onclick="switchView('weekly')">📊 Hebdo 12S</button>
  </div>
</div>

<div id="view-daily">
  <div class="subtabs">
    <button class="subtab active" id="subtab-planning" onclick="switchSubTab('planning')">Planning</button>
    <button class="subtab" id="subtab-reussites" onclick="switchSubTab('reussites')">Réussites</button>
  </div>
  <div class="content" id="planning-content"></div>
  <div class="content" id="reussites-content" style="display:none"></div>
</div>

<div id="view-weekly" style="display:none">
  <div class="subtabs">
    <button class="subtab active" id="subtab-semaine" onclick="switchWeekSubTab('semaine')">Semaine</button>
    <button class="subtab" id="subtab-overview" onclick="switchWeekSubTab('overview')">12 Semaines</button>
  </div>
  <div class="content" id="semaine-content"></div>
  <div class="content" id="overview-content" style="display:none"></div>
</div>

<script>
// ── Constants ──────────────────────────────────────────────────────────────────
const START_DATE = new Date(2026, 2, 28); // March 28, 2026
const STORAGE_KEY = "glow90_html_v1";

const GOALS = [
  { id: "salat", icon: "🕌", label: "Toutes mes prières" },
  { id: "mlm",   icon: "💼", label: "2h MLM accompli" },
  { id: "hawza", icon: "📖", label: "Hawza 100%" },
  { id: "sport", icon: "💪", label: "Séance de sport" },
  { id: "sleep", icon: "🌙", label: "Couché avant 22h45" },
];

const SCHEDULE = [
  { time: "05:30", icon: "💧", task: "Réveil — eau + Fajr + silence",         goalId: null },
  { time: "06:00", icon: "📖", task: "Révision Hawza + préparation",           goalId: "hawza" },
  { time: "07:00", icon: "🕌", task: "Hawza (cours)",                          goalId: "hawza" },
  { time: "12:15", icon: "🕌", task: "Zuhoor + Asr",                           goalId: "salat" },
  { time: "12:45", icon: "🍽️", task: "Déjeuner — téléphone posé",              goalId: null },
  { time: "13:30", icon: "🎧", task: "Podcast (écouter, pas parler)",          goalId: null },
  { time: "14:30", icon: "📖", task: "Révision matières Hawza",                goalId: "hawza" },
  { time: "16:30", icon: "😴", task: "Repos / Sieste courte",                  goalId: null },
  { time: "17:30", icon: "🧘", task: "Préparation mentale — mode calme",       goalId: null },
  { time: "18:15", icon: "🕌", task: "Maghreb + Icha",                         goalId: "salat" },
  { time: "19:00", icon: "💪", task: "Salle de sport",                         goalId: "sport" },
  { time: "20:30", icon: "🚿", task: "Douche + dîner léger",                   goalId: null },
  { time: "21:00", icon: "💼", task: "DEEP WORK — 2h MLM",                     goalId: "mlm" },
  { time: "22:45", icon: "🌙", task: "Bilan + EXTINCTION téléphone",           goalId: "sleep" },
];

const DAYS_SHORT = ["S","D","L","M","M","J","V"];

// ── State ──────────────────────────────────────────────────────────────────────
let data = { daily: {}, weekly: {} };
let currentView = "daily";
let currentSubTab = "planning";
let currentWeekSubTab = "semaine";
let activeWeek = 1;

// ── Storage ────────────────────────────────────────────────────────────────────
function loadData() {
  try {
    const saved = localStorage.getItem(STORAGE_KEY);
    if (saved) data = JSON.parse(saved);
  } catch(e) {}
}

function saveData() {
  try {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(data));
  } catch(e) {}
}

// ── Helpers ────────────────────────────────────────────────────────────────────
function getTodayKey() {
  const d = new Date();
  return `${d.getFullYear()}_${d.getMonth()}_${d.getDate()}`;
}

function getWeekAndDay(date) {
  const d = new Date(date || new Date());
  d.setHours(0,0,0,0);
  const s = new Date(START_DATE); s.setHours(0,0,0,0);
  const diff = Math.floor((d - s) / 86400000);
  if (diff < 0 || diff >= 84) return null;
  return { week: Math.floor(diff / 7) + 1, day: diff % 7 };
}

function wKey(week, day, goalId) { return `w${week}_d${day}_${goalId}`; }

function getWeekLabel(w) {
  const s = new Date(START_DATE);
  s.setDate(s.getDate() + (w - 1) * 7);
  const e = new Date(s); e.setDate(e.getDate() + 6);
  const f = d => d.toLocaleDateString("fr-FR", { day: "numeric", month: "short" });
  return `${f(s)} – ${f(e)}`;
}

function barColor(pct) {
  if (pct >= 85) return "#c8a84b";
  if (pct >= 60) return "#7eb87e";
  if (pct >= 30) return "#c4874a";
  return "#2a2a2a";
}

function weeklyScore(w) {
  let n = 0;
  for (let d = 0; d < 7; d++)
    GOALS.forEach(g => { if (data.weekly[wKey(w,d,g.id)]) n++; });
  return n;
}

function weeklyPct(w) { return Math.round(weeklyScore(w) / 35 * 100); }

function drawCircle(svgId, val, max, color, isPercent) {
  const svg = document.getElementById(svgId);
  if (!svg) return;
  const pct = isPercent ? val : Math.round(val / max * 100);
  const r = 22, circ = 2 * Math.PI * r;
  const offset = circ - (circ * pct / 100);
  const label = isPercent ? `${val}%` : `${val}/${max}`;
  svg.innerHTML = `
    <circle cx="27" cy="27" r="${r}" fill="none" stroke="#1e1e1e" stroke-width="3"/>
    <circle cx="27" cy="27" r="${r}" fill="none" stroke="${color}" stroke-width="3"
      stroke-dasharray="${circ}" stroke-dashoffset="${offset}"
      stroke-linecap="round" transform="rotate(-90 27 27)"
      style="transition:stroke-dashoffset 0.6s ease"/>
    <text x="27" y="31" text-anchor="middle" fill="${color}" font-size="11" font-family="Georgia">${label}</text>
  `;
}

// ── Toggle logic ───────────────────────────────────────────────────────────────
function toggleTask(idx) {
  const todayKey = getTodayKey();
  if (!data.daily[todayKey]) data.daily[todayKey] = { tasks: {}, goals: {} };
  const cur = data.daily[todayKey];
  const wasOn = !!cur.tasks[idx];
  cur.tasks[idx] = !wasOn;

  const item = SCHEDULE[idx];
  if (item.goalId && !wasOn) {
    cur.goals[item.goalId] = true;
    const wd = getWeekAndDay();
    if (wd) data.weekly[wKey(wd.week, wd.day, item.goalId)] = true;
  }
  saveData();
  render();
}

function toggleGoal(goalId) {
  const todayKey = getTodayKey();
  if (!data.daily[todayKey]) data.daily[todayKey] = { tasks: {}, goals: {} };
  const cur = data.daily[todayKey];
  const wasOn = !!cur.goals[goalId];
  cur.goals[goalId] = !wasOn;
  const wd = getWeekAndDay();
  if (wd) data.weekly[wKey(wd.week, wd.day, goalId)] = !wasOn;
  saveData();
  render();
}

function toggleWeeklyCell(week, day, goalId) {
  const key = wKey(week, day, goalId);
  data.weekly[key] = !data.weekly[key];
  saveData();
  render();
}

// ── View switching ─────────────────────────────────────────────────────────────
function switchView(v) {
  currentView = v;
  document.getElementById("view-daily").style.display = v === "daily" ? "block" : "none";
  document.getElementById("view-weekly").style.display = v === "weekly" ? "block" : "none";
  document.getElementById("tab-daily").className = "tab" + (v === "daily" ? " active" : "");
  document.getElementById("tab-weekly").className = "tab" + (v === "weekly" ? " active" : "");
  render();
}

function switchSubTab(t) {
  currentSubTab = t;
  document.getElementById("planning-content").style.display = t === "planning" ? "block" : "none";
  document.getElementById("reussites-content").style.display = t === "reussites" ? "block" : "none";
  document.getElementById("subtab-planning").className = "subtab" + (t === "planning" ? " active" : "");
  document.getElementById("subtab-reussites").className = "subtab" + (t === "reussites" ? " active" : "");
}

function switchWeekSubTab(t) {
  currentWeekSubTab = t;
  document.getElementById("semaine-content").style.display = t === "semaine" ? "block" : "none";
  document.getElementById("overview-content").style.display = t === "overview" ? "block" : "none";
  document.getElementById("subtab-semaine").className = "subtab" + (t === "semaine" ? " active" : "");
  document.getElementById("subtab-overview").className = "subtab" + (t === "overview" ? " active" : "");
}

function setWeek(w) {
  activeWeek = w;
  render();
}

// ── Render ─────────────────────────────────────────────────────────────────────
function render() {
  const todayKey = getTodayKey();
  const todayGoals = data.daily[todayKey]?.goals || {};
  const todayTasks = data.daily[todayKey]?.tasks || {};
  const goalsDone = GOALS.filter(g => todayGoals[g.id]).length;
  const tasksDone = Object.values(todayTasks).filter(Boolean).length;
  const totalDone = Array.from({length:12},(_,i)=>i+1).reduce((a,w)=>a+weeklyScore(w),0);
  const globalPct = Math.round(totalDone / (12*7*5) * 100);

  // Date
  const dateStr = new Date().toLocaleDateString("fr-FR", { weekday:"long", day:"numeric", month:"long" });
  document.getElementById("dateStr").textContent = dateStr;

  // Circles
  drawCircle("svg-reussites", goalsDone, 5, "#c8a84b", false);
  drawCircle("svg-taches", tasksDone, SCHEDULE.length, "#7a8c7a", false);
  drawCircle("svg-global", globalPct, 100, "#6b7c93", true);

  // Planning
  let planHTML = "";
  SCHEDULE.forEach((item, i) => {
    const done = !!todayTasks[i];
    const hasGoal = !!item.goalId;
    const borderLeft = done ? "3px solid #4a8a4a" : (hasGoal ? "3px solid #c8a84b" : "3px solid #2a2a2a");
    planHTML += `
      <div class="task-row ${done?'done':'undone'}" style="border-left:${borderLeft}" onclick="toggleTask(${i})">
        <span class="task-time">${item.time}</span>
        <span class="task-icon">${item.icon}</span>
        <span class="task-text ${done?'done':'undone'}">${item.task}${hasGoal?'<span style="margin-left:6px;font-size:10px;color:#c8a84b44">★</span>':''}</span>
        <span class="check ${done?'done':'undone'}">${done?'✓':''}</span>
      </div>`;
  });
  planHTML += `<div class="hint">★ = comptabilisé dans les réussites</div>`;
  document.getElementById("planning-content").innerHTML = planHTML;

  // Réussites
  let goalHTML = `<div style="font-size:11px;letter-spacing:4px;color:#555;text-transform:uppercase;text-align:center;margin-bottom:20px">Coche tes 5 réussites</div>`;
  GOALS.forEach(g => {
    const done = !!todayGoals[g.id];
    goalHTML += `
      <div class="goal-row ${done?'done':'undone'}" onclick="toggleGoal('${g.id}')">
        <span class="goal-icon">${g.icon}</span>
        <span class="goal-label ${done?'done':'undone'}">${g.label}</span>
        <span class="goal-check ${done?'done':'undone'}">${done?'✓':''}</span>
      </div>`;
  });
  if (goalsDone === 5) goalHTML += `<div class="perfect">★ JOURNÉE PARFAITE ★</div>`;
  document.getElementById("reussites-content").innerHTML = goalHTML;

  // Week picker
  let pickerHTML = `<div class="week-picker">`;
  for (let w = 1; w <= 12; w++) {
    const p = weeklyPct(w);
    const active = activeWeek === w;
    pickerHTML += `<button class="week-btn ${active?'active':''}" style="${active?'border:1px solid '+barColor(p):''};color:${active?'#f0e8d8':'#555'}" onclick="setWeek(${w})">
      <div style="font-size:9px;color:#555">S${w}</div>
      <div style="color:${p>0?barColor(p):'#2a2a2a'};font-size:11px">${p>0?p+'%':'·'}</div>
    </button>`;
  }
  pickerHTML += `</div>`;

  // Semaine detail
  const wpct = weeklyPct(activeWeek);
  let semaineHTML = pickerHTML;
  semaineHTML += `<div class="week-info">
    <div class="week-title">Semaine ${activeWeek}</div>
    <div class="week-sub">${getWeekLabel(activeWeek)}</div>
    <div class="week-score">${weeklyScore(activeWeek)}/35 · ${wpct}%</div>
  </div>`;

  GOALS.forEach(g => {
    const row = Array.from({length:7}, (_,d) => !!data.weekly[wKey(activeWeek,d,g.id)]);
    const count = row.filter(Boolean).length;
    semaineHTML += `<div class="goal-grid-row">
      <div class="goal-grid-header">
        <span style="font-size:15px">${g.icon}</span>
        <span class="goal-grid-label">${g.label}</span>
        <span class="goal-grid-count" style="color:${count===7?'#c8a84b':'#555'}">${count}/7</span>
      </div>
      <div class="day-grid">`;
    DAYS_SHORT.forEach((dl, d) => {
      const checked = row[d];
      semaineHTML += `<div class="day-cell ${checked?'checked':'unchecked'}" onclick="toggleWeeklyCell(${activeWeek},${d},'${g.id}')">
        <span class="day-letter ${checked?'checked':'unchecked'}">${dl}</span>
        ${checked?'<span class="day-tick">✓</span>':''}
      </div>`;
    });
    semaineHTML += `</div></div>`;
  });
  if (wpct === 100) semaineHTML += `<div class="perfect">★ SEMAINE PARFAITE ★</div>`;
  document.getElementById("semaine-content").innerHTML = semaineHTML;

  // Overview
  let overviewHTML = `<div style="font-size:11px;letter-spacing:4px;color:#555;text-transform:uppercase;text-align:center;margin-bottom:20px">28 mars → 25 juin 2026</div>`;
  for (let w = 1; w <= 12; w++) {
    const p = weeklyPct(w);
    const c = barColor(p);
    let dotsHTML = "";
    for (let d = 0; d < 7; d++) {
      const filled = GOALS.filter(g => data.weekly[wKey(w,d,g.id)]).length;
      const dc = filled===5?"#c8a84b":filled>=3?"#7eb87e":filled>=1?"#c4874a":"#1a1a1a";
      dotsHTML += `<div class="mini-dot" style="background:${dc}"></div>`;
    }
    overviewHTML += `<div class="overview-row" onclick="setWeek(${w});switchWeekSubTab('semaine')">
      <div class="overview-header">
        <span style="color:#666">S${w} <span style="color:#444;font-size:10px">${getWeekLabel(w)}</span></span>
        <span style="color:${p>0?c:'#333'}">${p>0?p+'%':'—'}</span>
      </div>
      <div class="overview-bar-bg"><div class="overview-bar" style="width:${p}%;background:${c}"></div></div>
      <div class="mini-dots">${dotsHTML}</div>
    </div>`;
  }
  overviewHTML += `<div class="legend">
    <div class="legend-item"><div class="legend-dot" style="background:#1a1a1a"></div>0%</div>
    <div class="legend-item"><div class="legend-dot" style="background:#c4874a"></div>1–59%</div>
    <div class="legend-item"><div class="legend-dot" style="background:#7eb87e"></div>60–84%</div>
    <div class="legend-item"><div class="legend-dot" style="background:#c8a84b"></div>85–100%</div>
  </div>`;
  document.getElementById("overview-content").innerHTML = overviewHTML;
}

// ── Midnight refresh ───────────────────────────────────────────────────────────
function scheduleMidnightRefresh() {
  const now = new Date();
  const midnight = new Date(now);
  midnight.setHours(24, 0, 0, 0);
  setTimeout(() => { location.reload(); }, midnight - now);
}

// ── Init ───────────────────────────────────────────────────────────────────────
loadData();
render();
scheduleMidnightRefresh();
</script>
</body>
</html>
