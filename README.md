# Hoppscotch AIO Docker

## Overview

This project provides a complete Docker-based deployment of [Hoppscotch](https://hoppscotch.io) - a free, fast, and beautiful API request builder. Hoppscotch is an open-source alternative to Postman that runs entirely in your browser or as a desktop application.

### What is Hoppscotch?

Hoppscotch is a lightweight, web-based API development ecosystem that helps developers:
- Build and test REST, GraphQL, WebSocket, and other API requests
- Organize API collections and environments
- Collaborate with teams on API development
- Generate API documentation
- Mock API responses

### What this project provides

This Docker setup includes:
- **Hoppscotch AIO (All-in-One)**: The complete Hoppscotch application including frontend, backend API, and admin panel
- **PostgreSQL Database**: Persistent storage for user data, collections, and settings
- **Pre-configured Environment**: Ready-to-use configuration with sensible defaults

## Features

- 🚀 **One-command deployment** with Docker Compose
- 🔐 **Email authentication** (with optional SMTP configuration)
- 💾 **Persistent data storage** with PostgreSQL
- 🔧 **Fully configurable** through environment variables
- 📱 **Desktop app compatible** for connecting to your self-hosted instance

## Requirements

- **Docker** (version 20.10 or later) or **Podman**
- **Docker Compose** (version 2.0 or later) or **Podman Compose**
- **2GB RAM** minimum (4GB recommended)
- **1GB disk space** for the application and database

## Quick Start

### 1. Clone and Setup

```bash
git clone https://github.com/leoneljdias/hoppscotch-aio-docker.git
cd hoppscotch-aio-docker
```

### 2. Configure Environment (Optional)

Edit the `.env` file to customize your deployment:

```bash
# Basic configuration - change these for production
JWT_SECRET="your-secure-jwt-secret-here"
SESSION_SECRET="your-secure-session-secret-here"
DATA_ENCRYPTION_KEY="your-32-character-encryption-key-here"

# Your domain (if using a custom domain)
HOPPSCOTCH_HOST=localhost:5000
VITE_BASE_URL=http://localhost:5000
```

### 3. Start the Services

**Using Docker:**
```bash
docker compose up -d
```

**Using Podman:**
```bash
podman-compose up -d
```

### 4. Access Your Instance

- **Hoppscotch Web App**: [http://localhost:5000](http://localhost:5000)
- **Admin Panel**: [http://localhost:5000](http://localhost:5000/admin)

## Connecting Hoppscotch Desktop App

Add your self-hosted Hoppscotch instance to Hoppscotch Desktop App:

1. Open Hoppscotch Desktop App
2. Click the Hoppscotch logo in the top-left corner
3. Click "Add an instance"
4. Enter the URL of your self-hosted Hoppscotch instance (e.g., `http://localhost:3000`)
5. Click "Connect"

**Note**: Download the desktop app from [Hoppscotch Downloads](https://hoppscotch.com/download) if you haven't already.

## Configuration

### Environment Variables

Key configuration options in `.env`:

| Variable | Description | Default |
|----------|-------------|---------|
| `HOPPSCOTCH_HOST` | Your domain name | `hoppscotch.domain.com` |
| `JWT_SECRET` | Secret for JWT tokens | `secret1233` ⚠️ Change this |
| `SESSION_SECRET` | Session encryption secret | `XXXXXXXXXX` ⚠️ Change this |
| `DATA_ENCRYPTION_KEY` | 32-char encryption key | `abcdefghijklmnopqrstuvwxyz123456` |
| `VITE_ALLOWED_AUTH_PROVIDERS` | Authentication methods | `EMAIL` |

### SMTP Configuration (Optional)

To enable email sending (for password resets, etc.), configure SMTP:

```bash
MAILER_SMTP_ENABLE="true"
MAILER_USE_CUSTOM_CONFIGS="true"
MAILER_SMTP_HOST="your-smtp-server.com"
MAILER_SMTP_PORT="587"
MAILER_SMTP_SECURE="true"
MAILER_SMTP_USER="your-email@domain.com"
MAILER_SMTP_PASSWORD="your-app-password"
MAILER_ADDRESS_FROM="noreply@yourdomain.com"
```

## Configuration

## Production Deployment

### Security Considerations

For production deployments:

1. **Change default secrets**:
   ```bash
   JWT_SECRET="$(openssl rand -base64 32)"
   SESSION_SECRET="$(openssl rand -base64 32)"
   DATA_ENCRYPTION_KEY="$(openssl rand -base64 32 | cut -c1-32)"
   ```

2. **Use HTTPS**: Configure SSL/TLS with a reverse proxy like nginx or traefik
3. **Secure database**: Change the default PostgreSQL password
4. **Configure firewall**: Restrict access to necessary ports only
5. **Regular backups**: Backup your PostgreSQL data volume

### Domain Setup

1. Update `HOPPSCOTCH_HOST` in `.env` with your domain
2. Configure DNS to point to your server
3. Set up SSL certificates (Let's Encrypt recommended)
4. Configure a reverse proxy (nginx, traefik, etc.) to handle SSL termination

## Troubleshooting

### Common Issues

**Service won't start:**
```bash
# Check logs
docker compose logs hoppscotch-aio
docker compose logs hoppscotch-db
```

**Database connection issues:**
```bash
# Restart services
docker compose restart
```

**Desktop app won't connect:**
- Verify the instance URL is correct and accessible
- Check that ports are not blocked
- Ensure CORS origins are properly configured in `WHITELISTED_ORIGINS`

### Data Backup

```bash
# Backup database
docker exec hoppscotch-db pg_dump -U postgres hoppscotch > backup.sql

# Restore database
docker exec -i hoppscotch-db psql -U postgres hoppscotch < backup.sql
```

## Support

- **Documentation**: [Hoppscotch Docs](https://docs.hoppscotch.io)
- **Community**: [Discord](https://hoppscotch.io/discord)
- **Issues**: [GitHub Issues](https://github.com/hoppscotch/hoppscotch/issues)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

Hoppscotch is licensed under the MIT License - see the [Hoppscotch License](https://github.com/hoppscotch/hoppscotch/blob/main/LICENSE) for details.  
