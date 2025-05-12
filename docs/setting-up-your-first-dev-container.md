# Setting Up Your First Dev Container

## 1. Prerequisites
Ensure you have the following installed:
- Docker (version 20.10+): https://docs.docker.com/get-docker
- Visual Studio Code (version 1.60+): https://code.visualstudio.com/download
- Remote - Containers extension: install from the VS Code Marketplace

Validate setup:
```bash
docker --version
code --version
```

## 2. Quickstart Demo
1. Open your project folder in VS Code.
2. Press `Ctrl+Shift+P` (Cmd+Shift+P on Mac) and choose **Remote-Containers: Open Folder in Container**.
3. Select **Show All Definitions...** then pick **Node.js & TypeScript** (or any predefined config).
4. Wait as VS Code builds and attaches to the container. You’ll see a green bar indicating the container context.

## 3. devcontainer.json Walkthrough
Create a `.devcontainer` folder and add `devcontainer.json`:
```json
{
  "name": "Node.js Dev",
  "image": "mcr.microsoft.com/vscode/devcontainers/javascript-node:18",
  "extensions": ["dbaeumer.vscode-eslint", "esbenp.prettier-vscode"],
  "forwardPorts": [3000],
  "postCreateCommand": "npm ci"
}
```
Reopen in container to apply these settings.

## 4. Tips for Smooth Setup
- **Inspect logs**: View the **Dev Containers** output panel in VS Code for build errors.
- **Layer caching**: Place commands that change less frequently at the top of your Dockerfile.
- **Use features**: Leverage the Dev Container [feature library](https://containers.dev/feature-gallery/) to add tools without custom Dockerfiles.

## 5. Summary
You now have a working Dev Container. Next, explore features like multi-stage builds, add more port forwards, or integrate a `docker-compose.yml` for complex services. Your environment is reproducible and sharable across teams.
