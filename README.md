<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Examen Interactivo: Bombas, Turbinas e Hidráulica</title>
  <style>
    :root {
      --bg: #0f172a;
      --panel: #111827;
      --card: #1e293b;
      --accent: #38bdf8;
      --accent-dark: #0284c7;
      --green: #22c55e;
      --green-dark: #15803d;
      --danger: #ef4444;
      --warning: #f59e0b;
      --text: #e5e7eb;
      --muted: #94a3b8;
      --border: #334155;
      --white: #ffffff;
      --purple: #a78bfa;
    }

    * { box-sizing: border-box; }

    body {
      margin: 0;
      font-family: Arial, Helvetica, sans-serif;
      background: radial-gradient(circle at top, #164e63 0, var(--bg) 42%, #020617 100%);
      color: var(--text);
      min-height: 100vh;
    }

    header {
      padding: 32px 18px 18px;
      text-align: center;
    }

    header h1 {
      margin: 0;
      font-size: clamp(26px, 5vw, 46px);
      color: var(--white);
      letter-spacing: -0.5px;
    }

    header p {
      max-width: 900px;
      margin: 12px auto 0;
      color: #cbd5e1;
      line-height: 1.6;
      font-size: 16px;
    }

    .container {
      width: min(1120px, calc(100% - 28px));
      margin: 0 auto 44px;
    }

    .teacher-banner {
      background: rgba(2, 6, 23, .72);
      border: 1px solid var(--border);
      border-radius: 20px;
      padding: 14px 18px;
      text-align: center;
      color: #dbeafe;
      line-height: 1.5;
      margin-bottom: 18px;
    }

    .teacher-banner strong { color: #fff; }

    .student-box {
      display: grid;
      grid-template-columns: 1.4fr .9fr .9fr;
      gap: 12px;
      background: rgba(15, 23, 42, 0.78);
      border: 1px solid var(--border);
      border-radius: 22px;
      padding: 18px;
      margin-bottom: 20px;
      box-shadow: 0 12px 34px rgba(0,0,0,.22);
    }

    .field label {
      display: block;
      font-size: 13px;
      color: #bae6fd;
      margin-bottom: 7px;
      font-weight: 700;
    }

    .field input {
      width: 100%;
      padding: 12px 13px;
      border-radius: 14px;
      border: 1px solid var(--border);
      background: #020617;
      color: var(--white);
      outline: none;
      font-size: 15px;
    }

    .field input:focus {
      border-color: var(--accent);
      box-shadow: 0 0 0 3px rgba(56, 189, 248, .15);
    }

    .choose-blocks {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 18px;
      margin: 22px 0 24px;
    }

    .block-card {
      background: rgba(30, 41, 59, 0.94);
      border: 1px solid var(--border);
      border-radius: 26px;
      padding: 24px;
      box-shadow: 0 16px 40px rgba(0,0,0,.28);
      position: relative;
      overflow: hidden;
      transition: transform .18s ease, border .18s ease;
    }

    .block-card:hover {
      transform: translateY(-4px);
      border-color: var(--accent);
    }

    .block-card::before {
      content: "";
      position: absolute;
      inset: 0 auto 0 0;
      width: 8px;
      background: var(--accent);
    }

    .block-card.turbinas::before { background: var(--green); }

    .block-card h2 {
      margin: 0 0 10px;
      font-size: 26px;
      color: #fff;
    }

    .block-card p {
      color: #cbd5e1;
      line-height: 1.6;
      margin: 0 0 14px;
    }

    .topic-list {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin: 14px 0 18px;
    }

    .chip {
      display: inline-flex;
      align-items: center;
      background: #082f49;
      color: #bae6fd;
      border: 1px solid #075985;
      border-radius: 999px;
      padding: 6px 10px;
      font-size: 12px;
      font-weight: 700;
    }

    .turbinas .chip {
      background: #052e16;
      color: #bbf7d0;
      border-color: #166534;
    }

    button {
      border: 0;
      cursor: pointer;
      border-radius: 999px;
      padding: 12px 18px;
      font-weight: 800;
      color: #031923;
      background: var(--accent);
      transition: transform .15s ease, opacity .15s ease, background .15s ease;
    }

    button:hover { transform: translateY(-2px); }
    button:disabled { opacity: .55; cursor: not-allowed; transform: none; }

    .secondary { background: #cbd5e1; color: #0f172a; }
    .success { background: var(--green); color: #052e16; }
    .danger { background: var(--danger); color: #fff; }
    .warning { background: var(--warning); color: #1f1300; }
    .purple { background: var(--purple); color: #1e1b4b; }

    .exam-area { display: none; }

    .dashboard {
      display: grid;
      grid-template-columns: repeat(5, 1fr);
      gap: 12px;
      margin: 18px 0;
    }

    .stat {
      background: rgba(15, 23, 42, 0.82);
      border: 1px solid var(--border);
      border-radius: 18px;
      padding: 15px;
      box-shadow: 0 10px 28px rgba(0,0,0,.22);
      min-height: 92px;
    }

    .stat span {
      display: block;
      color: var(--muted);
      font-size: 13px;
      margin-bottom: 6px;
    }

    .stat strong {
      font-size: 24px;
      color: var(--white);
    }

    .stat .small-strong { font-size: 18px; line-height: 1.25; }

    .progress-wrap {
      background: #020617;
      border: 1px solid var(--border);
      border-radius: 999px;
      overflow: hidden;
      height: 16px;
      margin: 16px 0 22px;
    }

    .progress-bar {
      height: 100%;
      width: 0%;
      background: linear-gradient(90deg, var(--accent), var(--green));
      transition: width .35s ease;
    }

    .controls {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      justify-content: center;
      margin: 18px 0 26px;
    }

    .result-box {
      display: none;
      margin: 26px 0;
      padding: 24px;
      border-radius: 24px;
      background: linear-gradient(135deg, rgba(8, 47, 73, .96), rgba(15, 23, 42, .96));
      border: 1px solid #0ea5e9;
      box-shadow: 0 18px 44px rgba(0,0,0,.34);
      text-align: center;
    }

    .result-box h2 {
      margin: 0 0 10px;
      font-size: 30px;
    }

    .result-box p {
      color: #dbeafe;
      line-height: 1.6;
      margin: 8px auto;
      max-width: 820px;
    }

    .platform-note {
      margin-top: 18px;
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
    }

    .note-item {
      background: rgba(2, 6, 23, .58);
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 12px;
    }

    .note-item span {
      display: block;
      color: var(--muted);
      font-size: 12px;
      margin-bottom: 5px;
    }

    .note-item strong {
      color: #fff;
      font-size: 18px;
    }

    .quiz {
      display: grid;
      gap: 18px;
    }

    .question-card {
      background: rgba(30, 41, 59, 0.94);
      border: 1px solid var(--border);
      border-radius: 22px;
      padding: 22px;
      box-shadow: 0 16px 40px rgba(0,0,0,.28);
      position: relative;
      overflow: hidden;
    }

    .question-card::before {
      content: "";
      position: absolute;
      top: 0;
      left: 0;
      width: 7px;
      height: 100%;
      background: var(--accent);
    }

    .question-card.turbinas::before { background: var(--green); }

    .question-top {
      display: flex;
      justify-content: space-between;
      gap: 12px;
      align-items: center;
      margin-bottom: 12px;
    }

    .badge {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      background: #082f49;
      color: #bae6fd;
      border: 1px solid #075985;
      border-radius: 999px;
      padding: 6px 11px;
      font-size: 13px;
      font-weight: 700;
    }

    .badge.green {
      background: #052e16;
      color: #bbf7d0;
      border-color: #166534;
    }

    .level {
      font-size: 12px;
      color: #fde68a;
      background: #451a03;
      border: 1px solid #92400e;
      padding: 6px 10px;
      border-radius: 999px;
      white-space: nowrap;
    }

    .question-card h2 {
      font-size: 19px;
      line-height: 1.45;
      margin: 0 0 16px;
      color: var(--white);
    }

    .options {
      display: grid;
      gap: 10px;
    }

    .option {
      display: flex;
      gap: 10px;
      align-items: flex-start;
      background: #0f172a;
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 13px;
      color: var(--text);
      cursor: pointer;
      line-height: 1.45;
      transition: border .15s ease, background .15s ease, transform .15s ease;
    }

    .option:hover {
      border-color: var(--accent);
      transform: translateX(4px);
    }

    .option input {
      margin-top: 4px;
      accent-color: var(--accent);
    }

    .option.correct {
      border-color: var(--green);
      background: rgba(34, 197, 94, .16);
    }

    .option.incorrect {
      border-color: var(--danger);
      background: rgba(239, 68, 68, .14);
    }

    .feedback {
      display: none;
      margin-top: 14px;
      padding: 14px;
      border-radius: 16px;
      background: #020617;
      border: 1px solid var(--border);
      color: #cbd5e1;
      line-height: 1.55;
    }

    .feedback strong { color: var(--white); }

    .history-box {
      margin: 28px 0;
      background: rgba(2, 6, 23, .72);
      border: 1px solid var(--border);
      border-radius: 22px;
      padding: 20px;
      display: none;
    }

    .history-box h2 { margin: 0 0 12px; }

    table {
      width: 100%;
      border-collapse: collapse;
      overflow: hidden;
      border-radius: 14px;
    }

    th, td {
      border-bottom: 1px solid var(--border);
      padding: 11px;
      text-align: left;
      color: #dbeafe;
      font-size: 14px;
    }

    th {
      color: #fff;
      background: #0f172a;
    }

    .footer-note {
      color: var(--muted);
      text-align: center;
      line-height: 1.6;
      margin: 26px 0 8px;
      font-size: 14px;
    }

    @media (max-width: 900px) {
      .student-box { grid-template-columns: 1fr; }
      .choose-blocks { grid-template-columns: 1fr; }
      .dashboard { grid-template-columns: repeat(2, 1fr); }
      .platform-note { grid-template-columns: repeat(2, 1fr); }
    }

    @media (max-width: 560px) {
      .dashboard { grid-template-columns: 1fr; }
      .platform-note { grid-template-columns: 1fr; }
      .question-top { flex-direction: column; align-items: flex-start; }
      .question-card { padding: 18px; }
      button { width: 100%; }
      th, td { font-size: 12px; }
    }
  </style>
</head>
<body>
  <header>
    <h1>Examen Interactivo</h1>
    <p>Elige el bloque con el que deseas empezar. Al presionar <strong>Calificar y enviar nota</strong>, la plataforma calcula tu nota, la muestra en pantalla y abre WhatsApp con el mensaje listo para el docente.</p>
  </header>

  <main class="container">
    <div class="teacher-banner">
      Docente configurado: <strong>WhatsApp +51 940 849 095</strong>. Por seguridad de WhatsApp, el navegador abre el mensaje listo; solo se debe confirmar el envío en WhatsApp.
    </div>

    <section class="student-box" aria-label="Datos del estudiante">
      <div class="field">
        <label for="studentName">Nombre del estudiante</label>
        <input id="studentName" type="text" placeholder="Escribe tu nombre completo" oninput="saveStudentData()" />
      </div>
      <div class="field">
        <label for="studentCode">Código o sección</label>
        <input id="studentCode" type="text" placeholder="Ej.: Sección A" oninput="saveStudentData()" />
      </div>
      <div class="field">
        <label for="courseName">Curso</label>
        <input id="courseName" type="text" value="Turbomáquinas" oninput="saveStudentData()" />
      </div>
    </section>

    <section class="choose-blocks" id="chooseBlocks">
      <article class="block-card">
        <h2>Bloque 1: Bombas</h2>
        <p>Preguntas sobre definición, clasificación, selección, bombas centrífugas, partes, materiales y mantenimiento.</p>
        <div class="topic-list">
          <span class="chip">Bombas</span>
          <span class="chip">Centrífugas</span>
          <span class="chip">Caudal</span>
          <span class="chip">Presión</span>
          <span class="chip">Materiales</span>
        </div>
        <button onclick="startBlock('bombas')">Comenzar Bloque 1</button>
      </article>

      <article class="block-card turbinas">
        <h2>Bloque 2: Turbinas e hidráulica</h2>
        <p>Preguntas sobre centrales hidroeléctricas, turbinas, presas, conducción, cámara de carga, golpe de ariete y chimeneas de equilibrio.</p>
        <div class="topic-list">
          <span class="chip">Turbinas</span>
          <span class="chip">Hidroeléctricas</span>
          <span class="chip">Presa</span>
          <span class="chip">Golpe de ariete</span>
          <span class="chip">Chimenea de equilibrio</span>
        </div>
        <button class="success" onclick="startBlock('turbinas')">Comenzar Bloque 2</button>
      </article>
    </section>

    <section class="exam-area" id="examArea">
      <section class="dashboard" aria-label="Panel de puntuación">
        <div class="stat"><span>Bloque activo</span><strong class="small-strong" id="activeBlock">-</strong></div>
        <div class="stat"><span>Preguntas</span><strong id="totalQuestions">0</strong></div>
        <div class="stat"><span>Respondidas</span><strong id="answeredCount">0</strong></div>
        <div class="stat"><span>Puntaje</span><strong id="scoreCount">0</strong></div>
        <div class="stat"><span>Nota vigesimal</span><strong id="gradeCount">0/20</strong></div>
      </section>

      <div class="progress-wrap" aria-label="Barra de avance">
        <div class="progress-bar" id="progressBar"></div>
      </div>

      <section class="controls">
        <button onclick="checkExamAndSend()" class="success">Calificar y enviar nota al docente</button>
        <button onclick="showAllFeedback()" class="warning">Mostrar explicaciones</button>
        <button onclick="resetCurrentBlock()" class="danger">Reiniciar bloque</button>
        <button onclick="shuffleCurrentBlock()" class="purple">Mezclar preguntas</button>
        <button onclick="backToBlocks()" class="secondary">Cambiar de bloque</button>
      </section>

      <section class="result-box" id="resultBox">
        <h2 id="resultTitle">Resultado</h2>
        <p id="resultText"></p>
        <p id="resultAdvice"></p>
        <div class="platform-note">
          <div class="note-item"><span>Estudiante</span><strong id="platformStudent">-</strong></div>
          <div class="note-item"><span>Bloque</span><strong id="platformBlock">-</strong></div>
          <div class="note-item"><span>Puntaje</span><strong id="platformScore">-</strong></div>
          <div class="note-item"><span>Nota</span><strong id="platformGrade">-</strong></div>
        </div>
      </section>

      <section class="quiz" id="quiz"></section>
    </section>

    <section class="history-box" id="historyBox">
      <h2>Registro de notas en la plataforma</h2>
      <table>
        <thead>
          <tr>
            <th>Fecha</th>
            <th>Estudiante</th>
            <th>Bloque</th>
            <th>Puntaje</th>
            <th>Nota</th>
          </tr>
        </thead>
        <tbody id="historyBody"></tbody>
      </table>
    </section>

    <p class="footer-note">
      La nota queda visible en esta plataforma y también se guarda en el historial local del navegador usado por el estudiante.
    </p>
  </main>

  <script>
    const TEACHER_PHONE = "51940849095";

    const questionBanks = {
      bombas: [
        {
          topic: "Bombas",
          level: "Básico",
          question: "¿Cuál es la función principal de una bomba dentro de un sistema hidráulico?",
          options: [
            "Transformar energía eléctrica directamente en energía química.",
            "Recibir energía mecánica y entregarla al fluido como presión, velocidad o altura.",
            "Eliminar por completo las pérdidas por fricción en una tubería.",
            "Convertir energía del fluido en electricidad sin partes móviles."
          ],
          answer: 1,
          explanation: "Una bomba recibe energía mecánica de un motor y la transmite al fluido, aumentando su presión, velocidad o posición."
        },
        {
          topic: "Concepto",
          level: "Básico",
          question: "Cuando una bomba de pozo profundo lleva agua del subsuelo hacia la superficie, principalmente está aumentando la energía de:",
          options: ["Posición o altura.", "Combustión.", "Radiación.", "Magnetismo."],
          answer: 0,
          explanation: "Al elevar el agua desde una cota inferior a una superior, la bomba incrementa la energía de posición del fluido."
        },
        {
          topic: "Bomba vs. turbina",
          level: "Básico",
          question: "En la comparación hidráulica, ¿cómo se interpreta una bomba?",
          options: ["Como motor hidráulico.", "Como generador hidráulico.", "Como alternador eléctrico.", "Como válvula de seguridad."],
          answer: 1,
          explanation: "La bomba entrega energía al fluido; por eso se compara con un generador hidráulico."
        },
        {
          topic: "Selección",
          level: "Intermedio",
          question: "¿Qué factores son esenciales para seleccionar correctamente el tipo de bomba?",
          options: [
            "Solo el color y la marca.",
            "Presión, caudal y características del líquido como viscosidad, temperatura, pH y sólidos.",
            "Solo el diámetro exterior de la carcasa.",
            "Solo la potencia nominal del motor."
          ],
          answer: 1,
          explanation: "La selección depende de presión, gasto o caudal y propiedades del líquido: viscosidad, temperatura, pH, densidad, abrasión e impurezas."
        },
        {
          topic: "Clasificación",
          level: "Intermedio",
          question: "¿En qué caso suele ser adecuada una bomba de desplazamiento positivo reciprocante?",
          options: [
            "Gastos pequeños, presiones altas y líquidos limpios.",
            "Gastos muy grandes y presiones bajas.",
            "Solo para agua con muchas piedras grandes.",
            "Solo para generar energía eléctrica."
          ],
          answer: 0,
          explanation: "Las bombas reciprocantes se aplican normalmente en caudales pequeños, presiones altas y líquidos limpios."
        },
        {
          topic: "Clasificación",
          level: "Intermedio",
          question: "Las bombas de desplazamiento positivo rotatorias son especialmente útiles para:",
          options: [
            "Líquidos viscosos y gastos pequeños o medianos.",
            "Solo aire comprimido a baja presión.",
            "Grandes caudales con líquidos no viscosos.",
            "Eliminar totalmente la abrasión."
          ],
          answer: 0,
          explanation: "Las rotatorias se usan en gastos pequeños y medianos, presiones altas y líquidos viscosos."
        },
        {
          topic: "Centrífugas",
          level: "Intermedio",
          question: "¿Por qué las bombas centrífugas son muy utilizadas en la práctica?",
          options: [
            "Porque no tienen impulsor.",
            "Porque trabajan solo con líquidos altamente viscosos.",
            "Porque tienen descarga relativamente constante y amplio rango de caudales.",
            "Porque no requieren motor."
          ],
          answer: 2,
          explanation: "Las centrífugas son comunes por su descarga constante, rango amplio de operación y menor complejidad frente a bombas reciprocantes."
        },
        {
          topic: "Partes",
          level: "Básico",
          question: "¿Qué componente de una bomba centrífuga transmite energía directamente al fluido mediante rotación?",
          options: ["Impulsor.", "Cimentación.", "Manómetro.", "Canal de descarga."],
          answer: 0,
          explanation: "El impulsor gira y transfiere energía al líquido, elevando su energía hidráulica."
        },
        {
          topic: "Partes",
          level: "Básico",
          question: "¿Por dónde ingresa normalmente el fluido a una bomba centrífuga?",
          options: ["Boquilla de succión.", "Alternador.", "Vertedero.", "Chimenea de equilibrio."],
          answer: 0,
          explanation: "El fluido entra por la boquilla de succión y sale por la boquilla de descarga."
        },
        {
          topic: "Tamaño",
          level: "Intermedio",
          question: "El tamaño nominal de una bomba centrífuga suele determinarse por:",
          options: [
            "El color de la carcasa.",
            "El diámetro interior de la brida de descarga.",
            "La longitud del cable eléctrico.",
            "La altura del operador."
          ],
          answer: 1,
          explanation: "El tamaño nominal se determina generalmente por el diámetro interior de la brida de descarga, aunque esto no basta para definir el caudal."
        },
        {
          topic: "Rotación",
          level: "Intermedio",
          question: "Para identificar el sentido de rotación de una bomba horizontal, el observador debe ubicarse:",
          options: [
            "En el lado del acople de la bomba.",
            "Debajo de la cimentación.",
            "Dentro de la tubería de descarga.",
            "En el canal de desfogue."
          ],
          answer: 0,
          explanation: "En bombas horizontales, el punto de observación se toma desde el lado del acople."
        },
        {
          topic: "Materiales",
          level: "Intermedio",
          question: "¿Qué condición del servicio puede influir en la selección de materiales de una bomba?",
          options: [
            "Corrosión, abrasión, temperatura, carga de operación y vida esperada.",
            "Solo la forma del tablero eléctrico.",
            "Solo el color del impulsor.",
            "La cantidad de ventanas del ambiente."
          ],
          answer: 0,
          explanation: "El material debe seleccionarse considerando corrosión, acción electroquímica, abrasión, temperatura, carga y vida esperada."
        },
        {
          topic: "Mantenimiento",
          level: "Intermedio",
          question: "¿Qué problema puede observarse en el mantenimiento correctivo de bombas expuestas a agua con sólidos o ambiente agresivo?",
          options: ["Corrosión y desgaste.", "Aumento ilimitado de eficiencia.", "Desaparición del eje.", "Generación eléctrica directa."],
          answer: 0,
          explanation: "El desgaste, la corrosión y la abrasión son problemas comunes que deben revisarse en mantenimiento."
        },
        {
          topic: "Aplicación",
          level: "Avanzado",
          question: "Si se requiere mover grandes caudales con presiones reducidas o medianas y líquidos no muy viscosos, conviene evaluar una bomba:",
          options: ["Centrífuga.", "Manual de bicicleta.", "Exclusivamente reciprocante.", "Sin impulsor."],
          answer: 0,
          explanation: "Las bombas dinámicas del tipo centrífugo se aplican en gastos grandes y presiones reducidas o medianas."
        },
        {
          topic: "Comprensión",
          level: "Avanzado",
          question: "¿Por qué el diámetro de descarga por sí solo no define el caudal real de una bomba centrífuga?",
          options: [
            "Porque también influyen la velocidad de rotación y el diámetro del impulsor.",
            "Porque el caudal solo depende de la pintura.",
            "Porque la descarga no existe en bombas centrífugas.",
            "Porque el caudal siempre es cero."
          ],
          answer: 0,
          explanation: "El caudal depende de variables como velocidad de rotación, diámetro del impulsor y condiciones de operación, no solo del tamaño nominal."
        }
      ],
      turbinas: [
        {
          topic: "Hidroeléctricas",
          level: "Básico",
          question: "¿Qué es una central hidroeléctrica?",
          options: [
            "Una instalación que aprovecha masas de agua en movimiento para generar electricidad mediante turbinas y alternadores.",
            "Un sistema que solo almacena agua sin producir energía.",
            "Una bomba que eleva agua hacia una montaña.",
            "Una instalación que convierte arena en electricidad."
          ],
          answer: 0,
          explanation: "Una central hidroeléctrica aprovecha la energía del agua para mover turbinas acopladas a alternadores."
        },
        {
          topic: "Energía",
          level: "Básico",
          question: "¿Cuál es la secuencia energética general en una central hidroeléctrica?",
          options: [
            "Energía eléctrica → energía química → energía hidráulica.",
            "Energía potencial → energía cinética → energía mecánica de rotación → energía eléctrica.",
            "Energía térmica → energía nuclear → energía hidráulica.",
            "Energía eléctrica → energía potencial → energía cinética."
          ],
          answer: 1,
          explanation: "El agua posee energía potencial; al conducirse adquiere energía cinética; mueve la turbina y el alternador produce electricidad."
        },
        {
          topic: "Turbina",
          level: "Básico",
          question: "¿Qué función cumple la turbina hidráulica?",
          options: [
            "Transforma la energía del agua en energía mecánica de rotación.",
            "Almacena sedimentos finos.",
            "Eleva el pH del río.",
            "Reemplaza la presa."
          ],
          answer: 0,
          explanation: "La turbina recibe la energía del agua y la convierte en movimiento rotacional para accionar el alternador."
        },
        {
          topic: "Potencia",
          level: "Intermedio",
          question: "¿Qué expresa la potencia efectiva en una central hidroeléctrica?",
          options: [
            "La capacidad real de energía que se puede entregar de forma continua.",
            "La capacidad ideal sin condiciones reales.",
            "La potencia de los sedimentos.",
            "La energía usada solo para iluminación interna."
          ],
          answer: 0,
          explanation: "La potencia efectiva representa la capacidad real de entrega continua."
        },
        {
          topic: "Componentes",
          level: "Intermedio",
          question: "¿Cuál de los siguientes pertenece al conjunto de obras hidráulicas?",
          options: [
            "Presa, toma, desarenador, cámara de carga y tubería forzada.",
            "Alternador, excitación y regulador de tensión.",
            "Transformador domiciliario.",
            "Medidor de energía de una vivienda."
          ],
          answer: 0,
          explanation: "Las obras hidráulicas almacenan, captan, conducen y regulan el agua antes y después de la turbina."
        },
        {
          topic: "Presa",
          level: "Básico",
          question: "¿Cuál es la función principal de una presa?",
          options: [
            "Elevar el nivel del agua, crear desnivel y permitir control o derivación del caudal.",
            "Eliminar la energía potencial del agua.",
            "Reemplazar al alternador.",
            "Aumentar la arena hacia la turbina."
          ],
          answer: 0,
          explanation: "La presa eleva el nivel del agua, forma embalse y facilita el aprovechamiento energético."
        },
        {
          topic: "Captación",
          level: "Intermedio",
          question: "La toma o captación sirve principalmente para:",
          options: [
            "Permitir el ingreso controlado del agua hacia el sistema de conducción.",
            "Convertir directamente electricidad en agua.",
            "Destruir la tubería forzada.",
            "Aumentar el golpe de ariete."
          ],
          answer: 0,
          explanation: "La captación dirige el agua desde el río, canal o embalse hacia la conducción de la central."
        },
        {
          topic: "Aliviadores",
          level: "Intermedio",
          question: "¿Para qué sirven los aliviadores?",
          options: [
            "Para evacuar caudales excedentes y proteger el sistema durante crecidas.",
            "Para introducir piedras grandes al sistema.",
            "Para cerrar permanentemente el canal.",
            "Para medir la nota del estudiante."
          ],
          answer: 0,
          explanation: "Los aliviadores evacuan caudales superiores a los deseados, cumpliendo una función de seguridad."
        },
        {
          topic: "Desripiador",
          level: "Intermedio",
          question: "¿Qué separa principalmente un desripiador?",
          options: [
            "Material grueso como ramas, piedras grandes o elementos flotantes.",
            "Energía eléctrica del alternador.",
            "Vapor de agua de la turbina.",
            "Solo moléculas de oxígeno."
          ],
          answer: 0,
          explanation: "El desripiador retiene material grueso antes de que el agua pase a etapas más finas de limpieza."
        },
        {
          topic: "Desarenador",
          level: "Intermedio",
          question: "¿Cuál es el objetivo principal de un desarenador?",
          options: [
            "Reducir la velocidad del agua para que arena y partículas se depositen antes de llegar a la turbina.",
            "Aumentar la cantidad de arena hacia la turbina.",
            "Eliminar la necesidad de presa.",
            "Transformar presión en calificación."
          ],
          answer: 0,
          explanation: "El desarenador sedimenta partículas, reduciendo el desgaste por abrasión en la turbina."
        },
        {
          topic: "Conducción",
          level: "Intermedio",
          question: "Los canales, túneles y galerías de conducción se usan para:",
          options: [
            "Conducir el agua desde la captación hasta la tubería forzada o cámara de carga.",
            "Guardar notas académicas.",
            "Reemplazar todos los equipos electromecánicos.",
            "Aumentar la sedimentación dentro de la turbina."
          ],
          answer: 0,
          explanation: "Estos conductos artificiales trasladan el agua hacia la zona donde se aprovecha su energía."
        },
        {
          topic: "Cámara de carga",
          level: "Intermedio",
          question: "¿Qué función cumple la cámara de carga?",
          options: [
            "Amortiguar ondas de presión y proveer volumen de agua antes de la tubería forzada.",
            "Reemplazar al alternador.",
            "Eliminar todas las compuertas.",
            "Servir solo como oficina."
          ],
          answer: 0,
          explanation: "La cámara de carga ayuda a regular el caudal y amortiguar variaciones de presión por maniobras bruscas."
        },
        {
          topic: "Golpe de ariete",
          level: "Avanzado",
          question: "¿Qué describe mejor el golpe de ariete?",
          options: [
            "Una variación brusca de presión causada por cambios rápidos en la velocidad del agua dentro de una tubería.",
            "Un tipo de presa de concreto armado.",
            "Una falla exclusiva del generador eléctrico.",
            "Una forma de aumentar sedimentos."
          ],
          answer: 0,
          explanation: "El golpe de ariete se produce por cierres o aperturas bruscas que generan ondas de presión."
        },
        {
          topic: "Chimenea de equilibrio",
          level: "Avanzado",
          question: "¿Cómo ayuda una chimenea de equilibrio ante una sobrepresión?",
          options: [
            "Permite que el nivel de agua suba y transforma parte de la energía cinética en energía potencial.",
            "Bloquea totalmente el paso de agua sin variación de nivel.",
            "Convierte directamente presión en energía eléctrica.",
            "Aumenta la sobrepresión hasta romper la tubería."
          ],
          answer: 0,
          explanation: "Ante sobrepresión, el agua asciende en la chimenea, amortiguando el golpe de ariete."
        },
        {
          topic: "Tipos de centrales",
          level: "Intermedio",
          question: "¿Qué caracteriza a una central de pasada o agua fluente?",
          options: [
            "Utiliza el agua mientras fluye por el río y su producción depende del caudal disponible.",
            "Siempre tiene gran embalse anual y caudal constante.",
            "No requiere toma ni turbina.",
            "Funciona con vapor, no con agua."
          ],
          answer: 0,
          explanation: "Las centrales de pasada dependen del caudal natural; producen más en avenidas y menos en estiaje."
        },
        {
          topic: "Tipos de centrales",
          level: "Intermedio",
          question: "¿Qué caracteriza a una central a pie de presa?",
          options: [
            "La sala de máquinas se ubica aguas abajo, cerca de la base de la presa, aprovechando el desnivel creado.",
            "No utiliza presa ni tubería.",
            "Solo funciona con viento.",
            "No necesita turbina."
          ],
          answer: 0,
          explanation: "En centrales a pie de presa, la presa genera el desnivel y la casa de máquinas se ubica en la parte inferior aguas abajo."
        }
      ]
    };

    let activeBlockKey = null;
    let currentQuestions = [];

    const quiz = document.getElementById("quiz");

    function saveStudentData() {
      const data = {
        name: document.getElementById("studentName").value,
        code: document.getElementById("studentCode").value,
        course: document.getElementById("courseName").value
      };
      localStorage.setItem("studentDataTurbomaquinas", JSON.stringify(data));
    }

    function loadStudentData() {
      const saved = localStorage.getItem("studentDataTurbomaquinas");
      if (!saved) return;
      try {
        const data = JSON.parse(saved);
        document.getElementById("studentName").value = data.name || "";
        document.getElementById("studentCode").value = data.code || "";
        document.getElementById("courseName").value = data.course || "Turbomáquinas";
      } catch (e) {}
    }

    function blockTitle(key) {
      return key === "bombas" ? "Bloque 1: Bombas" : "Bloque 2: Turbinas e hidráulica";
    }

    function startBlock(key) {
      activeBlockKey = key;
      currentQuestions = [...questionBanks[key]];
      document.getElementById("chooseBlocks").style.display = "none";
      document.getElementById("examArea").style.display = "block";
      document.getElementById("activeBlock").textContent = blockTitle(key);
      document.getElementById("resultBox").style.display = "none";
      renderQuiz();
      window.scrollTo({ top: 0, behavior: "smooth" });
    }

    function renderQuiz() {
      quiz.innerHTML = "";
      document.getElementById("totalQuestions").textContent = currentQuestions.length;
      document.getElementById("scoreCount").textContent = "0";
      document.getElementById("gradeCount").textContent = "0/20";

      currentQuestions.forEach((q, index) => {
        const card = document.createElement("article");
        card.className = "question-card " + (activeBlockKey === "turbinas" ? "turbinas" : "");
        card.dataset.index = index;

        const optionsHTML = q.options.map((opt, optIndex) => `
          <label class="option" data-option="${optIndex}">
            <input type="radio" name="q${index}" value="${optIndex}" onchange="updateStats()" />
            <span><strong>${String.fromCharCode(65 + optIndex)}.</strong> ${opt}</span>
          </label>
        `).join("");

        card.innerHTML = `
          <div class="question-top">
            <span class="badge ${activeBlockKey === "turbinas" ? "green" : ""}">Pregunta ${index + 1} · ${q.topic}</span>
            <span class="level">Nivel: ${q.level}</span>
          </div>
          <h2>${q.question}</h2>
          <div class="options">${optionsHTML}</div>
          <div class="feedback" id="feedback-${index}">
            <strong>Explicación:</strong> ${q.explanation}
          </div>
        `;

        quiz.appendChild(card);
      });

      updateStats();
    }

    function updateStats() {
      let answered = 0;
      currentQuestions.forEach((_, index) => {
        if (document.querySelector(`input[name="q${index}"]:checked`)) answered++;
      });
      document.getElementById("answeredCount").textContent = answered;
      document.getElementById("progressBar").style.width = `${(answered / currentQuestions.length) * 100}%`;
    }

    function checkExamAndSend() {
      const studentName = document.getElementById("studentName").value.trim();
      const studentCode = document.getElementById("studentCode").value.trim();
      const courseName = document.getElementById("courseName").value.trim() || "Turbomáquinas";

      if (!studentName) {
        alert("Antes de calificar, escribe el nombre del estudiante.");
        document.getElementById("studentName").focus();
        return;
      }

      let score = 0;
      let answered = 0;

      currentQuestions.forEach((q, index) => {
        const selected = document.querySelector(`input[name="q${index}"]:checked`);
        const card = document.querySelector(`.question-card[data-index="${index}"]`);
        const labels = card.querySelectorAll(".option");
        labels.forEach(label => label.classList.remove("correct", "incorrect"));

        if (selected) {
          answered++;
          const selectedValue = Number(selected.value);
          if (selectedValue === q.answer) {
            score++;
            labels[selectedValue].classList.add("correct");
          } else {
            labels[selectedValue].classList.add("incorrect");
            labels[q.answer].classList.add("correct");
          }
        } else {
          labels[q.answer].classList.add("correct");
        }

        document.getElementById(`feedback-${index}`).style.display = "block";
      });

      const percent = Math.round((score / currentQuestions.length) * 100);
      const grade = ((score / currentQuestions.length) * 20).toFixed(2);
      const now = new Date();
      const dateText = now.toLocaleString("es-PE");

      document.getElementById("scoreCount").textContent = score;
      document.getElementById("gradeCount").textContent = `${grade}/20`;
      document.getElementById("answeredCount").textContent = answered;
      document.getElementById("progressBar").style.width = `${(answered / currentQuestions.length) * 100}%`;

      showResult(score, percent, grade, studentName, studentCode, courseName, dateText);
      saveGradeToPlatform(dateText, studentName, studentCode, courseName, score, grade);
      openWhatsAppReport(studentName, studentCode, courseName, score, percent, grade, dateText);
    }

    function showResult(score, percent, grade, studentName, studentCode, courseName, dateText) {
      const resultBox = document.getElementById("resultBox");
      const title = document.getElementById("resultTitle");
      const text = document.getElementById("resultText");
      const advice = document.getElementById("resultAdvice");

      resultBox.style.display = "block";
      title.textContent = `Nota obtenida: ${grade}/20`;
      text.textContent = `${studentName}${studentCode ? " · " + studentCode : ""} resolvió ${blockTitle(activeBlockKey)} con ${score} de ${currentQuestions.length} respuestas correctas (${percent}%).`;

      if (percent >= 90) {
        advice.textContent = "Resultado excelente. El estudiante domina el bloque evaluado.";
      } else if (percent >= 70) {
        advice.textContent = "Buen resultado. Se recomienda repasar las preguntas falladas para consolidar el tema.";
      } else if (percent >= 50) {
        advice.textContent = "Resultado en proceso. Se recomienda reforzar los conceptos principales del bloque.";
      } else {
        advice.textContent = "Resultado bajo. Se recomienda volver a estudiar el bloque antes de una nueva evaluación.";
      }

      document.getElementById("platformStudent").textContent = studentName;
      document.getElementById("platformBlock").textContent = activeBlockKey === "bombas" ? "Bloque 1" : "Bloque 2";
      document.getElementById("platformScore").textContent = `${score}/${currentQuestions.length}`;
      document.getElementById("platformGrade").textContent = `${grade}/20`;

      resultBox.scrollIntoView({ behavior: "smooth", block: "center" });
    }

    function openWhatsAppReport(studentName, studentCode, courseName, score, percent, grade, dateText) {
      const message =
`NOTA DE EXAMEN - ${courseName}

Estudiante: ${studentName}
${studentCode ? "Código/Sección: " + studentCode + "
" : ""}Bloque: ${blockTitle(activeBlockKey)}
Puntaje: ${score}/${currentQuestions.length}
Porcentaje: ${percent}%
Nota vigesimal: ${grade}/20
Fecha: ${dateText}

Mensaje generado automáticamente desde la plataforma HTML.`;

      const url = `https://wa.me/${TEACHER_PHONE}?text=${encodeURIComponent(message)}`;
      window.open(url, "_blank");
    }

    function saveGradeToPlatform(dateText, studentName, studentCode, courseName, score, grade) {
      const item = {
        date: dateText,
        student: studentName,
        code: studentCode,
        course: courseName,
        block: blockTitle(activeBlockKey),
        score: `${score}/${currentQuestions.length}`,
        grade: `${grade}/20`
      };

      const saved = JSON.parse(localStorage.getItem("gradeHistoryTurbomaquinas") || "[]");
      saved.unshift(item);
      localStorage.setItem("gradeHistoryTurbomaquinas", JSON.stringify(saved.slice(0, 20)));
      renderHistory();
    }

    function renderHistory() {
      const saved = JSON.parse(localStorage.getItem("gradeHistoryTurbomaquinas") || "[]");
      const box = document.getElementById("historyBox");
      const body = document.getElementById("historyBody");

      if (!saved.length) {
        box.style.display = "none";
        return;
      }

      box.style.display = "block";
      body.innerHTML = saved.map(item => `
        <tr>
          <td>${item.date}</td>
          <td>${item.student}${item.code ? " · " + item.code : ""}</td>
          <td>${item.block}</td>
          <td>${item.score}</td>
          <td><strong>${item.grade}</strong></td>
        </tr>
      `).join("");
    }

    function showAllFeedback() {
      currentQuestions.forEach((_, index) => {
        const feedback = document.getElementById(`feedback-${index}`);
        if (feedback) feedback.style.display = "block";
      });
    }

    function resetCurrentBlock() {
      document.querySelectorAll("input[type='radio']").forEach(input => input.checked = false);
      document.querySelectorAll(".option").forEach(label => label.classList.remove("correct", "incorrect"));
      document.querySelectorAll(".feedback").forEach(f => f.style.display = "none");
      document.getElementById("scoreCount").textContent = "0";
      document.getElementById("gradeCount").textContent = "0/20";
      document.getElementById("answeredCount").textContent = "0";
      document.getElementById("progressBar").style.width = "0%";
      document.getElementById("resultBox").style.display = "none";
      window.scrollTo({ top: 0, behavior: "smooth" });
    }

    function shuffleCurrentBlock() {
      currentQuestions = currentQuestions
        .map(value => ({ value, sort: Math.random() }))
        .sort((a, b) => a.sort - b.sort)
        .map(({ value }) => value);
      document.getElementById("resultBox").style.display = "none";
      renderQuiz();
      window.scrollTo({ top: 0, behavior: "smooth" });
    }

    function backToBlocks() {
      document.getElementById("examArea").style.display = "none";
      document.getElementById("chooseBlocks").style.display = "grid";
      document.getElementById("resultBox").style.display = "none";
      window.scrollTo({ top: 0, behavior: "smooth" });
    }

    loadStudentData();
    renderHistory();
  </script>
</body>
</html>
