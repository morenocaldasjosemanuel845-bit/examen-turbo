<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Examen Interactivo: Turbomáquinas e Hidroeléctricas</title>
  <style>
    :root {
      --bg: #0f172a;
      --panel: #111827;
      --card: #1e293b;
      --accent: #38bdf8;
      --accent-2: #22c55e;
      --danger: #ef4444;
      --warning: #f59e0b;
      --text: #e5e7eb;
      --muted: #94a3b8;
      --border: #334155;
      --white: #ffffff;
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
      padding: 32px 18px 20px;
      text-align: center;
    }

    header h1 {
      margin: 0;
      font-size: clamp(26px, 5vw, 46px);
      color: var(--white);
      letter-spacing: -0.5px;
    }

    header p {
      max-width: 850px;
      margin: 12px auto 0;
      color: #cbd5e1;
      line-height: 1.6;
      font-size: 16px;
    }

    .container {
      width: min(1100px, calc(100% - 28px));
      margin: 0 auto 40px;
    }

    .dashboard {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 14px;
      margin: 18px 0;
    }

    .stat {
      background: rgba(15, 23, 42, 0.8);
      border: 1px solid var(--border);
      border-radius: 18px;
      padding: 16px;
      box-shadow: 0 10px 28px rgba(0,0,0,.25);
    }

    .stat span {
      display: block;
      color: var(--muted);
      font-size: 13px;
      margin-bottom: 6px;
    }

    .stat strong {
      font-size: 26px;
      color: var(--white);
    }

    .progress-wrap {
      background: #020617;
      border: 1px solid var(--border);
      border-radius: 999px;
      overflow: hidden;
      height: 16px;
      margin: 16px 0 24px;
    }

    .progress-bar {
      height: 100%;
      width: 0%;
      background: linear-gradient(90deg, var(--accent), var(--accent-2));
      transition: width .35s ease;
    }

    .controls {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      justify-content: center;
      margin: 18px 0 28px;
    }

    button {
      border: 0;
      cursor: pointer;
      border-radius: 999px;
      padding: 12px 18px;
      font-weight: 700;
      color: #031923;
      background: var(--accent);
      transition: transform .15s ease, opacity .15s ease, background .15s ease;
    }

    button:hover { transform: translateY(-2px); }
    button:disabled { opacity: .55; cursor: not-allowed; transform: none; }

    .secondary { background: #cbd5e1; color: #0f172a; }
    .success { background: var(--accent-2); color: #052e16; }
    .danger { background: var(--danger); color: #fff; }
    .warning { background: var(--warning); color: #1f1300; }

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
      border-color: var(--accent-2);
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

    .result-box {
      display: none;
      margin: 26px 0;
      padding: 24px;
      border-radius: 24px;
      background: linear-gradient(135deg, rgba(8, 47, 73, .95), rgba(15, 23, 42, .95));
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
      max-width: 760px;
    }

    .mini-game {
      margin: 28px 0;
      padding: 22px;
      background: rgba(2, 6, 23, .76);
      border: 1px solid var(--border);
      border-radius: 22px;
    }

    .mini-game h2 {
      margin: 0 0 8px;
    }

    .mini-game p {
      color: #cbd5e1;
      line-height: 1.6;
    }

    .flashcards {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 12px;
      margin-top: 16px;
    }

    .flashcard {
      min-height: 120px;
      perspective: 900px;
      cursor: pointer;
    }

    .flash-inner {
      height: 100%;
      position: relative;
      transform-style: preserve-3d;
      transition: transform .5s ease;
    }

    .flashcard.flipped .flash-inner {
      transform: rotateY(180deg);
    }

    .flash-front,
    .flash-back {
      position: absolute;
      inset: 0;
      backface-visibility: hidden;
      border-radius: 18px;
      padding: 16px;
      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;
      border: 1px solid var(--border);
      font-weight: 700;
      line-height: 1.45;
    }

    .flash-front {
      background: #1e293b;
      color: #e0f2fe;
    }

    .flash-back {
      background: #082f49;
      color: #bae6fd;
      transform: rotateY(180deg);
    }

    .footer-note {
      color: var(--muted);
      text-align: center;
      line-height: 1.6;
      margin: 26px 0 8px;
      font-size: 14px;
    }

    @media (max-width: 850px) {
      .dashboard { grid-template-columns: repeat(2, 1fr); }
      .flashcards { grid-template-columns: 1fr; }
    }

    @media (max-width: 520px) {
      .dashboard { grid-template-columns: 1fr; }
      .question-top { flex-direction: column; align-items: flex-start; }
      .question-card { padding: 18px; }
      button { width: 100%; }
    }
  </style>
</head>
<body>
  <header>
    <h1>Examen Interactivo: Turbomáquinas e Hidroeléctricas</h1>
    <p>
      Practica con preguntas tipo examen sobre bombas, bombas centrífugas, centrales hidroeléctricas,
      golpe de ariete y componentes hidráulicos. Responde, revisa tu puntuación y aprende con retroalimentación inmediata.
    </p>
  </header>

  <main class="container">
    <section class="dashboard" aria-label="Panel de puntuación">
      <div class="stat"><span>Preguntas</span><strong id="totalQuestions">0</strong></div>
      <div class="stat"><span>Respondidas</span><strong id="answeredCount">0</strong></div>
      <div class="stat"><span>Puntaje</span><strong id="scoreCount">0</strong></div>
      <div class="stat"><span>Rendimiento</span><strong id="percentScore">0%</strong></div>
    </section>

    <div class="progress-wrap" aria-label="Barra de avance">
      <div class="progress-bar" id="progressBar"></div>
    </div>

    <section class="controls">
      <button onclick="checkExam()" class="success">Calificar examen</button>
      <button onclick="showAllFeedback()" class="warning">Mostrar explicaciones</button>
      <button onclick="resetExam()" class="danger">Reiniciar</button>
      <button onclick="shuffleQuestions()" class="secondary">Mezclar preguntas</button>
    </section>

    <section class="result-box" id="resultBox">
      <h2 id="resultTitle">Resultado</h2>
      <p id="resultText"></p>
      <p id="resultAdvice"></p>
    </section>

    <section class="mini-game">
      <h2>Mini repaso rápido</h2>
      <p>Haz clic en cada tarjeta para revelar la idea clave antes de resolver el examen.</p>
      <div class="flashcards">
        <div class="flashcard" onclick="this.classList.toggle('flipped')">
          <div class="flash-inner">
            <div class="flash-front">¿Qué hace una bomba?</div>
            <div class="flash-back">Entrega energía mecánica al fluido en forma de presión, velocidad o altura.</div>
          </div>
        </div>
        <div class="flashcard" onclick="this.classList.toggle('flipped')">
          <div class="flash-inner">
            <div class="flash-front">¿Qué hace una turbina?</div>
            <div class="flash-back">Recibe energía del fluido y la transforma en energía mecánica de rotación.</div>
          </div>
        </div>
        <div class="flashcard" onclick="this.classList.toggle('flipped')">
          <div class="flash-inner">
            <div class="flash-front">¿Qué es el golpe de ariete?</div>
            <div class="flash-back">Una variación brusca de presión causada por cambios rápidos en el flujo.</div>
          </div>
        </div>
      </div>
    </section>

    <section class="quiz" id="quiz"></section>

    <p class="footer-note">
      Recomendación: primero responde sin mirar las explicaciones; luego usa la retroalimentación para reforzar los puntos débiles.
    </p>
  </main>

  <script>
    const questions = [
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
        explanation: "Una bomba es un transformador de energía: recibe energía mecánica de un motor y la entrega al fluido, aumentando su presión, velocidad o posición."
      },
      {
        topic: "Bombas",
        level: "Básico",
        question: "En la comparación hidráulica del material, ¿cómo se interpreta una bomba y cómo una turbina?",
        options: [
          "La bomba es un motor hidráulico y la turbina es un generador hidráulico.",
          "Ambas solo aumentan la presión del fluido.",
          "La bomba es un generador hidráulico y la turbina es un motor hidráulico.",
          "La bomba y la turbina funcionan exactamente igual."
        ],
        answer: 2,
        explanation: "La bomba entrega energía al fluido, por eso se compara con un generador hidráulico. La turbina recibe energía del fluido y produce trabajo mecánico, por eso se compara con un motor hidráulico."
      },
      {
        topic: "Selección de bombas",
        level: "Intermedio",
        question: "¿Qué factores son esenciales para seleccionar correctamente el tipo de bomba?",
        options: [
          "Solo el color, el tamaño exterior y la marca.",
          "Presión, caudal y características del líquido como viscosidad, temperatura, pH y sólidos en suspensión.",
          "Únicamente el diámetro de la tubería de descarga.",
          "Solo la potencia del motor eléctrico."
        ],
        answer: 1,
        explanation: "La selección depende de la presión, el gasto o caudal y de las propiedades del líquido: viscosidad, temperatura, pH, densidad, abrasión e impurezas."
      },
      {
        topic: "Tipos de bombas",
        level: "Intermedio",
        question: "¿En qué caso suele ser más adecuada una bomba de desplazamiento positivo reciprocante?",
        options: [
          "Gastos pequeños, presiones altas y líquidos limpios.",
          "Gastos extremadamente grandes y presiones muy bajas.",
          "Líquidos muy sucios con grandes sólidos flotantes.",
          "Solo para centrales hidroeléctricas de gran altura."
        ],
        answer: 0,
        explanation: "Las bombas reciprocantes se aplican normalmente en caudales pequeños, presiones altas y líquidos limpios."
      },
      {
        topic: "Bombas centrífugas",
        level: "Intermedio",
        question: "¿Por qué las bombas centrífugas son muy utilizadas en la práctica?",
        options: [
          "Porque siempre eliminan la cavitación.",
          "Porque solo funcionan con líquidos muy viscosos.",
          "Porque tienen descarga relativamente constante, amplio rango de caudales y menos problemas de válvulas que las reciprocantes.",
          "Porque no necesitan impulsor ni eje."
        ],
        answer: 2,
        explanation: "Las bombas centrífugas destacan por su descarga constante, amplio rango de operación y menor complejidad frente a problemas típicos de válvulas en bombas reciprocantes."
      },
      {
        topic: "Partes de bomba",
        level: "Básico",
        question: "¿Qué componente de una bomba centrífuga transmite energía directamente al fluido mediante rotación?",
        options: [
          "Impulsor.",
          "Cimentación.",
          "Manómetro.",
          "Canal de descarga."
        ],
        answer: 0,
        explanation: "El impulsor gira y transfiere energía al líquido, aumentando su energía hidráulica."
      },
      {
        topic: "Materiales",
        level: "Intermedio",
        question: "¿Qué condición del servicio puede influir en la selección de materiales de una bomba?",
        options: [
          "Solo la forma de la sala de máquinas.",
          "Corrosión, abrasión, temperatura de bombeo, carga de operación y vida esperada.",
          "La cantidad de focos instalados en el ambiente.",
          "El tipo de pintura exterior, sin considerar el fluido."
        ],
        answer: 1,
        explanation: "El material debe seleccionarse considerando la corrosión, la acción electroquímica, la abrasión, la temperatura, la carga y la vida esperada del equipo."
      },
      {
        topic: "Hidroeléctricas",
        level: "Básico",
        question: "¿Qué es una central hidroeléctrica?",
        options: [
          "Una instalación que transforma energía solar directamente en presión hidráulica.",
          "Una instalación que aprovecha masas de agua en movimiento para generar electricidad mediante turbinas y alternadores.",
          "Un sistema que solo almacena agua sin producir energía.",
          "Una bomba que eleva agua hacia una montaña."
        ],
        answer: 1,
        explanation: "Una central hidroeléctrica aprovecha la energía del agua para mover turbinas acopladas a alternadores, generando energía eléctrica."
      },
      {
        topic: "Conversión de energía",
        level: "Básico",
        question: "¿Cuál es la secuencia energética general en una central hidroeléctrica?",
        options: [
          "Energía eléctrica → energía potencial → energía química.",
          "Energía potencial del agua → energía cinética → energía mecánica de rotación → energía eléctrica.",
          "Energía térmica → energía nuclear → energía hidráulica.",
          "Energía eléctrica → energía mecánica → energía potencial del agua."
        ],
        answer: 1,
        explanation: "El agua almacenada posee energía potencial; al conducirse adquiere energía cinética; en la turbina produce energía mecánica; y el alternador la transforma en electricidad."
      },
      {
        topic: "Potencia",
        level: "Intermedio",
        question: "¿Qué expresa la potencia efectiva en una central hidroeléctrica?",
        options: [
          "La capacidad real de energía que se puede entregar de forma continua.",
          "La capacidad ideal sin considerar condiciones reales.",
          "La energía acumulada en los sedimentos.",
          "La potencia que solo se entrega durante emergencias."
        ],
        answer: 0,
        explanation: "La potencia efectiva representa la capacidad real de entrega continua, a diferencia de la potencia instalada, que se asocia a condiciones ideales."
      },
      {
        topic: "Componentes",
        level: "Intermedio",
        question: "¿Cuál de los siguientes pertenece al conjunto de obras hidráulicas de una central hidroeléctrica?",
        options: [
          "Alternador y regulador de tensión.",
          "Excitación del generador.",
          "Presa, toma, desarenador, cámara de carga y tubería forzada.",
          "Transformador de distribución domiciliaria."
        ],
        answer: 2,
        explanation: "Las obras hidráulicas almacenan, captan, conducen y regulan el agua antes y después de la turbina."
      },
      {
        topic: "Presa",
        level: "Básico",
        question: "¿Cuál es la función principal de una presa en una central hidroeléctrica?",
        options: [
          "Disminuir siempre la altura disponible del agua.",
          "Elevar el nivel del agua, crear desnivel y permitir el control o derivación del caudal.",
          "Reemplazar completamente a la turbina.",
          "Evitar que el agua tenga energía potencial."
        ],
        answer: 1,
        explanation: "La presa eleva el nivel del agua, permite formar un embalse y facilita el aprovechamiento del desnivel para producir energía."
      },
      {
        topic: "Aliviadores",
        level: "Intermedio",
        question: "¿Para qué sirven los aliviadores en una central hidroeléctrica?",
        options: [
          "Para evacuar caudales excedentes y proteger el sistema durante crecidas.",
          "Para aumentar la arena que ingresa a la turbina.",
          "Para transformar electricidad en energía cinética.",
          "Para cerrar permanentemente la tubería forzada."
        ],
        answer: 0,
        explanation: "Los aliviadores evacuan caudales superiores a los deseados, especialmente durante crecidas, cumpliendo una función de protección y seguridad."
      },
      {
        topic: "Desarenador",
        level: "Intermedio",
        question: "¿Cuál es el objetivo principal de un desarenador?",
        options: [
          "Aumentar la velocidad del agua para arrastrar más sedimentos.",
          "Reducir la velocidad del agua para que arena y partículas se depositen antes de llegar a la turbina.",
          "Generar electricidad directamente sin turbina.",
          "Medir únicamente la temperatura del agua."
        ],
        answer: 1,
        explanation: "El desarenador permite sedimentar arena y partículas, reduciendo el desgaste por abrasión en la turbina."
      },
      {
        topic: "Cámara de carga",
        level: "Intermedio",
        question: "¿Qué función cumple la cámara de carga?",
        options: [
          "Amortiguar ondas de presión y proveer volumen de agua antes de la tubería forzada.",
          "Reemplazar al alternador.",
          "Eliminar la necesidad de compuertas.",
          "Servir únicamente como oficina de control."
        ],
        answer: 0,
        explanation: "La cámara de carga se ubica entre la conducción abierta y la tubería forzada; ayuda a regular el caudal y amortiguar variaciones de presión."
      },
      {
        topic: "Golpe de ariete",
        level: "Avanzado",
        question: "¿Qué describe mejor el golpe de ariete?",
        options: [
          "Una variación brusca de presión causada por cambios rápidos en la velocidad del agua dentro de una tubería.",
          "Un método para aumentar sedimentos en el canal.",
          "Una falla exclusiva de motores eléctricos, sin relación con tuberías.",
          "Un tipo de presa de concreto armado."
        ],
        answer: 0,
        explanation: "El golpe de ariete se produce por maniobras bruscas como cierres rápidos de válvulas, generando ondas de sobrepresión o depresión."
      },
      {
        topic: "Golpe de ariete",
        level: "Avanzado",
        question: "¿Cuál es una medida adecuada para atenuar el golpe de ariete?",
        options: [
          "Cerrar las válvulas lo más rápido posible.",
          "Accionar válvulas progresivamente e instalar chimeneas de equilibrio cuando corresponda.",
          "Eliminar todas las cámaras de carga.",
          "Aumentar sin control la velocidad del flujo."
        ],
        answer: 1,
        explanation: "El cierre gradual reduce cambios bruscos de velocidad. Las chimeneas de equilibrio ayudan a absorber variaciones de presión."
      },
      {
        topic: "Chimenea de equilibrio",
        level: "Avanzado",
        question: "¿Cómo actúa una chimenea de equilibrio ante una sobrepresión?",
        options: [
          "Permite que el nivel de agua suba, transformando parte de la energía cinética en energía potencial.",
          "Bloquea totalmente el paso del agua sin variación de nivel.",
          "Aumenta intencionalmente la presión hasta romper la tubería.",
          "Convierte directamente presión en energía eléctrica."
        ],
        answer: 0,
        explanation: "Ante sobrepresión, el agua asciende en la chimenea. Así se amortigua el golpe de ariete y se reducen variaciones bruscas de presión."
      },
      {
        topic: "Tipos de centrales",
        level: "Intermedio",
        question: "¿Qué caracteriza a una central de pasada o agua fluente?",
        options: [
          "Utiliza el agua mientras fluye por el río y su producción depende del caudal disponible.",
          "Siempre tiene gran embalse anual y caudal totalmente constante.",
          "No requiere toma, canal ni turbina.",
          "Solo funciona con vapor de agua."
        ],
        answer: 0,
        explanation: "Las centrales de pasada aprovechan el caudal natural; en avenidas producen más y en estiaje disminuye su potencia."
      },
      {
        topic: "Tipos de centrales",
        level: "Intermedio",
        question: "¿Qué ventaja ambiental se atribuye a las centrales de derivación o filo de agua?",
        options: [
          "Al no bloquear completamente el cauce, pueden tener menor impacto por inundación de terrenos adyacentes.",
          "Siempre eliminan todo impacto ambiental.",
          "No utilizan agua del río.",
          "Funcionan sin obras de captación."
        ],
        answer: 0,
        explanation: "Estas centrales captan parte del caudal y lo devuelven al río; por eso, comparadas con grandes embalses, pueden reducir inundaciones de áreas adyacentes."
      }
    ];

    let currentQuestions = [...questions];
    const quiz = document.getElementById("quiz");

    function renderQuiz() {
      quiz.innerHTML = "";
      document.getElementById("totalQuestions").textContent = currentQuestions.length;

      currentQuestions.forEach((q, index) => {
        const card = document.createElement("article");
        card.className = "question-card";
        card.dataset.index = index;

        const optionsHTML = q.options.map((opt, optIndex) => `
          <label class="option" data-option="${optIndex}">
            <input type="radio" name="q${index}" value="${optIndex}" onchange="updateStats()" />
            <span><strong>${String.fromCharCode(65 + optIndex)}.</strong> ${opt}</span>
          </label>
        `).join("");

        card.innerHTML = `
          <div class="question-top">
            <span class="badge">Pregunta ${index + 1} · ${q.topic}</span>
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

    function checkExam() {
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
      document.getElementById("scoreCount").textContent = score;
      document.getElementById("percentScore").textContent = `${percent}%`;
      document.getElementById("answeredCount").textContent = answered;
      document.getElementById("progressBar").style.width = `${(answered / currentQuestions.length) * 100}%`;

      const resultBox = document.getElementById("resultBox");
      const title = document.getElementById("resultTitle");
      const text = document.getElementById("resultText");
      const advice = document.getElementById("resultAdvice");

      resultBox.style.display = "block";
      title.textContent = `Obtuviste ${score} de ${currentQuestions.length} puntos (${percent}%)`;

      if (percent >= 90) {
        text.textContent = "Excelente dominio. Estás listo para responder preguntas conceptuales y aplicadas.";
        advice.textContent = "Reto final: explica con tus propias palabras la diferencia entre bomba, turbina, cámara de carga y chimenea de equilibrio.";
      } else if (percent >= 70) {
        text.textContent = "Buen resultado. Comprendes la mayoría de conceptos importantes.";
        advice.textContent = "Refuerza especialmente las preguntas donde confundiste componentes hidráulicos y tipos de centrales.";
      } else if (percent >= 50) {
        text.textContent = "Vas en camino, pero aún necesitas repasar conceptos clave.";
        advice.textContent = "Revisa bombas centrífugas, golpe de ariete, desarenadores, cámaras de carga y clasificación de centrales.";
      } else {
        text.textContent = "Necesitas reforzar la base antes del examen.";
        advice.textContent = "Empieza por la secuencia de energía en una hidroeléctrica y la diferencia entre bomba y turbina.";
      }

      resultBox.scrollIntoView({ behavior: "smooth", block: "center" });
    }

    function showAllFeedback() {
      currentQuestions.forEach((_, index) => {
        document.getElementById(`feedback-${index}`).style.display = "block";
      });
    }

    function resetExam() {
      document.querySelectorAll("input[type='radio']").forEach(input => input.checked = false);
      document.querySelectorAll(".option").forEach(label => label.classList.remove("correct", "incorrect"));
      document.querySelectorAll(".feedback").forEach(f => f.style.display = "none");
      document.getElementById("scoreCount").textContent = "0";
      document.getElementById("percentScore").textContent = "0%";
      document.getElementById("answeredCount").textContent = "0";
      document.getElementById("progressBar").style.width = "0%";
      document.getElementById("resultBox").style.display = "none";
      window.scrollTo({ top: 0, behavior: "smooth" });
    }

    function shuffleQuestions() {
      currentQuestions = currentQuestions
        .map(value => ({ value, sort: Math.random() }))
        .sort((a, b) => a.sort - b.sort)
        .map(({ value }) => value);
      document.getElementById("resultBox").style.display = "none";
      document.getElementById("scoreCount").textContent = "0";
      document.getElementById("percentScore").textContent = "0%";
      renderQuiz();
      window.scrollTo({ top: 0, behavior: "smooth" });
    }

    renderQuiz();
  </script>
</body>
</html>
