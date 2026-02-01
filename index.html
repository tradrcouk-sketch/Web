/* -----------
  ETHICAL RETENTION DESIGN
  - Personalization (quiz + scoring)
  - Compare tools (sorting/filtering)
  - Save + kit planner (localStorage)
  - Clear affiliate disclosure
  - No dark patterns, no fake timers, no forced signups
----------- */

const $ = (sel, el = document) => el.querySelector(sel);
const $$ = (sel, el = document) => Array.from(el.querySelectorAll(sel));

/**
 * Replace these with YOUR niche products + YOUR affiliate URLs.
 * Keep: name, category, price, rating, why, tags, url
 */
const PRODUCTS = [
  {
    id: "p1",
    name: "Lightweight Travel Tripod",
    category: "Travel",
    price: 89,
    rating: 4.6,
    why: "Compact, stable, great starter pick for portability.",
    tags: ["lightweight", "budget", "beginner"],
    url: "https://example.com/affiliate/tripod"
  },
  {
    id: "p2",
    name: "Pro-grade Carry Backpack",
    category: "Travel",
    price: 179,
    rating: 4.8,
    why: "Comfort + organization; ideal for frequent use.",
    tags: ["premium", "durable", "pro"],
    url: "https://example.com/affiliate/backpack"
  },
  {
    id: "p3",
    name: "Budget Wireless Earbuds",
    category: "Audio",
    price: 49,
    rating: 4.3,
    why: "Good sound for the money; easy everyday pick.",
    tags: ["budget", "casual", "commute"],
    url: "https://example.com/affiliate/earbuds"
  },
  {
    id: "p4",
    name: "Noise-Canceling Headphones",
    category: "Audio",
    price: 299,
    rating: 4.7,
    why: "Best for focus + flights; strong ANC performance.",
    tags: ["premium", "commute", "pro"],
    url: "https://example.com/affiliate/anc"
  },
  {
    id: "p5",
    name: "All-in-one Charger Kit",
    category: "Accessories",
    price: 39,
    rating: 4.5,
    why: "Useful add-on most people forget; reduces friction.",
    tags: ["budget", "travel", "essential"],
    url: "https://example.com/affiliate/charger"
  },
  {
    id: "p6",
    name: "Compact Power Bank",
    category: "Accessories",
    price: 59,
    rating: 4.6,
    why: "Reliable backup power; great for all-day use.",
    tags: ["mid", "travel", "essential"],
    url: "https://example.com/affiliate/powerbank"
  }
];

// ---------- State (persisted) ----------
const LS_KEYS = {
  saved: "smartpicks_saved_v1",
  kit: "smartpicks_kit_v1",
  quiz: "smartpicks_quiz_v1"
};

let saved = loadLS(LS_KEYS.saved, []); // array of product ids
let kit = loadLS(LS_KEYS.kit, []);     // array of {id, qty}
let quizState = loadLS(LS_KEYS.quiz, { step: 0, answers: {} });

let activeProfile = null; // computed from quiz answers
let tableSort = { key: "match", dir: "desc" };

