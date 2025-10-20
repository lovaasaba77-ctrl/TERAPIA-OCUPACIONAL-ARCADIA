<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Lista de Verificación Terapia Ocupacional 2025</title>
<style>
  body { font-family: Arial, sans-serif; margin: 20px; background: #f5f5f5; }
  h1,h2 { color: #2c3e50; }
  fieldset { margin-bottom: 15px; padding: 15px; background: #fff; border-radius: 5px; }
  label { display: block; margin-bottom: 5px; }
  input[type="text"], input[type="number"], textarea { width: 100%; padding: 5px; margin-bottom: 10px; }
  .checkbox-group { margin-left: 20px; }
  button { padding: 10px 15px; margin: 5px 0; background-color: #2980b9; color: #fff; border: none; border-radius: 5px; cursor: pointer; }
  button:hover { background-color: #3498db; }
  #informe { white-space: pre-wrap; background: #ecf0f1; padding: 10px; border-radius: 5px; margin-top: 10px; }
</style>
</head>
<body>
<h1>Lista de Verificación Terapia Ocupacional 2025</h1>

<fieldset>
  <legend>Datos del Paciente</legend>
  <label>Nombre: <input type="text" id="nombre"></label>
  <label>Edad: <input type="number" id="edad"></label>
  <label>Fecha: <input type="text" id="fecha" placeholder="dd/mm/aaaa"></label>
  <label>Terapeuta: <input type="text" id="terapeuta"></label>
</fieldset>

<fieldset>
  <legend>Motricidad Fina</legend>
  <div class="checkbox-group">
    <label><input type="checkbox" value="Realiza encaje de piezas en tablero"> Realiza encaje de piezas en tablero</label>
    <label><input type="checkbox" value="Realiza ensarte de piezas"> Realiza ensarte de piezas</label>
    <label><input type="checkbox" value="Coloca monedas en tarro"> Coloca monedas en tarro</label>
    <label><input type="checkbox" value="Manipula objetos pequeños"> Manipula objetos pequeños</label>
    <label><input type="checkbox" value="Realiza coordinación óculomanual"> Realiza coordinación óculomanual</label>
    <label><input type="checkbox" value="Encaja y desencaja piezas con resistencia"> Encaja y desencaja piezas con resistencia</label>
    <label><input type="checkbox" value="Abre y cierra tarros (enroscar y desenroscar)"> Abre y cierra tarros (enroscar y desenroscar)</label>
    <label><input type="checkbox" value="Hace pinza fina con y sin resistencia"> Hace pinza fina con y sin resistencia</label>
    <label><input type="checkbox" value="Manipula plastilina (aplasta, amasa y moldea)"> Manipula plastilina (aplasta, amasa y moldea)</label>
    <label><input type="checkbox" value="Recorta figuras"> Recorta figuras</label>
    <label><input type="checkbox" value="Rasga figuras"> Rasga figuras</label>
    <label><input type="checkbox" value="Simula el uso de herramientas (atornilla, desenrosca)"> Simula el uso de herramientas (atornilla, desenrosca)</label>
  </div>
</fieldset>

<!-- Aquí se pueden añadir los demás ítems: Grafo, Visoperceptual, Atención, Aritmética, Lectoescritura, AVD, Lenguaje, Programas específicos, Apoyos y estrategias, Conductas en exceso, Neurodesarrollo -->

<fieldset>
  <legend>Observaciones adicionales</legend>
  <textarea id="observaciones" rows="5" placeholder="Anota conductas, tolerancia, participación, etc."></textarea>
</fieldset>

<button onclick="generarInforme()">Generar Informe</button>
<button onclick="descargarPDF()">Descargar PDF</button>

<h2>Informe Final</h2>
<div id="informe"></div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<script>
function generarInforme() {
  const nombre = document.getElementById('nombre').value;
  const edad = document.getElementById('edad').value;
  const fecha = document.getElementById('fecha').value;
  const terapeuta = document.getElementById('terapeuta').value;
  const observaciones = document.getElementById('observaciones').value;

  let items = [];
  document.querySelectorAll('input[type="checkbox"]:checked').forEach(cb => {
    items.push(cb.value);
  });

  const texto = `
Datos del Paciente
Nombre: ${nombre}
Edad: ${edad}
Fecha: ${fecha}
Terapeuta: ${terapeuta}

OBJETIVOS DE PROGRAMAS IMPLEMENTADOS:
Se implementan programas orientados al desarrollo de habilidades motoras, cognitivas, sensoriales y de autorregulación emocional, mediante estrategias adaptadas al perfil del paciente y su nivel de participación.

EXPLORACIÓN / EVALUACIÓN:
Durante la sesión, se trabajan las siguientes actividades:
${items.map(i => '- ' + i).join('\n')}

EVOLUCIÓN / OBSERVACIONES:
${observaciones}

RECOMENDACIONES:
Continuar con estrategias estructuradas y reforzadores específicos para mantener la motivación. Implementar rutinas visuales y actividades sensoriales reguladoras. Involucrar a la familia en la generalización de logros observados en contexto terapéutico.
`;

  document.getElementById('informe').innerText = texto;
}

function descargarPDF() {
  const { jsPDF } = window.jspdf;
  const doc = new jsPDF();
  let texto = document.getElementById('informe').innerText;
  let lines = doc.splitTextToSize(texto, 180);
  doc.text(lines, 10, 10);
  doc.save('Informe_Terapia_Ocupacional.pdf');
}
</script>

</body>
</html>
