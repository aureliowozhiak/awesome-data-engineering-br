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

## Padrões de arquitetura por cloud

### AWS — Lakehouse clássico

```
S3 (raw) → Glue/EMR (transform) → S3 (Parquet/Delta) → Athena/Redshift → QuickSight
                ↑
            MWAA (Airflow)
```

### GCP — Analytics serverless

```
Cloud Storage → Dataflow/BigQuery (ELT) → BigQuery (DW) → Looker/Metabase
                    ↑
              Cloud Composer (Airflow)
```

### Azure — Enterprise

```
ADLS Gen2 → Databricks/Synapse → Synapse SQL Pool → Power BI
                ↑
          Data Factory / Airflow
```

---

## Otimização de custos

| Prática | Economia estimada | Cloud |
|---------|-------------------|-------|
| Particionar tabelas por data | 30–70% em queries | Todas |
| Usar storage classes (S3 IA, GCS Nearline) | 40–60% em dados frios | AWS, GCP |
| Auto-suspend em warehouses | 50%+ em DW ocioso | Snowflake, Redshift |
| Spot/Preemptible instances para Spark | 60–80% em batch | AWS, GCP, Azure |
| Comprimir em Parquet + Snappy/ZSTD | 70–90% em storage | Todas |
| Reserved instances para workloads estáveis | 30–50% | Todas |

---

## IAM e segurança — boas práticas

- **Princípio do menor privilégio** — roles específicas por pipeline (não admin)
- **Separação de ambientes** — contas/projects distintos para dev/staging/prod
- **Secrets Manager** — nunca credenciais em código ou variáveis plain text
- **Encryption at rest** — S3 SSE, GCS CMEK, Azure Storage Encryption
- **VPC/Private Link** — tráfego de dados sem exposição pública
- **Audit logs** — CloudTrail (AWS), Cloud Audit Logs (GCP), Activity Log (Azure)

---

## Sandboxes e free tiers para praticar

| Cloud | Recurso gratuito | Limite |
|-------|------------------|--------|
| AWS | Free Tier (12 meses) | S3, Lambda, RDS limitados |
| AWS | Skill Builder labs | Labs hands-on gratuitos |
| GCP | BigQuery Sandbox | 1 TB queries/mês grátis |
| GCP | $300 créditos (90 dias) | Novos usuários |
| Azure | Free Account | $200 créditos (30 dias) |
| Snowflake | Free Trial | 30 dias, warehouse XS |
| Databricks | Community Edition | Cluster single-node grátis |

---

## Checklist de domínio Cloud

- [ ] Conheço serviços de storage, compute e DW da cloud escolhida
- [ ] Sei provisionar recursos com Terraform ou console
- [ ] Configuro IAM com least privilege
- [ ] Monitoro custos (Cost Explorer, Billing, Cost Management)
- [ ] Entendo diferença entre regiões e zonas de disponibilidade
- [ ] Implemento backup e disaster recovery para dados críticos

---

## Recursos

- [AWS Skill Builder](https://skillbuilder.aws/)
- [Microsoft Learn — Azure Data](https://learn.microsoft.com/azure/data/)
- [Google Cloud Skills Boost](https://www.cloudskillsboost.google/)

[Certificações](../interview/README.md#certificacoes) · [Projetos cloud](../projects/README.md)

> 💡 O módulo **Google Cloud Platform para Dados** está previsto na trilha [DataEngineer.help](https://dataengineer.help).

[← Voltar ao Awesome Data Engineering BR](../../README.md)
