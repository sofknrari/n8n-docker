# n8n-docker
Easiest way to deploy n8n service with your own domain by a few steps

# 🚀 N8N Deployment with SSL & Reverse Proxy

<div align="center">

![N8N Logo](https://raw.githubusercontent.com/n8n-io/n8n/master/docs/static/img/n8n-logo.png)

### Automated workflow platform with secure HTTPS access and automatic SSL renewal

[![Docker](https://img.shields.io/badge/Docker-✓-blue?logo=docker)](https://docker.com)
[![SSL](https://img.shields.io/badge/SSL-Let's%20Encrypt-green?logo=letsencrypt)](https://letsencrypt.org)
[![Nginx](https://img.shields.io/badge/Proxy-Nginx-success?logo=nginx)](https://nginx.org)

</div>

## 📋 Overview

This repository provides a complete Docker Compose setup for deploying **N8N** with:
- 🔒 **Automatic HTTPS** via Let's Encrypt
- 🌐 **Reverse Proxy** with Nginx
- 🔄 **Auto-renewal** of SSL certificates
- 🏠 **Custom domain** support
- 🐳 **Containerized** architecture

## 🛠 Prerequisites

Before deployment, ensure you have:

- ✅ **Docker** and **Docker Compose** installed
- ✅ **Domain name** pointing to your server IP
- ✅ **Ports 80 & 443** open on your firewall
- ✅ **Email address** for SSL certificates

## 🚀 Quick Start

### 1. Clone & Setup
```bash
git clone <your-repo-url>
cd n8n-deployment
mkdir -p certs vhost html data
```
2. Configuration
Update the docker-compose.yml file:

```yaml
environment:
  - DEFAULT_EMAIL=your-real-email@domain.com  # ✏️ Replace with your email
```
3. DNS Configuration
Ensure your domain points to your server IP:

```dns
example.com.    A    xx.xx.xx.xx
```
4. Deployment
```bash
docker-compose up -d
```
5. Verification
Check if all services are running:

```bash
docker-compose ps
```
📁 Project Structure
text
n8n-deployment/
├── 📄 docker-compose.yml          # Main deployment file
├── 📄 docker-compose.override.yml # Domain configuration
├── 📁 data/                       # N8N persistent data
├── 📁 certs/                      # SSL certificates (auto-generated)
├── 📁 vhost/                      # Nginx virtual hosts
├── 📁 html/                       # Web root for challenges
└── 📄 README.md                   # This file
🔧 Services Architecture
```
graph LR
    A[User] --> B[443:HTTPS]
    A --> C[80:HTTP]
    B --> D[Nginx Proxy]
    C --> D
    D --> E[SSL Companion]
    D --> F[N8N App]
    E --> G[Let's Encrypt]
```

🌐 Access Points
Service	URL	Port	Purpose
N8N Web UI	https://example.com	443	Main application
HTTP Redirect	http://example.com	80	Auto-redirect to HTTPS
Internal N8N	http://localhost:5678	5678	Direct container access
🔒 SSL Features
✅ Automatic issuance of Let's Encrypt certificates

✅ Auto-renewal 30 days before expiration

✅ HTTP to HTTPS automatic redirect

✅ Secure cookies enabled

✅ HSTS headers (recommended)

📊 Monitoring & Logs
Check service status:
```bash
docker-compose logs n8n
docker-compose logs nginx-proxy
docker-compose logs ssl-companion
```
Monitor SSL certificates:
```bash
docker exec ssl-companion ls -la /etc/nginx/certs
```
Force certificate renewal:
```bash
docker exec ssl-companion /app/force_renew
```
⚙️ Environment Variables
Variable	Purpose	Default
VIRTUAL_HOST	Domain name	example.com
LETSENCRYPT_HOST	SSL domain	example.com
DEFAULT_EMAIL	SSL contact	Your email
N8N_EDITOR_BASE_URL	Public URL	https://example.com/
🛡️ Security Notes
🔐 Never expose port 5678 directly to internet

📧 Use valid email for certificate notifications

🔄 Keep Docker updated for security patches

💾 Regular backups of ./data directory

🚨 Troubleshooting
Common Issues:
SSL not working

Check DNS propagation

Verify ports 80/443 are open

Check companion logs for ACME errors

N8N inaccessible

```bash
docker-compose restart n8n nginx-proxy
```
Certificate renewal failing

```bash
docker-compose down && docker-compose up -d
```
📝 Maintenance
Update all services:
```bash
docker-compose pull
docker-compose up -d
```
Backup data:
```bash
tar -czf n8n-backup-$(date +%Y%m%d).tar.gz ./data
```
Restore from backup:
```bash
tar -xzf n8n-backup-YYYYMMDD.tar.gz
```
🤝 Contributing
Feel free to:

🐛 Report bugs

💡 Suggest features

🔧 Submit pull requests

📚 Improve documentation
