# Linux e Shell para Engenharia de Dados — grep, awk, jq, cron e SSH

> Domine **Linux** e o **terminal** para operar servidores, depurar **pipelines**, agendar jobs com **cron** e automatizar tarefas de **engenharia de dados**.

[← Índice](../../README.md) · [Docker](../docker/README.md) · [Airflow](../airflow/README.md) · [Recursos](../resources/README.md#linux) · [Git](../git/README.md)

---

## Por que Linux importa para o engenheiro de dados?

Quase todo servidor de **data engineering** — Airflow, Spark, bancos, bastion hosts — roda **Linux**. O dia a dia inclui logs, SSH, permissões, disco cheio e scripts de automação.

Um **engenheiro de dados** usa shell para:

- Inspecionar logs de DAGs e jobs Spark
- Filtrar CSVs/JSON com `grep`, `awk`, `jq`
- Agendar tarefas simples com **cron** (ou entender o que o Airflow substitui)
- Conectar via **SSH** e transferir arquivos (`scp`/`rsync`)

**Importância:** ⭐⭐⭐⭐

---

## O que você precisa dominar

| Tópico | Nível | Descrição |
|--------|-------|-----------|
| Navegação e arquivos | ⭐⭐⭐⭐⭐ | `cd`, `ls`, `find`, `du`, `df` |
| grep / awk / sed | ⭐⭐⭐⭐⭐ | Filtrar e transformar texto |
| jq | ⭐⭐⭐⭐ | JSON de APIs e logs |
| Permissões e usuários | ⭐⭐⭐⭐ | `chmod`, `chown`, sudo |
| Processos | ⭐⭐⭐⭐ | `ps`, `top`/`htop`, `kill` |
| cron / systemd timers | ⭐⭐⭐⭐ | Agendamento |
| SSH e túneis | ⭐⭐⭐⭐⭐ | Acesso seguro a servidores |

---

## Quando usar shell vs outras ferramentas

| Cenário | Ferramenta recomendada |
|---------|------------------------|
| Explorar log rápido | `grep` / `rg` + `tail` |
| Transformar CSV ad hoc | `awk` ou Python/pandas |
| JSON de API | `curl` + `jq` |
| Job recorrente simples | cron (ou Airflow se for pipeline) |
| Pipeline de dados real | Airflow / Prefect / Dagster |
| Ambiente reproduzível | [Docker](../docker/README.md) |

---

## Recursos recomendados

### Documentação e guias
- [Linux Journey](https://linuxjourney.com/) — gratuito e didático
- [GNU Grep Manual](https://www.gnu.org/software/grep/manual/)
- [jq Manual](https://jqlang.github.io/jq/manual/)

### Cursos e prática
- OverTheWire Bandit (exercícios de shell)
- Explicador de Cron do repositório: [tools/cron-expression-explainer/](../../tools/cron-expression-explainer/)

### Projetos práticos
- Script que baixa CSV, valida com `awk`/`jq` e sobe para S3/`aws s3`
- Cron que limpa logs antigos de um worker
- Alias e funções no `.bashrc` para rotina de DE

---

## Exemplos práticos

### grep, awk e jq no dia a dia

```bash
# Erros recentes no Airflow
grep "ERROR" /var/log/airflow/*.log | tail -20

# Colunas 1 e 3 de um CSV
awk -F',' '{print $1, $3}' dados.csv | head

# Campo de uma resposta JSON
curl -s https://api.exemplo.com/dados | jq '.results[0].name'

# Contar ocorrências de status
jq -r '.[].status' events.json | sort | uniq -c | sort -nr
```

### Monitorar recursos e disco

```bash
htop                          # CPU e memória
df -h                         # espaço em disco
du -sh /data/lake/*           # tamanho por diretório
free -h                       # memória
```

### SSH e transferência

```bash
ssh usuario@servidor-airflow
ssh -L 8080:localhost:8080 usuario@servidor   # túnel para UI local
scp arquivo.csv usuario@servidor:/data/inbox/
rsync -avz --progress ./out/ usuario@servidor:/data/out/
```

### Cron — exemplos comuns

```cron
# Minuto Hora Dia Mês DiaSemana Comando
0 6 * * * /opt/scripts/sync_dimensoes.sh
*/15 * * * * /usr/bin/curl -s http://localhost:8080/health >/dev/null
0 2 * * 0 find /var/log/jobs -name "*.log" -mtime +14 -delete
```

```bash
crontab -e    # editar
crontab -l    # listar
```

---

## Padrões úteis em produção

| Padrão | Quando usar | Exemplo |
|--------|-------------|---------|
| **Logs rotacionados** | Workers Airflow/Spark | `logrotate` ou retenção no app |
| **Script idempotente** | Cron / hooks | Verifica se já rodou hoje |
| **Exit codes** | Automação | `set -euo pipefail` no bash |
| **Least privilege** | SSH e jobs | Usuário dedicado, chave sem senha interativa |
| **Dry-run** | Scripts destrutivos | Flag `--dry-run` antes de apagar |

---

## Anti-padrões comuns

- **Rodar tudo como root** no servidor de dados
- **Hardcode de senhas** em scripts no home
- **Cron sem log** — redirecione stdout/stderr para arquivo
- **`rm -rf` sem dry-run** em paths montados do lake
- **Ignorar timezone** em cron vs Airflow (`TZ` / UTC)

---

## Checklist de domínio Linux/Shell

- [ ] Navego no filesystem e inspeciono disco/memória
- [ ] Extraio informação de logs com grep/awk
- [ ] Manipulo JSON com jq
- [ ] Configuro cron e entendo expressões
- [ ] Conecto via SSH e uso túneis quando preciso
- [ ] Escrevo scripts bash com `set -euo pipefail`
- [ ] Entendo permissões básicas (`chmod`/`chown`)

---

## Próximos passos na trilha

1. Empacote ambientes com [Docker](../docker/README.md)
2. Orquestre pipelines com [Airflow](../airflow/README.md) (além do cron)
3. Versionamento em [Git](../git/README.md)
4. Pratique perguntas de [entrevista](../interview/README.md)

> 💡 O módulo **Shell Script: Introdução e Automação de Tarefas** na trilha [DataEngineer.help](https://dataengineer.help) cobre automação no terminal.

---


---

## Conceitos que caem no quiz / entrevistas

### grep / awk / sed / jq
Filtram e transformam texto/JSON — dia a dia de logs de pipeline.

### Processos
- `SIGTERM` = graceful; `kill -9` = `SIGKILL` forçado (último recurso).
- `nohup cmd &` sobrevive ao logout SSH.
- `ps`, `top`/`htop` para CPU/memória.

### systemd vs cron
`journalctl -u serviço` lê logs. Timers systemd integram journal e dependências; cron clássico ainda aparece legado.

### Disco, memória, SSH, permissões
`df -h`, `du -sh`, `free -h`. SSH/scp/rsync para acesso e transferência. `chmod` altera rwx; `chown` altera dono.

---

[← Voltar ao Awesome Data Engineering BR](../../README.md)
