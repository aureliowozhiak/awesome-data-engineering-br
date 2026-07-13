# Comunicação Técnica para Engenheiros de Dados — RFC, Status e Stakeholders

> Aprenda **comunicação técnica** em **engenharia de dados**: RFCs, status updates, alinhamento com stakeholders e documentação que evita retrabalho.

[← Índice](../../README.md) · [Soft Skills](../soft-skills/README.md) · [Architecture](../architecture/README.md) · [Git](../git/README.md) · [English](../english/README.md)

---

## Por que comunicação é parte do trabalho de DE?

Um pipeline invisível ou mal explicado gera desconfiança. O **engenheiro de dados** precisa escrever **RFCs**, atualizar status, abrir PRs claros e falar com produto/financeiro sem perder precisão.

Comunicação técnica eficaz cobre:

- Propostas de mudança (RFC / ADR)
- Status de entrega e incidentes
- Contratos de dados com consumidores
- Code review e handoff entre turnos

**Importância:** ⭐⭐⭐⭐⭐

---

## O que você precisa dominar

| Formato | Nível | Uso |
|---------|-------|-----|
| RFC / ADR curto | ⭐⭐⭐⭐⭐ | Decisões de arquitetura e tools |
| Status update | ⭐⭐⭐⭐⭐ | Semana / sprint / incidente |
| PR description | ⭐⭐⭐⭐⭐ | Contexto, testes, riscos |
| Data contract | ⭐⭐⭐⭐ | Schema, SLA, owners |
| Runbook | ⭐⭐⭐⭐ | Operação e on-call |
| Apresentação executiva | ⭐⭐⭐ | Impacto sem jargão excessivo |

---

## Quando usar cada artefato

| Situação | Artefato |
|----------|----------|
| Trocar Kafka por Pub/Sub (ou vice-versa) | **RFC** com alternativas |
| “Por que escolhemos partição por data?” | **ADR** (Architecture Decision Record) |
| Sprint update para PM | **Status** (feito / bloqueio / próximo) |
| Mudança em modelo dbt | **PR** + nota de breaking change |
| Mart usado pelo financeiro | **Data contract** + canal de suporte |
| Pipeline caiu às 3h | **Incidente** + postmortem curto |

---

## Recursos recomendados

### Guias e templates
- [GitHub — Pull request](https://docs.github.com/en/pull-requests) — boa higiene de PR
- ADRs: formato MADR / “Context → Decision → Consequences”
- [Soft skills](../soft-skills/README.md) e [English](../english/README.md)

### Prática
- Escrever 1 RFC por trimestre no time
- Template de PR no repositório de dbt/Airflow
- Postmortem blameless após incidente real

---

## Exemplos práticos

### Template mínimo de RFC de dados

```markdown
# RFC: Carga incremental de pedidos (CRM → gold)

## Contexto
O full refresh diário de fct_orders leva 90 min e atrasa o BI.

## Objetivo
Freshness ≤ 2h com custo ≤ atual.

## Alternativas
1. Full refresh (status quo)
2. Incremental por updated_at + merge
3. CDC via Debezium

## Proposta
Opção 2 no curto prazo; CDC no roadmap Q3.

## Impacto
- Breaking change: não
- Testes: unicidade order_id, freshness
- Rollback: reexecutar full refresh

## Decisão / próximos passos
...
```

### Status update (Slack/e-mail)

```text
Status — Mart Vendas (12/05)
✅ Feito: silver.orders com dedupe; testes dbt no CI
🚧 Em andamento: fct_orders incremental (PR #128)
⛔ Bloqueio: acesso de leitura ao schema CRM (ticket #4521)
Next: gold + alerta de freshness; ETA qui se o acesso sair até ter
```

### PR description útil

```markdown
## O que
Torna stg_orders incremental por updated_at.

## Por quê
Reduz runtime de 45min → ~6min no ambiente de staging.

## Como testei
- [x] dbt build -s stg_orders+
- [x] Comparação de contagem vs full refresh (diff < 0.01%)

## Riscos
Late-arriving updates > 7 dias fora da janela — documentado no README do model.
```

---

## Princípios de clareza com stakeholders

| Princípio | Exemplo |
|-----------|---------|
| **Lide com o “porquê”** | “Precisamos disso para fechar D+1 do financeiro” |
| **Trade-offs explícitos** | “Mais freshness = +30% custo de compute” |
| **Uma ideia por parágrafo** | Evite misturar incidente e roadmap |
| **Call to action** | “Preciso de aprovação até sexta” |
| **Sem jargão sem necessidade** | Explique “watermark” se a audiência for negócio |

---

## Anti-padrões de comunicação

- **RFC de 20 páginas** sem TL;DR
- **Status só feliz** — esconde bloqueios
- **PR sem contexto** (“fix”)
- **Acordo verbal** sobre SLA de dados sem registro
- **Culpa em postmortem** — reduz aprendizado

---

## Checklist de comunicação técnica

- [ ] Escrevo RFC/ADR com contexto, opções e decisão
- [ ] Mando status com feito / bloqueio / próximo
- [ ] Descrevo PRs com testes e riscos
- [ ] Documento contratos (schema + freshness + owner)
- [ ] Adapto o nível de detalhe à audiência
- [ ] Fecho incidentes com learnings acionáveis
- [ ] Mantenho runbooks atualizados

---

## Próximos passos na trilha

1. Combine com [Soft Skills](../soft-skills/README.md)
2. Decisões de desenho em [Architecture](../architecture/README.md)
3. Vocabulário em [English](../english/README.md)
4. Colaboração via [Git](../git/README.md) e PRs

> 💡 Na trilha [DataEngineer.help](https://dataengineer.help), documentar e explicar soluções é parte do diferencial profissional.

---

[← Voltar ao Awesome Data Engineering BR](../../README.md)
