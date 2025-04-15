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
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            position: relative;
            z-index: 1;
        }
        
        h1 {
            color: #ff6b6b;
            margin-bottom: 30px;
            font-size: 32px;
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
            padding: 15px 40px;
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
            position: absolute; /* Quando está em modo esquivo, torna-se posicionamento absoluto */
            z-index: 100;
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
        const buttonContainer = document.querySelector(".button-container");
        
        let botaoClicado = false;
        
        // Função para posicionar o botão "Não" em um local aleatório
        function posicionarBotaoNao() {
            const containerRect = container.getBoundingClientRect();
            // Determinar área segura dentro do container
            const margemSeguranca = 20;
            const maxX = containerRect.width - btnNao.offsetWidth - margemSeguranca;
            const maxY = containerRect.height - btnNao.offsetHeight - margemSeguranca;
            
            // Posição aleatória dentro da área do container
            const x = Math.random() * maxX + margemSeguranca;
            const y = Math.random() * maxY + margemSeguranca;
            
            btnNao.style.left = x + "px";
            btnNao.style.top = y + "px";
        }
        
        // Move o botão quando clica em "Não"
        btnNao.addEventListener("click", function(e) {
            e.preventDefault(); // Evita comportamento padrão
            
            // Na primeira vez que o botão é clicado, adiciona a classe para posicionamento absoluto
            if (!botaoClicado) {
                botaoClicado = true;
                btnNao.classList.add('esquivo');
            }
            
            posicionarBotaoNao(); // Reposiciona o botão
        });
        
        // Animação quando clica em "Sim"
        btnSim.addEventListener("click", function() {
            // Mostrar mensagem
            message.classList.add("show");
            
            // Criar confetes
            for (let i = 0; i < 100; i++) {
                createConfetti();
            }
            
            // Criar corações
            for (let i = 0; i < 20; i++) {
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
    </script>
</body>
</html>
