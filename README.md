<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>San Valentín Especial</title>
  <style>
    /* General: cada "pantalla" ocupa toda la ventana */
    .screen {
      display: none;
      width: 100vw;
      height: 100vh;
      position: absolute;
      top: 0;
      left: 0;
    }
    /* Pantalla 1: Pregunta inicial con fondo temático y osito */
    #screen1 {
      display: block;
      background: url('https://images.pexels.com/photos/3755765/pexels-photo-3755765.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260') no-repeat center center;
      background-size: cover;
      text-align: center;
      color: white;
    }
    #screen1 .question {
      font-size: 36px;
      margin-top: 30%;
    }
    #screen1 .buttons {
      margin-top: 20px;
    }
    #screen1 button {
      font-size: 24px;
      padding: 10px 20px;
      margin: 10px;
      border: none;
      border-radius: 10px;
      cursor: pointer;
    }
    #screen1 button#si {
      background-color: #ff4d4d;
      color: white;
    }
    #screen1 button#no {
      background-color: #888;
      color: white;
    }
    #screen1 .teddy {
      margin-top: 20px;
      width: 150px;
    }
    /* Pantalla 2: Gatito, frases de amor y corazones flotantes */
    #screen2 {
      background: #ffe6e6;
      text-align: center;
      padding-top: 30px;
      color: #b30000;
    }
    #screen2 .kitten {
      width: 200px;
    }
    #screen2 .love-phrases {
      font-size: 24px;
      margin: 20px;
    }
    /* Los corazones flotantes se generan dinámicamente */
    .heart {
      position: absolute;
      font-size: 24px;
      animation: float 4s linear infinite;
    }
    @keyframes float {
      0% { transform: translateY(100vh); opacity: 1; }
      100% { transform: translateY(-10vh); opacity: 0; }
    }
    /* Pantalla 3: Rompecabezas */
    #screen3 {
      background: #fff;
      text-align: center;
      padding-top: 20px;
    }
    #puzzle-board {
      margin: auto;
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-gap: 5px;
      width: 310px;
      height: 310px;
      border: 2px solid #b30000;
      padding: 5px;
    }
    .puzzle-cell {
      width: 100px;
      height: 100px;
      border: 1px dashed #ccc;
    }
    #puzzle-pieces {
      margin: 20px auto;
      width: 320px;
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      justify-content: center;
    }
    .puzzle-piece {
      width: 100px;
      height: 100px;
      border: 1px solid #b30000;
      cursor: grab;
      background-image: url('
      https://raw.githubusercontent.com/Alexiscj23/San-valentines/refs/heads/main/IMG_20190812_212839.jpg  ');
      background-size: 300px 300px;
    }
    /* Pantalla 4: Libro (Slider) con 5 páginas */
    #screen4 {
      background: #ffe6e6;
      text-align: center;
      padding: 20px;
      color: #b30000;
    }
    .slider {
      position: relative;
      width: 80%;
      max-width: 600px;
      margin: 0 auto;
      overflow: hidden;
    }
    .slides {
      display: flex;
      transition: transform 0.5s ease-in-out;
    }
    .slide {
      min-width: 100%;
      box-sizing: border-box;
      padding: 20px;
    }
    .slide img {
      width: 100%;
      max-height: 300px;
      object-fit: cover;
      border: 2px solid #b30000;
      border-radius: 10px;
    }
    .slide .caption {
      font-size: 20px;
      margin-top: 10px;
    }
    .slider-controls {
      margin-top: 10px;
    }
    .slider-controls button {
      padding: 10px 20px;
      font-size: 18px;
      border: none;
      background-color: #ff4d4d;
      color: white;
      border-radius: 5px;
      cursor: pointer;
      margin: 0 10px;
    }
  </style>
