# Git

```bash
# Show the working tree status
git status
```

```bash
# Pull the latest changes from the remote
git pull
```

# Docker

```bash
# List running containers
docker ps
```

```bash
# Stop the Compose stack and remove its volumes
docker compose down -v
```

```bash
# Build and start the Compose stack in the background
docker compose up -d --build
```

```bash
# Stop the Compose stack, remove its volumes, then rebuild and start it
docker compose down -v && docker compose up -d --build
```
