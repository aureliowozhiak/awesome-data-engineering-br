# Docker para Engenharia de Dados — Compose, Airflow e Images

> Domine **Docker** e **Docker Compose** para padronizar ambientes de **Airflow**, bancos, **Spark** e stacks locais de **engenharia de dados**.

[← Índice](../../README.md) · [Airflow](../airflow/README.md) · [Recursos](../resources/README.md#docker) · [Git](../git/README.md) · [Linux](../linux/README.md)

---

## Por que Docker é essencial para o engenheiro de dados?

**Docker** empacota aplicações e dependências em **containers** — o mesmo ambiente roda no seu laptop, no CI e em produção. Em **data engineering**, isso evita o clássico “funciona na minha máquina” ao subir **Airflow**, **PostgreSQL**, **MinIO**, **Kafka** e notebooks.

Um **engenheiro de dados** usa Docker para:

- Subir stacks locais com Compose (Postgres + MinIO + Airflow)
- Isolar versões de Python, Java e drivers JDBC
- Testar DAGs e imagens antes do deploy
- Padronizar CI/CD de pipelines e ferramentas de dados

**Importância:** ⭐⭐⭐⭐⭐

---

## O que você precisa dominar

| Tópico | Nível | Descrição |
|--------|-------|-----------|
| Imagens e containers | ⭐⭐⭐⭐⭐ | `build`, `run`, `exec`, volumes |
| Dockerfile | ⭐⭐⭐⭐⭐ | Camadas, cache, multi-stage |
| Docker Compose | ⭐⭐⭐⭐⭐ | Stacks multi-serviço locais |
| Volumes e redes | ⭐⭐⭐⭐ | Persistência e comunicação |
| Healthchecks | ⭐⭐⭐⭐ | Dependências entre serviços |
| Registry e tags | ⭐⭐⭐ | Versionar e publicar imagens |
| Recursos (CPU/mem) | ⭐⭐⭐ | Limites em stacks pesadas |

---

## Quando usar Docker vs alternativas

| Cenário | Ferramenta recomendada |
|---------|------------------------|
| Stack local de DE (DB + object storage) | **Docker Compose** |
| Orquestração Airflow / Spark local | Compose + imagens oficiais |
| Produção em escala | Kubernetes / ECS / Cloud Run |
| Só um script Python isolado | `venv` / Poetry (sem Docker) |
| Ambiente idêntico ao CI | Mesma imagem no GitHub Actions |

---

## Recursos recomendados

### Documentação oficial
- [Docker Docs](https://docs.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- [Apache Airflow — Running on Docker](https://airflow.apache.org/docs/apache-airflow/stable/howto/docker-compose/index.html)

### Cursos e tutoriais gratuitos
- [Docker Getting Started](https://docs.docker.com/get-started/) — oficial
- [Play with Docker](https://labs.play-with-docker.com/) — lab no browser

### Projetos práticos
- Compose com Postgres + MinIO (S3-compatible)
- Subir Airflow oficial via `docker-compose.yaml`
- Dockerfile customizado para DAG com dependências extras

---

## Exemplos práticos

### Compose mínimo — Postgres + MinIO

```yaml
# docker-compose.yml
services:
  postgres:
    image: postgres:15
    environment:
      POSTGRES_DB: dados
      POSTGRES_USER: de
      POSTGRES_PASSWORD: de123
    ports: ["5432:5432"]
    volumes: ["pgdata:/var/lib/postgresql/data"]
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U de -d dados"]
      interval: 5s
      retries: 5

  minio:
    image: minio/minio
    command: server /data --console-address ":9001"
    ports: ["9000:9000", "9001:9001"]
    environment:
      MINIO_ROOT_USER: minio
      MINIO_ROOT_PASSWORD: minio123
    volumes: ["miniodata:/data"]

volumes:
  pgdata:
  miniodata:
```

```bash
docker compose up -d
docker compose ps
docker compose logs -f postgres
```

### Dockerfile enxuto para job Python

```dockerfile
FROM python:3.11-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY src/ ./src/
CMD ["python", "-m", "src.pipeline"]
```

### Comandos do dia a dia

```bash
docker build -t meu-etl:1.0 .
docker run --rm -e ENV=dev meu-etl:1.0
docker exec -it <container> bash
docker system prune -f   # limpar imagens órfãs (cuidado)
```

---

## Padrões em stacks de dados

| Padrão | Quando usar | Exemplo |
|--------|-------------|---------|
| **Compose para local** | Dev e demos | Postgres + Airflow + Redis |
| **Imagem oficial + override** | Customizar Airflow | `Dockerfile` com `pip install` extras |
| **Named volumes** | Persistência de DB | `pgdata:/var/lib/postgresql/data` |
| **Healthcheck + depends_on** | Ordem de boot | Airflow espera Postgres healthy |
| **Multi-stage build** | Imagens menores | build deps → runtime slim |

---

## Anti-padrões comuns

- **Guardar secrets no Dockerfile** — use env, secrets do Compose ou vault
- **`latest` em produção** — pinne tags (`postgres:15.4`)
- **Rodar tudo como root** sem necessidade
- **Montar o disco inteiro** sem entender bind mounts
- **Ignorar limites de memória** em stacks Spark/Airflow locais

---

## Checklist de domínio Docker

- [ ] Escrevo Dockerfile e Compose do zero
- [ ] Uso volumes para persistir Postgres/MinIO
- [ ] Subo e debugo uma stack Airflow com Compose
- [ ] Entendo camadas, cache de build e multi-stage
- [ ] Configuro healthchecks e `depends_on`
- [ ] Versionei imagens com tags semânticas
- [ ] Sei inspecionar logs e entrar no container (`exec`)

---

## Próximos passos na trilha

1. Combine com [Linux](../linux/README.md) para operar containers no servidor
2. Versionamento e CI em [Git](../git/README.md)
3. Orquestração real em [Airflow](../airflow/README.md)
4. Infra na nuvem com [Terraform](../terraform/README.md)

> 💡 O módulo **Docker e CI/CD para Dados** está previsto na trilha [DataEngineer.help](https://dataengineer.help).

---

[← Voltar ao Awesome Data Engineering BR](../../README.md)
