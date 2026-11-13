---
name: profile-infrastructure
description: "Reglas específicas para infraestructura/DevOps (Docker, CI/CD, Terraform, Kubernetes)"
---

# Perfil: Infrastructure/DevOps

Reglas específicas para infraestructura como código, pipelines de CI/CD, contenedores y orquestación.

## Cuándo Cargar

| Indicadores | Acciona este perfil |
|-------------|---------------------|
| `Dockerfile`, `docker-compose.yml` | Containerization |
| `.github/workflows/*.yml` | GitHub Actions |
| `Jenkinsfile`, `.gitlab-ci.yml` | Jenkins/GitLab CI |
| `terraform/`, `main.tf` | Terraform/IaC |
| `kubernetes/`, `helm/` | K8s/Helm |
| `ansible/`, `chef/`, `puppet/` | Configuration management |
| `aws/`, `azure/`, `gcp/` | Cloud provider configs |

## Reglas Core

### Infrastructure as Code
- All infrastructure defined in code, not console clicks
- Version control all config files
- Idempotent operations (apply twice = same result)
- State management documented (remote state, backends)

### Security First
- No secrets in code (use environment variables, secret managers)
- Least privilege principle for all services
- Image vulnerability scanning in CI
- Network policies default-deny

### Immutability
- Prefer immutable deployments over mutable updates
- Blue/green or canary deployments when possible
- Rollback procedures tested and documented
- Configuration drift detection active

## Patterns Obligatorios

### Docker Best Practices
```dockerfile
# Multi-stage builds for smaller images
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

FROM node:20-alpine
WORKDIR /app
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/dist ./dist
USER node
CMD ["node", "dist/main.js"]
```

### Terraform Structure
```
infra/
├── modules/           # Reusable modules
│   ├── vpc/
│   ├── rds/
│   └── ecs/
├── environments/      # Environment-specific
│   ├── dev/
│   ├── staging/
│   └── prod/
└── state/             # Remote state configuration
```

### CI/CD Pipeline
```yaml
stages:
  - test
  - build
  - security-scan
  - deploy-staging
  - deploy-production
```

## Commands Comunes

| Task | Command |
|------|---------|
| Docker build | `docker build -t image:tag .` |
| Docker run | `docker run -d -p 8080:80 image:tag` |
| Terraform init | `terraform init -backend-config=...` |
| Terraform plan | `terraform plan -out=tfplan` |
| Terraform apply | `terraform apply tfplan` |
| Kubectl apply | `kubectl apply -f manifest.yaml` |
| Helm install | `helm install release chart/` |

## Anti-Patterns Específicos

| Anti-pattern | Problema | Solución |
|-------------|----------|----------|
| Hardcoded credentials in configs | Security breach risk | Use secret managers (AWS Secrets Manager, Vault) |
| Monolithic Dockerfiles | Slow builds, large images | Multi-stage builds, minimal base images |
| Direct cloud console changes | Drift from codebase | Enforce IaC only, disable manual changes |
| Single region deployment | Availability risk | Multi-region strategy for critical services |
| No rollback plan | Extended downtime on failure | Automated rollbacks, blue/green deployments |
| Unscanned images in production | Vulnerability exposure | Trivy/Snyk scans in CI pipeline |

## Security Checklist

- [ ] No hardcoded secrets in code
- [ ] Images scanned for vulnerabilities
- [ ] Networks use default-deny policies
- [ ] Services run as non-root user
- [ ] Minimum required permissions granted
- [ ] Audit logging enabled
- [ ] Backup/restore tested
- [ ] Disaster recovery documented

## Verification Checklist

- [ ] Infrastructure code passes linting/formatting
- [ ] Security scan shows no high/critical vulnerabilities
- [ ] Deployment is idempotent (safe to re-run)
- [ ] Rollback procedure documented and tested
- [ ] Monitoring/alerting configured
- [ ] Cost estimate reviewed
- [ ] Access controls documented
- [ ] Backup strategy in place
