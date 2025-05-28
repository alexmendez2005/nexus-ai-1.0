<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NexusAI - Interfaz Innovadora</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary-color: #6e48aa;
            --secondary-color: #9d50bb;
            --accent-color: #4776e6;
            --dark-color: #1a1a2e;
            --light-color: #f8f9fa;
            --success-color: #4caf50;
            --warning-color: #ff9800;
            --error-color: #f44336;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, var(--dark-color), #16213e);
            color: var(--light-color);
            height: 100vh;
            overflow: hidden;
        }
        
        .app-container {
            display: grid;
            grid-template-columns: 280px 1fr;
            grid-template-rows: 80px 1fr;
            height: 100vh;
        }
        
        /* Header */
        .header {
            grid-column: 1 / 3;
            background: rgba(26, 26, 46, 0.8);
            backdrop-filter: blur(10px);
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0 2rem;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            z-index: 10;
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 1rem;
        }
        
        .logo-icon {
            font-size: 2rem;
            color: var(--accent-color);
        }
        
        .logo-text {
            font-size: 1.5rem;
            font-weight: 700;
            background: linear-gradient(to right, var(--primary-color), var(--accent-color));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .user-controls {
            display: flex;
            align-items: center;
            gap: 1.5rem;
        }
        
        .user-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: transform 0.3s;
        }
        
        .user-avatar:hover {
            transform: scale(1.1);
        }
        
        /* Sidebar */
        .sidebar {
            background: rgba(26, 26, 46, 0.7);
            backdrop-filter: blur(10px);
            border-right: 1px solid rgba(255, 255, 255, 0.1);
            padding: 2rem 1rem;
            overflow-y: auto;
        }
        
        .nav-menu {
            display: flex;
            flex-direction: column;
            gap: 0.5rem;
            margin-bottom: 2rem;
        }
        
        .nav-item {
            display: flex;
            align-items: center;
            gap: 1rem;
            padding: 0.8rem 1rem;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s;
            color: rgba(255, 255, 255, 0.7);
        }
        
        .nav-item:hover, .nav-item.active {
            background: rgba(110, 72, 170, 0.3);
            color: white;
        }
        
        .nav-item i {
            font-size: 1.2rem;
        }
        
        .conversations {
            margin-top: 2rem;
        }
        
        .conversations-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1rem;
            padding: 0 0.5rem;
        }
        
        .conversations-title {
            font-size: 0.9rem;
            text-transform: uppercase;
            letter-spacing: 1px;
            color: rgba(255, 255, 255, 0.5);
        }
        
        .new-chat-btn {
            background: none;
            border: none;
            color: var(--accent-color);
            cursor: pointer;
            font-size: 1.2rem;
            transition: transform 0.3s;
        }
        
        .new-chat-btn:hover {
            transform: scale(1.1);
        }
        
        .conversation-list {
            display: flex;
            flex-direction: column;
            gap: 0.5rem;
        }
        
        .conversation-item {
            padding: 0.8rem 1rem;
            border-radius: 8px;
            cursor: pointer;
            font-size: 0.9rem;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            transition: all 0.3s;
            color: rgba(255, 255, 255, 0.7);
        }
        
        .conversation-item:hover, .conversation-item.active {
            background: rgba(110, 72, 170, 0.3);
            color: white;
        }
        
        /* Main Content */
        .main-content {
            display: flex;
            flex-direction: column;
            background: url('https://images.unsplash.com/photo-1451187580459-43490279c0fa?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2072&q=80') no-repeat center center;
            background-size: cover;
            position: relative;
            overflow: hidden;
        }
        
        .main-content::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(26, 26, 46, 0.85);
            backdrop-filter: blur(2px);
        }
        
        .chat-container {
            flex: 1;
            overflow-y: auto;
            padding: 2rem;
            position: relative;
            z-index: 1;
            display: flex;
            flex-direction: column;
            gap: 1.5rem;
        }
        
        .message {
            max-width: 80%;
            padding: 1.2rem 1.5rem;
            border-radius: 18px;
            position: relative;
            line-height: 1.6;
            animation: fadeIn 0.3s ease-out;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .user-message {
            align-self: flex-end;
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            border-bottom-right-radius: 4px;
            color: white;
            box-shadow: 0 4px 15px rgba(110, 72, 170, 0.3);
        }
        
        .ai-message {
            align-self: flex-start;
            background: rgba(255, 255, 255, 0.1);
            border-bottom-left-radius: 4px;
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        }
        
        .message-time {
            font-size: 0.7rem;
            opacity: 0.7;
            margin-top: 0.5rem;
            text-align: right;
        }
        
        .input-container {
            padding: 1.5rem;
            background: rgba(26, 26, 46, 0.7);
            backdrop-filter: blur(10px);
            border-top: 1px solid rgba(255, 255, 255, 0.1);
            position: relative;
            z-index: 1;
        }
        
        .input-box {
            display: flex;
            align-items: center;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 50px;
            padding: 0.5rem 1.5rem;
            border: 1px solid rgba(255, 255, 255, 0.1);
            transition: all 0.3s;
        }
        
        .input-box:focus-within {
            border-color: var(--accent-color);
            box-shadow: 0 0 0 2px rgba(71, 118, 230, 0.3);
        }
        
        .message-input {
            flex: 1;
            background: transparent;
            border: none;
            color: white;
            padding: 1rem 0;
            font-size: 1rem;
            outline: none;
            resize: none;
            max-height: 150px;
        }
        
        .message-input::placeholder {
            color: rgba(255, 255, 255, 0.5);
        }
        
        .send-btn {
            background: linear-gradient(135deg, var(--accent-color), #5a67d8);
            border: none;
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .send-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 0 15px rgba(71, 118, 230, 0.5);
        }
        
        .tools-menu {
            display: flex;
            gap: 1rem;
            margin-bottom: 1rem;
            justify-content: center;
        }
        
        .tool-btn {
            background: rgba(255, 255, 255, 0.05);
            border: none;
            border-radius: 50px;
            padding: 0.5rem 1.2rem;
            color: rgba(255, 255, 255, 0.7);
            display: flex;
            align-items: center;
            gap: 0.5rem;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 0.9rem;
        }
        
        .tool-btn:hover {
            background: rgba(110, 72, 170, 0.3);
            color: white;
        }
        
        .footer {
            text-align: center;
            padding: 1rem;
            font-size: 0.8rem;
            color: rgba(255, 255, 255, 0.5);
            position: relative;
            z-index: 1;
        }
        
        .footer a {
            color: var(--accent-color);
            text-decoration: none;
            transition: all 0.3s;
        }
        
        .footer a:hover {
            text-decoration: underline;
        }
        
        /* Responsive Design */
        @media (max-width: 768px) {
            .app-container {
                grid-template-columns: 1fr;
                grid-template-rows: 80px 1fr;
            }
            
            .sidebar {
                position: absolute;
                width: 280px;
                height: 100%;
                z-index: 100;
                transform: translateX(-100%);
                transition: transform 0.3s;
            }
            
            .sidebar.active {
                transform: translateX(0);
            }
            
            .menu-toggle {
                display: flex;
            }
        }
        
        /* 3D Elements */
        .floating-shapes {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            z-index: 0;
            overflow: hidden;
        }
        
        .shape {
            position: absolute;
            opacity: 0.1;
            border-radius: 50%;
            filter: blur(40px);
        }
        
        .shape-1 {
            width: 300px;
            height: 300px;
            background: var(--primary-color);
            top: -100px;
            left: -100px;
            animation: float 15s infinite ease-in-out;
        }
        
        .shape-2 {
            width: 400px;
            height: 400px;
            background: var(--accent-color);
            bottom: -150px;
            right: -100px;
            animation: float 18s infinite ease-in-out reverse;
        }
        
        .shape-3 {
            width: 200px;
            height: 200px;
            background: var(--secondary-color);
            top: 50%;
            left: 30%;
            animation: float 12s infinite ease-in-out;
        }
        
        @keyframes float {
            0%, 100% { transform: translate(0, 0); }
            25% { transform: translate(50px, 50px); }
            50% { transform: translate(0, 100px); }
            75% { transform: translate(-50px, 50px); }
        }
        
        /* Special Effects */
        .typing-indicator {
            display: flex;
            gap: 0.5rem;
            padding: 1rem;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 50px;
            width: fit-content;
            margin-bottom: 1rem;
        }
        
        .typing-dot {
            width: 8px;
            height: 8px;
            background: rgba(255, 255, 255, 0.7);
            border-radius: 50%;
            animation: typingAnimation 1.4s infinite ease-in-out;
        }
        
        .typing-dot:nth-child(1) { animation-delay: 0s; }
        .typing-dot:nth-child(2) { animation-delay: 0.2s; }
        .typing-dot:nth-child(3) { animation-delay: 0.4s; }
        
        @keyframes typingAnimation {
            0%, 60%, 100% { transform: translateY(0); opacity: 0.6; }
            30% { transform: translateY(-8px); opacity: 1; }
        }
        
        /* Context Menu */
        .context-menu {
            position: absolute;
            background: rgba(26, 26, 46, 0.95);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 8px;
            padding: 0.5rem 0;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            z-index: 1000;
            display: none;
        }
        
        .context-menu-item {
            padding: 0.7rem 1.5rem;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 0.9rem;
            color: rgba(255, 255, 255, 0.8);
            white-space: nowrap;
        }
        
        .context-menu-item:hover {
            background: rgba(110, 72, 170, 0.3);
            color: white;
        }
        
        .context-menu-item i {
            margin-right: 0.8rem;
            width: 20px;
            text-align: center;
        }
        
        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        
        ::-webkit-scrollbar-track {
            background: rgba(255, 255, 255, 0.05);
            border-radius: 10px;
        }
        
        ::-webkit-scrollbar-thumb {
            background: rgba(110, 72, 170, 0.5);
            border-radius: 10px;
        }
        
        ::-webkit-scrollbar-thumb:hover {
            background: var(--primary-color);
        }
    </style>
</head>
<body>
    <div class="app-container">
        <!-- Header -->
        <header class="header">
            <div class="logo">
                <div class="logo-icon">
                    <i class="fas fa-robot"></i>
                </div>
                <div class="logo-text">NexusAI</div>
            </div>
            <div class="user-controls">
                <button class="tool-btn">
                    <i class="fas fa-sun"></i> Modo claro
                </button>
                <div class="user-avatar">
                    <i class="fas fa-user"></i>
                </div>
            </div>
        </header>
        
        <!-- Sidebar -->
        <aside class="sidebar">
            <nav class="nav-menu">
                <div class="nav-item active">
                    <i class="fas fa-comment"></i>
                    <span>Nuevo chat</span>
                </div>
                <div class="nav-item">
                    <i class="fas fa-brain"></i>
                    <span>Modelos</span>
                </div>
                <div class="nav-item">
                    <i class="fas fa-graduation-cap"></i>
                    <span>Aprendizaje</span>
                </div>
                <div class="nav-item">
                    <i class="fas fa-cog"></i>
                    <span>Ajustes</span>
                </div>
            </nav>
            
            <div class="conversations">
                <div class="conversations-header">
                    <div class="conversations-title">Conversaciones recientes</div>
                    <button class="new-chat-btn" title="Nueva conversación">
                        <i class="fas fa-plus"></i>
                    </button>
                </div>
                <div class="conversation-list">
                    <div class="conversation-item active">
                        <i class="fas fa-message"></i> Optimización de código
                    </div>
                    <div class="conversation-item">
                        <i class="fas fa-message"></i> Ideas para startup
                    </div>
                    <div class="conversation-item">
                        <i class="fas fa-message"></i> Historia del arte moderno
                    </div>
                    <div class="conversation-item">
                        <i class="fas fa-message"></i> Recetas saludables
                    </div>
                    <div class="conversation-item">
                        <i class="fas fa-message"></i> Plan de ejercicios
                    </div>
                </div>
            </div>
        </aside>
        
        <!-- Main Content -->
        <main class="main-content">
            <div class="floating-shapes">
                <div class="shape shape-1"></div>
                <div class="shape shape-2"></div>
                <div class="shape shape-3"></div>
            </div>
            
            <div class="chat-container" id="chatContainer">
                <div class="message ai-message">
                    ¡Hola! Soy NexusAI, tu asistente de inteligencia artificial avanzada. Combino las capacidades de los mejores modelos como DeepSeek y ChatGPT con un enfoque innovador. 
                    <br><br>
                    ¿En qué puedo ayudarte hoy?
                    <div class="message-time">hoy, 10:30 AM</div>
                </div>
                
                <div class="message user-message">
                    Diseña una IA con todas las capacidades de deepseek y chatgpt, pero con un escritorio más innovador, que tenga mis derechos de autor Alexander y mi instagram ig: 7alex.07
                    <div class="message-time">hoy, 10:32 AM</div>
                </div>
                
                <div class="typing-indicator">
                    <div class="typing-dot"></div>
                    <div class="typing-dot"></div>
                    <div class="typing-dot"></div>
                </div>
            </div>
            
            <div class="tools-menu">
                <button class="tool-btn">
                    <i class="fas fa-magic"></i> Mejorar redacción
                </button>
                <button class="tool-btn">
                    <i class="fas fa-code"></i> Generar código
                </button>
                <button class="tool-btn">
                    <i class="fas fa-chart-line"></i> Analizar datos
                </button>
                <button class="tool-btn">
                    <i class="fas fa-image"></i> Crear imágenes
                </button>
            </div>
            
            <div class="input-container">
                <div class="input-box">
                    <textarea class="message-input" placeholder="Escribe un mensaje..." rows="1"></textarea>
                    <button class="send-btn">
                        <i class="fas fa-paper-plane"></i>
                    </button>
                </div>
            </div>
            
            <footer class="footer">
                NexusAI v2.3.5 - © <span id="year"></span> Todos los derechos reservados a <a href="https://www.instagram.com/7alex.07/" target="_blank">Alexander (@7alex.07)</a>
            </footer>
        </main>
    </div>
    
    <!-- Context Menu -->
    <div class="context-menu" id="contextMenu">
        <div class="context-menu-item">
            <i class="fas fa-copy"></i> Copiar
        </div>
        <div class="context-menu-item">
            <i class="fas fa-share"></i> Compartir
        </div>
        <div class="context-menu-item">
            <i class="fas fa-edit"></i> Editar
        </div>
        <div class="context-menu-item">
            <i class="fas fa-trash"></i> Eliminar
        </div>
    </div>
    
    <script>
        // Set current year in footer
        document.getElementById('year').textContent = new Date().getFullYear();
        
        // Auto-resize textarea
        const textarea = document.querySelector('.message-input');
        textarea.addEventListener('input', function() {
            this.style.height = 'auto';
            this.style.height = (this.scrollHeight) + 'px';
        });
        
        // Context menu
        const chatContainer = document.getElementById('chatContainer');
        const contextMenu = document.getElementById('contextMenu');
        
        chatContainer.addEventListener('contextmenu', function(e) {
            e.preventDefault();
            contextMenu.style.display = 'block';
            contextMenu.style.left = e.pageX + 'px';
            contextMenu.style.top = e.pageY + 'px';
        });
        
        document.addEventListener('click', function() {
            contextMenu.style.display = 'none';
        });
        
        // Simulate AI response after 2 seconds
        setTimeout(function() {
            document.querySelector('.typing-indicator').remove();
            
            const aiResponse = document.createElement('div');
            aiResponse.className = 'message ai-message';
            aiResponse.innerHTML = `
                He diseñado una interfaz innovadora para NexusAI que combina lo mejor de DeepSeek y ChatGPT con un enfoque visual moderno y personalizado para ti, Alexander.
                <br><br>
                Características principales:
                <ul style="margin-left: 1.5rem; margin-top: 0.5rem;">
                    <li>Interfaz con efectos de cristal y elementos flotantes</li>
                    <li>Sistema de conversaciones organizadas</li>
                    <li>Modos de interacción múltiples</li>
                    <li>Diseño completamente responsive</li>
                    <li>Tus derechos de autor y referencia a tu Instagram (@7alex.07) integrados</li>
                </ul>
                <br>
                ¿Te gustaría que añada alguna funcionalidad específica?
                <div class="message-time">hoy, 10:33 AM</div>
            `;
            
            document.getElementById('chatContainer').appendChild(aiResponse);
            chatContainer.scrollTop = chatContainer.scrollHeight;
        }, 2000);
        
        // Send message on Enter (but not Shift+Enter)
        textarea.addEventListener('keydown', function(e) {
            if (e.key === 'Enter' && !e.shiftKey) {
                e.preventDefault();
                sendMessage();
            }
        });
        
        // Send message on button click
        document.querySelector('.send-btn').addEventListener('click', sendMessage);
        
        function sendMessage() {
            const messageText = textarea.value.trim();
            if (messageText) {
                // Add user message
                const userMessage = document.createElement('div');
                userMessage.className = 'message user-message';
                userMessage.innerHTML = `
                    ${messageText}
                    <div class="message-time">hoy, ${new Date().toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'})}</div>
                `;
                document.getElementById('chatContainer').appendChild(userMessage);
                
                // Clear input
                textarea.value = '';
                textarea.style.height = 'auto';
                
                // Show typing indicator
                const typingIndicator = document.createElement('div');
                typingIndicator.className = 'typing-indicator';
                typingIndicator.innerHTML = `
                    <div class="typing-dot"></div>
                    <div class="typing-dot"></div>
                    <div class="typing-dot"></div>
                `;
                document.getElementById('chatContainer').appendChild(typingIndicator);
                
                // Scroll to bottom
                chatContainer.scrollTop = chatContainer.scrollHeight;
                
                // Simulate AI response after 1-3 seconds
                setTimeout(function() {
                    typingIndicator.remove();
                    
                    const aiResponse = document.createElement('div');
                    aiResponse.className = 'message ai-message';
                    aiResponse.innerHTML = `
                        He procesado tu solicitud. Como IA avanzada con capacidades similares a DeepSeek y ChatGPT, puedo ayudarte con:
                        <br><br>
                        <strong>1.</strong> Generación de código y optimización<br>
                        <strong>2.</strong> Análisis de datos complejos<br>
                        <strong>3.</strong> Creación de contenido innovador<br>
                        <strong>4.</strong> Soluciones personalizadas para tus proyectos<br>
                        <br>
                        La interfaz actual ya incluye tus datos de copyright y referencia a tu Instagram en el footer.
                        <div class="message-time">hoy, ${new Date().toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'})}</div>
                    `;
                    
                    document.getElementById('chatContainer').appendChild(aiResponse);
                    chatContainer.scrollTop = chatContainer.scrollHeight;
                }, 1000 + Math.random() * 2000);
            }
        }
    </script>
</body>
</html>
