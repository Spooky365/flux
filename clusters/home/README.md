# 

name: Build and Push Docker Image
on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v1

      - name: Get latest image tag
        id: get_latest_tag
        run: |
          # Fetch the latest tag from the Docker registry
          latest_tag=$(docker run --rm -i {{registry}}/{{image_name}}:latest /bin/bash -c 'echo ${{tag_prefix}}$(($(ls /path/to/tags | grep -oE "[0-9]+" | sort -n | tail -n 1)+1))')
          echo "::set-output name=latest_tag::$latest_tag"

      - name: Build and push Docker image
        uses: docker/build-push-action@v2
        with:
          context: .
          push: true
          tags: |
            latest
            ${{ github.sha }}
            ${{ steps.get_latest_tag.outputs.latest_tag }}









            name: Build and Push Docker Image
on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set IMAGE_TAG variable
        run: echo "IMAGE_TAG=0.1" >> $GITHUB_ENV

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v1

      - name: Build and push Docker image
        uses: docker/build-push-action@v2
        with:
          context: .
          push: true
          tags: |
            latest
            ${{ github.sha }}
            ${{ env.IMAGE_TAG }}












            name: Build and Push Docker Image
on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v1

      - name: Modify IMAGE_TAG variable
        run: echo "1" >> ${{ env.IMAGE_TAG }}

      - name: Build and push Docker image
        uses: docker/build-push-action@v2
        with:
          context: .
          push: true
          tags: |
            latest
            ${{ github.sha }}
            ${{ env.IMAGE_TAG }}

            