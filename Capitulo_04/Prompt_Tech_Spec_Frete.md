**ATUE COMO:** Arquiteto de Software Sênior e Engenheiro de Dados.

**CONTEXTO:**
Estamos refinando a História de Usuário para o "Motor de Cálculo de Frete" da TechBrazil. Esta é uma história de Backend (sem interface visual direta). A regra é cobrar por peso e distância. Preciso das especificações técnicas para blindar o desenvolvimento.

**DETALHES DA HISTÓRIA (INPUT):**

* **Narrativa do Épico:**
    Como Gerente Financeiro/E-commerce,
    Quero configurar regras de frete baseadas no valor do carrinho (ticket) e na zona geográfica de entrega,
    Para que a empresa pare de subsidiar entregas deficitárias e proteja a margem de lucro antes da Black Friday.

* **Critérios de Aceitação:**
    1. O sistema deve aplicar frete integral (sem subsídio) para qualquer carrinho abaixo de R$ [X] (valor a definir), independentemente da região.
    2. O cálculo de frete deve aplicar um fator multiplicador de preço (ou tabela diferenciada) para Zonas de Entrega consideradas "Distantes".
    3. O checkout deve exibir o valor atualizado do frete em tempo real, mantendo a performance da página (SLA de resposta < 200ms).

**SUA MISSÃO:**
Gere as especificações técnicas para atingir a Definition of Ready (DoR).

**ESTRUTURA DA RESPOSTA:**

1.  **Design Técnico (Contrato de Interface):**
    * Como não temos tela, precisamos do contrato da API.
    * Esboce um exemplo de **JSON de Request** (O que o sistema envia: CEP, Peso, Valor).
    * Esboce um exemplo de **JSON de Response** (O que a API devolve: ValorFrete, Prazo, Transportadora).

2.  **Requisitos Não-Funcionais (NFRs - Qualidade de Serviço):**
    * **Performance:** Qual a latência máxima aceitável (em ms) para não travar o checkout na Black Friday?
    * **Resiliência:** Defina o Fallback. O que acontece se o serviço dos Correios cair? (Ex: Retornar tabela fixa ou erro tratado?)

3.  **Observabilidade e Dados (Logs & Metrics):**
    * Quais eventos devemos registrar para auditoria e monitoramento no Data Lake/PowerBI? (Ex: `api_frete_timeout`, `calculo_sucesso`).
    * *Nota:* Não inclua dados sensíveis (PII) nos logs.

4.  **Sugestão de Modelagem Visual:**
    * Qual diagrama (Sequência ou Atividade) explica melhor essa integração? Justifique.

**CENÁRIO TÉCNICO:** Alta concorrência (Black Friday). API Rest.
