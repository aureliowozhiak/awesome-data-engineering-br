# English for Data Engineers — Vocabulário Técnico e Comunicação

> Aprenda **English for Data Engineers**: vocabulário técnico de **pipelines**, **cloud**, **warehouses** e frases úteis para PRs, RFCs e entrevistas internacionais.

[← Índice](../../README.md) · [Soft Skills](../soft-skills/README.md) · [Communication](../communication/README.md) · [Interview](../interview/README.md) · [Kafka](../kafka/README.md)

---

## Why English matters for data engineers

Most **documentation**, cloud consoles, Stack Overflow answers, and job posts in **data engineering** are in English. Even in Brazil, seniors read docs in English daily and often write PRs or RFCs for global teams.

As a **data engineer**, English helps you:

- Read official docs (Spark, dbt, Airflow, Kafka) faster
- Write clear PR descriptions and incident updates
- Interview with international companies
- Follow talks, RFCs, and design docs

**Importance:** ⭐⭐⭐⭐

---

## What to practice

| Area | Level | Focus |
|------|-------|-------|
| Core DE vocabulary | ⭐⭐⭐⭐⭐ | pipeline, warehouse, latency, throughput |
| Cloud & infra terms | ⭐⭐⭐⭐ | bucket, IAM role, provision, region |
| Pipeline verbs | ⭐⭐⭐⭐⭐ | ingest, transform, backfill, retry |
| Reliability language | ⭐⭐⭐⭐ | SLA, freshness, idempotent, exactly-once |
| Soft communication | ⭐⭐⭐⭐ | trade-off, blocker, follow-up |
| Interview storytelling | ⭐⭐⭐⭐ | STAR answers in English |

---

## When to use English vs Portuguese

| Situation | Language tip |
|-----------|--------------|
| Internal Brazilian stakeholders | Portuguese; keep English terms when standard (`SLA`, `mart`) |
| GitHub issues / open source | English |
| Cloud IAM & error messages | English (search exact strings) |
| Resume for global roles | English |
| Pairing with local squad | Portuguese OK; docs often bilingual |

---

## Recommended resources

### Free practice
- Official docs: read one page aloud per day (Airflow / dbt / Kafka)
- [Google Tech Writing](https://developers.google.com/tech-writing) — clear technical English
- YouTube: Databricks, Confluent, AWS re:Invent talks (1.25× speed)

### Vocabulary building
- Keep a personal glossary (EN → PT) of terms you meet in tickets
- Flashcards for verbs: *ingest, upsert, backfill, compact, partition*

### Related guides
- [Communication](../communication/README.md) · [Interview](../interview/README.md) · [Soft Skills](../soft-skills/README.md)

---

## Core vocabulary (EN → meaning)

| English | Portuguese (approx.) | Example |
|---------|----------------------|---------|
| **Pipeline** | Pipeline / fluxo | “The ingestion pipeline failed.” |
| **Batch / streaming** | Lote / tempo real | “We use batch for daily reports.” |
| **Latency / throughput** | Latência / vazão | “Low latency, high throughput.” |
| **Backfill** | Recarga histórica | “We need to backfill 30 days.” |
| **Watermark** | Marca d’água (incremental) | “Incremental load by watermark.” |
| **Idempotent** | Idempotente | “Retries must be idempotent.” |
| **Freshness** | Atualidade dos dados | “Mart freshness SLA is 2 hours.” |
| **Schema evolution** | Evolução de schema | “Backward-compatible schema evolution.” |
| **Partition pruning** | Poda de partições | “Filter by date for partition pruning.” |
| **Dead letter queue (DLQ)** | Fila de mensagens inválidas | “Invalid events go to the DLQ.” |
| **Lineage** | Linhagem / rastreio | “We track column-level lineage.” |
| **Orchestration** | Orquestração | “Airflow handles orchestration.” |

---

## Useful phrases for PRs and status

### Pull request

```text
## What
Makes stg_orders incremental based on updated_at.

## Why
Cuts runtime from 45 minutes to ~6 minutes in staging.

## How I tested
- dbt build -s stg_orders+
- Row count matches full refresh within 0.01%

## Risks / follow-ups
Late-arriving updates older than 7 days are out of window — documented in the model README.
```

### Status update

```text
Done: silver.orders dedupe + dbt tests in CI
In progress: incremental fct_orders (PR #128)
Blocker: read access to CRM schema (ticket #4521)
Next: gold mart + freshness alert; ETA Thursday if access lands by Tue
```

### Meeting / design discussion

```text
"The trade-off is freshness versus cost."
"I'd like to propose an incremental load first, then CDC later."
"Can we align on the grain of this fact table?"
"What's the SLA for this dashboard?"
"Let's spike for two days and then decide."
```

---

## Interview snippets (STAR-friendly)

```text
Situation: Our daily full refresh missed the finance D+1 deadline.
Task: Reduce load time without breaking historical accuracy.
Action: I designed an incremental merge on updated_at, added uniqueness tests,
        and a freshness alert.
Result: Runtime dropped from 90 to 12 minutes; SLA met for 30 days straight.
```

---

## Common false friends & tips

| Watch out | Tip |
|-----------|-----|
| **Actual** ≠ “atual” | Use *current* / *up-to-date* |
| **Commit** (Git) vs *compromise* | Different meanings |
| **Push** to prod | Common; also *deploy* / *release* |
| **Job** | Airflow/Spark job, not only “emprego” |
| Pronunciation | Practice: *schema*, *cache*, *queue*, *idempotent* |

---

## Checklist — English for DE

- [ ] I can read cloud/Spark/dbt docs without translating every line
- [ ] I write PR descriptions in clear English
- [ ] I know core terms: backfill, freshness, idempotent, watermark
- [ ] I can explain a pipeline trade-off in English
- [ ] I practice one STAR story for interviews
- [ ] I keep a personal EN↔PT glossary
- [ ] I search errors using the exact English message

---

## Next steps

1. Apply phrases in [Communication](../communication/README.md)
2. Practice interview answers in [Interview](../interview/README.md)
3. Read English docs for [Kafka](../kafka/README.md), [Airflow](../airflow/README.md), [dbt](../dbt/README.md)
4. Strengthen collaboration via [Soft Skills](../soft-skills/README.md)

> 💡 Technical English shows up throughout the [DataEngineer.help](https://dataengineer.help) learning path — docs, tools, and real-world terminology.

---


---

## Quiz glossary extras (must-know)

| Term | Meaning |
|------|---------|
| upstream / downstream | Producers before you / consumers after you |
| backfill | Reprocess historical data |
| stale data | Data older than expected freshness |
| trade-off | Pros/cons choice |
| on-call | Incident duty rotation |
| runbook | Step-by-step ops procedure |
| deprecation | Announced sunsetting of API/column/pipeline |
| LGTM | Looks Good To Me (review approve) |
| scope creep | Uncontrolled scope growth |
| SLA / SLO | Agreement vs internal objective |
| pipeline | Ingest/transform/load flow |
| idempotent | Safe under retries |
| stakeholder | Interested party |
| throughput / latency | Volume/time vs delay |
| deploy / rollback | Ship / undo release |
| watermark / checkpoint | Incremental progress / saved state |
| owner / handover | Accountable person / handoff |
| incident / postmortem | Outage event / learnings write-up |

---

[← Back to Awesome Data Engineering BR](../../README.md)
