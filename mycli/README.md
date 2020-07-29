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

### Notes

This image uses mycli 1.10.0. More recent versions of mycli return query results slowly in Docker. For example:

```mysql
> SELECT *
FROM table
LIMIT 10
```

| Client | Timing |
| --- | --- |
| mysql 5.7 | 0.03 s |
| mycli 1.10.0 | 0.03 s |
| mycli 1.21.1 | 2.50 s |

As best I can tell, mycli 1.10.0 is the latest version that closely matches standard MySQL's timing in Docker. It does seem like it's just a delay in displaying the results, not actually in running the query on the server. If you find an alternate solution, feel free to open an issue or a PR.

Relatedly, pymysql version 0.9.2 is pinned to support mycli 1.10.0. Subsequent versions of pymysql [remove a function](https://github.com/PyMySQL/PyMySQL/commit/fe0cd60e6f9e3bc0fb81f76f7e4fa30a1e1b34cc#diff-40496cc4a0f4db6907de60f7ce470b95) that is needed in mycli 1.10.0.
