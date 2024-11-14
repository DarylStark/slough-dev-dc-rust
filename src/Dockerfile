# hadolint ignore=DL3007
FROM dast1986/slough-dev-dc-generic-base:latest AS base

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Configure Starship
ENV PROMPTNAME="RUST"

# Download and install Rustup
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y

# Set the default command to bash
CMD ["bash"]