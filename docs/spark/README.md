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

[Entrevistas Spark](../interview/README.md#spark) · [Delta Lake](../../README.md#delta-lake) · [Projetos](../projects/README.md)

> 💡 Na trilha [DataEngineer.help](https://dataengineer.help), os módulos **PySpark e DataFrames** e **Tabelas Delta e Camadas Bronze/Silver/Gold** aprofundam este conteúdo.

[← Voltar ao Awesome Data Engineering BR](../../README.md)
