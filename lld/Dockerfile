FROM debian

RUN apt-get update && apt-get -y upgrade \
  && apt-get -y install cmake clang python subversion git

# https://lld.llvm.org/getting_started.html
RUN mkdir /home/llvm-project && cd /home/llvm-project \
  && svn co -q http://llvm.org/svn/llvm-project/llvm/trunk llvm \
  && cd llvm/tools \
  && svn co -q http://llvm.org/svn/llvm-project/lld/trunk lld

RUN mkdir -p /home/llvm-build/llvm && cd /home/llvm-build/llvm \
  && cmake -G "Unix Makefiles" /home/llvm-project/llvm -DLLVM_EXPERIMENTAL_TARGETS_TO_BUILD=WebAssembly -DLLVM_TARGETS_TO_BUILD=WebAssembly \
  && make -j4 \
  && make check-lld

# https://github.com/cloudflare/cloudflare-workers-wasm-demo#how-to-build
RUN mkdir /home/wasm-demo && cd /home/wasm-demo \
  && git clone --recursive https://github.com/cloudflare/cloudflare-workers-wasm-demo.git \
  && make
