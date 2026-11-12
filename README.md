# Art Studio Hub

Art Studio Hub is a workspace for independent artists to manage their artwork and studio records. The local environment runs a React frontend, a NestJS API, and a PostgreSQL database.

## Prerequisites

- Docker Desktop running in Linux container mode
- PowerShell on Windows

Run the commands below from the repository root, where `compose.yaml` is located.

## Local setup

On the first run, create `.env` from the example:

```powershell
Copy-Item .env.example .env
```

Use `.env` for local settings and commit `.env.example` as the shared template.

Validate the Compose configuration and start all three services:

```powershell
docker compose config --quiet
docker compose up -d --build --wait
docker compose ps
```

## Verify the services

- **Web** — Open `http://localhost:5173` and confirm that the React starter page loads.
- **API** — Run the command below and confirm that `status` is `ok`.
- **Database** — Confirm that `db` is marked `healthy` in `docker compose ps`.

```powershell
Invoke-RestMethod -Uri 'http://localhost:3000/health'
```

## Troubleshooting

List all containers, including stopped ones, and inspect the logs for the failing service:

```powershell
docker compose ps -a
docker compose logs --tail 50 api
```

Replace `api` with `web` or `db` to inspect another service.

## Stop the environment

```powershell
docker compose down
```

This removes the containers and keeps PostgreSQL data in the `postgres_data` volume. Adding `-v` also deletes the volume and its data.