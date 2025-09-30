# Deployment

- [Deployment](#deployment)
  - [Overview](#overview)
    - [📦 Local Setup](#-local-setup)
    - [🏗️ Production Image Build](#️-production-image-build)
    - [🚀 Publish to Docker Hub](#-publish-to-docker-hub)
  - [Deploy Local Setup](#deploy-local-setup)
  - [Prod Image Build](#prod-image-build)
  - [Publish Image](#publish-image)

## Overview

This guide outlines the steps to deploy the Rafnav Bench application, covering local setup, production image creation, and publishing to Docker Hub.

### 📦 Local Setup

- Create an apps.json file listing private GitHub repositories.
- Replace {{PAT}} with your GitHub personal access token.
- Encode the JSON file to Base64 for use in Docker builds.

### 🏗️ Production Image Build

- Use Docker to build a production image with build arguments including the encoded apps list, user guide name, and support email.

### 🚀 Publish to Docker Hub

- Authenticate with Docker CLI using your Docker Hub PAT.
- Push the built image to the rafnav/rafnav_bench:prod repository.


## Deploy Local Setup

Create a new JSON file called apps.json

```sh
touch apps.json
```

Copy below and replace all ```{{PAT}}``` with your personal access token from github that has read access to the private repos

```json
[
  {
    "url": "https://{{PAT}}@github.com/cronos-capital/rafnav_core.git",
    "branch": "main"
  },
  {
    "url": "https://{{PAT}}@github.com/cronos-capital/matter_management.git",
    "branch": "main"
  },
  {
    "url": "https://{{PAT}}@github.com/cronos-capital/raf_finance.git",
    "branch": "main"
  },
  {
    "url": "https://{{PAT}}@github.com/cronos-capital/filing.git",
    "branch": "main"
  },
  {
    "url": "https://{{PAT}}@github.com/cronos-capital/documentation.git",
    "branch": "main"
  }
]
```

Generate a Base 64 shell variable of the apps list. This will be passed as a build argument for the docker image later.

```sh
export APPS_JSON_BASE64=$(base64 -w 0 apps.json)
```

## Prod Image Build

Build the production version of the image using the below command:

```sh
docker build --build-arg=APPS_JSON_BASE64=$APPS_JSON_BASE64 --build-arg=VITE_USER_GUIDE_NAME="user_guide.pdf" --build-arg=VITE_SUPPORT_MAIL="rafnav@webridge.co.za" -t rafnav/rafnav_bench:prod --file=images/production/Containerfile . --no-cache
```

## Publish Image

Publish the newly built docker image to docker hub using your [PAT from Docker Hub](https://docs.docker.com/security/access-tokens/)

Log in to Docker using the Docker cli \
At the password prompt, paste your PAT.

```sh
docker login -u [username]
```

Push the image using the following command:

```sh
docker push rafnav/rafnav_bench:prod
```

Follow the instructions outlined here, [Live server update](./update-live-server.md), to pull the updated image onto the prod server.
