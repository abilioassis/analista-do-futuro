Olá, time de UX.

Estruturei a especificação abaixo focando na redução da carga cognitiva do usuário VIP. O objetivo é que ele perceba o benefício *imediatamente* ao entrar no carrinho, validando sua decisão de compra durante a alta concorrência da Black Friday.

Aqui está a descrição do Wireframe de Baixa Fidelidade para a tela de **Carrinho de Compras (Versão VIP)**.

---

### 1. Elementos de Informação
Estes são os dados e componentes que **precisam** constar na interface para atender aos critérios de aceitação e à regra de negócio.

*   **Tag/Badge de Reconhecimento:** Um elemento visual no topo da página ou próximo ao nome do usuário indicando o status "Cliente VIP" ou "Black Friday VIP Member".
*   **Seletor de Frete (Modificado):**
    *   Input de CEP (padrão).
    *   **Valor do Frete Original (Riscado/Strikethrough):** O valor que seria cobrado pelas regras restritivas do Épico 1 (ex: R$ 45,00).
    *   **Valor do Frete VIP (Destacado):** O valor final para o VIP (ex: "Grátis" ou "R$ 22,50").
    *   **Label de Benefício:** Texto curto ao lado do preço explicando a origem do desconto (ex: "Benefício VIP").
*   **Resumo do Pedido (Order Summary):**
    *   Subtotal dos produtos.
    *   Linha de Descontos: Deve separar o que é desconto de produto do que é desconto de logística/frete.
    *   **Totalizador de Economia:** "Você economizou R$ X nesta compra" (Somando promoções de Black Friday + Benefício de Frete VIP).
*   **CTA de Checkout (Botão de Ação):** Deve permanecer inalterado em função, mas livre de obstruções visuais.

---

### 2. Hierarquia Visual
A organização visual deve guiar o olho do usuário para confirmar a vantagem financeira antes de prosseguir para o pagamento.

1.  **Nível 1 (Foco Principal - Conversão):**
    *   **Botão "Finalizar Compra" / "Ir para Pagamento":** Continua sendo o elemento de maior peso visual.
    *   **Total Final do Pedido:** O valor a pagar deve estar claro e próximo ao botão.

2.  **Nível 2 (Foco Secundário - Retenção/Validação):**
    *   **Bloco de Frete com Desconto VIP:** Diferente do carrinho padrão onde o frete é uma informação "dolorosa" (em cinza ou pequeno), aqui ele deve ganhar destaque (cor de destaque/sucesso). O "Grátis" ou o valor reduzido deve competir em atenção com o subtotal.
    *   **Mensagem de Feedback VIP:** A faixa ou box que avisa que o desconto foi aplicado.

3.  **Nível 3 (Informação de Apoio):**
    *   Lista de produtos (fotos e nomes).
    *   Valor original do frete (riscado) – deve ser visível o suficiente para comparação, mas com baixo contraste (cinza claro) para não confundir a leitura do total.

---

### 3. Microcopy (Texto de Interface)
Considerando o contexto de Black Friday (urgência) e o status VIP (exclusividade).

#### Estado A: Sucesso (Meta Atingida)
*Cenário: O usuário é VIP e o benefício (ex: Frete Grátis) foi aplicado automaticamente.*

*   **Banner de Topo/Feedback:** "Olá, VIP! Seu benefício exclusivo de Black Friday foi ativado."
*   **Linha do Frete:** "Frete VIP: ~~R$ 35,00~~ **Grátis**"
*   **Rodapé do Resumo:** "Economia VIP aplicada com sucesso."

#### Estado B: Upsell / Incentivo (Meta Não Atingida)
*Cenário: O usuário é VIP, mas a regra de negócio exige um valor mínimo (ex: R$ 200,00) para liberar o frete grátis total, caso contrário ele tem apenas 50% de desconto. Precisamos incentivá-lo a aumentar o ticket médio.*

*   **Banner de Topo/Feedback:** "Você tem 50% OFF no frete. Quer **Frete Grátis**?"
*   **Barra de Progresso ou Aviso Próximo ao Total:** "Adicione mais **R$ 45,00** ao carrinho para desbloquear **Frete Grátis VIP**."
*   **Linha do Frete:** "Frete VIP (50% OFF): ~~R$ 30,00~~ **R$ 15,00**"

---

### 📝 Nota do Arquiteto para UI:
Ao desenhar, considere que a **consulta ao CRM pode ter um delay de milissegundos**.
*   Preveja um estado de *loading* (skeleton screen) apenas na área de cálculo de frete, para não bloquear a visualização dos produtos.
*   Use uma cor distinta (ex: Dourado, Roxo ou o Verde da marca) especificamente para os elementos VIP, diferenciando-os dos descontos "comuns" de Black Friday que todos os usuários veem.
