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

## Respostas modelo para perguntas frequentes

### ETL vs ELT?

> **ETL** transforma dados antes de carregar no destino — comum em pipelines legados e quando o destino não tem compute robusto. **ELT** carrega dados brutos primeiro e transforma dentro do warehouse com SQL — padrão moderno com Snowflake, BigQuery e dbt, aproveitando o poder de processamento do DW.

### O que é idempotência em pipelines?

> Uma operação é idempotente quando executá-la múltiplas vezes produz o mesmo resultado. Em pipelines, isso significa que reprocessar um dia inteiro não duplica dados. Implemente com `MERGE`, `INSERT OVERWRITE` por partição, ou deletes + inserts atômicos.

### Batch vs streaming?

> **Batch** processa dados em lotes agendados (diário, horário) — mais simples, mais barato, latência de minutos/horas. **Streaming** processa eventos conforme chegam — latência de segundos, mais complexo e caro. Use batch para relatórios e streaming quando o negócio exige dados quase em tempo real (fraude, personalização).

### Medallion architecture?

> Três camadas no data lake: **Bronze** (raw, dados como chegaram), **Silver** (limpos, tipados, deduplicados) e **Gold** (agregados, prontos para BI). Cada camada tem SLA e qualidade crescentes. Padrão dominante em lakehouse com Delta Lake, Iceberg ou Hudi.

---

## Formato STAR para perguntas comportamentais

| Letra | Significado | Exemplo |
|-------|-------------|---------|
| **S** | Situação | "O pipeline de vendas falhava toda segunda-feira..." |
| **T** | Tarefa | "Precisava identificar a causa e garantir SLA de 8h" |
| **A** | Ação | "Analisei logs do Airflow, encontrei race condition no XCom, refatorei para staging em S3" |
| **R** | Resultado | "SLA passou de 60% para 99%, e documentei o padrão para o time" |

Prepare 3–5 histórias STAR cobrindo: resolução de incidente, projeto do zero, conflito técnico, aprendizado rápido de ferramenta nova.

---

## Take-home projects — dicas

- Leia o enunciado com atenção e faça perguntas clarificadoras (por email)
- Entregue em 48–72h, não antes (parece apressado) nem depois (sem extensão)
- Inclua README com: setup, decisões de arquitetura, trade-offs, o que faria diferente
- Código limpo > features extras — testes e documentação impressionam mais
- Se usar IA, declare e explique como validou o código

---

## Negociação salarial no Brasil

| Dica | Detalhe |
|------|---------|
| Pesquise antes | Glassdoor, Levels.fyi, comunidades (Data Hackers) |
| CLT vs PJ | PJ paga 30–50% mais, mas sem benefícios |
| Remoto internacional | Salários em USD/EUR para empresas gringas |
| Não dê o primeiro número | Pergunte a faixa da vaga primeiro |
| Pacote total | Considere VR, PLR, stock options, home office |

---

## Recursos para praticar

| Tipo | Recurso |
|------|---------|
| SQL ao vivo | [DataLemur](https://datalemur.com/), [LeetCode Database](https://leetcode.com/problemset/database/) |
| System design | [ByteByteGo](https://blog.bytebytego.com/), desenhe no Excalidraw |
| Mock interviews | [Pramp](https://www.pramp.com/), colegas da comunidade |
| Perguntas reais | [Glassdoor](https://www.glassdoor.com.br/) — busque por empresa + "data engineer" |

---

## Dicas para o dia da entrevista

> ✅ Pratique SQL ao vivo em [DataLemur](https://datalemur.com/) e [LeetCode Database](https://leetcode.com/problemset/database/)

> ✅ Tenha 2–3 projetos no GitHub para mostrar código real

> ✅ Prepare histórias no formato STAR (Situação, Tarefa, Ação, Resultado)

---

[Certificações](../../README.md#certificacoes) · [Projetos](../projects/README.md) · [Livros](../books/README.md)

---

[← Voltar ao Awesome Data Engineering BR](../../README.md)
