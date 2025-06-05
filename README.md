# Create-your-dream-Horse
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Unique PRE Horses - Diseña tu caballo ideal</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 700px;
      margin: 20px auto;
      padding: 0 15px;
      background: #fafafa;
    }
    h1 {
      text-align: center;
      color: #4B3B2B;
    }
    .phase {
      display: none;
      margin-top: 20px;
    }
    .phase.active {
      display: block;
    }
    .options {
      display: flex;
      justify-content: space-around;
      flex-wrap: wrap;
      margin-top: 15px;
    }
    .option {
      border: 3px solid transparent;
      border-radius: 8px;
      cursor: pointer;
      margin: 10px;
      max-width: 150px;
      transition: border-color 0.3s;
    }
    .option img {
      max-width: 100%;
      border-radius: 8px;
      display: block;
    }
    .option.selected {
      border-color: #a26e49;
      box-shadow: 0 0 10px rgba(162, 110, 73, 0.7);
    }
    button {
      background-color: #a26e49;
      color: white;
      border: none;
      padding: 12px 25px;
      font-size: 1rem;
      border-radius: 5px;
      cursor: pointer;
      margin-top: 25px;
      display: block;
      margin-left: auto;
      margin-right: auto;
      transition: background-color 0.3s;
    }
    button:hover {
      background-color: #7a5231;
    }
    .error {
      color: red;
      text-align: center;
      margin-top: 10px;
    }
  </style>
</head>
<body>

  <h1>Diseña tu caballo ideal - Unique PRE Horses</h1>

  <!-- Fase 1: Elegir raza -->
  <div class="phase active" id="phase1">
    <h2>¿Qué raza prefieres?</h2>
    <div class="options" id="breedOptions">
      <div class="option" data-value="PRE">
        <img src="https://i.imgur.com/9a8qBbH.jpg" alt="Raza PRE" />
        <p style="text-align:center;">PRE</p>
      </div>
      <div class="option" data-value="PSL">
        <img src="https://i.imgur.com/E3H9OvA.jpg" alt="Raza PSL" />
        <p style="text-align:center;">PSL</p>
      </div>
      <div class="option" data-value="Mezcla">
        <img src="https://i.imgur.com/8xvTqKa.jpg" alt="Raza Mezcla" />
        <p style="text-align:center;">Mezcla</p>
      </div>
    </div>
    <button id="next1">Siguiente</button>
    <p class="error" id="error1" style="display:none;">Por favor, selecciona una raza.</p>
  </div>

  <!-- Fase 2: Elegir color -->
  <div class="phase" id="phase2">
    <h2>¿Qué color prefieres?</h2>
    <div class="options" id="colorOptions">
      <div class="option" data-value="Blanco">
        <img src="https://i.imgur.com/xyqImA8.jpg" alt="Color Blanco" />
        <p style="text-align:center;">Blanco</p>
      </div>
      <div class="option" data-value="Marrón">
        <img src="https://i.imgur.com/Vo5dJ6S.jpg" alt="Color Marrón" />
        <p style="text-align:center;">Marrón</p>
      </div>
      <div class="option" data-value="Negro">
        <img src="https://i.imgur.com/qHVf8Fn.jpg" alt="Color Negro" />
        <p style="text-align:center;">Negro</p>
      </div>
      <div class="option" data-value="Alazán">
        <img src="https://i.imgur.com/k1CQ4Cy.jpg" alt="Color Alazán" />
        <p style="text-align:center;">Alazán</p>
      </div>
    </div>
    <button id="next2">Siguiente</button>
    <p class="error" id="error2" style="display:none;">Por favor, selecciona un color.</p>
  </div>

  <!-- Fase 3: Resumen -->
  <div class="phase" id="phase3">
    <h2>¡Este es tu caballo ideal!</h2>
    <p><strong>Raza:</strong> <span id="selectedBreed"></span></p>
    <p><strong>Color:</strong> <span id="selectedColor"></span></p>
    <button id="restart">Diseñar otro caballo</button>
  </div>

<script>
  // Variables para guardar las selecciones
  let selectedBreed = null;
  let selectedColor = null;

  // Función para manejar selección de opciones
  function setupOptions(phaseId, optionClass, callback) {
    const options = document.querySelectorAll(`#${phaseId} .option`);
    options.forEach(option => {
      option.addEventListener('click', () => {
        options.forEach(o => o.classList.remove('selected'));
        option.classList.add('selected');
        callback(option.getAttribute('data-value'));
      });
    });
  }

  // Mostrar fase y ocultar otras
  function showPhase(phaseId) {
    document.querySelectorAll('.phase').forEach(phase => {
      phase.classList.remove('active');
    });
    document.getElementById(phaseId).classList.add('active');
  }

  // Fase 1: Raza
  setupOptions('phase1', 'option', (value) => {
    selectedBreed = value;
    document.getElementById('error1').style.display = 'none';
  });

  document.getElementById('next1').addEventListener('click', () => {
    if (!selectedBreed) {
      document.getElementById('error1').style.display = 'block';
      return;
    }
    showPhase('phase2');
  });

  // Fase 2: Color
  setupOptions('phase2', 'option', (value) => {
    selectedColor = value;
    document.getElementById('error2').style.display = 'none';
  });

  document.getElementById('next2').addEventListener('click', () => {
    if (!selectedColor) {
      document.getElementById('error2').style.display = 'block';
      return;
    }
    // Mostrar resumen
    document.getElementById('selectedBreed').textContent = selectedBreed;
    document.getElementById('selectedColor').textContent = selectedColor;
    showPhase('phase3');
  });

  // Reiniciar el cuestionario
  document.getElementById('restart').addEventListener('click', () => {
    selectedBreed = null;
    selectedColor = null;
    document.querySelectorAll('.option').forEach(o => o.classList.remove('selected'));
    showPhase('phase1');
  });
</script>

</body>
</html>
