# Rifrifancoin-
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rifrifancoin (RIFC) - Plataforma Mejorada</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&family=Montserrat:wght@400;500;600;700&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    
    <!-- Firebase SDK -->
    <script src="https://www.gstatic.com/firebasejs/9.22.2/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.2/firebase-auth-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.2/firebase-firestore-compat.js"></script>
    
    <style>
        :root {
            --primary: #0066cc; /* Azul amazigh más vibrante */
            --secondary: #4CAF50; /* Verde */
            --accent: #FFD700; /* Amarillo dorado */
            --dark-bg: #0a192f;
            --card-bg: #162a47;
            --light-card: #2c3e50;
            --text-light: #f1f5f9;
            --text-gray: #94a3b8;
            --success: #4caf50;
            --warning: #ff9800;
            --error: #f44336;
            --info: #2196f3;
            --radius: 14px;
            --shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
            --transition: all 0.3s ease;
            --amazigh-blue: #005f73; /* Azul amazigh profundo */
            --amazigh-yellow: #ffd700; /* Amarillo amazigh */
            --amazigh-green: #2a9d8f; /* Verde amazigh */
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Montserrat', 'Poppins', sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, var(--dark-bg) 0%, #0c1426 100%);
            color: var(--text-light);
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }
        
        /* Pantalla de autenticación */
        .auth-screen {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            padding: 20px;
            background: rgba(10, 25, 47, 0.95);
            z-index: 100;
            position: relative;
        }
        
        .auth-logo {
            margin-bottom: 40px;
            text-align: center;
            animation: fadeIn 1s ease;
        }
        
        .auth-logo h1 {
            font-size: 2.8rem;
            background: linear-gradient(135deg, var(--amazigh-blue), var(--amazigh-yellow));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 10px;
            letter-spacing: 1px;
            font-weight: 700;
        }
        
        .auth-logo p {
            color: var(--text-gray);
            font-size: 1.2rem;
            max-width: 500px;
        }
        
        .auth-card {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 30px;
            width: 100%;
            max-width: 480px;
            box-shadow: var(--shadow);
            border: 1px solid rgba(255, 255, 255, 0.08);
            animation: slideUp 0.5s ease;
        }
        
        .auth-tabs {
            display: flex;
            margin-bottom: 25px;
            background: rgba(0, 0, 0, 0.2);
            border-radius: 30px;
            padding: 5px;
        }
        
        .auth-tab {
            flex: 1;
            text-align: center;
            padding: 12px;
            cursor: pointer;
            border-radius: 30px;
            transition: var(--transition);
            font-weight: 500;
        }
        
        .auth-tab.active {
            background: linear-gradient(135deg, var(--amazigh-blue), var(--amazigh-yellow));
            color: white;
        }
        
        .auth-form {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }
        
        .input-group {
            position: relative;
        }
        
        .input-group i {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: var(--text-gray);
        }
        
        .form-input {
            width: 100%;
            padding: 16px 16px 16px 48px;
            background: rgba(0, 0, 0, 0.25);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 12px;
            color: var(--text-light);
            font-size: 1rem;
            transition: var(--transition);
        }
        
        .form-input:focus {
            outline: none;
            border-color: var(--amazigh-blue);
            box-shadow: 0 0 0 3px rgba(0, 102, 204, 0.3);
        }
        
        .auth-btn {
            background: linear-gradient(135deg, var(--amazigh-blue), var(--amazigh-yellow));
            color: white;
            border: none;
            padding: 16px;
            border-radius: 12px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            margin-top: 10px;
            position: relative;
            overflow: hidden;
            letter-spacing: 0.5px;
        }
        
        .auth-btn:hover {
            opacity: 0.9;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 102, 204, 0.4);
        }
        
        .auth-btn::after {
            content: '';
            position: absolute;
            top: -50%;
            left: -60%;
            width: 40px;
            height: 200%;
            background: rgba(255, 255, 255, 0.3);
            transform: rotate(25deg);
            transition: all 0.7s;
        }
        
        .auth-btn:hover::after {
            left: 120%;
        }
        
        .auth-links {
            text-align: center;
            margin-top: 20px;
            color: var(--text-gray);
        }
        
        .auth-links a {
            color: var(--text-light);
            text-decoration: none;
            transition: color 0.3s;
        }
        
        .auth-links a:hover {
            color: var(--amazigh-blue);
        }
        
        .google-auth-btn {
            background: #fff;
            color: #757575;
            border: none;
            padding: 16px;
            border-radius: 12px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            margin-top: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        
        .google-auth-btn:hover {
            background: #f5f5f5;
            transform: translateY(-2px);
        }
        
        /* Aplicación principal */
        .app-container {
            display: none;
            flex-direction: column;
            min-height: 100vh;
            max-width: 500px;
            margin: 0 auto;
            background: var(--dark-bg);
            position: relative;
            overflow-x: hidden;
            box-shadow: 0 0 30px rgba(0, 0, 0, 0.5);
        }
        
        .app-container.active {
            display: flex;
        }
        
        .app-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px;
            background: rgba(22, 42, 71, 0.95);
            backdrop-filter: blur(10px);
            z-index: 100;
            border-bottom: 1px solid rgba(255, 255, 255, 0.08);
        }
        
        .user-info {
            font-weight: 500;
            font-size: 1.1rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .user-info i {
            color: var(--amazigh-blue);
        }
        
        .header-actions {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .icon-btn {
            background: rgba(255, 255, 255, 0.1);
            border: none;
            width: 42px;
            height: 42px;
            border-radius: 50%;
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: var(--transition);
            font-size: 1.1rem;
        }
        
        .icon-btn:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: scale(1.05);
        }
        
        .icon-btn.active {
            background: rgba(0, 102, 204, 0.3);
        }
        
        .app-content {
            flex: 1;
            padding: 20px;
            overflow-y: auto;
            padding-bottom: 150px;
        }
        
        .content-section {
            display: none;
        }
        
        .content-section.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        @keyframes slideUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .section-title {
            font-size: 1.8rem;
            margin-bottom: 15px;
            background: linear-gradient(135deg, var(--amazigh-blue), var(--amazigh-yellow));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            position: relative;
            padding-bottom: 10px;
            font-weight: 700;
        }
        
        .section-title::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 50px;
            height: 4px;
            background: linear-gradient(135deg, var(--amazigh-blue), var(--amazigh-yellow));
            border-radius: 3px;
        }
        
        .card {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 20px;
            margin-bottom: 20px;
            box-shadow: var(--shadow);
            border: 1px solid rgba(255, 255, 255, 0.08);
            position: relative;
            overflow: hidden;
        }
        
        .mining-card {
            position: relative;
            overflow: hidden;
        }
        
        .mining-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 5px;
            background: linear-gradient(135deg, var(--amazigh-green), #2e7d32);
        }
        
        .mining-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .mining-status {
            background: rgba(255, 255, 255, 0.1);
            padding: 6px 16px;
            border-radius: 30px;
            font-size: 0.9rem;
            font-weight: 600;
        }
        
        .mining-status.active {
            background: rgba(76, 175, 80, 0.3);
            color: var(--amazigh-green);
            animation: pulse 1.5s infinite;
        }
        
        @keyframes pulse {
            0% { box-shadow: 0 0 0 0 rgba(76, 175, 80, 0.4); }
            70% { box-shadow: 0 0 0 10px rgba(76, 175, 80, 0); }
            100% { box-shadow: 0 0 0 0 rgba(76, 175, 80, 0); }
        }
        
        .mining-core {
            width: 150px;
            height: 150px;
            margin: 0 auto 20px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--amazigh-green), #2e9d8f);
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            box-shadow: 0 0 30px rgba(42, 157, 143, 0.4);
            transition: all 0.5s;
        }
        
        .mining-core.mining-active {
            animation: pulse-core 2s infinite;
        }
        
        @keyframes pulse-core {
            0% { box-shadow: 0 0 0 0 rgba(42, 157, 143, 0.4); }
            70% { box-shadow: 0 0 0 20px rgba(42, 157, 143, 0); }
            100% { box-shadow: 0 0 0 0 rgba(42, 157, 143, 0); }
        }
        
        .mining-core-inner {
            width: 70px;
            height: 70px;
            background: var(--card-bg);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2rem;
            color: var(--text-light);
        }
        
        .mining-stats {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin-bottom: 20px;
        }
        
        .stat-item {
            background: rgba(0, 0, 0, 0.2);
            border-radius: var(--radius);
            padding: 15px;
            text-align: center;
            transition: transform 0.3s;
        }
        
        .stat-item:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }
        
        .stat-label {
            color: var(--text-gray);
            font-size: 0.9rem;
            margin-bottom: 5px;
        }
        
        .stat-value {
            font-size: 1.5rem;
            font-weight: 600;
            color: var(--text-light);
        }
        
        .mining-btn {
            width: 100%;
            padding: 15px;
            border-radius: 12px;
            background: var(--amazigh-blue);
            border: none;
            color: white;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
            margin-top: 10px;
            position: relative;
            overflow: hidden;
        }
        
        .mining-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, var(--amazigh-green), #2e9d8f);
            opacity: 0;
            transition: opacity 0.3s;
        }
        
        .mining-btn:hover::before {
            opacity: 1;
        }
        
        .mining-btn span {
            position: relative;
            z-index: 1;
        }
        
        .mining-btn.mining-active {
            background: linear-gradient(135deg, var(--amazigh-green), #2e9d8f);
        }
        
        .mining-btn.mining-active:hover::before {
            transform: scale(1.05);
        }
        
        .mining-btn.disabled {
            background: rgba(255, 255, 255, 0.05);
            cursor: not-allowed;
        }
        
        .referral-card {
            text-align: center;
        }
        
        .referral-code {
            background: rgba(0, 0, 0, 0.2);
            padding: 15px;
            border-radius: var(--radius);
            font-size: 1.2rem;
            font-weight: 600;
            margin: 20px 0;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .copy-btn {
            background: rgba(255, 255, 255, 0.1);
            border: none;
            padding: 8px 15px;
            border-radius: 30px;
            color: white;
            cursor: pointer;
            transition: var(--transition);
        }
        
        .copy-btn:hover {
            background: rgba(255, 255, 255, 0.2);
        }
        
        .referral-stats {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 15px;
            margin: 20px 0;
        }
        
        .referrals-list {
            margin-top: 20px;
        }
        
        .referral-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 0;
            border-bottom: 1px solid rgba(255, 255, 255, 0.05);
        }
        
        .referral-info {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .referral-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--amazigh-blue), var(--amazigh-yellow));
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .referral-name {
            font-weight: 500;
        }
        
        .referral-bonus {
            background: rgba(76, 175, 80, 0.2);
            color: var(--amazigh-green);
            padding: 5px 10px;
            border-radius: 30px;
            font-size: 0.9rem;
        }
        
        .withdraw-btn {
            background: linear-gradient(135deg, var(--amazigh-green), #2e9d8f);
            color: white;
            border: none;
            padding: 15px;
            border-radius: 12px;
            font-size: 1.1rem;
            font-weight: 600;
            width: 100%;
            margin-top: 20px;
            margin-bottom: 20px;
            cursor: pointer;
            transition: var(--transition);
        }
        
        .withdraw-btn:hover {
            opacity: 0.9;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(42, 157, 143, 0.4);
        }
        
        /* Sección de Mensajes */
        .messages-card {
            text-align: center;
        }
        
        .messages-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        
        .messages-list {
            display: flex;
            flex-direction: column;
            gap: 12px;
            max-height: 300px;
            overflow-y: auto;
            padding-right: 5px;
            margin-bottom: 15px;
        }
        
        .message-item {
            background: var(--light-card);
            border-radius: var(--radius);
            padding: 15px;
            display: flex;
            align-items: flex-start;
            gap: 15px;
            border: 1px solid rgba(255, 255, 255, 0.08);
            transition: var(--transition);
        }
        
        .message-item:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }
        
        .message-item.unread {
            background: rgba(0, 102, 204, 0.15);
            border-left: 3px solid var(--amazigh-blue);
        }
        
        .message-icon {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--amazigh-blue), var(--amazigh-yellow));
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2rem;
        }
        
        .message-content {
            flex: 1;
            text-align: left;
        }
        
        .message-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 5px;
        }
        
        .message-sender {
            font-weight: 600;
        }
        
        .message-time {
            color: var(--text-gray);
            font-size: 0.8rem;
        }
        
        .message-subject {
            font-weight: 500;
            margin-bottom: 5px;
        }
        
        .message-text {
            color: var(--text-gray);
            font-size: 0.9rem;
        }
        
        .message-form {
            display: flex;
            flex-direction: column;
            gap: 10px;
            margin-top: 20px;
        }
        
        .message-input {
            background: rgba(0, 0, 0, 0.25);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 12px;
            color: var(--text-light);
            padding: 12px 15px;
            font-size: 1rem;
            min-height: 80px;
            resize: vertical;
        }
        
        .message-input:focus {
            outline: none;
            border-color: var(--amazigh-blue);
        }
        
        .send-message-btn {
            background: linear-gradient(135deg, var(--amazigh-blue), var(--amazigh-yellow));
            color: white;
            border: none;
            padding: 12px;
            border-radius: 12px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: var(--transition);
        }
        
        .send-message-btn:hover {
            opacity: 0.9;
            transform: translateY(-2px);
        }
        
        /* Modal de mensaje */
        .message-modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.7);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 2000;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s;
        }
        
        .message-modal.active {
            opacity: 1;
            visibility: visible;
        }
        
        .message-content-modal {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 30px;
            width: 90%;
            max-width: 500px;
            box-shadow: var(--shadow);
            transform: translateY(20px);
            transition: transform 0.3s;
            max-height: 90vh;
            overflow-y: auto;
        }
        
        .message-modal.active .message-content-modal {
            transform: translateY(0);
        }
        
        .message-header-modal {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .message-sender-modal {
            display: flex;
            align-items: center;
            gap: 12px;
        }
        
        .message-icon-modal {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--amazigh-blue), var(--amazigh-yellow));
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
        }
        
        .message-info-modal {
            display: flex;
            flex-direction: column;
        }
        
        .message-sender-name {
            font-weight: 600;
            font-size: 1.2rem;
        }
        
        .message-subject-modal {
            font-size: 1.1rem;
            margin: 20px 0;
            font-weight: 600;
        }
        
        .message-body-modal {
            line-height: 1.6;
            margin-bottom: 30px;
            color: var(--text-gray);
        }
        
        .message-actions {
            display: flex;
            gap: 10px;
            margin-top: 20px;
        }
        
        .message-action-btn {
            padding: 10px 20px;
            border-radius: 8px;
            border: none;
            cursor: pointer;
            font-weight: 500;
            transition: var(--transition);
        }
        
        .close-modal {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            color: var(--text-gray);
            font-size: 1.5rem;
            cursor: pointer;
        }
        
        /* Menú de usuario */
        .user-menu {
            position: fixed;
            top: 0;
            left: 0;
            width: 280px;
            height: 100%;
            background: var(--card-bg);
            z-index: 1000;
            transform: translateX(-100%);
            transition: transform 0.3s ease;
            padding: 20px;
            box-shadow: 5px 0 15px rgba(0, 0, 0, 0.3);
            overflow-y: auto;
        }
        
        .user-menu.active {
            transform: translateX(0);
        }
        
        .user-menu-header {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 30px;
            padding-bottom: 20px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .user-menu-avatar {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--amazigh-blue), var(--amazigh-yellow));
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.8rem;
        }
        
        .user-menu-info {
            flex: 1;
        }
        
        .user-menu-name {
            font-weight: 600;
            font-size: 1.2rem;
            margin-bottom: 5px;
        }
        
        .user-menu-email {
            color: var(--text-gray);
            font-size: 0.9rem;
        }
        
        .user-menu-close {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            color: var(--text-gray);
            font-size: 1.5rem;
            cursor: pointer;
        }
        
        .menu-section {
            margin-bottom: 25px;
        }
        
        .menu-title {
            color: var(--text-gray);
            font-size: 0.9rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 15px;
        }
        
        .menu-item {
            display: flex;
            align-items: center;
            gap: 12px;
            padding: 12px 15px;
            border-radius: 8px;
            margin-bottom: 8px;
            cursor: pointer;
            transition: var(--transition);
        }
        
        .menu-item:hover {
            background: rgba(255, 255, 255, 0.1);
        }
        
        .menu-item i {
            width: 24px;
            text-align: center;
            color: var(--text-gray);
        }
        
        .menu-item.active {
            background: rgba(0, 102, 204, 0.2);
        }
        
        .menu-item.active i {
            color: var(--amazigh-blue);
        }
        
        .menu-item-text {
            flex: 1;
        }
        
        .menu-badge {
            background: rgba(76, 175, 80, 0.2);
            color: var(--amazigh-green);
            padding: 3px 8px;
            border-radius: 30px;
            font-size: 0.8rem;
            font-weight: 600;
        }
        
        /* Barra de navegación */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: rgba(22, 42, 71, 0.95);
            backdrop-filter: blur(10px);
            display: flex;
            justify-content: space-around;
            padding: 15px 0;
            border-top: 1px solid rgba(255, 255, 255, 0.08);
            z-index: 100;
            max-width: 500px;
            margin: 0 auto;
        }
        
        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            text-decoration: none;
            color: var(--text-gray);
            font-size: 0.8rem;
            transition: var(--transition);
            padding: 5px 15px;
            border-radius: 20px;
        }
        
        .nav-item i {
            font-size: 1.3rem;
            margin-bottom: 5px;
        }
        
        .nav-item.active {
            color: white;
            background: rgba(0, 102, 204, 0.2);
        }
        
        .nav-item.active i {
            color: var(--amazigh-blue);
        }
        
        /* Modal de selección de idiomas */
        .language-modal {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.7);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s;
        }
        
        .language-modal.active {
            opacity: 1;
            visibility: visible;
        }
        
        .language-content {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 30px;
            width: 90%;
            max-width: 400px;
            text-align: center;
            box-shadow: var(--shadow);
            transform: translateY(20px);
            transition: transform 0.3s;
        }
        
        .language-modal.active .language-content {
            transform: translateY(0);
        }
        
        .language-title {
            font-size: 1.5rem;
            margin-bottom: 20px;
            color: white;
        }
        
        .language-options {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
        }
        
        .language-option {
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: var(--radius);
            padding: 15px;
            cursor: pointer;
            transition: var(--transition);
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        
        .language-option:hover {
            background: rgba(0, 102, 204, 0.2);
            border-color: var(--amazigh-blue);
        }
        
        .language-option.active {
            background: rgba(0, 102, 204, 0.3);
            border-color: var(--amazigh-blue);
        }
        
        .language-option i {
            font-size: 2rem;
            margin-bottom: 10px;
            color: var(--text-light);
        }
        
        .language-name {
            font-weight: 500;
        }
        
        /* Notificaciones */
        .notification-toast {
            position: fixed;
            top: 20px;
            right: 20px;
            background: var(--card-bg);
            color: white;
            padding: 15px 25px;
            border-radius: var(--radius);
            box-shadow: var(--shadow);
            border-left: 4px solid var(--amazigh-blue);
            transform: translateX(120%);
            transition: transform 0.3s;
            z-index: 1000;
            max-width: 350px;
        }
        
        .notification-toast.show {
            transform: translateX(0);
        }
        
        .notification-toast.success {
            border-left-color: var(--amazigh-green);
        }
        
        .notification-toast.warning {
            border-left-color: var(--warning);
        }
        
        .notification-toast.error {
            border-left-color: var(--error);
        }
        
        /* Animación de fondo */
        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            pointer-events: none;
        }
        
        .particle {
            position: absolute;
            width: 2px;
            height: 2px;
            background: rgba(42, 157, 143, 0.5);
            border-radius: 50%;
            animation: float 15s infinite linear;
        }
        
        @keyframes float {
            0% {
                transform: translateY(0) translateX(0);
                opacity: 0;
            }
            10% {
                opacity: 1;
            }
            90% {
                opacity: 1;
            }
            100% {
                transform: translateY(-100vh) translateX(100px);
                opacity: 0;
            }
        }
        
        /* Progress bar */
        .progress-container {
            margin: 20px 0;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            height: 10px;
            position: relative;
            overflow: hidden;
        }
        
        .progress-bar {
            height: 100%;
            background: linear-gradient(135deg, var(--amazigh-green), #2e9d8f);
            border-radius: 10px;
            width: 0%;
            transition: width 0.5s;
        }
        
        .progress-text {
            text-align: center;
            margin-top: 10px;
            font-size: 0.9rem;
            color: var(--text-gray);
        }
        
        /* Overlay para menú */
        .menu-overlay {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0, 0, 0, 0.5);
            z-index: 999;
            opacity: 0;
            visibility: hidden;
            transition: all 0.3s;
        }
        
        .menu-overlay.active {
            opacity: 1;
            visibility: visible;
        }
        
        /* Spinner de carga */
        .spinner {
            display: none;
            width: 40px;
            height: 40px;
            margin: 20px auto;
            border: 4px solid rgba(255, 255, 255, 0.1);
            border-radius: 50%;
            border-top-color: var(--amazigh-blue);
            animation: spin 1s ease-in-out infinite;
        }
        
        @keyframes spin {
            to { transform: rotate(360deg); }
        }
        
        /* Responsive */
        @media (max-width: 600px) {
            .mining-core {
                width: 120px;
                height: 120px;
            }
            
            .mining-core-inner {
                width: 60px;
                height: 60px;
            }
            
            .stat-value {
                font-size: 1.3rem;
            }
            
            .app-content {
                padding: 15px;
            }
            
            .card {
                padding: 15px;
            }
            
            .language-options {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .auth-logo h1 {
                font-size: 2.2rem;
            }
            
            .auth-logo p {
                font-size: 1rem;
            }
            
            .auth-card {
                padding: 20px;
            }
            
            .user-menu {
                width: 85%;
            }
        }
    </style>
</head>
<body>
    <!-- Fondo de partículas -->
    <div class="particles" id="particles"></div>
    
    <!-- Pantalla de autenticación -->
    <div id="authScreen" class="auth-screen">
        <div class="auth-logo">
            <h1>Rifrifancoin</h1>
            <p>Minería, referidos y mensajes para ganar RIFC</p>
        </div>
        
        <div class="auth-card">
            <div class="auth-tabs">
                <div class="auth-tab active" id="loginTab">Iniciar Sesión</div>
                <div class="auth-tab" id="registerTab">Registrarse</div>
            </div>
            
            <form class="auth-form" id="authForm">
                <div class="input-group">
                    <i class="fas fa-envelope"></i>
                    <input type="email" class="form-input" id="loginEmail" placeholder="Correo Electrónico" required>
                </div>
                
                <div class="input-group">
                    <i class="fas fa-lock"></i>
                    <input type="password" class="form-input" id="loginPassword" placeholder="Contraseña" required minlength="6">
                </div>
                
                <div id="registerFields" style="display: none;">
                    <div class="input-group">
                        <i class="fas fa-user"></i>
                        <input type="text" class="form-input" id="registerName" placeholder="Nombre Completo" required>
                    </div>
                    
                    <div class="input-group">
                        <i class="fas fa-lock"></i>
                        <input type="password" class="form-input" id="registerPassword" placeholder="Confirmar Contraseña" required minlength="6">
                    </div>
                    
                    <div class="input-group">
                        <i class="fas fa-user-friends"></i>
                        <input type="text" class="form-input" id="referralCodeInput" placeholder="Código de referido (opcional)">
                    </div>
                </div>
                
                <button type="submit" class="auth-btn" id="authSubmit">Iniciar Sesión</button>
                
                <button type="button" class="google-auth-btn" id="googleAuthBtn">
                    <i class="fab fa-google"></i>
                    Registrarse con Google
                </button>
                
                <div class="spinner" id="authSpinner"></div>
            </form>
            
            <div class="auth-links">
                <a href="#" id="forgotPassword">¿Olvidaste tu contraseña?</a>
            </div>
        </div>
    </div>
    
    <!-- Menú de usuario -->
    <div class="user-menu" id="userMenu">
        <button class="user-menu-close" id="closeUserMenu">
            <i class="fas fa-times"></i>
        </button>
        
        <div class="user-menu-header">
            <div class="user-menu-avatar">
                <i class="fas fa-user"></i>
            </div>
            <div class="user-menu-info">
                <div class="user-menu-name" id="userMenuName">Minero RIFC</div>
                <div class="user-menu-email" id="userMenuEmail">minero@rifrifancoin.com</div>
            </div>
        </div>
        
        <div class="menu-section">
            <div class="menu-title">Cuenta</div>
            
            <div class="menu-item" id="profileMenuItem">
                <i class="fas fa-user-cog"></i>
                <div class="menu-item-text">Perfil</div>
            </div>
            
            <div class="menu-item" id="securityMenuItem">
                <i class="fas fa-shield-alt"></i>
                <div class="menu-item-text">Seguridad</div>
            </div>
            
            <div class="menu-item" id="kycMenuItem">
                <i class="fas fa-id-card"></i>
                <div class="menu-item-text">Verificación KYC</div>
                <div class="menu-badge">Pendiente</div>
            </div>
        </div>
        
        <div class="menu-section">
            <div class="menu-title">Configuración</div>
            
            <div class="menu-item" id="notificationsMenuItem">
                <i class="fas fa-bell"></i>
                <div class="menu-item-text">Notificaciones</div>
            </div>
            
            <div class="menu-item" id="languageMenuItem">
                <i class="fas fa-globe"></i>
                <div class="menu-item-text">Idioma</div>
            </div>
            
            <div class="menu-item" id="privacyMenuItem">
                <i class="fas fa-lock"></i>
                <div class="menu-item-text">Privacidad</div>
            </div>
        </div>
        
        <div class="menu-section">
            <div class="menu-title">Soporte</div>
            
            <div class="menu-item" id="helpMenuItem">
                <i class="fas fa-question-circle"></i>
                <div class="menu-item-text">Ayuda</div>
            </div>
            
            <div class="menu-item" id="contactMenuItem">
                <i class="fas fa-headset"></i>
                <div class="menu-item-text">Contactar Soporte</div>
            </div>
            
            <div class="menu-item" id="aboutMenuItem">
                <i class="fas fa-info-circle"></i>
                <div class="menu-item-text">Acerca de</div>
            </div>
        </div>
        
        <div class="menu-item" id="logoutMenuItem" style="margin-top: 30px; background: rgba(244, 67, 54, 0.1);">
            <i class="fas fa-sign-out-alt" style="color: var(--error);"></i>
            <div class="menu-item-text" style="color: var(--error);">Cerrar Sesión</div>
        </div>
    </div>
    
    <!-- Overlay para menú -->
    <div class="menu-overlay" id="menuOverlay"></div>
    
    <!-- Aplicación principal -->
    <div id="appScreen" class="app-container">
        <!-- Barra superior -->
        <header class="app-header">
            <button id="userMenuBtn" class="icon-btn" style="margin-right: auto;">
                <i class="fas fa-bars"></i>
            </button>
            
            <div class="user-info" id="userGreeting">
                <i class="fas fa-user"></i>
                <span>Hola, Minero</span>
            </div>
            
            <div class="header-actions">
                <button id="languageBtn" class="icon-btn" title="Idioma">
                    <i class="fas fa-globe"></i>
                </button>
                <button id="notificationsToggleBtn" class="icon-btn" title="Notificaciones">
                    <i class="fas fa-bell"></i>
                </button>
            </div>
        </header>
        
        <!-- Contenido principal -->
        <main class="app-content">
            <!-- Sección de Minería -->
            <section id="miningSection" class="content-section active">
                <div class="mining-card card">
                    <div class="mining-header">
                        <h2 class="section-title">Minería RIFC</h2>
                        <div class="mining-status" id="miningStatus">INACTIVA</div>
                    </div>
                    
                    <div class="mining-core" id="miningCore">
                        <div class="mining-core-inner">
                            <i class="fas fa-microchip"></i>
                        </div>
                    </div>
                    
                    <div class="mining-stats">
                        <div class="stat-item">
                            <div class="stat-label">RIFC por ciclo</div>
                            <div class="stat-value" id="rifcPerCycle">10.0</div>
                        </div>
                        
                        <div class="stat-item">
                            <div class="stat-label">RIFC Minados</div>
                            <div class="stat-value" id="coinsMined">0.00</div>
                        </div>
                        
                        <div class="stat-item">
                            <div class="stat-label">Tiempo activo</div>
                            <div class="stat-value" id="miningTime">00:00:00</div>
                        </div>
                        
                        <div class="stat-item">
                            <div class="stat-label">Bonificación</div>
                            <div class="stat-value" id="bonusRate">0%</div>
                        </div>
                    </div>
                    
                    <div class="progress-container">
                        <div class="progress-bar" id="miningProgress"></div>
                        <div class="progress-text" id="progressText">Progreso: 0%</div>
                    </div>
                    
                    <button class="mining-btn" id="miningBtn">
                        <span>INICIAR MINERÍA</span>
                    </button>
                </div>
                
                <div class="card">
                    <h2 class="section-title">Estadísticas</h2>
                    <canvas id="miningChart" height="250"></canvas>
                </div>
            </section>
            
            <!-- Sección de Referidos -->
            <section id="referralsSection" class="content-section">
                <div class="referral-card card">
                    <h2 class="section-title">Programa de Referidos</h2>
                    <p id="referralDescription">Invita amigos y gana 5 RIFC por cada referido activo + 100 RIFC de bienvenida</p>
                    
                    <div class="referral-code">
                        <span id="referralCode">RIFC-5F8G9H</span>
                        <button class="copy-btn" id="copyRefBtn">
                            <i class="fas fa-copy"></i> Copiar
                        </button>
                    </div>
                    
                    <div class="referral-stats">
                        <div class="stat-item">
                            <div class="stat-label">Referidos</div>
                            <div class="stat-value" id="referralsCount">0</div>
                        </div>
                        
                        <div class="stat-item">
                            <div class="stat-label">Ganancia total</div>
                            <div class="stat-value" id="bonusEarned">0 RIFC</div>
                        </div>
                    </div>
                    
                    <h3 style="margin: 20px 0 10px; text-align: left;" id="referralsTitle">Tus referidos activos</h3>
                    
                    <div class="referrals-list" id="referralsList">
                        <!-- Los referidos se añadirán dinámicamente -->
                    </div>
                    
                    <button class="withdraw-btn" id="withdrawBtn">Retirar Fondos</button>
                </div>
            </section>
            
            <!-- Sección de Mensajes -->
            <section id="messagesSection" class="content-section">
                <div class="card">
                    <div class="messages-header">
                        <h2 class="section-title">Mensajes</h2>
                    </div>
                    
                    <div class="messages-list" id="messagesList">
                        <!-- Mensajes se añadirán dinámicamente -->
                    </div>
                    
                    <!-- Formulario para enviar mensajes -->
                    <div class="message-form">
                        <textarea class="message-input" id="messageInput" placeholder="Escribe tu mensaje..." required maxlength="500"></textarea>
                        <div style="text-align: right; font-size: 0.8rem; color: var(--text-gray);">
                            <span id="charCount">0</span>/500
                        </div>
                        <button class="send-message-btn" id="sendMessageBtn">
                            <i class="fas fa-paper-plane"></i> Enviar Mensaje
                        </button>
                    </div>
                </div>
            </section>
        </main>
        
        <!-- Barra de navegación inferior -->
        <nav class="bottom-nav">
            <a href="#" class="nav-item active" data-section="miningSection">
                <i class="fas fa-microchip"></i>
                <span>Minería</span>
            </a>
            
            <a href="#" class="nav-item" data-section="referralsSection">
                <i class="fas fa-user-friends"></i>
                <span>Referidos</span>
            </a>
            
            <a href="#" class="nav-item" data-section="messagesSection">
                <i class="fas fa-comments"></i>
                <span>Mensajes</span>
            </a>
        </nav>
    </div>
    
    <!-- Modal de selección de idiomas -->
    <div id="languageModal" class="language-modal">
        <div class="language-content">
            <button class="close-modal" id="closeLangModal">
                <i class="fas fa-times"></i>
            </button>
            
            <h2 class="language-title">Selecciona tu idioma</h2>
            
            <div class="language-options">
                <div class="language-option active" data-lang="es">
                    <i class="fas fa-language"></i>
                    <div class="language-name">Español</div>
                </div>
                
                <div class="language-option" data-lang="en">
                    <i class="fas fa-language"></i>
                    <div class="language-name">English</div>
                </div>
                
                <div class="language-option" data-lang="fr">
                    <i class="fas fa-language"></i>
                    <div class="language-name">Français</div>
                </div>
                
                <div class="language-option" data-lang="de">
                    <i class="fas fa-language"></i>
                    <div class="language-name">Deutsch</div>
                </div>
                
                <div class="language-option" data-lang="am-tif">
                    <i class="fas fa-language"></i>
                    <div class="language-name">ⵜⴰⵎⴰⵣⵉⵖⵜ (Tifinagh)</div>
                </div>
                
                <div class="language-option" data-lang="am-lat">
                    <i class="fas fa-language"></i>
                    <div class="language-name">Tamazight (Latino)</div>
                </div>
                
                <div class="language-option" data-lang="ar">
                    <i class="fas fa-language"></i>
                    <div class="language-name">العربية</div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Modal de mensaje -->
    <div id="messageModal" class="message-modal">
        <div class="message-content-modal">
            <button class="close-modal" id="closeMessageModal">
                <i class="fas fa-times"></i>
            </button>
            
            <div class="message-header-modal">
                <div class="message-sender-modal">
                    <div class="message-icon-modal">
                        <i class="fas fa-info-circle"></i>
                    </div>
                    <div class="message-info-modal">
                        <div class="message-sender-name">Soporte RIFC</div>
                        <div class="message-time">hace 2 horas</div>
                    </div>
                </div>
            </div>
            
            <div class="message-subject-modal">¡Bienvenido a Rifrifancoin!</div>
            
            <div class="message-body-modal">
                <p>Hola Minero,</p>
                <p>¡Bienvenido a nuestra plataforma de minería RIFC! Estamos encantados de tenerte con nosotros.</p>
                <p>Con Rifrifancoin puedes ganar tokens RIFC mediante:</p>
                <ul style="margin-left: 20px; margin-top: 10px; margin-bottom: 10px;">
                    <li>Minería continua en la plataforma (10 RIFC cada 4 horas)</li>
                    <li>Invitar amigos con tu código de referido (5 RIFC por referido + 100 RIFC de bienvenida)</li>
                    <li>Eventos especiales</li>
                </ul>
                <p>Para empezar, te recomendamos:</p>
                <ol style="margin-left: 20px; margin-top: 10px; margin-bottom: 10px;">
                    <li>Iniciar la minería en la sección principal</li>
                    <li>Compartir tu código de referido con amigos</li>
                </ol>
                <p>Si tienes alguna pregunta, no dudes en contactar con nuestro equipo de soporte.</p>
                <p>¡Feliz minería!</p>
                <p>El equipo de Rifrifancoin</p>
            </div>
            
            <div class="message-actions">
                <button class="message-action-btn" style="background: var(--amazigh-blue); color: white;">Responder</button>
                <button class="message-action-btn" style="background: rgba(255, 255, 255, 0.1); color: white;">Cerrar</button>
            </div>
        </div>
    </div>

    <div class="notification-toast" id="notificationToast"></div>

    <script>
        // Configuración de Firebase (reemplaza con tus credenciales)
        const firebaseConfig = {
            apiKey: "AIzaSyCeDj-KRjpVDiJ02aBkN0_yMNzldlDgkd4",
            authDomain: "rifrifancoin.firebaseapp.com",
            projectId: "rifrifancoin",
            storageBucket: "rifrifancoin.appspot.com",
            messagingSenderId: "614599675754",
            appId: "1:614599675754:web:1933d1aa458b3aab695f13"
        };
        
        // Inicializar Firebase
        firebase.initializeApp(firebaseConfig);
        const auth = firebase.auth();
        const db = firebase.firestore();
        
        document.addEventListener('DOMContentLoaded', function() {
            // Configuración de la minería
            const MINING_CYCLE_DURATION = 4 * 60 * 60 * 1000; // 4 horas en milisegundos
            const RIFC_PER_CYCLE = 10; // 10 RIFC por cada ciclo de 4 horas
            const REFERRAL_BONUS = 5; // 5 RIFC por cada referido activo
            const WELCOME_BONUS = 100; // 100 RIFC de bienvenida para referidos
            
            // Configuración de idiomas
            const translations = {
                'es': {
                    'greeting': 'Hola, Minero',
                    'mining': 'Minería',
                    'referrals': 'Referidos',
                    'messages': 'Mensajes',
                    'account': 'Cuenta',
                    'mining_title': 'Minería RIFC',
                    'mining_status': 'INACTIVA',
                    'mining_status_active': 'ACTIVA',
                    'start_mining': 'INICIAR MINERÍA',
                    'mining_in_progress': 'MINANDO...',
                    'rifc_per_cycle': 'RIFC por ciclo',
                    'coins_mined': 'RIFC Minados',
                    'mining_time': 'Tiempo activo',
                    'bonus_rate': 'Bonificación',
                    'referral_program': 'Programa de Referidos',
                    'referral_description': 'Invita amigos y gana 5 RIFC por cada referido activo + 100 RIFC de bienvenida',
                    'your_code': 'Tu código de referido:',
                    'copy': 'Copiar',
                    'referrals_count': 'Referidos',
                    'bonus_earned': 'Ganancia total',
                    'active_referrals': 'Tus referidos activos',
                    'withdraw': 'Retirar Fondos',
                    'messages_title': 'Mensajes',
                    'copied': 'Copiado al portapapeles',
                    'login_success': 'Sesión iniciada correctamente',
                    'mining_started': 'Minería iniciada',
                    'mining_stopped': 'Minería detenida',
                    'withdraw_notice': 'Función de retiro disponible próximamente',
                    'withdraw_minimum': 'Mínimo 10 RIFC para retirar',
                    'withdraw_processing': 'Procesando retiro...',
                    'withdraw_success': 'Retiro completado',
                    'login_button': 'Iniciar Sesión',
                    'register_button': 'Registrarse',
                    'mining_4h_active': 'Minería activa por 4 horas',
                    'mining_4h_complete': '¡Minería de 4 horas completada! +10 RIFC',
                    'mining_already_active': 'Ya tienes una sesión de minería activa',
                    'progress_label': 'Progreso',
                    'message_received': 'Nuevo mensaje recibido',
                    'no_messages': 'No tienes mensajes',
                    'notifications_off': 'Notificaciones desactivadas',
                    'notifications_on': 'Notificaciones activadas',
                    'google_login': 'Registrarse con Google',
                    'send_message': 'Enviar Mensaje',
                    'message_sent': 'Mensaje enviado correctamente',
                    'password_reset': 'Enlace para restablecer contraseña enviado',
                    'invalid_email': 'Por favor ingresa un email válido',
                    'short_password': 'La contraseña debe tener al menos 6 caracteres',
                    'password_mismatch': 'Las contraseñas no coinciden',
                    'name_required': 'Por favor ingresa tu nombre',
                    'referral_added': '¡Nuevo referido registrado! +5 RIFC',
                    'welcome_bonus': '¡Bienvenida de 100 RIFC por referido!'
                },
                'en': {
                    'greeting': 'Hello, Miner',
                    'mining': 'Mining',
                    'referrals': 'Referrals',
                    'messages': 'Messages',
                    'account': 'Account',
                    'mining_title': 'RIFC Mining',
                    'mining_status': 'INACTIVE',
                    'mining_status_active': 'ACTIVE',
                    'start_mining': 'START MINING',
                    'mining_in_progress': 'MINING...',
                    'rifc_per_cycle': 'RIFC per cycle',
                    'coins_mined': 'RIFC Mined',
                    'mining_time': 'Active time',
                    'bonus_rate': 'Bonus',
                    'referral_program': 'Referral Program',
                    'referral_description': 'Invite friends and earn 5 RIFC per active referral + 100 RIFC welcome bonus',
                    'your_code': 'Your referral code:',
                    'copy': 'Copy',
                    'referrals_count': 'Referrals',
                    'bonus_earned': 'Total earnings',
                    'active_referrals': 'Your active referrals',
                    'withdraw': 'Withdraw Funds',
                    'messages_title': 'Messages',
                    'copied': 'Copied to clipboard',
                    'login_success': 'Successfully logged in',
                    'mining_started': 'Mining started',
                    'mining_stopped': 'Mining stopped',
                    'withdraw_notice': 'Withdrawal feature coming soon',
                    'withdraw_minimum': 'Minimum 10 RIFC to withdraw',
                    'withdraw_processing': 'Processing withdrawal...',
                    'withdraw_success': 'Withdrawal completed',
                    'login_button': 'Log In',
                    'register_button': 'Register',
                    'mining_4h_active': 'Mining active for 4 hours',
                    'mining_4h_complete': '4-hour mining completed! +10 RIFC',
                    'mining_already_active': 'You already have an active mining session',
                    'progress_label': 'Progress',
                    'message_received': 'New message received',
                    'no_messages': 'You have no messages',
                    'notifications_off': 'Notifications disabled',
                    'notifications_on': 'Notifications enabled',
                    'google_login': 'Sign up with Google',
                    'send_message': 'Send Message',
                    'message_sent': 'Message sent successfully',
                    'password_reset': 'Password reset link sent',
                    'invalid_email': 'Please enter a valid email',
                    'short_password': 'Password must be at least 6 characters',
                    'password_mismatch': 'Passwords do not match',
                    'name_required': 'Please enter your name',
                    'referral_added': 'New referral registered! +5 RIFC',
                    'welcome_bonus': '100 RIFC welcome bonus for referral!'
                },
                'am-tif': {
                    'greeting': 'ⴰⵣⵓⵍ, ⴰⵎⵔⵔⴰⵙ',
                    'mining': 'ⴰⵎⵔⵔⴰⵙ',
                    'referrals': 'ⵉⵎⴰⵡⵍⴰⵏ',
                    'messages': 'ⵉⵙⵙⵉⵙⵏ',
                    'account': 'ⴰⵎⵖⵔⵉⴼ',
                    'mining_title': 'ⴰⵎⵔⵔⴰⵙ RIFC',
                    'mining_status': 'ⵓⵔ ⵜⵉⵍⵉⴷ',
                    'mining_status_active': 'ⵉⵜⵜⵉⵍⵉⴷ',
                    'start_mining': 'ⵙⵙⵓⵔⵙ ⴰⵎⵔⵔⴰⵙ',
                    'mining_in_progress': 'ⴰⵎⵔⵔⴰⵙ ⴷ...',
                    'rifc_per_cycle': 'RIFC ⵙ ⵜⴰⵙⵙⵓⵜⵜ',
                    'coins_mined': 'RIFC ⵉⵎⵔⵔⴰⵙⵏ',
                    'mining_time': 'ⴰⵎⵙ ⵏ ⵓⵔ ⵜⵉⵍⵉⴷ',
                    'bonus_rate': 'ⴰⴼⴰⵢⴷⴰ',
                    'referral_program': 'ⴰⵎⵓⴽⵍⴰ ⵏ ⵉⵎⴰⵡⵍⴰⵏ',
                    'referral_description': 'ⵢⴰⵜ ⵉⵎⴰⵡⵍ ⵉⵜⵜⵉⵍⵉⴷ ⵉⵣⵣⴰ 5 RIFC + 100 RIFC ⵏ ⵜⴰⵎⴰⵢⵏⵓⵜ',
                    'your_code': 'ⴰⵎⴰⵜⵜⴰⵢ ⵏⵏⵓⵏ ⵏ ⵉⵎⴰⵡⵍⴰⵏ:',
                    'copy': 'ⵙⵙⵓⴼⵍ',
                    'referrals_count': 'ⵉⵎⴰⵡⵍⴰⵏ',
                    'bonus_earned': 'ⴰⴼⴰⵢⴷⴰ ⵉⵎⵣⵣⴰⵢⵏ',
                    'active_referrals': 'ⵉⵎⴰⵡⵍⴰⵏ ⵏⵏⵓⵏ ⵉⵜⵜⵉⵍⵉⴷⵏ',
                    'withdraw': 'ⴰⵙⵖⵍ ⵉⴷⵔⴰⵔⵏ',
                    'messages_title': 'ⵉⵙⵙⵉⵙⵏ',
                    'copied': 'ⵜⵙⵙⵓⴼⵍⴷ ⵙ ⵜⴰⵙⵓⵜⵜ',
                    'login_success': 'ⵜⵓⵎⵎⵉⴷ ⴷ ⵜⵓⵙⵙⵏⴰ ⴰⵎⵖⵔⵉⴼ',
                    'mining_started': 'ⵓⵔ ⵢⵏⵏⴰ ⴰⵎⵔⵔⴰⵙ',
                    'mining_stopped': 'ⵓⵔ ⵢⵏⵏⴰ ⴰⵎⵔⵔⴰⵙ',
                    'withdraw_notice': 'ⵜⴰⵎⵓⵙⵙⴰ ⵏ ⵓⵙⵖⵍ ⵏ ⵉⴷⵔⴰⵔⵏ ⴰⵔ ⵜⵉⵜ ⵙ ⵓⵙⵙⵉ',
                    'withdraw_minimum': 'ⴰⴷⴷⵓⵔ ⵏ 10 RIFC ⴰⴼⴰⴷ ⵙⵙⵖⵍⵏ',
                    'withdraw_processing': 'ⴰⵔ ⵉⵙⵙⵖⵍⵏ...',
                    'withdraw_success': 'ⵓⵔ ⵢⵏⵏⴰ ⵓⵙⵖⵍ ⵏ ⵉⴷⵔⴰⵔⵏ',
                    'login_button': 'ⴽⵛⵎ ⴰⵎⵖⵔⵉⴼ',
                    'register_button': 'ⴰⵏⵎⴰⵙ',
                    'mining_4h_active': 'ⴰⵎⵔⵔⴰⵙ ⵉⵜⵜⵉⵍⵉⴷ ⴷ 4 ⵉⵙⵙⵉⴳⴰⵙⵏ',
                    'mining_4h_complete': 'ⴰⵎⵔⵔⴰⵙ ⵏ 4 ⵉⵙⵙⵉⴳⴰⵙⵏ ⵓⵔ ⵢⵏⵏⴰ! +10 RIFC',
                    'mining_already_active': 'ⵢⴰ ⵜⵙⵙⵏⴷ ⵜⴰⵎⵔⵔⴰⵙⵜ ⵏⵏⵓⵏ ⵉⵜⵜⵉⵍⵉⴷ',
                    'progress_label': 'ⴰⵙⵖⵓⵔ',
                    'message_received': 'ⵜⴰⵎⵙⵙⴰⵏⵜ ⵜⴰⵎⴰⵢⵏⵓⵜ ⵜⵓⵎⵎⵉⴷ',
                    'no_messages': 'ⵓⵔ ⵜⵙⵙⵏⴷ ⵉⵙⵙⵉⵙⵏ ⵏⵏⵓⵏ',
                    'notifications_off': 'ⵉⵙⵙⵉⵏⴰⵢⵏ ⵓⵔ ⵜⵉⵍⵉⴷⵏ',
                    'notifications_on': 'ⵉⵙⵙⵉⵏⴰⵢⵏ ⵉⵜⵜⵉⵍⵉⴷⵏ',
                    'google_login': 'ⴰⵏⵎⴰⵙ ⵙ Google',
                    'send_message': 'ⴰⵣⵏ ⵜⴰⵎⵙⵙⴰⵏⵜ',
                    'message_sent': 'ⵜⴰⵎⵙⵙⴰⵏⵜ ⵜⵓⵎⵎⵉⴷ ⴷ ⵜⵓⵙⵙⵏⴰ',
                    'password_reset': 'ⴰⵙⵇⵍ ⵏ ⵓⵙⵉⵏⵉⵏ ⵏ ⵜⴰⵎⵓⵙⵙⴰ ⵜⵓⵎⵎⵉⴷ',
                    'invalid_email': 'ⵜⴰⵙⵙⵓⵜⴷ ⵜⴰⵎⴰⵢⵍ ⵜⴰⵎⴰⵜⵜⴰⵢ',
                    'short_password': 'ⵜⴰⵎⵓⵙⵙⴰ ⵉⵍⴰ ⵜⵉⵍⵉ ⴷ 6 ⵉⵙⴽⴽⵉⵍⵏ',
                    'password_mismatch': 'ⵜⵉⵎⵓⵙⵙⴰⵡⵉⵏ ⵓⵔ ⵜⵎⵉⵍⴰⵏ',
                    'name_required': 'ⵜⴰⵙⵙⵓⵜⴷ ⵜⴰⵙⵏⴰ ⵏⵏⵓⵏ',
                    'referral_added': 'ⵉⵎⴰⵡⵍ ⴰⵎⴰⵢⵏⵓⵜ ⵓⵔ ⵢⵏⵏⴰ! +5 RIFC',
                    'welcome_bonus': '100 RIFC ⵏ ⵜⴰⵎⴰⵢⵏⵓⵜ ⵉⵎⴰⵡⵍⴰⵏ!'
                },
                'am-lat': {
                    'greeting': 'Azul, Amrras',
                    'mining': 'Amrras',
                    'referrals': 'Imawlan',
                    'messages': 'Issisn',
                    'account': 'Amghrif',
                    'mining_title': 'Amrras RIFC',
                    'mining_status': 'Ur tilid',
                    'mining_status_active': 'Ittilid',
                    'start_mining': 'Ssurs amrras',
                    'mining_in_progress': 'Amrras d...',
                    'rifc_per_cycle': 'RIFC s tassutt',
                    'coins_mined': 'RIFC imrrasn',
                    'mining_time': 'Ams n ur tilid',
                    'bonus_rate': 'Afayda',
                    'referral_program': 'Amukla n imawlan',
                    'referral_description': 'Yat imawl ittilid izza 5 RIFC + 100 RIFC n tamaynout',
                    'your_code': 'Amattay nnn n imawlan:',
                    'copy': 'Ssufl',
                    'referrals_count': 'Imawlan',
                    'bonus_earned': 'Afayda imzzayn',
                    'active_referrals': 'Imawlan nnn ittilidn',
                    'withdraw': 'Asghl idrarn',
                    'messages_title': 'Issisn',
                    'copied': 'Tssufld s tasutt',
                    'login_success': 'Tummid d tussna amghrif',
                    'mining_started': 'Ur yenna amrras',
                    'mining_stopped': 'Ur yenna amrras',
                    'withdraw_notice': 'Tamussa n usghl n idrarn ar tit s ussi',
                    'withdraw_minimum': 'Addur n 10 RIFC afad ssghln',
                    'withdraw_processing': 'Ar issghln...',
                    'withdraw_success': 'Ur yenna usghl n idrarn',
                    'login_button': 'Kcm amghrif',
                    'register_button': 'Anmas',
                    'mining_4h_active': 'Amrras ittilid d 4 issignasn',
                    'mining_4h_complete': 'Amrras n 4 issignasn ur yenna! +10 RIFC',
                    'mining_already_active': 'Ya tssnd tamrrast nnn ittilid',
                    'progress_label': 'Asghur',
                    'message_received': 'Tamssant tamaynout tummid',
                    'no_messages': 'Ur tssnd issisn nnn',
                    'notifications_off': 'Issinayn ur tilidn',
                    'notifications_on': 'Issinayn ittilidn',
                    'google_login': 'Anmas s Google',
                    'send_message': 'Azn tamssant',
                    'message_sent': 'Tamssant tummid d tussna',
                    'password_reset': 'Asql n usinin n tamussa tummid',
                    'invalid_email': 'Tassutd tamayl tamattay',
                    'short_password': 'Tamussa ila tilid d 6 iskkiln',
                    'password_mismatch': 'Timussawin ur tmilant',
                    'name_required': 'Tassutd tasna nnn',
                    'referral_added': 'Imawl amaynout ur yenna! +5 RIFC',
                    'welcome_bonus': '100 RIFC n tamaynout imawlan!'
                },
                'ar': {
                    'greeting': 'مرحبا، عامل المناجم',
                    'mining': 'التعدين',
                    'referrals': 'الإحالات',
                    'messages': 'الرسائل',
                    'account': 'الحساب',
                    'mining_title': 'تعدين RIFC',
                    'mining_status': 'غير نشط',
                    'mining_status_active': 'نشط',
                    'start_mining': 'بدء التعدين',
                    'mining_in_progress': 'جاري التعدين...',
                    'rifc_per_cycle': 'RIFC لكل دورة',
                    'coins_mined': 'RIFC المستخرجة',
                    'mining_time': 'الوقت النشط',
                    'bonus_rate': 'المكافأة',
                    'referral_program': 'برنامج الإحالة',
                    'referral_description': 'قم بدعوة الأصدقاء واكسب 5 RIFC لكل إحالة نشطة + 100 RIFC مكافأة ترحيبية',
                    'your_code': 'رمز الإحالة الخاص بك:',
                    'copy': 'نسخ',
                    'referrals_count': 'الإحالات',
                    'bonus_earned': 'إجمالي الأرباح',
                    'active_referrals': 'إحالاتك النشطة',
                    'withdraw': 'سحب الأموال',
                    'messages_title': 'الرسائل',
                    'copied': 'تم النسخ إلى الحافظة',
                    'login_success': 'تم تسجيل الدخول بنجاح',
                    'mining_started': 'بدأ التعدين',
                    'mining_stopped': 'توقف التعدين',
                    'withdraw_notice': 'ميزة السحب قريبا',
                    'withdraw_minimum': 'الحد الأدنى للسحب 10 RIFC',
                    'withdraw_processing': 'جاري معالجة السحب...',
                    'withdraw_success': 'تم السحب بنجاح',
                    'login_button': 'تسجيل الدخول',
                    'register_button': 'تسجيل',
                    'mining_4h_active': 'التعدين نشط لمدة 4 ساعات',
                    'mining_4h_complete': 'اكتمل التعدين لمدة 4 ساعات! +10 RIFC',
                    'mining_already_active': 'لديك بالفعل جلسة تعدين نشطة',
                    'progress_label': 'التقدم',
                    'message_received': 'تم استلام رسالة جديدة',
                    'no_messages': 'ليس لديك رسائل',
                    'notifications_off': 'الإشعارات معطلة',
                    'notifications_on': 'الإشعارات مفعلة',
                    'google_login': 'التسجيل عبر جوجل',
                    'send_message': 'إرسال رسالة',
                    'message_sent': 'تم إرسال الرسالة بنجاح',
                    'password_reset': 'تم إرسال رابط إعادة تعيين كلمة المرور',
                    'invalid_email': 'الرجاء إدخال بريد إلكتروني صحيح',
                    'short_password': 'يجب أن تتكون كلمة المرور من 6 أحرف على الأقل',
                    'password_mismatch': 'كلمات المرور غير متطابقة',
                    'name_required': 'الرجاء إدخال اسمك',
                    'referral_added': 'تم تسجيل إحالة جديدة! +5 RIFC',
                    'welcome_bonus': '100 RIFC مكافأة ترحيبية للإحالة!'
                }
            };
            
            let currentLang = 'es';
            let isMining = false;
            let miningInterval;
            let coinsMined = 0;
            let miningTime = 0;
            let bonusRate = 0;
            let referralCount = 0;
            let currentMiningCycleStart = 0;
            let cyclesCompleted = 0;
            let totalBalance = 0;
            let notificationsEnabled = true;
            let currentUser = null;
            
            // Elementos DOM
            const authScreen = document.getElementById('authScreen');
            const appScreen = document.getElementById('appScreen');
            const authForm = document.getElementById('authForm');
            const loginTab = document.getElementById('loginTab');
            const registerTab = document.getElementById('registerTab');
            const registerFields = document.getElementById('registerFields');
            const authSubmit = document.getElementById('authSubmit');
            const authSpinner = document.getElementById('authSpinner');
            const miningBtn = document.getElementById('miningBtn');
            const miningStatus = document.getElementById('miningStatus');
            const miningCore = document.getElementById('miningCore');
            const rifcPerCycle = document.getElementById('rifcPerCycle');
            const coinsMinedEl = document.getElementById('coinsMined');
            const miningTimeEl = document.getElementById('miningTime');
            const bonusRateEl = document.getElementById('bonusRate');
            const copyRefBtn = document.getElementById('copyRefBtn');
            const referralCode = document.getElementById('referralCode');
            const navItems = document.querySelectorAll('.nav-item');
            const contentSections = document.querySelectorAll('.content-section');
            const languageBtn = document.getElementById('languageBtn');
            const languageModal = document.getElementById('languageModal');
            const closeLangModal = document.getElementById('closeLangModal');
            const languageOptions = document.querySelectorAll('.language-option');
            const userGreeting = document.getElementById('userGreeting');
            const notificationToast = document.getElementById('notificationToast');
            const referralsCountEl = document.getElementById('referralsCount');
            const bonusEarnedEl = document.getElementById('bonusEarned');
            const particlesContainer = document.getElementById('particles');
            const miningProgress = document.getElementById('miningProgress');
            const progressText = document.getElementById('progressText');
            const referralsList = document.getElementById('referralsList');
            const messagesList = document.getElementById('messagesList');
            const messageInput = document.getElementById('messageInput');
            const charCount = document.getElementById('charCount');
            const sendMessageBtn = document.getElementById('sendMessageBtn');
            const notificationsToggleBtn = document.getElementById('notificationsToggleBtn');
            const messageModal = document.getElementById('messageModal');
            const closeMessageModal = document.getElementById('closeMessageModal');
            const googleAuthBtn = document.getElementById('googleAuthBtn');
            const forgotPassword = document.getElementById('forgotPassword');
            const userMenu = document.getElementById('userMenu');
            const userMenuBtn = document.getElementById('userMenuBtn');
            const closeUserMenu = document.getElementById('closeUserMenu');
            const menuOverlay = document.getElementById('menuOverlay');
            const userMenuName = document.getElementById('userMenuName');
            const userMenuEmail = document.getElementById('userMenuEmail');
            const logoutMenuItem = document.getElementById('logoutMenuItem');
            const languageMenuItem = document.getElementById('languageMenuItem');
            
            // Referidos de ejemplo
            const sampleReferrals = [
                { name: 'Carlos Rodríguez', joined: '2023-05-15' },
                { name: 'María García', joined: '2023-06-02' },
                { name: 'Juan Pérez', joined: '2023-06-20' }
            ];
            
            // Mensajes de ejemplo
            const sampleMessages = [
                {
                    id: 1,
                    sender: 'Soporte RIFC',
                    content: '¡Bienvenido a la plataforma! Recuerda iniciar la minería para ganar tus primeros RIFC.',
                    time: 'hace 2 horas',
                    read: false
                },
                {
                    id: 2,
                    sender: 'Ana López',
                    content: '¿Alguien sabe cómo aumentar la velocidad de minería?',
                    time: 'hace 1 día',
                    read: true
                }
            ];
            
            // Validar email
            function validateEmail(email) {
                const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
                return re.test(email);
            }
            
            // Función para generar código de referido
            function generateReferralCode() {
                return 'RIFC-' + Math.random().toString(36).substr(2, 6).toUpperCase();
            }
            
            // Mostrar spinner de carga
            function showSpinner(element) {
                element.style.display = 'block';
            }
            
            // Ocultar spinner de carga
            function hideSpinner(element) {
                element.style.display = 'none';
            }
            
            // Guardar datos de usuario en Firestore
            async function saveUserData() {
                if (!currentUser) return;
                
                try {
                    await db.collection('users').doc(currentUser.uid).set({
                        coinsMined: coinsMined,
                        miningTime: miningTime,
                        bonusRate: bonusRate,
                        referralCount: referralCount,
                        totalBalance: totalBalance,
                        isMining: isMining,
                        currentMiningCycleStart: currentMiningCycleStart,
                        cyclesCompleted: cyclesCompleted,
                        lastLogin: new Date(),
                        referralCode: referralCode.textContent
                    }, { merge: true });
                    
                    console.log("Datos de usuario guardados en Firestore");
                } catch (error) {
                    console.error("Error al guardar datos de usuario:", error);
                    showNotification("Error al guardar datos", 'error');
                }
            }
            
            // Cargar datos de usuario desde Firestore
            async function loadUserData() {
                if (!currentUser) return;
                
                try {
                    const doc = await db.collection('users').doc(currentUser.uid).get();
                    if (doc.exists) {
                        const data = doc.data();
                        coinsMined = data.coinsMined || 0;
                        miningTime = data.miningTime || 0;
                        bonusRate = data.bonusRate || 0;
                        referralCount = data.referralCount || 0;
                        totalBalance = data.totalBalance || 0;
                        isMining = data.isMining || false;
                        currentMiningCycleStart = data.currentMiningCycleStart || 0;
                        cyclesCompleted = data.cyclesCompleted || 0;
                        
                        // Si hay un código de referido guardado, mostrarlo
                        if (data.referralCode) {
                            referralCode.textContent = data.referralCode;
                        } else {
                            // Generar un nuevo código si no existe
                            referralCode.textContent = generateReferralCode();
                            await saveUserData();
                        }
                        
                        updateUI();
                        renderReferrals();
                        renderMessages();
                        
                        // Si la minería estaba activa, reanudarla
                        if (isMining) {
                            const currentTime = Date.now();
                            const elapsedTime = currentTime - currentMiningCycleStart;
                            
                            if (elapsedTime < MINING_CYCLE_DURATION) {
                                startMining(currentMiningCycleStart);
                                showNotification(translations[currentLang].mining_4h_active, 'success');
                            } else {
                                completeMiningCycle();
                            }
                        }
                    } else {
                        // Si es un nuevo usuario, crear registro
                        referralCode.textContent = generateReferralCode();
                        await saveUserData();
                    }
                } catch (error) {
                    console.error("Error al cargar datos de usuario:", error);
                    showNotification("Error al cargar datos", 'error');
                }
            }
            
            // Crear partículas para el fondo
            function createParticles() {
                for (let i = 0; i < 50; i++) {
                    const particle = document.createElement('div');
                    particle.classList.add('particle');
                    particle.style.left = `${Math.random() * 100}%`;
                    particle.style.top = `${Math.random() * 100}%`;
                    particle.style.animationDuration = `${Math.random() * 10 + 10}s`;
                    particle.style.animationDelay = `${Math.random() * 5}s`;
                    particlesContainer.appendChild(particle);
                }
            }
            
            // Actualizar la interfaz de usuario
            function updateUI() {
                coinsMinedEl.textContent = coinsMined.toFixed(2);
                rifcPerCycle.textContent = (RIFC_PER_CYCLE + (REFERRAL_BONUS * referralCount)).toFixed(1);
                bonusRateEl.textContent = (REFERRAL_BONUS * referralCount) + ' RIFC';
                referralsCountEl.textContent = referralCount;
                bonusEarnedEl.textContent = (REFERRAL_BONUS * referralCount + WELCOME_BONUS * referralCount) + ' RIFC';
                
                // Actualizar tiempo de minería
                const hours = Math.floor(miningTime / 3600);
                const minutes = Math.floor((miningTime % 3600) / 60);
                const seconds = miningTime % 60;
                miningTimeEl.textContent = `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
                
                // Actualizar barra de progreso
                if (isMining) {
                    const currentTime = Date.now();
                    const elapsedTime = currentTime - currentMiningCycleStart;
                    const progress = Math.min(100, (elapsedTime / MINING_CYCLE_DURATION) * 100);
                    miningProgress.style.width = `${progress}%`;
                    progressText.textContent = `${translations[currentLang].progress_label}: ${progress.toFixed(1)}%`;
                } else {
                    miningProgress.style.width = '0%';
                    progressText.textContent = `${translations[currentLang].progress_label}: 0%`;
                }
            }
            
            // Renderizar referidos
            function renderReferrals() {
                referralsList.innerHTML = '';
                
                if (referralCount === 0) {
                    referralsList.innerHTML = `<p style="text-align: center; color: var(--text-gray); padding: 20px;">${currentLang === 'es' ? 'Aún no tienes referidos' : 'You have no referrals yet'}</p>`;
                    return;
                }
                
                sampleReferrals.forEach((referral, index) => {
                    if (index < referralCount) {
                        const referralItem = document.createElement('div');
                        referralItem.classList.add('referral-item');
                        
                        referralItem.innerHTML = `
                            <div class="referral-info">
                                <div class="referral-avatar">
                                    <i class="fas fa-user"></i>
                                </div>
                                <div class="referral-name">${referral.name}</div>
                            </div>
                            <div class="referral-bonus">+${REFERRAL_BONUS + WELCOME_BONUS} RIFC</div>
                        `;
                        
                        referralsList.appendChild(referralItem);
                    }
                });
            }
            
            // Renderizar mensajes
            function renderMessages() {
                messagesList.innerHTML = '';
                
                if (sampleMessages.length === 0) {
                    messagesList.innerHTML = `<p style="text-align: center; color: var(--text-gray); padding: 20px;">${translations[currentLang].no_messages}</p>`;
                    return;
                }
                
                sampleMessages.forEach(message => {
                    const messageItem = document.createElement('div');
                    messageItem.classList.add('message-item');
                    if (!message.read) messageItem.classList.add('unread');
                    messageItem.setAttribute('data-id', message.id);
                    
                    messageItem.innerHTML = `
                        <div class="message-icon">
                            <i class="fas fa-user"></i>
                        </div>
                        <div class="message-content">
                            <div class="message-header">
                                <div class="message-sender">${message.sender}</div>
                                <div class="message-time">${message.time}</div>
                            </div>
                            <div class="message-text">${message.content}</div>
                        </div>
                    `;
                    
                    messagesList.appendChild(messageItem);
                });
                
                // Añadir event listeners a los mensajes
                document.querySelectorAll('.message-item').forEach(item => {
                    item.addEventListener('click', function() {
                        const messageId = parseInt(this.getAttribute('data-id'));
                        openMessage(messageId);
                    });
                });
            }
            
            // Abrir mensaje
            function openMessage(messageId) {
                const message = sampleMessages.find(m => m.id === messageId);
                if (message) {
                    // Marcar como leído si no lo estaba
                    if (!message.read) {
                        message.read = true;
                        saveUserData();
                        renderMessages();
                    }
                    
                    // Mostrar el modal con el mensaje
                    document.querySelector('.message-sender-name').textContent = message.sender;
                    document.querySelector('.message-time').textContent = message.time;
                    document.querySelector('.message-subject-modal').textContent = 'Mensaje de la comunidad';
                    document.querySelector('.message-body-modal').innerHTML = `
                        <p>${message.content}</p>
                    `;
                    
                    messageModal.classList.add('active');
                }
            }
            
            // Mostrar notificación
            function showNotification(message, type = 'info') {
                if (!notificationsEnabled && type !== 'error') return;
                
                notificationToast.textContent = message;
                notificationToast.className = 'notification-toast';
                notificationToast.classList.add(type);
                notificationToast.classList.add('show');
                
                setTimeout(() => {
                    notificationToast.classList.remove('show');
                }, 3000);
            }
            
            // Completar ciclo de minería
            function completeMiningCycle() {
                if (!isMining) return;
                
                // Añadir RIFC ganados en este ciclo
                const earnedThisCycle = RIFC_PER_CYCLE + (REFERRAL_BONUS * referralCount);
                coinsMined += earnedThisCycle;
                cyclesCompleted++;
                
                // Reiniciar el ciclo
                currentMiningCycleStart = Date.now();
                
                // Mostrar notificación
                showNotification(`${translations[currentLang].mining_4h_complete} (+${earnedThisCycle} RIFC)`, 'success');
                
                // Guardar datos
                saveUserData();
                updateUI();
            }
            
            // Iniciar minería
            function startMining(startTimestamp) {
                if (isMining) {
                    showNotification(translations[currentLang].mining_already_active, 'warning');
                    return;
                }
                
                isMining = true;
                currentMiningCycleStart = startTimestamp || Date.now();
                
                miningStatus.textContent = translations[currentLang].mining_status_active;
                miningStatus.classList.add('active');
                miningBtn.classList.add('mining-active');
                miningBtn.classList.add('disabled');
                miningBtn.querySelector('span').textContent = translations[currentLang].mining_in_progress;
                miningCore.classList.add('mining-active');
                
                miningInterval = setInterval(() => {
                    const currentTime = Date.now();
                    const elapsedTime = currentTime - currentMiningCycleStart;
                    
                    if (elapsedTime >= MINING_CYCLE_DURATION) {
                        completeMiningCycle();
                        return;
                    }
                    
                    // Calcular RIFC minados en este ciclo
                    const rifcPerMillisecond = (RIFC_PER_CYCLE + (REFERRAL_BONUS * referralCount)) / MINING_CYCLE_DURATION;
                    coinsMined = rifcPerMillisecond * elapsedTime;
                    miningTime = Math.floor(elapsedTime / 1000);
                    
                    updateUI();
                    saveUserData();
                    
                }, 1000);
                
                saveUserData();
                showNotification(translations[currentLang].mining_started, 'success');
            }
            
            // Detener minería
            function stopMining() {
                if (!isMining) return;
                
                isMining = false;
                clearInterval(miningInterval);
                miningStatus.textContent = translations[currentLang].mining_status;
                miningStatus.classList.remove('active');
                miningBtn.classList.remove('mining-active');
                miningBtn.classList.remove('disabled');
                miningBtn.querySelector('span').textContent = translations[currentLang].start_mining;
                miningCore.classList.remove('mining-active');
                currentMiningCycleStart = 0;
                miningTime = 0;
                
                saveUserData();
                showNotification(translations[currentLang].mining_stopped, 'info');
            }
            
            // Inicializar gráfico de minería
            function initMiningChart() {
                const ctx = document.getElementById('miningChart').getContext('2d');
                new Chart(ctx, {
                    type: 'line',
                    data: {
                        labels: ['Lun', 'Mar', 'Mié', 'Jue', 'Vie', 'Sáb', 'Dom'],
                        datasets: [{
                            label: 'RIFC Minados',
                            data: [1.2, 1.8, 2.3, 1.7, 2.5, 3.1, 4.2],
                            borderColor: '#4caf50',
                            backgroundColor: 'rgba(76, 175, 80, 0.1)',
                            borderWidth: 2,
                            tension: 0.3,
                            fill: true
                        }]
                    },
                    options: {
                        responsive: true,
                        plugins: {
                            legend: {
                                display: false
                            }
                        },
                        scales: {
                            y: {
                                beginAtZero: true,
                                grid: {
                                    color: 'rgba(255, 255, 255, 0.05)'
                                },
                                ticks: {
                                    color: '#a0aec0'
                                }
                            },
                            x: {
                                grid: {
                                    color: 'rgba(255, 255, 255, 0.05)'
                                },
                                ticks: {
                                    color: '#a0aec0'
                                }
                            }
                        }
                    }
                });
            }
            
            // Añadir referido
            function addReferral() {
                referralCount++;
                totalBalance += REFERRAL_BONUS + WELCOME_BONUS;
                updateUI();
                saveUserData();
                renderReferrals();
                showNotification(`${translations[currentLang].referral_added} (+${REFERRAL_BONUS} RIFC)`, 'success');
                showNotification(`${translations[currentLang].welcome_bonus} (+${WELCOME_BONUS} RIFC)`, 'success');
            }
            
            // Aplicar traducciones
            function applyTranslations() {
                if (userGreeting.querySelector('span')) {
                    userGreeting.querySelector('span').textContent = translations[currentLang].greeting;
                }
                miningStatus.textContent = isMining ? 
                    translations[currentLang].mining_status_active : 
                    translations[currentLang].mining_status;
                miningBtn.querySelector('span').textContent = isMining ? 
                    translations[currentLang].mining_in_progress : 
                    translations[currentLang].start_mining;
                
                document.querySelectorAll('.nav-item')[0].querySelector('span').textContent = translations[currentLang].mining;
                document.querySelectorAll('.nav-item')[1].querySelector('span').textContent = translations[currentLang].referrals;
                document.querySelectorAll('.nav-item')[2].querySelector('span').textContent = translations[currentLang].messages;
                
                document.getElementById('miningSection').querySelector('.section-title').textContent = translations[currentLang].mining_title;
                document.getElementById('referralsSection').querySelector('.section-title').textContent = translations[currentLang].referral_program;
                document.getElementById('messagesSection').querySelector('.section-title').textContent = translations[currentLang].messages_title;
                
                document.querySelectorAll('.stat-label')[0].textContent = translations[currentLang].rifc_per_cycle;
                document.querySelectorAll('.stat-label')[1].textContent = translations[currentLang].coins_mined;
                document.querySelectorAll('.stat-label')[2].textContent = translations[currentLang].mining_time;
                document.querySelectorAll('.stat-label')[3].textContent = translations[currentLang].bonus_rate;
                
                if (document.querySelectorAll('.stat-label')[4]) {
                    document.querySelectorAll('.stat-label')[4].textContent = translations[currentLang].referrals_count;
                    document.querySelectorAll('.stat-label')[5].textContent = translations[currentLang].bonus_earned;
                }
                
                if (document.getElementById('referralsTitle')) {
                    document.getElementById('referralsTitle').textContent = translations[currentLang].active_referrals;
                }
                
                if (document.getElementById('referralDescription')) {
                    document.getElementById('referralDescription').textContent = translations[currentLang].referral_description;
                }
                
                document.querySelector('.withdraw-btn').textContent = translations[currentLang].withdraw;
                document.querySelector('#copyRefBtn').innerHTML = `<i class="fas fa-copy"></i> ${translations[currentLang].copy}`;
                document.querySelector('#googleAuthBtn').innerHTML = `<i class="fab fa-google"></i> ${translations[currentLang].google_login}`;
                document.querySelector('#sendMessageBtn').innerHTML = `<i class="fas fa-paper-plane"></i> ${translations[currentLang].send_message}`;
                document.querySelector('#authSubmit').textContent = registerFields.style.display === 'block' ? 
                    translations[currentLang].register_button : 
                    translations[currentLang].login_button;
            }
            
            // Iniciar la aplicación
            function initApp() {
                createParticles();
                
                // Contador de caracteres para mensajes
                messageInput.addEventListener('input', function() {
                    charCount.textContent = this.value.length;
                });
                
                // Observador de autenticación de Firebase
                auth.onAuthStateChanged(user => {
                    if (user) {
                        // Usuario autenticado
                        currentUser = user;
                        
                        // Actualizar información del usuario
                        userMenuName.textContent = user.displayName || "Minero RIFC";
                        userMenuEmail.textContent = user.email;
                        userGreeting.querySelector('span').textContent = translations[currentLang].greeting + (user.displayName ? `, ${user.displayName.split(' ')[0]}` : '');
                        
                        // Cargar datos del usuario
                        loadUserData();
                        
                        // Mostrar aplicación
                        authScreen.style.display = 'none';
                        appScreen.classList.add('active');
                        initMiningChart();
                        
                        showNotification(translations[currentLang].login_success, 'success');
                    } else {
                        // Usuario no autenticado
                        authScreen.style.display = 'flex';
                        appScreen.classList.remove('active');
                    }
                });
                
                // Cambiar entre login y registro
                loginTab.addEventListener('click', () => {
                    loginTab.classList.add('active');
                    registerTab.classList.remove('active');
                    registerFields.style.display = 'none';
                    authSubmit.textContent = translations[currentLang].login_button;
                });
                
                registerTab.addEventListener('click', () => {
                    registerTab.classList.add('active');
                    loginTab.classList.remove('active');
                    registerFields.style.display = 'block';
                    authSubmit.textContent = translations[currentLang].register_button;
                });
                
                // Iniciar sesión/registrarse
                authForm.addEventListener('submit', async (e) => {
                    e.preventDefault();
                    
                    const email = document.getElementById('loginEmail').value;
                    const password = document.getElementById('loginPassword').value;
                    
                    if (!validateEmail(email)) {
                        showNotification(translations[currentLang].invalid_email, 'error');
                        return;
                    }
                    
                    if (password.length < 6) {
                        showNotification(translations[currentLang].short_password, 'error');
                        return;
                    }
                    
                    showSpinner(authSpinner);
                    authSubmit.disabled = true;
                    
                    try {
                        if (registerFields.style.display === 'block') {
                            // Registro
                            const name = document.getElementById('registerName').value;
                            const confirmPassword = document.getElementById('registerPassword').value;
                            const referralCodeInput = document.getElementById('referralCodeInput').value;
                            
                            if (password !== confirmPassword) {
                                showNotification(translations[currentLang].password_mismatch, 'error');
                                hideSpinner(authSpinner);
                                authSubmit.disabled = false;
                                return;
                            }
                            
                            if (!name) {
                                showNotification(translations[currentLang].name_required, 'error');
                                hideSpinner(authSpinner);
                                authSubmit.disabled = false;
                                return;
                            }
                            
                            // Crear usuario con Firebase Auth
                            const userCredential = await auth.createUserWithEmailAndPassword(email, password);
                            const user = userCredential.user;
                            
                            // Actualizar perfil con nombre
                            await user.updateProfile({
                                displayName: name
                            });
                            
                            // Generar código de referido
                            const refCode = generateReferralCode();
                            referralCode.textContent = refCode;
                            
                            // Procesar código de referido si existe
                            if (referralCodeInput) {
                                // Aquí iría la lógica para procesar el código de referido
                                // Por ahora solo mostramos un mensaje
                                showNotification('Código de referido aplicado', 'success');
                                addReferral();
                            }
                            
                            // Mostrar mensaje de éxito
                            showNotification(translations[currentLang].login_success, 'success');
                        } else {
                            // Inicio de sesión
                            await auth.signInWithEmailAndPassword(email, password);
                            showNotification(translations[currentLang].login_success, 'success');
                        }
                    } catch (error) {
                        console.error("Error de autenticación:", error);
                        showNotification(error.message, 'error');
                    } finally {
                        hideSpinner(authSpinner);
                        authSubmit.disabled = false;
                    }
                });
                
                // Registro con Google
                googleAuthBtn.addEventListener('click', async () => {
                    try {
                        const provider = new firebase.auth.GoogleAuthProvider();
                        await auth.signInWithPopup(provider);
                    } catch (error) {
                        console.error("Error en autenticación con Google:", error);
                        showNotification(error.message, 'error');
                    }
                });
                
                // Olvidé contraseña
                forgotPassword.addEventListener('click', (e) => {
                    e.preventDefault();
                    const email = document.getElementById('loginEmail').value;
                    
                    if (!validateEmail(email)) {
                        showNotification(translations[currentLang].invalid_email, 'error');
                        return;
                    }
                    
                    auth.sendPasswordResetEmail(email)
                        .then(() => {
                            showNotification(translations[currentLang].password_reset, 'success');
                        })
                        .catch(error => {
                            showNotification(error.message, 'error');
                        });
                });
                
                // Cerrar sesión
                logoutMenuItem.addEventListener('click', () => {
                    if (confirm(currentLang === 'es' ? '¿Estás seguro de que quieres cerrar sesión?' : 'Are you sure you want to log out?')) {
                        auth.signOut();
                    }
                });
                
                // Copiar código de referido
                copyRefBtn.addEventListener('click', () => {
                    navigator.clipboard.writeText(referralCode.textContent).then(() => {
                        showNotification(translations[currentLang].copied, 'success');
                    }).catch(err => {
                        console.error('Error al copiar:', err);
                    });
                });
                
                // Navegación
                navItems.forEach(item => {
                    item.addEventListener('click', (e) => {
                        e.preventDefault();
                        const sectionId = item.getAttribute('data-section');
                        
                        navItems.forEach(navItem => navItem.classList.remove('active'));
                        item.classList.add('active');
                        
                        contentSections.forEach(section => section.classList.remove('active'));
                        document.getElementById(sectionId).classList.add('active');
                    });
                });
                
                // Gestión de idiomas
                languageBtn.addEventListener('click', () => {
                    languageModal.classList.add('active');
                });
                
                languageMenuItem.addEventListener('click', () => {
                    languageModal.classList.add('active');
                    userMenu.classList.remove('active');
                    menuOverlay.classList.remove('active');
                });
                
                closeLangModal.addEventListener('click', () => {
                    languageModal.classList.remove('active');
                });
                
                languageOptions.forEach(option => {
                    option.addEventListener('click', () => {
                        const lang = option.getAttribute('data-lang');
                        if (translations[lang]) {
                            currentLang = lang;
                            applyTranslations();
                            languageOptions.forEach(opt => opt.classList.remove('active'));
                            option.classList.add('active');
                            languageModal.classList.remove('active');
                        }
                    });
                });
                
                // Toggle notificaciones
                notificationsToggleBtn.addEventListener('click', () => {
                    notificationsEnabled = !notificationsEnabled;
                    notificationsToggleBtn.classList.toggle('active', notificationsEnabled);
                    
                    if (notificationsEnabled) {
                        showNotification(translations[currentLang].notifications_on, 'success');
                    } else {
                        showNotification(translations[currentLang].notifications_off, 'warning');
                    }
                });
                
                // Cerrar modal de mensaje
                closeMessageModal.addEventListener('click', () => {
                    messageModal.classList.remove('active');
                });
                
                // Enviar mensaje
                sendMessageBtn.addEventListener('click', function() {
                    const messageText = messageInput.value.trim();
                    if (messageText) {
                        const newMessage = {
                            id: sampleMessages.length + 1,
                            sender: currentLang === 'es' ? 'Tú' : 'You',
                            content: messageText,
                            time: currentLang === 'es' ? 'justo ahora' : 'just now',
                            read: true
                        };
                        
                        sampleMessages.unshift(newMessage);
                        renderMessages();
                        messageInput.value = '';
                        charCount.textContent = '0';
                        showNotification(translations[currentLang].message_sent, 'success');
                    }
                });
                
                // Manejar Enter para enviar mensaje
                messageInput.addEventListener('keypress', function(e) {
                    if (e.key === 'Enter' && !e.shiftKey) {
                        e.preventDefault();
                        sendMessageBtn.click();
                    }
                });
                
                // Iniciar/detener minería
                miningBtn.addEventListener('click', () => {
                    if (isMining) {
                        stopMining();
                    } else {
                        startMining();
                    }
                });
                
                // Retirar fondos
                document.getElementById('withdrawBtn').addEventListener('click', () => {
                    if (coinsMined < 10) {
                        showNotification(translations[currentLang].withdraw_minimum, 'error');
                        return;
                    }
                    
                    showNotification(translations[currentLang].withdraw_processing, 'info');
                    
                    setTimeout(() => {
                        totalBalance += coinsMined;
                        coinsMined = 0;
                        updateUI();
                        saveUserData();
                        showNotification(translations[currentLang].withdraw_success, 'success');
                    }, 2000);
                });
                
                // Menú de usuario
                userMenuBtn.addEventListener('click', () => {
                    userMenu.classList.add('active');
                    menuOverlay.classList.add('active');
                });
                
                closeUserMenu.addEventListener('click', () => {
                    userMenu.classList.remove('active');
                    menuOverlay.classList.remove('active');
                });
                
                menuOverlay.addEventListener('click', () => {
                    userMenu.classList.remove('active');
                    menuOverlay.classList.remove('active');
                });
                
                // Simular referidos (para demostración)
                setTimeout(() => {
                    addReferral();
                }, 5000);
                
    </script>
</body>
</html>
