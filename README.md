[28/10, 8:54 pm] Simra: <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="theme-color" content="#0B0F1A">
  <title>Ledgerly — Expense Tracker</title>
  <link rel="stylesheet" href="style.css">
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body>
  <canvas id="bg"></canvas>

  <header class="topbar">
    <a class="brand" href="#">LEDGER<span>LY</span></a>
    <nav id="tabs" aria-label="Main">
      <button data-v="dashboard" class="on">Dashboard</button>
      <button data-v="transactions">Transactions</button>
      <button data-v="reports">Reports</button>
    </nav>
  </header>

  <main>
    <section class="page active" id="dashboard">
      <div class="heading">
        <div>
          <p class="eyebrow">PERSONAL FINANCE</p>
          <h1 id="wHi">Welcome.</h1>
          <p id="wDate" class="muted"></p>
        </div>
        <div class="month-control">
          <label for="month">REPORTING MONTH</label>
          <input class="in" id="month" type="month">
        </div>
      </div>

      <div class="card hero">
        <p class="eyebrow">TOTAL BALANCE</p>
        <h2 id="sBal">₹0.00</h2>
        <p id="wMsg" class="muted">Start tracking your money.</p>
        <div class="trk"><b id="wBar"></b></div>
        <small id="wRate" class="muted">0% of income spent</small>

        <div class="name-box">
          <label for="wName">YOUR NAME</label>
          <input class="in" id="wName" maxlength="40"
                 placeholder="Enter your name">
        </div>
        <button class="btn" id="qE" type="button">+ Add expense</button>
      </div>

      <div class="cards">
        <article class="card">
          <p class="muted">MONTHLY INCOME</p>
          <h3 class="positive" id="sInc">₹0.00</h3>
        </article>
        <article class="card">
          <p class="muted">MONTHLY EXPENSES</p>
          <h3 class="negative" id="sExp">₹0.00</h3>
        </article>
        <article class="card">
          <p class="muted">SAVINGS RATE</p>
          <h3 id="sRate">—</h3>
        </article>
      </div>

      <div class="g2">
        <article class="card">
          <h3>Expense breakdown</h3>
          <div class="chart-wrap">
            <canvas id="cDon"></canvas>
          </div>
          <p id="chartEmpty" class="muted">
            Add expenses to see your chart.
          </p>
          <div id="categoryLegend"></div>
        </article>

        <article class="card">
          <h3>Recent transactions</h3>
          <div id="recentList"></div>
        </article>
      </div>

      <article class="card">
        <h3>Add a transaction</h3>

        <form id="form" novalidate>
          <div class="seg" id="seg">
            <span class="pill"></span>
            <button type="button" data-t="expense" class="on">Expense</button>
            <button type="button" data-t="income">Income</button>
          </div>

          <div class="form-grid">
            <div>
              <label for="amount">Amount (₹)</label>
              <input class="in" id="amount" type="number"
                     min="0.01" step="0.01" placeholder="0.00" required>
            </div>
            <div>
              <label for="title">Transaction name</label>
              <input class="in" id="title" maxlength="60"
                     placeholder="e.g. Groceries" required>
            </div>
            <div>
              <label for="cat">Category</label>
              <select class="in" id="cat" required></select>
            </div>
            <div>
              <label for="date">Date</label>
              <input class="in" id="date" type="date" required>
            </div>
          </div>

          <p id="formError" class="error" role="alert"></p>
          <button class="btn" type="submit">Add transaction</button>
          <button class="btn secondary" type="reset">Clear</button>
        </form>
      </article>
    </section>

    <section class="page" id="transactions">
      <div class="heading">
        <div>
          <p class="eyebrow">YOUR FINANCIAL RECORDS</p>
          <h1>Transactions</h1>
        </div>
        <button class="btn" id="exportBtn" type="button">Export CSV</button>
      </div>

      <div class="cards">
        <article class="card">
          <p class="muted">ALL-TIME INCOME</p>
          <h3 id="allInc" class="positive">₹0.00</h3>
        </article>
        <article class="card">
          <p class="muted">ALL-TIME EXPENSES</p>
          <h3 id="allExp" class="negative">₹0.00</h3>
        </article>
        <article class="card">
          <p class="muted">TRANSACTIONS</p>
          <h3 id="txCount">0</h3>
        </article>
      </div>

      <article class="card">
        <h3>Transaction history</h3>

        <div class="filters">
          <input class="in" id="searchTx" placeholder="Search transactions">
          <select class="in" id="filterType">
            <option value="all">All types</option>
            <option value="income">Income</option>
            <option value="expense">Expense</option>
          </select>
          <select class="in" id="filterCat">
            <option value="all">All categories</option>
          </select>
        </div>

        <div class="table-wrap">
          <table>
            <thead>
              <tr>
                <th>Name</th>
                <th>Category</th>
                <th>Date</th>
                <th>Type</th>
                <th>Amount</th>
                <th>Action</th>
              </tr>
            </thead>
            <tbody id="tbody"></tbody>
          </table>
        </div>

        <p id="tableEmpty" class="muted">No transactions found.</p>
        <p id="tableCount" class="muted"></p>
      </article>
    </section>

    <section class="page" id="reports">
      <div class="heading">
        <div>
          <p class="eyebrow">FINANCIAL INSIGHTS</p>
          <h1>Reports</h1>
        </div>
        <div class="month-control">
          <label for="reportMonth">REPORTING MONTH</label>
          <input class="in" id="reportMonth" type="month">
        </div>
      </div>

      <div class="cards">
        <article class="card">
          <p class="muted">INCOME</p>
          <h3 id="rInc" class="positive">₹0.00</h3>
        </article>
        <article class="card">
          <p class="muted">EXPENSES</p>
          <h3 id="rExp" class="negative">₹0.00</h3>
        </article>
        <article class="card">
          <p class="muted">NET SAVINGS</p>
          <h3 id="rNet">₹0.00</h3>
        </article>
      </div>

      <div class="g2">
        <article class="card">
          <h3>Income vs expenses</h3>
          <div class="chart-wrap"><canvas id="cFlow"></canvas></div>
        </article>
        <article class="card">
          <h3>Category totals</h3>
          <div id="reportCategories"></div>
        </article>
      </div>

      <article class="card">
        <h3>Monthly summary</h3>
        <div id="reportSummary"></div>
      </article>
    </section>
  </main>

  <footer>
    LEDGERLY · PERSONAL FINANCE · DATA SAVED IN YOUR BROWSER
  </footer>

  <div id="deleteModal" class="modal" hidden>
    <div class="modal-box card" role="dialog" aria-modal="true"
         aria-labelledby="deleteHeading">
      <h3 id="deleteHeading">Delete transaction?</h3>
      <p class="muted">You can undo this action immediately afterward.</p>
      <button id="dYes" class="btn danger" type="button">Delete</button>
      <button id="dNo" class="btn secondary" type="button">Cancel</button>
    </div>
  </div>

  <div id="toast" class="toast" role="status" aria-live="polite"></div>

  <script src="script.js"></script>
