# KPA Datastores

Docker Compose stack for MySQL 8.4, MySQL 8.0, PostgreSQL 18, and Valkey.

## Setup

Create a local `.env` from `.env.example` and replace every `change-me-*` value before starting the stack.

```powershell
Copy-Item .env.example .env
docker compose up -d
```

For MySQL and PostgreSQL, image password variables initialize only an empty data directory. Existing database directories keep their current users and passwords.

By default, ports are bound to `127.0.0.1` only:

| Service | Container port | Host port |
| --- | ---: | ---: |
| MySQL 8.4 | 3306 | 3306 |
| MySQL 8.0 | 3306 | 33060 |
| PostgreSQL 18 | 5432 | 5432 |
| Valkey | 6379 | 6379 |

Set `*_BIND_ADDRESS=0.0.0.0` only when the host firewall and network access rules are already locked down.

## Data

Runtime data is stored in ignored bind-mounted directories:

- `mysql/data-84`
- `mysql/data`
- `postgresql/data-18`
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
