# Mini-starter-guides for Devs testing new software

## Meilisearch

**What it is:** Lightweight, super-fast search engine.

**Time:** ~5–10 min.

**Prereqs**

Docker 24+ and Docker Compose v2.

### Quickstart
```
# Pull & run (with local data volume)
docker run -it --rm \
  -p 7700:7700 \
  -v $(pwd)/meili_data:/meili_data \
  getmeili/meilisearch:v1.16
```

See https://www.meilisearch.com/docs/

### Test it works

```
# Health check (should return 200 and JSON with "status":"available")
curl http://localhost:7700/health
```

### Common tweaks

* Want an API key? Relaunch with: `-e MEILI_MASTER_KEY='MASTER_KEY'` (or CLI flag). 

* Persist data: keep the `-v $(pwd)/meili_data:/meili_data` mount.

### Cleanup

```
# Stop the container (Ctrl+C) — data stays in ./meili_data
```

## Onyx

**What it is:** Gen-AI chat + enterprise search you can run locally.

**Time:** ~5–20 min on a dev laptop.

**Prereqs**

Docker 24+ and Docker Compose v2.

### Quickstart

**Option 1 (recommended)** - Use the provided installation script:

```
curl -fsSL https://raw.githubusercontent.com/onyx-dot-app/onyx/main/deployment/docker_compose/install.sh > install.sh && chmod +x install.sh && ./install.sh
```

**Option 2** - Step by step instructions:

```
# 1) Clone
git clone https://github.com/onyx-dot-app/onyx.git
cd onyx/deployment/docker_compose

# 2) Launch (pull prebuilt images)
docker compose up -d
# (Alternatively) build from source:
# docker compose up -d --build --force-recreate
```

The stack comes up and becomes available at http://localhost:3000 after initialization. 

See https://docs.onyx.app/deployment/overview

### Test it works

Open http://localhost:3000 in your browser. You should see the Onyx UI (login/onboarding). 

If needed later: set up auth (Basic/OAuth/OIDC/SAML) after the first boot. 

### Common tweaks

Apple Silicon (M1/M2/M3): if any image lacks arm64, add --platform=linux/amd64 to build/run. (Most users won’t need this, but it’s a quick fix.)

Port busy? Change host port in the compose file or stop the other service and re-run.

### Cleanup

```
docker compose down -v
```

## NocoDB

**What it is:** Open-source Airtable-like (no-code DB UI).

**Time:** ~8–10 min.

**Prereqs**

Docker 24+ and Docker Compose v2.

### Quickstart
```
git clone https://github.com/nocodb/nocodb
cd nocodb/docker-compose/2_pg
docker compose up -d
```

### Test it works

Open http://localhost:8080 and complete onboarding.

### Common tweaks

* Ports busy? Edit docker-compose.yml to change 8080:8080, then `docker compose up -d`. 

* Logs if startup is slow: `docker compose logs`. 

### Cleanup
```
docker compose down -v
```
