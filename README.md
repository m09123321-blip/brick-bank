/* =========================
   MOBILE (до 768px)
========================= */
@media (max-width: 768px) {

    /* Общие отступы */
    .container {
        padding: 0 12px;
    }

    /* Header */
    .header-content {
        flex-direction: column;
        gap: 15px;
    }

    .logo-text {
        font-size: 22px;
    }

    .nav-links {
        flex-wrap: wrap;
        justify-content: center;
        gap: 12px;
    }

    .auth-btn {
        width: 100%;
        max-width: 280px;
    }

    /* Основной layout */
    .main-layout {
        flex-direction: column;
        gap: 20px;
    }

    /* Sidebar -> сверху */
    .sidebar {
        width: 100%;
        position: relative;
        top: 0;
        height: auto;
    }

    .sidebar-nav {
        display: flex;
        overflow-x: auto;
        gap: 10px;
    }

    .nav-item {
        white-space: nowrap;
        margin-bottom: 0;
        padding: 10px 14px;
        font-size: 14px;
    }

    /* Hero */
    .hero h1 {
        font-size: 24px;
    }

    .hero p {
        font-size: 15px;
    }

    /* Баланс */
    .balance-amount {
        font-size: 22px;
    }

    /* Карты */
    .cards-grid {
        grid-template-columns: 1fr;
    }

    .virtual-card {
        height: auto;
        padding-bottom: 25px;
    }

    .card-number {
        font-size: 16px;
    }

    /* Профиль */
    .profile-header {
        flex-direction: column;
        text-align: center;
    }

    .profile-avatar {
        width: 80px;
        height: 80px;
    }

    .avatar-mask {
        width: 70px;
        height: 70px;
        font-size: 30px;
    }

    /* Таблицы → скролл */
    .transfers-history {
        overflow-x: auto;
    }

    .history-table {
        min-width: 600px;
    }

    /* Кликер */
    .clicker-btn {
        width: 120px;
        height: 120px;
        font-size: 18px;
    }

    .clicker-counter {
        font-size: 36px;
    }

    /* Кнопки */
    .btn {
        width: 100%;
    }
}