// ---------- Quiz Model ----------
const QUIZ = [
  {
    key: "budget",
    title: "What’s your budget vibe?",
    help: "This helps us prioritize value vs premium features.",
    options: [
      { value: "budget", title: "Budget", desc: "Best value, fewer extras" },
      { value: "mid", title: "Mid-range", desc: "Balanced features + price" },
      { value: "premium", title: "Premium", desc: "Top performance + comfort" }
    ]
  },
  {
    key: "use",
    title: "How will you use it most?",
    help: "We’ll match products that fit your main scenario.",
    options: [
      { value: "travel", title: "Travel / on the go", desc: "Portable, compact, durable" },
      { value: "commute", title: "Commute / daily", desc: "Convenient, reliable, easy" },
      { value: "home", title: "Mostly at home", desc: "Comfort + performance" }
    ]
  },
  {
    key: "priority",
    title: "Pick your #1 priority",
    help: "This becomes your strongest scoring weight.",
    options: [
      { value: "lightweight", title: "Lightweight", desc: "Small + easy to carry" },
      { value: "durable", title: "Durable", desc: "Built to last" },
      { value: "performance", title: "Performance", desc: "Best output/quality" }
    ]
  },
  {
    key: "skill",
    title: "What’s your experience level?",
    help: "We’ll avoid overkill if you’re just starting out.",
    options: [
      { value: "beginner", title: "Beginner", desc: "Simple, forgiving picks" },
      { value: "intermediate", title: "Intermediate", desc: "More control and options" },
      { value: "pro", title: "Pro", desc: "Max capability, fewer compromises" }
    ]
  },
  {
    key: "style",
    title: "Decision style",
    help: "How do you want recommendations presented?",
    options: [
      { value: "fast", title: "Fast picks", desc: "Top 3, no fuss" },
      { value: "compare", title: "Let me compare", desc: "Show me trade-offs" },
      { value: "plan", title: "Help me plan a kit", desc: "Bundle-friendly suggestions" }
    ]
  }
];

// ---------- Init ----------
init();

function init(){
  $("#year").textContent = String(new Date().getFullYear());

  // Build category dropdown
  const categories = Array.from(new Set(PRODUCTS.map(p => p.category))).sort();
  const sel = $("#categorySelect");
  categories.forEach(c => {
    const opt = document.createElement("option");
    opt.value = c;
    opt.textContent = c;
    sel.appendChild(opt);
  });

  // Wire UI
  $("#btnOpenSaved").addEventListener("click", openDrawer);
  $("#drawerBackdrop").addEventListener("click", closeDrawer);
  $("#drawerClose").addEventListener("click", closeDrawer);
  $("#btnClearSaved").addEventListener("click", () => { saved = []; persist(); renderAll(); });

  $("#btnOpenDisclosure").addEventListener("click", openModal);
  $("#modalBackdrop").addEventListener("click", closeModal);
  $("#modalClose").addEventListener("click", closeModal);
  $("#modalOk").addEventListener("click", closeModal);

  $("#btnShare").addEventListener("click", sharePicks);
  $("#btnExportData").addEventListener("click", exportData);

  $("#btnRandomize").addEventListener("click", () => {
    // playful micro-interaction: random answer set then compute
    quizState.answers = {
      budget: pick(["budget","mid","premium"]),
      use: pick(["travel","commute","home"]),
      priority: pick(["lightweight","durable","performance"]),
      skill: pick(["beginner","intermediate","pro"]),
      style: pick(["fast","compare","plan"])
    };
    quizState.step = QUIZ.length;
    persist();
    computeProfileAndRenderResults(true);
    document.location.hash = "#quiz";
  });

  // Quiz nav
  $("#btnPrev").addEventListener("click", () => { goStep(quizState.step - 1); });
  $("#btnNext").addEventListener("click", () => {
    if (quizState.step < QUIZ.length - 1) goStep(quizState.step + 1);
    else computeProfileAndRenderResults(true);
  });
  $("#btnResetQuiz").addEventListener("click", resetQuiz);

  // Compare controls
  $("#searchInput").addEventListener("input", renderCompare);
  $("#maxPrice").addEventListener("input", () => {
    $("#maxPriceLabel").textContent = `£${$("#maxPrice").value}`;
    renderCompare();
  });
  $("#categorySelect").addEventListener("change", renderCompare);
  $("#btnClearFilters").addEventListener("click", () => {
    $("#searchInput").value = "";
    $("#maxPrice").value = "500";
    $("#maxPriceLabel").textContent = "£500";
    $("#categorySelect").value = "all";
    renderCompare();
  });
  $("#btnSortScore").addEventListener("click", () => {
    tableSort = { key: "match", dir: tableSort.dir === "desc" ? "asc" : "desc" };
    renderCompare();
  });

  $$("#compareTable .thbtn").forEach(btn => {
    btn.addEventListener("click", () => {
      const key = btn.dataset.sort;
      if (tableSort.key === key) tableSort.dir = tableSort.dir === "asc" ? "desc" : "asc";
      else tableSort = { key, dir: "asc" };
      renderCompare();
    });
  });

  $("#btnClearKit").addEventListener("click", () => { kit = []; persist(); renderAll(); });

  // Reading progress
  document.addEventListener("scroll", renderReadingProgress, { passive: true });

  // First render
  renderQuiz();
  computeProfileAndRenderResults(false);
  renderAll();
}

