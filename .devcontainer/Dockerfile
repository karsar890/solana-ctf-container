FROM ubuntu:24.04

WORKDIR /workspace

RUN apt-get update && apt-get install -y \
    build-essential \
    pkg-config \
    libudev-dev \
    llvm \
    libclang-dev \
    protobuf-compiler \
    libssl-dev \
    curl \
    git \
    python3 \
    python3-pip \
    python3-venv \
    && rm -rf /var/lib/apt/lists/*

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y

ENV PATH="/root/.cargo/bin:$PATH"

ENV NVM_DIR="/root/.nvm"

RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash \
    && . "$NVM_DIR/nvm.sh" \
    && nvm install node \
    && nvm use node \
    && npm install --global yarn

ENV PATH="$NVM_DIR/versions/node/$(. $NVM_DIR/nvm.sh && nvm which current | xargs dirname):$PATH"

RUN sh -c "$(curl -sSfL https://release.anza.xyz/stable/install)"

ENV PATH="/root/.local/share/solana/install/active_release/bin:$PATH"

RUN cargo install --git https://github.com/solana-foundation/anchor avm --force

RUN /root/.cargo/bin/avm install latest && /root/.cargo/bin/avm use latest
