FROM debian:stable

RUN apt-get update && apt-get -y upgrade \
  && apt-get install -y cmake python ninja-build g++ git

RUN git clone https://github.com/llvm-mirror/llvm --branch release_70 /llvm \
 && git clone https://github.com/llvm-mirror/clang --branch release_70 /llvm/tools/clang \
 && git clone https://github.com/llvm-mirror/lld --branch release_70 /llvm/tools/lld \
 && mkdir /build && cd /build \
 && cmake -G Ninja -DLLVM_EXPERIMENTAL_TARGETS_TO_BUILD=WebAssembly -DCMAKE_BUILD_TYPE=release -DCMAKE_INSTALL_PREFIX=/usr/ /llvm \
 && ninja \
 && ninja install \
 && cd / \
 && rm -rf build llvm

# https://github.com/cloudflare/cloudflare-workers-wasm-demo#how-to-build
RUN git clone --recursive https://github.com/cloudflare/cloudflare-workers-wasm-demo.git /wasm-demo \
  && cd /wasm-demo \
  && make
