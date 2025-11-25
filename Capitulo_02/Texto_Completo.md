# 📘 CAPÍTULO 2: DA ESTRATÉGIA AO ÉPICO (GITHUB PROJECTS & AI)

### 🎯 OBJETIVOS TÁTICOS DA MISSÃO

*   **Traduzir dialetos:** Converter "Financês" (OKRs e Metas de Lucro) em "Agilês" (Épicos e Issues).
*   **Derrubar a "Grande Muralha":** Eliminar os silos entre a Gestão (Planilhas) e a Engenharia (Código) usando o GitHub Projects.
*   **Dominar o "Context Switching":** Aprender a alternar os modos de operação da IA (de Motor Lógico para Consultor Estratégico).

---

## 1. O Problema Gerencial: A Grande Muralha 🧱

Existe uma doença silenciosa nas empresas: a **Fragmentação de Contexto**.

Observe o campo de batalha corporativo:

*   👔 **A Diretoria** vive em planilhas de Excel e slides de PowerPoint.
*   📋 **A Gerência** vive em ferramentas de tickets burocráticas (que os devs odeiam).
*   💻 **O Time de Desenvolvimento** vive no GitHub/GitLab (onde o trabalho real acontece).

Entre esses grupos, existe uma **Grande Muralha**. A estratégia é definida no Excel, mas morre antes de chegar ao repositório de código. O desenvolvedor recebe uma tarefa (*"Mudar botão para azul"*) sem saber que a meta da empresa era *"Aumentar a conversão em 10%"*.

**Resultado?** O botão fica azul, mas a conversão não sobe. O desenvolvedor vira um "cumpridor de tarefas" desmotivado.

A solução do Analista de Negócios Ágil é brutalmente simples: **Se o código mora no GitHub, a estratégia também deve morar lá.** Nós vamos demolir a muralha e gerenciar o projeto onde a construção acontece.

---

## 2. Fundamentação Teórica: A Pirâmide Simplificada 🔺

Para conectar o CEO ao Estagiário sem perder o sentido, usamos uma hierarquia de valor enxuta baseada nas melhores práticas de Análise de Negócios (Howard Podeswa):

1.  **ESTRATÉGIA (OKR):** O objetivo macro. *Ex: Aumentar Margem de Lucro.*
2.  **INICIATIVA:** O projeto temporário. *Ex: Novo Motor de Frete.*
3.  **ÉPICO:** A fatia de entrega. *Ex: Precificação Dinâmica por Região.*

### A Simplicidade do GitHub

Muitas ferramentas de gestão complicam isso com dez tipos de objetos diferentes. O GitHub é elegante:

*   Tudo é uma **Issue**.
*   Um **Épico** é apenas uma Issue com uma Label `Epic`.
*   Tarefas filhas são Issues listadas dentro do Épico.

Simplicidade é poder. Menos configuração, mais entrega.

---

## 3. Mão Na Massa: O Tutorial Técnico 🛠️

Vamos voltar ao Google AI Studio. Mas atenção, soldado: precisamos fazer um ajuste crítico agora.

### 🔄 PASSO 0: O RESET TÁTICO (CRÍTICO!)

> [!IMPORTANT]
> **ATENÇÃO:** Se você veio direto do Capítulo 1, sua IA ainda está configurada nas *System Instructions* para agir como um "Motor de Frete". Se você pedir uma análise estratégica agora, ela vai tentar calcular o frete do seu texto ou dar erro.

A IA é uma ferramenta multimodal. Você precisa trocar a chave.

1.  No Google AI Studio, clique em **Create New** (Canto superior esquerdo) ou apague o texto das *System Instructions*.
2.  Deixe a caixa **System Instructions VAZIA** para esta missão.

**Por que?** Queremos que a IA use sua criatividade total como consultora, sem as amarras de regras rígidas de cálculo.

### 🌪️ PASSO 1: A ANÁLISE DO CAOS

Agora que a "sala de guerra" está limpa, vamos lidar com o problema. Você recebeu um e-mail confuso do CEO Roberto.

**O E-mail do Caos:**
> "Pessoal, vi os números. Estamos perdendo dinheiro com frete grátis para quem compra pouco! Precisamos parar com isso. Quero que o sistema cobre caro de quem mora longe e dê desconto pra quem é VIP. E tem que ser rápido, porque a Black Friday tá chegando. Ah, e o pessoal do Acre reclamou que não consegue comprar. Resolvam."

Copie o Prompt abaixo e cole na caixa de Chat (**User Input**):

```markdown
ATUE COMO: Analista de Negócios Sênior especialista em E-commerce.

CONTEXTO: Recebi um e-mail desestruturado do CEO (abaixo) com demandas urgentes. Preciso transformar isso em trabalho técnico organizado.

E-MAIL DO CEO: "Pessoal, vi os números. Estamos perdendo dinheiro com frete grátis para quem compra pouco! Precisamos parar com isso. Quero que o sistema cobre caro de quem mora longe e dê desconto pra quem é VIP. E tem que ser rápido, porque a Black Friday tá chegando. Ah, e o pessoal do Acre reclamou que não consegue comprar. Resolvam."

SUA MISSÃO:
1. Analise o pedido e identifique os Objetivos de Negócio.
2. Quebre essa demanda em 3 ÉPICOS TÉCNICOS claros para o time de desenvolvimento.
3. Para cada Épico, escreva:
   - Título (Formato: Verbo + Objeto)
   - Narrativa do Épico (Formato: Como <persona>, quero <ação>, para <valor>)
   - Critérios de Aceitação (Listar 3 checkboxes)

FORMATO: Markdown pronto para copiar e colar.
```

