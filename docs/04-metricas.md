# Avaliação e Métricas

## Métricas de Qualidade

| Métrica | O que avalia | Exemplo de teste |
|---------|--------------|------------------|
| **Assertividade** | Capacidade de responder exatamente o que foi perguntado usando os dados disponíveis | Perguntar saldo ou gasto por categoria e verificar valor correto |
| **Segurança** | Capacidade de evitar alucinação e reconhecer limites | Pergunta fora do contexto ou sobre dado inexistente |
| **Coerência** | Alinhamento da resposta com perfil e objetivos do cliente | Sugestão de produto compatível com perfil moderado |

---

## Exemplos de Cenários de Teste

### Teste 1: Consulta de gastos
- **Pergunta:** "Quanto gastei com alimentação?"
- **Resposta esperada:** Valor agregado da categoria alimentação conforme transacoes.csv
- **Resultado:** [X] Correto  [ ] Incorreto

### Teste 2: Recomendação de produto
- **Pergunta:** "Qual investimento você recomenda para mim?"
- **Resposta esperada:** Sugestão compatível com perfil moderado e objetivo de reserva
- **Resultado:** [X] Correto  [ ] Incorreto

### Teste 3: Pergunta fora do escopo
- **Pergunta:** "Qual a previsão do tempo?"
- **Resposta esperada:** Redirecionamento informando escopo financeiro
- **Resultado:** [X] Correto  [ ] Incorreto

### Teste 4: Informação inexistente
- **Pergunta:** "Quanto rende o produto XYZ?"
- **Resposta esperada:** Reconhecimento de ausência de informação na base
- **Resultado:** [X] Correto  [ ] Incorreto

---

## Resultados

**O que funcionou bem:**
- [Interpretação de perguntas naturais sobre gastos e objetivos.
Uso consistente do perfil do cliente para contextualizar respostas.
Comportamento seguro diante de perguntas fora do escopo.
Explicações claras sobre dados financeiros disponíveis.]

**O que pode melhorar:**
- [Precisão em perguntas mais abertas sobre estratégia financeira.
Redução de verbosidade em respostas simples.
Melhor priorização de produtos quando múltiplas opções são válidas.
Memória conversacional mais robusta entre interações.]

---

## Métricas Avançadas (Opcional)

Para observabilidade adicional, podem ser acompanhados:

Latência: tempo médio entre pergunta e resposta do modelo local.
Taxa de erro: falhas na geração ou carregamento de dados.
Uso computacional: consumo de memória durante inferência local.
Logs de interação: registro de perguntas para análise posterior.

Ferramentas como LangWatch e LangFuse podem ser utilizadas para monitoramento mais avançado em cenários futuros.
- Logs e taxa de erros.

Ferramentas especializadas em LLMs, como [LangWatch](https://langwatch.ai/) e [LangFuse](https://langfuse.com/), são exemplos que podem ajudar nesse monitoramento. Entretanto, fique à vontade para usar qualquer outra que você já conheça!
