<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Convite Especial</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0f8ff;
            margin: 0;
            overflow: hidden;
        }
        
        .container {
            text-align: center;
            background-color: white;
            padding: 20px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            position: relative;
            z-index: 1;
            width: 80%;
            max-width: 500px;
        }
        
        h1 {
            color: #ff6b6b;
            margin-bottom: 30px;
            font-size: 28px;
        }
        
        .button-container {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin-top: 30px;
            min-height: 60px;
            position: relative;
        }
        
        button {
            padding: 15px 30px;
            font-size: 18px;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: transform 0.3s, background-color 0.3s;
        }
        
        #btnSim {
            background-color: #4caf50;
            color: white;
        }
        
        #btnSim:hover {
            background-color: #3e8e41;
            transform: scale(1.05);
        }
        
        #btnNao {
            background-color: #ff6b6b;
            color: white;
            position: relative; /* Inicialmente posicionado normalmente no fluxo */
        }
        
        #btnNao.esquivo {
            position: fixed; /* Mudamos para fixed para garantir visibilidade na tela */
            z-index: 100;
            transition: all 0.3s ease; /* Animação suave para transição */
        }
        
        #btnNao:hover {
            background-color: #ff5252;
        }
        
        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            background-color: #f00;
            border-radius: 50%;
            animation: fall 3s linear forwards;
        }
        
        @keyframes fall {
            to {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }
        
        .message {
            font-size: 24px;
            color: #4caf50;
            margin-top: 20px;
            opacity: 0;
            transition: opacity 1s;
        }
        
        .show {
            opacity: 1;
        }
        
        .heart {
            font-size: 24px;
            position: absolute;
            animation: float 3s ease-in-out infinite;
        }
        
        @keyframes float {
            0% { transform: translateY(0) rotate(0deg); opacity: 1; }
            100% { transform: translateY(-100px) rotate(360deg); opacity: 0; }
        }
        
        /* Responsividade para dispositivos móveis */
        @media (max-width: 480px) {
            h1 {
                font-size: 24px;
            }
            
            button {
                padding: 12px 25px;
                font-size: 16px;
            }
            
            .button-container {
                gap: 15px;
            }
            
            .message {
                font-size: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Quer almoçar comigo?</h1>
        <div class="button-container">
            <button id="btnSim">Sim</button>
            <button id="btnNao">Não</button>
        </div>
        <div id="message" class="message">Ótimo! Vamos ter um almoço incrível!</div>
    </div>

    <script>
        const btnNao = document.getElementById("btnNao");
        const btnSim = document.getElementById("btnSim");
        const message = document.getElementById("message");
        const container = document.querySelector(".container");
        
        let botaoClicado = false;
        
        // Função para posicionar o botão "Não" em um local aleatório, mas sempre visível
        function posicionarBotaoNao() {
            // Obter dimensões do botão
            const botaoWidth = btnNao.offsetWidth;
            const botaoHeight = btnNao.offsetHeight;
            
            // Garantir que o botão fique dentro dos limites da tela
            const maxX = window.innerWidth - botaoWidth - 10; // 10px de margem
            const maxY = window.innerHeight - botaoHeight - 10; // 10px de margem
            
            // Gerar posição aleatória dentro dos limites visíveis
            const x = Math.max(10, Math.random() * maxX);
            const y = Math.max(10, Math.random() * maxY);
            
            // Aplicar a nova posição
            btnNao.style.left = x + "px";
            btnNao.style.top = y + "px";
        }
        
        // Move o botão quando clica em "Não"
        btnNao.addEventListener("click", function(e) {
            e.preventDefault(); // Evita comportamento padrão
            
            // Na primeira vez que o botão é clicado, adiciona a classe para posicionamento fixo
            if (!botaoClicado) {
                botaoClicado = true;
                btnNao.classList.add('esquivo');
            }
            
            posicionarBotaoNao(); // Reposiciona o botão
        });
        
        // Para dispositivos touch, previne que o toque no botão "Não" cause scroll
        btnNao.addEventListener("touchstart", function(e) {
            e.preventDefault();
        });
        
        // Animação quando clica em "Sim"
        btnSim.addEventListener("click", function() {
            // Mostrar mensagem
            message.classList.add("show");
            
            // Criar confetes
            for (let i = 0; i < 50; i++) { // Reduzimos para melhor performance em mobile
                createConfetti();
            }
            
            // Criar corações
            for (let i = 0; i < 10; i++) { // Reduzimos para melhor performance em mobile
                setTimeout(() => {
                    createHeart();
                }, i * 150);
            }
            
            // Esconder o botão "Não"
            btnNao.style.display = "none";
            
            // Animar o botão "Sim"
            btnSim.style.transform = "scale(1.2)";
            setTimeout(() => {
                btnSim.style.transform = "scale(1)";
            }, 300);
        });
        
        // Função para criar confete
        function createConfetti() {
            const confetti = document.createElement("div");
            confetti.className = "confetti";
            
            // Posição inicial
            const startX = Math.random() * window.innerWidth;
            confetti.style.left = startX + "px";
            confetti.style.top = "-10px";
            
            // Cor aleatória
            const colors = ["#ff6b6b", "#4caf50", "#3498db", "#f1c40f", "#9b59b6", "#e67e22"];
            const randomColor = colors[Math.floor(Math.random() * colors.length)];
            confetti.style.backgroundColor = randomColor;
            
            // Tamanho aleatório
            const size = Math.random() * 10 + 5;
            confetti.style.width = size + "px";
            confetti.style.height = size + "px";
            
            // Velocidade e tempo aleatórios
            const duration = Math.random() * 3 + 2;
            confetti.style.animation = `fall ${duration}s linear forwards`;
            
            document.body.appendChild(confetti);
            
            // Remover após a animação
            setTimeout(() => {
                confetti.remove();
            }, duration * 1000);
        }
        
        // Função para criar coração
        function createHeart() {
            const heart = document.createElement("div");
            heart.className = "heart";
            heart.innerHTML = "❤️";
            
            // Posição inicial aleatória em baixo da tela
            const startX = Math.random() * window.innerWidth;
            heart.style.left = startX + "px";
            heart.style.top = (window.innerHeight - 50) + "px";
            
            // Tamanho aleatório
            const size = Math.random() * 20 + 15;
            heart.style.fontSize = size + "px";
            
            // Velocidade aleatória
            const duration = Math.random() * 2 + 2;
            heart.style.animation = `float ${duration}s ease-in-out forwards`;
            
            document.body.appendChild(heart);
            
            // Remover após a animação
            setTimeout(() => {
                heart.remove();
            }, duration * 1000);
        }
        
        // Ajustar layout para dispositivos móveis
        function ajustarParaMobile() {
            if (window.innerWidth <= 480) {
                // Ajustes específicos para mobile se necessário
            }
        }
        
        // Chamar ajustes ao carregar e redimensionar
        window.addEventListener('load', ajustarParaMobile);
        window.addEventListener('resize', ajustarParaMobile);
    </script>
</body>
</html>
