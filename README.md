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
            color: white;
            overflow-x: hidden;
        }

        .animated-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        .orb {
            position: absolute;
            border-radius: 50%;
            filter: blur(60px);
            opacity: 0.4;
            animation: float 20s infinite ease-in-out;
        }

        .orb1 {
            width: 300px;
            height: 300px;
            background: radial-gradient(circle, #ff69b4, transparent);
            top: 10%;
            left: 10%;
        }

        .orb2 {
            width: 250px;
            height: 250px;
            background: radial-gradient(circle, #d946ef, transparent);
            bottom: 20%;
            right: 10%;
            animation-delay: 7s;
        }

        @keyframes float {
            0%, 100% { transform: translate(0, 0); }
            50% { transform: translate(50px, 50px); }
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 15px;
            position: relative;
            z-index: 10;
        }

        .header {
            text-align: center;
            background: rgba(26, 10, 30, 0.8);
            backdrop-filter: blur(20px);
            padding: 20px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(255, 105, 180, 0.3);
            border: 2px solid rgba(255, 105, 180, 0.2);
            margin-bottom: 15px;
        }

        .header h1 {
            font-size: 2em;
            font-weight: bold;
            background: linear-gradient(45deg, #ff69b4, #d946ef);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .header p {
            color: #ff69b4;
            font-size: 0.9em;
            margin-top: 5px;
        }

        .main-grid {
            display: grid;
            grid-template-columns: 250px 1fr;
            gap: 15px;
        }

        .card {
            background: rgba(26, 10, 30, 0.85);
            backdrop-filter: blur(20px);
            border-radius: 20px;
            padding: 20px;
            box-shadow: 0 10px 30px rgba(255, 105, 180, 0.2);
            border: 2px solid rgba(255, 105, 180, 0.2);
        }

        .employees-card {
            max-height: calc(100vh - 150px);
            overflow-y: auto;
        }

        .employees-card::-webkit-scrollbar {
            width: 6px;
        }

        .employees-card::-webkit-scrollbar-thumb {
            background: linear-gradient(135deg, #ff69b4, #d946ef);
            border-radius: 10px;
        }

        .employees-title {
            font-size: 1.2em;
            font-weight: bold;
            margin-bottom: 15px;
            text-align: center;
            background: linear-gradient(45deg, #ff69b4, #d946ef);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .employee-item {
            background: linear-gradient(135deg, rgba(255, 105, 180, 0.15), rgba(217, 70, 239, 0.15));
            padding: 10px 15px;
            margin-bottom: 8px;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 2px solid transparent;
            font-size: 0.95em;
        }

        .employee-item:hover {
            background: linear-gradient(135deg, rgba(255, 105, 180, 0.3), rgba(217, 70, 239, 0.3));
            transform: translateX(5px);
            border-color: #ff69b4;
        }

        .employee-item.selected {
            background: linear-gradient(135deg, #ff69b4, #d946ef);
            border-color: #fff;
        }

        .status-card {
            text-align: center;
            padding: 30px 20px;
        }

        .status-text {
            font-size: 1.3em;
            color: #ff69b4;
            margin-bottom: 15px;
            font-weight: bold;
        }

        .timer {
            font-size: 2.5em;
            font-weight: bold;
            background: linear-gradient(45deg, #ff69b4, #d946ef);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 20px;
            font-family: 'Courier New', monospace;
        }

        .stats {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin: 20px 0;
        }

        .stat-item {
            background: linear-gradient(135deg, rgba(255, 105, 180, 0.2), rgba(217, 70, 239, 0.2));
            padding: 15px;
            border-radius: 15px;
            text-align: center;
            border: 1px solid rgba(255, 105, 180, 0.3);
        }

        .stat-value {
            font-size: 1.5em;
            font-weight: bold;
            color: #ff69b4;
        }

        .stat-label {
            font-size: 0.85em;
            color: #d1a3c4;
            margin-top: 5px;
        }

        .btn {
            padding: 12px 30px;
            border: none;
            border-radius: 15px;
            font-size: 1em;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .btn-danger {
            background: linear-gradient(45deg, #dc3545, #c82333);
            color: white;
            box-shadow: 0 5px 20px rgba(220, 53, 69, 0.4);
        }

        .btn-danger:hover {
            transform: scale(1.05);
        }

        .hidden {
            display: none;
        }

        .notification {
            position: fixed;
            top: 15px;
            right: 15px;
            background: rgba(26, 10, 30, 0.95);
            backdrop-filter: blur(20px);
            border-radius: 15px;
            padding: 15px 20px;
            box-shadow: 0 10px 30px rgba(255, 105, 180, 0.4);
            border: 2px solid;
            z-index: 1000;
            min-width: 280px;
            transform: translateX(400px);
            opacity: 0;
            transition: all 0.5s ease;
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
            margin-bottom: 8px;
            font-size: 1em;
            font-weight: bold;
        }

        .notification-header.success { color: #28a745; }
        .notification-header.error { color: #dc3545; }
        .notification-header.info { color: #17a2b8; }

        .notification-icon {
            font-size: 1.2em;
            margin-right: 10px;
        }

        .notification-body {
            color: #e0e0e0;
            font-size: 0.9em;
        }

        .login-placeholder {
            text-align: center;
            padding: 40px 20px;
        }

        .login-placeholder h2 {
            color: #ff69b4;
            font-size: 1.5em;
            margin-bottom: 10px;
        }

        .login-placeholder p {
            color: #d1a3c4;
            font-size: 1em;
        }

        @media (max-width: 768px) {
            .main-grid {
                grid-template-columns: 1fr;
            }

            .header h1 {
                font-size: 1.5em;
            }

            .timer {
                font-size: 2em;
            }

            .stats {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="animated-bg">
        <div class="orb orb1"></div>
        <div class="orb orb2"></div>
    </div>
    
    <div class="container">
        <div class="header">
            <h1>🌸 CLUB PÉTALO 🌸</h1>
            <p>Sistema de Fichajes</p>
        </div>

        <div class="main-grid">
            <div class="card employees-card">
                <div class="employees-title">👥 Empleados</div>
                <div id="employeesList"></div>
            </div>

            <div class="card">
                <div id="loginForm">
                    <div class="login-placeholder">
                        <div style="font-size: 2em; margin-bottom: 15px;">👈</div>
                        <h2>Selecciona tu nombre</h2>
                        <p>Haz clic en tu nombre para fichar</p>
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
                                <div class="stat-label">Entrada</div>
                            </div>
                            <div class="stat-item">
                                <div class="stat-value" id="totalHoras">0h 0m</div>
                                <div class="stat-label">Total</div>
                            </div>
                        </div>
                        <button class="btn btn-danger" onclick="desfichar()">
                            🌸 Desfichar Salida 🌸
                        </button>
                    </div>
                </div>
            </div>
        </div>
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
            'Hinako': 'Mizuki',
            'Hinako': 'Mizuki',
            'Hinako': 'Mizuki',
            'Hinako': 'Mizuki',
        };

        let startTime, timerInterval, userData = {}, selectedEmployee = null;

        function loadEmpleados() {
            const list = document.getElementById('employeesList');
            for (const [nombre, apellidos] of Object.entries(EMPLEADOS)) {
                const item = document.createElement('div');
                item.className = 'employee-item';
                item.textContent = `${nombre} ${apellidos}`;
                item.onclick = () => selectEmployee(`${nombre} ${apellidos}`, item);
                list.appendChild(item);
            }
        }

        function selectEmployee(nombre, element) {
            if (userData.activeSession) {
                showNotification('error', 'Error', 'Ya hay una sesión activa');
                return;
            }
            document.querySelectorAll('.employee-item').forEach(i => i.classList.remove('selected'));
            element.classList.add('selected');
            selectedEmployee = nombre;
            fichar();
        }

        function showNotification(type, title, message) {
            const container = document.getElementById('notificationContainer');
            const notification = document.createElement('div');
            notification.className = `notification ${type}`;
            const icons = {success: '✅', error: '❌', info: 'ℹ️'};
            
            notification.innerHTML = `
                <div class="notification-header ${type}">
                    <span class="notification-icon">${icons[type]}</span>
                    <span>${title}</span>
                </div>
                <div class="notification-body">${message}</div>
            `;
            
            container.appendChild(notification);
            setTimeout(() => notification.classList.add('show'), 10);
            setTimeout(() => {
                notification.classList.remove('show');
                setTimeout(() => notification.remove(), 500);
            }, 3000);
        }

        function loadUserData() {
            userData = {totalMinutes: 0, sessions: [], activeSession: null};
            updateTotalHoras();
        }

        function saveActiveSession(nombre) {
            userData.activeSession = {startTime: startTime.toISOString(), nombre: nombre};
        }

        function clearActiveSession() {
            userData.activeSession = null;
        }

        function formatTime(minutes) {
            return `${Math.floor(minutes / 60)}h ${minutes % 60}m`;
        }

        function formatTimer(seconds) {
            const h = Math.floor(seconds / 3600);
            const m = Math.floor((seconds % 3600) / 60);
            const s = seconds % 60;
            return `${h.toString().padStart(2, '0')}:${m.toString().padStart(2, '0')}:${s.toString().padStart(2, '0')}`;
        }

        function updateTotalHoras() {
            document.getElementById('totalHoras').textContent = formatTime(userData.totalMinutes);
        }

        function fichar() {
            if (!selectedEmployee) {
                showNotification('error', 'Error', 'Selecciona un empleado');
                return;
            }

            startTime = new Date();
            saveActiveSession(selectedEmployee);
            
            document.getElementById('loginForm').classList.add('hidden');
            document.getElementById('statusPanel').classList.remove('hidden');
            document.getElementById('nombreCompleto').textContent = selectedEmployee;
            document.getElementById('horaEntrada').textContent = startTime.toLocaleTimeString('es-ES', {hour: '2-digit', minute: '2-digit'});
            
            timerInterval = setInterval(updateTimer, 1000);
            showNotification('success', '¡Fichaje Registrado!', `Entrada: ${startTime.toLocaleTimeString('es-ES')}`);
        }

        function updateTimer() {
            if (!startTime) return;
            const elapsed = Math.floor((new Date() - startTime) / 1000);
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
                        {name: "👤 Empleado", value: nombre, inline: true},
                        {name: "🕐 Entrada", value: startTime.toLocaleTimeString('es-ES'), inline: true},
                        {name: "🕐 Salida", value: endTime.toLocaleTimeString('es-ES'), inline: true},
                        {name: "⏱️ Sesión", value: formatTime(sessionMinutes), inline: true},
                        {name: "📊 Total", value: formatTime(userData.totalMinutes), inline: true},
                        {name: "📅 Fecha", value: new Date().toLocaleDateString('es-ES'), inline: true}
                    ],
                    footer: {text: "Club Pétalo"},
                    timestamp: new Date().toISOString()
                }]
            };
            
            showNotification('info', '¡Desfichaje!', `Sesión: ${formatTime(sessionMinutes)}`);
            updateTotalHoras();
            
            if (WEBHOOK_URL) {
                fetch(WEBHOOK_URL, {
                    method: 'POST',
                    headers: {'Content-Type': 'application/json'},
                    body: JSON.stringify(embedData)
                }).then(r => {
                    if (r.ok) showNotification('success', '✓ Webhook', 'Guardado en Discord');
                    else showNotification('error', '✗ Webhook', 'Error al guardar');
                }).catch(() => showNotification('error', '✗ Conexión', 'No se pudo conectar'));
            }
            
            clearInterval(timerInterval);
            document.getElementById('loginForm').classList.remove('hidden');
            document.getElementById('statusPanel').classList.add('hidden');
            document.getElementById('timer').textContent = '00:00:00';
            document.querySelectorAll('.employee-item').forEach(i => i.classList.remove('selected'));
            selectedEmployee = null;
            startTime = null;
        }

        window.onload = () => {
            loadEmpleados();
            loadUserData();
        };
    </script>
</body>
</html>