</body>
</html>
[28/10, 8:56 pm] Simra: :root {
  --bg: #0B0F1A;
  --s1: #131A2A;
  --edge: #2A3550;
  --ind: #6C7CFF;
  --mint: #2DD4BF;
  --inc: #34D399;
  --exp: #FB7185;
  --tx: #E8ECF5;
  --mu: #94A3B8;
  color-scheme: dark;
}

* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background: radial-gradient(1200px 700px at 70% -10%, #17214a, var(--bg)) fixed;
  color: var(--tx);
  font: 15px/1.5 Inter, system-ui, sans-serif;
}

button, input, select {
  font: inherit;
}

button {
  cursor: pointer;
}

#bg {
  position: fixed;
  inset: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
  pointer-events: none;
  opacity: 0.12;
}

.topbar {
  position: sticky;
  top: 0;
  z-index: 5;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
  min-height: 70px;
  padding: 12px 5%;
  background: rgba(11, 15, 26, 0.88);
  border-bottom: 1px solid var(--edge);
  backdrop-filter: blur(14px);
}

.brand {
  color: var(--tx);
  font-size: 21px;
  font-weight: 900;
  letter-spacing: 1.5px;
  text-decoration: none;
}

.brand span {
  color: var(--mint);
}

#tabs {
  display: flex;
  gap: 6px;
}

#tabs button {
  padding: 10px 15px;
  border: 1px solid transparent;
  border-radius: 9px;
  color: var(--mu);
  background: transparent;
}

#tabs button:hover,
#tabs button.on {
  color: var(--tx);
  background: #6c7cff1b;
  border-color: #6c7cff55;
}

main {
  width: min(1200px, 92%);
  margin: 30px auto;
}

.page {
  display: none;
}

.page.active {
  display: block;
  animation: fadeIn 0.25s ease;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(5px); }
  to { opacity: 1; transform: translateY(0); }
}

.heading {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
  margin-bottom: 22px;
}

h1, h2, h3, p {
  overflow-wrap: anywhere;
}

h1 {
  font-size: clamp(27px, 4vw, 36px);
  margin: 0;
}

h2 {
  font-size: clamp(32px, 5vw, 45px);
  margin: 0;
}

h3 {
  font-size: 18px;
  margin: 0 0 15px;
}

.eyebrow {
  color: var(--mint);
  font-size: 10px;
  font-weight: 800;
  letter-spacing: 2px;
}

