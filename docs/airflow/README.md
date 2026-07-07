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

## Exemplo de DAG com TaskFlow API (Airflow 2.x)

```python
from airflow.decorators import dag, task
from datetime import datetime

@dag(
    schedule="0 6 * * 1-5",
    start_date=datetime(2025, 1, 1),
    catchup=False,
    tags=["etl", "vendas"],
)
def pipeline_vendas_diario():
    @task()
    def extrair():
        return [{"id": 1, "valor": 100}, {"id": 2, "valor": 200}]

    @task()
    def transformar(dados):
        return [d for d in dados if d["valor"] > 0]

    @task()
    def carregar(dados):
        print(f"Carregando {len(dados)} registros...")

    carregar(transformar(extrair()))

pipeline_vendas_diario()
```

---

## Serviços managed de Airflow

| Serviço | Cloud | Quando usar |
|---------|-------|-------------|
| **MWAA** | AWS | Stack AWS, integração S3/Glue/Redshift |
| **Cloud Composer** | GCP | Stack GCP, BigQuery nativo |
| **Astronomer** | Multi-cloud | Time quer suporte enterprise |
| **Self-hosted** | Qualquer | Controle total, custo menor em escala |

---

## Operadores mais usados em DE

| Operator | Uso |
|----------|-----|
| `PythonOperator` | Lógica customizada em Python |
| `BashOperator` | Scripts shell, CLI tools |
| `SQLOperator` | Executar SQL no warehouse |
| `S3ToRedshiftOperator` | Carga S3 → Redshift |
| `DatabricksSubmitRunOperator` | Disparar job Spark |
| `DbtCloudRunJobOperator` | Executar modelos dbt |

---

## Troubleshooting comum

| Problema | Causa provável | Solução |
|----------|----------------|---------|
| DAG não aparece | Erro de sintaxe no import | `airflow dags list-import-errors` |
| Task presa em `queued` | Pool/concurrency esgotado | Ajustar pools ou `parallelism` |
| SLA miss frequente | Task lenta ou dependência externa | Otimizar task ou aumentar timeout |
| XCom muito grande | Passando DataFrame via XCom | Usar staging em S3/GCS |
| Backfill demorado | `catchup=True` em DAG antigo | `catchup=False` + backfill manual |

---

## Checklist de produção

- [ ] Todas as tasks são idempotentes (re-run seguro)
- [ ] `catchup=False` em DAGs que não precisam de histórico
- [ ] Conexões e variáveis no Airflow Connections/Variables (não no código)
- [ ] Alertas configurados (email, Slack, PagerDuty) para falhas
- [ ] DAGs testados no CI com `DagBag`
- [ ] Pools definidos para tasks que consomem recursos limitados
- [ ] Documentação da DAG (`doc_md`) preenchida

---

## Ferramentas online do repositório

- [Explicador de Cron](../../tools/cron-expression-explainer/) — traduz `schedule_interval` e mostra próximas execuções

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
