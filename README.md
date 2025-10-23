# PRIME_SEGUS-CLICKER
yt prime_segus
[auto_clicker_pavel_matuska.html](https://github.com/user-attachments/files/23103673/auto_clicker_pavel_matuska.html)
<!doctype html>
<html lang="cs">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Auto Clicker - Klikací hra</title>
<style>
  :root{--bg:#0f1724;--card:#0b1220;--accent:#ffb703;--muted:#9aa6b2;--glass:rgba(255,255,255,0.03)}
  body{font-family:Inter,system-ui,Segoe UI,Roboto,Helvetica,Arial; background:linear-gradient(180deg,#071428 0%, #0f1724 100%); color:#e6eef6; margin:0; padding:20px}
  .wrap{max-width:1150px;margin:0 auto;display:grid;grid-template-columns:1fr 420px;gap:20px}
  header{grid-column:1/-1;display:flex;justify-content:space-between;align-items:center;margin-bottom:6px}
  h1{font-size:20px;margin:0}
  .panel{background:var(--card);border-radius:12px;padding:16px;box-shadow:0 6px 24px rgba(2,6,23,0.6);border:1px solid rgba(255,255,255,0.03)}
  .big-click{display:flex;flex-direction:column;align-items:center;justify-content:center;padding:28px;border-radius:12px;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));}
  .money{font-size:28px;font-weight:700;color:var(--accent)}
  .cps{color:var(--muted);margin-top:6px}
  button.click-btn{margin-top:18px;background:linear-gradient(180deg,#ff8a00,#ff6b00);border:none;color:#081225;padding:18px 22px;border-radius:12px;font-weight:700;font-size:20px;cursor:pointer;box-shadow:0 6px 18px rgba(255,107,0,0.18)}
  .shop{max-height:720px;overflow:auto;padding:8px;margin-top:12px;border-radius:8px;background:var(--glass)}
  .car-item{display:flex;align-items:center;justify-content:space-between;padding:10px;border-radius:8px;margin-bottom:8px;background:linear-gradient(180deg, rgba(255,255,255,0.01), rgba(255,255,255,0.00));border:1px solid rgba(255,255,255,0.02)}
  .left{display:flex;gap:12px;align-items:center}
  .badge{width:56px;height:40px;border-radius:8px;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));display:flex;align-items:center;justify-content:center;font-weight:700}
  .meta{font-size:14px}
  .price{font-weight:700;color:var(--accent)}
  .controls{display:flex;gap:8px;align-items:center}
  input[type=search]{width:100%;padding:10px;border-radius:10px;border:none;background:rgba(255,255,255,0.02);color:inherit}
  .top-stats{display:flex;gap:12px;align-items:center}
  .small{font-size:12px;color:var(--muted)}
  .owned{font-size:13px;color:#94f9b8;font-weight:700}
  .buy-btn{background:#0ea5a2;border:none;color:#001821;padding:8px 10px;border-radius:8px;cursor:pointer;font-weight:700}
  .disabled{opacity:0.45;pointer-events:none}
  .footer{grid-column:1/-1;text-align:center;color:var(--muted);margin-top:14px;font-size:13px}
  /* responsive */
  @media(max-width:980px){.wrap{grid-template-columns:1fr;}.shop{max-height:420px}}
</style>
</head>
<body>
<div class="wrap">
<header>
  <h1>Auto Clicker — klikni pro peníze</h1>
  <div class="top-stats small">
    <div>Hráč: <strong>Pavel</strong></div>
    <div id="version">Auta: <strong id="totalCars">500</strong></div>
  </div>
</header>

<section class="panel big-click">
  <div class="money" id="money">0 Kč</div>
  <div class="cps" id="cps">0 / sek</div>
  <button class="click-btn" id="clickBtn">🚗 Klikni!</button>
  <div style="width:100%;margin-top:16px;display:flex;gap:8px">
    <input id="search" type="search" placeholder="Hledat značku nebo název (např. Toyota, Model 12)"/>
    <select id="sort">
      <option value="price_asc">Nejnižší cena</option>
      <option value="price_desc">Nejvyšší cena</option>
      <option value="cps_desc">Nejvyšší CPS</option>
    </select>
  </div>

  <div class="panel" style="width:100%;margin-top:12px">
    <div style="display:flex;justify-content:space-between;align-items:center">
      <div class="small">Obchody</div>
      <div class="small">Filtrovat a kupovat pasivní příjem</div>
    </div>
    <div class="shop" id="shop"></div>
  </div>
</section>

<aside class="panel">
  <h3 style="margin-top:0">Rychlý přehled</h3>
  <div style="margin-top:8px">
    <div class="small">Klikací zisk na klik</div>
    <div style="font-weight:700;font-size:20px;margin-top:6px" id="perClick">1 Kč</div>
  </div>

  <div style="margin-top:12px">
    <div class="small">Dostupné upgrady</div>
    <div style="display:flex;gap:8px;margin-top:8px">
      <button class="buy-btn" id="upgradeClick">Zvýšit klik (+1 Kč) — cena: <span id="upgradeClickPrice">100</span> Kč</button>
    </div>
  </div>

  <div style="margin-top:12px">
    <div class="small">Rychlé ovládání</div>
    <div style="display:flex;gap:8px;margin-top:8px">
      <button class="buy-btn" id="sellAll">Prodat všechno (50% návrat)</button>
    </div>
  </div>

  <div style="margin-top:12px">
    <div class="small">Statistiky</div>
    <div style="margin-top:6px" class="meta">
      Vlastněno: <span class="owned" id="ownedCount">0</span><br/>
      Peníze utraceno: <span id="spent">0</span> Kč
    </div>
  </div>
</aside>

<footer class="footer">Vytvořil Pavel Matuška — hra pro zábavu. Použité názvy značek jsou skutečné, loga nejsou oficiální.</footer>
</div>

<script>
// --- Data: brands (real brands) and generated 500 cars ---
const brands = ["Toyota","Volkswagen","Ford","Honda","BMW","Mercedes-Benz","Audi","Hyundai","Nissan","Kia","Renault","Peugeot","Chevrolet","Mazda","Subaru","Volvo","Jaguar","Land Rover","Porsche","Ferrari","Lamborghini","Bentley","Rolls-Royce","Mitsubishi","Suzuki","Mini","Alfa Romeo","Citroen","Dacia","Tesla","Infiniti","Acura","Genesis","Saab","Skoda","Seat","Opel","Chrysler","Dodge","Jeep","GMC","Ram","Iveco","McLaren","Aston Martin","Pagani","Koenigsegg","Rivian","Lucid","Polestar","Mahindra","Tata","BYD"];
function generateCars(){
  const cars = [];
  let id = 1;
  for(let i=0;i<500;i++){
    const brand = brands[i % brands.length];
    const modelNum = Math.floor(i/brands.length)+1;
    const modelSuffix = [""," GT"," Sport"," S"," X"," Plus"," RS"," Turbo"," Hybrid"," EV"," R"][i % 11];
    const name = brand + " Model " + modelNum + modelSuffix;
    const base = 50 + i*12;
    const price = Math.round(base * Math.pow(1.035, i));
    const cps = Math.max(1, Math.round(price / 2500));
    cars.push({ id: id++, brand, name, price, cps, owned:0 });
  }
  return cars;
}
let cars = generateCars();
// --- Game state ---
let money = 0;
let perClick = 1;
let totalCPS = 0;
let spent = 0;
// --- UI helpers ---
const moneyEl = document.getElementById('money');
const cpsEl = document.getElementById('cps');
const perClickEl = document.getElementById('perClick');
const shopEl = document.getElementById('shop');
const ownedCountEl = document.getElementById('ownedCount');
const spentEl = document.getElementById('spent');
const totalCarsEl = document.getElementById('totalCars');
totalCarsEl.textContent = cars.length;
// format money
function fmt(n){
  if(n>=1e9) return (n/1e9).toFixed(2)+' G';
  if(n>=1e6) return (n/1e6).toFixed(2)+' M';
  if(n>=1e3) return (n/1e3).toFixed(2)+' k';
  return Math.round(n);
}
function updateUI(){
  moneyEl.textContent = fmt(money) + ' Kč';
  cpsEl.textContent = fmt(totalCPS) + ' / sek';
  perClickEl.textContent = fmt(perClick) + ' Kč';
  ownedCountEl.textContent = cars.reduce((s,c)=>s+c.owned,0);
  spentEl.textContent = fmt(spent);
  renderShop();
}
// render shop based on search & sort
function renderShop(){
  const q = document.getElementById('search').value.trim().toLowerCase();
  const sort = document.getElementById('sort').value;
  let list = cars.filter(c=> c.name.toLowerCase().includes(q) || c.brand.toLowerCase().includes(q));
  if(sort==='price_asc') list.sort((a,b)=>a.price-b.price);
  if(sort==='price_desc') list.sort((a,b)=>b.price-a.price);
  if(sort==='cps_desc') list.sort((a,b)=>b.cps-b.cps);
  shopEl.innerHTML = '';
  for(const c of list){
    const el = document.createElement('div'); el.className='car-item';
    el.innerHTML = `
      <div class="left">
        <div class="badge">${c.brand.split(' ')[0].slice(0,3).toUpperCase()}</div>
        <div>
          <div class="meta"><strong>${c.name}</strong></div>
          <div class="small">${c.brand} • CPS: ${c.cps}</div>
        </div>
      </div>
      <div class="controls">
        <div class="price">${fmt(c.price)} Kč</div>
        <button class="buy-btn" data-id="${c.id}">Koupit</button>
      </div>`;
    shopEl.appendChild(el);
  }
  // attach buy handlers
  shopEl.querySelectorAll('.buy-btn').forEach(b=> b.addEventListener('click',()=> buyCar(Number(b.dataset.id))));
}
// --- Actions ---
document.getElementById('clickBtn').addEventListener('click', ()=> {
  money += perClick;
  updateUI();
});
document.getElementById('search').addEventListener('input', renderShop);
document.getElementById('sort').addEventListener('change', renderShop);
function buyCar(id){
  const car = cars.find(x=>x.id===id);
  if(!car) return;
  if(money < car.price){ alert('Nedostatek peněz!'); return; }
  money -= car.price;
  car.owned += 1;
  spent += car.price;
  totalCPS += car.cps;
  updateUI();
}
// upgrade click
let upgradeClickPrice = 100;
document.getElementById('upgradeClickPrice').textContent = fmt(upgradeClickPrice);
document.getElementById('upgradeClick').addEventListener('click', ()=> {
  if(money < upgradeClickPrice){ alert('Potřebuješ víc peněz.'); return; }
  money -= upgradeClickPrice;
  perClick += 1;
  upgradeClickPrice = Math.round(upgradeClickPrice * 2.2);
  document.getElementById('upgradeClickPrice').textContent = fmt(upgradeClickPrice);
  updateUI();
});
// sell all
document.getElementById('sellAll').addEventListener('click', ()=> {
  const owned = cars.reduce((s,c)=>s+c.owned,0);
  if(owned===0){ alert('Nic k prodeji.'); return; }
  let refund = 0;
  cars.forEach(c=> { if(c.owned>0){ refund += c.price * c.owned * 0.5; totalCPS -= c.cps * c.owned; c.owned = 0; } });
  money += Math.floor(refund);
  updateUI();
});
// passive income tick
setInterval(()=> {
  money += totalCPS;
  updateUI();
}, 1000);
// autosave to localStorage
function save(){
  const state = { money, perClick, totalCPS, spent, cars };
  localStorage.setItem('auto_clicker_save', JSON.stringify(state));
}
function load(){
  const s = localStorage.getItem('auto_clicker_save');
  if(!s) return;
  try{
    const st = JSON.parse(s);
    money = st.money||money;
    perClick = st.perClick||perClick;
    totalCPS = st.totalCPS||totalCPS;
    spent = st.spent||spent;
    // merge owned counts
    if(st.cars && st.cars.length===cars.length){
      cars.forEach((c,i)=> c.owned = st.cars[i].owned || 0);
    }
  }catch(e){ console.warn('Load failed',e); }
}
window.addEventListener('beforeunload', save);
document.addEventListener('visibilitychange', ()=> { if(document.visibilityState==='hidden') save(); });
// keyboard shortcuts
document.addEventListener('keydown',(e)=>{
  if(e.key===' ') { e.preventDefault(); document.getElementById('clickBtn').click(); }
  if(e.key==='s' && (e.ctrlKey||e.metaKey)){ e.preventDefault(); save(); alert('Uloženo'); }
});
// initial
load();
updateUI();
</script>
</body>
</html>
