# n8n-local-podman

A quick repo for self-hosting n8n using Podman instead of Docker.

## Podman Install

Start here: https://podman.io/docs/installation#macos

Podman can be downloaded from the [Podman.io](https://podman.io/) website.

After installing, you need to create and start your first Podman machine:

```zsh
n8n-local-podman % podman machine init
n8n-local-podman % podman machine start
```

You can then verify the installation information using:

```zsh
n8n-local-podman % podman info
```

### Podman Compose

To install **Podman Compose** using pip3, follow these steps:

```zsh
n8n-local-podman % pip3 install podman-compose
```

After installation, try running:

```zsh
n8n-local-podman % podman-compose --version

podman-compose version 1.3.0
podman version 5.4.0
```

## Launch N8N

Run the following command to start n8n:

```zsh
n8n-local-podman % podman-compose -f podman-compose.yaml up -d
```

This will start the n8n container in detached mode.

![](images/podman-compose.png)

Access n8n by opening your web browser and navigating to http://localhost:5678.
You'll be prompted to log in using the credentials specified in the environment variables.

```zsh
n8n-local-podman % podman ps
CONTAINER ID  IMAGE                                 COMMAND          CREATED        STATUS        PORTS                             NAMES
81a80c9220e4  docker.io/library/postgres:16-alpine  postgres         3 minutes ago  Up 3 minutes  5432/tcp                          podman_postgres_1
81d81b63266a  docker.io/n8nio/n8n:latest                             3 minutes ago  Up 3 minutes  0.0.0.0:5678->5678/tcp            n8n
b354510fa908  docker.io/qdrant/qdrant:latest        ./entrypoint.sh  3 minutes ago  Up 3 minutes  0.0.0.0:6333->6333/tcp, 6334/tcp  qdrant
```

To stop the containers started with podman-compose, you can use the following command:

```zsh
n8n-local-podman % podman-compose -f podman-compose.yaml down
```

This command will stop and remove all the containers defined in your `podman-compose.yaml` file. The `-f` flag specifies
the compose file to use, ensuring it uses the same file you used to start the containers.

If you want to stop the containers without removing them, you can use:

```zsh
n8n-local-podman % podman-compose -f podman-compose.yaml stop
```

This will stop the containers but keep them in a stopped state, allowing you to start them again later without
recreating them.