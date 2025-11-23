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
