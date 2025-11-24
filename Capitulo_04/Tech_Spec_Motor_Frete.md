## 🛠️ Especificação Técnica (Tech Spec) - Motor de Cálculo de Frete

**Objetivo Técnico:** Implementar uma API de alta performance para cálculo de frete que suporte regras de negócio dinâmicas (subsídio por ticket e zona geográfica), com foco em resiliência e proteção de margem.

### 1. Design Técnico (Contrato de Interface - API Contract)

Para garantir a desacoplamento entre o Frontend (Checkout) e o Backend (Motor de Frete), utilizaremos uma API RESTful. O contrato deve suportar os dados necessários para as regras de negócio (valor do carrinho e geolocalização).

**Endpoint Sugerido:** `POST /api/v1/logistics/freight/calculate`

#### **JSON de Request (Entrada)**
*O que o Checkout envia para o Motor:*

```json
{
  "cartId": "a1b2c3d4-e5f6-7890",
  "customer": {
    "zipCode": "69000-000" // CEP Destino (Crítico para regra de Zona Distante)
  },
  "cartValue": 149.90, // Valor total dos produtos (Crítico para regra de Subsídio)
  "items": [
    {
      "sku": "TECH-12345",
      "quantity": 1,
      "weightInGrams": 500,
      "dimensions": {
        "length": 20,
        "width": 15,
        "height": 10
      },
      "category": "eletronicos" // Pode influenciar regras específicas de transportadora
    }
  ],
  "storeId": "TB-BR-MAIN"
}
```

#### **JSON de Response (Saída)**
*O que a API devolve para o Checkout:*

```json
{
  "calculationId": "req_99887766", // Trace ID para auditoria
  "zipCodeOrigin": "01000-000",
  "zipCodeDestination": "69000-000",
  "appliedRules": [
    "NO_SUBSIDY_LOW_TICKET", // Flag indicando que o subsídio foi removido (Regra < R$ X)
    "REMOTE_ZONE_SURCHARGE"  // Flag indicando sobretaxa de zona distante
  ],
  "options": [
    {
      "carrierId": "CORREIOS_SEDEX",
      "carrierName": "Correios Sedex",
      "serviceType": "EXPRESS",
      "deliveryTimeDays": 3,
      "price": 45.50, // Preço final já calculado com as regras
      "originalPrice": 45.50, // Preço sem subsídio (para comparação analítica)
      "currency": "BRL"
    },
    {
      "carrierId": "TOTAL_EXPRESS_STD",
      "carrierName": "Total Express",
      "serviceType": "STANDARD",
      "deliveryTimeDays": 8,
      "price": 22.90,
      "currency": "BRL"
    }
  ]
}
```

---

### 2. Requisitos Não-Funcionais (NFRs - Qualidade de Serviço)

Dado o cenário de **Black Friday**, a estabilidade é inegociável.

#### **Performance (Latência e Throughput)**
*   **SLA de Latência:** O cálculo deve ser retornado em **p95 < 150ms** e **p99 < 200ms**.
    *   *Estratégia:* Implementar Cache (Redis) com TTL curto (ex: 5 min) para consultas repetidas de mesmo CEP + Faixa de Peso, evitando chamadas desnecessárias a APIs externas de transportadoras.
*   **Throughput:** O sistema deve suportar picos de até **10.000 RPM** (Requisições por Minuto) com auto-scaling horizontal (Kubernetes HPA baseado em CPU e Custom Metrics).

#### **Resiliência (Fallback Strategy)**
*   **Cenário de Falha:** O serviço dos Correios ou Gateway de Frete (ex: Intelipost/Frenet) está fora do ar ou respondendo acima de 500ms (Timeout).
*   **Padrão Circuit Breaker:** Implementar Circuit Breaker. Se a taxa de erro externo > 10%, abrir o circuito.
*   **Comportamento de Fallback (Plano B):**
    1.  O sistema **NÃO** deve retornar erro 500 para o cliente.
    2.  Deve-se consultar uma **Tabela de Contingência Interna** (armazenada em banco de alta leitura como DynamoDB ou MongoDB).
    3.  Esta tabela deve conter preços "seguros" (com margem de segurança de +15% para evitar prejuízo) baseados apenas em Faixa de CEP e Peso, ignorando cotação em tempo real.
    4.  A flag `isFallback: true` deve ser logada internamente.

---

### 3. Observabilidade e Dados (Logs & Metrics)

Como Engenheiro de Dados, precisamos garantir que cada cálculo gere insumos para o time financeiro analisar a rentabilidade.

#### **Eventos Estruturados (JSON Logs)**
Os logs devem ser enviados para o Data Lake (S3/BigQuery) via stream (Kinesis/Kafka).

**Evento 1: `freight_calculated`**
*   **Objetivo:** Auditoria financeira e validação das regras.
*   **Campos:**
    *   `cart_id`: UUID
    *   `cart_value`: Decimal
    *   `freight_value_final`: Decimal
    *   `rule_subsidy_applied`: Boolean (False se valor < X)
    *   `rule_remote_zone`: Boolean (True se for Norte/Nordeste interior, por exemplo)
    *   `calculation_source`: "REALTIME_API" ou "FALLBACK_TABLE"
    *   `processing_time_ms`: Integer

**Evento 2: `freight_external_error`**
*   **Objetivo:** Monitorar saúde das transportadoras parceiras.
*   **Campos:** `carrier_name`, `error_code`, `latency_ms`.

#### **O que NÃO logar (Segurança/LGPD):**
*   Nome do Cliente.
*   Endereço completo (Rua, Número, Complemento).
*   Documentos (CPF/CNPJ).
*   *Apenas o CEP (ZipCode) é permitido para fins de cálculo de zona.*

---

### 4. Sugestão de Modelagem Visual

**Diagrama Recomendado: Diagrama de Sequência (Sequence Diagram)**

**Justificativa:**
Como estamos lidando com uma integração de Backend que envolve dependências externas e requisitos temporais estritos, o Diagrama de Sequência é o artefato ideal para a Definition of Ready (DoR). Ele ilustra claramente:

1.  O **fluxo da chamada** do Checkout para o Motor de Frete.
2.  O momento exato da **verificação das regras de negócio** (If Cart < X -> Remove Subsídio).
3.  A chamada paralela ou sequencial para as **APIs das Transportadoras**.
4.  A ativação do **Fallback** em caso de timeout.

*Exemplo textual do fluxo:*
`Checkout -> [API Gateway] -> Motor de Frete -> (Cache Redis?) --(miss)--> [Regras de Negócio] -> APIs Externas -> (Merge de Resultados) -> Retorno JSON.`

---

### ✅ Checklist para Aprovação (DoR)
1.  [ ] Tabela de "Zonas Distantes" (faixas de CEP) fornecida pelo time de Logística.
2.  [ ] Valor de corte "R$ [X]" definido pelo Financeiro.
3.  [ ] Credenciais das APIs das transportadoras configuradas no ambiente de Staging.
4.  [ ] Tabela de Contingência (Fallback) populada no banco de dados.
