# Quiz-do-Dia-do-Trabalho<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Quiz - Dia do Trabalhador</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
    }
    .container {
      background: #fff;
      padding: 30px;
      border-radius: 12px;
      box-shadow: 0 0 12px rgba(0,0,0,0.2);
      max-width: 600px;
      width: 90%;
      text-align: center;
    }
    input[type="text"] {
      padding: 10px;
      width: 80%;
      border: 1px solid #ccc;
      border-radius: 5px;
      margin-bottom: 20px;
    }
    button {
      padding: 10px 20px;
      background-color: #007BFF;
      border: none;
      color: white;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background-color: #0056b3;
    }
    .hidden {
      display: none;
    }
    .question {
      text-align: left;
      margin-top: 20px;
    }
    .option {
      margin: 10px 0;
      text-align: left;
    }
    #timer {
      font-weight: bold;
      margin-top: 10px;
      color: red;
    }
  </style>
</head>
<body>
  <div class="container">
    <div id="ra-section">
      <h2>Quiz do Dia do Trabalhador</h2>
      <p>Digite seu RA para responder:</p>
      <input type="text" id="raInput" placeholder="Ex: 123456">
      <button onclick="verificarRA()">Começar</button>
    </div>

    <div id="quiz-section" class="hidden">
      <div id="question-container"></div>
      <p id="timer"></p>
    </div>
  </div>

  <script>
    const perguntas = [
      {
        pergunta: "Em que data é comemorado o Dia do Trabalhador no Brasil?",
        opcoes: ["7 de setembro", "1º de maio", "15 de novembro", "4 de outubro"],
        correta: 1
      },
      {
        pergunta: "Qual foi a principal reivindicação da greve de Chicago em 1886?",
        opcoes: ["Fim do trabalho aos domingos", "Aumento do salário mínimo", "Redução da jornada para 8 horas", "Criação de férias remuneradas"],
        correta: 2
      },
      {
        pergunta: "Em que país aconteceu a greve que deu origem ao Dia do Trabalhador?",
        opcoes: ["França", "Estados Unidos", "Inglaterra", "Brasil"],
        correta: 1
      },
      {
        pergunta: "Qual cidade foi o palco central da greve de 1886?",
        opcoes: ["Nova York", "Chicago", "Boston", "Washington"],
        correta: 1
      },
      {
        pergunta: "Em que ano o Brasil transformou o 1º de maio em feriado oficialmente por decreto?",
        opcoes: ["1924", "1930", "1988", "2002"],
        correta: 0
      },
      {
        pergunta: "Qual presidente brasileiro oficializou o feriado do Dia do Trabalhador?",
        opcoes: ["Getúlio Vargas", "Artur Bernardes", "Juscelino Kubitschek", "João Goulart"],
        correta: 1
      },
      {
        pergunta: "Qual desses direitos NÃO fazia parte das reivindicações iniciais do movimento operário?",
        opcoes: ["Jornada de 8 horas", "Condições dignas de trabalho", "Direito à aposentadoria", "Valorização dos salários"],
        correta: 2
      },
      {
        pergunta: "Em que ano o 1º de maio foi oficialmente incluído como feriado nacional por lei no Brasil?",
        opcoes: ["1988", "1943", "2002", "1977"],
        correta: 2
      },
      {
        pergunta: "Qual é o principal motivo da comemoração do Dia do Trabalhador em 1º de maio?",
        opcoes: ["É o dia em que foi assinada a Lei Áurea", "Marca o início da Revolução Industrial", "Homenageia uma greve histórica por melhores condições de trabalho", "Comemora a fundação da ONU"],
        correta: 2
      },
      {
        pergunta: "Qual país reduziu pela primeira vez a jornada de trabalho para 8 horas após a greve de 1886?",
        opcoes: ["Brasil", "Estados Unidos", "França", "Inglaterra"],
        correta: 2
      },
      {
        pergunta: "Qual era a jornada comum de trabalho antes das reivindicações em Chicago?",
        opcoes: ["6 horas", "8 horas", "12 horas", "10 horas"],
        correta: 2
      },
      {
        pergunta: "O Dia do Trabalho começou a ser comemorado, de forma não oficial, pelos trabalhadores no Brasil na década de:",
        opcoes: ["1890", "1900", "1910", "1920"],
        correta: 2
      },
      {
        pergunta: "Em que ano a jornada de 8 horas começou a ser oficialmente adotada em países como a França?",
        opcoes: ["1886", "1919", "1924", "1945"],
        correta: 1
      },
      {
        pergunta: "Qual destes é um objetivo atual do Dia do Trabalho?",
        opcoes: ["Celebrar conquistas de empresas", "Reduzir a carga tributária", "Reforçar a valorização do trabalhador", "Incentivar o comércio internacional"],
        correta: 2
      },
      {
        pergunta: "Qual das práticas abaixo pode ser considerada uma forma de trabalho escravo contemporâneo?",
        opcoes: ["Pagamento de salário abaixo do mínimo legal", "Jornada de trabalho de 8 horas sem registro em carteira", "Trabalho temporário sem contrato assinado", "Atraso eventual no pagamento de salário"],
        correta: 0
      }
    ];

    function verificarRA() {
      const ra = document.getElementById("raInput").value.trim();
      if (!ra) {
        alert("Por favor, digite seu RA.");
        return;
      }

      if (localStorage.getItem("quiz_ra_" + ra)) {
        alert("Você já respondeu o quiz.");
        return;
      }

      iniciarQuiz(ra);
    }

    function iniciarQuiz(ra) {
      document.getElementById("ra-section").classList.add("hidden");
      document.getElementById("quiz-section").classList.remove("hidden");

      const pergunta = perguntas[Math.floor(Math.random() * perguntas.length)];
      const container = document.getElementById("question-container");
      let html = `<div class='question'><strong>${pergunta.pergunta}</strong></div>`;

      pergunta.opcoes.forEach((opcao, index) => {
        html += `<div class='option'><label><input type='radio' name='resposta' value='${index}'> ${opcao}</label></div>`;
      });

      html += `<button onclick='enviarResposta(${pergunta.correta}, "${ra}")'>Responder</button>`;
      container.innerHTML = html;
      iniciarTimer();
    }

    let tempo = 30;
    let cronometro;

    function iniciarTimer() {
      const timer = document.getElementById("timer");
      timer.innerText = `Tempo restante: ${tempo}s`;

      cronometro = setInterval(() => {
        tempo--;
        timer.innerText = `Tempo restante: ${tempo}s`;
        if (tempo <= 0) {
          clearInterval(cronometro);
          timer.innerText = "Tempo esgotado!";
          document.querySelectorAll('input[name="resposta"]').forEach(input => input.disabled = true);
        }
      }, 1000);
    }

    function enviarResposta(correta, ra) {
      clearInterval(cronometro);
      const selecionada = document.querySelector('input[name="resposta"]:checked');
      if (!selecionada) {
        alert("Você precisa selecionar uma resposta antes de enviar.");
        return;
      }

      const valor = parseInt(selecionada.value);
      const msg = valor === correta ? "✅ Resposta correta!" : "❌ Resposta incorreta.";
      document.getElementById("question-container").innerHTML += `<p><strong>${msg}</strong></p>`;
      localStorage.setItem("quiz_ra_" + ra, true);
    }
  </script>
</body>
</html>
