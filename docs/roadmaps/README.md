# Roadmap de Engenharia de Dados — Trilha Completa 2025

> O **roadmap engenharia de dados** definitivo em português. Do zero ao profissional pronto para o mercado brasileiro de **data engineering**.

[← Índice principal](../../README.md) · [SQL](../sql/README.md) · [Python](../python/README.md) · [Projetos](../projects/README.md)

---

## Visão geral da trilha

Este roadmap foi desenhado para quem quer **aprender engenharia de dados** de forma estruturada, cobrindo fundamentos, ferramentas de produção e preparação para o mercado.

```mermaid
flowchart TD
    A[🎯 Fundamentos] --> B[📊 SQL]
    A --> C[🐍 Python]
    A --> D[📦 Git]
    A --> E[🐧 Linux]
    B --> F[🗄️ Modelagem de Dados]
    C --> F
    F --> G[🔄 ETL / ELT]
    G --> H[🌊 Airflow]
    G --> I[⚡ Spark]
    H --> J[☁️ Cloud]
    I --> J
    J --> K[🏢 Data Warehouse]
    J --> L[🏠 Lakehouse]
    K --> M[📡 Streaming / Kafka]
    L --> M
    M --> N[✅ Boas Práticas]
    N --> O[🛠️ Projetos]
    O --> P[📁 Portfólio]
    P --> Q[💼 Entrevistas]
```

---

## Fase 1 — Fundamentos (2–3 meses)

| Etapa | Tempo | Recursos |
|-------|-------|----------|
| SQL básico e avançado | 4–6 semanas | [Guia SQL](../sql/README.md) |
| Python para dados | 4–6 semanas | [Guia Python](../python/README.md) |
| Git e versionamento | 1–2 semanas | [README principal](../../README.md#git) |
| Linux e terminal | 2 semanas | [README principal](../../README.md#linux) |
| Docker básico | 1–2 semanas | [README principal](../../README.md#docker) |

**Objetivo:** Resolver problemas de manipulação de dados com SQL e Python, versionar código no GitHub.

---

## Fase 2 — Dados e Pipelines (2–3 meses)

| Etapa | Tempo | Recursos |
|-------|-------|----------|
| Modelagem dimensional | 2–3 semanas | [Data Modeling](../../README.md#data-modeling) |
| PostgreSQL | 2 semanas | [Recursos](../resources/README.md) |
| ETL/ELT conceitos | 2 semanas | [README principal](../../README.md#etl-e-elt) |
| Apache Airflow | 3–4 semanas | [Guia Airflow](../airflow/README.md) |
| dbt | 3 semanas | [Guia dbt](../dbt/README.md) |

**Objetivo:** Construir um pipeline batch completo com orquestração e transformações versionadas.

---

## Fase 3 — Escala e Cloud (3–4 meses)

| Etapa | Tempo | Recursos |
|-------|-------|----------|
| Apache Spark | 4–6 semanas | [Guia Spark](../spark/README.md) |
| Cloud (AWS/GCP/Azure) | 4–6 semanas | [Guia Cloud](../cloud/README.md) |
| Data Warehouse | 2–3 semanas | [README principal](../../README.md#data-warehouse) |
| Lakehouse | 2–3 semanas | [README principal](../../README.md#lakehouse) |
| Terraform | 2 semanas | [README principal](../../README.md#terraform) |

**Objetivo:** Processar datasets grandes, deploy em cloud, modelar camadas medallion.

---

## Fase 4 — Streaming e Produção (2 meses)

| Etapa | Tempo | Recursos |
|-------|-------|----------|
| Kafka | 3 semanas | [Guia Kafka](../kafka/README.md) |
| CI/CD para dados | 2 semanas | [Recursos](../resources/README.md) |
| Data Quality | 2 semanas | Great Expectations, dbt tests |
| Observabilidade | 1 semana | Logs, métricas, alertas |

---

## Fase 5 — Mercado (contínuo)

- [30+ projetos](../projects/README.md) no portfólio
- [Desafios práticos](../../README.md#desafios)
- [Entrevistas](../interview/README.md)
- [Certificações](../../README.md#certificacoes)
- Networking em [comunidades](../../README.md#comunidades)

---

## Perfis de transição

| De | Foco inicial | Tempo estimado |
|----|--------------|----------------|
| Analista de dados | SQL avançado + Python + dbt | 6–9 meses |
| Desenvolvedor backend | SQL + Airflow + cloud | 4–6 meses |
| DBA | Python + Spark + cloud DW | 6–8 meses |
| Estudante | Fundamentos completos | 12–18 meses |

> 💡 Esta trilha segue a mesma progressão da grade do [DataEngineer.help](https://dataengineer.help) — dos fundamentos (SQL, Python, Shell) aos projetos de portfólio.

[← Voltar ao Awesome Data Engineering BR](../../README.md)