.muted {
  color: var(--mu);
  font-size: 13px;
}

.card {
  min-width: 0;
  padding: 22px;
  margin-bottom: 18px;
  background: rgba(19, 26, 42, 0.88);
  border: 1px solid var(--edge);
  border-radius: 16px;
  box-shadow: 0 10px 30px #00000012;
  backdrop-filter: blur(14px);
}

.hero {
  background: radial-gradient(ellipse at 90% 10%, #6c7cff22, transparent 45%),
              rgba(19, 26, 42, 0.92);
  border-color: #49568a;
}

.hero .btn {
  margin-top: 15px;
}

.name-box {
  max-width: 260px;
  margin-top: 20px;
}

label {
  display: block;
  margin-bottom: 7px;
  color: var(--mu);
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 1px;
}

.month-control {
  width: 190px;
  flex-shrink: 0;
}

.in {
  width: 100%;
  min-width: 0;
  padding: 12px;
  color: var(--tx);
  background: #0d1424;
  border: 1px solid var(--edge);
  border-radius: 9px;
  outline: none;
}

.in:focus {
  border-color: var(--ind);
  box-shadow: 0 0 0 3px #6c7cff18;
}

.cards {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 16px;
}

.cards .card {
  margin-bottom: 18px;
}

.cards h3 {
  margin: 10px 0 0;
  font-size: clamp(20px, 2.5vw, 27px);
}

.positive {
  color: var(--inc);
}

.negative {
  color: var(--exp);
}

.g2 {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 18px;
}

.trk {
  height: 6px;
  margin: 14px 0 5px;
  overflow: hidden;
  border-radius: 10px;
  background: #263149;
}

.trk b {
  display: block;
  width: 0;
  height: 100%;
  background: linear-gradient(90deg, var(--ind), var(--mint));
  transition: width 0.4s ease;
}

.seg {
  position: relative;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4px;
  padding: 4px;
  margin: 20px 0;
  border: 1px solid var(--edge);
  border-radius: 10px;
  background: #0d1424;
  isolation: isolate;
}

.seg button {
  position: relative;
  z-index: 1;
  padding: 11px;
  color: var(--mu);
  border: 0;
  border-radius: 7px;
  background: transparent;
}

.seg button.on {
  color: white;
}

.seg .pill {
  position: absolute;
  z-index: 0;
  top: 4px;
  bottom: 4px;
  left: 4px;
  width: calc(50% - 4px);
  border: 1px solid #fb718555;
  border-radius: 7px;
  background: #fb718522;
  transition: transform 0.25s, background 0.25s;
}

.seg.inc .pill {
  transform: translateX(100%);
  border-color: #34d39955;
  background: #34d39922;
}

.form-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 16px;
  margin-bottom: 18px;
}

.btn {
  padding: 11px 17px;
  color: white;
  font-weight: 700;
  background: linear-gradient(135deg, #7584ff, #5866e8);
  border: 1px solid transparent;
  border-radius: 9px;
}

.btn:hover {
  filter: brightness(1.12);
}

.btn.secondary {
  color: var(--tx);
  background: #1a2438;
  border-color: var(--edge);
}

.btn.danger {
  background: var(--exp);
  color: #210b12;
}

.error {
  color: var(--exp);
  font-size: 12px;
}

.chart-wrap {
  position: relative;
  height: 240px;
  max-width: 100%;
}

#categoryLegend {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 8px;
  margin-top: 15px;
  color: var(--mu);
  font-size: 12px;
}

.legend-item {
  display: flex;
  align-items: center;
  gap: 7px;
}

.legend-dot {
  width: 9px;
  height: 9px;
  flex-shrink: 0;
  border-radius: 3px;
}

.recent-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 10px;
  padding: 13px 0;
  border-bottom: 1px solid #ffffff10;
}

.recent-item:last-child {
  border-bottom: 0;
}

.recent-info {
  flex: 1;
  min-width: 0;
}

.recent-info strong,
.recent-info small {
  display: block;
}

