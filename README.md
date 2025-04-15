<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Convite Especial</title>
    <style>
        * {
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }
        
        body, html {
            height: 100%;
            width: 100%;
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
            background-color: #f0f8ff;
            overflow: hidden;
            position: fixed;
        }
        
        .app-container {
            height: 100%;
            width: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        
        .card {
            background-color: white;
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.1);
            text-align: center;
            width: 100%;
            max-width: 400px;
            position: relative;
            z-index: 5;
        }
        
        h1 {
            color: #ff6b6b;
            margin-bottom: 30px;
            font-size: 24px;
        }
        
        .button-area {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 30px;
            margin-bottom: 20px;
            min-height: 60px;
            position: relative;
        }
        
        .btn {
            padding: 12px 25px;
            font-size: 16px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            outline: none;
            transition: transform 0.2s, background-color 0.2s;
            -webkit-touch-callout: none;
            -webkit-user-select: none;
            user-select: none;
        }
        
        .btn-sim {
            background-color: #4caf50;
            color: white;
        }
        
        .btn-sim:hover, .btn-sim:active {
            background-color: #3e8e41;
            transform: scale(1.05);
        }
        
        .btn-nao {
            background-color: #ff6b6b;
            color: white;
        }
        
        .btn-nao:hover, .btn-nao:active {
            background-color: #ff5252;
        }
        
        /* Botão não quando está em modo "fujão" */
        .botao-fujao {
            position: fixed !important;
            z-index: 1000;
        }
        
        .message {
            color: #4caf50;
            font-size: 20px;
            margin-top: 20px;
            opacity: 0;
            transition: opacity 0.5s;
        }
        
        .show {
            opacity: 1;
        }
        
        .confetti {
            position: fixed;
            width: 10px;
            height: 10px;
            border-radius: 50%;
            z-index: 4;
            opacity: 0.8;
        }
        
        .heart {
            position: fixed;
            font-size: 24px;
            z-index: 4;
        }
        
        @keyframes fall {
            to {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }
        
        @keyframes float {
            0% { transform: translateY(0); opacity: 1; }
            100% { transform: translateY(-100px); opacity: 0; }
        }
    </style>
</head>
<body>
    <div class="app-container">
        <div class="card">
            <h1>Quer almoçar comigo?</h1>
            <div class="button-area">
                <button id="btnSim" class="btn btn-sim">Sim</button>
                <button id="btnNao" class="btn btn-nao">Não</button>
            </div>
            <div id="message" class="message">Ótimo! Vamos ter um almoço incrível!</div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const btnSim = document.getElementById('btnSim');
            const btnNao = document.getElementById('btnNao');
            const message = document.getElementById('message');
            
            let primeiroClique = true;
            
            // Função para obter posição aleatória, mas sempre visível na tela
            function getPosicaoSegura() {
                const botaoWidth = btnNao.offsetWidth;
                const botaoHeight = btnNao.offsetHeight;
                
                // Garantir que o botão fique dentro dos limites da tela
                // com uma margem de segurança
                const margemSeguranca = 20;
                const maxX = window.innerWidth - botaoWidth - margemSeguranca;
                const maxY = window.innerHeight - botaoHeight - margemSeguranca;
                
                const x = Math.max(margemSeguranca, Math.floor(Math.random() * maxX));
                const y = Math.max(margemSeguranca, Math.floor(Math.random() * maxY));
                
                return { x, y };
            }
            
            // Manipulador para o botão "Não"
            btnNao.addEventListener('click', function(e) {
                e.preventDefault();
                e.stopPropagation();
                
                // Na primeira vez, converte o botão para posição fixa
                if (primeiroClique) {
                    primeiroClique = false;
                    btnNao.classList.add('botao-fujao');
                }
                
                // Obtém nova posição e aplica
                const novaPosicao = getPosicaoSegura();
                btnNao.style.left = novaPosicao.x + 'px';
                btnNao.style.top = novaPosicao.y + 'px';
                
                // Impede comportamento padrão em dispositivos touch
                return false;
            });
            
            // Também trata touchstart para dispositivos móveis
            btnNao.addEventListener('touchstart', function(e) {
                e.preventDefault();
                e.stopPropagation();
                
                // Na primeira vez, converte o botão para posição fixa
                if (primeiroClique) {
                    primeiroClique = false;
                    btnNao.classList.add('botao-fujao');
                }
                
                // Obtém nova posição e aplica
                const novaPosicao = getPosicaoSegura();
                btnNao.style.left = novaPosicao.x + 'px';
                btnNao.style.top = novaPosicao.y + 'px';
                
                return false;
            });
            
            // Manipulador para o botão "Sim"
            btnSim.addEventListener('click', function() {
                // Mostrar mensagem
                message.classList.add('show');
                
                // Criar confetes
                criarFestinha();
                
                // Esconder o botão "Não"
                btnNao.style.display = 'none';
                
                // Animar o botão "Sim"
                btnSim.style.transform = 'scale(1.2)';
                setTimeout(() => {
                    btnSim.style.transform = 'scale(1)';
                }, 300);
            });
            
            // Função para criar elementos de animação (confetes e corações)
            function criarFestinha() {
                // Criar confetes
                const numElementos = (window.innerWidth < 600) ? 30 : 50;
                
                for (let i = 0; i < numElementos; i++) {
                    // Cria confete
                    setTimeout(() => {
                        const confetti = document.createElement('div');
                        confetti.className = 'confetti';
                        
                        // Posição inicial aleatória na parte superior
                        const startX = Math.random() * window.innerWidth;
                        confetti.style.left = startX + 'px';
                        confetti.style.top = '-10px';
                        
                        // Cor aleatória
                        const colors = ['#ff6b6b', '#4caf50', '#3498db', '#f1c40f', '#9b59b6', '#e67e22'];
                        const randomColor = colors[Math.floor(Math.random() * colors.length)];
                        confetti.style.backgroundColor = randomColor;
                        
                        // Tamanho aleatório
                        const size = Math.random() * 8 + 5;
                        confetti.style.width = size + 'px';
                        confetti.style.height = size + 'px';
                        
                        // Animação
                        const duration = Math.random() * 2 + 1;
                        confetti.style.animation = `fall ${duration}s linear forwards`;
                        
                        document.body.appendChild(confetti);
                        
                        // Limpar após animação
                        setTimeout(() => {
                            confetti.remove();
                        }, duration * 1000);
                    }, i * 50);
                    
                    // Cria coração (menos corações que confetes)
                    if (i % 3 === 0) {
                        setTimeout(() => {
                            const heart = document.createElement('div');
                            heart.className = 'heart';
                            heart.innerHTML = '❤️';
                            
                            // Posição inicial
                            const startX = Math.random() * window.innerWidth;
                            heart.style.left = startX + 'px';
                            heart.style.bottom = '20px';
                            
                            // Tamanho
                            const size = Math.random() * 15 + 15;
                            heart.style.fontSize = size + 'px';
                            
                            // Animação
                            const duration = Math.random() * 2 + 1;
                            heart.style.animation = `float ${duration}s ease-in-out forwards`;
                            
                            document.body.appendChild(heart);
                            
                            // Limpar após animação
                            setTimeout(() => {
                                heart.remove();
                            }, duration * 1000);
                        }, i * 150);
                    }
                }
            }
            
            // Prevenir comportamentos indesejados em dispositivos móveis
            document.addEventListener('touchmove', function(e) {
                if (e.target === btnNao) {
                    e.preventDefault();
                }
            }, { passive: false });
        });
    </script>
</body>
</html>
