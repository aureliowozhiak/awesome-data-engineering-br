# Projetos de Engenharia de Dados para Portfólio

> Mais de 30 ideias de projetos para praticar **engenharia de dados**, construir portfólio e impressionar recrutadores no mercado brasileiro.

[← Índice](../../README.md) · [Roadmap](../roadmaps/README.md) · [SQL](../sql/README.md) · [Python](../python/README.md)

---

## Por que projetos importam?

Recrutadores de **data engineering** valorizam portfólio com código real no GitHub. Projetos demonstram que você sabe construir **pipelines de dados** end-to-end — não apenas completar cursos.

---

## Projetos iniciantes (nível júnior)

| # | Projeto | Stack sugerida |
|---|---------|----------------|
| 1 | ETL de CSV para PostgreSQL | Python, Pandas, SQLAlchemy |
| 2 | Pipeline de API REST para banco | Python, requests, PostgreSQL |
| 3 | Dashboard de qualidade de dados | SQL, Python, Grafana |
| 4 | Web scraper agendado | Python, BeautifulSoup, cron |
| 5 | Análise exploratória automatizada | Pandas, Jupyter, Markdown reports |
| 6 | Backup automatizado de banco | Bash, pg_dump, S3 |
| 7 | CLI para validar schemas CSV | Python, Click, Pandera |
| 8 | Docker Compose: Postgres + Adminer | Docker, SQL |
| 9 | GitHub Actions para rodar testes SQL | Git, CI/CD |
| 10 | Dimensional model do zero (Northwind) | SQL, diagrama ER |

---

## Projetos intermediários

| # | Projeto | Stack sugerida |
|---|---------|----------------|
| 11 | Pipeline completo com Airflow | Airflow, Python, PostgreSQL |
| 12 | Projeto dbt com 3 camadas | dbt, BigQuery ou DuckDB |
| 13 | Data lake local com MinIO | Docker, S3 API, Parquet |
| 14 | CDC com Debezium + Kafka | Kafka, Docker, PostgreSQL |
| 15 | ETL serverless AWS | Lambda, S3, Glue, Athena |
| 16 | Pipeline GCP com Cloud Functions | GCS, BigQuery, Pub/Sub |
| 17 | API de dados com FastAPI | FastAPI, PostgreSQL, Docker |
| 18 | Monitoramento de freshness | Airflow, Slack alerts, SQL |
| 19 | Great Expectations suite | Python, GE, PostgreSQL |
| 20 | Terraform: data platform mínima | Terraform, AWS S3 + RDS |

---

## Projetos avançados

| # | Projeto | Stack sugerida |
|---|---------|----------------|
| 21 | Lakehouse com Delta Lake | Spark, Delta, S3/Databricks |
| 22 | Streaming Kafka → Spark → DW | Kafka, Spark Streaming, Snowflake |
| 23 | Plataforma medallion completa | S3, Spark, dbt, Airflow |
| 24 | Data mesh com domínios | dbt, múltiplos warehouses |
| 25 | Feature store simplificado | Spark, Redis, MLflow |
| 26 | Open table format comparison | Iceberg vs Delta vs Hudi |
| 27 | Real-time analytics com ClickHouse | Kafka, ClickHouse, Grafana |
| 28 | Multi-cloud abstraction layer | Python, adapters AWS/GCP |
| 29 | Data catalog com OpenMetadata | Docker, PostgreSQL, APIs |
| 30 | Pipeline com LGPD compliance | Anonimização, audit logs |
| 31 | Cost optimization dashboard | Cloud billing APIs, SQL |
| 32 | ML pipeline com feature engineering | Spark, Airflow, MLflow |
| 33 | Log aggregation platform | Kafka, Elasticsearch, Kibana |
| 34 | Reverse ETL prototype | dbt, Census/Hightouch pattern |
| 35 | IoT data pipeline simulado | MQTT, Kafka, TimescaleDB |

---

## Como apresentar no GitHub

- README com diagrama de arquitetura (Mermaid)
- Instruções claras de setup (`docker-compose up`)
- Dados de exemplo ou script de seed
- Testes automatizados
- Badges de CI/CD

---

[Desafios no README principal](../../README.md#desafios) · [Entrevistas](../interview/README.md)

> 💡 A seção **Projetos Práticos & Portfólio** da trilha [DataEngineer.help](https://dataengineer.help) inclui ETL de Kaggle, pipelines Airflow + BigQuery e Databricks end-to-end.

[← Voltar ao Awesome Data Engineering BR](../../README.md)
