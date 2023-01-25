FROM alpine:3.14

RUN apk add musl-dev
# Install Curl for Rust Install
RUN apk add curl 
# Install ca-certificates for https connection
RUN apk add ca-certificates 
# Install Nightly Rust Toolchain
RUN curl --proto '=https' \
         --tlsv1.2 -sSf https://sh.rustup.rs | \
         sh -s -- --default-toolchain nightly -y
ENV PATH=$PATH:/root/.cargo/bin
# Install wasm-bindgen-cli & Add WASM32 Rust Target
RUN source /root/.cargo/env; \
    cargo install -f wasm-bindgen-cli; \
    rustup target add wasm32-unknown-unknown; 
# Install GCC Compiler
RUN apk add gcc

RUN apk add make

ENV ROCKET_ADDRESS=0.0.0.0
EXPOSE 8000

# Copy this directory (Rust Code) into Docker Image
COPY ./ ./
# Run Rust Code
# CMD ["cargo", "run --release"]
ENTRYPOINT ./entrypoint.sh
