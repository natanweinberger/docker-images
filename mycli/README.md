# MyCLI Docker image

### 1. Build the image

```bash
$ docker build -t mycli .
```

### 2. Run a container

Tip: as you use mycli, your query history is recorded inside the container at `/data/.mycli-history`. However, it will be lost when you remove the container. To make it persist to future mycli containers, mount an empty local file to the container's path `/data/.mycli-history`. Your query history will be written to the local file and will be available to future mycli containers.

```bash
# Skip this step if you don't want query history to be shared to future containers
$ touch /tmp/.mycli-history
```

```bash
$ docker run \
--rm \
-it \
-v /tmp/.mycli-history:/data/.mycli-history \  # Remove this line if you don't want to persist query history
mycli \
mycli -h $host --port $port -u$username -p$password $database
```
