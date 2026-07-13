# Terraform IaC para Engenharia de Dados — S3, IAM e Warehouses

> Aprenda **Terraform** para provisionar infraestrutura de **dados** na nuvem: **S3**, **IAM**, catálogos, warehouses e redes com **Infrastructure as Code**.

[← Índice](../../README.md) · [Cloud](../cloud/README.md) · [Docker](../docker/README.md) · [Git](../git/README.md) · [Recursos](../resources/README.md#terraform)

---

## Por que Terraform para data engineering?

Pipelines precisam de buckets, roles, networks e warehouses. Fazer isso só no console gera drift e ambiente irreproduzível. **Terraform** declara a infra em código versionado no **Git**, com plan/apply revisáveis em PR.

Um **engenheiro de dados** (ou DE + plataforma) usa Terraform para:

- Criar buckets S3/GCS/ADLS com lifecycle e encryption
- Definir IAM least-privilege para jobs e usuários
- Provisionar Redshift, BigQuery datasets, Snowflake resources (via providers)
- Padronizar ambientes dev/staging/prod

**Importância:** ⭐⭐⭐⭐

---

## O que você precisa dominar

| Tópico | Nível | Descrição |
|--------|-------|-----------|
| Providers e resources | ⭐⭐⭐⭐⭐ | AWS/GCP/Azure basics |
| State e backend remoto | ⭐⭐⭐⭐⭐ | S3 + DynamoDB / Terraform Cloud |
| Variables e outputs | ⭐⭐⭐⭐⭐ | Módulos reutilizáveis |
| Modules | ⭐⭐⭐⭐ | Bucket + IAM como bloco |
| Workspaces / envs | ⭐⭐⭐⭐ | dev vs prod |
| Plan em CI | ⭐⭐⭐⭐ | PR com diff de infra |
| Import e drift | ⭐⭐⭐ | Trazer recurso existente |

---

## Quando usar Terraform vs alternativas

| Cenário | Ferramenta recomendada |
|---------|------------------------|
| Infra multi-cloud declarativa | **Terraform** / OpenTofu |
| Só AWS e time nativo AWS | CloudFormation / CDK |
| Apps em Kubernetes | Helm + Terraform para cluster |
| Só transformações SQL | **dbt** (não é IaC de cloud) |
| Experimento rápido único | Console (depois importe para TF) |

---

## Recursos recomendados

### Documentação oficial
- [Terraform Docs](https://developer.hashicorp.com/terraform/docs)
- [AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
- [Exemplos AWS](https://github.com/hashicorp/terraform-provider-aws/tree/main/examples)

### Cursos e labs
- HashiCorp Learn — Terraform Associate (trilhas gratuitas)
- Workshops oficiais de remote state

### Projetos práticos
- S3 data lake + IAM role para Glue/Airflow
- Bucket versionado + lifecycle para raw/bronze
- Dataset BigQuery ou schema Snowflake via provider

---

## Exemplos práticos

### S3 bucket para data lake (AWS)

```hcl
resource "aws_s3_bucket" "lake" {
  bucket = "empresa-dados-lake-${var.env}"
}

resource "aws_s3_bucket_versioning" "lake" {
  bucket = aws_s3_bucket.lake.id
  versioning_configuration {
    status = "Enabled"
  }
}

resource "aws_s3_bucket_server_side_encryption_configuration" "lake" {
  bucket = aws_s3_bucket.lake.id
  rule {
    apply_server_side_encryption_by_default {
      sse_algorithm = "AES256"
    }
  }
}

resource "aws_s3_bucket_public_access_block" "lake" {
  bucket                  = aws_s3_bucket.lake.id
  block_public_acls       = true
  block_public_policy     = true
  ignore_public_acls      = true
  restrict_public_buckets = true
}
```

### IAM role mínima para job de ingestão

```hcl
resource "aws_iam_role" "ingest" {
  name = "de-ingest-${var.env}"
  assume_role_policy = jsonencode({
    Version = "2012-10-17"
    Statement = [{
      Effect    = "Allow"
      Principal = { Service = "ec2.amazonaws.com" }
      Action    = "sts:AssumeRole"
    }]
  })
}

resource "aws_iam_role_policy" "ingest_s3" {
  name = "s3-raw-write"
  role = aws_iam_role.ingest.id
  policy = jsonencode({
    Version = "2012-10-17"
    Statement = [{
      Effect   = "Allow"
      Action   = ["s3:PutObject", "s3:GetObject", "s3:ListBucket"]
      Resource = [
        aws_s3_bucket.lake.arn,
        "${aws_s3_bucket.lake.arn}/raw/*"
      ]
    }]
  })
}
```

### Fluxo local

```bash
terraform init
terraform plan -var="env=dev" -out=tfplan
terraform apply tfplan
terraform state list
```

---

## Padrões IaC para dados

| Padrão | Quando usar | Exemplo |
|--------|-------------|---------|
| **Remote state** | Time > 1 pessoa | Backend S3 + lock |
| **Módulo lake** | Vários buckets/camadas | module `data_lake` |
| **Least privilege IAM** | Jobs e usuários | Policy só no prefixo `raw/` |
| **Plan no PR** | Governança | GitHub Actions + comment |
| **Tags obrigatórias** | Custo e ownership | `project`, `owner`, `env` |

---

## Anti-padrões comuns

- **State local no laptop** compartilhado por várias pessoas
- **Credenciais no `.tf`** — use variables, env ou OIDC
- **`*` em Action/Resource** sem necessidade
- **Apply sem plan revisado** em prod
- **Misturar lógica de negócio ETL** dentro do Terraform

---

## Checklist de domínio Terraform

- [ ] Escrevo resources básicos (S3, IAM) do zero
- [ ] Uso remote state com locking
- [ ] Organizo código em modules e variáveis
- [ ] Rodo plan/apply com segurança por ambiente
- [ ] Evito secrets no código e no state (sensitive)
- [ ] Integro `terraform plan` no CI de PRs
- [ ] Entendo drift e `terraform import` básico

---

## Próximos passos na trilha

1. Aprofunde provedores em [Cloud](../cloud/README.md)
2. Versionamento e PRs em [Git](../git/README.md)
3. Ambientes locais com [Docker](../docker/README.md)
4. Arquitetura alvo em [Architecture](../architecture/README.md) e [Lakehouse](../lakehouse/README.md)

> 💡 O módulo **Infra como Código (Terraform + dbt Cloud)** está previsto na trilha [DataEngineer.help](https://dataengineer.help).

---

[← Voltar ao Awesome Data Engineering BR](../../README.md)
