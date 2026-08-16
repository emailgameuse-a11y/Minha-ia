# Minha-ia
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Minha IA</title>

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: Arial, sans-serif;
    }

    body {
      background: #0f0f14;
      color: white;
      height: 100vh;
      display: flex;
      flex-direction: column;
    }

    header {
      height: 65px;
      background: #17171f;
      border-bottom: 1px solid #292934;
      display: flex;
      align-items: center;
      padding: 0 20px;
      font-size: 20px;
      font-weight: bold;
    }

    .logo {
      width: 38px;
      height: 38px;
      border-radius: 50%;
      background: linear-gradient(135deg, #6c5ce7, #00cec9);
      display: flex;
      align-items: center;
      justify-content: center;
      margin-right: 12px;
      font-size: 20px;
    }

    #chat {
      flex: 1;
      overflow-y: auto;
      padding: 25px;
      display: flex;
      flex-direction: column;
      gap: 15px;
    }

    .message {
      max-width: 80%;
      padding: 13px 17px;
      border-radius: 15px;
      line-height: 1.5;
      white-space: pre-wrap;
    }

    .user {
      align-self: flex-end;
      background: #5f4de4;
      border-bottom-right-radius: 4px;
    }

    .bot {
      align-self: flex-start;
      background: #20202a;
      border-bottom-left-radius: 4px;
    }

    .typing {
      color: #aaa;
      font-style: italic;
    }

    .input-area {
      padding: 15px;
      background: #17171f;
      border-top: 1px solid #292934;
      display: flex;
      gap: 10px;
    }

    #input {
      flex: 1;
      background: #24242e;
      color: white;
      border: none;
      outline: none;
      padding: 14px;
      border-radius: 12px;
      font-size: 16px;
    }

    button {
      border: none;
      background: #6c5ce7;
      color: white;
      padding: 0 20px;
      border-radius: 12px;
      cursor: pointer;
      font-size: 16px;
    }

    button:hover {
      background: #5948d4;
    }

    @media (max-width: 600px) {
      #chat {
        padding: 15px;
      }

      .message {
        max-width: 90%;
      }

      button {
        padding: 0 15px;
      }
    }
  </style>
</head>

<body>

<header>
  <div class="logo">🤖</div>
  Minha IA
</header>

<div id="chat">
  <div class="message bot">
    Olá! 👋 Eu sou a Minha IA. Como posso ajudar?
  </div>
</div>

<div class="input-area">
  <input
    id="input"
    type="text"
    placeholder="Digite sua mensagem..."
    autocomplete="off"
  >

  <button onclick="sendMessage()">Enviar</button>
</div>

<script>
  const input = document.getElementById("input");
  const chat = document.getElementById("chat");

  input.addEventListener("keydown", function(event) {
    if (event.key === "Enter") {
      sendMessage();
    }
  });

  function addMessage(text, type) {
    const message = document.createElement("div");

    message.className = "message " + type;
    message.textContent = text;

    chat.appendChild(message);
    chat.scrollTop = chat.scrollHeight;

    return message;
  }

  function sendMessage() {
    const text = input.value.trim();

    if (!text) return;

    addMessage(text, "user");
    input.value = "";

    const typing = addMessage("Digitando...", "bot typing");

    setTimeout(() => {
      typing.remove();

      const response = generateResponse(text);

      addMessage(response, "bot");
    }, 700);
  }

  function generateResponse(text) {
    const msg = text.toLowerCase();

    if (msg.includes("oi") ||
        msg.includes("olá") ||
        msg.includes("ola")) {
      return "Olá! 😄 É um prazer falar com você!";
    }

    if (msg.includes("seu nome")) {
      return "Meu nome é Minha IA 🤖";
    }

    if (msg.includes("quem é você") ||
        msg.includes("quem e voce")) {
      return "Eu sou uma IA criada em HTML, CSS e JavaScript!";
    }

    if (msg.includes("como você está") ||
        msg.includes("como voce esta")) {
      return "Estou funcionando perfeitamente! 🚀";
    }

    if (msg.includes("obrigado") ||
        msg.includes("obrigada")) {
      return "De nada! 😄";
    }

    if (msg.includes("tchau")) {
      return "Até mais! 👋";
    }

    if (msg.includes("hora")) {
      return "Agora são " +
        new Date().toLocaleTimeString("pt-BR");
    }

    if (msg.includes("data")) {
      return "Hoje é " +
        new Date().toLocaleDateString("pt-BR");
    }

    return "Ainda estou aprendendo 🧠. Essa versão funciona com respostas programadas. Podemos conectar uma API de IA para eu conseguir responder perguntas de verdade!";
  }
</script>

</body>
</html>