.recent-info strong {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.recent-info small {
  color: var(--mu);
  font-size: 11px;
}

.recent-amount {
  white-space: nowrap;
  font-size: 13px;
  font-weight: 800;
}

.filters {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr;
  gap: 12px;
  margin: 20px 0;
}

.table-wrap {
  width: 100%;
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
  text-align: left;
  white-space: nowrap;
}

th {
  padding: 13px 10px;
  color: var(--mu);
  font-size: 10px;
  letter-spacing: 1px;
  border-bottom: 1px solid var(--edge);
}

td {
  padding: 14px 10px;
  font-size: 12px;
  border-bottom: 1px solid #ffffff0c;
}

tbody tr:hover {
  background: #ffffff05;
}

.type-badge {
  padding: 4px 8px;
  border-radius: 6px;
  font-size: 10px;
}

.type-badge.income {
  color: var(--inc);
  background: #34d39918;
}

.type-badge.expense {
  color: var(--exp);
  background: #fb718518;
}

.delete-btn {
  padding: 6px 10px;
  color: var(--exp);
  background: #fb718510;
  border: 1px solid #fb718540;
  border-radius: 7px;
}

.report-category {
  margin: 17px 0;
}

.report-top {
  display: flex;
  justify-content: space-between;
  gap: 10px;
  font-size: 12px;
  margin-bottom: 7px;
}

.report-track {
  height: 6px;
  overflow: hidden;
  border-radius: 10px;
  background: #263149;
}

.report-track span {
  display: block;
  height: 100%;
  background: linear-gradient(90deg, var(--ind), var(--mint));
}

#reportSummary {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 12px;
  margin-top: 15px;
}

.summary-box {
  padding: 15px;
  border: 1px solid var(--edge);
  border-radius: 10px;
  background: #0d1424;
}

.summary-box small,
.summary-box strong {
  display: block;
}

.summary-box small {
  color: var(--mu);
  margin-bottom: 8px;
}

.summary-box strong {
  overflow-wrap: anywhere;
}

.modal {
  position: fixed;
  z-index: 10;
  inset: 0;
  display: grid;
  place-items: center;
  padding: 20px;
  background: #050914cc;
  backdrop-filter: blur(8px);
}

.modal[hidden] {
  display: none;
}

.modal-box {
  width: min(420px, 100%);
  margin: 0;
}

.modal-box .btn {
  margin-top: 10px;
}

.toast {
  position: fixed;
  z-index: 20;
  right: 20px;
  bottom: 20px;
  max-width: calc(100% - 40px);
  padding: 13px 17px;
  color: var(--tx);
  background: #131f2b;
  border: 1px solid #34d39955;
  border-radius: 10px;
  box-shadow: 0 10px 30px #0005;
  opacity: 0;
  transform: translateY(10px);
  pointer-events: none;
  transition: 0.2s;
}

.toast.show {
  opacity: 1;
  transform: translateY(0);
  pointer-events: auto;
}

.toast button {
  margin-left: 12px;
  color: var(--mint);
  background: transparent;
  border: 0;
  font-weight: 800;
}

footer {
  padding: 25px 15px 35px;
  text-align: center;
  color: var(--mu);
  font-size: 10px;
  letter-spacing: 1px;
  border-top: 1px solid #ffffff10;
}

.shake {
  animation: sh 0.3s;
}

@keyframes sh {
  25% { transform: translateX(-4px); }
  75% { transform: translateX(4px); }
}

@media (max-width: 850px) {
  .g2 {
    grid-template-columns: 1fr;
  }

  .topbar {
    padding: 12px 4%;
  }

  main {
    width: 94%;
  }
}

@media (max-width: 650px) {
  .topbar {
    align-items: flex-start;
    flex-direction: column;
    gap: 10px;
  }

  #tabs {
    width: 100%;
  }

  #tabs button {
    flex: 1;
    padding: 9px 5px;
    font-size: 12px;
  }

  .heading {
    align-items: stretch;
    flex-direction: column;
  }

  .month-control {
    width: 100%;
    max-width: 240px;
  }

  .cards {
    grid-template-columns: 1fr;
    gap: 0;
  }

  .form-grid,
  .filters,
  #reportSummary {
    grid-template-columns: 1fr;
  }

  .card {
    padding: 17px;
  }

  #categoryLegend {
    grid-template-columns: 1fr;
  }
}

@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation: none !important;
    transition: none !important;
  }
}
[28/10, 8:56 pm] Simra: 'use strict';

// ---------- HELPERS ----------

const $ = selector => document.querySelector(selector);

const ld = (key, fallback) => {
  try {
    const saved = localStorage.getItem(key);
    return saved === null ? fallback : JSON.parse(saved);
  } catch {
    return fallback;
  }
};

const sv = (key, value) => {
  try {
    localStorage.setItem(key, JSON.stringify(value));
    return true;
  } catch {
    toast('Unable to save data. Check browser storage.');
    return false;
  }
};

const money = amount => new Intl.NumberFormat('en-IN', {
  style: 'currency',
  currency: 'INR',
  maximumFractionDigits: 2
}).format(amount);

const localToday = () => {
  const d = new Date();
  d.setMinutes(d.getMinutes() - d.getTimezoneOffset());
  return d.toISOString().slice(0, 10);
};

const formatDate = date => {
  const d = new Date(date + 'T12:00:00');
  return Number.isNaN(d.getTime())
    ? date
    : d.toLocaleDateString('en-IN', {
        day: 'numeric',
        month: 'short',
        year: 'numeric'
      });
};

