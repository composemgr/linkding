## 👋 Welcome to linkding 🚀

Self-hosted bookmark manager with tagging and browser extension support

## 📋 Description

Linkding is a self-hosted bookmark manager. Bookmarks can be tagged, filtered,
searched full-text, archived and read later, and there is a browser extension
and a bookmarklet for saving links from anywhere.

## 🚀 Services

- **app**: sissbruecker/linkding:latest

## 📦 Installation

### Option 1: Quick Install

```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/linkding/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone

```bash
git clone "https://github.com/composemgr/linkding" ~/.local/srv/docker/linkding
cd ~/.local/srv/docker/linkding
cp default.env .env
docker compose --env-file .env up -d
```

### Option 3: Using composemgr

```bash
composemgr install linkding
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
APP_ADMIN_USER=admin
APP_ADMIN_PASS=replace-with-a-random-password
```

See `docker-compose.yaml` for complete list of configurable options.

### Environment Files

`default.env.sample` holds the full set of variables and is copied to `.env`
before starting the stack:

```bash
cp default.env .env
docker compose --env-file .env up -d
```

`app.env.sample` holds the app-specific overrides and is copied to `app.env`:

```bash
cp app.env.sample app.env
```

`composemgr up` applies `app.env` and `default.env` automatically. Raw
`docker compose` commands need `--env-file .env` to pick up the same values.

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, published on `172.17.0.1:64235` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

The proxy variants publish no host ports. The app is reachable only through the
proxy network.

## 🌐 Access

- **Web Interface**: http://172.17.0.1:64235

## 📂 Volumes

- `./volumes/data/linkding` - SQLite database and uploaded assets

## 🔐 Security

- Change all default passwords before deploying to production
- Use strong secrets for all authentication tokens
- Configure HTTPS using a reverse proxy (nginx, traefik, caddy)
- Regularly update Docker images for security patches
- Backup your data regularly

`LD_SUPERUSER_NAME` and `LD_SUPERUSER_PASSWORD` only apply when the database is
empty, on first start. After that, change the password in the linkding settings
instead, otherwise the new value has no effect.

`LD_ENABLE_AUTH_PROXY` is off, so linkding does its own authentication. Only turn
it on if the proxy in front of it actually enforces authentication, because
linkding will then trust the forwarded headers.

## 🔍 Logging

```shell
docker compose --env-file .env logs -f app
```

## 🛠️ Management

```bash
# Start services
docker compose --env-file .env up -d

# Stop services
docker compose --env-file .env down

# Update to latest images
docker compose --env-file .env pull && docker compose --env-file .env up -d

# View logs
docker compose --env-file .env logs -f

# Restart services
docker compose --env-file .env restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
