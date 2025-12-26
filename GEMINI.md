# Project Overview

This repository contains a Docker-based development environment for ROS 2. It uses a `Dockerfile.base` to create various ROS 2 development images with a custom `lazyvim` and Neovim setup. The images are built and published to the GitHub Container Registry using a GitHub Actions workflow.

The Dockerfile installs a specific version of Neovim, a custom Neovim configuration from a separate repository, and several development tools. It also sets up a non-root user for development.

## Building and Running

The Docker images are built automatically by a GitHub Actions workflow defined in `.github/workflows/docker-build.yaml`. This workflow builds multiple images in parallel based on a matrix of base images.

To build an image locally, you can use the `docker build` command. You need to provide the `BASE_IMAGE` build argument. For example:

```bash
docker build --build-arg BASE_IMAGE=osrf/ros:jazzy-desktop-noble -t ros-dev-image .
```

To run a container from one of the built images:

```bash
docker run -it --rm ros-dev-image
```

## Development Conventions

*   The project uses a `Dockerfile.base` to define the common layers of the Docker images.
*   A GitHub Actions workflow is used to automate the building and publishing of the Docker images.
*   The workflow uses a matrix strategy to build multiple image variations.
*   The Docker images are pushed to the GitHub Container Registry.
*   The Neovim configuration is managed in a separate repository and cloned into the image during the build process.
*   The development environment is set up with a non-root user.
*   ROS 2 environment is sourced automatically in the user's `.bashrc` file.