const escapeHTML = value => String(value).replace(/[&<>"']/g, ch => ({
  '&': '&amp;',
  '<': '&lt;',
  '>': '&gt;',
  '"': '&quot;',
  "'": '&#39;'
})[ch]);

const sum = (list, kind) =>
  list.filter(x => x.type === kind)
      .reduce((total, x) => total + x.amount, 0);

const inM = m => tx.filter(x => x.date.startsWith(m));

// ---------- DATA ----------

let tx = ld('ledgerly.tx', []);

if (!Array.isArray(tx)) tx = [];

tx = tx.filter(x =>
  x &&
  typeof x.id === 'string' &&
  typeof x.title === 'string' &&
  typeof x.date === 'string' &&
  Number.isFinite(Number(x.amount)) &&
  Number(x.amount) > 0 &&
  ['income', 'expense'].includes(x.type)
).map(x => ({
  ...x,
  amount: Math.round(Number(x.amount) * 100) / 100,
  category: typeof x.category === 'string' ? x.category : 'Other'
}));

let type = 'expense';
let uname = ld('ledgerly.name', '');
if (typeof uname !== 'string') uname = '';

let month = localToday().slice(0, 7);
let pend = null;
let donChart = null;
let flowChart = null;
let toastTimer = null;
let undoTimer = null;

const categories = {
  expense: [
    'Food & Dining',
    'Transport',
    'Shopping',
    'Bills & Utilities',
    'Education',
    'Health',
    'Entertainment',
    'Travel',
    'Other'
  ],
  income: [
    'Salary',
    'Business',
    'Freelance',
    'Allowance',
    'Investment',
    'Gift',
    'Other'
  ]
};

const palette = [
  '#6C7CFF',
  '#2DD4BF',
  '#FB7185',
  '#FBBF24',
  '#A78BFA',
  '#38BDF8',
  '#34D399',
  '#F97316',
  '#94A3B8'
];

// ---------- TOAST ----------

function toast(message, undoCallback = null) {
  const el = $('#toast');

  clearTimeout(toastTimer);
  clearTimeout(undoTimer);
  el.replaceChildren();

  const text = document.createElement('span');
  text.textContent = message;
  el.appendChild(text);

  if (undoCallback) {
    const button = document.createElement('button');
    button.type = 'button';
    button.textContent = 'UNDO';

    button.addEventListener('click', () => {
      clearTimeout(undoTimer);
      el.classList.remove('show');
      undoCallback();
    });

    el.appendChild(button);

    undoTimer = setTimeout(() => {
      el.classList.remove('show');
    }, 6500);
  } else {
    toastTimer = setTimeout(() => {
      el.classList.remove('show');
    }, 3000);
  }

  el.classList.add('show');
}

// ---------- NAVIGATION ----------

function showPage(name) {
  document.querySelectorAll('.page').forEach(page => {
    page.classList.toggle('active', page.id === name);
  });

  document.querySelectorAll('#tabs button').forEach(button => {
    button.classList.toggle('on', button.dataset.v === name);
  });

  if (name === 'reports') renderReports();

  window.scrollTo({ top: 0, behavior: 'smooth' });
}

$('#tabs').addEventListener('click', e => {
  const button = e.target.closest('button[data-v]');
  if (button) showPage(button.dataset.v);
});

// ---------- CATEGORY SELECTORS ----------

function fillCategories() {
  const select = $('#cat');
  const previous = select.value;

  select.innerHTML = categories[type].map(category =>
    `<option value="${escapeHTML(category)}">${escapeHTML(category)}</option>`
  ).join('');

  if (categories[type].includes(previous)) {
    select.value = previous;
  }
}

function fillFilterCategories() {
  const select = $('#filterCat');
  const previous = select.value;

  const all = [...new Set([
    ...categories.expense,
    ...categories.income,
    ...tx.map(x => x.category)
  ])];

  select.innerHTML =
    '<option value="all">All categories</option>' +
    all.map(category =>
      `<option value="${escapeHTML(category)}">${escapeHTML(category)}</option>`
    ).join('');

  if (all.includes(previous)) select.value = previous;
}

// ---------- INCOME / EXPENSE TOGGLE ----------

function setType(nextType) {
  type = nextType;

  $('#seg').classList.toggle('inc', type === 'income');

  document.querySelectorAll('#seg button').forEach(button => {
    button.classList.toggle('on', button.dataset.t === type);
  });

  fillCategories();
  $('#formError').textContent = '';
}

$('#seg').addEventListener('click', e => {
  const button = e.target.closest('button[data-t]');
  if (button) setType(button.dataset.t);
});

// ---------- PERSONALIZATION ----------

$('#wName').value = uname;

