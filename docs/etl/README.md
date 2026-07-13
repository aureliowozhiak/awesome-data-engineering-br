# ETL Pipelines — Extract, Transform, Load e Qualidade de Dados

> Domine **ETL** e **ELT**: extrair, transformar e carregar dados com qualidade, orquestração e padrões usados em **engenharia de dados** no Brasil.

[← Índice](../../README.md) · [Airflow](../airflow/README.md) · [dbt](../dbt/README.md) · [SQL](../sql/README.md) · [Streaming](../streaming/README.md)

---

## O que é ETL (e ELT)?

**ETL** (*Extract, Transform, Load*) é o processo clássico de mover dados de fontes para um destino analítico. Em warehouses modernos na nuvem, o padrão **ELT** (*Extract, Load, Transform*) prevalece: carrega o bruto e transforma com SQL/**dbt** no próprio DW.

Um **engenheiro de dados** desenha pipelines para:

- Extrair de APIs, bancos OLTP, arquivos e eventos
- Transformar com limpeza, joins e regras de negócio
- Carregar em lake, warehouse ou serving layer
- Garantir **qualidade**, idempotência e observabilidade

**Importância:** ⭐⭐⭐⭐⭐

---

## O que você precisa dominar

| Tópico | Nível | Descrição |
|--------|-------|-----------|
| Extract (batch e incremental) | ⭐⭐⭐⭐⭐ | Full load vs CDC/watermark |
| Transformações | ⭐⭐⭐⭐⭐ | Limpeza, tipagem, dedupe |
| Load / upsert / merge | ⭐⭐⭐⭐⭐ | Append, overwrite, SCD |
| Qualidade de dados | ⭐⭐⭐⭐⭐ | Testes, contratos, SLAs |
| Orquestração | ⭐⭐⭐⭐⭐ | Airflow, Prefect, Dagster |
| Idempotência e retries | ⭐⭐⭐⭐ | Pipelines seguros |
| Observabilidade | ⭐⭐⭐⭐ | Logs, métricas, lineage |

---

## Quando usar ETL vs ELT vs streaming

| Cenário | Abordagem |
|---------|-----------|
| Transformações pesadas antes do DW (legado/on-prem) | **ETL** |
| Cloud DW (BigQuery, Snowflake, Redshift) | **ELT** + dbt |
| Eventos em tempo real | **Streaming** ([Kafka](../kafka/README.md) / Flink) |
| Arquivos diários SFTP/API | Batch orquestrado (Airflow) |
| Mudanças linha a linha no OLTP | CDC (Debezium etc.) |

---

## Recursos recomendados

### Documentação e guias
- [Airflow Concepts](https://airflow.apache.org/docs/apache-airflow/stable/core-concepts/overview.html)
- [dbt Docs — Build](https://docs.getdbt.com/docs/build/build)
- [Great Expectations](https://greatexpectations.io/)

### Cursos e prática
- Projetos ETL open source no [guia de projetos](../projects/README.md)
- Tutoriais oficiais Airflow + dbt

### Livros
- *Fundamentals of Data Engineering* — Joe Reis & Matt Housley
- *Designing Data-Intensive Applications* — Martin Kleppmann (conceitos)

---

## Exemplos práticos

### Pipeline em camadas (mental model)

```text
Fonte (API/DB/S3)
    → Bronze (raw, append-only)
    → Silver (limpo, tipado, deduplicado)
    → Gold (marts analíticos / fatos e dimensões)
```

### Extract incremental por watermark (SQL)

```sql
-- Extrai apenas o que mudou desde a última carga
SELECT *
FROM source.orders
WHERE updated_at > (
  SELECT COALESCE(MAX(updated_at), '1970-01-01')
  FROM staging.orders_watermark
);
```

### Checks de qualidade (conceitual)

```yaml
# Exemplo estilo testes declarativos
tests:
  - name: orders_pk_unique
    type: unique
    column: order_id
  - name: amount_not_null
    type: not_null
    column: amount
  - name: amount_positive
    type: accepted_range
    column: amount
    min: 0
```

### Orquestração — dependências

```text
extract_orders >> validate_raw >> transform_silver >> publish_gold >> notify_sla
```

---

## Padrões de carga

| Padrão | Quando usar | Risco |
|--------|-------------|-------|
| **Full refresh** | Tabelas pequenas | Custo e downtime |
| **Append** | Eventos imutáveis | Duplicatas se reprocessar mal |
| **Merge / upsert** | Dimensões e CDC | Precisa chave confiável |
| **Overwrite partição** | Fatos diários | Ideal com partição por data |
| **SCD Type 2** | Histórico de atributos | Complexidade de query |

---

## Anti-padrões comuns

- **Pipeline sem idempotência** — reexecução duplica dados
- **Só “job rodou OK”** sem testes de qualidade
- **Transformação opaca** em script único de 2k linhas
- **Sem watermark/CDC** e full load diário em tabela enorme
- **Ignorar late-arriving data** em janelas de negócio

---

## Checklist de domínio ETL

- [ ] Distingo ETL vs ELT e quando usar cada um
- [ ] Implemento carga incremental com watermark ou CDC
- [ ] Garanto idempotência e retries seguros
- [ ] Defino testes de completude, unicidade e validade
- [ ] Orquestro dependências (Airflow ou similar)
- [ ] Monitoro freshness e falhas com alerta
- [ ] Documento contratos de dados (schema + SLA)

---

## Próximos passos na trilha

1. Orquestração em [Airflow](../airflow/README.md)
2. Transformações versionadas em [dbt](../dbt/README.md)
3. Modelo dimensional em [Data Modeling](../data-modeling/README.md)
4. Tempo real em [Streaming](../streaming/README.md)

> 💡 Os módulos de **pipelines** e **qualidade de dados** da trilha [DataEngineer.help](https://dataengineer.help) aprofundam ETL/ELT na prática.

---


---

## Conceitos que caem no quiz / entrevistas

### ETL vs ELT
ETL transforma antes de carregar. ELT carrega raw e transforma no destino (dbt/SQL) — padrão cloud moderno.

### Idempotência e watermark
Reexecutar = mesmo resultado efetivo. Watermark marca progresso incremental (`updated_at`/offset).

### Schema drift, dead letter, quality, orquestração
Drift = origem muda schema. DLQ isola registros ruins. Quality checks = null/unicidade/volume. Orquestrador garante upstream → downstream.

### Staging, CDC, reverse ETL
Staging = zona intermediária. CDC captura mudanças. Reverse ETL envia dados curados de volta ao operacional (CRM etc.).

---

[← Voltar ao Awesome Data Engineering BR](../../README.md)
