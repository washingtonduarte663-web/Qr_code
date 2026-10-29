import os
from openai import OpenAI

# --- 1. CONFIGURAÇÃO SEGURA DA CHAVE ---
# Nunca cole sua chave direto no código. Coloque no terminal:
# No PC: setx OPENAI_API_KEY "sua-chave-aqui"
# No vscode.dev / Linux: export OPENAI_API_KEY="sua-chave-aqui"
# Ou crie um arquivo .env com: OPENAI_API_KEY=sua-chave-aqui

# Pega a chave do sistema
#api_key = os.getenv("OPENAI_API_KEY")

#if not api_key:
 #   print("ERRO: Chave não encontrada!")
#    print("Crie uma chave em: https://platform.openai.com/api-keys")
 #   print("Depois rode: export OPENAI_API_KEY='sua-chave'")
  #  exit()
#
# --- 2. CONECTANDO NA IA ---
# Para usar Gemini (do Google - é grátis):
# client = OpenAI(
#     api_key=os.getenv("GEMINI_API_KEY"),
#     base_url="https://generativelanguage.googleapis.com/v1beta/openai/"
# )
# modelo = "gemini-2.0-flash"

# Para usar Groq (muito rápido eapi_key=os.getenv("GROQ_API_KEY"),base_url="https://api.groq.com/openai/v1")
 modelo = "llama-3.3-70b-versatile"

# Para usar OpenAI / ChatGPT (padrão):
#client = OpenAI(api_key=api_key)
#modelo = "gpt-4o-mini" # modelo mais barato e bom

# --- 3. SUA IA PERSONALIZÁVEL ---
def perguntar_para_ia(pergunta, historico=[]):
    mensagens = [
        {"role": "system", "content": "Você é uma IA assistente útil, criada em Python. Responda em português brasileiro."}
    ]
    mensagens.extend(historico)
    mensagens.append({"role": "user", "content": pergunta})

    resposta = client.chat.completions.create(
        model=modelo,
        messages=mensagens,
        temperature=0.7
    )
    return resposta.choices[0].message.content

# --- 4. CHAT NO TERMINAL ---
print(f"IA conectada com modelo {modelo} - digite 'sair' para encerrar")
historico = []

while True:
    texto = input("\nVocê: ")
    if texto.lower() == "sair":
        break
    
    resposta = perguntar_para_ia(texto, historico)
    print(f"\nIA: {resposta}")

    # Mantém memória da conversa
    historico.append({"role": "user", "content": texto})
    historico.append({"role": "assistant", "content": resposta})import os
from openai import OpenAI

# --- 1. CONFIGURAÇÃO SEGURA DA CHAVE ---
# Nunca cole sua chave direto no código. Coloque no terminal:
# No PC: setx OPENAI_API_KEY "sua-chave-aqui"
# No vscode.dev / Linux: export OPENAI_API_KEY="sua-chave-aqui"
# Ou crie um arquivo .env com: OPENAI_API_KEY=sua-chave-aqui

# Pega a chave do sistema
#api_key = os.getenv("OPENAI_API_KEY")

#if not api_key:
 #   print("ERRO: Chave não encontrada!")
#    print("Crie uma chave em: https://platform.openai.com/api-keys")
 #   print("Depois rode: export OPENAI_API_KEY='sua-chave'")
  #  exit()
#
# --- 2. CONECTANDO NA IA ---
# Para usar Gemini (do Google - é grátis):
# client = OpenAI(
#     api_key=os.getenv("GEMINI_API_KEY"),
#     base_url="https://generativelanguage.googleapis.com/v1beta/openai/"
# )
# modelo = "gemini-2.0-flash"

# Para usar Groq (muito rápido eapi_key=os.getenv("GROQ_API_KEY"),base_url="https://api.groq.com/openai/v1")
 modelo = "llama-3.3-70b-versatile"

# Para usar OpenAI / ChatGPT (padrão):
#client = OpenAI(api_key=api_key)
#modelo = "gpt-4o-mini" # modelo mais barato e bom

# --- 3. SUA IA PERSONALIZÁVEL ---
def perguntar_para_ia(pergunta, historico=[]):
    mensagens = [
        {"role": "system", "content": "Você é uma IA assistente útil, criada em Python. Responda em português brasileiro."}
    ]
    mensagens.extend(historico)
    mensagens.append({"role": "user", "content": pergunta})

    resposta = client.chat.completions.create(
        model=modelo,
        messages=mensagens,
        temperature=0.7
    )
    return resposta.choices[0].message.content

# --- 4. CHAT NO TERMINAL ---
print(f"IA conectada com modelo {modelo} - digite 'sair' para encerrar")
historico = []

while True:
    texto = input("\nVocê: ")
    if texto.lower() == "sair":
        break
    
    resposta = perguntar_para_ia(texto, historico)
    print(f"\nIA: {resposta}")

    # Mantém memória da conversa
    historico.append({"role": "user", "content": texto})
    historico.append({"role": "assistant", "content": resposta})