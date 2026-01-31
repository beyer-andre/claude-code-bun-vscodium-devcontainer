# Bun based Claude Code and OpenCode devcontainer for VSCodium 

## Features

- Based on the [Claude Code development container reference implementation](https://github.com/anthropics/claude-code/tree/main/.devcontainer)
- Includes [OpenCode](https://github.com/anomalyco/opencode)
- Uses [Bun](https://bun.sh/) instead of Node.js
- Supports [VSCodium](https://github.com/VSCodium/vscodium) with [DevPod Containers extension](https://github.com/3timeslazy/vscodium-devpodcontainers)
- Works with [DevPod CLI](https://devpod.sh/docs/getting-started/install#install-devpod-cli)
- Docker-in-Docker [feature](https://github.com/devcontainers/features/tree/main/src/docker-in-docker) integrated
- Default zsh, tmux installed
- Forwarded container port 3000

## Setup

1. Install dependencies
   - ssh
   - [Docker](https://docs.docker.com/engine/)
   - [VSCodium](https://github.com/VSCodium/vscodium) with [DevPod Containers extension](https://github.com/3timeslazy/vscodium-devpodcontainers)
   - [DevPod CLI](https://devpod.sh/docs/getting-started/install#install-devpod-cli) (see also [installation](https://fabiorehm.com/blog/2025/11/11/devpod-ssh-devcontainers/#installation))

2. Install and configure DevPod CLI
   ```bash
   # Install DevPod (Linux)
   curl -L -o devpod "https://github.com/loft-sh/devpod/releases/latest/download/devpod-linux-amd64" && \
     sudo install -c -m 0755 devpod /usr/local/bin && \
     rm -f devpod
   
   # Add and configure Docker provider
   devpod provider add docker
   devpod provider use docker

   # Disable telemetry (enabled by default)
   devpod context set-options -o TELEMETRY=false

   # Set VSCodium as default IDE
   devpod ide use codium
   ```

3. Create bind-mounted configuration directories for Claude Code and OpenCode
   ```bash
   mkdir ~/.claude-devcontainer && mkdir ~/.opencode-devcontainer
   ```

4. Copy the .devcontainer folder into your project

## Usage
```bash
# Change into a project with the .devcontainer directory
cd my-project

# Start devcontainer and IDE
devpod up .

# Start devcontainer without IDE
devpod up . --ide none

# SSH into the devcontainer
ssh my-project.devpod

# Run agents inside devcontainer
#claude --dangerously-skip-permissions
#opencode

# Delete devcontainer
devpod delete my-project
```

## References
- [Claude Code Docs: Development containers](https://code.claude.com/docs/en/devcontainer)
- [DevPod: SSH-Based Devcontainers Without IDE Lock-in](https://fabiorehm.com/blog/2025/11/11/devpod-ssh-devcontainers/)
- [How to isolate Claude Code using DevContainer setup](https://medium.com/@a8n.one/how-to-isolate-claude-code-using-devcontainer-setup-68f8e2d109c8)
- [DevPod Containers extension](https://github.com/3timeslazy/vscodium-devpodcontainers)
