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

[Snowflake](../../README.md#snowflake) · [BigQuery](../../README.md#bigquery) · [Projetos](../projects/README.md)

> 💡 Os módulos **dbt – Fundamentos** e **dbt Avançado** estão previstos na trilha [DataEngineer.help](https://dataengineer.help).

[← Voltar ao Awesome Data Engineering BR](../../README.md)
