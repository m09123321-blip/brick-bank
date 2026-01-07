<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Кирпич Банк - Виртуальный банк нового поколения</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Arial, sans-serif;
        }

        :root {
            --bg-dark: #0c1417;
            --dark-green: #1a3a2a;
            --moss-green: #2d5a3d;
            --sage-green: #4a7c5f;
            --soft-green: #6ba084;
            --light-green: #8bc0a7;
            --accent-green: #5d9b7b;
            --accent-gold: #c9a959;
            --text-light: #d4e6d4;
            --text-muted: #a0b8a0;
            --card-bg: #15231d;
            --input-bg: #1c2c24;
            --glow-green: 0 0 10px rgba(77, 175, 124, 0.3);
            --glow-gold: 0 0 10px rgba(201, 169, 89, 0.3);
        }

        body {
            background-color: var(--bg-dark);
            color: var(--text-light);
            overflow-x: hidden;
            background-image: 
                radial-gradient(circle at 10% 20%, rgba(26, 58, 42, 0.3) 0%, transparent 20%),
                radial-gradient(circle at 90% 80%, rgba(45, 90, 61, 0.3) 0%, transparent 20%);
            background-attachment: fixed;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        /* Header */
        header {
            padding: 15px 0;
            border-bottom: 1px solid var(--dark-green);
            position: sticky;
            top: 0;
            background-color: rgba(12, 20, 23, 0.95);
            backdrop-filter: blur(10px);
            z-index: 100;
        }

        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .logo-icon {
            width: 45px;
            height: 45px;
            background: linear-gradient(135deg, var(--dark-green), var(--accent-green));
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: var(--glow-green);
        }

        .logo-icon i {
            font-size: 22px;
            color: var(--light-green);
        }

        .logo-text {
            font-size: 24px;
            font-weight: 700;
            color: var(--light-green);
            letter-spacing: 0.5px;
        }

        .nav-links {
            display: flex;
            gap: 15px;
        }

        .nav-links a {
            color: var(--text-muted);
            text-decoration: none;
            font-weight: 500;
            transition: all 0.3s;
            padding: 6px 12px;
            border-radius: 6px;
            font-size: 13px;
        }

        .nav-links a:hover {
            color: var(--light-green);
            background: rgba(45, 90, 61, 0.2);
        }

        .nav-links a.active {
            color: var(--light-green);
            background: rgba(45, 90, 61, 0.3);
            border: 1px solid var(--moss-green);
        }

        .auth-btn {
            background: linear-gradient(135deg, var(--dark-green), var(--accent-green));
            color: var(--text-light);
            border: 1px solid var(--moss-green);
            padding: 8px 18px;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 13px;
        }

        .auth-btn:hover {
            background: linear-gradient(135deg, var(--moss-green), var(--accent-green));
            box-shadow: var(--glow-green);
        }

        /* Main Layout */
        .main-layout {
            display: flex;
            gap: 25px;
            margin-top: 25px;
        }

        .sidebar {
            width: 240px;
            flex-shrink: 0;
            position: sticky;
            top: 85px;
            height: calc(100vh - 110px);
            overflow-y: auto;
            padding-right: 10px;
        }

        .main-content {
            flex: 1;
            min-width: 0;
        }

        /* Sidebar Navigation */
        .sidebar-nav {
            background-color: var(--card-bg);
            border-radius: 10px;
            padding: 15px;
            border: 1px solid var(--dark-green);
        }

        .nav-item {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 10px 12px;
            color: var(--text-muted);
            text-decoration: none;
            border-radius: 8px;
            margin-bottom: 6px;
            transition: all 0.3s;
            cursor: pointer;
            border: 1px solid transparent;
        }

        .nav-item:hover {
            background-color: rgba(45, 90, 61, 0.2);
            color: var(--light-green);
            border-color: var(--moss-green);
        }

        .nav-item.active {
            background: linear-gradient(135deg, rgba(45, 90, 61, 0.3), rgba(77, 175, 124, 0.1));
            color: var(--light-green);
            border: 1px solid var(--moss-green);
        }

        .nav-item i {
            width: 18px;
            text-align: center;
            color: var(--accent-green);
        }

        /* Content Sections */
        .content-section {
            display: none;
            animation: fadeIn 0.4s ease;
        }

        .content-section.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Hero Section */
        .hero {
            padding: 30px 0;
            text-align: center;
        }

        .hero h1 {
            font-size: 32px;
            margin-bottom: 15px;
            color: var(--light-green);
            font-weight: 600;
        }

        .hero p {
            font-size: 16px;
            max-width: 700px;
            margin: 0 auto 25px;
            color: var(--text-muted);
            line-height: 1.5;
        }

        /* Balance Display */
        .balance-display {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
            gap: 15px;
            margin-bottom: 25px;
        }

        .balance-item {
            background-color: var(--card-bg);
            padding: 18px;
            border-radius: 10px;
            text-align: center;
            border: 1px solid var(--dark-green);
            transition: all 0.3s;
        }

        .balance-item:hover {
            border-color: var(--moss-green);
            box-shadow: var(--glow-green);
        }

        .balance-amount {
            font-size: 26px;
            font-weight: 600;
            margin: 8px 0;
        }

        .balance-amount.rub {
            color: var(--accent-green);
        }

        .balance-amount.crypto {
            color: var(--accent-gold);
        }

        /* Cards Section */
        .cards-section {
            margin-bottom: 25px;
        }

        .section-title {
            color: var(--light-green);
            margin-bottom: 15px;
            font-size: 20px;
            font-weight: 600;
        }

        .cards-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .virtual-card {
            width: 100%;
            height: 185px;
            background: linear-gradient(135deg, var(--dark-green), var(--card-bg));
            border-radius: 12px;
            padding: 18px;
            position: relative;
            overflow: hidden;
            border: 1px solid var(--moss-green);
            transition: all 0.4s;
            cursor: pointer;
        }

        .virtual-card:hover {
            transform: translateY(-3px);
            box-shadow: var(--glow-green);
        }

        .card-balance {
            position: absolute;
            top: 15px;
            right: 15px;
            background: rgba(26, 58, 42, 0.7);
            padding: 4px 10px;
            border-radius: 6px;
            font-weight: 600;
            color: var(--accent-green);
            font-size: 14px;
            border: 1px solid var(--moss-green);
        }

        .card-logo {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
        }

        .card-chip {
            width: 36px;
            height: 28px;
            background: linear-gradient(135deg, var(--accent-gold), #d4b672);
            border-radius: 5px;
            position: relative;
            overflow: hidden;
        }

        .card-number {
            font-family: 'Courier New', monospace;
            font-size: 18px;
            letter-spacing: 2px;
            margin-bottom: 20px;
            color: var(--text-light);
        }

        .card-details {
            display: flex;
            justify-content: space-between;
            font-size: 13px;
            color: var(--text-light);
        }

        .card-design {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-image: 
                radial-gradient(circle at 20% 80%, rgba(77, 175, 124, 0.1) 0%, transparent 50%),
                radial-gradient(circle at 80% 20%, rgba(45, 90, 61, 0.1) 0%, transparent 50%);
            z-index: -1;
        }

        .add-card-btn {
            background: rgba(45, 90, 61, 0.1);
            border: 2px dashed var(--moss-green);
            border-radius: 12px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            color: var(--accent-green);
            font-size: 40px;
            cursor: pointer;
            transition: all 0.3s;
        }

        .add-card-btn:hover {
            background: rgba(45, 90, 61, 0.2);
            border-color: var(--accent-green);
        }

        /* Profile Section */
        .profile-section {
            background-color: var(--card-bg);
            border-radius: 10px;
            padding: 25px;
            border: 1px solid var(--dark-green);
        }

        .profile-header {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 25px;
        }

        .profile-avatar {
            width: 90px;
            height: 90px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--dark-green), var(--accent-green));
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            border: 2px solid var(--moss-green);
        }

        .avatar-mask {
            width: 80px;
            height: 80px;
            background-color: var(--bg-dark);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 36px;
            color: var(--accent-green);
        }

        .profile-info {
            flex: 1;
        }

        .profile-name {
            font-size: 22px;
            color: var(--light-green);
            margin-bottom: 5px;
        }

        .profile-email {
            color: var(--text-muted);
            margin-bottom: 8px;
            font-size: 14px;
        }

        .profile-stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 15px;
            margin-top: 25px;
        }

        .stat-item {
            background: rgba(45, 90, 61, 0.1);
            padding: 12px;
            border-radius: 8px;
            text-align: center;
            border: 1px solid var(--dark-green);
        }

        .stat-value {
            font-size: 22px;
            font-weight: 600;
            color: var(--accent-green);
            margin: 6px 0;
        }

        /* Transfers History */
        .transfers-history {
            background-color: var(--card-bg);
            border-radius: 10px;
            padding: 20px;
            border: 1px solid var(--dark-green);
            margin-top: 25px;
        }

        .history-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 15px;
        }

        .history-table th {
            text-align: left;
            padding: 12px 10px;
            color: var(--accent-green);
            border-bottom: 1px solid var(--moss-green);
            font-weight: 600;
            font-size: 14px;
        }

        .history-table td {
            padding: 12px 10px;
            border-bottom: 1px solid rgba(160, 184, 160, 0.1);
            font-size: 14px;
        }

        .transfer-type {
            display: inline-block;
            padding: 3px 8px;
            border-radius: 4px;
            font-size: 11px;
            font-weight: 600;
        }

        .transfer-type.income {
            background: rgba(77, 175, 124, 0.1);
            color: var(--accent-green);
            border: 1px solid rgba(77, 175, 124, 0.3);
        }

        .transfer-type.outcome {
            background: rgba(201, 169, 89, 0.1);
            color: var(--accent-gold);
            border: 1px solid rgba(201, 169, 89, 0.3);
        }

        /* Top Users Section */
        .top-users {
            background-color: var(--card-bg);
            border-radius: 10px;
            padding: 20px;
            border: 1px solid var(--dark-green);
            margin-top: 25px;
        }

        .top-users-list {
            margin-top: 15px;
        }

        .top-user-item {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 12px;
            background: rgba(45, 90, 61, 0.1);
            border-radius: 8px;
            margin-bottom: 8px;
            transition: all 0.3s;
            border: 1px solid transparent;
        }

        .top-user-item:hover {
            background: rgba(45, 90, 61, 0.2);
            border-color: var(--moss-green);
        }

        .user-rank {
            width: 28px;
            height: 28px;
            background: linear-gradient(135deg, var(--dark-green), var(--accent-green));
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 600;
            color: var(--text-light);
            font-size: 13px;
        }

        .user-avatar {
            width: 36px;
            height: 36px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--dark-green), var(--accent-gold));
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--text-light);
        }

        .user-info {
            flex: 1;
        }

        .user-name {
            font-weight: 600;
            font-size: 14px;
        }

        .user-balance {
            color: var(--accent-green);
            font-weight: 600;
            font-size: 14px;
        }

        /* Clicker Game */
        .clicker-game {
            background-color: var(--card-bg);
            border-radius: 10px;
            padding: 25px;
            border: 1px solid var(--dark-green);
            text-align: center;
            margin-top: 25px;
        }

        .clicker-counter {
            font-size: 42px;
            margin-bottom: 25px;
            color: var(--accent-green);
            text-shadow: 0 0 5px rgba(77, 175, 124, 0.3);
        }

        .clicker-btn {
            width: 140px;
            height: 140px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--dark-green), var(--accent-green));
            border: 3px solid var(--moss-green);
            color: var(--text-light);
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            margin: 0 auto 25px;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.2s;
            box-shadow: var(--glow-green);
        }

        .clicker-btn:active {
            transform: scale(0.95);
            box-shadow: 0 0 20px rgba(77, 175, 124, 0.5);
        }

        .clicker-stats {
            display: flex;
            justify-content: space-around;
            margin-top: 25px;
        }

        /* Forms */
        .form-container {
            background-color: var(--card-bg);
            border-radius: 10px;
            padding: 25px;
            border: 1px solid var(--dark-green);
            margin-top: 25px;
        }

        .form-title {
            color: var(--light-green);
            margin-bottom: 15px;
            text-align: center;
            font-size: 20px;
            font-weight: 600;
        }

        .form-group {
            margin-bottom: 15px;
        }

        .form-group label {
            display: block;
            margin-bottom: 6px;
            color: var(--text-muted);
            font-size: 14px;
        }

        .form-control {
            width: 100%;
            padding: 10px 12px;
            background-color: var(--input-bg);
            border: 1px solid var(--dark-green);
            border-radius: 6px;
            color: var(--text-light);
            font-size: 14px;
            transition: all 0.3s;
        }

        .form-control:focus {
            outline: none;
            border-color: var(--accent-green);
            box-shadow: 0 0 0 2px rgba(77, 175, 124, 0.1);
        }

        .btn {
            padding: 10px 20px;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 14px;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            text-decoration: none;
            border: 1px solid transparent;
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--dark-green), var(--accent-green));
            color: var(--text-light);
            border-color: var(--moss-green);
        }

        .btn-secondary {
            background: transparent;
            color: var(--accent-green);
            border: 1px solid var(--moss-green);
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: var(--glow-green);
        }

        .btn-primary:hover {
            background: linear-gradient(135deg, var(--moss-green), var(--accent-green));
        }

        .btn-secondary:hover {
            background: rgba(45, 90, 61, 0.2);
        }

        /* Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(12, 20, 23, 0.9);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            backdrop-filter: blur(5px);
        }

        .modal-content {
            background-color: var(--card-bg);
            border-radius: 10px;
            padding: 25px;
            max-width: 450px;
            width: 90%;
            border: 1px solid var(--moss-green);
            box-shadow: var(--glow-green);
            position: relative;
        }

        .close-modal {
        
