# Core Concepts

## Containers vs. VMs

Containers share the host's OS kernel, providing lightweight isolation and near-instant startup. Virtual machines emulate complete hardware stacks and separate kernels, resulting in higher resource usage and slower boots. Containers offer minimal footprints and quick iteration, making them ideal for development environments.

## Custom Dockerfiles

Authoring a `Dockerfile` allows you to extend an existing Dev Container image or build from scratch. Typical steps include:

```Dockerfile
FROM mcr.microsoft.com/vscode/devcontainers/base:ubuntu
RUN apt-get update && apt-get install -y git curl
``` 
Extending official base images reduces maintenance overhead, while full custom images grant granular control over every layer.

## devcontainer.json

The `devcontainer.json` file configures your environment. Key properties:
- `dockerFile` or `image` — define build source
- `extensions` — auto-install VS Code extensions
- `forwardPorts` — map container ports to the host
- `mounts` — attach volumes or bind mounts
- `postCreateCommand` — execute commands after creation

Example:

```json
{
  "dockerFile": "Dockerfile",
  "extensions": ["ms-azuretools.vscode-docker"],
  "forwardPorts": [8080],
  "postCreateCommand": "npm install"
}
```

### Dev Container Features

Dev Container **features** are reusable presets you can declare in `devcontainer.json` instead of crafting full Dockerfiles. They enable easy installation of languages, runtimes, CLIs, and utilities. Example:
```json
"features": {
  "ghcr.io/devcontainers/features/node:1": { "version": "18" },
  "ghcr.io/devcontainers/features/docker-in-docker:1": {}
}
```
Explore the feature registry at https://containers.dev/featuredef/ for additional options.

### Customizations

Use `devcontainer.json` properties to tailor your environment:
- **settings**: Override VS Code settings per project:
  ```json
  "settings": {
    "editor.tabSize": 2,
    "terminal.integrated.shell.linux": "/bin/bash"
  }
  ```
- **extensions**: Auto-install VS Code extensions:
  ```json
  "extensions": ["ms-vscode.vscode-node-azure-pack", "dbaeumer.vscode-eslint"]
  ```
- **containerEnv**: Define environment variables inside the container:
  ```json
  "containerEnv": {
    "NODE_ENV": "development",
    "DEBUG": "*"
  }
  ```
- **remoteUser**: Specify the user (e.g., `vscode`) inside the container.
- **postStartCommand**: Commands to run each time the container starts.

By combining features with settings, extensions, and environment variables, you can craft a fully reproducible and customized dev environment.

## Dotfiles Support

Sync your personal dotfiles by specifying a Git repo:

```json
"dotfilesGitRepository": "https://github.com/yourusername/dotfiles.git"
```
This ensures your shell, editor, and git configs are applied within the container.

## Summary

These core concepts empower you to select the right container base, customize builds with Dockerfiles, configure VS Code via `devcontainer.json`, and maintain consistent settings with dotfiles. Together, they provide a robust, reproducible dev environment.
