# Setup Docker Action

This GitHub Action sets up Docker and logs in to Azure Container Registry.

## Description

This action performs the following steps:

1. Sets up the Azure CLI and logs in.
2. Sets up Docker Buildx.
3. Logs in to the specified Azure Container Registry.
4. Pulls the standard image tag and stores it in `env.image_tag`

## Inputs

| Name      | Description                             | Required | Default              |
|-----------|-----------------------------------------|----------|----------------------|
| acr_repo  | Azure Container Registry Repository     | true     | `acrsbsharedservices`|

## Example Usage

```yaml
name: Build and Push Docker Image

on:
  push:
    branches:
      - main

jobs:
  build-and-push:
    runs-on: 
      group: sb-runners
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Setup Docker and Login to ACR
        uses: SE-Sustainability-Business/sbaction-setupdocker@v1
      
      - name: Build and Push My Image
        uses: docker/build-push-action@v6
        with:
          context: .
          file: .cicd/Dockerfile
          push: true
          tags: acrsbsharedservices.azurecr.io/my_image:${{ env.hash }} 
```
