# Use the official Microsoft Dev Containers base image.
# It already ships with a non-root `vscode` user (UID 1000), common dev
# tools (git, curl, gnupg, sudo, etc.) and is the recommended base for
# GitHub Codespaces. This avoids UID conflicts and most user-setup issues.
FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

# Use noninteractive front-end for automated builds.
ENV DEBIAN_FRONTEND=noninteractive

# Pin TFLint version for reproducible Codespace builds.
# Bump this explicitly when you want to upgrade.
ARG TFLINT_VERSION=v0.62.0

# Install Azure CLI, Terraform and TFLint.
# - Azure CLI is installed from the official Microsoft APT repository
#   (more reliable than the `aka.ms/InstallAzureCLIDeb` bootstrap script
#   that previously failed intermittently during Codespace creation).
# - Terraform is installed from the official HashiCorp APT repository
#   using a signed-by keyring (apt-key is deprecated).
# - TFLint is installed from a pinned GitHub release, architecture-aware
#   (works on both amd64 and arm64 Codespaces).
RUN set -eux; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        gnupg \
        lsb-release \
        unzip; \
    \
    # --- Microsoft / Azure CLI repository ---------------------------------
    install -d -m 0755 /etc/apt/keyrings; \
    curl -fsSL https://packages.microsoft.com/keys/microsoft.asc \
        | gpg --dearmor -o /etc/apt/keyrings/microsoft.gpg; \
    chmod a+r /etc/apt/keyrings/microsoft.gpg; \
    AZ_DIST="$(lsb_release -cs)"; \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/microsoft.gpg] https://packages.microsoft.com/repos/azure-cli/ ${AZ_DIST} main" \
        > /etc/apt/sources.list.d/azure-cli.list; \
    \
    # --- HashiCorp / Terraform repository ---------------------------------
    curl -fsSL https://apt.releases.hashicorp.com/gpg \
        | gpg --dearmor -o /etc/apt/keyrings/hashicorp-archive-keyring.gpg; \
    chmod a+r /etc/apt/keyrings/hashicorp-archive-keyring.gpg; \
    echo "deb [signed-by=/etc/apt/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" \
        > /etc/apt/sources.list.d/hashicorp.list; \
    \
    apt-get update; \
    apt-get install -y --no-install-recommends azure-cli terraform; \
    \
    # --- TFLint (pinned release) ------------------------------------------
    ARCH="$(dpkg --print-architecture)"; \
    curl -fsSL -o /tmp/tflint.zip \
        "https://github.com/terraform-linters/tflint/releases/download/${TFLINT_VERSION}/tflint_linux_${ARCH}.zip"; \
    unzip -o /tmp/tflint.zip -d /usr/local/bin; \
    chmod +x /usr/local/bin/tflint; \
    rm -f /tmp/tflint.zip; \
    \
    # --- Cleanup ----------------------------------------------------------
    apt-get clean; \
    rm -rf /var/lib/apt/lists/*

# Smoke-test that the binaries are installed and on PATH at build time.
# If any of these fail, the image build fails fast with a clear error.
RUN az version && terraform -version && tflint --version

# Default to the non-root `vscode` user provided by the base image.
USER vscode

LABEL org.opencontainers.image.source="https://github.com/patkoch/azure-terraform-codespace" \
      org.opencontainers.image.description="Devcontainer image with Azure CLI, Terraform and TFLint"
