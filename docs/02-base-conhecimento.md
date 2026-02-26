# Base de Conhecimento

## Dados Utilizados

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Permite ao agente recuperar interações anteriores do cliente, evitar repetição de explicações e manter continuidade do atendimento |
| `perfil_investidor.json` | JSON | Define características do cliente (perfil, renda, objetivos e tolerância a risco), servindo como base para personalização das respostas |
| `produtos_financeiros.json` | JSON | Catálogo de produtos disponíveis com risco, rentabilidade e indicação de uso, permitindo ao agente sugerir opções compatíveis com o perfil |
| `transacoes.csv` | CSV | Histórico financeiro do cliente usado para análise de padrão de gastos, cálculo de saldo e identificação de comportamento financeiro |

---

## Adaptações nos Dados

[Sim. Os dados mockados foram expandidos para ir além de uma simples lista de transações.
Foram incluídos:
Categorias automáticas (alimentação, moradia, transporte, lazer etc.).
Identificação de recorrência (ex: assinaturas mensais).
Campo de renda fixa e renda variável.
Meta financeira declarada pelo usuário.
Indicador de comprometimento de renda (%).
Histórico mensal consolidado (resumo por mês).
A ideia foi estruturar os dados de forma que o modelo não precise “interpretar números soltos”, mas receba contexto organizado.]

---

## Estratégia de Integração

### Como os dados são carregados?

[Os dados (JSON ou banco leve) são carregados no início da sessão.
O backend transforma essas informações em dois formatos:
Estrutura bruta para cálculos determinísticos.
Estrutura resumida e organizada para envio ao modelo.
Sempre que o usuário faz uma pergunta, o sistema atualiza os cálculos antes de montar o contexto enviado ao modelo.]

### Como os dados são usados no prompt?

[Os dados não vão integralmente no system prompt.
O system prompt define regras fixas (ex: “responda apenas com base nos dados fornecidos”).
Os dados financeiros do usuário são inseridos dinamicamente como contexto a cada interação relevante. O envio prioriza:
Resumo financeiro atual.
Transações recentes.
Indicadores consolidados (saldo, média de gasto, projeção).
Isso evita contexto excessivo e reduz risco de erro.]

---

## Exemplo de Contexto Montado

Contexto Financeiro Atual do Cliente

Dados do Cliente:
Nome: João Silva

Perfil financeiro: Moderado

Renda média mensal: R$ 7.000

Saldo disponível atual: R$ 5.000

Comprometimento da renda: 62%

Resumo do mês atual:

Total gasto até agora: R$ 4.320

Categoria com maior despesa: Alimentação (R$ 1.150)

Despesas recorrentes identificadas: Streaming, Aluguel, Academia

Últimas transações:

01/11: Supermercado – R$ 450 – Categoria: Alimentação

03/11: Streaming – R$ 55 – Categoria: Assinatura

05/11: Restaurante – R$ 120 – Categoria: Alimentação

07/11: Combustível – R$ 300 – Categoria: Transporte

Meta declarada:

Formar reserva de emergência de R$ 20.000
