# Data Warehouse — OLAP e Warehouses na Nuvem

> Entenda **data warehouse**, **OLAP** e warehouses modernos (**BigQuery**, **Snowflake**, **Redshift**, **Databricks SQL**) para **engenharia de dados**.

[← Índice](../../README.md) · [Data Modeling](../data-modeling/README.md) · [SQL](../sql/README.md) · [dbt](../dbt/README.md) · [Cloud](../cloud/README.md) · [Lakehouse](../lakehouse/README.md)

---

## O que é um data warehouse?

Um **data warehouse (DW)** é um repositório analítico otimizado para consultas **OLAP** — agregações, histórico e BI — separado dos sistemas **OLTP** de produção. Warehouses modernos na **nuvem** separam storage e compute e escalam sob demanda.

Um **engenheiro de dados** trabalha no DW para:

- Modelar fatos/dimensões e marts
- Orquestrar ELT com SQL e dbt
- Otimizar custo (slots, warehouses, clustering)
- Garantir governança, acesso e qualidade

**Importância:** ⭐⭐⭐⭐⭐

---

## O que você precisa dominar

| Tópico | Nível | Descrição |
|--------|-------|-----------|
| OLTP vs OLAP | ⭐⭐⭐⭐⭐ | Cargas e padrões distintos |
| Arquitetura DW | ⭐⭐⭐⭐⭐ | Staging → marts |
| Warehouses cloud | ⭐⭐⭐⭐⭐ | BigQuery, Snowflake, Redshift |
| Particionamento / clustering | ⭐⭐⭐⭐⭐ | Performance e custo |
| Materialized views | ⭐⭐⭐⭐ | Agregados frequentes |
| Governança e IAM | ⭐⭐⭐⭐ | Roles, row-level security |
| Integração lake/lakehouse | ⭐⭐⭐⭐ | External tables, Delta/Iceberg |

---

## Quando usar DW vs lake vs OLTP

| Cenário | Escolha |
|---------|---------|
| BI, dashboards, SQL analítico | **Data warehouse** |
| Raw multi-formato, science, baixo custo storage | **Data lake** / lakehouse |
| Transações do app (pedido, pagamento) | **OLTP** (Postgres etc.) |
| Ambos analitico + arquivos abertos | **Lakehouse** |
| Latência sub-segundo operacional | Serving DB / cache (não DW clássico) |

---

## Recursos recomendados

### Documentação oficial
- [BigQuery Docs](https://cloud.google.com/bigquery/docs)
- [Snowflake Docs](https://docs.snowflake.com/)
- [Amazon Redshift](https://docs.aws.amazon.com/redshift/)
- [Databricks SQL](https://docs.databricks.com/sql/index.html)

### Cursos e prática
- Sandboxes gratuitos / trials dos provedores
- [Guia SQL](../sql/README.md) + [dbt](../dbt/README.md)

### Livros
- *The Data Warehouse Toolkit* — Kimball
- *Fundamentals of Data Engineering* — Reis & Housley

---

## Exemplos práticos

### Camadas típicas no DW

```text
Landing / Staging  →  Intermediate (limpo)  →  Marts (fct_ / dim_)
     ELT load              dbt models              BI / API
```

### Partição por data (BigQuery-style)

```sql
CREATE TABLE analytics.events
PARTITION BY DATE(event_ts)
AS
SELECT * FROM staging.events;
```

### Query com partition pruning

```sql
SELECT
  user_id,
  COUNT(*) AS events
FROM analytics.events
WHERE event_ts >= TIMESTAMP '2025-01-01'
  AND event_ts <  TIMESTAMP '2025-02-01'
GROUP BY user_id;
```

### Comparativo rápido de cloud DWs

| Plataforma | Força | Atenção |
|------------|-------|---------|
| **BigQuery** | Serverless, SQL padrão | Custo por bytes escaneados |
| **Snowflake** | Separação compute, time travel | Warehouses idle / créditos |
| **Redshift** | Ecossistema AWS | Dimensionamento de nós/RA3 |
| **Databricks SQL** | Lakehouse unificado | Governança Unity Catalog |

---

## Padrões de uso

| Padrão | Quando usar | Exemplo |
|--------|-------------|---------|
| **ELT** | Cloud DW | Load raw → dbt transform |
| **Incremental models** | Tabelas grandes | Filtro `updated_at` |
| **Clustering** | Filtros frequentes | cluster por `customer_id` |
| **Views materializadas** | Agregados quentes | MV de vendas diárias |
| **Clone / time travel** | Dev e auditoria | Snowflake clone, BQ snapshots |

---

## Anti-padrões comuns

- **`SELECT *` em tabelas enormes** sem filtro de partição
- **Misturar OLTP e OLAP** no mesmo banco sob carga
- **Sem controle de custo** (slots/warehouses sempre ligados)
- **Marts sem dono** e métricas conflitantes
- **Copiar modelo 3FN do OLTP** direto para BI

---

## Checklist de domínio Data Warehouse

- [ ] Explico OLTP vs OLAP com exemplos
- [ ] Modelo staging → intermediate → marts
- [ ] Uso partições e clustering conscientemente
- [ ] Escrevo SQL eficiente no dialeto do DW
- [ ] Orquestro ELT com dbt/Airflow
- [ ] Monitoro custo e freshness
- [ ] Conheço ao menos um DW cloud em profundidade

---

## Próximos passos na trilha

1. Modele com [Data Modeling](../data-modeling/README.md)
2. Transforme com [dbt](../dbt/README.md) e [SQL](../sql/README.md)
3. Compare com [Lakehouse](../lakehouse/README.md)
4. Infra em [Cloud](../cloud/README.md) e [Terraform](../terraform/README.md)

> 💡 A trilha [DataEngineer.help](https://dataengineer.help) aprofunda SQL analítico e warehouses modernos na prática.

---

[← Voltar ao Awesome Data Engineering BR](../../README.md)
