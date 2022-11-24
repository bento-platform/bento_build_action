# bento_build_action
GitHub CI composite action to build development and production containers for Bento components.

To use this in a Bento service repository, create a GitHub Actions workflow 
which looks something like the following:

```yaml
name: Build and push bento_my_cool_service
on:
  release:
    types: [ published ]
  pull_request:
    branches:
      - master
  push:
    branches:
      - master

jobs:
  build-push:
    runs-on: ubuntu-latest

    permissions:
      contents: read
      packages: write

    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Run Bento build action
        uses: bento-platform/bento_build_action@v0.7
        with:
          registry: ghcr.io
          registry-username: ${{ github.actor }}
          registry-password: ${{ secrets.GITHUB_TOKEN }}
          image-name: ghcr.io/bento-platform/bento_my_cool_service
          development-dockerfile: dev.Dockerfile
          dockerfile: Dockerfile
```