function renderAll(){
  updateSavedCount();
  renderSavedDrawer();
  renderHeroPicks();
  renderCompare();
  renderKit();
  renderAddons();
  $("#statSaved").textContent = String(saved.length);
}

function updateSavedCount(){
  $("#savedCount").textContent = String(saved.length);
}

// ---------- Quiz ----------
function goStep(step){
  step = clamp(step, 0, QUIZ.length - 1);
  quizState.step = step;
  persist();
  renderQuiz();
}

function resetQuiz(){
  quizState = { step: 0, answers: {} };
  activeProfile = null;
  persist();
  renderQuiz();
  $("#quizResult").hidden = true;
  $("#picksEmpty").hidden = false;
  $("#picksList").hidden = true;
  renderAll();
}

function renderQuiz(){
  const step = quizState.step;
  const q = QUIZ[step];

  $("#btnPrev").disabled = step === 0;
  $("#btnNext").textContent = step === QUIZ.length - 1 ? "See results" : "Next";

  const pct = Math.round((step / QUIZ.length) * 100);
  $("#quizBar").style.width = `${pct}%`;
  $("#quizStepText").textContent = `Step ${step + 1} of ${QUIZ.length}`;

  const body = $("#quizBody");
  body.innerHTML = "";

  const h = document.createElement("h3");
  h.className = "qtitle";
  h.textContent = q.title;

  const p = document.createElement("p");
  p.className = "qhelp";
  p.textContent = q.help;

  const opts = document.createElement("div");
  opts.className = "opts";

  q.options.forEach(opt => {
    const btn = document.createElement("button");
    btn.type = "button";
    btn.className = "opt";
    btn.setAttribute("aria-pressed", quizState.answers[q.key] === opt.value ? "true" : "false");

    btn.innerHTML = `
      <div class="opt__title">${escapeHtml(opt.title)}</div>
      <div class="opt__desc">${escapeHtml(opt.desc)}</div>
    `;

    btn.addEventListener("click", () => {
      quizState.answers[q.key] = opt.value;
      persist();
      renderQuiz(); // refresh pressed state

      // micro-win: auto-advance unless last step
      if (quizState.step < QUIZ.length - 1) {
        setTimeout(() => goStep(quizState.step + 1), 140);
      } else {
        setTimeout(() => computeProfileAndRenderResults(true), 140);
      }
    });

    opts.appendChild(btn);
  });

  body.appendChild(h);
  body.appendChild(p);
  body.appendChild(opts);
}

function computeProfileAndRenderResults(show){
  // If incomplete, don't force results
  if (!isQuizComplete()){
    activeProfile = null;
    $("#statMatches").textContent = "—";
    renderAll();
    return;
  }

  activeProfile = buildProfile(quizState.answers);

  const scored = PRODUCTS
    .map(p => ({ p, score: scoreProduct(p, activeProfile) }))
    .sort((a,b) => b.score - a.score);

  $("#statMatches").textContent = String(scored.length);

  if (show){
    $("#quizResult").hidden = false;
    const grid = $("#resultGrid");
    grid.innerHTML = "";
    scored.slice(0,3).forEach(({p, score}, idx) => {
      const card = document.createElement("div");
      card.className = "resultCard";
      card.innerHTML = `
        <h4>${idx+1}. ${escapeHtml(p.name)}</h4>
        <p><strong>Match:</strong> ${Math.round(score)} / 100</p>
        <p>${escapeHtml(p.why)}</p>
      `;
      grid.appendChild(card);
    });

    // show picks in hero panel too
    renderHeroPicks();

    // a tiny celebration (no external libs)
    confettiBurst(18);
  }

  renderAll();
}

