<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Quiz Feitec</title>
  <link rel="shortcut icon" href="comp.ico" type="image/x-icon" >
  <style>
    body {
      background-color: #cce7ff; /* Azul claro */
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 20px;
    }

    .container {
      max-width: 650px;
      background-color: #e6f2ff; /* Azul bem claro */
      padding: 30px;
      margin: auto;
      border-radius: 15px;
      box-shadow: 0 0 15px rgba(0, 51, 102, 0.25); /* sombra azul escura */
      position: relative;
    }

    h1 {
      text-align: center;
      color: #003366; /* Azul escuro */
      font-size: 28px;
      margin-bottom: 25px;
    }

    .pergunta, .resultadoBox {
      margin-bottom: 25px;
      padding: 15px;
      border: 1px dashed #003366; /* Azul escuro */
      border-radius: 10px;
      background: #cce7ff; /* Azul claro para blocos */
    }

    .pergunta p, .resultadoBox p {
      font-weight: bold;
      margin-bottom: 10px;
      color: #003366; /* Azul escuro */
    }

    label {
      display: block;
      margin: 5px 0;
      color: #003366; /* Azul escuro */
    }

    button {
      background-color: #336699; /* Azul médio */
      color: white;
      border: none;
      padding: 12px 24px;
      border-radius: 8px;
      cursor: pointer;
      font-size: 16px;
      margin: 15px auto;
      display: block;
      box-shadow: 0 4px 8px rgba(0, 51, 102, 0.2);
      transition: transform 0.2s;
    }

    button:hover {
      transform: scale(1.05);
    }

    /* Resultados */
    .correto {
      color: #336699; /* Azul médio */
    }

    .errado {
      color: #68abeee0; /* Azul claro */
    }

    .final {
      color: #003366; /* Azul escuro */
      font-size: 20px;
      text-align: center;
    }

    /* Esconde a tela de resultado até ser usada */
    #resultadoTela {
      display: none;
    }
  </style>
</head>
<body>

  <!-- Tela do Quiz -->
  <div class="container" id="quizTela">
    <h1>✩‧₊˚ QUIZ FEITEC ˚₊‧✩</h1>

    <form id="quizForm">
      <!-- Pergunta 1 -->
      <div class="pergunta">
        <p>1. O que significa a sigla HTML?</p>
        <label><input type="radio" name="q1" value="a"> a) Hyper Trainer Marking Language</label>
        <label><input type="radio" name="q1" value="b"> b) Hyper Text Markup Language</label>
        <label><input type="radio" name="q1" value="c"> c) Home Tool Markup Language</label>
        <label><input type="radio" name="q1" value="d"> d) Nenhuma das anteriores</label>
      </div>

      <!-- Pergunta 2 -->
      <div class="pergunta">
        <p>2. No que podemos usar o CSS?</p>
        <label><input type="radio" name="q2" value="a"> a) Para estilizar páginas HTML</label>
        <label><input type="radio" name="q2" value="b"> b) Para gerenciar bancos de dados</label>
        <label><input type="radio" name="q2" value="c"> c) Para criar servidores</label>
        <label><input type="radio" name="q2" value="d"> d) Para compilar código C</label>
      </div>

      <!-- Pergunta 3 -->
      <div class="pergunta">
        <p>3. O que faz o JavaScript?</p>
        <label><input type="radio" name="q3" value="a"> a) Linguagem de marcação</label>
        <label><input type="radio" name="q3" value="b"> b) Folha de estilo</label>
        <label><input type="radio" name="q3" value="c"> c) Linguagem de programação para web</label>
        <label><input type="radio" name="q3" value="d"> d) Banco de dados</label>
      </div>

       <div class="pergunta">
        <p>4.O que é robótica?</p>
        <label><input type="radio" name="q4" value="a"> a) Estudo dos seres vivos. </label>
        <label><input type="radio" name="q4" value="b"> b) Cultivo com IA. </label>
        <label><input type="radio" name="q4" value="c"> c) Medicina cardíaca. </label>
        <label><input type="radio" name="q4" value="d"> d) Estudo e criação de robôs. </label>
      </div>

      <div class="pergunta">
        <p>5.Como funciona a Garra Robótica?</p>
        <label><input type="radio" name="q5" value="a"> a) Usa motores, sensores e programação. </label>
        <label><input type="radio" name="q5" value="b"> b) Precisa estar sempre conectada ao PC. </label>
        <label><input type="radio" name="q5" value="c"> c) Funciona com sensores de luz. </label>
        <label><input type="radio" name="q5" value="d"> d) Usa mágica e ímãs. </label>
      </div>

      <button type="button" onclick="verificarRespostas()">Enviar</button>
    </form>
  </div>

  <!-- Tela de Resultados -->
  <div class="container" id="resultadoTela">
    <h1>Resultado do Quiz</h1>
    <div id="resultado"></div>
    <p style="text-align:center; font-weight:bold; color:#003366;">
      Obrigada pela participação :)
    </p>
    <button onclick="resetQuiz()">Resetar</button>
  </div>

  <script>
    function verificarRespostas() {
      const respostasCertas = { q1: "b", q2: "a", q3: "c", q4: "d", q5: "a" };
      const respostasUsuario = {
        q1: document.querySelector('input[name="q1"]:checked')?.value || "",
        q2: document.querySelector('input[name="q2"]:checked')?.value || "",
        q3: document.querySelector('input[name="q3"]:checked')?.value || "",
        q4: document.querySelector('input[name="q4"]:checked')?.value || "",
        q5: document.querySelector('input[name="q5"]:checked')?.value || ""
      };

      let resultadoHTML = "";
      let pontos = 0;

      for (let i = 1; i <= 5; i++) {
        const resp = respostasUsuario[`q${i}`];
        if (!resp) {
          resultadoHTML += `<div class="resultadoBox errado">Questão ${i}: Não respondida</div>`;
        } else if (resp === respostasCertas[`q${i}`]) {
          resultadoHTML += `<div class="resultadoBox correto">Questão ${i}: Você marcou "${resp}" → Correto!</div>`;
          pontos++;
        } else {
          resultadoHTML += `<div class="resultadoBox errado">Questão ${i}: Você marcou "${resp}" → Errado!</div>`;
        }
      }

      resultadoHTML += `<p class="final">Você acertou ${pontos} de 5 questões</p>`;

      document.getElementById("quizTela").style.display = "none";
      document.getElementById("resultadoTela").style.display = "block";
      document.getElementById("resultado").innerHTML = resultadoHTML;
    }

    function resetQuiz() {
      document.getElementById("quizForm").reset();
      document.getElementById("resultado").innerHTML = "";
      document.getElementById("quizTela").style.display = "block";
      document.getElementById("resultadoTela").style.display = "none";
    }
  </script>

</body>
</html>
