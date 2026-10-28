[28/10, 6:48 pm] Simra: <nav id="tabs" aria-label="Main">
  <button data-v="dashboard" class="on">Dashboard</button>
  <button data-v="transactions">Transactions</button>
  <button data-v="reports">Reports</button>
</nav>
<div class="card hero">
  <h1 id="wHi">Welcome.</h1><p id="wDate"></p><p id="wMsg"></p>
  <div class="trk"><b id="wBar"></b></div>
  <input class="in" id="wName" placeholder="Your name">
  <button class="btn" id="qE">Add expense</button>
</div>
<form id="form" novalidate>
  <div class="seg" id="seg"><span class="pill"></span>
    <button type="button" data-t="expense" class="on">Expense</button>
    <button type="button" data-t="income">Income</button></div>
  <input class="in" id="amount" type="number" min="0" step="0.01">
  <input class="in" id="title" maxlength="60">
  <select class="in" id="cat"></select>
  <input class="in" id="date" type="date">
  <button class="btn" type="submit">Add transaction</button>
</form>
<canvas id="cDon"></canvas>   <!-- Chart.js doughnut -->
<table><tbody id="tbody"></tbody></table>   <!-- transaction history -->
[28/10, 6:48 pm] Simra: :root{--bg:#0B0F1A;--s1:#131A2A;--edge:#2A3550;--ind:#6C7CFF;--mint:#2DD4BF;
      --inc:#34D399;--exp:#FB7185;--tx:#E8ECF5;--mu:#94A3B8;color-scheme:dark}
body{background:radial-gradient(1200px 700px at 70% -10%,#17214a,var(--bg)) fixed;
     color:var(--tx);font:15px/1.5 Inter,system-ui,sans-serif}
#bg{position:fixed;inset:0;z-index:-1;pointer-events:none}     /* 3D canvas */
.nav{position:sticky;top:0;display:flex;height:64px;backdrop-filter:blur(14px)}
.card{background:rgba(19,26,42,.72);backdrop-filter:blur(14px);
      border:1px solid var(--edge);border-radius:16px;padding:20px}
.cards{display:grid;grid-template-columns:repeat(3,1fr);gap:16px}
.g2{display:grid;grid-template-columns:7fr 5fr;gap:16px}
.seg.inc .pill{transform:translateX(100%);background:var(--inc)}  /* toggle slide */
.shake{animation:sh .3s}
@keyframes sh{25%{transform:translateX(-4px)}75%{transform:translateX(4px)}}
@media(max-width:900px){.g2{grid-template-columns:1fr}}
@media(max-width:720px){#tabs{position:fixed;bottom:0;left:0;right:0}}   /* bottom tab bar */
@media(prefers-reduced-motion:reduce){*{animation:none!important}}
[28/10, 6:48 pm] Simra: let tx = ld('ledgerly.tx', null);                 // load saved transactions
const sv = (k,v) => localStorage.setItem(k, JSON.stringify(v));

$('#form').onsubmit = e => {                      // add a transaction
  e.preventDefault();
  const a = parseFloat($('#amount').value), t = $('#title').value.trim();
  if (!(a > 0) || !t) { /* show error + shake */ return; }
  tx.push({id:'t'+Date.now(), date:$('#date').value, type, title:t,
           category:$('#cat').value, amount:Math.round(a*100)/100});
  sv('ledgerly.tx', tx); toast('Transaction added'); render();
};

const sum = (l,t) => l.filter(x => x.type===t).reduce((a,x) => a+x.amount, 0);
const inM = m => tx.filter(x => x.date.startsWith(m));    // transactions of a month

function render(){
  const mt = inM(month), inc = sum(mt,'income'), exp = sum(mt,'expense');
  tween($('#sBal'), sum(tx,'income') - sum(tx,'expense'));  // balance
  tween($('#sInc'), inc);  tween($('#sExp'), exp);
  welcome(inc, exp);  renderTable();  /* charts + report also updated */
}

function welcome(inc, exp){
  const h = now.getHours();
  const g = h<12 ? 'Good morning' : h<18 ? 'Good afternoon' : 'Good evening';
  $('#wHi').textContent = g + (uname ? ', ' + uname : '') + '.';
  const r = inc ? Math.round(exp/inc*100) : 0;
  $('#wMsg').textContent = `You’ve spent ${r}% of your income and have ${money(inc-exp)} left.`;
  $('#wBar').style.width = Math.min(100, r) + '%';
}

$('#dYes').onclick = () => {                      // confirmed delete + undo
  const i = tx.findIndex(x => x.id === pend), [r] = tx.splice(i, 1);
  sv('ledgerly.tx', tx); render();
  toast('Transaction deleted', () => { tx.push(r); sv('ledgerly.tx', tx); render(); });
};
