# Linkding

A self-hosted application for managing linkding.

## Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/linkding/main/docker-compose.yaml" | docker compose -f - up -d
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/linkding" ~/.local/srv/docker/linkding
cd ~/.local/srv/docker/linkding
docker compose up -d
```

### Option 3: Using composemgr
```bash
composemgr install linkding
```

## Configuration

See docker-compose.yaml for environment variables and configuration options.

## Documentation

Check the official project documentation for detailed setup and usage information.
