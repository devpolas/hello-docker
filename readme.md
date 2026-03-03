# Docker CMD

### Build docker image with tag name

```sh
docker build -t express-server:latest .
```

_if any issue create or build docker image run this cmd_

```sh
docker build -t express-server:latest --network host .
```

`or`

```sh
docker build -t express-server:latest --network=host .
```

### Run docker images with detach mode with expose port and delete after stop container

```sh
docker run --rm --name node-server -d -p 8080:8080 express-server:latest # container name is node-server
```

### Visit [localhost:8080](http://localhost:8080/) for server response

_output_

```json
{
  "message": "Hello World!"
}
```

### Check docker running container

```sh
docker ps
```

### Check all docker running container

```sh
docker ps -a
```

### Stop docker container

```sh
docker stop node-server # your container name
```
