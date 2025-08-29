# BMAD-Method Development Container

Docker-in-Docker development environment for [BMAD-METHOD](https://github.com/bmad-code-org/BMAD-METHOD) - a comprehensive AI-powered development methodology.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Quick Start](#quick-start)
- [Container Setup](#container-setup)
- [Working with the Container](#working-with-the-development-container)
- [BMAD-Method Installation](#bmad-method-setup)
- [Additional Tools](#additional-setup)
- [Troubleshooting](#troubleshooting)
- [Resources](#resources)

## Prerequisites

Before you begin, ensure you have the following installed on your local machine:

1. **Visual Studio Code** - [Download VS Code](https://code.visualstudio.com/)
2. **Docker Desktop** - [Download Docker](https://www.docker.com/products/docker-desktop/)
   - Windows: Docker Desktop for Windows
   - macOS: Docker Desktop for Mac
   - Linux: Docker Engine and Docker Compose
3. **Dev Containers extension** for VS Code
   - Install from VS Code Extensions marketplace or run:
   ```bash
   code --install-extension ms-vscode-remote.remote-containers
   ```

**Note:** This container includes Node.js 20+ which is required for BMAD-Method.

## Quick Start

**TL;DR**: Get up and running in 5 minutes:
1. Clone this repo: `git clone https://github.com/vipasane/bmad-method-dind.git`
2. Open in VS Code and click "Reopen in Container" when prompted
3. Once container is running, install BMAD-Method: `npx bmad-method install`
4. Start developing with BMAD methodology!

## Container Setup

### 1. Clone the Repository

```bash
git clone https://github.com/vipasane/bmad-method-dind.git
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

Exit Claude Code

### GitHub Integration

Configure GitHub CLI (if not already configured):
```bash
gh auth login
```

#### Authenticate to github
Follow the prompts to authenticate with your GitHub account.
```bash
https://github.com/login/device
```
Paste code there (XXXX-XXXX)


### Initialize github app
```bash
claude
/install-github-app
```
And Follow the installation path

*** NOTE: Browser links might not work for authentication calls through host OS and non-default browsers do prepare to copy & paste in those stages ***
For more information or Troubleshooting this phase please refer
https://github.com/anthropics/claude-code-action/blob/main/docs/setup.md

### BMAD-Method Setup

#### Quick Start Options

##### Option 1: One-Command Installation (Recommended)
```bash
# Latest version
npx bmad-method install

# OR for stable version
npx bmad-method@stable install
```

##### Option 2: Clone and Install
```bash
# Clone the BMAD-Method repository
git clone https://github.com/bmadcode/bmad-method.git
cd bmad-method
npm run install:bmad
```

##### Option 3: Update Existing Installation
```bash
# If BMAD-Method is already installed
git pull
npm run install:bmad
```

#### Getting Started with BMAD

After installation, you have two paths:

**Fast Web UI Start (2 minutes):**
1. Get the full stack team file from `/dist/teams/team-fullstack.txt`
2. Create a new AI agent (Gemini or CustomGPT)
3. Upload the team file with instructions
4. Start chatting with `*help` or `*analyst`
5. Use `#bmad-orchestrator` for guidance
6. Move to IDE once PRD and architecture are complete

**Direct IDE Development:**
- Start with the User Guide in `docs/user-guide.md`
- Explore available AI agents in `bmad-core/agents/`
- Join the [Discord Community](https://discord.gg/gk8jAdXWmj) for support

#### Key BMAD Features
- **Automatic Updates**: BMAD preserves your custom configurations while updating
- **Backup System**: Creates `.bak` files automatically before changes
- **Expansion Packs**: Supports additional functionality modules
- **AI Agent Integration**: Built-in support for various AI development workflows

#### Using BMAD with Claude Code

Once Claude Code is installed and BMAD is set up, you can leverage BMAD methodology directly through Claude:

**BMAD Commands in Claude Code:**
```bash
# Generate BMAD team files for Claude
*help                    # Get BMAD assistance
*analyst                 # Start with BMAD analyst agent
#bmad-orchestrator      # Use BMAD orchestrator for project guidance

# BMAD workflow integration
claude /bmad-init        # Initialize BMAD workflow in current project
claude /bmad-analyze     # Analyze project with BMAD methodology
claude /bmad-architect   # Generate architecture using BMAD patterns
```

**Recommended Claude + BMAD Workflow:**
1. **Planning Phase**: Use `*analyst` to define PRD and requirements
2. **Architecture Phase**: Use `#bmad-orchestrator` for system design
3. **Development Phase**: Switch to Claude Code IDE for implementation
4. **Integration**: Use BMAD expansion packs through Claude commands

**BMAD Team File Integration:**
- Upload `/dist/teams/team-fullstack.txt` to Claude for comprehensive development support
- Use BMAD agents directly through Claude Code slash commands
- Leverage Claude's context with BMAD's structured methodology

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

### BMAD-Method Issues

#### Installation Problems
```bash
# Clear npm cache if installation fails
npm cache clean --force
npx bmad-method install

# For permission issues, try with sudo (Linux/macOS)
sudo npx bmad-method install
```

#### Update Issues
```bash
# If updates fail, force reinstall
rm -rf node_modules
npm run install:bmad
```

#### Node.js Version Issues
- BMAD requires Node.js 20+
- This container includes the correct version
- Verify with: `node --version`

#### Claude Code + BMAD Integration Issues
```bash
# If BMAD commands don't work in Claude Code
claude --version        # Verify Claude Code is installed
bmad-method --version   # Verify BMAD is installed

# Refresh BMAD team files if outdated
cd BMAD-METHOD
git pull
npm run build

# Re-upload team files to Claude if needed
# File location: ./dist/teams/team-fullstack.txt
```

**Common Integration Problems:**
- **BMAD commands not recognized**: Ensure BMAD is installed in the same environment as Claude Code
- **Team files not working**: Re-download latest team files from `/dist/teams/` directory
- **Slash commands failing**: Verify GitHub integration is properly configured with `/install-github-app`

## Resources

### Development Container
- [VS Code Remote Containers Documentation](https://code.visualstudio.com/docs/remote/containers)
- [Dev Container Specification](https://containers.dev/)
- [Docker Desktop Documentation](https://docs.docker.com/desktop/)

### BMAD-Method
- [BMAD-Method Repository](https://github.com/bmad-code-org/BMAD-METHOD)
- [BMAD User Guide](https://github.com/bmad-code-org/BMAD-METHOD/blob/main/docs/user-guide.md)
- [Discord Community](https://discord.gg/gk8jAdXWmj)
- [AI Agents Documentation](https://github.com/bmad-code-org/BMAD-METHOD/blob/main/bmad-core/agents)

### Additional Tools
- [Claude Code Documentation](https://github.com/anthropics/claude-code-action/blob/main/docs/setup.md)
- [GitHub CLI Documentation](https://cli.github.com/manual/)


