# bmad-method-dind
Docker development container (Docker in Docker image) for BMAD-method (https://github.com/bmad-code-org/BMAD-METHOD)

## Prerequisites

Before you begin, ensure you have the following installed on your local machine:

1. **Visual Studio Code** - [Download VS Code](https://code.visualstudio.com/)
2. **Docker Desktop** - [Download Docker](https://www.docker.com/products/docker-desktop/)
   - Windows: Docker Desktop for Windows
   - macOS: Docker Desktop for Mac
   - Linux: Docker Engine and Docker Compose
3. **Remote - Containers extension** for VS Code
   - Install from VS Code Extensions marketplace or run:
   ```bash
   code --install-extension ms-vscode-remote.remote-containers
   ```

## Setup Instructions

### 1. Clone the Repository

```bash
git clone <your-repository-url>
cd bmad-method-dind
```

### 2. Open in VS Code with Remote Containers

There are multiple ways to open the project in a Dev Container:

#### Option A: Using Command Palette
1. Open VS Code
2. Open the cloned folder: `File > Open Folder...`
3. Press `F1` or `Ctrl+Shift+P` (Windows/Linux) or `Cmd+Shift+P` (macOS)
4. Type and select: `Remote-Containers: Reopen in Container`

#### Option B: Using the Quick Action
1. Open the folder in VS Code
2. When VS Code detects the `.devcontainer` folder, a notification will appear
3. Click `Reopen in Container`

#### Option C: From VS Code Terminal
```bash
code .
# Then use Option A or B
```

### 3. Wait for Container Build

The first time you open the project in a container:
- VS Code will build the Docker image based on the configuration
- This may take several minutes depending on your internet connection
- You'll see progress in the VS Code terminal

### 4. Verify the Environment

Once the container is running, verify the setup:

```bash
# Check Docker is available (Docker-in-Docker)
docker --version

# Check Node.js is installed
node --version
npm --version

# Check GitHub CLI is available
gh --version
```

## Working with the Development Container

### Container Features

This development container includes:
- **Docker-in-Docker**: Run Docker commands inside the container
- **Node.js LTS**: With npm, yarn, and pnpm package managers
- **GitHub CLI**: For GitHub integration
- **VS Code Extensions**: Markdown support pre-configured

### Common Commands

#### Rebuild Container
If you make changes to the container configuration:
1. Press `F1` → `Remote-Containers: Rebuild Container`

#### Restart Container
1. Press `F1` → `Remote-Containers: Restart Container`

#### Open Terminal in Container
1. Press `` Ctrl+` `` or `View > Terminal`
2. The terminal automatically opens inside the container

### Port Forwarding

To forward ports from the container to your local machine:
1. Add to `.devcontainer/devcontainer.json`:
   ```json
   "forwardPorts": [3000, 8080]
   ```
2. Or forward manually: Press `F1` → `Forward a Port`

## Additional Setup

### Claude Code

#### Install Claude
```bash
npm install -g @anthropic-ai/claude-code@latest
```

#### Initialize Claude & set credentials
```bash
claude --dangerously-skip-permissions
```

### GitHub Integration

Configure GitHub CLI (if not already configured):
```bash
gh auth login
```

Follow the prompts to authenticate with your GitHub account.

### BMAD-Method Setup

Clone and setup the BMAD-Method repository inside the container:
```bash
# Clone the BMAD-Method repository
git clone https://github.com/bmad-code-org/BMAD-METHOD.git

# Navigate to the directory
cd BMAD-METHOD

# Follow the BMAD-Method specific setup instructions
```

## Troubleshooting

### Container Won't Start
- Ensure Docker Desktop is running
- Check Docker Desktop settings for resource allocation (CPU, Memory)
- Try: `docker system prune` to clean up Docker resources

### Permission Issues
- The container runs as a non-root user by default
- To run as root, uncomment in `.devcontainer/devcontainer.json`:
  ```json
  "remoteUser": "root"
  ```

### Slow Performance
- Increase Docker Desktop resource limits
- Windows: Ensure WSL 2 is enabled for better performance
- macOS: Check Docker Desktop preferences for resource allocation

### Extension Issues
- Extensions are installed in the container, not locally
- To add more extensions, modify `.devcontainer/devcontainer.json`:
  ```json
  "customizations": {
    "vscode": {
      "extensions": [
        "extension.id.here"
      ]
    }
  }
  ```

## Resources

- [VS Code Remote Containers Documentation](https://code.visualstudio.com/docs/remote/containers)
- [Dev Container Specification](https://containers.dev/)
- [BMAD-Method Repository](https://github.com/bmad-code-org/BMAD-METHOD)


