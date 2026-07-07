# SQL para Engenharia de Dados — Guia Completo em Português

> Domine **SQL** para construir **pipelines de dados**, modelar **data warehouses** e resolver problemas reais de **engenharia de dados** no Brasil.

[← Índice principal](../../README.md) · [Python](../python/README.md) · [PostgreSQL](../resources/README.md#postgresql) · [dbt](../dbt/README.md) · [Entrevistas](../interview/README.md)

---

## Por que SQL é a habilidade nº 1 do engenheiro de dados?

**SQL** (Structured Query Language) é a linguagem universal para consultar, transformar e governar dados em **bancos de dados** relacionais e em praticamente todo **data warehouse** moderno — de **PostgreSQL** a **BigQuery**, **Snowflake** e **Databricks**. Se você quer **aprender engenharia de dados**, comece pelo SQL.

Um **engenheiro de dados** usa SQL diariamente para:

- Escrever transformações em camadas bronze, silver e gold
- Criar views materializadas e tabelas agregadas
- Validar qualidade de dados em pipelines **ETL** e **ELT**
- Otimizar queries em ambientes de **cloud** (AWS, Azure, GCP)

---

## O que você precisa dominar

| Tópico | Nível | Descrição |
|--------|-------|-----------|
| SELECT, WHERE, JOINs | ⭐⭐⭐⭐⭐ | Base de toda consulta analítica |
| Window Functions | ⭐⭐⭐⭐⭐ | Rankings, running totals, deduplicação |
| CTEs e subqueries | ⭐⭐⭐⭐ | Código legível e manutenível |
| Agregações e GROUP BY | ⭐⭐⭐⭐⭐ | Métricas de negócio |
| Índices e EXPLAIN | ⭐⭐⭐⭐ | Performance em produção |
| DDL e DML | ⭐⭐⭐⭐ | Criação e manutenção de schemas |
| Stored Procedures | ⭐⭐⭐ | Legado e bancos corporativos |

---

## Quando usar SQL vs outras ferramentas

| Cenário | Ferramenta recomendada |
|---------|------------------------|
| Transformações em DW na nuvem | SQL + **dbt** |
| Processamento massivo distribuído | **Apache Spark** (PySpark SQL) |
| Banco transacional | **PostgreSQL**, MySQL |
| Análise ad hoc rápida | **DuckDB**, BigQuery |
| Streaming em tempo real | **Kafka** + Flink/KsqlDB |

---

## Recursos recomendados

### Documentação oficial
- [PostgreSQL Docs](https://www.postgresql.org/docs/)
- [BigQuery SQL Reference](https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax)
- [Snowflake SQL Reference](https://docs.snowflake.com/en/sql-reference)

### Cursos gratuitos
- [SQLBolt](https://sqlbolt.com/) — interativo, do básico ao avançado
- [Mode SQL Tutorial](https://mode.com/sql-tutorial/)
- [Select Star SQL](https://selectstarsql.com/) — didático e gratuito

### Livros
- *SQL for Data Analysis* — Cathy Tanimura
- *Learning SQL* — Alan Beaulieu
- *SQL Performance Explained* — Markus Winand

### Projetos práticos
- Monte um **data warehouse** com dimensões e fatos a partir de CSVs
- Reproduza o modelo Northwind ou Chinook com queries analíticas
- Implemente SCD Type 2 em SQL puro

---

## Exemplos práticos de SQL

### Window function — ranking e deduplicação

```sql
-- Top 3 pedidos por cliente (deduplica mantendo o mais recente)
WITH ranked AS (
  SELECT
    customer_id,
    order_id,
    order_date,
    total,
    ROW_NUMBER() OVER (
      PARTITION BY customer_id
      ORDER BY order_date DESC
    ) AS rn
  FROM orders
)
SELECT customer_id, order_id, order_date, total
FROM ranked
WHERE rn = 1;
```

### CTE — pipeline legível em camadas

```sql
WITH raw_events AS (
  SELECT * FROM staging.events WHERE event_date = CURRENT_DATE - 1
),
cleaned AS (
  SELECT
    user_id,
    event_type,
    event_ts,
    COALESCE(amount, 0) AS amount
  FROM raw_events
  WHERE user_id IS NOT NULL
),
daily_metrics AS (
  SELECT
    user_id,
    COUNT(*) AS event_count,
    SUM(amount) AS total_amount
  FROM cleaned
  GROUP BY user_id
)
SELECT * FROM daily_metrics;
```

### SCD Type 2 — dimensão com histórico

```sql
-- Colunas típicas: valid_from, valid_to, is_current
UPDATE dim_customer
SET valid_to = CURRENT_DATE - 1, is_current = FALSE
WHERE customer_id = 123 AND is_current = TRUE;

INSERT INTO dim_customer (customer_id, name, city, valid_from, valid_to, is_current)
VALUES (123, 'Ana Silva', 'São Paulo', CURRENT_DATE, '9999-12-31', TRUE);
```

---

## Padrões SQL em data warehouses

| Padrão | Quando usar | Exemplo |
|--------|-------------|---------|
| **Staging → Intermediate → Mart** | ELT com dbt | `stg_orders` → `int_orders_enriched` → `fct_orders` |
| **Incremental** | Tabelas grandes com append | `WHERE updated_at > (SELECT MAX(updated_at) FROM target)` |
| **MERGE / UPSERT** | CDC e atualizações | `MERGE INTO target USING source ON ...` |
| **Materialized view** | Agregações frequentes | `CREATE MATERIALIZED VIEW mv_daily_sales AS ...` |
| **Partition pruning** | Tabelas particionadas por data | `WHERE event_date BETWEEN '2025-01-01' AND '2025-01-31'` |

---

## Anti-padrões comuns

- **`SELECT *`** em pipelines de produção — sempre liste colunas explicitamente
- **Subqueries correlacionadas** quando window functions resolvem melhor
- **JOIN sem filtro de partição** em tabelas particionadas por data
- **Funções em colunas indexadas** no WHERE (`WHERE YEAR(date) = 2025` → use range)
- **CTEs materializadas desnecessárias** — em alguns engines, CTEs não são otimizadas como esperado

---

## Checklist de domínio SQL

- [ ] Escrevo JOINs (INNER, LEFT, FULL) sem ambiguidade
- [ ] Uso window functions para ranking, running totals e deduplicação
- [ ] Organizo queries complexas com CTEs nomeadas
- [ ] Analiso execution plan com `EXPLAIN` / `EXPLAIN ANALYZE`
- [ ] Implemento SCD Type 2 em SQL puro
- [ ] Escrevo queries incrementais com filtro de watermark
- [ ] Conheço diferenças entre dialetos (PostgreSQL, BigQuery, Snowflake, Spark SQL)

---

## Ferramentas online do repositório

- [SQL Formatter](../../tools/sql-formatter/) — formata e identa queries SQL no navegador
- [CSV Profiler](../../tools/csv-profiler/) — perfil de qualidade antes de modelar no DW

---

## Próximos passos na trilha

1. Aprofunde em [PostgreSQL](../resources/README.md#postgresql) para bancos transacionais
2. Aprenda [dbt](../dbt/README.md) para transformações versionadas
3. Pratique perguntas de [entrevista](../interview/README.md#sql)
4. Veja [projetos](../projects/README.md) que exigem SQL avançado

> 💡 Os módulos **SQL Essencial** e **SQL Avançado** da trilha [DataEngineer.help](https://dataengineer.help) cobrem esse conteúdo em profundidade.

---

[← Voltar ao Awesome Data Engineering BR](../../README.md)
