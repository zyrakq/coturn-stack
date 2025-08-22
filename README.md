# 🔄 COTURN Stack

A simple Docker-based COTURN server setup for WebRTC applications 🚀

## 📋 What is COTURN?

COTURN is a free open-source implementation of TURN and STUN servers for VoIP and WebRTC. It helps establish peer-to-peer connections when direct communication between clients is not possible due to NAT/firewall restrictions.

## ✨ Features

- 🐳 **Docker-based deployment** - Easy setup and management
- 🔒 **Authentication support** - Secure access with secret-based auth
- 🌐 **Multiple protocols** - Supports both TCP and UDP
- ⚡ **Production-ready** - Configured for real-world usage
- 🔧 **Simple configuration** - Environment-based setup

## 🚀 Quick Start

### Prerequisites

- Docker and Docker Compose installed 📦
- Basic understanding of WebRTC concepts 🧠

### Setup

1. **Clone the repository** 📥

   ```bash
   git clone <repository-url>
   cd coturn-stack
   ```

2. **Configure environment** ⚙️

   ```bash
   cd src
   cp .env.example .env
   ```

3. **Edit configuration** ✏️

   ```bash
   nano .env
   ```

   Update the following variables:
   - `COTURN_SECRET_KEY` - Your secret key for authentication
   - `COTURN_DOMAIN` - Your domain name

4. **Start the server** 🎯

   ```bash
   docker-compose up -d
   ```

## 🔧 Configuration

### Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `COTURN_SECRET_KEY` | Secret key for authentication | `Z11ZugvTopHBxq4FatCOKV52vghfFKE8...` |
| `COTURN_DOMAIN` | Your domain/realm | `example.com` |

### Ports

| Port | Protocol | Description |
|------|----------|-------------|
| `3478` | TCP/UDP | STUN/TURN server |
| `5349` | TCP/UDP | STUN/TURN over TLS |
| `49152-65535` | UDP | Media relay ports |

## 🔍 Usage

### Testing the Server

You can test your COTURN server using online STUN/TURN testers or WebRTC applications.

### Integration

Use the following configuration in your WebRTC applications:

```javascript
const iceServers = [
  {
    urls: 'stun:your-domain.com:3478'
  },
  {
    urls: 'turn:your-domain.com:3478',
    username: 'your-username',
    credential: 'your-secret-key'
  }
];
```

## 🛠️ Management

### View logs

```bash
docker-compose logs -f turn
```

### Restart service

```bash
docker-compose restart turn
```

### Stop service

```bash
docker-compose down
```

## 🔒 Security Considerations

- 🔑 Use a strong, randomly generated secret key
- 🌐 Configure proper firewall rules
- 🔄 Regularly update the COTURN image
- 📊 Monitor server usage and logs

## 📚 Resources

- [COTURN Official Documentation](https://github.com/coturn/coturn)
- [WebRTC Documentation](https://webrtc.org/)
- [Docker Compose Reference](https://docs.docker.com/compose/)

## 📄 License

This project is dual-licensed under:

- Apache License 2.0
- MIT License

Choose the license that best fits your needs! 🎉

## 🤝 Contributing

Contributions are welcome! Please feel free to submit issues and pull requests.

---

Made with ❤️ for the WebRTC community
