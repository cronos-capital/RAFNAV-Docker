# RAFNav Development Setup

## Introduction

You will be working in the `./development` folder a.k.a. a dev workspace. Follow the steps below to set up the workspace.

### Workspace Setup

1. Clone the Repo into your working directory

```sh
git clone https://github.com/cronos-capital/RAFNAV-Docker.git
cd RAFNAV-Docker
```

2. Create the devcontainer and VsCode configuration from the templates provided

```sh
cp -R devcontainer-example .devcontainer
cp -R development/vscode-example development/.vscode
```

## Build the Docker Image

Run the following command in your working directory

```sh
docker build -t rafnav_bench:latest ./images/development
```

> You may change the tag to a more relevant naming convention. However, you need to change the image used for development in the correct docker-compose file under ```./.devcontainer/docker-compose.yml```

### Container Initialization

We will be attaching a VS Code window to the docker container workspace. This requires the [dev containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

1. Open the RAFNAV-Docker folder with Vs Code.
2. Open the command pallet with _ctrl + shift + p_ or _View->Command Pallet_
3. Run the command `dev containers: Reopen in container`
4. Wait for the container to warm up...

### GitHub Login (GitHub CLI)

- Make sure you have git and Github CLI installed on **windows**
- Log in to GitHub from VsCode to sync your github credentials with GitHub

### RAFNAV Installation

#### Development Branch Apps Install

```sh
  frap-install -j apps-development.json -v
```

#### Prod Apps Install

```sh
 frap-install -j apps-prod.json -v
```

**Note: For additional args and configs run `frap-install --help` first.**

2. cd into Rafnav's development bench. An alias has already been assigned. Run the following command:

```sh
go-rafnav_bench
```

1. Now you are able to start development on RAFNAV with all the dependencies and the correct environment set-up.

### Default Credentials

MariaDB Root Password: 123

> Unless changed in the docker or docker-compose file

First site's Administrator password: admin

> Unless changed in the docker or docker-compose file
