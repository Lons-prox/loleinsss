<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sitio con Anuncios</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }

        body {
            background: #f0f0f0;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            align-items: center;
            padding: 20px;
        }

        .ad-block {
            background: white;
            width: 100%;
            max-width: 600px;
            height: 150px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 1.2rem;
            color: #333;
        }

        .skip-btn {
            background: #4CAF50;
            color: white;
            border: none;
            padding: 0.8rem 2rem;
            border-radius: 25px;
            cursor: pointer;
            font-size: 1rem;
            margin: 20px 0;
            opacity: 0.5;
            transition: opacity 0.3s;
        }

        .skip-btn.active {
            opacity: 1;
        }

        .timer {
            font-size: 1.2rem;
            color: #333;
            margin: 10px 0;
        }

        /* Estilos para el pop-up de anuncio */
        .popup-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.7);
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }

        .popup {
            background: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            position: relative;
            width: 90%;
            max-width: 400px;
        }

        .close-btn {
            position: absolute;
            top: 10px;
            background: #ff4d4d;
            color: white;
            border: none;
            padding: 5px 10px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 1rem;
        }

        .close-btn.left {
            left: 10px;
        }

        .close-btn.right {
            right: 10px;
        }
    </style>
</head>
<body>
    <!-- Pop-up de anuncio -->
    <div class="popup-overlay" id="popupOverlay">
        <div class="popup">
            <button class="close-btn left" id="closeLeft">X</button>
            <button class="close-btn right" id="closeRight">X</button>
            <div class="ad-block">Anuncio Emergente (Simulado)</div>
        </div>
    </div>

    <!-- Bloques de anuncio (arriba) -->
    <div class="ad-block" id="adBlock1">
        Bloque de Anuncio 1 (Simulado)
    </div>
    <div class="ad-block" id="adBlock2">
        Bloque de Anuncio 2 (Simulado)
    </div>

    <!-- Temporizador -->
    <div class="timer" id="timer">10</div>

    <!-- Botón para saltar fase -->
    <button class="skip-btn" onclick="nextPhase()" id="skipBtn" disabled>Saltar Fase</button>

    <!-- Bloques de anuncio (abajo) -->
    <div class="ad-block" id="adBlock3">
        Bloque de Anuncio 3 (Simulado)
    </div>
    <div class="ad-block" id="adBlock4">
        Bloque de Anuncio 4 (Simulado)
    </div>

    <script>
        let currentPhase = 1;
        const totalPhases = 4;
        let timeLeft = 10; // Contador de 10 (20 segundos reales)

        const adBlocks = [
            document.getElementById('adBlock1'),
            document.getElementById('adBlock2'),
            document.getElementById('adBlock3'),
            document.getElementById('adBlock4')
        ];
        const timerElement = document.getElementById('timer');
        const skipButton = document.getElementById('skipBtn');
        const popupOverlay = document.getElementById('popupOverlay');
        const closeLeft = document.getElementById('closeLeft');
        const closeRight = document.getElementById('closeRight');

        // Mostrar pop-up al inicio de cada fase
        function showPopup() {
            popupOverlay.style.display = 'flex';
            setRandomCloseButton(); // Elegir aleatoriamente la "X" correcta
        }

        // Elegir aleatoriamente la "X" correcta (50% de probabilidad)
        function setRandomCloseButton() {
            const isLeftCorrect = Math.random() < 0.5; // 50% de probabilidad
            if (isLeftCorrect) {
                closeLeft.onclick = closePopup;
                closeRight.onclick = () => {}; // La "X" derecha no hace nada
            } else {
                closeRight.onclick = closePopup;
                closeLeft.onclick = () => {}; // La "X" izquierda no hace nada
            }
        }

        // Cerrar pop-up
        function closePopup() {
            popupOverlay.style.display = 'none';
        }

        // Iniciar temporizador
        function startTimer() {
            const timer = setInterval(() => {
                timeLeft--;
                timerElement.textContent = timeLeft;

                if (timeLeft <= 0) {
                    clearInterval(timer);
                    skipButton.disabled = false; // Habilitar el botón
                    skipButton.classList.add('active');
                }
            }, 2000); // 2000 ms = 2 segundos
        }

        // Cambiar de fase
        function nextPhase() {
            if (currentPhase < totalPhases) {
                currentPhase++;
                timeLeft = 10; // Reiniciar el contador a 10 (20 segundos reales)
                timerElement.textContent = timeLeft;
                skipButton.disabled = true; // Deshabilitar el botón
                skipButton.classList.remove('active');
                startTimer();
                showPopup(); // Mostrar anuncio emergente en cada fase
                adBlocks.forEach((block, index) => {
                    block.textContent = `Bloque de Anuncio ${currentPhase * 4 - 3 + index} (Simulado)`;
                });
            } else {
                window.location.href = 'https://mega.nz/TU_ENLACE_AQUI';
            }
        }

        // Iniciar primer temporizador y mostrar anuncio emergente
        showPopup();
        startTimer();
    </script>
</body>
</html>
