# 🌐 COTURN Stack

Complete Docker-based COTURN TURN/STUN server deployment with SSL certificate management for WebRTC applications and Matrix homeserver integration.

## 🧩 Components

### 🔐 SSL Automation

#### [🔒 Let's Encrypt Manager](src/ssl-automation/letsencrypt-manager)

Automatic SSL certificate management from Let's Encrypt for production deployments. Provides seamless HTTPS integration for Docker containers using nginx-proxy and acme-companion.
[Learn more about Let's Encrypt Manager configuration](src/ssl-automation/letsencrypt-manager/README.md).

#### [🏠 Step CA Manager](src/ssl-automation/step-ca-manager)

Local domain stack with trusted self-signed certificates for virtual network deployments. Includes private CA management and local DNS resolution for development environments.
[Learn more about Step CA Manager configuration](src/ssl-automation/step-ca-manager/README.md).

### 🔄 [COTURN Server](src/coturn/)

Modular Docker Compose configuration system for COTURN TURN/STUN server with support for multiple environments and SSL certificate integration. Provides production-ready TURN server deployment for WebRTC applications and Matrix homeserver voice/video calling.
[Learn more about COTURN configuration](src/coturn/README.md).

## 🚀 Quick Start

Each component has its own README with detailed setup instructions. Choose the certificate management solution that fits your deployment scenario.

### Basic Setup

1. **Choose SSL Management:**
   - Production: Use Let's Encrypt Manager
   - Development: Use Step CA Manager

2. **Deploy COTURN Server:**
   - Configure COTURN with desired environment and SSL settings

### Example Deployment

```bash
# 1. Build COTURN configurations
cd src/coturn/
sb build

# 2. Choose your deployment scenario
# For basic deployment
cd build/basic/

# For production with Let's Encrypt
cd build/letsencrypt/

# For production with Step CA
cd build/step-ca/

# 3. Configure environment
cp .env.example .env
# Edit .env with your values

# 4. Deploy
docker-compose up -d
```

## 🏗️ Architecture

```sh
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  WebRTC Client  │────│  COTURN Server  │────│  SSL Manager    │
│ (Browser/App)   │    │ (TURN/STUN)     │    │ (Let's Encrypt/ │
│                 │    │                 │    │  Step CA)       │
└─────────────────┘    └─────────────────┘    └─────────────────┘
          │                       │
          │                       │
┌─────────────────┐    ┌─────────────────┐
│ Matrix Client   │    │  Media Relay    │
│ (Element/Cinny) │    │  (UDP/TCP)      │
└─────────────────┘    └─────────────────┘
```

## 📋 Requirements

- Docker & Docker Compose
- Domain name (for production deployments)
- Email address (for Let's Encrypt)
- `yq` tool for configuration building
- Basic understanding of WebRTC concepts

## 🔧 Configuration

All services use modular Docker Compose configurations with:

- **Base components**: Core service definitions
- **Environment components**: Development, production, SSL configurations
- **Build system**: Automatic generation of deployment combinations

## 🌍 Deployment Scenarios

### Basic Deployment

```bash
# COTURN with basic configuration
cd src/coturn/build/basic/
docker-compose up -d
```

### Production Environment

```bash
# COTURN with Let's Encrypt SSL
cd src/coturn/build/letsencrypt/
docker-compose up -d

# COTURN with Step CA SSL
cd src/coturn/build/step-ca/
docker-compose up -d
```

## 🔐 Security Features

- **SSL/TLS Encryption**: Automatic certificate management
- **Authentication**: Secret-based TURN authentication
- **Network Isolation**: Docker network segmentation
- **Secret Management**: Environment-based configuration
- **Access Control**: Domain-based realm configuration

## 🎯 COTURN Features

- **Docker-based**: Containerized deployment with official COTURN image
- **Authentication**: Secure access with secret-based auth
- **Multiple Protocols**: Supports both TCP and UDP for STUN/TURN
- **SSL Support**: Full SSL/TLS support with Let's Encrypt and Step CA
- **Production-ready**: Configured for real-world usage
- **Simple Configuration**: Environment-based setup
- **Matrix Integration**: Ready for Matrix homeserver voice/video calling

## ⚙️ Advanced Configuration

### Ports

| Port | Protocol | Description |
|------|----------|-------------|
| `3478` | TCP/UDP | STUN/TURN server |
| `5349` | TCP/UDP | STUN/TURN over TLS |
| `49152-65535` | UDP | Media relay ports |

### Environment Variables

- `COTURN_SECRET_KEY`: Secret key for TURN authentication
- `COTURN_DOMAIN`: Your domain/realm
- `COMPOSE_PROJECT_NAME`: Project name for Docker Compose

## 🆘 Troubleshooting

### Common Issues

- **SSL Certificate Issues**: Check Let's Encrypt/Step CA configuration
- **Network Connectivity**: Ensure proper Docker network configuration
- **Port Conflicts**: Verify required ports are available
- **Authentication Issues**: Check secret key configuration

### Logs

```bash
# COTURN logs
docker logs coturn

# SSL automation logs
docker logs nginx-proxy
docker logs letsencrypt-companion  # or step-ca-manager
```

## 📚 Documentation

- [COTURN Server Configuration](src/coturn/README.md)
- [SSL Automation](src/ssl-automation/)
- [Official COTURN Documentation](https://github.com/coturn/coturn)
- [WebRTC Documentation](https://webrtc.org/)

## 🔗 Integration

### Matrix Homeserver Integration

COTURN integrates seamlessly with Matrix homeservers for voice and video calling:

```bash
# Example Matrix TURN configuration
CONDUIT_TURN_URIS='["turns:your-domain.com?transport=udp", "turns:your-domain.com?transport=tcp"]'
# OR turn:your-domain.com for without TLS
CONDUIT_TURN_SECRET=your-coturn-secret-key
```

### WebRTC Application Integration

Popular applications that can use COTURN:

- **Matrix Clients**: Element, Cinny, FluffyChat
- **Video Conferencing**: Jitsi, BigBlueButton
- **Communication Platforms**: Nextcloud Talk, Mattermost

## 🔒 Security Considerations

- 🔑 Use a strong, randomly generated secret key
- 🌐 Configure proper firewall rules for TURN ports
- 🔄 Regularly update the COTURN image
- 📊 Monitor server usage and logs
- 🔒 Enable SSL/TLS for production deployments

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test configurations
5. Submit a pull request

## 📄 License

This project is dual-licensed under:

- [Apache License 2.0](LICENSE-APACHE)
- [MIT License](LICENSE-MIT)

## 🔗 Related Projects

- [COTURN](https://github.com/coturn/coturn) - TURN and STUN server implementation
- [WebRTC.org](https://webrtc.org/) - Open project for web real-time communication
- [Matrix.org](https://matrix.org/) - Open network for secure, decentralized communication
- [Let's Encrypt](https://letsencrypt.org/) - Free SSL certificates
- [Smallstep](https://smallstep.com/) - Private certificate authority
