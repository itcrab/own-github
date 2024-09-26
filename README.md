# own-github
Setup own service like GitHub inside your local network

## Why?
New times force us to bring up our own services on our private local network.

# Synology setup

### Gitea (with SQLite3) + Actions by Gitea Act Runner
`compose.yml`
```YML
version: "3"

services:
  gitea_web:
    image: gitea/gitea:1.21.11
    container_name: gitea
    environment:
      - USER_UID=1000
      - USER_GID=1000
    restart: always
    volumes:
      - /volume1/docker/gitea/data:/data
    ports:
      - "10022:22"
      - "3000:3000"
  gitea_act_runner:
    image: gitea/act_runner:0.2.11
    container_name: gitea_act_runner
    depends_on:
      - gitea_web
    environment:
      - GITEA_RUNNER_REGISTRATION_TOKEN={{ TOKEN }}
      - GITEA_INSTANCE_URL=http://gitea:3000
      - GITEA_RUNNER_NAME=gitea_runner  
    restart: always
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /volume1/docker/gitea_runner/data:/data
```

### Gogs (with SQLite3)
`compose.yml`
```YML
services:
  gogs:
    image: gogs/gogs
    volumes:
      - /volume1/docker/gogs/data:/data
    ports:
      - "10022:22"
      - "3000:3000"
    restart: always
    environment:
      - RUN_CROND=true
```
