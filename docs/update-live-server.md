# Live server update

## Prerequisites

Ensure you have followed the steps to [create a new up-to-date production image.](./deployment.md)

## Remote connection

SSH into the linux server using VS Code's remote connection tool. Ensure that you public key is already on the host's server. For more info about setting up ssh read [the ssh document](./ssh.md)

## Pull update onto live server

Once you are logged into the prod server. Open a terminal and follow the below commands:

Shut down the exisitng containers:

```sh
docker compose -f rafnav-compose.yml down
```

> Wait until the containers are shut down and removed

Restart the docker compose environment and recreate the containers. This will pull the new image and correctly update.

```sh
docker compose -f rafnav-compose.yml up -d --force-recreate
```

> Note: **Not** shutting the containers down first may result in broken static files such as css & js. \
> See: <https://github.com/frappe/frappe_docker/wiki/Frequently-Asked-Questions#how-to-update>

Prune docker to save system space. Say yes when prompted.

```sh
docker system prune
```