function isQuizComplete(){
  return QUIZ.every(q => Boolean(quizState.answers[q.key]));
}

function buildProfile(ans){
  // Simple weights and tag preferences
  return {
    budget: ans.budget,     // budget | mid | premium
    use: ans.use,           // travel | commute | home
    priority: ans.priority, // lightweight | durable | performance
    skill: ans.skill,       // beginner | intermediate | pro
    style: ans.style        // fast | compare | plan
  };
}

function scoreProduct(prod, profile){
  // Base 50 + tag matches. Keep it understandable + tunable.
  let s = 50;

  // budget alignment
  if (profile.budget === "budget" && prod.tags.includes("budget")) s += 14;
  if (profile.budget === "mid" && (prod.tags.includes("mid") || prod.price <= 120)) s += 10;
  if (profile.budget === "premium" && (prod.tags.includes("premium") || prod.price >= 150)) s += 12;

  // use alignment
  if (profile.use === "travel" && (prod.tags.includes("travel") || prod.category === "Travel")) s += 12;
  if (profile.use === "commute" && prod.tags.includes("commute")) s += 12;
  if (profile.use === "home" && (prod.tags.includes("pro") || prod.tags.includes("performance"))) s += 8;

  // priority alignment
  if (profile.priority === "lightweight" && prod.tags.includes("lightweight")) s += 16;
  if (profile.priority === "durable" && prod.tags.includes("durable")) s += 16;
  if (profile.priority === "performance" && (prod.tags.includes("pro") || prod.tags.includes("premium"))) s += 16;

  // skill alignment
  if (profile.skill === "beginner" && prod.tags.includes("beginner")) s += 10;
  if (profile.skill === "pro" && prod.tags.includes("pro")) s += 10;

  // rating influence (soft)
  s += clamp((prod.rating - 4.0) * 10, 0, 10);

  // cap
  return clamp(s, 0, 100);
}

// ---------- Hero Picks ----------
function renderHeroPicks(){
  const picksList = $("#picksList");
  const empty = $("#picksEmpty");

  if (!activeProfile){
    empty.hidden = false;
    picksList.hidden = true;
    picksList.innerHTML = "";
    return;
  }

  const scored = PRODUCTS
    .map(p => ({ p, score: scoreProduct(p, activeProfile) }))
    .sort((a,b) => b.score - a.score)
    .slice(0,3);

  empty.hidden = true;
  picksList.hidden = false;
  picksList.innerHTML = "";

  scored.forEach(({p, score}) => {
    const row = document.createElement("div");
    row.className = "pick";
    row.innerHTML = `
      <div class="pick__left">
        <div>
          <div class="pick__name">
            ${escapeHtml(p.name)}
            <span class="badge2">Match ${Math.round(score)}/100</span>
          </div>
          <div class="pick__why">${escapeHtml(p.why)}</div>
        </div>
      </div>
      <div class="pick__right">
        <a class="btn btn--primary" href="${escapeAttr(p.url)}" target="_blank" rel="noopener noreferrer nofollow">
          View deal
        </a>
        <button class="btn btn--ghost" type="button" data-save="${p.id}">
          ${saved.includes(p.id) ? "Saved" : "Save"}
        </button>
        <button class="btn btn--ghost" type="button" data-kit="${p.id}">Add to kit</button>
      </div>
    `;

    // wire buttons
    row.querySelector(`[data-save="${p.id}"]`).addEventListener("click", () => toggleSaved(p.id));
    row.querySelector(`[data-kit="${p.id}"]`).addEventListener("click", () => addToKit(p.id));

    picksList.appendChild(row);
  });
}