</head>
<body>
  <!-- Pantalla 1: Pregunta inicial -->
  <div id="screen1" class="screen">
    <div class="question">¿Quieres ser mi San Valentín?</div>
    <div class="buttons">
      <button id="si" onclick="goToScreen2()">Sí</button>
      <button id="no" onclick="alert('Oh, qué pena!')">No</button>
    </div>
    <!-- Imagen de osito amoroso -->
    <img class="teddy" src="https://media.giphy.com/media/10LKovKon8DENq/giphy.gif" alt="Teddy amoroso">
  </div>

  <!-- Pantalla 2: Gatito dando besos y frases de amor con corazones flotantes -->
  <div id="screen2" class="screen">
    <img class="kitten" src="https://media.giphy.com/media/9o6wJbQ0Vb5U0/giphy.gif" alt="Kitten dando besos">
    <div class="love-phrases">
      "Tu amor me llena de alegría" <br>
      "Eres mi sol en los días grises" <br>
      "Cada beso tuyo es un regalo"
    </div>
    <button onclick="goToScreen3()" style="font-size:24px; padding:10px 20px; border:none; border-radius:10px; background-color:#ff4d4d; color:white; cursor:pointer;">Continuar</button>
  </div>

  <!-- Pantalla 3: Rompecabezas -->
  <div id="screen3" class="screen">
    <h2>Arma el rompecabezas</h2>
    <p>Arrastra y suelta las piezas para formar la imagen.</p>
    <div id="puzzle-board"></div>
    <div id="puzzle-pieces"></div>
    <p id="puzzle-message"></p>
    <button onclick="checkPuzzle()" style="font-size:24px; padding:10px 20px; border:none; border-radius:10px; background-color:#ff4d4d; color:white; cursor:pointer;">Verificar rompecabezas</button>
  </div>

  <!-- Pantalla 4: Libro interactivo (Slider) -->
  <div id="screen4" class="screen">
    <h2>Recuerdos de Amor</h2>
    <div class="slider">
      <div class="slides">
        <!-- Cada slide corresponde a una página del libro (5 en total) -->
        <div class="slide">
          <img src="https://github.com/tuusuario/tu-repositorio/raw/main/foto1.jpg" alt="Foto 1">
          <div class="caption">Frase de amor 1</div>
        </div>
        <div class="slide">
          <img src="https://github.com/tuusuario/tu-repositorio/raw/main/foto2.jpg" alt="Foto 2">
          <div class="caption">Frase de amor 2</div>
        </div>
        <div class="slide">
          <img src="https://github.com/tuusuario/tu-repositorio/raw/main/foto3.jpg" alt="Foto 3">
          <div class="caption">Frase de amor 3</div>
        </div>
        <div class="slide">
          <img src="https://github.com/tuusuario/tu-repositorio/raw/main/foto4.jpg" alt="Foto 4">
          <div class="caption">Frase de amor 4</div>
        </div>
        <div class="slide">
          <img src="https://github.com/tuusuario/tu-repositorio/raw/main/foto5.jpg" alt="Foto 5">
          <div class="caption">Frase de amor 5</div>
        </div>
      </div>
    </div>
    <div class="slider-controls">
      <button onclick="prevSlide()">Anterior</button>
      <button onclick="nextSlide()">Siguiente</button>
    </div>
  </div>

  <script>
    // Función para mostrar una pantalla y ocultar las demás
    function showScreen(id) {
      document.querySelectorAll('.screen').forEach(screen => {
        screen.style.display = 'none';
      });
      document.getElementById(id).style.display = 'block';
    }
    // Navegar a la Pantalla 2 (gatito)
    function goToScreen2() {
      showScreen('screen2');
      startFloatingHearts();
    }
    // Navegar a la Pantalla 3 (rompecabezas)
    function goToScreen3() {
      showScreen('screen3');
      setupPuzzle();
    }
    // Navegar a la Pantalla 4 (libro/slider)
    function goToScreen4() {
      showScreen('screen4');
    }

    // Función para iniciar los corazones flotantes en Screen2
    function startFloatingHearts() {
      setInterval(() => {
        const heart = document.createElement('div');
        heart.className = 'heart';
        heart.style.left = Math.random() * 100 + 'vw';
        heart.textContent = '❤️';
        heart.style.animationDuration = (Math.random() * 3 + 2) + 's';
        document.body.appendChild(heart);
        setTimeout(() => { heart.remove(); }, 5000);
      }, 500);
    }

    /* ====================
       ROMPECABEZAS (Screen 3)
       ==================== */
    const rows = 3, cols = 3, pieceWidth = 100, pieceHeight = 100;
    function setupPuzzle() {
      const board = document.getElementById('puzzle-board');
      const piecesContainer = document.getElementById('puzzle-pieces');
      board.innerHTML = '';
      piecesContainer.innerHTML = '';
      let pieces = [];
      // Crear celdas en el tablero
      for (let i = 0; i < rows * cols; i++) {
        let cell = document.createElement('div');
        cell.className = 'puzzle-cell';
        cell.dataset.index = i;
        cell.addEventListener('dragover', allowDrop);
        cell.addEventListener('drop', drop);
        board.appendChild(cell);
      }
      // Crear piezas del rompecabezas
      for (let r = 0; r < rows; r++) {
        for (let c = 0; c < cols; c++) {
          let index = r * cols + c;
          let piece = document.createElement('div');
          piece.className = 'puzzle-piece';
          piece.draggable = true;
          piece.dataset.index = index;
          piece.style.backgroundImage = "url('https://raw.githubusercontent.com/Alexiscj23/San-valentines/refs/heads/main/IMG_20190812_212839.jpg
            ')";
          piece.style.backgroundSize = `${cols * pieceWidth}px ${rows * pieceHeight}px`;
          piece.style.backgroundPosition = `-${c * pieceWidth}px -${r * pieceHeight}px`;
          piece.addEventListener('dragstart', dragStart);
          piece.addEventListener('dragend', dragEnd);
          pieces.push(piece);
        }
      }
      // Mezclar piezas
      pieces = shuffleArray(pieces);
      pieces.forEach(piece => piecesContainer.appendChild(piece));
    }
    function shuffleArray(array) {
      for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
      }
      return array;
    }
    let draggedPiece = null;
    function dragStart(e) {
      draggedPiece = this;
      setTimeout(() => { this.style.opacity = '0.5'; }, 0);
    }
    function dragEnd(e) {
      this.style.opacity = '1';
      draggedPiece = null;
    }
    function allowDrop(e) { e.preventDefault(); }
    function drop(e) {
      e.preventDefault();
      if (draggedPiece) {
        if (this.children.length > 0) {
          document.getElementById('puzzle-pieces').appendChild(this.children[0]);
        }
        this.appendChild(draggedPiece);
      }
    }
    function checkPuzzle() {
      let correct = 0;
      document.querySelectorAll('.puzzle-cell').forEach(cell => {
        if (cell.children.length > 0 && cell.children[0].dataset.index === cell.dataset.index)
          correct++;
      });
      if (correct === rows * cols) {
        document.getElementById('puzzle-message').textContent = "¡Rompecabezas armado perfectamente!";
        setTimeout(goToScreen4, 2000);
      } else {
        document.getElementById('puzzle-message').textContent = `Faltan ${rows * cols - correct} piezas correctas.`;
      }
    }

    /* ====================
       SLIDER (Screen 4)
       ==================== */
    let currentSlide = 0;
    function showSlide(index) {
      const slidesContainer = document.querySelector('.slides');
      const totalSlides = slidesContainer.children.length;
      if(index < 0) currentSlide = totalSlides - 1;
      else if(index >= totalSlides) currentSlide = 0;
      else currentSlide = index;
      slidesContainer.style.transform = `translateX(-${currentSlide * 100}%)`;
    }
    function nextSlide() { showSlide(currentSlide + 1); }
    function prevSlide() { showSlide(currentSlide - 1); }
  </script>
</body>
</html>
