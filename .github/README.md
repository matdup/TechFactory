# 🛡️ GitHub Workflows — CI/CD Suite

> **Centralized CI/CD & Security Pipelines** for all CTO Factory repositories  
> Universal automation that adapts to each project type - backend, frontend, infrastructure, docs, or monitoring

This **single `.github` folder** contains universal pipelines that automatically detect and adapt to your project type.

---

## 🎯 Auto-Detection Magic

The workflows automatically detect your project type:

| Project Type | Detection File | Actions Triggered |
|--------------|----------------|------------------|
| **Backend** | `go.mod` | Go validation, testing, security |
| **Frontend** | `package.json` | Node.js validation, testing, security |
| **Infrastructure** | `terraform/main.tf` | Terraform validation, security, deployment |
| **Documentation** | `mkdocs.yml` | Docs build & deployment |
| **Monitoring** | Project structure | Health checks & metrics |

---

## 📄 Full Documentation

You can access the detailed pipeline documentation and audit overview here:

👉 **[CTO Factory Pipelines Overview (Google Doc)](https://docs.google.com/document/d/1Oa3UDlAzR4AjBUYPFZcczIed0R_gptSYDwXhxkSp7hs/edit?usp=sharing)**

This document includes:
- Full phase-by-phase breakdown (CI/CD + Security)
- Secrets and compliance requirements
- Audit and SOC2 alignment
- Future roadmap for reusable workflows

---

## 🔧 Workflows

| File | Purpose |
|------|----------|
| **ci.yml** | Full CI/CD pipeline — validation, testing, build, security scan, deployment, monitoring |
| **security.yml** | Deep Security Suite — SAST, DAST, IaC, secrets, SBOM, compliance |

---

## 🚀 Features
- **Zero-trust automation** (Trivy, Snyk, Gitleaks, Tfsec)
- **Multi-language support** (Go, Node.js, Terraform, Python)
- **Smart deployment** - auto-detects project type for deployment
- **SBOM + code coverage** artifacts
- **Slack + SARIF + Dashboard** reporting
- **Production-ready** deployment hooks

---

## 🔒 Security
All secrets are managed via **GitHub Secrets**, never stored in code.  
The workflows enforce:
- Secret scanning on every commit  
- Critical vulnerability blocking  
- IaC compliance validation
- Weekly security scans (Monday 6AM)

---

## ✅ Usage
Simply include this `.github` folder at the **root level**.

---

## 🧩 Advanced: Centralized Reusable Workflows
For large organizations, you can centralize these workflows in a single repo (e.g. `org/github-actions`)
and call them from others using:

```yaml
jobs:
  use-central-ci:
    uses: org/github-actions/.github/workflows/ci.yml@main
```

---
🧾 **License Notice**  
This repository is proprietary and shared for demonstration purposes only.  
Reuse, redistribution, or inclusion in other portfolios is strictly prohibited.  
See [LICENSE](../LICENSE.md) for details.
---

---

📦 **Part of the Tech Factory Framework**  
Version: `v1.0` — Updated: 2025-11-03  