// ---------- Compare Table ----------
function renderCompare(){
  const tbody = $("#compareTbody");
  tbody.innerHTML = "";

  const q = ($("#searchInput").value || "").trim().toLowerCase();
  const maxP = Number($("#maxPrice").value);
  const cat = $("#categorySelect").value;

  let rows = PRODUCTS.slice();

  // filter
  rows = rows.filter(p => p.price <= maxP);
  if (cat !== "all") rows = rows.filter(p => p.category === cat);
  if (q){
    rows = rows.filter(p => {
      const blob = `${p.name} ${p.category} ${p.why} ${p.tags.join(" ")}`.toLowerCase();
      return blob.includes(q);
    });
  }

  // add match score if profile exists
  const withScore = rows.map(p => ({
    p,
    match: activeProfile ? scoreProduct(p, activeProfile) : null
  }));

  // sort
  withScore.sort((a,b) => {
    const dir = tableSort.dir === "asc" ? 1 : -1;
    const k = tableSort.key;
    if (k === "match"){
      const av = a.match ?? 0, bv = b.match ?? 0;
      return (av - bv) * dir;
    }
    if (k === "price") return (a.p.price - b.p.price) * dir;
    if (k === "rating") return (a.p.rating - b.p.rating) * dir;
    if (k === "name") return a.p.name.localeCompare(b.p.name) * dir;
    if (k === "category") return a.p.category.localeCompare(b.p.category) * dir;
    return 0;
  });

  withScore.forEach(({p, match}) => {
    const tr = document.createElement("tr");

    const matchText = activeProfile ? ` • Match ${Math.round(match)}/100` : "";
    tr.innerHTML = `
      <td><strong>${escapeHtml(p.name)}</strong><div class="tiny muted">${escapeHtml(p.tags.join(" • "))}${matchText}</div></td>
      <td>${escapeHtml(p.category)}</td>
      <td class="num">£${p.price}</td>
      <td>${p.rating.toFixed(1)} ★</td>
      <td class="muted">${escapeHtml(p.why)}</td>
      <td class="actionsCol">
        <a class="btn btn--primary" href="${escapeAttr(p.url)}" target="_blank" rel="noopener noreferrer nofollow">View</a>
        <button class="btn btn--ghost" type="button" data-save="${p.id}">${saved.includes(p.id) ? "Saved" : "Save"}</button>
        <button class="btn btn--ghost" type="button" data-kit="${p.id}">Add</button>
      </td>
    `;

    tr.querySelector(`[data-save="${p.id}"]`).addEventListener("click", () => toggleSaved(p.id));
    tr.querySelector(`[data-kit="${p.id}"]`).addEventListener("click", () => addToKit(p.id));
    tbody.appendChild(tr);
  });
}

// ---------- Saved + Kit ----------
function toggleSaved(id){
  if (saved.includes(id)) saved = saved.filter(x => x !== id);
  else saved = [...saved, id];
  persist();
  renderAll();
}

function addToKit(id){
  const row = kit.find(x => x.id === id);
  if (row) row.qty += 1;
  else kit.push({ id, qty: 1 });
  persist();
  renderAll();
}

function removeFromKit(id){
  kit = kit.filter(x => x.id !== id);
  persist();
  renderAll();
}

function setKitQty(id, qty){
  qty = clamp(Number(qty) || 1, 1, 99);
  const row = kit.find(x => x.id === id);
  if (!row) return;
  row.qty = qty;
  persist();
  renderAll();
}

function renderSavedDrawer(){
  $("#savedList").innerHTML = "";
  const list = $("#savedList");

  if (saved.length === 0){
    list.innerHTML = `<div class="muted">No saved items yet. Save a few from the quiz or compare table.</div>`;
    return;
  }

  saved.map(id => PRODUCTS.find(p => p.id === id))
    .filter(Boolean)
    .forEach(p => {
      const div = document.createElement("div");
      div.className = "kitItem";
      div.innerHTML = `
        <div>
          <div style="font-weight:800">${escapeHtml(p.name)}</div>
          <div class="tiny muted">£${p.price} • ${escapeHtml(p.category)}</div>
        </div>
        <div style="display:flex; gap:8px; align-items:center; flex-wrap:wrap; justify-content:flex-end">
          <a class="btn btn--primary" href="${escapeAttr(p.url)}" target="_blank" rel="noopener noreferrer nofollow">View</a>
          <button class="btn btn--ghost" type="button" data-remove="${p.id}">Remove</button>
        </div>
      `;
      div.querySelector(`[data-remove="${p.id}"]`).addEventListener("click", () => toggleSaved(p.id));
      list.appendChild(div);
    });
}

