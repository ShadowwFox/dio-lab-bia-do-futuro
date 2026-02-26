# Código da Aplicação

Arquitetura Escolhida

Interface: Streamlit

LLM: Llama 3.2 3B rodando local via Ollama

Base de Conhecimento: JSON e CSV carregados localmente

Backend: Python

Fluxo:

Usuário envia pergunta.

Sistema carrega dados (perfil, transações, produtos).

Dados são resumidos.

Prompt é montado.

Modelo local responde.

## Estrutura da Pasta

```
src/
├── app.py
├── agente.py
├── config.py
├── data/
│   ├── transacoes.csv
│   ├── perfil_investidor.json
│   ├── produtos_financeiros.json
│   └── historico_atendimento.csv
└── requirements.txt
```

## requirements.txt

```
streamlit
pandas
python-dotenv
ollama
```

## config.py

```
MODEL_NAME = "llama3.2:3b"
```
## agente.py

```
import json
import pandas as pd
import ollama
from config import MODEL_NAME


def carregar_dados():
    perfil = json.load(open("data/perfil_investidor.json", "r", encoding="utf-8"))
    produtos = json.load(open("data/produtos_financeiros.json", "r", encoding="utf-8"))
    transacoes = pd.read_csv("data/transacoes.csv")
    return perfil, produtos, transacoes


def resumir_transacoes(transacoes):
    total_gasto = transacoes["valor"].sum()
    por_categoria = transacoes.groupby("categoria")["valor"].sum().to_dict()
    return total_gasto, por_categoria


def montar_prompt(perfil, produtos, total_gasto, por_categoria, pergunta_usuario):

    contexto = f"""
Perfil do Cliente:
Nome: {perfil['nome']}
Renda Mensal: {perfil['renda_mensal']}
Perfil de Investidor: {perfil['perfil_investidor']}
Objetivo: {perfil['objetivo_principal']}

Resumo Financeiro:
Total gasto: {total_gasto}
Gastos por categoria: {por_categoria}

Produtos disponíveis:
{produtos}
"""

    system_prompt = """
Você é um agente financeiro.
Responda apenas com base nos dados fornecidos.
Nunca invente valores.
Se faltar dado, peça ao usuário.
"""

    prompt_final = f"{system_prompt}\n{contexto}\nPergunta: {pergunta_usuario}"

    return prompt_final


def gerar_resposta(prompt):
    response = ollama.chat(
        model=MODEL_NAME,
        messages=[{"role": "user", "content": prompt}]
    )
    return response["message"]["content"]


def responder(pergunta_usuario):
    perfil, produtos, transacoes = carregar_dados()
    total_gasto, por_categoria = resumir_transacoes(transacoes)
    prompt = montar_prompt(perfil, produtos, total_gasto, por_categoria, pergunta_usuario)
    return gerar_resposta(prompt)
```

## app.py

```
import streamlit as st
from agente import responder

st.set_page_config(page_title="Agente Financeiro", layout="centered")

st.title("Agente Financeiro Local")

if "historico" not in st.session_state:
    st.session_state.historico = []

pergunta = st.chat_input("Digite sua pergunta financeira")

if pergunta:
    resposta = responder(pergunta)

    st.session_state.historico.append(("Usuário", pergunta))
    st.session_state.historico.append(("Agente", resposta))

for autor, mensagem in st.session_state.historico:
    with st.chat_message("assistant" if autor == "Agente" else "user"):
        st.write(mensagem)
```

## Como Rodar

```
1️⃣ Instalar Ollama
https://ollama.com/

2️⃣ Baixar modelo
ollama pull llama3.2:3b

3️⃣ Instalar dependências
pip install -r requirements.txt

4️⃣ Rodar aplicação
streamlit run app.py
```