$('#wName').addEventListener('input', e => {
  uname = e.target.value.trim();
  sv('ledgerly.name', uname);

  const list = inM(month);
  welcome(sum(list, 'income'), sum(list, 'expense'));
});

function welcome(inc, exp) {
  const h = new Date().getHours();

  const greeting = h < 12
    ? 'Good morning'
    : h < 18
      ? 'Good afternoon'
      : 'Good evening';

  $('#wHi').textContent =
    greeting + (uname ? ', ' + uname : '') + '.';

  $('#wDate').textContent = new Date().toLocaleDateString('en-IN', {
    weekday: 'long',
    day: 'numeric',
    month: 'long',
    year: 'numeric'
  });

  const rate = inc > 0 ? Math.round(exp / inc * 100) : 0;
  const remaining = inc - exp;

  if (inc === 0 && exp === 0) {
    $('#wMsg').textContent = 'Start tracking your money today.';
  } else if (inc === 0) {
    $('#wMsg').textContent =
      'You have expenses recorded but no income this month.';
  } else {
    $('#wMsg').textContent =
      `You’ve spent ${rate}% of your income and have ${money(remaining)} left.`;
  }

  $('#wBar').style.width = Math.min(100, rate) + '%';
  $('#wRate').textContent = `${rate}% of monthly income spent`;

  $('#sRate').textContent =
    inc > 0 ? `${Math.round(remaining / inc * 100)}%` : '—';
}

// ---------- FORM ----------

$('#date').value = localToday();

function formError(message) {
  $('#formError').textContent = message;
  $('#form').classList.remove('shake');
  void $('#form').offsetWidth;
  $('#form').classList.add('shake');
}

$('#form').addEventListener('submit', e => {
  e.preventDefault();

  const amount = Number($('#amount').value);
  const title = $('#title').value.trim();
  const date = $('#date').value;
  const category = $('#cat').value;

  if (!Number.isFinite(amount) || amount <= 0) {
    return formError('Enter an amount greater than zero.');
  }

  if (!title) {
    return formError('Enter a transaction name.');
  }

  if (!date) {
    return formError('Select a transaction date.');
  }

  const parsedDate = new Date(date + 'T12:00:00');

  if (
    Number.isNaN(parsedDate.getTime()) ||
    parsedDate.toISOString().slice(0, 10) !== date
  ) {
    return formError('Select a valid date.');
  }

  const entry = {
    id: 't' + Date.now() + Math.random().toString(36).slice(2, 7),
    date,
    type,
    title,
    category,
    amount: Math.round(amount * 100) / 100
  };

  tx.push(entry);

  if (!sv('ledgerly.tx', tx)) {
    tx.pop();
    return formError('Unable to save transaction.');
  }

  month = date.slice(0, 7);
  $('#month').value = month;
  $('#reportMonth').value = month;

  $('#amount').value = '';
  $('#title').value = '';
  $('#date').value = localToday();
  $('#formError').textContent = '';

  render();
  toast('Transaction added successfully.');
});

$('#form').addEventListener('reset', () => {
  setTimeout(() => {
    $('#date').value = localToday();
    $('#formError').textContent = '';
  }, 0);
});

$('#qE').addEventListener('click', () => {
  showPage('dashboard');
  setType('expense');
  $('#amount').focus();
  $('#form').scrollIntoView({ behavior: 'smooth', block: 'center' });
});

// ---------- MONTH SELECTION ----------

$('#month').value = month;
$('#reportMonth').value = month;

$('#month').addEventListener('change', e => {
  if (!e.target.value) return;

  month = e.target.value;
  $('#reportMonth').value = month;
  render();
});

$('#reportMonth').addEventListener('change', e => {
  if (!e.target.value) return;

  month = e.target.value;
  $('#month').value = month;
  render();
});

// ---------- CHARTS ----------

function renderDonut(list) {
  const totals = {};

  list.filter(x => x.type === 'expense').forEach(x => {
    totals[x.category] = (totals[x.category] || 0) + x.amount;
  });

  const entries = Object.entries(totals).sort((a, b) => b[1] - a[1]);

  $('#chartEmpty').hidden = entries.length > 0;

  $('#categoryLegend').innerHTML = entries.map(([name, amount], i) => `
    <div class="legend-item">
      <span class="legend-dot"
            style="background:${palette[i % palette.length]}"></span>
      <span>${escapeHTML(name)}: ${money(amount)}</span>
    </div>
  `).join('');

  if (typeof Chart === 'undefined') return;

  if (donChart) donChart.destroy();

  donChart = new Chart($('#cDon'), {
    type: 'doughnut',
    data: {
      labels: entries.map(x => x[0]),
      datasets: [{
        data: entries.map(x => x[1]),
        backgroundColor: entries.map((_, i) =>
          palette[i % palette.length]
        ),
        borderColor: '#131A2A',
        borderWidth: 4,
        hoverOffset: 6
      }]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      cutout: '68%',
      plugins: {
        legend: { display: false },
        tooltip: {
          callbacks: {
            label: context =>
              `${context.label}: ${money(context.parsed)}`
          }
        }
      }
    }
  });
}

