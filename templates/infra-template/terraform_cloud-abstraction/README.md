```markdown
# 🌍 TechFactory Multi-Cloud Infrastructure

Deploy the same infrastructure on OVH, AWS, or Azure with a single command.

## 🚀 Quick Start

```bash
# OVH
terraform apply -var="cloud_provider=ovh" -var="ovh_project_id=your_project_id"

# AWS  
terraform apply -var="cloud_provider=aws"

# Azure
terraform apply -var="cloud_provider=azure"
```

## 📋 Configuration

1. **Copy the configuration template:**
   ```bash
   cp terraform.tfvars.example terraform.tfvars
   ```

2. **Edit `terraform.tfvars` with your settings:**
   ```hcl
   cloud_provider = "ovh"  # or "aws", "azure"
   project_name = "your-project"
   environment = "staging"
   # ... other variables
   ```

3. **Deploy:**
   ```bash
   terraform apply
   ```

## ☁️ Supported Clouds

| Cloud | Status | Requirements |
|-------|--------|--------------|
| **OVH** | ✅ Production Ready | OVH Project ID |
| **AWS** | ✅ Production Ready | AWS Credentials |
| **Azure** | ✅ Production Ready | Azure Service Principal |

## 🏗️ Architecture

- **VPC/VNet** with private subnets
- **Load Balancer** with health checks
- **Virtual Machine** with Docker & monitoring
- **Managed PostgreSQL** database
- **Security Groups** with zero-trust rules
- **Monitoring** with alerts and dashboards

## 🔐 Security Features

- Automated security scanning in CI/CD
- Secrets management with HashiCorp Vault
- Encrypted storage and communications
- Network isolation and firewall rules

## 📊 Outputs

After deployment, you'll get:
- Application URL
- Database connection details
- Instance information
- Monitoring endpoints

## 🛠️ Requirements

- Terraform >= 1.6.0
- Cloud provider credentials
- SSH key for instance access

## ❓ Troubleshooting

See the main project documentation or check the deployment logs in the cloud provider's console.
```

---
🧾 **License Notice**  
This repository is proprietary and shared for demonstration purposes only.  
Reuse, redistribution, or inclusion in other portfolios is strictly prohibited.  
See [LICENSE](../../../LICENSE.md) for details.

---

📦 **Part of the Tech Factory Framework**  
Version: `v1.0` — Updated: 2025-11-03 