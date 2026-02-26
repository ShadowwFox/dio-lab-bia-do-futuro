## Agente Financeiro Conversacional

Protótipo de agente financeiro baseado em LLM capaz de analisar dados estruturados do cliente, responder perguntas em linguagem natural e apoiar organização financeira pessoal.

O projeto demonstra integração entre modelo de linguagem local, base de conhecimento estruturada e interface conversacional simples.

Objetivo

Desenvolver um agente capaz de:

Interpretar perguntas financeiras em linguagem natural

Analisar histórico de transações

Utilizar perfil do cliente para contextualizar respostas

Explorar possibilidades financeiras compatíveis com o contexto

Manter comportamento seguro e transparente quanto às limitações

Problema

Grande parte das pessoas não possui clareza sobre seu comportamento financeiro.
Mesmo com acesso a aplicativos bancários, é comum dificuldade em:

Identificar padrões de gasto

Relacionar decisões atuais a impactos futuros

Acompanhar metas financeiras

Tomar decisões com base em dados

Ferramentas existentes frequentemente exigem esforço manual elevado ou conhecimento técnico.

Solução

O agente atua como um copiloto financeiro conversacional.

Ele integra dados do cliente (perfil, transações e catálogo de produtos) e permite que o usuário interaja via chat para compreender sua situação financeira de forma prática.

Principais capacidades:

Análise de gastos por categoria

Explicação da situação financeira atual

Apoio ao acompanhamento de metas

Exploração de opções financeiras compatíveis com perfil

Comportamento seguro diante de lacunas informacionais

Arquitetura

Interface: Streamlit (chat web simples)
LLM: Modelo local via Ollama (Llama 3.2 3B)
Base de conhecimento: JSON e CSV locais
Backend: Python

Fluxo geral:

Usuário envia pergunta

Dados estruturados são carregados

Sistema gera resumo financeiro

Prompt contextualizado é montado

Modelo local gera resposta

Resposta é exibida no chat

Estrutura do Projeto
src/
├── app.py              # Interface Streamlit
├── agente.py           # Lógica do agente
├── config.py           # Configuração do modelo
├── data/
│   ├── transacoes.csv
│   ├── perfil_investidor.json
│   ├── produtos_financeiros.json
│   └── historico_atendimento.csv

| Arquivo                   | Utilização                                    |
| ------------------------- | --------------------------------------------- |
| historico_atendimento.csv | Continuidade e memória conversacional         |
| perfil_investidor.json    | Contextualização do cliente                   |
| produtos_financeiros.json | Espaço de opções financeiras disponíveis      |
| transacoes.csv            | Análise comportamental e cálculos financeiros |

Estratégia Anti-Alucinação

Respostas baseadas prioritariamente nos dados fornecidos

Solicitação explícita quando faltar informação

Separação entre cálculos determinísticos e geração textual

Bloqueio de compartilhamento de dados sensíveis

Recomendações dependentes de contexto mínimo
└── requirements.txt

Como Executar
ollama pull llama3.2:3b
3. Instalar dependências
pip install -r requirements.txt
4. Executar aplicação
streamlit run app.py
Avaliação

A avaliação combinou testes estruturados e feedback de usuários.

Métricas consideradas:

Assertividade

Segurança

Coerência

Cenários de teste incluíram consulta de gastos, exploração de produtos, perguntas fora do escopo e solicitações de dados inexistentes.

Limitações

Dependência da qualidade dos dados fornecidos

Não executa operações financeiras

Não substitui consultoria profissional

Memória conversacional limitada ao protótipo

Capacidade analítica condicionada ao contexto disponível

Próximos Passos

Persistência real de memória conversacional

Integração com banco de dados

Camada de validação financeira mais robusta

Dashboard complementar de visualização

Avaliação com maior número de usuários

Pitch

O pitch apresenta o problema, funcionamento do agente, demonstração e diferenciais da solução.

Link do vídeo: (inserir após gravação)

Licença

Projeto desenvolvido para fins educacionais e experimentais.
