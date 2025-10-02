
# Onyx

**What it is:** Gen-AI chat + enterprise search you can run locally.

**Time:** ~5–15 min on a dev laptop.

**Prereqs:**

* Git, Docker Desktop (with Compose v2) installed. 
* https://docs.onyx.app

## Quickstart

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

## Test it

Open http://localhost:3000 in your browser. You should see the Onyx UI (login/onboarding). 

If needed later: set up auth (Basic/OAuth/OIDC/SAML) after the first boot. 

## Common tweaks

Apple Silicon (M1/M2/M3): if any image lacks arm64, add --platform=linux/amd64 to build/run. (Most users won’t need this, but it’s a quick fix.)

Port busy? Change host port in the compose file or stop the other service and re-run.

## Cleanup

```
docker compose down -v
```