function renderFlowChart(selectedMonth) {
  if (typeof Chart === 'undefined') return;

  if (flowChart) flowChart.destroy();

  const [year, monthNumber] = selectedMonth.split('-').map(Number);
  const labels = [];
  const incomes = [];
  const expenses = [];

  for (let i = 5; i >= 0; i--) {
    const d = new Date(year, monthNumber - 1 - i, 1);

    const key = `${d.getFullYear()}-${String(d.getMonth() + 1).padStart(2, '0')}`;
    const list = inM(key);

    labels.push(d.toLocaleDateString('en-IN', {
      month: 'short',
      year: '2-digit'
    }));

    incomes.push(sum(list, 'income'));
    expenses.push(sum(list, 'expense'));
  }

  flowChart = new Chart($('#cFlow'), {
    type: 'bar',
    data: {
      labels,
      datasets: [
        {
          label: 'Income',
          data: incomes,
          backgroundColor: '#34D399',
          borderRadius: 5
        },
        {
          label: 'Expenses',
          data: expenses,
          backgroundColor: '#FB7185',
          borderRadius: 5
        }
      ]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      plugins: {
        legend: {
          labels: { color: '#E8ECF5' }
        },
        tooltip: {
          callbacks: {
            label: context =>
              `${context.dataset.label}: ${money(context.parsed.y)}`
          }
        }
      },
      scales: {
        x: {
          ticks: { color: '#94A3B8' },
          grid: { display: false }
        },
        y: {
          beginAtZero: true,
          ticks: {
            color: '#94A3B8',
            callback: value => '₹' + value
          },
          grid: { color: '#ffffff10' }
        }
      }
    }
  });
}

// ---------- DASHBOARD ----------

function render() {
  const list = inM(month);
  const inc = sum(list, 'income');
  const exp = sum(list, 'expense');

  $('#sBal').textContent =
    money(sum(tx, 'income') - sum(tx, 'expense'));

  $('#sInc').textContent = money(inc);
  $('#sExp').textContent = money(exp);

  welcome(inc, exp);
  renderDonut(list);
  renderRecent();
  renderTable();
  renderReports();
}

function renderRecent() {
  const list = [...tx]
    .sort((a, b) => b.date.localeCompare(a.date) || b.id.localeCompare(a.id))
    .slice(0, 5);

  $('#recentList').innerHTML = list.length
    ? list.map(x => `
      <div class="recent-item">
        <div class="recent-info">
          <strong>${escapeHTML(x.title)}</strong>
          <small>${escapeHTML(x.category)} · ${formatDate(x.date)}</small>
        </div>
        <span class="recent-amount ${x.type === 'income' ? 'positive' : 'negative'}">
          ${x.type === 'income' ? '+' : '−'}${money(x.amount)}
        </span>
      </div>
    `).join('')
    : '<p class="muted">No transactions yet.</p>';
}

// ---------- TRANSACTION TABLE ----------

function renderTable() {
  fillFilterCategories();

  $('#allInc').textContent = money(sum(tx, 'income'));
  $('#allExp').textContent = money(sum(tx, 'expense'));
  $('#txCount').textContent = tx.length;

  const query = $('#searchTx').value.trim().toLowerCase();
  const filterType = $('#filterType').value;
  const filterCat = $('#filterCat').value;

  const list = [...tx]
    .filter(x =>
      (x.title + ' ' + x.category).toLowerCase().includes(query) &&
      (filterType === 'all' || x.type === filterType) &&
      (filterCat === 'all' || x.category === filterCat)
    )
    .sort((a, b) => b.date.localeCompare(a.date) || b.id.localeCompare(a.id));

  $('#tbody').innerHTML = list.map(x => `
    <tr>
      <td>${escapeHTML(x.title)}</td>
      <td>${escapeHTML(x.category)}</td>
      <td>${formatDate(x.date)}</td>
      <td>
        <span class="type-badge ${x.type}">
          ${x.type === 'income' ? 'Income' : 'Expense'}
        </span>
      </td>
      <td class="${x.type === 'income' ? 'positive' : 'negative'}">
        ${x.type === 'income' ? '+' : '−'}${money(x.amount)}
      </td>
      <td>
        <button class="delete-btn" data-delete="${escapeHTML(x.id)}">
          Delete
        </button>
      </td>
    </tr>
  `).join('');

  $('#tableEmpty').hidden = list.length > 0;
  $('#tableCount').textContent =
    `Showing ${list.length} of ${tx.length} transactions`;
}

