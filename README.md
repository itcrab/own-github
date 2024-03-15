# own-github
Setup own service like GitHub inside your local network

## Why?
New times force us to bring up our own services on our private local network.

# Synology setup

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
