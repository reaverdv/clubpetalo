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
            background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 50%, #fecfef 100%);
            min-height: 100vh;
            position: relative;
            overflow-x: hidden;
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
            width: 20px;
            height: 20px;
            background: radial-gradient(ellipse at center, #ff69b4, #ffb6c1);
            border-radius: 50% 0 50% 0;
            animation: fall linear infinite;
            transform-origin: center;
        }

        @keyframes fall {
            0% {
                transform: translateY(-100vh) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }

        .container {
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 10;
        }

        .header {
            text-align: center;
            margin-bottom: 40px;
            background: rgba(255, 255, 255, 0.9);
            backdrop-filter: blur(10px);
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(255, 105, 180, 0.3);
            border: 1px solid rgba(255, 182, 193, 0.3);
        }

        .header h1 {
            color: #d63384;
            font-size: 3em;
            font-weight: bold;
            text-shadow: 2px 2px 4px rgba(255, 105, 180, 0.3);
            margin-bottom: 10px;
            background: linear-gradient(45deg, #ff69b4, #d63384);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        .card {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(15px);
            border-radius: 20px;
            padding: 30px;
            margin-bottom: 20px;
            box-shadow: 0 15px 35px rgba(255, 105, 180, 0.2);
            border: 1px solid rgba(255, 182, 193, 0.3);
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #d63384;
            font-size: 1.1em;
        }

        .form-group select,
        .form-group input {
            width: 100%;
            padding: 15px;
            border: 2px solid #ffb6c1;
            border-radius: 15px;
            font-size: 16px;
            transition: all 0.3s ease;
            background: rgba(255, 255, 255, 0.8);
        }

        .form-group select:focus,
        .form-group input:focus {
            outline: none;
            border-color: #ff69b4;
            box-shadow: 0 0 20px rgba(255, 105, 180, 0.3);
            transform: translateY(-2px);
        }

        .btn {
            width: 100%;
            padding: 15px;
            border: none;
            border-radius: 15px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-bottom: 15px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .btn-primary {
            background: linear-gradient(45deg, #ff69b4, #ff1493);
            color: white;
            box-shadow: 0 10px 25px rgba(255, 105, 180, 0.4);
        }

        .btn-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 35px rgba(255, 105, 180, 0.6);
        }

        .btn-danger {
            background: linear-gradient(45deg, #dc3545, #c82333);
            color: white;
            box-shadow: 0 10px 25px rgba(220, 53, 69, 0.4);
        }

        .btn-danger:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 35px rgba(220, 53, 69, 0.6);
        }

        .status-card {
            text-align: center;
            min-height: 200px;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }

        .status-text {
            font-size: 1.5em;
            color: #d63384;
            margin-bottom: 20px;
            font-weight: bold;
        }

        .timer {
            font-size: 3em;
            font-weight: bold;
            color: #ff69b4;
            text-shadow: 2px 2px 4px rgba(255, 105, 180, 0.3);
            margin-bottom: 20px;
            font-family: 'Courier New', monospace;
        }

        .stats {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-top: 20px;
        }

        .stat-item {
            background: linear-gradient(45deg, #ffb6c1, #ffc0cb);
            padding: 15px;
            border-radius: 15px;
            text-align: center;
            box-shadow: 0 5px 15px rgba(255, 182, 193, 0.3);
        }

        .stat-value {
            font-size: 1.5em;
            font-weight: bold;
            color: #d63384;
        }

        .stat-label {
            font-size: 0.9em;
            color: #8b5a83;
            margin-top: 5px;
        }

        .hidden {
            display: none;
        }

        .pulse {
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        /* Notificaciones */
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: rgba(255, 255, 255, 0.98);
            backdrop-filter: blur(15px);
            border-radius: 20px;
            padding: 25px 30px;
            box-shadow: 0 15px 40px rgba(255, 105, 180, 0.4);
            border: 2px solid #ffb6c1;
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

        .notification.success {
            border-color: #28a745;
            box-shadow: 0 15px 40px rgba(40, 167, 69, 0.4);
        }

        .notification.error {
            border-color: #dc3545;
            box-shadow: 0 15px 40px rgba(220, 53, 69, 0.4);
        }

        .notification.info {
            border-color: #17a2b8;
            box-shadow: 0 15px 40px rgba(23, 162, 184, 0.4);
        }

        .notification-header {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
            font-size: 1.3em;
            font-weight: bold;
        }

        .notification-header.success {
            color: #28a745;
        }

        .notification-header.error {
            color: #dc3545;
        }

        .notification-header.info {
            color: #17a2b8;
        }

        .notification-icon {
            font-size: 1.5em;
            margin-right: 12px;
            animation: iconBounce 0.6s ease;
        }

        @keyframes iconBounce {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.2); }
        }

        .notification-body {
            color: #333;
            font-size: 1em;
            line-height: 1.4;
        }

        .notification-progress {
            height: 4px;
            background: linear-gradient(90deg, #ff69b4, #ff1493);
            border-radius: 2px;
            margin-top: 15px;
            animation: progressBar 3s linear;
            transform-origin: left;
        }

        @keyframes progressBar {
            from { transform: scaleX(1); }
            to { transform: scaleX(0); }
        }

        @media (max-width: 768px) {
            .container {
                padding: 10px;
            }
            
            .header h1 {
                font-size: 2em;
            }
            
            .timer {
                font-size: 2em;
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
    <div class="petals" id="petals"></div>
    
    <div class="container">
        <div class="header">
            <h1>🌸 CLUB PÉTALO 🌸</h1>
            <p style="color: #d63384; font-size: 1.2em;">Sistema de Fichajes</p>
        </div>

        <div class="card">
            <div id="loginForm">
                <div class="form-group">
                    <label for="empleado">Selecciona tu nombre</label>
                    <select id="empleado">
                        <option value="">-- Selecciona un empleado --</option>
                    </select>
                </div>
                <button class="btn btn-primary" onclick="fichar()">
                    🌸 Fichar Entrada 🌸
                </button>
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
                    <button class="btn btn-danger pulse" onclick="desfichar()">
                        🌸 Desfichar Salida 🌸
                    </button>
                </div>
            </div>
        </div>
    </div>

    <div id="notificationContainer"></div>

    <script>
        // ============ CONFIGURACIÓN ============
        const WEBHOOK_URL = 'https://discord.com/api/webhooks/1422188599360618597/JEr81dPlFVzJSRkTaYNF88dsfbz5_toyWNQE2lNmXN99na2l_8P9vYUMdf6mWfmADLVj';
        
        // Lista de empleados preconfigurada
        const EMPLEADOS = {
            'Chloe': 'Brown',
             'Selina': 'Gibson',
              'Zoe': 'Ross',
              'Ahmed': 'alim',
               'Alisha': 'Manrry',
                'khalil': 'Brown',
            'Alan': 'Riley',

        };
        // ======================================

        let startTime;
        let timerInterval;
        let userData = {};

        // Cargar empleados en el select
        function loadEmpleados() {
            const select = document.getElementById('empleado');
            for (const [nombre, apellidos] of Object.entries(EMPLEADOS)) {
                const option = document.createElement('option');
                option.value = `${nombre} ${apellidos}`;
                option.textContent = `${nombre} ${apellidos}`;
                select.appendChild(option);
            }
        }

        // Mostrar notificación
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

        // Crear pétalos que caen
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

        // Cargar datos del almacenamiento
        function loadUserData() {
            const stored = JSON.parse(localStorage.getItem('clubPetaloData') || '{}');
            userData = {
                totalMinutes: stored.totalMinutes || 0,
                sessions: stored.sessions || [],
                activeSession: stored.activeSession || null
            };
            updateTotalHours();
            
            if (userData.activeSession) {
                restoreActiveSession();
            }
        }

        // Restaurar sesión activa
        function restoreActiveSession() {
            const session = userData.activeSession;
            startTime = new Date(session.startTime);
            
            document.getElementById('loginForm').classList.add('hidden');
            document.getElementById('statusPanel').classList.remove('hidden');
            document.getElementById('nombreCompleto').textContent = session.nombre;
            document.getElementById('horaEntrada').textContent = startTime.toLocaleTimeString('es-ES', {hour: '2-digit', minute: '2-digit'});
            
            timerInterval = setInterval(updateTimer, 1000);
            updateTimer();
            
            showNotification('info', '¡Sesión Restaurada!', `Continuando tu fichaje desde las ${startTime.toLocaleTimeString('es-ES')}`);
        }

        // Guardar datos
        function saveUserData() {
            localStorage.setItem('clubPetaloData', JSON.stringify(userData));
        }

        // Guardar sesión activa
        function saveActiveSession(nombre) {
            userData.activeSession = {
                startTime: startTime.toISOString(),
                nombre: nombre
            };
            saveUserData();
        }

        // Limpiar sesión activa
        function clearActiveSession() {
            userData.activeSession = null;
            saveUserData();
        }

        // Formatear tiempo
        function formatTime(minutes) {
            const hours = Math.floor(minutes / 60);
            const mins = minutes % 60;
            return `${hours}h ${mins}m`;
        }

        // Formatear tiempo para el timer
        function formatTimer(seconds) {
            const hours = Math.floor(seconds / 3600);
            const minutes = Math.floor((seconds % 3600) / 60);
            const secs = seconds % 60;
            return `${hours.toString().padStart(2, '0')}:${minutes.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
        }

        // Actualizar total de horas
        function updateTotalHours() {
            document.getElementById('totalHoras').textContent = formatTime(userData.totalMinutes);
        }

        // Fichar entrada
        function fichar() {
            const empleadoSelect = document.getElementById('empleado');
            const nombreCompleto = empleadoSelect.value;
            
            if (!nombreCompleto) {
                showNotification('error', 'Error', 'Por favor, selecciona un empleado');
                return;
            }

            startTime = new Date();
            
            saveActiveSession(nombreCompleto);
            
            document.getElementById('loginForm').classList.add('hidden');
            document.getElementById('statusPanel').classList.remove('hidden');
            document.getElementById('nombreCompleto').textContent = nombreCompleto;
            document.getElementById('horaEntrada').textContent = startTime.toLocaleTimeString('es-ES', {hour: '2-digit', minute: '2-digit'});
            
            timerInterval = setInterval(updateTimer, 1000);
            
            showNotification('success', '¡Fichaje Registrado! 🌸', `Hora de entrada: ${startTime.toLocaleTimeString('es-ES')}`);
        }

        // Actualizar timer
        function updateTimer() {
            if (!startTime) return;
            
            const now = new Date();
            const elapsed = Math.floor((now - startTime) / 1000);
            document.getElementById('timer').textContent = formatTimer(elapsed);
        }

        // Desfichar
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
            
            clearActiveSession();
            
            const nombre = document.getElementById('nombreCompleto').textContent;
            
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
            
            showNotification('info', '¡Desfichaje Registrado! 🌸', `Sesión de ${formatTime(sessionMinutes)} completada`);
            
            if (WEBHOOK_URL) {
                fetch(WEBHOOK_URL, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify(embedData)
                }).then(response => {
                    if (response.ok) {
                        showNotification('success', '¡Webhook Enviado! ✅', 'Registro guardado en Discord correctamente');
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
            document.getElementById('empleado').value = '';
            document.getElementById('timer').textContent = '00:00:00';
            
            startTime = null;
        }

        // Inicializar
        window.onload = function() {
            loadEmpleados();
            loadUserData();
            createPetals();
        };
    </script>
</body>
</html>
