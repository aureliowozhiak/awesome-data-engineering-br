# Apache Airflow — Orquestração de Pipelines de Dados

> Aprenda **Apache Airflow** para orquestrar **pipelines de dados**, agendar jobs **ETL/ELT** e monitorar workflows em produção — habilidade essencial para qualquer **engenheiro de dados** no Brasil.

[← Índice principal](../../README.md) · [Python](../python/README.md) · [Spark](../spark/README.md) · [dbt](../dbt/README.md) · [Cloud](../cloud/README.md)

---

## O que é Apache Airflow?

**Apache Airflow** é uma plataforma open source para criar, agendar e monitorar workflows como **DAGs** (Directed Acyclic Graphs). É o padrão de mercado para orquestração de **pipelines de dados** em empresas que usam **Python**, **SQL** e ferramentas de **cloud**.

### Por que aprender Airflow?

- Adotado por Nubank, iFood, Magalu, startups e bancos no Brasil
- Integra com **AWS** (MWAA), **GCP** (Cloud Composer), **Azure**
- Ecossistema rico de operadores: S3, BigQuery, Snowflake, Spark, dbt
- Interface web para monitoramento e reprocessamento

### Quando usar

| Use Airflow | Considere alternativas |
|-------------|------------------------|
| Pipelines batch diários/horários | **Prefect**, **Dagster** para workflows modernos |
| Orquestração centralizada | **Step Functions** para serverless AWS |
| Equipes com cultura Python | **dbt Cloud** só para transformações SQL |

**Importância:** ⭐⭐⭐⭐⭐

---

## Conceitos fundamentais

| Conceito | Descrição |
|----------|-----------|
| DAG | Grafo de tarefas sem ciclos |
| Operator | Unidade de trabalho (PythonOperator, BashOperator) |
| Task | Instância de um operator no DAG |
| Scheduler | Dispara DAGs conforme cron |
| XCom | Troca de dados entre tasks |
| Connection | Credenciais de bancos e APIs |

---

## Recursos

### Documentação
- [Apache Airflow Docs](https://airflow.apache.org/docs/)
- [Astronomer Guides](https://www.astronomer.io/guides/)

### Tutoriais
- [Official Airflow Tutorial](https://airflow.apache.org/docs/apache-airflow/stable/tutorial/fundamentals.html)
- [Marc Lamberti — YouTube](https://www.youtube.com/c/MarcLamberti)

### Cursos
- DataCamp — Introduction to Airflow
- Udemy — Apache Airflow: The Hands-On Guide

### Livros
- *Data Pipelines with Apache Airflow* — Bas Harenslak & Julian de Ruiter

### Projetos
- Pipeline S3 → transformação Python → PostgreSQL
- DAG que executa modelos **dbt** diariamente
- Monitoramento de freshness com SLA alerts

---

## Boas práticas

> ⚠️ **Dica:** Nunca passe grandes volumes de dados via XCom. Use staging em S3/GCS.

- Idempotência em todas as tasks
- `catchup=False` para DAGs históricos
- Pools e priorities para recursos limitados
- Testes com `pytest-airflow` ou `dagbag`

---

[Entrevistas Airflow](../interview/README.md#airflow) · [Projetos](../projects/README.md) · [CI/CD](../resources/README.md#cicd)

> 💡 O módulo **Apache Airflow do Zero** está previsto na trilha [DataEngineer.help](https://dataengineer.help).

[← Voltar ao Awesome Data Engineering BR](../../README.md)
