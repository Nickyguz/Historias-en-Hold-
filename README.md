# Historias-en-Hold-
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Rompecabezas con Historias</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
      background-color: #f0f0f0;
    }
    .puzzle-container {
      display: flex;
      gap: 10px;
      margin-bottom: 20px;
    }
    .puzzle-piece {
      width: 80px;
      height: 80px;
      background-color: #cccccc;
      border: 2px solid #333;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      transition: opacity 0.3s;
    }
    .placed {
      background-color: #4caf50;
      color: white;
      cursor: default;
    }
    #storyModal {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background: rgba(0, 0, 0, 0.7);
      display: none;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      color: white;
    }
    #storyBox {
      background: #222;
      padding: 20px;
      border-radius: 8px;
      max-width: 400px;
      text-align: center;
    }
    #continueBtn {
      margin-top: 15px;
      padding: 10px 20px;
      background-color: #4caf50;
      border: none;
      color: white;
      cursor: pointer;
      border-radius: 5px;
    }
  </style>
</head>
<body>
  <div class="puzzle-container">
    <div class="puzzle-piece" data-index="0">1</div>
    <div class="puzzle-piece" data-index="1">2</div>
    <div class="puzzle-piece" data-index="2">3</div>
  </div>

  <div id="storyModal">
    <div id="storyBox">
      <p id="storyText"></p>
      <button id="continueBtn">Continuar</button>
    </div>
  </div>

  <script>
    const puzzlePieces = document.querySelectorAll('.puzzle-piece');
    let storyModal = document.getElementById('storyModal');
    let storyText = document.getElementById('storyText');
    let continueBtn = document.getElementById('continueBtn');

    let currentPieceIndex = 0;
    const stories = [
      "Esta es la historia detrás de la primera llamada...",
      "Una conversación inesperada cambió su día...",
      "Una historia de empatía al otro lado de la línea..."
    ];

    function showStory(index) {
      storyText.innerText = stories[index];
      storyModal.style.display = 'flex';
      disablePuzzleInteraction();
    }

    function hideStory() {
      storyModal.style.display = 'none';
      enablePuzzleInteraction();
    }

    function disablePuzzleInteraction() {
      puzzlePieces.forEach(piece => {
        piece.style.pointerEvents = 'none';
        piece.style.opacity = 0.5;
      });
    }

    function enablePuzzleInteraction() {
      puzzlePieces.forEach(piece => {
        if (!piece.classList.contains('placed')) {
          piece.style.pointerEvents = 'auto';
          piece.style.opacity = 1;
        }
      });
    }

    puzzlePieces.forEach((piece, index) => {
      piece.addEventListener('click', () => {
        if (index === currentPieceIndex) {
          piece.classList.add('placed');
          showStory(currentPieceIndex);
        }
      });
    });

    continueBtn.addEventListener('click', () => {
      currentPieceIndex++;
      hideStory();
    });
  </script>
</body>
</html>
