# Data Modeling — Kimball, Star Schema, Snowflake e SCD

> Aprenda **modelagem dimensional** para **data warehouse**: **Kimball**, **star/snowflake**, fatos, dimensões e **SCD** para **engenharia de dados**.

[← Índice](../../README.md) · [SQL](../sql/README.md) · [Data Warehouse](../data-warehouse/README.md) · [dbt](../dbt/README.md) · [Lakehouse](../lakehouse/README.md)

---

## Por que modelagem de dados é o coração do DW?

Sem um **modelo** claro, o warehouse vira um lago de tabelas confusas. A abordagem **Kimball** (dimensional) organiza o negócio em **fatos** (métricas) e **dimensões** (contexto), facilitando BI e performance.

Um **engenheiro de dados** modela para:

- Entregar marts compreensíveis para analytics
- Controlar granularidade e chaves surrogate
- Historiar mudanças com **SCD**
- Alinhar bronze/silver/gold a contratos de negócio

**Importância:** ⭐⭐⭐⭐⭐

---

## O que você precisa dominar

| Tópico | Nível | Descrição |
|--------|-------|-----------|
| Fatos e dimensões | ⭐⭐⭐⭐⭐ | Grão, additividade |
| Star schema | ⭐⭐⭐⭐⭐ | Modelo analítico padrão |
| Snowflake schema | ⭐⭐⭐ | Dimensões normalizadas |
| SCD Types 1/2/3 | ⭐⭐⭐⭐⭐ | Histórico de atributos |
| Surrogate keys | ⭐⭐⭐⭐⭐ | Independência da fonte |
| Conformidade de dimensões | ⭐⭐⭐⭐ | Dims compartilhadas |
| Data vault (visão) | ⭐⭐⭐ | Alternativa enterprise |

---

## Quando usar cada abordagem

| Cenário | Modelo recomendado |
|---------|-------------------|
| BI self-service, métricas claras | **Star schema** (Kimball) |
| Dimensões muito grandes/normalizadas | Snowflake (com cuidado) |
| Integração multi-fonte enterprise | Data Vault 2.0 (hub/link/sat) |
| Lakehouse analítico | Medallion + marts dimensionais |
| App OLTP | 3FN — não force dimensional no OLTP |

---

## Recursos recomendados

### Livros e referências
- *The Data Warehouse Toolkit* — Ralph Kimball
- *Star Schema: The Complete Reference* — Christopher Adamson
- Documentação dbt sobre modeling

### Cursos e guias
- [dbt Learn — Analytics Engineering](https://docs.getdbt.com/guides)
- Material Kimball Group (artigos clássicos)

### Projetos práticos
- Modelo Northwind/Chinook em star schema
- SCD Type 2 em SQL puro ([guia SQL](../sql/README.md))
- Marts dbt: `fct_*` + `dim_*`

---

## Exemplos práticos

### Star schema — esboço

```text
        dim_customer
             |
dim_date -- fct_orders -- dim_product
             |
        dim_store
```

### Tabela fato — grão: 1 linha por item de pedido

```sql
CREATE TABLE fct_order_items (
  order_item_sk   BIGINT PRIMARY KEY,
  order_id        BIGINT NOT NULL,
  order_date_sk   INT NOT NULL,      -- FK dim_date
  customer_sk     INT NOT NULL,      -- FK dim_customer
  product_sk      INT NOT NULL,      -- FK dim_product
  quantity        INT,
  unit_price      NUMERIC(12,2),
  line_total      NUMERIC(12,2)      -- métrica aditiva
);
```

### SCD Type 2 — histórico

```sql
-- Fecha versão atual
UPDATE dim_customer
SET valid_to = CURRENT_DATE - 1, is_current = FALSE
WHERE customer_id = 123 AND is_current = TRUE;

-- Abre nova versão
INSERT INTO dim_customer (
  customer_sk, customer_id, name, city,
  valid_from, valid_to, is_current
) VALUES (
  nextval('dim_customer_sk'), 123, 'Ana Silva', 'São Paulo',
  CURRENT_DATE, '9999-12-31', TRUE
);
```

### Tipos de SCD (resumo)

| Tipo | Comportamento | Uso |
|------|---------------|-----|
| **SCD1** | Sobrescreve | Correção de typo, sem histórico |
| **SCD2** | Nova linha + validade | Mudança de endereço, plano |
| **SCD3** | Coluna “anterior” | Só último valor anterior |

---

## Padrões e boas práticas

| Padrão | Quando usar | Exemplo |
|--------|-------------|---------|
| **Surrogate key** | Sempre em dims/fatos DW | `customer_sk` |
| **Degenerate dimension** | IDs de negócio na fato | `order_id` na fato |
| **Junk dimension** | Flags/low-cardinality juntos | `dim_order_flags` |
| **Role-playing** | Mesma dim_date várias vezes | order_date vs ship_date |
| **Conformidade** | Mesma dim em vários marts | `dim_customer` única |

---

## Anti-padrões comuns

- **Grão errado** na fato (mistura pedido e item)
- **Usar só natural key** da fonte como PK do DW
- **SCD2 em tudo** sem necessidade (custo e complexidade)
- **Dimensão que explode** (muito atributos mutáveis sem desenho)
- **Métricas não aditivas** tratadas como SUM sem cuidado (médias)

---

## Checklist de domínio em modelagem

- [ ] Defino o grão da fato antes de criar tabelas
- [ ] Separó fatos e dimensões com clareza
- [ ] Implemento SCD1 e SCD2 corretamente
- [ ] Uso surrogate keys e datas de validade
- [ ] Desenho star schema legível para BI
- [ ] Conheço trade-offs vs Data Vault e 3FN
- [ ] Documento dicionário de métricas com o negócio

---

## Próximos passos na trilha

1. Implemente no [Data Warehouse](../data-warehouse/README.md)
2. Transforme com [dbt](../dbt/README.md) e [SQL](../sql/README.md)
3. Camadas do lake em [Lakehouse](../lakehouse/README.md)
4. Pipelines em [ETL](../etl/README.md)

> 💡 A trilha [DataEngineer.help](https://dataengineer.help) cobre modelagem dimensional e marts na prática com SQL e dbt.

---

[← Voltar ao Awesome Data Engineering BR](../../README.md)