function renderKit(){
  const list = $("#kitList");
  const empty = $("#kitEmpty");
  list.innerHTML = "";

  if (kit.length === 0){
    empty.style.display = "block";
    $("#kitTotal").textContent = "£0";
    return;
  }
  empty.style.display = "none";

  let total = 0;
  kit.forEach(item => {
    const p = PRODUCTS.find(x => x.id === item.id);
    if (!p) return;
    total += p.price * item.qty;

    const row = document.createElement("div");
    row.className = "kitItem";
    row.innerHTML = `
      <div>
        <div style="font-weight:800">${escapeHtml(p.name)}</div>
        <div class="tiny muted">£${p.price} each • ${escapeHtml(p.category)}</div>
      </div>
      <div style="display:flex; gap:8px; align-items:center; flex-wrap:wrap; justify-content:flex-end">
        <label class="tiny muted" style="display:flex; align-items:center; gap:8px">
          Qty
          <input type="number" min="1" max="99" value="${item.qty}" style="width:78px"
                 class="qtyInput" data-qty="${p.id}" />
        </label>
        <button class="btn btn--ghost" type="button" data-del="${p.id}">Remove</button>
      </div>
    `;
    row.querySelector(`[data-del="${p.id}"]`).addEventListener("click", () => removeFromKit(p.id));
    row.querySelector(`[data-qty="${p.id}"]`).addEventListener("input", (e) => setKitQty(p.id, e.target.value));
    list.appendChild(row);
  });

  $("#kitTotal").textContent = `£${total}`;
}

function renderAddons(){
  const grid = $("#addonGrid");
  grid.innerHTML = "";

  // Suggest add-ons: essentials + travel if profile says travel
  const base = PRODUCTS.filter(p => p.tags.includes("essential"));
  const travelExtras = activeProfile?.use === "travel" ? PRODUCTS.filter(p => p.category === "Travel") : [];
  const pool = uniqueById([...base, ...travelExtras]).slice(0,4);

  pool.forEach(p => {
    const div = document.createElement("div");
    div.className = "addon";
    div.innerHTML = `
      <div>
        <div class="addon__name">${escapeHtml(p.name)}</div>
        <div class="addon__meta">£${p.price} • ${escapeHtml(p.why)}</div>
      </div>
      <div style="display:flex; gap:8px; align-items:center; flex-wrap:wrap; justify-content:flex-end">
        <a class="btn btn--primary" href="${escapeAttr(p.url)}" target="_blank" rel="noopener noreferrer nofollow">View</a>
        <button class="btn btn--ghost" type="button" data-kit="${p.id}">Add</button>
      </div>
    `;
    div.querySelector(`[data-kit="${p.id}"]`).addEventListener("click", () => addToKit(p.id));
    grid.appendChild(div);
  });
}

// ---------- Drawer / Modal ----------
function openDrawer(){
  $("#drawer").setAttribute("aria-hidden", "false");
  $("#btnGoCompare").focus();
}
function closeDrawer(){
  $("#drawer").setAttribute("aria-hidden", "true");
}

function openModal(){
  $("#modal").setAttribute("aria-hidden", "false");
  $("#modalOk").focus();
}
function closeModal(){
  $("#modal").setAttribute("aria-hidden", "true");
}

// ---------- Share / Export ----------
async function sharePicks(){
  if (!activeProfile){
    alert("Take the quiz first so we have picks to share.");
    return;
  }
  const top = PRODUCTS
    .map(p => ({ p, s: scoreProduct(p, activeProfile) }))
    .sort((a,b) => b.s - a.s)
    .slice(0,3)
    .map(x => `• ${x.p.name} (${Math.round(x.s)}/100)`);

  const text = `My Smart Picks:\n${top.join("\n")}\n\n(Generated by the quiz)`;
  try{
    if (navigator.share){
      await navigator.share({ title: document.title, text });
    } else {
      await navigator.clipboard.writeText(text);
      toast("Copied picks to clipboard!");
    }
  } catch {
    // user cancelled or unavailable
  }
}

