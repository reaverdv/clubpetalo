<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Club Pétalo - Sistema de Fichajes</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1a0a1e 0%, #2d1b3d 50%, #1a0a1e 100%);
            min-height: 100vh;
            position: relative;
            overflow-x: hidden;
            color: white;
        }

        .animated-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
            overflow: hidden;
        }

        .orb {
            position: absolute;
            border-radius: 50%;
            filter: blur(60px);
            opacity: 0.4;
            animation: float 20s infinite ease-in-out;
        }

        .orb1 {
            width: 400px;
            height: 400px;
            background: radial-gradient(circle, #ff69b4, transparent);
            top: 10%;
            left: 10%;
            animation-delay: 0s;
        }

        .orb2 {
            width: 350px;
            height: 350px;
            background: radial-gradient(circle, #d946ef, transparent);
            bottom: 20%;
            right: 10%;
            animation-delay: 7s;
        }

        .orb3 {
            width: 300px;
            height: 300px;
            background: radial-gradient(circle, #ec4899, transparent);
            top: 50%;
            left: 50%;
            animation-delay: 14s;
        }

        @keyframes float {
            0%, 100% {
                transform: translate(0, 0) scale(1);
            }
            25% {
                transform: translate(100px, -50px) scale(1.1);
            }
            50% {
                transform: translate(-50px, 100px) scale(0.9);
            }
            75% {
                transform: translate(80px, 50px) scale(1.05);
            }
        }

        .petals {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 1;
        }

        .petal {
            position: absolute;
            width: 15px;
            height: 15px;
            background: radial-gradient(ellipse at center, #ff69b4, #ffb6c1);
            border-radius: 50% 0 50% 0;
            animation: fall linear infinite;
            transform-origin: center;
            opacity: 0.6;
        }

        @keyframes fall {
            0% {
                transform: translateY(-100vh) rotate(0deg);
                opacity: 0.6;
            }
            100% {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }

        .container {
            display: grid;
            grid-template-columns: 1fr 320px;
            gap: 20px;
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 10;
            min-height: 100vh;
        }

        .main-content {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .header {
            text-align: center;
            background: rgba(26, 10, 30, 0.8);
            backdrop-filter: blur(20px);
            padding: 40px;
            border-radius: 30px;
            box-shadow: 0 20px 60px rgba(255, 105, 180, 0.3);
            border: 2px solid rgba(255, 105, 180, 0.2);
            animation: slideDown 0.8s ease-out;
        }

        @keyframes slideDown {
            from {
                transform: translateY(-50px);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }

        .header h1 {
            font-size: 3.5em;
            font-weight: bold;
            margin-bottom: 10px;
            background: linear-gradient(45deg, #ff69b4, #d946ef, #ec4899);
            background-size: 200% 200%;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            animation: gradientShift 3s ease infinite;
        }

        @keyframes gradientShift {
            0%, 100% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
        }

        .card {
            background: rgba(26, 10, 30, 0.85);
            backdrop-filter: blur(20px);
            border-radius: 30px;
            padding: 40px;
            box-shadow: 0 20px 60px rgba(255, 105, 180, 0.2);
            border: 2px solid rgba(255, 105, 180, 0.2);
            animation: fadeIn 0.8s ease-out;
            transition: transform 0.3s ease;
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 25px 70px rgba(255, 105, 180, 0.3);
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: scale(0.95);
            }
            to {
                opacity: 1;
                transform: scale(1);
            }
        }

        .status-card {
            text-align: center;
            min-height: 400px;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .status-text {
            font-size: 1.8em;
            color: #ff69b4;
            margin-bottom: 20px;
            font-weight: bold;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.8; transform: scale(1.05); }
        }

        .timer {
            font-size: 4em;
            font-weight: bold;
            background: linear-gradient(45deg, #ff69b4, #d946ef);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 30px;
            font-family: 'Courier New', monospace;
            text-shadow: 0 0 30px rgba(255, 105, 180, 0.5);
        }

        .stats {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin: 30px 0;
        }

        .stat-item {
            background: linear-gradient(135deg, rgba(255, 105, 180, 0.2), rgba(217, 70, 239, 0.2));
            padding: 25px;
            border-radius: 20px;
            text-align: center;
            border: 1px solid rgba(255, 105, 180, 0.3);
            transition: all 0.3s ease;
            animation: slideUp 0.6s ease-out;
        }

        .stat-item:hover {
            transform: scale(1.05);
            background: linear-gradient(135deg, rgba(255, 105, 180, 0.3), rgba(217, 70, 239, 0.3));
        }

        @keyframes slideUp {
            from {
                transform: translateY(30px);
                opacity: 0;
            }
            to {
                transform: translateY(0);
                opacity: 1;
            }
        }

        .stat-value {
            font-size: 2em;
            font-weight: bold;
            color: #ff69b4;
        }

        .stat-label {
            font-size: 0.9em;
            color: #d1a3c4;
            margin-top: 8px;
        }

        .btn {
            padding: 18px 40px;
            border: none;
            border-radius: 20px;
            font-size: 1.2em;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.4s ease;
            text-transform: uppercase;
            letter-spacing: 2px;
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
            background: rgba(255, 255, 255, 0.3);
            transform: translate(-50%, -50%);
            transition: width 0.6s, height 0.6s;
        }

        .btn:hover::before {
            width: 300px;
            height: 300px;
        }

        .btn span {
            position: relative;
            z-index: 1;
        }

        .btn-danger {
            background: linear-gradient(45deg, #dc3545, #c82333);
            color: white;
            box-shadow: 0 10px 30px rgba(220, 53, 69, 0.4);
        }

        .btn-danger:hover {
            transform: scale(1.05);
            box-shadow: 0 15px 40px rgba(220, 53, 69, 0.6);
        }

        .employees-sidebar {
            position: sticky;
            top: 20px;
            height: fit-content;
            max-height: calc(100vh - 40px);
            overflow-y: auto;
        }

        .employees-sidebar::-webkit-scrollbar {
            width: 8px;
        }

        .employees-sidebar::-webkit-scrollbar-track {
            background: rgba(255, 105, 180, 0.1);
            border-radius: 10px;
        }

        .employees-sidebar::-webkit-scrollbar-thumb {
            background: linear-gradient(135deg, #ff69b4, #d946ef);
            border-radius: 10px;
        }

        .employees-card {
            background: rgba(26, 10, 30, 0.85);
            backdrop-filter: blur(20px);
            border-radius: 30px;
            padding: 30px;
            box-shadow: 0 20px 60px rgba(255, 105, 180, 0.2);
            border: 2px solid rgba(255, 105, 180, 0.2);
            animation: slideLeft 0.8s ease-out;
        }

        @keyframes slideLeft {
            from {
                transform: translateX(50px);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }

        .employees-title {
            font-size: 1.5em;
            font-weight: bold;
            margin-bottom: 20px;
            text-align: center;
            background: linear-gradient(45deg, #ff69b4, #d946ef);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .employee-item {
            background: linear-gradient(135deg, rgba(255, 105, 180, 0.15), rgba(217, 70, 239, 0.15));
            padding: 15px 20px;
            margin-bottom: 12px;
            border-radius: 15px;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 2px solid transparent;
            animation: fadeInLeft 0.5s ease-out backwards;
        }

        .employee-item:nth-child(2) { animation-delay: 0.1s; }
        .employee-item:nth-child(3) { animation-delay: 0.2s; }
        .employee-item:nth-child(4) { animation-delay: 0.3s; }
        .employee-item:nth-child(5) { animation-delay: 0.4s; }
        .employee-item:nth-child(6) { animation-delay: 0.5s; }
        .employee-item:nth-child(7) { animation-delay: 0.6s; }
        .employee-item:nth-child(8) { animation-delay: 0.7s; }
        .employee-item:nth-child(9) { animation-delay: 0.8s; }
        .employee-item:nth-child(10) { animation-delay: 0.9s; }
        .employee-item:nth-child(11) { animation-delay: 1s; }

        @keyframes fadeInLeft {
            from {
                transform: translateX(-30px);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }

        .employee-item:hover {
            background: linear-gradient(135deg, rgba(255, 105, 180, 0.3), rgba(217, 70, 239, 0.3));
            transform: translateX(10px) scale(1.05);
            border-color: #ff69b4;
            box-shadow: 0 5px 20px rgba(255, 105, 180, 0.4);
        }

        .employee-item.selected {
            background: linear-gradient(135deg, #ff69b4, #d946ef);
            border-color: #fff;
            transform: scale(1.05);
            box-shadow: 0 8px 25px rgba(255, 105, 180, 0.5);
        }

        .employee-name {
            font-weight: 600;
            font-size: 1.1em;
        }

        .hidden {
            display: none;
        }

        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: rgba(26, 10, 30, 0.95);
            backdrop-filter: blur(20px);
            border-radius: 20px;
            padding: 25px 30px;
            box-shadow: 0 15px 40px rgba(255, 105, 180, 0.4);
            border: 2px solid;
            z-index: 1000;
            min-width: 320px;
            transform: translateX(400px);
            opacity: 0;
            transition: all 0.5s cubic-bezier(0.68, -0.55, 0.265, 1.55);
        }

        .notification.show {
            transform: translateX(0);
            opacity: 1;
        }

        .notification.success { border-color: #28a745; }
        .notification.error { border-color: #dc3545; }
        .notification.info { border-color: #17a2b8; }

        .notification-header {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
            font-size: 1.2em;
            font-weight: bold;
        }

        .notification-header.success { color: #28a745; }
        .notification-header.error { color: #dc3545; }
        .notification-header.info { color: #17a2b8; }

        .notification-icon {
            font-size: 1.5em;
            margin-right: 12px;
            animation: iconBounce 0.6s ease;
        }

        @keyframes iconBounce {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.3) rotate(10deg); }
        }

        .notification-body {
            color: #e0e0e0;
            font-size: 1em;
            line-height: 1.4;
        }

        .notification-progress {
            height: 4px;
            background: linear-gradient(90deg, #ff69b4, #d946ef);
            border-radius: 2px;
            margin-top: 15px;
            animation: progressBar 3s linear;
            transform-origin: left;
        }

        @keyframes progressBar {
            from { transform: scaleX(1); }
            to { transform: scaleX(0); }
        }

        @media (max-width: 1024px) {
            .container {
                grid-template-columns: 1fr;
            }
            
            .employees-sidebar {
                position: relative;
                top: 0;
                max-height: none;
            }

            .header h1 {
                font-size: 2.5em;
            }

            .timer {
                font-size: 3em;
            }
        }

        @media (max-width: 768px) {
            .header h1 {
                font-size: 2em;
            }

            .timer {
                font-size: 2.5em;
            }

            .stats {
                grid-template-columns: 1fr;
            }

            .notification {
                right: 10px;
                left: 10px;
                min-width: auto;
            }
        }
    </style>
</head>
<body>
    <div class="animated-bg">
        <div class="orb orb1"></div>
        <div class="orb orb2"></div>
        <div class="orb orb3"></div>
    </div>
    
    <div class="petals" id="petals"></div>
    
    <div class="container">
        <div class="main-content">
            <div class="header">
                <h1>🌸 CLUB PÉTALO 🌸</h1>
                <p style="color: #ff69b4; font-size: 1.3em; margin-top: 10px;">Sistema de Fichajes</p>
            </div>

            <div class="card">
                <div id="loginForm">
                    <div style="text-align: center; padding: 60px 0;">
                        <div style="font-size: 2em; color: #ff69b4; margin-bottom: 20px;">👈</div>
                        <h2 style="color: #ff69b4; font-size: 1.8em;">Selecciona tu nombre</h2>
                        <p style="color: #d1a3c4; margin-top: 10px; font-size: 1.1em;">Haz clic en tu nombre para fichar</p>
                    </div>
                </div>

                <div id="statusPanel" class="hidden">
                    <div class="status-card">
                        <div class="status-text">¡Trabajando! 💪</div>
                        <div id="nombreCompleto" class="status-text"></div>
                        <div class="timer" id="timer">00:00:00</div>
                        <div class="stats">
                            <div class="stat-item">
                                <div class="stat-value" id="horaEntrada">--:--</div>
                                <div class="stat-label">Hora de Entrada</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-value" id="totalHoras">0h 0m</div>
                                <div class="stat-label">Total Acumulado</div>
                            </div>
                        </div>
                        <button class="btn btn-danger" onclick="desfichar()">
                            <span>🌸 Desfichar Salida 🌸</span>
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <aside class="employees-sidebar">
            <div class="employees-card">
                <div class="employees-title">👥 Empleados</div>
                <div id="employeesList"></div>
            </div>
        </aside>
    </div>

    <div id="notificationContainer"></div>

    <script>
        const WEBHOOK_URL = 'https://discord.com/api/webhooks/1422188599360618597/JEr81dPlFVzJSRkTaYNF88dsfbz5_toyWNQE2lNmXN99na2l_8P9vYUMdf6mWfmADLVj';
        
        const EMPLEADOS = {
            'Chloe': 'Brown',
            'Selina': 'Gibson',
            'Zoe': 'Ross',
            'Ahmed': 'alim',
            'Alisha': 'Manrry',
            'khalil': 'Brown',
            'Alan': 'Riley',
            'Malik': 'Keller',
            'Isabella': 'Vera',
            'Hinako': 'Mizuki',
        };

        let startTime;
        let timerInterval;
        let userData = {};
        let selectedEmployee = null;

        function loadEmpleados() {
            const list = document.getElementById('employeesList');
            for (const [nombre, apellidos] of Object.entries(EMPLEADOS)) {
                const item = document.createElement('div');
                item.className = 'employee-item';
                item.innerHTML = `<div class="employee-name">${nombre} ${apellidos}</div>`;
                item.onclick = () => selectEmployee(`${nombre} ${apellidos}`, item);
                list.appendChild(item);
            }
        }

        function selectEmployee(nombre, element) {
            if (userData.activeSession) {
                showNotification('error', 'Error', 'Ya hay una sesión activa');
                return;
            }

            document.querySelectorAll('.employee-item').forEach(item => {
                item.classList.remove('selected');
            });
            
            element.classList.add('selected');
            selectedEmployee = nombre;
            fichar();
        }

        function showNotification(type, title, message) {
            const container = document.getElementById('notificationContainer');
            
            const notification = document.createElement('div');
            notification.className = `notification ${type}`;
            
            const iconMap = {
                success: '✅',
                error: '❌',
                info: 'ℹ️'
            };
            
            notification.innerHTML = `
                <div class="notification-header ${type}">
                    <span class="notification-icon">${iconMap[type]}</span>
                    <span>${title}</span>
                </div>
                <div class="notification-body">${message}</div>
                <div class="notification-progress"></div>
            `;
            
            container.appendChild(notification);
            
            setTimeout(() => notification.classList.add('show'), 10);
            
            setTimeout(() => {
                notification.classList.remove('show');
                setTimeout(() => {
                    if (notification.parentNode) {
                        notification.parentNode.removeChild(notification);
                    }
                }, 500);
            }, 3000);
        }

        function createPetals() {
            const petalsContainer = document.getElementById('petals');
            
            function createPetal() {
                const petal = document.createElement('div');
                petal.className = 'petal';
                petal.style.left = Math.random() * 100 + '%';
                petal.style.animationDuration = (Math.random() * 3 + 2) + 's';
                petal.style.animationDelay = Math.random() * 2 + 's';
                petalsContainer.appendChild(petal);
                
                setTimeout(() => {
                    if (petal.parentNode) {
                        petal.parentNode.removeChild(petal);
                    }
                }, 5000);
            }
            
            setInterval(createPetal, 300);
        }

        function loadUserData() {
            // Usando variables en memoria en lugar de localStorage
            userData = {
                totalMinutes: 0,
                sessions: [],
                activeSession: null
            };
            updateTotalHoras();
        }

        function restoreActiveSession() {
            const session = userData.activeSession;
            startTime = new Date(session.startTime);
            selectedEmployee = session.nombre;
            
            document.getElementById('loginForm').classList.add('hidden');
            document.getElementById('statusPanel').classList.remove('hidden');
            document.getElementById('nombreCompleto').textContent = session.nombre;
            document.getElementById('horaEntrada').textContent = startTime.toLocaleTimeString('es-ES', {hour: '2-digit', minute: '2-digit'});
            
            timerInterval = setInterval(updateTimer, 1000);
            updateTimer();
            
            showNotification('info', '¡Sesión Restaurada!', `Continuando tu fichaje desde las ${startTime.toLocaleTimeString('es-ES')}`);
        }

        function saveActiveSession(nombre) {
            userData.activeSession = {
                startTime: startTime.toISOString(),
                nombre: nombre
            };
        }

        function clearActiveSession() {
            userData.activeSession = null;
        }

        function formatTime(minutes) {
            const hours = Math.floor(minutes / 60);
            const mins = minutes % 60;
            return `${hours}h ${mins}m`;
        }

        function formatTimer(seconds) {
            const hours = Math.floor(seconds / 3600);
            const minutes = Math.floor((seconds % 3600) / 60);
            const secs = seconds % 60;
            return `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
        }

        function updateTotalHoras() {
            document.getElementById('totalHoras').textContent = formatTime(userData.totalMinutes);
        }

        function fichar() {
            if (!selectedEmployee) {
                showNotification('error', 'Error', 'Por favor, selecciona un empleado');
                return;
            }

            startTime = new Date();
            
            saveActiveSession(selectedEmployee);
            
            document.getElementById('loginForm').classList.add('hidden');
            document.getElementById('statusPanel').classList.remove('hidden');
            document.getElementById('nombreCompleto').textContent = selectedEmployee;
            document.getElementById('horaEntrada').textContent = startTime.toLocaleTimeString('es-ES', {hour: '2-digit', minute: '2-digit'});
            
            timerInterval = setInterval(updateTimer, 1000);
            
            showNotification('success', '¡Fichaje Registrado!', `Hora de entrada: ${startTime.toLocaleTimeString('es-ES')}`);
        }

        function updateTimer() {
            if (!startTime) return;
            
            const now = new Date();
            const elapsed = Math.floor((now - startTime) / 1000);
            document.getElementById('timer').textContent = formatTimer(elapsed);
        }

        function desfichar() {
            if (!startTime) return;
            
            const endTime = new Date();
            const sessionMinutes = Math.floor((endTime - startTime) / 60000);
            
            userData.totalMinutes += sessionMinutes;
            userData.sessions.push({
                start: startTime.toISOString(),
                end: endTime.toISOString(),
                minutes: sessionMinutes
            });
            
            const nombre = document.getElementById('nombreCompleto').textContent;
            
            clearActiveSession();
            
            const embedData = {
                embeds: [{
                    title: "🌸 Club Pétalo - Registro de Fichaje 🌸",
                    color: 0xFF69B4,
                    fields: [
                        {
                            name: "👤 Empleado",
                            value: nombre,
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
                            name: "⏱️ Horas Trabajadas (Sesión)",
                            value: formatTime(sessionMinutes),
                            inline: true
                        },
                        {
                            name: "📊 Total Horas Acumuladas",
                            value: formatTime(userData.totalMinutes),
                            inline: true
                        },
                        {
                            name: "📅 Fecha",
                            value: new Date().toLocaleDateString('es-ES'),
                            inline: true
                        }
                    ],
                    footer: {
                        text: "Club Pétalo - Sistema de Fichajes"
                    },
                    timestamp: new Date().toISOString()
                }]
            };
            
            showNotification('info', '¡Desfichaje Registrado!', `Sesión de ${formatTime(sessionMinutes)} completada`);
            updateTotalHoras();
            
            if (WEBHOOK_URL) {
                fetch(WEBHOOK_URL, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify(embedData)
                }).then(response => {
                    if (response.ok) {
                        showNotification('success', '¡Webhook Enviado!', 'Registro guardado en Discord correctamente');
                    } else {
                        showNotification('error', 'Error en Webhook', 'Verifica la URL del webhook configurada');
                    }
                }).catch(error => {
                    console.error('Error:', error);
                    showNotification('error', 'Error de Conexión', 'No se pudo conectar con Discord');
                });
            }
            
            clearInterval(timerInterval);
            
            document.getElementById('loginForm').classList.remove('hidden');
            document.getElementById('statusPanel').classList.add('hidden');
            document.getElementById('timer').textContent = '00:00:00';
            
            document.querySelectorAll('.employee-item').forEach(item => {
                item.classList.remove('selected');
            });
            
            selectedEmployee = null;
            startTime = null;
        }

        window.onload = function() {
            loadEmpleados();
            loadUserData();
            createPetals();
        };
    </script>
</body>
</html>
