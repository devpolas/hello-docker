---
# Docker CMD

## Build Docker image with a tag

```sh
docker build -t express-server:latest .
```

This builds the image using Docker’s **default bridge network**.

---

## Build Docker image with host network (if build gets stuck)

```sh
docker build -t express-server:latest --network=host .
```

### Why this is needed sometimes

During `docker build`, commands like `npm install` require internet access.
On some systems (especially **Alpine-based images** or DNS/IPv6 setups), Docker’s default bridge network may cause:

- DNS resolution issues
- TLS handshake hangs
- `npm install` freezing without errors

Using `--network=host` makes the build container use the **host’s network stack**, fixing those issues.

> ⚠️ **Important**
>
> - This affects **build-time only**
> - The final image **does NOT use host networking**
> - Safe for local development and CI
> - Not recommended for untrusted build environments

This behavior is related to how Docker isolates networking during image builds.

---

## Run Docker container (detached, auto-remove, port exposed)

```sh
docker run --rm --name node-server -d -p 8080:8080 express-server:latest
```

### Flags explained

- `--rm` → remove container after it stops
- `--name node-server` → custom container name
- `-d` → detached mode (runs in background)
- `-p 8080:8080` → map host port → container port

---

## Access the server

Visit:
👉 [http://localhost:8080](http://localhost:8080)

### Expected output

```json
{
  "message": "Hello World!"
}
```

---

## Check running containers

```sh
docker ps
```

## Check all containers (running + stopped)

```sh
docker ps -a
```

---

## Stop the container

```sh
docker stop node-server
```

---

## Best practice note (recommended for your setup)

If you want to **avoid `--network=host` completely**, use a Debian-based Node image instead of Alpine:

```Dockerfile
FROM node:24-bookworm
```

This solves most DNS/npm issues on Debian 13 systems like yours.

---
