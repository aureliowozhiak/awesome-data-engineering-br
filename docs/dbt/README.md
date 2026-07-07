# dbt — Transformação de Dados com SQL e Engenharia de Software

> **dbt** (data build tool) revolucionou o **ELT** moderno. Aprenda a versionar transformações SQL, testar qualidade e documentar seu **data warehouse**.

[← Índice](../../README.md) · [SQL](../sql/README.md) · [Airflow](../airflow/README.md) · [Cloud](../cloud/README.md)

---

## O que é dbt?

**dbt** é uma ferramenta que permite transformar dados diretamente no **data warehouse** usando SQL puro, com versionamento Git, testes, documentação e lineage automático. É o coração do padrão **ELT** em empresas que usam **Snowflake**, **BigQuery**, **Databricks** e **Redshift**.

### Por que aprender dbt?

- Padrão de mercado para transformações em **cloud**
- Aplica engenharia de software a dados: CI/CD, code review, testes
- Integra com **Airflow**, **Databricks**, Prefect, Dagster
- Comunidade enorme e pacotes reutilizáveis (dbt Hub)

### Quando usar

| dbt | Alternativa |
|-----|-------------|
| Transformações SQL no warehouse | Spark para volume extremo |
| Camadas staging → intermediate → mart | Stored procedures legadas |
| Documentação e testes de dados | Great Expectations standalone |

**Importância:** ⭐⭐⭐⭐⭐

---

## Conceitos dbt

- **Models** — SELECT statements versionados
- **Sources** — tabelas upstream declaradas
- **Tests** — unique, not_null, relationships
- **Macros** — Jinja reutilizável
- **Snapshots** — SCD Type 2
- **Seeds** — CSVs versionados

---

## Recursos

### Documentação
- [dbt Docs](https://docs.getdbt.com/)
- [dbt Learn](https://learn.getdbt.com/) — gratuito

### Tutoriais
- dbt Fundamentals (dbt Learn)
- [dbt Labs Blog](https://www.getdbt.com/blog)

### Livros
- *Analytics Engineering with dbt* — Randy Abernathy

### Projetos
- Projeto completo com staging, intermediate e marts
- Implementar métricas com semantic layer
- CI/CD com dbt Cloud ou GitHub Actions

---

## Estrutura de projeto dbt

```
meu_projeto_dbt/
├── dbt_project.yml
├── models/
│   ├── staging/          # 1:1 com fonte, renomear e tipar
│   │   └── stg_orders.sql
│   ├── intermediate/     # joins e lógica reutilizável
│   │   └── int_orders_enriched.sql
│   └── marts/            # tabelas finais para BI
│       └── fct_orders.sql
├── tests/
├── seeds/
├── macros/
├── snapshots/
└── packages.yml
```

---

## Exemplos de modelos e testes

### Model (`models/marts/fct_orders.sql`)

```sql
{{ config(materialized='table') }}

SELECT
    o.order_id,
    o.customer_id,
    c.customer_name,
    o.order_date,
    o.total_amount
FROM {{ ref('int_orders_enriched') }} o
LEFT JOIN {{ ref('dim_customers') }} c USING (customer_id)
```

### Schema YAML com testes (`models/marts/schema.yml`)

```yaml
version: 2
models:
  - name: fct_orders
    description: "Fato de pedidos para BI"
    columns:
      - name: order_id
        tests: [unique, not_null]
      - name: customer_id
        tests:
          - not_null
          - relationships:
              to: ref('dim_customers')
              field: customer_id
      - name: total_amount
        tests:
          - not_null
          - dbt_expectations.expect_column_values_to_be_between:
              min_value: 0
```

---

## Workflow de desenvolvimento

```
1. dbt run --select stg_*        # rodar staging local
2. dbt test                      # validar testes
3. git commit + PR               # code review
4. CI: dbt build (em sandbox)    # validação automática
5. merge → dbt run (prod)        # deploy em produção
6. dbt docs generate && serve    # documentação atualizada
```

---

## Pacotes dbt populares

| Pacote | Uso |
|--------|-----|
| `dbt-labs/dbt_utils` | Macros utilitárias (surrogate_key, pivot, etc.) |
| `calogica/dbt_expectations` | Testes avançados de qualidade |
| `dbt-labs/codegen` | Gerar YAML/schema automaticamente |
| `dbt-labs/audit_helper` | Comparar tabelas entre ambientes |

---

## Anti-padrões comuns

- Modelos com 500+ linhas sem CTEs — quebre em intermediate models
- `SELECT *` em models de produção
- Testes apenas `not_null` sem `unique` e `relationships`
- Não documentar colunas no `schema.yml`
- Rodar `dbt run` em produção sem CI/CD

---

## Checklist de domínio dbt

- [ ] Estruturo projeto em staging → intermediate → marts
- [ ] Escrevo testes (unique, not_null, relationships) para colunas críticas
- [ ] Uso `{{ ref() }}` e `{{ source() }}` corretamente
- [ ] Documento modelos e colunas no schema.yml
- [ ] Configuro materializations adequadas (view, table, incremental)
- [ ] Integro dbt no CI/CD (GitHub Actions ou dbt Cloud)
- [ ] Gero e publico documentação com `dbt docs`

---

[Snowflake](../../README.md#snowflake) · [BigQuery](../../README.md#bigquery) · [Projetos](../projects/README.md)

> 💡 Os módulos **dbt – Fundamentos** e **dbt Avançado** estão previstos na trilha [DataEngineer.help](https://dataengineer.help).

[← Voltar ao Awesome Data Engineering BR](../../README.md)
