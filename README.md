<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Brick Bank Futuristic</title>
<style>
:root {
    --bg-dark: #0a0a14;
    --neon-orange: #ff6b00;
    --neon-green: #00ff9d;
    --neon-pink: #ff006e;
    --neon-purple: #9d4edd;
    --text-light: #e0e0e0;
    --card-bg: #151522;
    --glow-orange: 0 0 10px rgba(255,107,0,0.7);
    --glow-green: 0 0 10px rgba(0,255,157,0.7);
}

body {
    margin:0;
    font-family:sans-serif;
    background:var(--bg-dark);
    color:var(--text-light);
}

header {
    display:flex;
    justify-content:space-between;
    align-items:center;
    padding:10px;
    background:var(--card-bg);
    position: sticky;
    top:0;
    z-index:100;
}

header .logo {
    font-size:20px;
    font-weight:bold;
    color:var(--neon-orange);
}

nav button {
    background:none;
    border:none;
    color:var(--neon-green);
    font-weight:bold;
    margin-left:10px;
    cursor:pointer;
    font-size:14px;
}

nav button.active {
    color:var(--neon-orange);
}

.container {
    padding:10px;
}

/* Секции */
.section {
    display:none;
    margin-top:10px;
}

.section.active {
    display:block;
}

/* Карты */
.card-container {
    display:flex;
    flex-wrap:wrap;
    gap:10px;
}

.card {
    background:var(--card-bg);
    padding:15px;
    border-radius:12px;
    width:150px;
    text-align:center;
    box-shadow:var(--glow-orange);
    font-size:12px;
}

/* Баланс */
.balance-box {
    background:var(--card-bg);
    padding:10px;
    border-radius:12px;
    text-align:center;
    box-shadow:var(--glow-green);
    margin-bottom:10px;
    font-size:14px;
}

/* Кнопки */
.btn {
    padding:6px 12px;
    border-radius:8px;
    font-size:12px;
    font-weight:bold;
    cursor:pointer;
    margin-top:5px;
}

.btn-orange {background:var(--neon-orange); color:white; box-shadow:var(--glow-orange);}
.btn-green {background:var(--neon-green); color:black; box-shadow:var(--glow-green);}

/* История */
.history-item {
    background:rgba(255,255,255,0.05);
    padding:8px;
    border-radius:8px;
    margin-bottom:5px;
    font-size:12px;
}

/* Кликер */
.clicker-btn {
    width:80px;
    height:80px;
    border-radius:50%;
    background:var(--neon-purple);
    color:white;
    font-weight:bold;
    font-size:14px;
    display:flex;
    align-items:center;
    justify-content:center;
    margin:10px auto;
    box-shadow:0 0 10px rgba(157,78,221,0.7);
}

</style>
</head>
<body>

<header>
    <div class="logo">Brick Bank 🚀</div>
    <nav>
        <button class="tab-btn active" data-tab="balanceSection">Баланс</button>
        <button class="tab-btn" data-tab="cardsSection">Карты</button>
        <button class="tab-btn" data-tab="historySection">История</button>
        <button class="tab-btn" data-tab="clickerSection">Кликер</button>
        <button class="tab-btn" data-tab="transferSection">Переводы</button>
    </nav>
</header>

<div class="container">

    <!-- Баланс -->
    <div class="section active" id="balanceSection">
        <div class="balance-box" id="balanceDisplay">Баланс: ₽0</div>
        <button class="btn btn-orange" id="addMoneyBtn">Пополнить</button>
    </div>

    <!-- Карты -->
    <div class="section" id="cardsSection">
        <button class="btn btn-green" id="addCardBtn">Добавить карту</button>
        <div class="card-container" id="cardsContainer"></div>
    </div>

    <!-- История -->
    <div class="section" id="historySection">
        <div id="historyContainer"></div>
    </div>

    <!-- Кликер -->
    <div class="section" id="clickerSection">
        <div id="clickerCounter" style="text-align:center; font-size:16px; margin-bottom:5px;">0 ₽</div>
        <button class="clicker-btn" id="clickerBtn">Клик!</button>
    </div>

    <!-- Переводы -->
    <div class="section" id="transferSection">
        <button class="btn btn-orange" id="sendMoneyBtn">Сделать перевод</button>
        <div id="transferContainer"></div>
    </div>

</div>

<script>
// --- Tabs ---
const tabs = document.querySelectorAll('.tab-btn');
const sections = document.querySelectorAll('.section');
tabs.forEach(tab => {
    tab.addEventListener('click', ()=>{
        tabs.forEach(t=>t.classList.remove('active'));
        tab.classList.add('active');
        sections.forEach(s=>s.classList.remove('active'));
        document.getElementById(tab.dataset.tab).classList.add('active');
    });
});

// --- Баланс ---
let balance = 0;
const balanceDisplay = document.getElementById('balanceDisplay');
function updateBalance() {
    balanceDisplay.textContent = 'Баланс: ₽' + balance;
    clickerCounter.textContent = balance + ' ₽';
}
document.getElementById('addMoneyBtn').onclick = ()=>{
    const sum = parseInt(prompt('Сколько добавить?'));
    if(!isNaN(sum)){ balance += sum; updateBalance(); addHistory('Пополнение', sum); }
}

// --- Карты ---
const cardsContainer = document.getElementById('cardsContainer');
document.getElementById('addCardBtn').onclick = ()=>{
    const number = Math.floor(1000000000000000 + Math.random()*9000000000000000); // рандом
    const cardDiv = document.createElement('div');
    cardDiv.className='card';
    cardDiv.textContent='Карта: '+number;
    cardsContainer.appendChild(cardDiv);
}

// --- История ---
const historyContainer = document.getElementById('historyContainer');
function addHistory(type, amount){
    const div = document.createElement('div');
    div.className='history-item';
    const funnyTexts = [
        'Оплачено космическим бананом 🍌',
        'Скинул на чай маме ☕',
        'Перевёл другу на мороженое 🍦',
        'Заплатил невидимому баристе 👻',
        'Отправил рубли в будущее 🛸'
    ];
    const text = funnyTexts[Math.floor(Math.random()*funnyTexts.length)];
    div.textContent = `${type}: ₽${amount} — ${text}`;
    historyContainer.prepend(div);
}

// --- Кликер ---
const clickerBtn = document.getElementById('clickerBtn');
const clickerCounter = document.getElementById('clickerCounter');
clickerBtn.onclick = ()=>{
    balance +=1;
    updateBalance();
    addHistory('Клик',1);
}

// --- Переводы ---
const transferContainer = document.getElementById('transferContainer');
document.getElementById('sendMoneyBtn').onclick = ()=>{
    const sum = parseInt(prompt('Сколько перевести?'));
    if(!sum || sum>balance) return alert('Недостаточно средств!');
    balance -= sum;
    updateBalance();
    const div = document.createElement('div');
    div.className='history-item';
    const funnyTexts = [
        'Перевод на марсианский кошелёк 🪐',
        'Отправил на кофе в метавселенную ☕',
        'Подарил другу виртуальный кота 🐱'
    ];
    div.textContent = `Перевод: ₽${sum} — ${funnyTexts[Math.floor(Math.random()*funnyTexts.length)]}`;
    transferContainer.prepend(div);
}
</script>

</body>
</html>
