# Soft Skills para Engenheiros de Dados — Colaboração, Priorização e Carreira

> Desenvolva **soft skills** essenciais para **engenheiros de dados**: colaboração com negócio, priorização, ownership e crescimento de carreira no Brasil.

[← Índice](../../README.md) · [Communication](../communication/README.md) · [English](../english/README.md) · [Interview](../interview/README.md) · [Roadmaps](../roadmaps/README.md)

---

## Por que soft skills importam tanto quanto Spark e SQL?

Pipelines excelentes falham se ninguém confia nos números, se o escopo nunca fecha ou se o time não se fala. Em **engenharia de dados**, você está na interface entre **produto**, **analytics**, **infra** e **negócio**.

Soft skills que diferenciam um DE sênior:

- Traduzir ambiguidade de negócio em requisitos técnicos
- Priorizar (impacto × esforço × risco)
- Dar e receber feedback em code review
- Assumir ownership de qualidade e custo dos dados
- Comunicar status sem jargão desnecessário

**Importância:** ⭐⭐⭐⭐⭐

---

## O que desenvolver

| Habilidade | Nível | Na prática do DE |
|------------|-------|------------------|
| Escuta ativa | ⭐⭐⭐⭐⭐ | Entender o “porquê” da métrica |
| Priorização | ⭐⭐⭐⭐⭐ | Backlog de pipelines vs firefighting |
| Ownership | ⭐⭐⭐⭐⭐ | SLA, qualidade, on-call |
| Colaboração cross-funcional | ⭐⭐⭐⭐⭐ | Analytics, ML, produto |
| Negociação de escopo | ⭐⭐⭐⭐ | MVP de dados vs “tudo agora” |
| Mentoria | ⭐⭐⭐ | Elevar o time |
| Autogestão | ⭐⭐⭐⭐⭐ | Foco em meio a incidentes |

---

## Quando investir em cada frente

| Situação | Foque em |
|----------|----------|
| Muitos pedidos ad hoc | Priorização e expectativas |
| Desconfiança nos dados | Transparência + qualidade + comunicação |
| Time crescendo | Mentoria e padrões |
| Entrevista / promoção | Storytelling de impacto ([Interview](../interview/README.md)) |
| Stakeholders internacionais | [English](../english/README.md) + clareza |

---

## Recursos recomendados

### Livros
- *The Manager's Path* — Camille Fournier (carreira e liderança técnica)
- *Radical Candor* — Kim Scott (feedback)
- *Staff Engineer* — Will Larson (influência sem gestão)

### Prática no repositório
- [Comunicação técnica](../communication/README.md) — RFCs e status
- [Roadmaps](../roadmaps/README.md) — planejamento de aprendizado
- [Entrevistas](../interview/README.md) — narrativas STAR

### Hábitos
- Retro de incidentes sem culpa (blameless)
- 1:1 com pares de analytics/produto
- Documentar decisões (ADR/RFC curto)

---

## Exemplos práticos

### Priorização simples de backlog de dados

| Pedido | Impacto | Esforço | Risco | Ordem |
|--------|---------|---------|-------|-------|
| Corrigir duplicata em fct_orders | Alto | Baixo | Alto | 1 |
| Novo dashboard “nice to have” | Médio | Médio | Baixo | 3 |
| Migração de tool sem dor atual | Baixo | Alto | Médio | 4 |
| Alerta de freshness no mart crítico | Alto | Baixo | Alto | 2 |

### Ownership — perguntas que um DE faz

```text
1. Qual o SLA de freshness deste mart?
2. Quem é alertado se falhar?
3. Qual o contrato de schema com o consumidor?
4. Como medimos qualidade (testes)?
5. Qual o custo mensal estimado deste pipeline?
```

### Feedback em code review (construtivo)

```text
Em vez de: "Isso está errado."
Prefira: "Nesse join podemos gerar fã-out; que tal validar grão
com um teste de unicidade em order_id + item_id?"
```

---

## Armadilhas comuns de carreira em DE

- **Herói silencioso** — resolve tudo sozinho, time não escala
- **Dizer sim a tudo** — vira fábrica de CSV ad hoc
- **Só ferramenta, zero contexto** — otimiza o que não importa
- **Evitar conflito** — dívida técnica e métricas duplicadas crescem
- **Não documentar impacto** — promoção fica difícil

---

## Checklist de soft skills

- [ ] Clarifico objetivo de negócio antes de codar
- [ ] Priorizo com critérios explícitos
- [ ] Comunico riscos e trade-offs cedo
- [ ] Faço code review educado e útil
- [ ] Assumo ownership de pipelines em produção
- [ ] Peço e ofereço feedback regularmente
- [ ] Registro conquistas com métricas (tempo, custo, qualidade)

---

## Próximos passos na trilha

1. Pratique [Comunicação técnica](../communication/README.md)
2. Melhore vocabulário em [English for Data Engineers](../english/README.md)
3. Prepare narrativas em [Entrevistas](../interview/README.md)
4. Planeje estudo em [Roadmaps](../roadmaps/README.md)

> 💡 Além da técnica, a trilha [DataEngineer.help](https://dataengineer.help) enfatiza projetos e comunicação como diferencial de carreira.

---


---

## Conceitos que caem no quiz / entrevistas

### Feedback SBI e conflito
Situação → Comportamento → Impacto. Conflito: interesses, não ego.

### Mentoring, estimativa, async, dizer não
Delegue com contexto e autonomia. Estime com buffer/range. Async remoto com escrita clara. Diga não via trade-offs explícitos.

### Onboarding, blameless postmortem, STAR, ownership
Onboarding até o 1º PR. Postmortem sem culpa. STAR = Situation/Task/Action/Result. Ownership = ponta a ponta.

### Psychological safety; OKR vs KPI
Safety = falar riscos cedo. KPI = saúde contínua; OKR = objetivos ambiciosos por ciclo.

---

[← Voltar ao Awesome Data Engineering BR](../../README.md)