function exportData(){
  const payload = {
    saved,
    kit,
    quiz: quizState,
    profile: activeProfile
  };
  const blob = new Blob([JSON.stringify(payload, null, 2)], { type: "application/json" });
  const a = document.createElement("a");
  a.href = URL.createObjectURL(blob);
  a.download = "my-smartpicks.json";
  document.body.appendChild(a);
  a.click();
  a.remove();
  toast("Exported your data.");
}

// ---------- Reading progress ----------
function renderReadingProgress(){
  const doc = document.documentElement;
  const scrollTop = doc.scrollTop || document.body.scrollTop;
  const scrollHeight = (doc.scrollHeight || document.body.scrollHeight) - doc.clientHeight;
  const pct = scrollHeight > 0 ? (scrollTop / scrollHeight) * 100 : 0;
  $("#readingBar").style.width = `${clamp(pct, 0, 100)}%`;
}

// ---------- Persistence ----------
function persist(){
  saveLS(LS_KEYS.saved, saved);
  saveLS(LS_KEYS.kit, kit);
  saveLS(LS_KEYS.quiz, quizState);
}

function loadLS(key, fallback){
  try{
    const raw = localStorage.getItem(key);
    if (!raw) return fallback;
    return JSON.parse(raw);
  } catch {
    return fallback;
  }
}
function saveLS(key, value){
  try{ localStorage.setItem(key, JSON.stringify(value)); } catch {}
}

// ---------- Tiny UI helpers ----------
function toast(msg){
  const t = document.createElement("div");
  t.textContent = msg;
  t.style.position = "fixed";
  t.style.left = "50%";
  t.style.bottom = "22px";
  t.style.transform = "translateX(-50%)";
  t.style.padding = "10px 12px";
  t.style.borderRadius = "14px";
  t.style.background = "rgba(12,14,20,.95)";
  t.style.border = "1px solid rgba(255,255,255,.16)";
  t.style.boxShadow = "0 18px 60px rgba(0,0,0,.45)";
  t.style.zIndex = "9999";
  document.body.appendChild(t);
  setTimeout(() => t.remove(), 1600);
}

function confettiBurst(n = 16){
  // super-light confetti: DOM nodes that fall then remove
  for (let i=0; i<n; i++){
    const s = document.createElement("span");
    s.style.position = "fixed";
    s.style.left = `${Math.random()*100}vw`;
    s.style.top = `-10px`;
    s.style.width = "10px";
    s.style.height = "10px";
    s.style.borderRadius = "3px";
    s.style.background = `hsl(${Math.random()*360}, 95%, 65%)`;
    s.style.opacity = "0.95";
    s.style.zIndex = "9999";
    const dur = 900 + Math.random()*900;
    const dx = (Math.random() - 0.5) * 120;
    s.animate([
      { transform: "translate(0,0) rotate(0deg)" },
      { transform: `translate(${dx}px, 110vh) rotate(${(Math.random()*720)-360}deg)` }
    ], { duration: dur, easing: "cubic-bezier(.2,.6,.2,1)" });
    document.body.appendChild(s);
    setTimeout(() => s.remove(), dur + 60);
  }
}

function uniqueById(arr){
  const m = new Map();
  arr.forEach(x => m.set(x.id, x));
  return Array.from(m.values());
}
function clamp(n, a, b){ return Math.max(a, Math.min(b, n)); }
function pick(arr){ return arr[Math.floor(Math.random()*arr.length)]; }

function escapeHtml(str){
  return String(str).replace(/[&<>"']/g, s => ({
    "&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#039;"
  }[s]));
}
function escapeAttr(str){
  // minimal escaping for attribute contexts
  return String(str).replace(/"/g, "%22");
}
