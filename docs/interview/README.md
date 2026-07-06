# Entrevistas para Engenheiro de Dados — Perguntas e Preparação

> Prepare-se para processos seletivos de **engenharia de dados** no Brasil. Perguntas frequentes de **SQL**, **Python**, **Spark**, **Airflow** e arquitetura.

[← Índice](../../README.md) · [SQL](../sql/README.md) · [Spark](../spark/README.md) · [Roadmap](../roadmaps/README.md)

---

## Como se preparar

Processos seletivos para **engenheiro de dados** no Brasil geralmente incluem:

1. **Triagem técnica** — SQL e Python ao vivo ou take-home
2. **System design** — arquitetura de pipelines e data platform
3. **Cultura e comportamental** — metodologias ágeis, comunicação
4. **Case técnico** — projeto prático ou pair programming

---

## Perguntas frequentes gerais

- O que é **engenharia de dados** e como difere de Data Science?
- Explique a diferença entre **ETL** e **ELT**.
- O que é idempotência em pipelines?
- Como você garante qualidade de dados?
- Descreva um pipeline que você construiu do zero.
- Como lida com falhas e reprocessamento?
- O que é data lineage e por que importa?
- Explique CAP theorem de forma prática.
- Batch vs streaming: quando usar cada um?
- O que é um **data lake** vs **data warehouse**?

---

## SQL {#sql}

### Básico
- Diferença entre INNER, LEFT, RIGHT e FULL JOIN
- O que faz GROUP BY e HAVING?
- Diferença entre WHERE e HAVING

### Intermediário
- Escreva query para encontrar duplicatas
- Ranking com ROW_NUMBER vs RANK vs DENSE_RANK
- Calcule média móvel de 7 dias
- Implemente SCD Type 2 em SQL

### Avançado
- Otimize uma query lenta — quais passos?
- Explique execution plan (EXPLAIN)
- Window functions vs self-join
- Diferença entre DELETE, TRUNCATE e DROP

---

## Python {#python}

- Diferença entre list, tuple, set e dict
- O que são generators e quando usar?
- Explique *args e **kwargs
- Como lidar com arquivos grandes que não cabem na memória?
- Decorators — conceito e exemplo
- Diferença entre multiprocessing e threading
- Como você testaria um pipeline ETL?
- Pandas vs Polars — trade-offs

---

## Spark {#spark}

- Diferença entre RDD, DataFrame e Dataset
- O que é shuffle e como evitar?
- Broadcast join — quando usar?
- Cache vs persist
- Como funciona o Catalyst Optimizer?
- Particionamento — boas práticas
- Diferença entre narrow e wide transformations
- Como debugar jobs Spark lentos?

---

## Airflow {#airflow}

- O que é uma DAG?
- Diferença entre Operator e Sensor
- Como garantir idempotência?
- O que é XCom e quais os riscos?
- Como fazer backfill?
- Pools, priorities e concurrency
- Airflow vs Prefect vs Dagster

---

## Arquitetura {#arquitetura}

- Desenhe um pipeline de ingestão de eventos de app mobile
- Como modelar um data warehouse para e-commerce?
- Lambda vs Kappa architecture
- Camadas bronze, silver, gold (medallion)
- Como escolher entre Parquet, Avro e ORC?
- Estratégias de particionamento em S3
- CDC (Change Data Capture) — abordagens
- Como implementar data mesh?
- Governança e LGPD em pipelines

---

## Dicas para o dia da entrevista

> ✅ Pratique SQL ao vivo em [DataLemur](https://datalemur.com/) e [LeetCode Database](https://leetcode.com/problemset/database/)

> ✅ Tenha 2–3 projetos no GitHub para mostrar código real

> ✅ Prepare histórias no formato STAR (Situação, Tarefa, Ação, Resultado)

---

[Certificações](../../README.md#certificacoes) · [Projetos](../projects/README.md) · [Livros](../books/README.md)

---

[← Voltar ao Awesome Data Engineering BR](../../README.md)