$('#searchTx').addEventListener('input', renderTable);
$('#filterType').addEventListener('change', renderTable);
$('#filterCat').addEventListener('change', renderTable);

// ---------- DELETE & UNDO ----------

$('#tbody').addEventListener('click', e => {
  const button = e.target.closest('[data-delete]');
  if (!button) return;

  pend = button.dataset.delete;
  $('#deleteModal').hidden = false;
  $('#dYes').focus();
});

function closeDeleteModal() {
  $('#deleteModal').hidden = true;
  pend = null;
}

$('#dNo').addEventListener('click', closeDeleteModal);

$('#deleteModal').addEventListener('click', e => {
  if (e.target === $('#deleteModal')) closeDeleteModal();
});

document.addEventListener('keydown', e => {
  if (e.key === 'Escape' && !$('#deleteModal').hidden) {
    closeDeleteModal();
  }
});

$('#dYes').addEventListener('click', () => {
  if (!pend) return;

  const index = tx.findIndex(x => x.id === pend);

  if (index === -1) {
    closeDeleteModal();
    return;
  }

  const [removed] = tx.splice(index, 1);

  if (!sv('ledgerly.tx', tx)) {
    tx.splice(index, 0, removed);
    closeDeleteModal();
    render();
    return;
  }

  closeDeleteModal();
  render();

  toast('Transaction deleted.', () => {
    if (tx.some(x => x.id === removed.id)) return;

    tx.push(removed);

    if (!sv('ledgerly.tx', tx)) {
      tx.pop();
      toast('Unable to restore transaction.');
      return;
    }

    render();
    toast('Transaction restored.');
  });
});

// ---------- REPORTS ----------

function renderReports() {
  const selectedMonth = $('#reportMonth').value || month;
  const list = inM(selectedMonth);

  const inc = sum(list, 'income');
  const exp = sum(list, 'expense');
  const net = inc - exp;

  $('#rInc').textContent = money(inc);
  $('#rExp').textContent = money(exp);
  $('#rNet').textContent = money(net);

  renderFlowChart(selectedMonth);

  const totals = {};

  list.filter(x => x.type === 'expense').forEach(x => {
    totals[x.category] = (totals[x.category] || 0) + x.amount;
  });

  const entries = Object.entries(totals).sort((a, b) => b[1] - a[1]);

  $('#reportCategories').innerHTML = entries.length
    ? entries.map(([name, amount]) => {
        const percentage = exp > 0 ? amount / exp * 100 : 0;

        return `
          <div class="report-category">
            <div class="report-top">
              <span>${escapeHTML(name)}</span>
              <span>${money(amount)} · ${Math.round(percentage)}%</span>
            </div>
            <div class="report-track">
              <span style="width:${percentage}%"></span>
            </div>
          </div>
        `;
      }).join('')
    : '<p class="muted">No expenses recorded for this month.</p>';

  const rate = inc > 0 ? Math.round(net / inc * 100) + '%' : 'N/A';

  $('#reportSummary').innerHTML = `
    <div class="summary-box">
      <small>NET CASH FLOW</small>
      <strong class="${net >= 0 ? 'positive' : 'negative'}">${money(net)}</strong>
    </div>
    <div class="summary-box">
      <small>SAVINGS RATE</small>
      <strong>${rate}</strong>
    </div>
    <div class="summary-box">
      <small>TRANSACTIONS</small>
      <strong>${list.length}</strong>
    </div>
  `;
}

// ---------- CSV EXPORT ----------

$('#exportBtn').addEventListener('click', () => {
  if (!tx.length) {
    toast('No transactions to export.');
    return;
  }

  const quote = value =>
    '"' + String(value).replace(/"/g, '""') + '"';

  const rows = [
    ['Date', 'Type', 'Title', 'Category', 'Amount (INR)'],
    ...tx.map(x => [
      x.date,
      x.type,
      x.title,
      x.category,
      x.amount.toFixed(2)
    ])
  ];

  const csv = '\uFEFF' +
    rows.map(row => row.map(quote).join(',')).join('\r\n');

  const blob = new Blob([csv], {
    type: 'text/csv;charset=utf-8;'
  });

  const url = URL.createObjectURL(blob);
  const link = document.createElement('a');

  link.href = url;
  link.download = `ledgerly-transactions-${localToday()}.csv`;
  document.body.appendChild(link);
  link.click();
  link.remove();

  setTimeout(() => URL.revokeObjectURL(url), 1000);
  toast('CSV file exported.');
});

// ---------- INITIALIZATION ----------

$('#month').value = month;
$('#reportMonth').value = month;

fillCategories();
fillFilterCategories();
render();
