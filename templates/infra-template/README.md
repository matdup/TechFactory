# 🚀 Infra Template - Tech Factory - Infrastructure as Code - multi cloud abstraction

>Production-ready Terraform infrastructure with enterprise security for OVH Cloud.
> Part of the [Tech Factory Framework](TechFactory/templates/infra-template/README.md)

---

## 🎯 Features

- ✅ **Private VPC** with secure subnets
- ✅ **Hardened Application Instance** with Docker
- ✅ **Managed PostgreSQL Database** with automated backups
- ✅ **Load Balancer** with health checks
- ✅ **Integrated Monitoring** (Node Exporter)
- ✅ **Zero Trust Security** (firewall, fail2ban)
- ✅ **Automated Database Backups**
- ✅ **OVH Infrastructure Alerting**

---

## 🚀 Quick Deployment

### Prerequisites

1. **OVH Cloud Account** with active project
2. **Terraform 1.6+** installed
3. **OVH Credentials** configured:

```bash
export OVH_ENDPOINT="ovh-eu"
export OVH_APPLICATION_KEY="your_app_key"
export OVH_APPLICATION_SECRET="your_app_secret" 
export OVH_CONSUMER_KEY="your_consumer_key"
```

### 10-Minute Deployment

```bash
cd infra-template/terraform

# Initialization
terraform init

# Planning
terraform plan -var="ovh_project_id=your_project_id"

# Deployment
terraform apply -var="ovh_project_id=your_project_id"

# Access application
echo "Application URL: http://$(terraform output -raw load_balancer_ip)"
```

---

## 🔧 Configuration

### Required Variables

```hcl
ovh_project_id = "your_ovh_project_id"  # OVH Project ID
```

### Optional Variables

```hcl
environment    = "production"           # development|staging|production
region         = "GRA"                  # GRA|SBG|DE|UK
instance_flavor = "d2-4"                # Instance type
database_plan  = "business"             # Database plan
```

---

## 🛡️ Security

### Implemented Measures

- 🔐 **Firewall (UFW)** with minimal rules
- 🚫 **Fail2Ban** for SSH protection
- 🐳 **Docker Hardening** with user namespace
- 📊 **Real-time Monitoring**
- 🔄 **Automated Database Backups**
- 📝 **Centralized Logging**

### Security Best Practices

**Restrict SSH Access:**
```hcl
ssh_allowed_cidr = "123.456.789.0/32"  # Your IP only
```

**Use Secure Secrets:**
```bash
# Never store in code!
export TF_VAR_ovh_project_id="your_project_id"
```

---

## 📊 Monitoring & Observability

### Available Metrics

- ✅ CPU/Memory usage via Node Exporter
- ✅ Disk space and IOPS
- ✅ Network traffic and errors
- ✅ Docker container health
- ✅ Application health checks

### Access Metrics

```bash
# System metrics
curl http://<server_ip>:9100/metrics

# Application health check
curl http://<load_balancer_ip>/health
```

---

## 🔄 CI/CD Integration

### GitHub Actions

```yaml
- name: Terraform Plan
  run: terraform plan -var="ovh_project_id=${{ secrets.OVH_PROJECT_ID }}"
  
- name: Terraform Apply
  if: github.ref == 'refs/heads/main'
  run: terraform apply -auto-approve -var="ovh_project_id=${{ secrets.OVH_PROJECT_ID }}"
```

### CI/CD Environment Variables

```yaml
env:
  OVH_ENDPOINT: ovh-eu
  OVH_APPLICATION_KEY: ${{ secrets.OVH_APPLICATION_KEY }}
  OVH_APPLICATION_SECRET: ${{ secrets.OVH_APPLICATION_SECRET }}
  OVH_CONSUMER_KEY: ${{ secrets.OVH_CONSUMER_KEY }}
```

---

## 📁 Project Structure

```
infra-template/terraform/
├── main.tf                 # Main configuration
├── variables.tf            # Variables and validation
├── outputs.tf              # Secure outputs
├── userdata.sh             # Initialization script
├── terraform.tfvars.example # Configuration example
└── README.md              # This documentation
```

---

## 🚨 Troubleshooting

### Common Issues

**OVH Authentication Error:**
```bash
# Verify credentials
ovh --endpoint=ovh-eu me
```

**Instance Not Starting:**
```bash
# Check logs
ssh user@instance_ip "sudo journalctl -u cloud-init"
```

**Database Inaccessible:**
```bash
# Check security rules
terraform output database_host
```

---

## 📞 Support

- 📚 OVH Documentation
- 🐛 GitHub Issues
- 💬 Discord

---

---

## 🛡️ CI/CD Integration

This template includes:
- **GitHub Actions** workflows (`ci.yml`, `security.yml`)
- Automated build, test, and deploy
- Security scanning (Trivy, Gitleaks, Snyk)
- Weekly compliance checks

---

## 🔒 Security Practices

- Zero secrets in code — use `.env` or GitHub Secrets
- Automated scanning on every push
- SOC2-aligned compliance via CI/CD
- Default firewall and container hardening

## 📄 License

MIT License - See LICENSE for details.


---

## 🧩 Related Templates
| Purpose | Template |
|----------|-----------|
| Infrastructure | [☁️ infra-template](../infra-template) |
| Monitoring | [📊 monitoring-template](../monitoring-template) |
| Documentation | [📚 docs-template](../docs-template) |

---

🧾 **License Notice**  
This repository is proprietary and shared for demonstration purposes only.  
Reuse, redistribution, or inclusion in other portfolios is strictly prohibited.  
See [LICENSE](../../LICENSE.md) for details.

---

📦 **Part of the Tech Factory Framework**  
Version: `v1.0` — Updated: 2025-11-03 