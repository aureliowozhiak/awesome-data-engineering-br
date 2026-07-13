# Apache Spark — Processamento Distribuído para Engenharia de Dados

> Domine **Apache Spark** e **PySpark** para processar terabytes de dados, construir **pipelines ETL** em escala e trabalhar com **lakehouse** em **Databricks** ou EMR.

[← Índice](../../README.md) · [Python](../python/README.md) · [Kafka](../kafka/README.md) · [Cloud](../cloud/README.md)

---

## O que é Apache Spark?

**Apache Spark** é um motor de processamento distribuído para big data. Suporta batch e streaming, roda em clusters **AWS** EMR, **GCP** Dataproc, **Azure** HDInsight e **Databricks**.

### Por que aprender Spark?

- Padrão para **ETL** em volume (GB a PB)
- API unificada: DataFrame, SQL, Streaming
- Integração com **Delta Lake**, **Iceberg**, Parquet
- Alta demanda no mercado brasileiro de **data engineering**

### Quando usar

| Spark | Alternativa |
|-------|-------------|
| Datasets > 10–50 GB | Pandas/Polars para dados menores |
| Transformações complexas distribuídas | SQL + dbt no warehouse |
| ML em escala (MLlib) | Frameworks especializados |
| Streaming estruturado | **Kafka** + Flink para ultra-low latency |

**Importância:** ⭐⭐⭐⭐⭐

---

## Conceitos-chave

- **RDD** — estrutura legada, ainda relevante em entrevistas
- **DataFrame/Dataset** — API moderna (use esta)
- **Spark SQL** — queries declarativas
- **Catalyst Optimizer** — otimização automática
- **Partitioning** — chave para performance
- **Shuffle** — operação cara, minimize

---

## Recursos

### Documentação
- [Spark Docs](https://spark.apache.org/docs/latest/)
- [Databricks Spark Guide](https://docs.databricks.com/spark/index.html)

### Cursos gratuitos
- [Spark Official Examples](https://github.com/apache/spark/tree/master/examples)
- Databricks Community Edition (free tier)

### Livros
- *Learning Spark* — O'Reilly
- *Spark: The Definitive Guide* — Bill Chambers
- *High Performance Spark* — Holden Karau

### Projetos
- ETL de logs JSON para Parquet particionado
- Join de datasets de bilhões de linhas com broadcast
- Structured Streaming com **Kafka**

---

## Exemplos PySpark

### Leitura e escrita com particionamento

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("etl-vendas").getOrCreate()

df = spark.read.parquet("s3://data-lake/bronze/vendas/")
df_filtered = df.filter("event_date >= '2026-01-01'")

(df_filtered
 .repartition("country")
 .write
 .mode("overwrite")
 .partitionBy("event_date")
 .parquet("s3://data-lake/silver/vendas/"))
```

### Window function em Spark SQL

```python
from pyspark.sql import functions as F
from pyspark.sql.window import Window

w = Window.partitionBy("customer_id").orderBy(F.desc("order_date"))

df.withColumn("rank", F.row_number().over(w)) \
  .filter("rank = 1") \
  .drop("rank")
```

### Broadcast join para tabela pequena

```python
from pyspark.sql.functions import broadcast

df_large.join(broadcast(df_small), "product_id")
```

---

## Tuning de performance

| Parâmetro | Default | Quando ajustar |
|-----------|---------|----------------|
| `spark.sql.shuffle.partitions` | 200 | Aumentar para jobs grandes; reduzir para datasets pequenos |
| `spark.default.parallelism` | # cores | Alinhar com número de executors × cores |
| `spark.sql.autoBroadcastJoinThreshold` | 10 MB | Aumentar se dim tables são maiores |
| `spark.serializer` | Kryo | Sempre usar Kryo em produção |

### Sintomas e diagnóstico

| Sintoma | Causa provável | Ação |
|---------|----------------|------|
| Job lento com poucos tasks ativas | Poucas partições | `repartition()` ou aumentar shuffle partitions |
| OOM no executor | Shuffle grande ou skew | Salting, broadcast join, mais memória |
| Muitas tasks pequenas | Over-partitioning | `coalesce()` após filtro agressivo |
| Spill to disk | Memória insuficiente | Aumentar `spark.executor.memory` |

---

## Structured Streaming — visão geral

```python
stream = (spark.readStream
    .format("kafka")
    .option("kafka.bootstrap.servers", "broker:9092")
    .option("subscribe", "eventos")
    .load())

parsed = stream.selectExpr("CAST(value AS STRING) as json")
query = (parsed.writeStream
    .format("delta")
    .outputMode("append")
    .option("checkpointLocation", "s3://checkpoints/eventos/")
    .start("s3://data-lake/silver/eventos/"))

query.awaitTermination()
```

---

## Checklist de domínio Spark

- [ ] Uso DataFrame API (não RDD) para código novo
- [ ] Entendo narrow vs wide transformations
- [ ] Sei quando usar broadcast join
- [ ] Particiono dados por colunas de filtro frequente
- [ ] Monitoro Spark UI (stages, shuffle read/write)
- [ ] Configuro checkpoint em Structured Streaming
- [ ] Escrevo em Parquet/Delta com particionamento adequado

---

## Ferramentas online do repositório

- [Parquet Viewer](../../tools/parquet-viewer/) — inspecionar schema, metadados e prévia de arquivos Parquet

---

[Entrevistas Spark](../interview/README.md#spark) · [Delta Lake](../../README.md#delta-lake) · [Projetos](../projects/README.md)

> 💡 Na trilha [DataEngineer.help](https://dataengineer.help), os módulos **PySpark e DataFrames** e **Tabelas Delta e Camadas Bronze/Silver/Gold** aprofundam este conteúdo.

[← Voltar ao Awesome Data Engineering BR](../../README.md)
