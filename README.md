<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>😺 UwU Café - Sistema de Fichajes</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
            background: #0a0a0a;
            min-height: 100vh;
            color: #e0e0e0;
            overflow-x: hidden;
        }

        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        .particle {
            position: absolute;
            background: rgba(255, 105, 180, 0.3);
            border-radius: 50%;
            animation: float-particle 15s infinite ease-in-out;
        }

        @keyframes float-particle {
            0%, 100% { transform: translate(0, 0) scale(1); opacity: 0.3; }
            50% { transform: translate(100px, -100px) scale(1.5); opacity: 0.6; }
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 10;
        }

        .header {
            background: rgba(20, 20, 20, 0.9);
            backdrop-filter: blur(20px);
            border: 2px solid rgb(255, 255, 255);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 30px;
            box-shadow: 0 0 20px rgba(16, 16, 16, 0.5);
            animation: slideDown 0.6s ease-out;
        }

        @keyframes slideDown {
            from { transform: translateY(-50px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        .header-content {
            display: flex;
            align-items: center;
            justify-content: space-between;
        }

        .header-left {
            display: flex;
            align-items: center;
            gap: 20px;
        }

        .logo {
            width: 70px;
            height: 70px;
            background: linear-gradient(135deg, #323232 0%, #323232 100%);
            border: 2px solid rgb(255, 255, 255);
            border-radius: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 35px;
            box-shadow: 0 0 10px rgba(16, 16, 16, 0.853);
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .header-title h1 {
            font-size: 2.2em;
            font-weight: 700;
            background: linear-gradient(135deg, #f7f4f5 0%, #f9f9f9 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 5px;
        }

        .header-title p {
            color: #f7f3f5;
            font-size: 0.95em;
        }

        .header-stats {
            display: flex;
            gap: 30px;
        }

        .header-stat {
            text-align: center;
            background: rgba(255, 255, 255, 0.1);
            padding: 15px 25px;
            border-radius: 15px;
            border: 1px solid rgba(255, 255, 255, 0.3);
        }

        .header-stat-value {
            font-size: 1.8em;
            font-weight: 700;
            background: linear-gradient(135deg, #f7f4f5 0%, #14ff14 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .header-stat-label {
            font-size: 0.85em;
            color: #ffc0cb;
            margin-top: 5px;
        }

        .main-content {
            display: grid;
            grid-template-columns: 350px 1fr;
            gap: 30px;
        }

        .card {
            background: rgba(20, 20, 20, 0.9);
            backdrop-filter: blur(20px);
            border: 2px solid rgba(255, 255, 255, 0.3);
            border-radius: 20px;
            box-shadow: 0 0 10px rgba(16, 16, 16, 0.853);
            overflow: hidden;
            animation: fadeIn 0.8s ease-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: scale(0.95); }
            to { opacity: 1; transform: scale(1); }
        }

        .tabs-container {
            background: rgba(0, 0, 0, 0.5);
            padding: 10px;
            border-bottom: 2px solid rgba(255, 255, 255, 0.3);
        }

        .tabs {
            display: flex;
            gap: 5px;
        }

        .tab {
            flex: 1;
            padding: 12px 20px;
            background: transparent;
            border: none;
            color: #a0a0a0;
            cursor: pointer;
            border-radius: 10px;
            font-size: 0.95em;
            font-weight: 600;
            transition: all 0.3s ease;
            position: relative;
        }

        .tab:hover {
            color: #fff;
            background: rgba(255, 255, 255, 0.1);
        }

        .tab.active {
            background: rgba(30, 30, 30, 0.144);
            border: 1px solid rgba(251, 250, 251, 0.3);
            color: #fff;
        }

        .tab-content {
            padding: 20px;
            max-height: calc(100vh - 200px);
            overflow-y: auto;
        }

        .tab-content::-webkit-scrollbar {
            width: 8px;
        }

        .tab-content::-webkit-scrollbar-track {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
        }

        .tab-content::-webkit-scrollbar-thumb {
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
        }

        .tab-panel {
            display: none;
            animation: fadeInPanel 0.4s ease-out;
        }

        .tab-panel.active {
            display: block;
        }

        @keyframes fadeInPanel {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .search-box {
            position: relative;
            margin-bottom: 20px;
        }

        .search-box input {
            width: 100%;
            padding: 12px 15px 12px 45px;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.3);
            border-radius: 12px;
            color: #fff;
            font-size: 0.95em;
            transition: all 0.3s ease;
        }

        .search-box input:focus {
            outline: none;
            background: rgba(255, 255, 255, 0.1);
            border-color: #f1eeef;
            box-shadow: 0 0 20px rgba(255, 255, 255, 0.3);
        }

        .search-box::before {
            content: '🔍';
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            font-size: 1.2em;
        }

        .employee-item {
            background: rgba(255, 255, 255, 0.05);
            padding: 15px;
            margin-bottom: 10px;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 1px solid rgba(255, 255, 255, 0.2);
            display: flex;
            align-items: center;
            gap: 12px;
            position: relative;
            overflow: hidden;
        }

        .employee-item::before {
            content: '';
            position: absolute;
            left: 0;
            top: 0;
            width: 4px;
            height: 100%;
            background: linear-gradient(135deg, #f7f4f5 0%, #bebabe 100%);
            transform: scaleY(0);
            transition: transform 0.3s ease;
        }

        .employee-item:hover {
            background: rgba(255, 255, 255, 0.15);
            transform: translateX(5px);
            border-color: #fefefe;
            box-shadow: 0 5px 20px rgba(255, 255, 255, 0.3);
        }

        .employee-item:hover::before {
            transform: scaleY(1);
        }

        .employee-item.selected {
            background: rgba(255, 255, 255, 0.2);
            border-color: #fefefe;
            box-shadow: 0 5px 20px rgba(255, 255, 255, 0.4);
        }

        .employee-item.selected::before {
            transform: scaleY(1);
        }

        .employee-avatar {
            width: 40px;
            height: 40px;
            border-radius: 10px;
            background: linear-gradient(135deg, #252525 0%, #252525 100%);
            display: flex;
            border: 1px solid #fefefe;
            align-items: center;
            justify-content: center;
            font-weight: 700;
            color: #fff;
            font-size: 1.1em;
        }

        .employee-info {
            flex: 1;
        }

        .employee-name {
            font-weight: 600;
            color: #fff;
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.5);
            margin-bottom: 5px;
        }

        .employee-rank {
            display: inline-block;
            padding: 3px 10px;
            border-radius: 8px;
            font-size: 0.75em;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .rank-jefa {
            background: linear-gradient(135deg, #ff1493 0%, #ff69b4 100%);
            color: white;
            box-shadow: 0 0 10px rgba(255, 20, 147, 0.5);
        }

        .rank-encargado, .rank-encargada {
            background: linear-gradient(135deg, #9333ea 0%, #c084fc 100%);
            color: white;
            box-shadow: 0 0 10px rgba(147, 51, 234, 0.5);
        }

        .rank-experimentado, .rank-experimentada {
            background: linear-gradient(135deg, #3b82f6 0%, #60a5fa 100%);
            color: white;
            box-shadow: 0 0 10px rgba(59, 130, 246, 0.5);
        }

        .rank-trabajador-fijo {
            background: linear-gradient(135deg, #10b981 0%, #34d399 100%);
            color: white;
            box-shadow: 0 0 10px rgba(16, 185, 129, 0.5);
        }

        .rank-practicas {
            background: linear-gradient(135deg, #f59e0b 0%, #fbbf24 100%);
            color: white;
            box-shadow: 0 0 10px rgba(245, 158, 11, 0.5);
        }

        .status-panel {
            padding: 40px;
            text-align: center;
        }

        .welcome-state {
            padding: 60px 40px;
            text-align: center;
        }

        .welcome-icon {
            font-size: 5em;
            margin-bottom: 20px;
            animation: wave 2s infinite;
        }

        @keyframes wave {
            0%, 100% { transform: rotate(0deg); }
            25% { transform: rotate(20deg); }
            75% { transform: rotate(-20deg); }
        }

        .welcome-state h2 {
            font-size: 1.8em;
            color: #f7f4f7;
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.5);
            margin-bottom: 15px;
        }

        .welcome-state p {
            color: #f7f4f7;
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.5);
            font-size: 1.1em;
        }

        .status-badge {
            display: inline-block;
            padding: 10px 25px;
            background: linear-gradient(135deg, #10b981 0%, #059669 100%);
            border-radius: 50px;
            font-weight: 600;
            margin-bottom: 20px;
            box-shadow: 0 5px 20px rgba(16, 185, 129, 0.4);
            animation: slideIn 0.5s ease-out;
        }

        @keyframes slideIn {
            from { transform: translateY(-20px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        .employee-name-display {
            font-size: 2em;
            font-weight: 700;
            margin-bottom: 30px;
            background: linear-gradient(135deg, #f7f4f7 0%, #ffffff 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .timer-display {
            font-size: 4em;
            font-weight: 700;
            font-family: 'Courier New', monospace;
            background: linear-gradient(135deg, #f7f4f7 0%, #ffffff 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 40px;
            letter-spacing: 3px;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 20px;
            margin-bottom: 40px;
        }

        .stat-card {
            background: rgba(255, 105, 180, 0.1);
            padding: 25px;
            border-radius: 15px;
            border: 1px solid rgba(255, 105, 180, 0.3);
            transition: all 0.3s ease;
        }

        .stat-card:hover {
            background: rgba(255, 105, 180, 0.15);
            transform: translateY(-5px);
            box-shadow: 0 10px 30px rgba(255, 105, 180, 0.3);
        }

        .stat-icon {
            font-size: 2em;
            margin-bottom: 10px;
        }

        .stat-value {
            font-size: 2em;
            font-weight: 700;
            color: #f7f4f7;
            margin-bottom: 5px;
        }

        .stat-label {
            color: #f7f4f7;
            font-size: 0.9em;
        }

        .btn {
            padding: 15px 40px;
            border: none;
            border-radius: 12px;
            font-size: 1em;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 1px;
            position: relative;
            overflow: hidden;
        }

        .btn::before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.2);
            transform: translate(-50%, -50%);
            transition: width 0.6s ease, height 0.6s ease;
        }

        .btn:hover::before {
            width: 300px;
            height: 300px;
        }

        .btn span {
            position: relative;
            z-index: 1;
        }

        .btn-primary {
            background: linear-gradient(135deg, #228d14 0%, #228d14 100%);
            color: white;
            box-shadow: 0 0 10px rgba(14, 14, 14, 0.4);
        }

        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 0 10px rgba(255, 255, 255, 0.6);
        }

        .btn-danger {
            background: linear-gradient(135deg, #ef4444 0%, #dc2626 100%);
            color: white;
            box-shadow: 0 0 10px rgba(239, 68, 68, 0.4);
        }

        .btn-danger:hover {
            transform: translateY(-3px);
            box-shadow: 0 0 10px rgba(239, 68, 68, 0.6);
        }

        .btn-secondary {
            background: rgba(255, 255, 255, 0.1);
            color: #fefefe;
            border: 2px solid #fefefe;
        }

        .btn-secondary:hover {
            background: rgba(255, 105, 180, 0.2);
        }

        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.85);
            backdrop-filter: blur(10px);
            z-index: 9999;
            display: none;
            align-items: center;
            justify-content: center;
            animation: fadeInOverlay 0.3s ease-out;
        }

        .modal-overlay.show {
            display: flex;
        }

        @keyframes fadeInOverlay {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .modal {
            background: #1a1a1a;
            border: 2px solid #fefefe;
            border-radius: 25px;
            padding: 40px;
            max-width: 500px;
            width: 90%;
            box-shadow: 0 0 20px rgba(15, 15, 15, 0.777);
            animation: modalBounce 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            position: relative;
        }

        @keyframes modalBounce {
            0% { transform: scale(0.5); opacity: 0; }
            100% { transform: scale(1); opacity: 1; }
        }

        .modal-header {
            text-align: center;
            margin-bottom: 30px;
        }

        .modal-icon {
            font-size: 4em;
            margin-bottom: 15px;
            animation: bounce 1s infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        .modal-title {
            font-size: 1.8em;
            font-weight: 700;
            background: linear-gradient(135deg, #fbfcfa 0%, #fcfffc 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 10px;
        }

        .modal-subtitle {
            color: #f7f4f7;
            font-size: 1.1em;
        }

        .modal-body {
            background: rgba(255, 255, 255, 0.05);
            padding: 25px;
            border-radius: 15px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            margin-bottom: 30px;
        }

        .modal-employee {
            font-size: 1.5em;
            font-weight: 700;
            color: #fefefe;
            text-align: center;
            margin-bottom: 15px;
        }

        .modal-time {
            text-align: center;
            color: #f7f4f7;
            font-size: 1.1em;
        }

        .modal-actions {
            display: flex;
            gap: 15px;
        }

        .modal-actions .btn {
            flex: 1;
        }

        .notification {
            position: fixed;
            top: 30px;
            right: 30px;
            background: #1a1a1a;
            backdrop-filter: blur(20px);
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.5);
            border: 2px solid;
            z-index: 10000;
            min-width: 350px;
            max-width: 400px;
            transform: translateX(450px);
            opacity: 0;
            transition: all 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);
        }

        .notification.show {
            transform: translateX(0);
            opacity: 1;
        }

        .notification.success { border-color: #10b981; }
        .notification.error { border-color: #ef4444; }
        .notification.info { border-color: #332655; }
        .notification.warning { border-color: #f59e0b; }

        .notification-header {
            display: flex;
            align-items: center;
            margin-bottom: 12px;
        }

        .notification-icon {
            width: 40px;
            height: 40px;
            border-radius: 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5em;
            margin-right: 15px;
        }

        .notification.success .notification-icon {
            background: linear-gradient(135deg, #10b981 0%, #059669 100%);
        }

        .notification.error .notification-icon {
            background: linear-gradient(135deg, #ef4444 0%, #dc2626 100%);
        }

        .notification.info .notification-icon {
            background: linear-gradient(135deg, #2a246c 0%, #2a246c 100%);
        }

        .notification.warning .notification-icon {
            background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);
        }

        .notification-content {
            flex: 1;
        }

        .notification-title {
            font-weight: 700;
            font-size: 1.1em;
            margin-bottom: 5px;
            color: #fff;
        }

        .notification-message {
            color: #a0a0a0;
            font-size: 0.95em;
            line-height: 1.4;
        }

        .notification-close {
            position: absolute;
            top: 15px;
            right: 15px;
            background: none;
            border: none;
            color: #a0a0a0;
            cursor: pointer;
            font-size: 1.2em;
            padding: 5px;
            line-height: 1;
            transition: all 0.3s ease;
        }

        .notification-close:hover {
            color: #fff;
            transform: rotate(90deg);
        }

        .notification-progress {
            position: absolute;
            bottom: 0;
            left: 0;
            height: 3px;
            background: linear-gradient(90deg, transparent, currentColor);
            animation: progress 5s linear;
        }

        @keyframes progress {
            from { width: 100%; }
            to { width: 0%; }
        }

        .hidden {
            display: none !important;
        }

        .letter-group {
            margin-bottom: 25px;
        }

        .letter-header {
            font-size: 1.2em;
            font-weight: 700;
            color: #fefefe;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 2px solid rgba(255, 255, 255, 0.3);
        }

        .discord-info {
            background: rgba(88, 101, 242, 0.1);
            border: 1px solid rgba(88, 101, 242, 0.3);
            border-radius: 15px;
            padding: 20px;
            margin-top: 30px;
            text-align: center;
        }

        .discord-info-title {
            color: #5865f2;
            font-weight: 700;
            font-size: 1.1em;
            margin-bottom: 10px;
        }

        .discord-info-text {
            color: #a0a0a0;
            font-size: 0.9em;
            line-height: 1.6;
        }

        @media (max-width: 1024px) {
            .main-content {
                grid-template-columns: 1fr;
            }

            .header-content {
                flex-direction: column;
                gap: 20px;
            }

            .header-stats {
                width: 100%;
                justify-content: space-around;
            }
        }

        @media (max-width: 768px) {
            .timer-display {
                font-size: 2.5em;
            }

            .stats-grid {
                grid-template-columns: 1fr;
            }

            .notification {
                right: 15px;
                left: 15px;
                min-width: auto;
                max-width: none;
                transform: translateY(-150px);
            }

            .notification.show {
                transform: translateY(0);
            }

            .modal {
                padding: 30px 20px;
            }

            .modal-actions {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="particles" id="particles"></div>
    
    <div class="modal-overlay" id="modalOverlay">
        <div class="modal">
            <div class="modal-header">
                <div class="modal-icon">😺</div>
                <div class="modal-title">¡Nya~! ¿Listo para trabajar?</div>
                <div class="modal-subtitle">Confirma tu entrada de servicio</div>
            </div>
            <div class="modal-body">
                <div class="modal-employee" id="modalEmployeeName"></div>
                <div class="modal-time" id="modalTime"></div>
            </div>
            <div class="modal-actions">
                <button class="btn btn-secondary" onclick="cancelClockIn()">
                    <span>✕ Cancelar</span>
                </button>
                <button class="btn btn-primary" onclick="confirmClockIn()">
                    <span>✓ Confirmar Entrada</span>
                </button>
            </div>
        </div>
    </div>
    
    <div class="container">
        <div class="header">
            <div class="header-content">
                <div class="header-left">
                    <div class="logo">😺</div>
                    <div class="header-title">
                        <h1>UwU Café</h1>
                        <p>Sistema de Gestión de Fichajes ✨</p>
                    </div>
                </div>
                <div class="header-stats">
                    <div class="header-stat">
                        <div class="header-stat-value" id="totalEmployees">10</div>
                        <div class="header-stat-label">Empleados</div>
                    </div>
                    <div class="header-stat">
                        <div class="header-stat-value" id="activeNow">0</div>
                        <div class="header-stat-label">En Servicio</div>
                    </div>
                </div>
            </div>
        </div>

        <div class="main-content">
            <div class="card">
                <div class="tabs-container">
                    <div class="tabs">
                        <button class="tab active" onclick="switchTab('all')">Todos</button>
                        <button class="tab" onclick="switchTab('az')">A-Z</button>
                        <button class="tab" onclick="switchTab('recent')">Recientes</button>
                    </div>
                </div>
                <div class="tab-content">
                    <div class="search-box">
                        <input type="text" id="searchInput" placeholder="Buscar empleado..." onkeyup="filterEmployees()">
                    </div>
                    <div class="tab-panel active" id="allPanel"></div>
                    <div class="tab-panel" id="azPanel"></div>
                    <div class="tab-panel" id="recentPanel"></div>
                </div>
            </div>

            <div class="card">
                <div id="welcomeScreen" class="welcome-state">
                    <div class="welcome-icon">👋</div>
                    <h2>¡Bienvenido al Sistema! 😺</h2>
                    <p>Selecciona tu nombre para comenzar tu jornada</p>
                    
                    <div class="discord-info">
                        <div class="discord-info-title">🔗 Instrucciones</div>
                        <div class="discord-info-text">
                            Leer esta norma para que puedas fichar correctamente.<br><br>
                            <strong>Pasos necesarios:</strong><br>
                            1. Busca tu nombre en la lista<br>
                            2. Haz clic en tu nombre<br>
                            3. Haz clic en "Confirmar Entrada"<br>
                            4. Si todo está correcto, verás un mensaje de confirmación<br>
                            5. Si no todo está correcto, verás un mensaje de error
                            <br><br>
                            <strong>Siempre que quieras finalizar tu jornada:</strong><br>
                            1. Haz clic en "Finalizar Jornada"<br>
                            2. Si todo está correcto, verás un mensaje de confirmación<br>
                            3. Si no todo está correcto, verás un mensaje de error
                        </div>
                    </div>
                </div>

                <div id="statusPanel" class="status-panel hidden">
                    <div class="status-badge">✓ En Servicio</div>
                    <div class="employee-name-display" id="employeeNameDisplay"></div>
                    <div class="timer-display" id="timerDisplay">00:00:00</div>
                    <div class="stats-grid">
                        <div class="stat-card">
                            <div class="stat-icon">🕐</div>
                            <div class="stat-value" id="entryTime">--:--</div>
                            <div class="stat-label">Hora de Entrada</div>
                        </div>
                        <div class="stat-card">
                            <div class="stat-icon">⏱️</div>
                            <div class="stat-value" id="totalTime">0h 0m</div>
                            <div class="stat-label">Tiempo Total</div>
                        </div>
                    </div>
                    <button class="btn btn-danger" onclick="clockOut()">
                        <span>🚪 Finalizar Jornada</span>
                    </button>
                </div>
            </div>
        </div>
    </div>

    <div id="notificationContainer"></div>

    <script>
        const WEBHOOK_URL = 'https://discord.com/api/webhooks/1422188599360618597/JEr81dPlFVzJSRkTaYNF88dsfbz5_toyWNQE2lNmXN99na2l_8P9vYUMdf6mWfmADLVj';
        
        const DISCORD_BOT_CONFIG = {
            enabled: false,
            botToken: '',
            guildId: '',
            roleId: '',
            employeeDiscordIds: {}
        };
        
        const EMPLOYEES = {
            'Chloe': { surname: 'Brown', rank: 'Jefa' },
            'Alisha': { surname: 'Manrry', rank: 'Encargada' },
            'Zoe': { surname: 'Ross', rank: 'Experimentada' },
            'Alan': { surname: 'Riley', rank: 'Prácticas' },
            'Malik': { surname: 'Keller', rank: 'Prácticas' },
            'Isabella': { surname: 'Vera', rank: 'Prácticas' },
            'Ian': { surname: 'Smith', rank: 'Prácticas' },
            'Alejandro': { surname: 'Fernandez', rank: 'Prácticas' },
            'Moira': { surname: 'Vera', rank: 'Prácticas' },
            'Woody': { surname: 'Brook', rank: 'Prácticas' },
        };

        let startTime, timerInterval, sessionData = {}, selectedEmployee = null, recentEmployees = [];
        let pendingClockIn = null;

        function createParticles() {
            const container = document.getElementById('particles');
            for (let i = 0; i < 20; i++) {
                const particle = document.createElement('div');
                particle.className = 'particle';
                particle.style.width = Math.random() * 6 + 2 + 'px';
                particle.style.height = particle.style.width;
                particle.style.left = Math.random() * 100 + '%';
                particle.style.top = Math.random() * 100 + '%';
                particle.style.animationDelay = Math.random() * 15 + 's';
                particle.style.animationDuration = (Math.random() * 10 + 10) + 's';
                container.appendChild(particle);
            }
        }

        function loadEmployees() {
            const allPanel = document.getElementById('allPanel');
            const azPanel = document.getElementById('azPanel');
            
            allPanel.innerHTML = '';
            Object.entries(EMPLOYEES).forEach(([name, data]) => {
                allPanel.appendChild(createEmployeeItem(name, data.surname, data.rank));
            });

            const sorted = Object.entries(EMPLOYEES).sort((a, b) => a[0].localeCompare(b[0]));
            const grouped = {};
            sorted.forEach(([name, data]) => {
                const letter = name[0].toUpperCase();
                if (!grouped[letter]) grouped[letter] = [];
                grouped[letter].push([name, data.surname, data.rank]);
            });

            azPanel.innerHTML = '';
            Object.entries(grouped).forEach(([letter, employees]) => {
                const group = document.createElement('div');
                group.className = 'letter-group';
                group.innerHTML = `<div class="letter-header">${letter}</div>`;
                employees.forEach(([name, surname, rank]) => {
                    group.appendChild(createEmployeeItem(name, surname, rank));
                });
                azPanel.appendChild(group);
            });

            updateRecentPanel();
        }

        function createEmployeeItem(name, surname, rank) {
            const item = document.createElement('div');
            item.className = 'employee-item';
            const fullName = `${name} ${surname}`;
            const initials = name[0] + (surname[0] || '');
            
            const rankClass = rank.toLowerCase()
                .normalize("NFD").replace(/[\u0300-\u036f]/g, "")
                .replace(/\s+/g, '-');
            
            item.innerHTML = `
                <div class="employee-avatar">${initials}</div>
                <div class="employee-info">
                    <div class="employee-name">${fullName}</div>
                    <div class="employee-rank rank-${rankClass}">${rank}</div>
                </div>
            `;
            
            item.onclick = () => selectEmployee(fullName, item);
            return item;
        }

        function updateRecentPanel() {
            const recentPanel = document.getElementById('recentPanel');
            recentPanel.innerHTML = '';
            
            if (recentEmployees.length === 0) {
                recentPanel.innerHTML = '<div style="text-align: center; color: #ffc0cb; padding: 40px;">😿 No hay fichajes recientes</div>';
                return;
            }

            recentEmployees.forEach(name => {
                const [firstName, ...rest] = name.split(' ');
                const surname = rest.join(' ');
                const employeeData = EMPLOYEES[firstName];
                const rank = employeeData ? employeeData.rank : 'Trabajador Fijo';
                recentPanel.appendChild(createEmployeeItem(firstName, surname, rank));
            });
        }

        function switchTab(tab) {
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
            
            event.target.classList.add('active');
            
            if (tab === 'all') document.getElementById('allPanel').classList.add('active');
            else if (tab === 'az') document.getElementById('azPanel').classList.add('active');
            else if (tab === 'recent') document.getElementById('recentPanel').classList.add('active');
        }

        function filterEmployees() {
            const search = document.getElementById('searchInput').value.toLowerCase();
            document.querySelectorAll('.employee-item').forEach(item => {
                const name = item.querySelector('.employee-name').textContent.toLowerCase();
                item.style.display = name.includes(search) ? 'flex' : 'none';
            });
        }

        function selectEmployee(name, element) {
            if (sessionData.active) {
                showNotification('error', '😿 Error', 'Ya hay una sesión activa. Debes desfichar primero.');
                return;
            }

            document.querySelectorAll('.employee-item').forEach(i => i.classList.remove('selected'));
            element.classList.add('selected');
            selectedEmployee = name;
            pendingClockIn = element;
            
            if (!recentEmployees.includes(name)) {
                recentEmployees.unshift(name);
                if (recentEmployees.length > 5) recentEmployees.pop();
                updateRecentPanel();
            }
            
            showConfirmationModal(name);
        }

        function showConfirmationModal(name) {
            const modal = document.getElementById('modalOverlay');
            const now = new Date();
            
            document.getElementById('modalEmployeeName').textContent = name;
            document.getElementById('modalTime').textContent = `🕐 ${now.toLocaleTimeString('es-ES', {
                hour: '2-digit',
                minute: '2-digit',
                second: '2-digit'
            })}`;
            
            modal.classList.add('show');
        }

        function cancelClockIn() {
            const modal = document.getElementById('modalOverlay');
            modal.classList.remove('show');
            
            if (pendingClockIn) {
                pendingClockIn.classList.remove('selected');
            }
            
            selectedEmployee = null;
            pendingClockIn = null;
            
            showNotification('info', '😺 Cancelado', 'Fichaje cancelado correctamente');
        }

        function confirmClockIn() {
            const modal = document.getElementById('modalOverlay');
            modal.classList.remove('show');
            clockIn();
        }

        function showNotification(type, title, message) {
            const container = document.getElementById('notificationContainer');
            const notification = document.createElement('div');
            notification.className = `notification ${type}`;
            
            const icons = {
                success: '✓',
                error: '✕',
                info: '😺',
                warning: '⚠'
            };
            
            notification.innerHTML = `
                <button class="notification-close" onclick="this.parentElement.remove()">✕</button>
                <div class="notification-header">
                    <div class="notification-icon">${icons[type]}</div>
                    <div class="notification-content">
                        <div class="notification-title">${title}</div>
                        <div class="notification-message">${message}</div>
                    </div>
                </div>
                <div class="notification-progress" style="color: ${
                    type === 'success' ? '#10b981' :
                    type === 'error' ? '#ef4444' :
                    type === 'info' ? '#ff69b4' : '#f59e0b'
                }"></div>
            `;
            
            container.appendChild(notification);
            
            setTimeout(() => notification.classList.add('show'), 10);
            setTimeout(() => {
                notification.classList.remove('show');
                setTimeout(() => notification.remove(), 500);
            }, 5000);
        }

        async function assignDiscordRole(employeeName, action) {
            if (!DISCORD_BOT_CONFIG.enabled) {
                return false;
            }

            const discordId = DISCORD_BOT_CONFIG.employeeDiscordIds[employeeName];
            if (!discordId) {
                return false;
            }

            const endpoint = action === 'add' ? 
                `https://discord.com/api/v10/guilds/${DISCORD_BOT_CONFIG.guildId}/members/${discordId}/roles/${DISCORD_BOT_CONFIG.roleId}` :
                `https://discord.com/api/v10/guilds/${DISCORD_BOT_CONFIG.guildId}/members/${discordId}/roles/${DISCORD_BOT_CONFIG.roleId}`;

            try {
                const response = await fetch(endpoint, {
                    method: action === 'add' ? 'PUT' : 'DELETE',
                    headers: {
                        'Authorization': `Bot ${DISCORD_BOT_CONFIG.botToken}`,
                        'Content-Type': 'application/json'
                    }
                });

                if (response.ok || response.status === 204) {
                    return true;
                }
                return false;
            } catch (error) {
                return false;
            }
        }

        async function clockIn() {
            if (!selectedEmployee) {
                showNotification('error', '😿 Error', 'Debes seleccionar un empleado primero.');
                return;
            }

            startTime = new Date();
            sessionData = {
                active: true,
                employee: selectedEmployee,
                startTime: startTime.toISOString(),
                totalMinutes: 0
            };
            
            document.getElementById('welcomeScreen').classList.add('hidden');
            document.getElementById('statusPanel').classList.remove('hidden');
            document.getElementById('employeeNameDisplay').textContent = selectedEmployee + ' 😺';
            document.getElementById('entryTime').textContent = startTime.toLocaleTimeString('es-ES', {
                hour: '2-digit',
                minute: '2-digit'
            });
            
            document.getElementById('activeNow').textContent = '1';
            
            timerInterval = setInterval(updateTimer, 1000);
            showNotification('success', '✓ Fichaje Registrado', 
                `${selectedEmployee} ha iniciado su jornada a las ${startTime.toLocaleTimeString('es-ES')}`);
            
            await assignDiscordRole(selectedEmployee, 'add');
        }

        function updateTimer() {
            if (!startTime) return;
            
            const now = new Date();
            const elapsed = Math.floor((now - startTime) / 1000);
            
            const hours = Math.floor(elapsed / 3600);
            const minutes = Math.floor((elapsed % 3600) / 60);
            const seconds = elapsed % 60;
            
            document.getElementById('timerDisplay').textContent = 
                `${String(hours).padStart(2, '0')}:${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
            
            const totalMinutes = Math.floor(elapsed / 60);
            const displayHours = Math.floor(totalMinutes / 60);
            const displayMinutes = totalMinutes % 60;
            document.getElementById('totalTime').textContent = `${displayHours}h ${displayMinutes}m`;
        }

        async function clockOut() {
            if (!startTime || !sessionData.active) return;
            
            const endTime = new Date();
            const sessionMinutes = Math.floor((endTime - startTime) / 60000);
            const sessionHours = Math.floor(sessionMinutes / 60);
            const sessionMins = sessionMinutes % 60;
            
            const embedData = {
                embeds: [{
                    title: "😺 UwU Café - Registro de Fichaje",
                    description: "Un empleado ha finalizado su jornada",
                    color: 0xFF69B4,
                    fields: [
                        {
                            name: "👤 Empleado",
                            value: sessionData.employee,
                            inline: true
                        },
                        {
                            name: "🕐 Hora de Entrada",
                            value: startTime.toLocaleTimeString('es-ES'),
                            inline: true
                        },
                        {
                            name: "🕐 Hora de Salida",
                            value: endTime.toLocaleTimeString('es-ES'),
                            inline: true
                        },
                        {
                            name: "⏱️ Duración de la Sesión",
                            value: `${sessionHours}h ${sessionMins}m`,
                            inline: true
                        },
                        {
                            name: "📅 Fecha",
                            value: new Date().toLocaleDateString('es-ES', {
                                weekday: 'long',
                                year: 'numeric',
                                month: 'long',
                                day: 'numeric'
                            }),
                            inline: false
                        }
                    ],
                    footer: {
                        text: "UwU Café - Sistema de Fichajes ✨"
                    },
                    timestamp: new Date().toISOString()
                }]
            };
            
            showNotification('info', '⏳ Procesando...', 'Registrando tu fichaje de salida.');
            
            if (WEBHOOK_URL) {
                fetch(WEBHOOK_URL, {
                    method: 'POST',
                    headers: {'Content-Type': 'application/json'},
                    body: JSON.stringify(embedData)
                })
                .then(response => {
                    if (response.ok) {
                        showNotification('success', '✓ Fichaje Completado', 
                            `Sesión de ${sessionHours}h ${sessionMins}m registrada correctamente en Discord.`);
                    } else {
                        showNotification('warning', '⚠️ Advertencia', 
                            'El fichaje se completó pero hubo un problema al enviar a Discord.');
                    }
                })
                .catch(error => {
                    showNotification('error', '✗ Error de Conexión', 
                        'No se pudo conectar con Discord. Verifica tu conexión.');
                });
            }
            
            await assignDiscordRole(sessionData.employee, 'remove');
            
            clearInterval(timerInterval);
            sessionData = {};
            startTime = null;
            selectedEmployee = null;
            pendingClockIn = null;
            
            document.getElementById('statusPanel').classList.add('hidden');
            document.getElementById('welcomeScreen').classList.remove('hidden');
            document.getElementById('timerDisplay').textContent = '00:00:00';
            document.getElementById('activeNow').textContent = '0';
            
            document.querySelectorAll('.employee-item').forEach(item => {
                item.classList.remove('selected');
            });
        }

        document.getElementById('modalOverlay').addEventListener('click', function(e) {
            if (e.target === this) {
                cancelClockIn();
            }
        });

        window.onload = () => {
            createParticles();
            loadEmployees();
            document.getElementById('totalEmployees').textContent = Object.keys(EMPLOYEES).length;
        };
    </script>
</body>
</html>
