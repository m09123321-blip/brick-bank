<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Кирпич Банк</title>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
<style>
:root {
    --bg-dark: #0a0a14;
    --neon-green: #00ff9d;
    --neon-purple: #9d4edd;
    --neon-pink: #ff006e;
    --neon-blue: #00d9ff;
    --neon-orange: #ff6b00;
    --text-light: #e0e0e0;
    --card-bg: #151522;
}

/* Общие стили */
body {
    margin: 0;
    font-family: 'Segoe UI', Arial, sans-serif;
    background-color: var(--bg-dark);
    color: var(--text-light);
}
.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
}

/* Заголовок */
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px 0;
    background-color: var(--card-bg);
}
.logo-text {
    font-size: 28px;
    font-weight: 800;
    background: linear-gradient(to right, var(--neon-orange), var(--neon-green));
    -webkit-background-clip: text;
    color: transparent;
}
.nav-links a {
    margin-left: 15px;
    text-decoration: none;
    color: var(--text-light);
}
.nav-links a:hover { color: var(--neon-orange); }
.auth-btn {
    background: linear-gradient(45deg, var(--neon-orange), var(--neon-green));
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 30px;
    cursor: pointer;
}

/* Основной контент */
.main-layout {
    display: flex;
    gap: 30px;
    margin-top: 30px;
}
.sidebar {
    width: 250px;
    background-color: var(--card-bg);
    border-radius: 15px;
    padding: 20px;
}
.nav-item {
    display: block;
    padding: 12px;
    border-radius: 10px;
    color: var(--text-light);
    margin-bottom: 8px;
    cursor: pointer;
}
.nav-item:hover { background-color: rgba(255,107,0,0.1); }

/* Основной контент справа */
.main-content {
    flex: 1;
}

/* Баланс */
.balance-item {
    background-color: var(--card-bg);
    padding: 20px;
    border-radius: 15px;
    margin-bottom: 20px;
    text-align: center;
}
.balance-amount.rub { color: var(--neon-orange); }
.balance-amount.crypto { color: var(--neon-purple); }

/* Карточки */
.virtual-card {
    background: linear-gradient(45deg, #1a1a2e, #16213e);
    border-radius: 20px;
    padding: 20px;
    margin-bottom: 20px;
    color: white;
}

/* Кнопки */
.btn-primary {
    background: linear-gradient(45deg, var(--neon-orange), var(--neon-green));
    color: white;
    border: none;
    padding: 12px 24px;
    border-radius: 30px;
    cursor: pointer;
}
.btn-primary:hover { opacity: 0.9; }

/* Модалки */
.modal {
    display: none;
    position: fixed;
    top:0; left:0; width:100%; height:100%;
    background: rgba(0,0,0,0.8);
    justify-content: center;
    align-items: center;
}
.modal-content {
    background-color: var(--card-bg);
    padding: 30px;
    border-radius: 15px;
}
</style>
</head>
<body>
<header class="container">
    <div class="logo-text">Кирпич Банк</div>
    <div class="nav-links">
        <a href="#">Главная</a>
        <a href="#">Баланс</a>
        <a href="#">Карты</a>
    </div>
    <button class="auth-btn">Войти</button>
</header>

<div class="container main-layout">
    <div class="sidebar">
        <div class="nav-item active"><i class="fa fa-home"></i> Главная</div>
        <div class="nav-item"><i class="fa fa-wallet"></i> Баланс</div>
        <div class="nav-item"><i class="fa fa-credit-card"></i> Карты</div>
    </div>
    <div class="main-content">
        <div class="balance-item">
            <div>Баланс Рублей</div>
            <div class="balance-amount rub">1000 ₽</div>
        </div>
        <div class="balance-item">
            <div>Баланс Crypto</div>
            <div class="balance-amount crypto">0.5 BTC</div>
        </div>

        <div class="virtual-card">
            <div>Виртуальная карта</div>
            <div>**** **** **** 1234</div>
        </div>
        <button class="btn-primary">Добавить карту</button>
    </div>
</div>
</body>
</html>
