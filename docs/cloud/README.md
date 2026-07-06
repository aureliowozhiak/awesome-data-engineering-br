# Cloud para Engenharia de Dados — AWS, Azure e GCP

> Guia completo de **cloud** para **engenheiros de dados**: serviços de storage, compute, orquestração e **data warehouse** nas três principais plataformas.

[← Índice](../../README.md) · [Airflow](../airflow/README.md) · [Spark](../spark/README.md) · [dbt](../dbt/README.md)

---

## Por que cloud é obrigatório na engenharia de dados?

Praticamente toda vaga de **engenheiro de dados** no Brasil exige experiência com pelo menos uma plataforma de **cloud**. Os serviços managed reduzem operação de infraestrutura e aceleram a entrega de **pipelines de dados**.

---

## Comparativo das três clouds

| Serviço | AWS | Azure | GCP |
|---------|-----|-------|-----|
| Object Storage | S3 | Blob Storage | Cloud Storage |
| Data Warehouse | Redshift | Synapse | BigQuery |
| Spark Managed | EMR | HDInsight | Dataproc |
| Orquestração | MWAA | Data Factory | Cloud Composer |
| Streaming | Kinesis / MSK | Event Hubs | Pub/Sub |
| Catálogo | Glue | Purview | Data Catalog |
| IaC | CloudFormation | ARM / Bicep | Deployment Manager |

---

## AWS para Data Engineering

**Importância:** ⭐⭐⭐⭐⭐ (maior adoção no Brasil corporativo)

### Serviços essenciais
- **S3** — data lake
- **Glue** — ETL serverless e catálogo
- **Redshift** — data warehouse
- **EMR** — Spark/Hive managed
- **MWAA** — Airflow managed
- **Lambda** — funções serverless
- **Athena** — SQL sobre S3
- **Kinesis** — streaming

### Certificações
- AWS Certified Data Engineer – Associate
- AWS Solutions Architect (complementar)

[Detalhes no README principal → AWS](../../README.md#aws)

---

## Azure para Data Engineering

**Importância:** ⭐⭐⭐⭐ (forte em enterprise e governo)

### Serviços essenciais
- **Azure Data Lake Storage Gen2**
- **Azure Synapse Analytics**
- **Azure Data Factory**
- **Azure Databricks**
- **Event Hubs**
- **Azure Purview**

[Detalhes → Azure](../../README.md#azure)

---

## GCP para Data Engineering

**Importância:** ⭐⭐⭐⭐ (BigQuery é referência em DW serverless)

### Serviços essenciais
- **BigQuery** — DW serverless
- **Cloud Storage** — data lake
- **Dataflow** — Beam/Spark streaming
- **Cloud Composer** — Airflow
- **Pub/Sub** — mensageria
- **Dataproc** — Spark managed

[Detalhes → GCP](../../README.md#gcp)

---

## Terraform e IaC

Infraestrutura como código é essencial para ambientes reproduzíveis. Veja [Terraform no guia principal](../../README.md#terraform).

---

## Recursos

- [AWS Skill Builder](https://skillbuilder.aws/)
- [Microsoft Learn — Azure Data](https://learn.microsoft.com/azure/data/)
- [Google Cloud Skills Boost](https://www.cloudskillsboost.google/)

[Certificações](../interview/README.md#certificacoes) · [Projetos cloud](../projects/README.md)

> 💡 O módulo **Google Cloud Platform para Dados** está previsto na trilha [DataEngineer.help](https://dataengineer.help).

[← Voltar ao Awesome Data Engineering BR](../../README.md)
