# ==========================================================
# FREITAS LOURENÇO - MOTOR DE IA PARA CAPTIVE PORTAL & WI-FI
# Desenvolvido para automação comercial avançada
# ==========================================================

from flask import Flask, request, jsonify, render_template_string
import datetime

app = Flask(__name__)

# Base de conhecimento comercial da Freitas Lourenço para a IA
BASE_CONHECIMENTO = {
    "promocao": "Olá! Seja bem-vindo à nossa rede Wi-Fi. Hoje temos ofertas especiais em organizadores e produtos de utilidade para o seu negócio!",
    "cadastro": "Para continuar navegando com alta velocidade, aproveite para conhecer nosso sistema de PDV e Controle de Estoque.",
    "horario": "Nosso estabelecimento funciona de segunda a sábado das 08:00 às 18:00.",
    "suporte": "Precisa de ajuda com o sistema Freitas Lourenço ou com o sinal de rede? Fale com nosso atendimento no balcão."
}

# Template HTML/CSS moderno embutido para rodar direto na nuvem
TEMPLATE_CHAT = """
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FREITAS LOURENÇO - Conexão Inteligente</title>
    <style>
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: #0f172a; color: #f8fafc; margin: 0; padding: 20px; display: flex; justify-content: center; align-items: center; height: 100vh; }
        .chat-container { width: 100%; max-width: 450px; background: #1e293b; border-radius: 12px; box-shadow: 0 10px 25px rgba(0,0,0,0.5); display: flex; flex-direction: column; overflow: hidden; border: 1px solid #334155; }
        .chat-header { background: #2563eb; color: white; padding: 15px; text-align: center; font-weight: bold; font-size: 1.1rem; }
        .chat-messages { padding: 15px; height: 320px; overflow-y: auto; display: flex; flex-direction: column; gap: 10px; }
        .message { padding: 10px 14px; border-radius: 8px; max-width: 80%; font-size: 0.95rem; line-height: 1.4; }
        .message.bot { background: #334155; align-self: flex-start; color: #e2e8f0; }
        .message.user { background: #2563eb; align-self: flex-end; color: white; }
        .chat-input-area { display: flex; padding: 10px; background: #0f172a; border-top: 1px solid #334155; }
        .chat-input-area input { flex: 1; padding: 10px; border: 1px solid #334155; border-radius: 6px; background: #1e293b; color: white; outline: none; }
        .chat-input-area button { background: #2563eb; color: white; border: none; padding: 10px 16px; margin-left: 8px; border-radius: 6px; cursor: pointer; font-weight: bold; }
        .chat-input-area button:hover { background: #1d4ed8; }
    </style>
</head>
<body>
    <div class="chat-container">
        <div class="chat-header">FREITAS LOURENÇO &bull; Wi-Fi Inteligente</div>
        <div class="chat-messages" id="chatMessages">
            <div class="message bot">Olá! Seja bem-vindo. Estou conectado à rede da Freitas Lourenço. Digite 'promoção', 'horario' ou 'suporte' para conversarmos!</div>
        </div>
        <div class="chat-input-area">
            <input type="text" id="userInput" placeholder="Digite sua mensagem..." onkeypress="handleKeyPress(event)">
            <button onclick="enviarMensagem()">Enviar</button>
        </div>
    </div>

    <script>
        async function enviarMensagem() {
            const input = document.getElementById('userInput');
            const mensagemTexto = input.value.trim();
            if (!mensagemTexto) return;

            const chatMessages = document.getElementById('chatMessages');
            chatMessages.innerHTML += `<div class="message user">${mensagemTexto}</div>`;
            input.value = '';
            chatMessages.scrollTop = chatMessages.scrollHeight;

            try {
                const response = await fetch('/api/chat', {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ mensagem: mensagemTexto })
                });
                const data = await response.json();
                chatMessages.innerHTML += `<div class="message bot">${data.resposta}</div>`;
                chatMessages.scrollTop = chatMessages.scrollHeight;
            } catch (error) {
                chatMessages.innerHTML += `<div class="message bot">Erro de conexão com o servidor da IA.</div>`;
            }
        }
        function handleKeyPress(event) {
            if (event.key === 'Enter') enviarMensagem();
        }
    </script>
</body>
</html>
"""

@app.route("/")
def home():
    return render_template_string(TEMPLATE_CHAT)

@app.route("/api/chat", methods=["POST"])
def chat_api():
    dados = request.get_json()
    mensagem_usuario = dados.get("mensagem", "").lower()
    
    # Processamento inteligente da IA baseada em regras de negócio comerciais
    resposta = "Desculpe, não entendi bem. Tente digitar 'promoção', 'cadastro' ou 'suporte' para ver como posso ajudar."
    
    for chave, texto in BASE_CONHECIMENTO.items():
        if chave in mensagem_usuario:
            resposta = texto
            break
            
    # Adiciona registro de auditoria temporal automatizada
    hora_atual = datetime.datetime.now().strftime("%H:%M")
    
    return jsonify({"resposta": f"{resposta} [Registrado às {hora_atual} - Freitas Lourenço AI]"})

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000, debug=True)
