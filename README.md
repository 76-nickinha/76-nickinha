<!DOCTYPE html><html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>studLED - Plataforma de Reforço Escolar</title>
  <style>
    * { box-sizing: border-box; }
    body { font-family: Arial, sans-serif; margin: 0; background-color: #f0f2f5; }
    header { background-color: #004aad; color: white; padding: 20px; text-align: center; }
    nav a { margin: 0 10px; color: white; text-decoration: none; font-weight: bold; }
    section { padding: 20px; }
    .hidden { display: none; }
    .button { padding: 10px 20px; background-color: #004aad; color: white; border: none; border-radius: 5px; cursor: pointer; text-decoration: none; }
    .course-card { background: white; border-radius: 10px; padding: 20px; margin: 10px 0; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
    input, textarea, select { width: 100%; padding: 10px; margin: 10px 0; border-radius: 5px; border: 1px solid #ccc; }
    footer { background: #004aad; color: white; text-align: center; padding: 20px; }
    .auth-request { background: #fff3cd; border: 1px solid #ffeeba; padding: 10px; margin: 10px 0; border-radius: 5px; }
    .score-box { background-color: #d1fae5; border: 1px solid #10b981; padding: 10px; margin-top: 10px; border-radius: 5px; color: #065f46; }
    .challenge { background-color: #e0f7fa; padding: 10px; border: 1px solid #00acc1; border-radius: 5px; margin-top: 10px; }
    .mural { background: #fff; padding: 20px; border-radius: 10px; margin-top: 30px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); }
    .mural-message { border-bottom: 1px solid #ccc; padding: 5px 0; }
  </style>
</head>
<body>
  <header>
    <h1>studLED</h1>
    <p>Reforço Escolar Online para o Ensino Fundamental</p>
    <nav>
      <a href="#cursos">Cursos</a>
      <a href="#mural">Mural</a>
      <a href="#login">Entrar</a>
    </nav>
  </header>  <section id="login">
    <h2>Login do Aluno</h2>
    <input type="text" id="aluno-nome" placeholder="Nome do Aluno">
    <input type="password" id="senha" placeholder="Senha">
    <button class="button" onclick="loginAluno()">Entrar</button>
    <div id="mensagem-autorizacao" class="auth-request hidden"></div>
  </section>  <section id="cursos" class="hidden">
    <h2>Cursos Disponíveis</h2>
    <div class="course-card">
      <h3>Matemática</h3>
      <a class="button" href="https://pt.khanacademy.org/math" target="_blank">Aprofundar no Khan Academy</a>
      <div class="score-box" id="score-mat">Pontuação: <span id="mat-certos">0</span>/10</div>
      <div>
        <p><strong>Quanto é 3 + 4?</strong></p>
        <input type="text" id="resposta-mat">
        <button class="button" onclick="verificarResposta('mat', '7')">Responder</button>
      </div>
      <div class="challenge">
        <p><strong>Desafio:</strong> Resolva: (5 + 3) x 2</p>
      </div>
    </div><div class="course-card">
  <h3>Português</h3>
  <a class="button" href="https://pt.khanacademy.org/humanities/grammar" target="_blank">Aprofundar no Khan Academy</a>
  <div class="score-box" id="score-port">Pontuação: <span id="port-certos">0</span>/10</div>
  <div>
    <p><strong>Qual é o plural de "casa"?</strong></p>
    <input type="text" id="resposta-port">
    <button class="button" onclick="verificarResposta('port', 'casas')">Responder</button>
  </div>
  <div class="challenge">
    <p><strong>Desafio:</strong> Crie uma frase com a palavra "amizade".</p>
  </div>
</div>

  </section>  <section id="mural" class="hidden">
    <h2>Mural de Mensagens</h2>
    <div class="mural">
      <textarea id="mensagemAluno" placeholder="Escreva sua mensagem aqui..."></textarea>
      <button class="button" onclick="enviarMensagem()">Enviar</button>
      <div id="mensagens"></div>
    </div>
  </section>  <footer>
    <p>studLED &copy; 2025 - Desenvolvido para reforço escolar com carinho.</p>
  </footer>  <script>
    const senhaCorreta = "studLED123";
    const alunosPendentes = [];

    function loginAluno() {
      const nome = document.getElementById("aluno-nome").value;
      const senha = document.getElementById("senha").value;
      const msg = document.getElementById("mensagem-autorizacao");

      if (senha === senhaCorreta) {
        alunosPendentes.push(nome);
        msg.classList.remove("hidden");
        msg.textContent = `Aluno ${nome} solicitou acesso. Aguarde autorização.`;

        setTimeout(() => {
          msg.classList.add("hidden");
          document.getElementById("login").classList.add("hidden");
          document.getElementById("cursos").classList.remove("hidden");
          document.getElementById("mural").classList.remove("hidden");
        }, 2000);
      } else {
        alert("Senha incorreta.");
      }
    }

    const pontuacoes = {
      mat: { certos: 0 },
      port: { certos: 0 }
    };

    function verificarResposta(curso, respostaCorreta) {
      const input = document.getElementById(`resposta-${curso}`);
      const resposta = input.value.trim().toLowerCase();
      if (pontuacoes[curso].certos < 10) {
        if (resposta === respostaCorreta.toLowerCase()) pontuacoes[curso].certos++;
        document.getElementById(`${curso}-certos`).textContent = pontuacoes[curso].certos;
        input.value = "";
      } else {
        alert("Você já completou os 10 acertos desse curso!");
      }
    }

    function enviarMensagem() {
      const mensagem = document.getElementById("mensagemAluno").value;
      if (mensagem.trim()) {
        const mensagensDiv = document.getElementById("mensagens");
        const novaMensagem = document.createElement("div");
        novaMensagem.className = "mural-message";
        novaMensagem.textContent = mensagem;
        mensagensDiv.prepend(novaMensagem);
        document.getElementById("mensagemAluno").value = "";
      }
    }
  </script></body>
</html>
