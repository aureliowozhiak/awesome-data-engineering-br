# Apache Kafka — Streaming e Eventos em Engenharia de Dados

> Aprenda **Kafka** para arquiteturas event-driven, **streaming** de dados em tempo real e integração com **Spark**, **Flink** e **pipelines ETL**.

[← Índice](../../README.md) · [Spark](../spark/README.md) · [Cloud](../cloud/README.md) · [Recursos](../resources/README.md)

---

## O que é Apache Kafka?

**Apache Kafka** é uma plataforma distribuída de streaming de eventos. Funciona como backbone de arquiteturas modernas de **engenharia de dados**, conectando produtores e consumidores de mensagens com alta throughput e durabilidade.

### Por que aprender Kafka?

- Base de arquiteturas real-time em fintechs, e-commerce e IoT
- Integração nativa com **Spark Structured Streaming**, Flink, ksqlDB
- Conceitos de event sourcing e CQRS
- Managed services: AWS MSK, Confluent Cloud, Azure Event Hubs

### Quando usar

| Kafka | Alternativa |
|-------|-------------|
| Eventos em tempo real entre sistemas | RabbitMQ para filas simples |
| Log de eventos imutável | S3 + batch para latência alta |
| Múltiplos consumidores independentes | Pub/Sub do GCP |
| Replay de eventos históricos | — |

**Importância:** ⭐⭐⭐⭐

---

## Conceitos fundamentais

| Termo | Descrição |
|-------|-----------|
| Topic | Canal de mensagens |
| Partition | Unidade de paralelismo |
| Offset | Posição no log |
| Consumer Group | Consumidores cooperativos |
| Broker | Servidor Kafka |
| Schema Registry | Contratos Avro/Protobuf |

---

## Recursos

### Documentação
- [Kafka Documentation](https://kafka.apache.org/documentation/)
- [Confluent Docs](https://docs.confluent.io/)

### Cursos
- Confluent Fundamentals (gratuito)
- Udemy — Apache Kafka Series

### Livros
- *Kafka: The Definitive Guide* — Neha Narkhede
- *Designing Event-Driven Systems* — Ben Stopford

### Projetos
- Producer/consumer Python com confluent-kafka
- Pipeline Kafka → Spark Streaming → Delta Lake
- Dead letter queue para mensagens inválidas

---

[Streaming no guia principal](../../README.md#streaming) · [Entrevistas](../interview/README.md)

> 💡 O módulo **Kafka e Streaming** está previsto na trilha [DataEngineer.help](https://dataengineer.help).

[← Voltar ao Awesome Data Engineering BR](../../README.md)