Aperte **Run**. A IA vai transformar o pânico do Roberto em um plano de batalha estruturado em segundos.

### ✨ O Resultado (A Mágica Acontece)

Em segundos, o Gemini devolve uma análise estruturada. Veja como ele organizou o caos do Roberto:

---

#### ÉPICO 1: Reestruturar Motor de Cálculo de Frete
**Prioridade:** Crítica
**Narrativa do Épico:**
Como Gerente Financeiro/E-commerce, Quero configurar regras de frete baseadas no valor do carrinho (ticket) e na zona geográfica de entrega, Para que a empresa pare de subsidiar entregas deficitárias e proteja a margem de lucro antes da Black Friday.

**Critérios de Aceitação:**
- [ ] O sistema deve aplicar frete integral (sem subsídio) para qualquer carrinho abaixo de R$ [X].
- [ ] O cálculo de frete deve aplicar um fator multiplicador para Zonas de Entrega "Distantes".
- [ ] O checkout deve exibir o valor atualizado do frete em tempo real (SLA < 200ms).

*(...A IA também gerou o Épico 2: Benefícios VIP e Épico 3: Correção Acre...)*

---

> [!NOTE]
> **A LÓGICA POR TRÁS DA ESTRUTURA (MINDSET)**
>
> **Por que criar um Projeto novo?**
> Na Análise Ágil, chamamos isso de **Iniciativa**.
> *   **O Problema:** O CEO quer estancar a perda de margem.
> *   **A Iniciativa (O Board):** É o container temporário onde focaremos energia.
> *   **Os Épicos (As Issues):** São as grandes entregas.
>
> **Rastreabilidade:** Todo item deve "pagar aluguel".
> *   Problema (DOR): "Perdendo dinheiro" ➔ Solução: **Épico 1**.
> *   Problema (GANHO): "Desconto VIP" ➔ Solução: **Épico 2**.
> *   Problema (RISCO): "Acre reclamou" ➔ Solução: **Épico 3**.

---

## 4. Estudo de Caso: TechBrazil no GitHub 🐙

Com a resposta da IA em mãos, vamos para a ferramenta real.

### 0. O Batismo (Criando o Repositório)
Antes de criar os cards, precisamos de uma "casa" para o projeto.
1.  Acesse o GitHub e faça login.
2.  Clique no ícone `+` e selecione **New repository**.
3.  **Repository name:** `techbrazil-checkout`.
4.  **Public/Private:** Selecione `Public`.
5.  Marque a opção **Add a README file**.
6.  Clique em **Create repository**.

### 1. Configurando o Quartel General (Project Board)
1.  Acesse a aba **Projects** no menu superior do repositório.
2.  Clique no botão verde **Link a project** ou **New Project**.
3.  Na janela de templates, localize a seção *Featured* e selecione **Kanban**.
4.  Defina o nome do projeto como: `Iniciativa: Checkout Dinâmico` e clique em **Create**.

### 2. Criando o Épico
1.  Na coluna **Backlog**, clique no botão `+ Add item` e selecione **Create new issue**.
2.  **Título:** Cole o título gerado pela IA: `Reestruturar Motor de Cálculo de Frete`.
3.  **Descrição:** Cole todo o restante do texto da IA (Narrativa e Critérios).

> [!TIP]
> **Nota Técnica:** O GitHub renderiza nativamente o Markdown da IA. Os colchetes `[ ]` se transformarão automaticamente em checkboxes interativos ao salvar.

### 3. A Etiqueta de Poder (Taxonomia)
Antes de salvar, precisamos classificar este item.
1.  Clique no ícone **Labels** na parte inferior da janela.
2.  Digite `Epic` e selecione **Create new label**.
3.  **Sugestão visual:** Escolha a cor **Roxo Escuro** (padrão de mercado para Épicos).
4.  Repita o processo para criar a label `Prioridade: Alta` (Cor: Vermelha).
5.  Clique no botão verde **Create**.

**O Resultado:** Agora, quando o Desenvolvedor olhar o projeto, ele não vê um desejo vago. Ele vê uma Issue técnica, priorizada e documentada, vivendo dentro do repositório onde o código será escrito.

---

## 5. Resumo do Comandante 🎖️

Leve isto para o front:

*   🧠 **Domine o Context Switching:** A IA não é mágica, é uma ferramenta configurável. Saiba quando usar *System Instructions* (regras rígidas) e quando deixá-las vazias (análise criativa).
*   🏷️ **Simplicidade no GitHub:** Não invente processos complexos. Um Épico é apenas uma Issue com uma etiqueta. Se é fácil de criar, é fácil de manter.
*   🏗️ **Derrube a Muralha:** Nunca mantenha os requisitos em um lugar e o código em outro. A verdade deve ser única e centralizada.

---

### 🔜 PRÓXIMA MISSÃO
**Temos os Épicos. Agora precisamos desenhar a jornada do usuário. Mas cuidado: não vamos desenhar telas "bonitinhas". Vamos projetar experiências baseadas em dados.**

[➡️ Avance para o Capítulo 3](#)
```
