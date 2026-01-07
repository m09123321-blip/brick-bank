<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Brick Bank</title>
<style>
    :root {
        --bg-dark: #0a0a14;
        --neon-purple: #9d4edd;
        --neon-green: #00ff9d;
        --neon-blue: #00d9ff;
        --text-light: #e0e0e0;
        --card-bg: #151522;
        --glow-purple: 0 0 15px rgba(157, 78, 221, 0.7);
        --glow-green: 0 0 15px rgba(0, 255, 157, 0.7);
    }
    * {margin:0; padding:0; box-sizing:border-box; font-family:sans-serif;}
    body {background:var(--bg-dark); color:var(--text-light);}
    header {padding:15px; text-align:center; font-size:24px; font-weight:bold; color:var(--neon-purple);}
    nav {display:flex; justify-content:center; gap:15px; margin-bottom:10px;}
    nav button {padding:8px 15px; border:none; border-radius:10px; cursor:pointer; font-weight:bold; background:rgba(157,78,221,0.3); color:var(--text-light);}
    nav button.active {background:linear-gradient(45deg, var(--neon-purple), var(--neon-green)); color:white;}
    .section {display:none; padding:20px;}
    .section.active {display:block;}
    .balance {font-size:28px; margin-bottom:20px; text-align:center;}
    .cards {display:flex; gap:15px; overflow-x:auto; margin-bottom:20px;}
    .card {min-width:200px; background:linear-gradient(45deg, rgba(157,78,221,0.5), rgba(0,255,157,0.5)); padding:15px; border-radius:15px; position:relative;}
    .card-number {font-family:monospace; font-size:16px; margin-bottom:10px;}
    .card-balance {font-weight:bold; font-size:20px; color:white;}
    .clicker {text-align:center; margin-bottom:20px;}
    .clicker button {padding:20px; border:none; border-radius:50%; font-size:20px; cursor:pointer; background:linear-gradient(45deg,var(--neon-purple),var(--neon-green)); color:white;}
    .transfer-form {max-width:400px; margin:auto; display:flex; flex-direction:column; gap:10px;}
    .transfer-form input, .transfer-form select {padding:10px; border-radius:10px; border:none; background:rgba(157,78,221,0.2); color:white;}
    .transfer-form button {padding:10px; border:none; border-radius:10px; background:linear-gradient(45deg,var(--neon-purple),var(--neon-green)); color:white; cursor:pointer;}
    .history {margin-top:20px;}
    .history-item {background:rgba(157,78,221,0.2); padding:10px; margin-bottom:5px; border-radius:8px;}
    .notification {position:fixed; top:20px; right:20px; background:linear-gradient(45deg,var(--neon-purple),var(--neon-green)); padding:10px 20px; border-radius:10px; color:white; display:none; z-index:100;}
</style>
</head>
<body>

<header>🧱 Brick Bank</header>

<nav>
    <button class="tab-btn active" data-tab="home">Главная</button>
    <button class="tab-btn" data-tab="clicker">Кликер</button>
    <button class="tab-btn" data-tab="transfer">Переводы</button>
    <button class="tab-btn" data-tab="profile">Личный кабинет</button>
</nav>

<div class="notification" id="notification">Баланс пополнен! 🧱</div>

<div id="home" class="section active">
    <div class="balance">Баланс: <span id="balance">0</span> 🧱</div>
    <div class="cards" id="cards">
        <!-- Карты будут генерироваться здесь -->
    </div>
</div>

<div id="clicker" class="section">
    <div class="clicker">
        <button id="clickerBtn">+1 🧱</button>
        <div>Баланс: <span id="clickerBalance">0</span> 🧱</div>
    </div>
</div>

<div id="transfer" class="section">
    <form class="transfer-form" id="transferForm">
        <select id="fromCard"></select>
        <select id="toCard"></select>
        <input type="number" id="transferAmount" placeholder="Сумма 🧱">
        <button type="submit">Перевести</button>
    </form>
    <div class="history" id="history"></div>
</div>

<div id="profile" class="section">
    <div class="balance">Ваш баланс: <span id="profileBalance">0</span> 🧱</div>
    <div class="cards" id="profileCards"></div>
</div>

<script>
let balance = 0;
let clickerBalance = 0;
let cards = [];
let history = [];

function createCard() {
    const number = '🧱' + Math.floor(1000 + Math.random()*9000);
    const card = {number: number, balance: 0};
    cards.push(card);
    updateCards();
}

function updateCards() {
    const cardsDiv = document.getElementById('cards');
    const profileCards = document.getElementById('profileCards');
    const fromCard = document.getElementById('fromCard');
    const toCard = document.getElementById('toCard');
    cardsDiv.innerHTML = '';
    profileCards.innerHTML = '';
    fromCard.innerHTML = '';
    toCard.innerHTML = '';
    cards.forEach((c, i) => {
        const div = document.createElement('div');
        div.className = 'card';
        div.innerHTML = `<div class="card-number">${c.number}</div><div class="card-balance">${c.balance} 🧱</div>`;
        cardsDiv.appendChild(div);

        const div2 = div.cloneNode(true);
        profileCards.appendChild(div2);

        const option1 = document.createElement('option'); option1.value=i; option1.text=c.number;
        const option2 = document.createElement('option'); option2.value=i; option2.text=c.number;
        fromCard.appendChild(option1);
        toCard.appendChild(option2);
    });
}

function showNotification(msg) {
    const notif = document.getElementById('notification');
    notif.innerText = msg;
    notif.style.display='block';
    setTimeout(()=>{notif.style.display='none';}, 2500);
}

document.getElementById('clickerBtn').addEventListener('click', ()=>{
    balance++;
    clickerBalance++;
    document.getElementById('balance').innerText=balance;
    document.getElementById('clickerBalance').innerText=clickerBalance;
    document.getElementById('profileBalance').innerText=balance;
    showNotification('Баланс пополнен на 1 🧱!');
});

document.getElementById('transferForm').addEventListener('submit', e=>{
    e.preventDefault();
    const from = +document.getElementById('fromCard').value;
    const to = +document.getElementById('toCard').value;
    const amount = +document.getElementById('transferAmount').value;
    if(from===to){alert('Нельзя перевести на ту же карту!'); return;}
    if(cards[from].balance<amount){alert('Недостаточно средств!'); return;}
    cards[from].balance -= amount;
    cards[to].balance += amount;
    history.push(`Перевод: ${amount} 🧱 с ${cards[from].number} на ${cards[to].number}`);
    updateCards();
    updateHistory();
    showNotification(`Перевод ${amount} 🧱 выполнен!`);
});

function updateHistory(){
    const histDiv = document.getElementById('history');
    histDiv.innerHTML='';
    history.slice().reverse().forEach(h=>{
        const div=document.createElement('div');
        div.className='history-item';
        div.innerText=h;
        histDiv.appendChild(div);
    });
}

// вкладки
document.querySelectorAll('.tab-btn').forEach(btn=>{
    btn.addEventListener('click', ()=>{
        document.querySelectorAll('.tab-btn').forEach(b=>b.classList.remove('active'));
        btn.classList.add('active');
        const tab = btn.dataset.tab;
        document.querySelectorAll('.section').forEach(sec=>sec.classList.remove('active'));
        document.getElementById(tab).classList.add('active');
    });
});

// Генерация первых карт
for(let i=0;i<3;i++){createCard();}
</script>

</body>
</html>
