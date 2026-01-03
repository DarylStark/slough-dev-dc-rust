# Slough - Dev Container - Rust

A pre-configured development container image for Rust development, part of the Slough project by Daryl Stark.

## About the Slough Project

The Slough project is a comprehensive initiative by Daryl Stark to deliver consistent development tooling through dev containers. The goal is to provide standardized, ready-to-use development environments that ensure consistency across different machines and team members, eliminating the "works on my machine" problem.

This particular container is configured specifically for Rust development, including all necessary tools and dependencies to start developing Rust applications immediately.

## Quick Start

### Using as a Dev Container

#### Image Information

The container image is available on Docker Hub:

```
dast1968/slough-dev-dc-rust:1.0.0
```

#### In VS Code

1. Install the [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
2. Create a `.devcontainer/devcontainer.json` file in your project root:

```json
{
  "name": "Rust Development",
  "image": "dast1968/slough-dev-dc-rust:1.0.0",
  "customizations": {
    "vscode": {
      "extensions": [
        "rust-lang.rust-analyzer"
      ]
    }
  }
}
```

3. Open the command palette (F1 or Ctrl+Shift+P / Cmd+Shift+P)
4. Select **"Dev Containers: Reopen in Container"**
5. VS Code will download the image and start your development environment

#### Using Docker Directly

You can also run the container directly with Docker:

```bash
docker run -it --rm -v $(pwd):/workspace -w /workspace dast1968/slough-dev-dc-rust:1.0.0
```

## Container Configuration

### User Information

- **Username**: `developer`
- **Sudo Access**: Available **without password** - you can run `sudo` commands freely without authentication
- **Shell**: Bash with Starship prompt configured for Rust development

### What's Included

This container is based on the Slough generic base image and includes:

#### Core Rust Tools

- **Rust Toolchain** (installed via Rustup):
  - `rustc` - The Rust compiler
  - `cargo` - Rust's package manager and build tool
  - `rustup` - Rust toolchain installer and version manager
  - Standard library documentation

#### Build Tools

- **build-essential**: Complete set of build tools including:
  - GCC/G++ compilers
  - make
  - libc development libraries
  - Other compilation dependencies needed for Rust crates with native dependencies

#### From Base Image

The base image (`slough-dev-dc-generic-base`) provides:
- Git for version control
- Docker CLI (when Docker socket is mounted)
- Starship prompt for an enhanced command-line experience
- Common development utilities

### Using the Installed Tools

#### Working with Rust

Create a new Rust project:
```bash
cargo new my_project
cd my_project
```

Build your project:
```bash
cargo build
```

Run your project:
```bash
cargo run
```

Run tests:
```bash
cargo test
```

Check your code without building:
```bash
cargo check
```

Format your code:
```bash
cargo fmt
```

Lint your code:
```bash
cargo clippy
```

#### Managing Rust Versions

Update Rust to the latest stable version:
```bash
rustup update
```

Install a specific toolchain:
```bash
rustup install nightly
rustup default nightly
```

Show installed toolchains:
```bash
rustup show
```

## Tips for Working with Dev Containers

### General Tips

1. **Persistent Storage**: Files in your project directory (mounted volume) persist between container restarts
2. **Extensions**: Install VS Code extensions inside the container for the best experience
3. **Git Configuration**: Configure Git inside the container or use credential helpers
4. **Port Forwarding**: VS Code automatically forwards ports from the container to your host

### Microsoft Windows Specific Tips

#### Prerequisites

1. **Install WSL 2**: Dev Containers work best with WSL 2 on Windows
   - Run `wsl --install` in PowerShell as Administrator
   - Restart your computer when prompted

2. **Install Docker Desktop**: 
   - Download from [docker.com](https://www.docker.com/products/docker-desktop)
   - Enable WSL 2 integration in Docker Desktop settings
   - In Settings → Resources → WSL Integration, enable your WSL distributions

3. **VS Code Setup**:
   - Install VS Code on Windows
   - Install the "Dev Containers" extension
   - Optionally install the "WSL" extension

#### Working on Windows

**Option 1: Work from WSL 2** (Recommended)
1. Open VS Code
2. Use the WSL extension to connect to WSL
3. Open your project folder in WSL
4. Use "Reopen in Container" from the command palette
5. This gives the best performance and compatibility

**Option 2: Work from Windows**
1. Clone your repository to your Windows file system
2. Open the folder in VS Code
3. Use "Reopen in Container" from the command palette
4. Note: File system operations may be slower compared to WSL 2

#### Common Windows Issues and Solutions

**Issue**: Slow file system performance
- **Solution**: Store your code in the WSL 2 file system (`\\wsl$\Ubuntu\home\username\`) rather than Windows file system (`C:\`)

**Issue**: Line ending conflicts
- **Solution**: Configure Git to handle line endings:
  ```bash
  git config --global core.autocrlf input
  ```

**Issue**: Docker daemon not accessible
- **Solution**: Ensure Docker Desktop is running and WSL 2 integration is enabled in Docker Desktop settings

**Issue**: Permission errors
- **Solution**: Avoid using Windows file system; work within WSL 2 file system where Unix permissions work correctly

## Development Workflow

Here's a typical development workflow with this container:

1. **Start Development**:
   - Open your project in VS Code
   - Reopen in container
   - Wait for container to start

2. **Code**:
   - Write your Rust code
   - Use `cargo check` for quick feedback
   - Run `cargo clippy` for linting suggestions
   - Format with `cargo fmt`

3. **Build and Test**:
   - Build with `cargo build` or `cargo build --release`
   - Test with `cargo test`
   - Run with `cargo run`

4. **Commit**:
   - All changes are visible on your host system
   - Commit and push using Git from inside or outside the container

## License

Copyright 2024 Daryl Stark - Licensed under the MIT License

## Contributing

This is part of the Slough project. For issues, suggestions, or contributions, please visit the [GitHub repository](https://github.com/DarylStark/slough-dev-dc-rust).
