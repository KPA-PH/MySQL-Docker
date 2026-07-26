# KPA Datastores

Docker Compose stack for Valkey 9 and the Socket.IO service.

## Setup

Create a local `.env` from `.env.example` and replace every `change-me-*` value before starting the stack.

```powershell
Copy-Item .env.example .env
docker compose up -d
```

Without a bind-address override, Valkey is published on `127.0.0.1` only.
The provided `.env.example` uses `0.0.0.0` for firewall-allowlisted server
deployments:

| Service | Container port | Host port |
| --- | ---: | ---: |
| Valkey 9 | 6379 | 6379 |
| Socket.IO | 11203 | 11203 |

Use `VALKEY9_BIND_ADDRESS=0.0.0.0` only when the host firewall and network
access rules are already locked down.

## Valkey memory

Valkey is configured as a cache with a 10 GB `maxmemory` ceiling and the
`allkeys-lfu` eviction policy. The container is limited to 12 GB by default,
leaving headroom for Valkey overhead and the host operating system on a 16 GB
server.

Set `VALKEY9_MEMORY_LIMIT` in `.env` to change the container limit. Keep the
container limit above Valkey's `maxmemory` setting.

## Data

Runtime data is stored in ignored bind-mounted directories:

- `valkey/data`

Back up these directories, or use database-native backups, before image upgrades or configuration changes.

## Validation

Render and validate the Compose file without starting containers:

```powershell
docker compose --env-file .env config
```

Check runtime health:

```powershell
docker compose ps
```
