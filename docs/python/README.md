# Python para Engenharia de Dados — Guia Completo em Português

> **Python para dados** é a linguagem mais usada por **engenheiros de dados** no Brasil. Aprenda a construir **pipelines de dados**, integrar APIs e orquestrar **ETL/ELT** com código limpo e testável.

[← Índice principal](../../README.md) · [SQL](../sql/README.md) · [Airflow](../airflow/README.md) · [Spark](../spark/README.md) · [Projetos](../projects/README.md)

---

## Por que Python domina a engenharia de dados?

**Python** combina sintaxe legível, ecossistema maduro e integração nativa com ferramentas de **data engineering**: **Apache Airflow**, **Apache Spark** (PySpark), **dbt** (via adapters), **Kafka** (confluent-kafka), SDKs de **AWS**, **Azure** e **GCP**.

Um **engenheiro de dados** usa Python para:

- Escrever DAGs no **Apache Airflow**
- Processar dados com **Pandas**, **Polars** e **PySpark**
- Consumir **APIs REST** e webhooks
- Automatizar deploy de infraestrutura com scripts e **Terraform**
- Criar testes de qualidade de dados com **Great Expectations**

---

## Bibliotecas essenciais

| Biblioteca | Uso | Importância |
|------------|-----|-------------|
| Pandas / Polars | Transformação em memória | ⭐⭐⭐⭐⭐ |
| PySpark | Big data distribuído | ⭐⭐⭐⭐⭐ |
| requests / httpx | Consumo de APIs | ⭐⭐⭐⭐ |
| SQLAlchemy | ORM e conexões DB | ⭐⭐⭐⭐ |
| pytest | Testes automatizados | ⭐⭐⭐⭐ |
| boto3 / google-cloud | SDKs de cloud | ⭐⭐⭐⭐⭐ |
| FastAPI | APIs de dados | ⭐⭐⭐ |
| Great Expectations | Data quality | ⭐⭐⭐⭐ |

---

## Roadmap Python para dados

```
Fundamentos → Estruturas de dados → OOP básica → Virtualenv/Poetry
     ↓
Pandas/Polars → SQLAlchemy → APIs REST → Testes (pytest)
     ↓
Airflow (DAGs) → PySpark → Cloud SDKs → CI/CD
```

---

## Recursos

### Documentação
- [Python Docs (PT-BR)](https://docs.python.org/pt-br/3/)
- [Pandas Documentation](https://pandas.pydata.org/docs/)
- [PySpark API](https://spark.apache.org/docs/latest/api/python/)

### Cursos gratuitos
- [Automate the Boring Stuff](https://automatetheboringstuff.com/)
- [Kaggle Python Course](https://www.kaggle.com/learn/python)
- [Real Python](https://realpython.com/) — artigos profundos

### Livros
- *Python for Data Analysis* — Wes McKinney
- *Effective Python* — Brett Slatkin
- *Data Pipelines with Apache Airflow* — Bas Harenslak

### Projetos
- ETL de API pública para **PostgreSQL**
- Web scraper com agendamento via cron/Airflow
- CLI para validar arquivos Parquet

---

## Links relacionados

- [Apache Airflow](../airflow/README.md) — orquestração com Python
- [Apache Spark](../spark/README.md) — PySpark para escala
- [Projetos práticos](../projects/README.md)
- [Entrevistas Python](../interview/README.md#python)

> 💡 A trilha [DataEngineer.help](https://dataengineer.help) inclui módulos de **Python Básico**, **Estruturas de Dados** e **Pandas** alinhados a este guia.

[← Voltar ao Awesome Data Engineering BR](../../README.md)
