# 🛡️ Monitoring Setup Guide

## 🎯 Overview

Complete observability stack for Tech Factory infrastructure featuring:
- 📊 **Metrics**: Prometheus + Node Exporter
- 📝 **Logs**: Loki + Promtail  
- 🚨 **Alerts**: Alertmanager
- 📈 **Visualization**: Grafana
- 🔔 **Uptime**: Uptime Kuma
- 🔐 **Secrets**: HashiCorp Vault

## 🚀 Quick Start

### 1. Prerequisites

```bash
# Install Docker & Docker Compose
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER

# Clone the monitoring template
git clone https://github.com/project-template/monitoring-template
cd monitoring-template

### 2. Environment Configuration
# Copy and configure environment
cp .env.example .env

# Edit .env with your settings
nano .env

# Required environment variables:
GRAFANA_ADMIN_PASSWORD=your_secure_password
DOMAIN_NAME=your-monitoring-domain.com

3. Deploy Monitoring Stack
# Start all services
docker-compose -f docker-compose.monitoring.yml up -d

# Verify services are running
docker-compose -f docker-compose.monitoring.yml ps

4. Access Dashboards
Grafana: http://localhost:3000 (admin/your_password)
Prometheus: http://localhost:9090
Alertmanager: http://localhost:9093
Uptime Kuma: http://localhost:3001
Vault UI: http://localhost:8300

🔧 Configuration Details

Prometheus Targets

Edit prometheus/prometheus.yml to add your application targets:
- job_name: 'your_app'
  static_configs:
    - targets: ['your-app-server:8080']
  metrics_path: /metrics
  scrape_interval: 30s

Grafana Data Sources

Data sources are auto-configured via provisioning. Check grafana/provisioning/datasources/datasources.yml

Alert Rules

Modify prometheus/alerting.yml to define custom alerts:

groups:
- name: instance
  rules:
  - alert: InstanceDown
    expr: up == 0
    for: 5m
    labels:
      severity: critical
    annotations:
      summary: "Instance {{ $labels.instance }} down"
      description: "{{ $labels.instance }} has been down for more than 5 minutes."

🛡️ Security Hardening

1. Network Security
# Configure firewall rules
ufw allow 3000/tcp comment 'Grafana'
ufw allow 9090/tcp comment 'Prometheus'
ufw allow 9093/tcp comment 'Alertmanager'
ufw --force enable


2. SSL/TLS Configuration

# Add to docker-compose.monitoring.yml
nginx:
  image: nginx:alpine
  ports:
    - "443:443"
  volumes:
    - ./nginx/nginx.conf:/etc/nginx/nginx.conf
    - ./ssl/:/etc/nginx/ssl/


3. Authentication

Enable Grafana authentication:
# In grafana.ini
[auth]
disable_login_form = false
[auth.anonymous]
enabled = false

📊 Monitoring Best Practices

1. Key Metrics to Monitor

Metric	Alert Threshold	Description
CPU Usage	> 80% for 5m	High CPU utilization
Memory Usage	> 90% for 5m	Memory pressure
Disk Usage	> 85%	Low disk space
Service Uptime	< 1 for 2m	Service down
HTTP Errors	> 5% for 5m	High error rate


2. Alerting Strategy

P1 Critical: Immediate notification (SMS/Slack)
P2 High: Notification within 15 minutes
P3 Medium: Daily digest
P4 Low: Weekly review


3. Log Retention

Application logs: 30 days
Audit logs: 1 year
Security logs: 2 years


🔄 Maintenance

Daily Checks

Review alert dashboard
Check service health
Verify backup status
Review security scans


Weekly Tasks

Update container images
Review log patterns
Check storage usage
Validate backup restoration


Monthly Tasks

Security audit
Performance review
Capacity planning
Documentation update


🚨 Troubleshooting

Common Issues

1 Prometheus not scraping

bash
# Check target status
curl http://localhost:9090/api/v1/targets


2Grafana login issues

bash
# Reset admin password
docker exec -it grafana grafana-cli admin reset-admin-password newpassword


3 High memory usage

bash
# Check Prometheus memory
docker stats prometheus


Log Locations

Prometheus: /var/lib/docker/volumes/prometheus_data
Grafana: /var/lib/docker/volumes/grafana_data
Loki: /var/lib/docker/volumes/loki_data

📞 Support

📚 Documentation
🐛 Issues
💬 Slack
🚨 Emergency


🔗 Useful Links

Prometheus Documentation
Grafana Documentation
Loki Documentation
Alertmanager Documentation