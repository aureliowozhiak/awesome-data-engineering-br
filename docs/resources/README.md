# Recursos Complementares — Engenharia de Dados

> Git, Linux, Docker, PostgreSQL, Terraform, CI/CD, formatos de arquivo e ferramentas que todo **engenheiro de dados** precisa conhecer.

[← Índice](../../README.md) · [SQL](../sql/README.md) · [Python](../python/README.md) · [Cloud](../cloud/README.md)

---

## Git {#git}

**Importância:** ⭐⭐⭐⭐⭐

Versionamento é obrigatório para **pipelines de dados** modernos. Todo projeto dbt, Airflow e infraestrutura usa Git.

- [Pro Git Book](https://git-scm.com/book/pt-br/v2) — gratuito em português
- [GitHub Skills](https://skills.github.com/) — tutoriais interativos
- [Conventional Commits](https://www.conventionalcommits.org/) — padrão de mensagens
- **Guia completo:** [Git & GitHub para DE](../git/README.md)

> 💡 O módulo **Git & GitHub para Engenheiros de Dados** está previsto na trilha [DataEngineer.help](https://dataengineer.help).

---

## Linux {#linux}

**Importância:** ⭐⭐⭐⭐

Servidores de **data engineering** rodam Linux. Terminal, SSH, cron e permissões são do dia a dia.

- [Linux Journey](https://linuxjourney.com/) — gratuito
- Comandos essenciais: `grep`, `awk`, `sed`, `curl`, `jq`, `htop`
- Gerenciamento de processos e systemd
- **Guia completo:** [Linux/shell para DE](../linux/README.md)

> 💡 O módulo **Shell Script: Introdução e Automação de Tarefas** na trilha [DataEngineer.help](https://dataengineer.help) cobre automação no terminal.

---

## Docker {#docker}

**Importância:** ⭐⭐⭐⭐⭐

Containers padronizam ambientes de desenvolvimento e deploy de **Airflow**, **Spark**, bancos e ferramentas.

- [Docker Docs](https://docs.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/) — stacks locais
- Projeto: `docker-compose` com Postgres + Airflow + MinIO
- **Guia completo:** [Docker para engenharia de dados](../docker/README.md)

> 💡 O módulo **Docker e CI/CD para Dados** está previsto na trilha [DataEngineer.help](https://dataengineer.help).

---

## PostgreSQL {#postgresql}

**Importância:** ⭐⭐⭐⭐⭐

O **banco de dados** open source mais usado em **engenharia de dados** para cargas transacionais, staging e OLTP.

- [PostgreSQL Tutorial](https://www.postgresqltutorial.com/)
- Extensões: `pg_stat_statements`, `postgres_fdw`, TimescaleDB
- [Guia SQL](../sql/README.md)

---

## Terraform {#terraform}

**Importância:** ⭐⭐⭐⭐

Infraestrutura como código para **AWS**, **Azure** e **GCP**.

- [Terraform Docs](https://developer.hashicorp.com/terraform/docs)
- [Terraform AWS Examples](https://github.com/hashicorp/terraform-provider-aws/tree/main/examples)
- Projeto: S3 bucket + IAM + Glue catalog
- **Guia completo:** [Terraform IaC para dados](../terraform/README.md)

> 💡 O módulo **Infra como Código (Terraform + dbt Cloud)** está previsto na trilha [DataEngineer.help](https://dataengineer.help).

---

## CI/CD {#cicd}

**Importância:** ⭐⭐⭐⭐

Deploy automatizado de DAGs, modelos dbt e infraestrutura.

| Ferramenta | Uso |
|------------|-----|
| GitHub Actions | CI/CD mais popular em OSS |
| GitLab CI | Enterprise |
| Jenkins | Legado, ainda comum |
| ArgoCD | GitOps para Kubernetes |

- Testar DAGs com `dagbag` no CI
- `dbt build` em pull requests
- Terraform plan em PRs

---

## Formatos de arquivo

| Formato | Uso | Doc |
|---------|-----|-----|
| **Parquet** | Colunar, padrão de lake | [Parquet Docs](https://parquet.apache.org/docs/) |
| **Delta Lake** | ACID no lake | [Delta.io](https://delta.io/) |
| **Iceberg** | Table format aberto | [Iceberg Docs](https://iceberg.apache.org/) |
| **Avro** | Schema evolution, Kafka | [Avro Docs](https://avro.apache.org/docs/) |
| **ORC** | Hive/legacy | [ORC Docs](https://orc.apache.org/) |

> 💡 O módulo **Tabelas Delta e Camadas Bronze/Silver/Gold** da trilha [DataEngineer.help](https://dataengineer.help) aprofunda Delta Lake e arquitetura medallion.

---

## Ferramentas adicionais

| Ferramenta | Descrição | Importância |
|------------|-----------|-------------|
| **DuckDB** | OLAP in-process, ótimo para local | ⭐⭐⭐⭐ |
| **ClickHouse** | OLAP ultra-rápido | ⭐⭐⭐⭐ |
| **Apache Hive** | SQL sobre Hadoop, legado | ⭐⭐⭐ |
| **Great Expectations** | Data quality | ⭐⭐⭐⭐ |
| **OpenMetadata** | Data catalog | ⭐⭐⭐ |
| **Metabase / Superset** | BI open source | ⭐⭐⭐ |

---

## Comandos Linux essenciais para DE

```bash
# Explorar arquivos de log
grep "ERROR" /var/log/airflow/*.log | tail -20
awk -F',' '{print $1, $3}' dados.csv | head
jq '.results[0].name' resposta_api.json

# Monitorar recursos
htop                          # CPU e memória
df -h                         # espaço em disco
du -sh /data/lake/*           # tamanho por diretório

# Rede e APIs
curl -s https://api.exemplo.com/dados | jq .
ssh usuario@servidor-airflow

# Agendamento
crontab -e                    # editar cron jobs
crontab -l                    # listar cron jobs
```

---

## Docker Compose — stack local para DE

```yaml
# docker-compose.yml — ambiente mínimo para praticar
version: "3.8"
services:
  postgres:
    image: postgres:15
    environment:
      POSTGRES_DB: dados
      POSTGRES_USER: de
      POSTGRES_PASSWORD: de123
    ports: ["5432:5432"]
    volumes: ["pgdata:/var/lib/postgresql/data"]

  minio:
    image: minio/minio
    command: server /data --console-address ":9001"
    ports: ["9000:9000", "9001:9001"]
    environment:
      MINIO_ROOT_USER: minio
      MINIO_ROOT_PASSWORD: minio123

volumes:
  pgdata:
```

Suba com `docker-compose up -d` e pratique pipelines contra Postgres + MinIO (S3-compatible).

---

## Data Quality — ferramentas e práticas

| Ferramenta | Tipo | Quando usar |
|------------|------|-------------|
| **dbt tests** | Declarativo (SQL) | Testes em transformações do warehouse |
| **Great Expectations** | Programático (Python) | Validação em pipelines ETL |
| **Soda Core** | YAML-based | Checks em data contracts |
| **CSV Profiler** (ferramenta do repo) | Browser | Exploração rápida de CSVs |

### Checks essenciais de qualidade

- **Completude** — % de nulos em colunas críticas
- **Unicidade** — chaves primárias sem duplicatas
- **Validade** — tipos, ranges, formatos (email, CPF, data)
- **Consistência** — mesma métrica em fontes diferentes
- **Freshness** — dados atualizados dentro do SLA

---

## Ferramentas online do repositório

Hub com ferramentas que rodam 100% no navegador — úteis no dia a dia do engenheiro de dados:

| Ferramenta | Categoria | Link |
|-----------|-----------|------|
| SQL Formatter | SQL | [tools/sql-formatter/](../../tools/sql-formatter/) |
| JSON Formatter | JSON | [tools/json-formatter/](../../tools/json-formatter/) |
| CSV Profiler | Data Quality | [tools/csv-profiler/](../../tools/csv-profiler/) |
| Parquet Viewer | Parquet | [tools/parquet-viewer/](../../tools/parquet-viewer/) |
| Explicador de Cron | Airflow | [tools/cron-expression-explainer/](../../tools/cron-expression-explainer/) |
| JSON↔CSV, UUID, Hash, Base64 | Utilitários | [tools/](../../tools/) |

👉 [Hub completo de ferramentas](../../tools/index.html)

---

## Cheatsheets

- [PostgreSQL Cheat Sheet](https://www.postgresqltutorial.com/postgresql-cheat-sheet/)
- [Docker Cheat Sheet](https://docs.docker.com/get-started/docker_cheatsheet.pdf)
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
- [dbt Cheat Sheet](https://docs.getdbt.com/guides/dbt-cheatsheet)
- [Spark Cheat Sheet](https://spark.apache.org/docs/latest/api/python/quickstart.html)

Veja também [Cheatsheets no README principal](../../README.md#cheatsheets).

---

## Malha de links

- [SQL](../sql/README.md) · [Python](../python/README.md) · [Airflow](../airflow/README.md)
- [Spark](../spark/README.md) · [Kafka](../kafka/README.md) · [dbt](../dbt/README.md)
- [Cloud](../cloud/README.md) · [Projetos](../projects/README.md) · [Entrevistas](../interview/README.md)

[← Voltar ao Awesome Data Engineering BR](../../README.md)
