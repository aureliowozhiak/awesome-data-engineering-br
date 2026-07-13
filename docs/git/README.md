# Git & GitHub para Engenharia de Dados — Branching, PRs e Commits

> Aprenda **Git** e **GitHub** para versionar **pipelines**, modelos **dbt**, DAGs **Airflow** e infraestrutura com **branching**, **Pull Requests** e **Conventional Commits**.

[← Índice](../../README.md) · [dbt](../dbt/README.md) · [Airflow](../airflow/README.md) · [Recursos](../resources/README.md#git) · [Comunicação](../communication/README.md)

---

## Por que Git é obrigatório em data engineering?

Todo projeto moderno de **engenharia de dados** vive em repositório: transformações **dbt**, DAGs do **Airflow**, jobs **Spark** e código **Terraform**. Sem **Git**, não há revisão, rollback nem CI.

Um **engenheiro de dados** usa Git diariamente para:

- Versionar SQL, Python e configs de pipeline
- Abrir PRs com testes (`dbt build`, lint, unit tests)
- Colaborar com analytics e plataforma via code review
- Rastrear mudanças que quebraram produção (blame/bisect)

**Importância:** ⭐⭐⭐⭐⭐

---

## O que você precisa dominar

| Tópico | Nível | Descrição |
|--------|-------|-----------|
| clone, status, add, commit, push | ⭐⭐⭐⭐⭐ | Fluxo básico |
| Branching e merge | ⭐⭐⭐⭐⭐ | Feature branches |
| Pull Requests / Code review | ⭐⭐⭐⭐⭐ | Qualidade e alinhamento |
| Conventional Commits | ⭐⭐⭐⭐ | Histórico legível e changelog |
| Rebase e resolve conflitos | ⭐⭐⭐⭐ | Histórico limpo |
| `.gitignore` e secrets | ⭐⭐⭐⭐⭐ | Não versionar credenciais |
| GitHub Actions (visão) | ⭐⭐⭐ | CI de dbt/Airflow |

---

## Quando usar cada fluxo

| Cenário | Prática recomendada |
|---------|---------------------|
| Mudança pequena em SQL/dbt | Branch curta + PR com testes |
| Feature grande (novo pipeline) | Branch longa + PRs incrementais |
| Hotfix em produção | Branch `fix/` + review rápida |
| Experimentos locais | Branch descartável (não force-push em shared) |
| Release de infra | PR com `terraform plan` no CI |

---

## Recursos recomendados

### Documentação oficial
- [Pro Git Book (PT-BR)](https://git-scm.com/book/pt-br/v2) — gratuito
- [GitHub Docs](https://docs.github.com/)
- [Conventional Commits](https://www.conventionalcommits.org/)

### Cursos e labs gratuitos
- [GitHub Skills](https://skills.github.com/) — tutoriais interativos
- [Learn Git Branching](https://learngitbranching.js.org/) — visual e prático

### Projetos práticos
- Repo dbt com PR template e `dbt build` no CI
- Monorepo de DAGs Airflow com lint no GitHub Actions
- Conventional Commits + changelog automático

---

## Exemplos práticos

### Fluxo feature → PR

```bash
git checkout -b feat/stg-orders-incremental
# ... edita models/staging/stg_orders.sql
git add models/staging/stg_orders.sql
git commit -m "feat(dbt): torna stg_orders incremental por updated_at"
git push -u origin HEAD
# Abra o PR no GitHub e peça review
```

### Conventional Commits — tipos úteis para DE

```text
feat(airflow): adiciona DAG de ingestão CRM
fix(dbt): corrige join duplicado em fct_orders
docs(readme): atualiza setup do ambiente local
chore(ci): roda dbt test em pull requests
refactor(spark): extrai função de deduplicação
perf(sql): particiona tabela de eventos por data
```

### `.gitignore` típico de projeto de dados

```gitignore
.env
*.pem
credentials.json
.dbt/logs/
target/
__pycache__/
.venv/
*.parquet
data/raw/
```

### Resolver conflito com calma

```bash
git fetch origin
git rebase origin/main
# resolve arquivos em conflito
git add .
git rebase --continue
git push --force-with-lease
```

---

## Branching para times de dados

| Branch | Uso |
|--------|-----|
| `main` / `master` | Produção estável |
| `feat/*` | Nova feature ou modelo |
| `fix/*` | Correção urgente |
| `chore/*` | CI, deps, limpeza |
| `docs/*` | Só documentação |

**Regra prática:** PRs pequenos (< 400 linhas quando possível) revisam mais rápido e quebram menos pipelines.

---

## Checklist de domínio Git/GitHub

- [ ] Crio branches, commits e PRs com confiança
- [ ] Escrevo mensagens no padrão Conventional Commits
- [ ] Nunca committo secrets (`.env`, keys, tokens)
- [ ] Resolvo conflitos de merge/rebase
- [ ] Uso template de PR (contexto, testes, riscos)
- [ ] Entendo `force-with-lease` vs `force`
- [ ] Configuro ou leio workflows básicos de CI

---

## Próximos passos na trilha

1. Aplique versionamento em [dbt](../dbt/README.md) e [Airflow](../airflow/README.md)
2. Melhore PRs com [Comunicação técnica](../communication/README.md)
3. Automatize deploy com CI em [Recursos](../resources/README.md#cicd)
4. Infra versionada com [Terraform](../terraform/README.md)

> 💡 O módulo **Git & GitHub para Engenheiros de Dados** está previsto na trilha [DataEngineer.help](https://dataengineer.help).

---


---

## Conceitos que caem no quiz / entrevistas

### Commit, branch, PR
Commit = snapshot + mensagem. Branch = linha paralela. PR = merge com review.

### Conventional Commits
Prefixos `feat:`, `fix:`, `docs:` — histórico legível e changelog.

### Merge vs rebase; reset vs revert
- **Merge** preserva histórico das branches.
- **Rebase** lineariza (só use em commits locais/não compartilhados).
- **`reset --soft`**: move HEAD mantendo stage.
- **`revert`**: novo commit que desfaz (seguro em main). Não force-push em main.

### Bisect, stash, .gitignore, conflitos
- `bisect`: busca binária do commit quebrou.
- `stash`: guarda WIP temporariamente.
- `.gitignore`: nunca versionar `.env`/secrets.
- Conflito: edite marcadores → `git add` → conclua merge/rebase.

---

[← Voltar ao Awesome Data Engineering BR](../../README.md)
