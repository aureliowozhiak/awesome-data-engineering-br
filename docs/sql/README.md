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

## Próximos passos na trilha

1. Aprofunde em [PostgreSQL](../resources/README.md#postgresql) para bancos transacionais
2. Aprenda [dbt](../dbt/README.md) para transformações versionadas
3. Pratique perguntas de [entrevista](../interview/README.md#sql)
4. Veja [projetos](../projects/README.md) que exigem SQL avançado

> 💡 Os módulos **SQL Essencial** e **SQL Avançado** da trilha [DataEngineer.help](https://dataengineer.help) cobrem esse conteúdo em profundidade.

---

[← Voltar ao Awesome Data Engineering BR](../../README.md)
