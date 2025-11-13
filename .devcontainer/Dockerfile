FROM ubuntu:22.04

# Use noninteractive front-end for automated builds
ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Etc/UTC

# Minimal, consolidated RUN to reduce layers and improve caching.
# - use --no-install-recommends to keep image small
# - install required tools (curl, gnupg, lsb-release, unzip, git, wget)
# - install Azure CLI using official script (run as root inside container)
# - add HashiCorp repo using a signed keyring (apt-key is deprecated)
# - install terraform from HashiCorp repo
# - install latest TFLint binary from GitHub releases
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    ca-certificates \
    curl \
    gnupg \
    lsb-release \
    software-properties-common \
    unzip \
    wget \
    git \
    openssh-client && \
    \
    # Install Azure CLI (official script). No sudo needed in container.
    curl -sL https://aka.ms/InstallAzureCLIDeb | bash && \
    \
    # Add HashiCorp GPG key and repository (use signed-by to avoid apt-key)
    curl -fsSL https://apt.releases.hashicorp.com/gpg | gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" > /etc/apt/sources.list.d/hashicorp.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends terraform && \
    \
    # Install latest TFLint release (linux amd64)
    TFLINT_VER=$(curl -s https://api.github.com/repos/terraform-linters/tflint/releases/latest | grep -Po '"tag_name": "\K[^"]+') && \
    curl -Lo /tmp/tflint.zip "https://github.com/terraform-linters/tflint/releases/download/${TFLINT_VER}/tflint_linux_amd64.zip" && \
    unzip /tmp/tflint.zip -d /tmp && mv /tmp/tflint /usr/local/bin/tflint && chmod +x /usr/local/bin/tflint && rm -rf /tmp/tflint* && \
    \
    # Cleanup apt caches to keep image small
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Provide metadata
LABEL org.opencontainers.image.source="https://github.com/patkoch/azure_terraform_codespace" \
      org.opencontainers.image.description="Devcontainer base image with Azure CLI, Terraform, and TFLint"

# NOTE: Consider adding a non-root user or exposing versions via ARGs depending on how the devcontainer is used.