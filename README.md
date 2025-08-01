# 🤖 Maubot Stack

A comprehensive Docker stack for running Maubot with certificate management solutions.

Maubot is a modular bot system for Matrix that allows you to easily create and manage bots with a web interface. Perfect for creating bridges between Matrix and other platforms.

## 🧩 Components

### 🔐 SSL Automation

#### [🔒 Let's Encrypt Manager](src/ssl-automation/letsencrypt-manager)

Automatic SSL certificate management from Let's Encrypt for production deployments. Provides seamless HTTPS integration for Docker containers using nginx-proxy and acme-companion.
[Learn more about Let's Encrypt Manager configuration](src/ssl-automation/letsencrypt-manager/README.md).

#### [🏠 Step CA Manager](src/ssl-automation/step-ca-manager)

Local domain stack with trusted self-signed certificates for virtual network deployments. Includes private CA management and local DNS resolution for development environments.
[Learn more about Step CA Manager configuration](src/ssl-automation/step-ca-manager/README.md).

## 🌐 Services

### 🤖 Maubot

**Location:** [`src/maubot/`](src/maubot/)

Modular bot system for Matrix with web management interface. Supports plugins, multiple bot instances, and integration with various Matrix homeservers.

### 🌉 Matrix Bridges

**Location:** [`src/matrix-bridges/`](src/matrix-bridges/)

Collection of bridges for connecting Matrix to other communication platforms (planned).

## 🔗 Integration Services

### 📡 RSShub

**Location:** [`src/integration-services/rsshub/`](src/integration-services/rsshub/)

RSS feed generator and aggregator service. Supports various sources including Telegram channels, social media platforms, and news sites. Includes Redis caching, Browserless Chrome integration, and authentication options.
[Learn more about RSShub configuration](src/integration-services/rsshub/README.md).

## 🎯 Use Cases

- **🌐 Production Deployment**: Use Maubot + Let's Encrypt Manager for public-facing Matrix bots
- **🏠 Internal Networks**: Use Maubot + Step CA Manager for private/development environments
- **🔧 Development**: Use Maubot standalone for local development
- **🤖 Bots and Automation**: Create Matrix bots with web management interface
- **🌉 Bridges**: Connect Matrix to other platforms (Telegram, Discord, etc.)
- **📡 RSS Aggregation**: Use RSShub for generating RSS feeds from various sources
- **🔗 Content Integration**: Combine RSShub with Maubot for RSS-to-Matrix notifications

## 🚀 Quick Start

Each component has its own README with detailed setup instructions. Choose the certificate management solution that fits your deployment scenario.

### For Maubot

1. Navigate to the maubot directory:

   ```bash
   cd src/maubot/
   ```

2. Build configurations:

   ```bash
   ./build.sh
   ```

3. Choose your desired configuration and follow instructions in [src/maubot/README.md](src/maubot/README.md)

## 📄 License

This project is dual-licensed under:

- [Apache License 2.0](LICENSE-APACHE)
- [MIT License](LICENSE-MIT)
