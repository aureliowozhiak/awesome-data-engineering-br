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

## Estrutura de projeto Python para ETL

```
meu-pipeline/
├── src/
│   ├── extract/       # conectores de fonte (API, DB, arquivos)
│   ├── transform/     # regras de negócio e limpeza
│   ├── load/          # escrita no destino
│   └── utils/         # logging, config, helpers
├── tests/
│   ├── test_extract.py
│   └── test_transform.py
├── dags/              # DAGs Airflow (se aplicável)
├── config/
│   └── settings.yaml
├── requirements.txt   # ou pyproject.toml com Poetry
├── Dockerfile
└── README.md
```

---

## Exemplos práticos de código

### Processar arquivo grande sem estourar memória

```python
import csv

def read_in_chunks(path, chunk_size=10_000):
    with open(path, newline="", encoding="utf-8") as f:
        reader = csv.DictReader(f)
        chunk = []
        for row in reader:
            chunk.append(row)
            if len(chunk) >= chunk_size:
                yield chunk
                chunk = []
        if chunk:
            yield chunk

for batch in read_in_chunks("dados.csv"):
    process(batch)  # transforma e carrega cada lote
```

### Consumir API REST com retry

```python
import httpx
import time

def fetch_with_retry(url, max_retries=3):
    for attempt in range(max_retries):
        try:
            response = httpx.get(url, timeout=30)
            response.raise_for_status()
            return response.json()
        except httpx.HTTPError as e:
            wait = 2 ** attempt
            print(f"Tentativa {attempt + 1} falhou: {e}. Aguardando {wait}s...")
            time.sleep(wait)
    raise RuntimeError(f"Falha após {max_retries} tentativas: {url}")
```

### Teste de pipeline com pytest

```python
import pandas as pd
from transform.clean import normalize_dates

def test_normalize_dates():
    df = pd.DataFrame({"created_at": ["2026-01-15", "invalid", None]})
    result = normalize_dates(df, "created_at")
    assert result["created_at"].notna().sum() == 1
    assert str(result["created_at"].iloc[0]) == "2026-01-15"
```

---

## Ambiente de desenvolvimento

| Ferramenta | Uso | Comando |
|------------|-----|---------|
| **venv** | Ambiente virtual nativo | `python -m venv .venv && source .venv/bin/activate` |
| **Poetry** | Gerenciamento moderno de deps | `poetry init && poetry add pandas` |
| **pip-tools** | requirements.txt pinado | `pip-compile requirements.in` |
| **pre-commit** | Hooks de qualidade | `pre-commit install` |

---

## Anti-padrões comuns

- Carregar dataset inteiro com `pd.read_csv()` sem `chunksize` ou `dtype`
- Hardcodar credenciais no código — use variáveis de ambiente ou secrets manager
- Ignorar type hints e testes em pipelines de produção
- Misturar lógica de negócio com código de conexão (viola SRP)
- Não logar erros com contexto (fonte, linha, timestamp)

---

## Checklist de domínio Python

- [ ] Uso generators/chunks para arquivos grandes
- [ ] Escrevo testes pytest para transformações críticas
- [ ] Consumo APIs com timeout e retry exponencial
- [ ] Gerencio dependências com venv ou Poetry
- [ ] Conheço Pandas/Polars para transformação em memória
- [ ] Integro com SDKs de cloud (boto3, google-cloud)
- [ ] Estruturo projetos ETL com separação extract/transform/load

---

## Ferramentas online do repositório

- [JSON Formatter](../../tools/json-formatter/) · [JSON→CSV](../../tools/json-to-csv/) · [CSV→JSON](../../tools/csv-to-json/)
- [CSV Profiler](../../tools/csv-profiler/) — validar dados antes do pipeline

---

## Links relacionados

- [Apache Airflow](../airflow/README.md) — orquestração com Python
- [Apache Spark](../spark/README.md) — PySpark para escala
- [Projetos práticos](../projects/README.md)
- [Entrevistas Python](../interview/README.md#python)

> 💡 A trilha [DataEngineer.help](https://dataengineer.help) inclui módulos de **Python Básico**, **Estruturas de Dados** e **Pandas** alinhados a este guia.

[← Voltar ao Awesome Data Engineering BR](../../README.md)
