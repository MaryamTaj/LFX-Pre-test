# LFX-Mentorship-Proposal-3170

## About:
This repository includes the pre-test for the LFX Mentorship (Mar-May, 2024) Proposal #3170: Integrate whisper.cpp as a new WASI-NN backend. You can find more details here: https://github.com/WasmEdge/WasmEdge/issues/3170

## Installation: 

### Local Version:
To create a local version of the remote repository, I cloned it using the terminal.
1. `$ git clone https://github.com/WasmEdge/WasmEdge.git`
2. `git checkout hydai/0.13.5_ggml_lts`

### Software Dependencies:
I also installed the following dependencies:
1. Cmake: `$ brew install cmake`
2. Ninja: `$ brew install ninja`
3. LLVM: `$ brew install llvm`

### Build WasmEdge with WASI-NN llama.cpp Backend:
I followed this [guide](https://wasmedge.org/docs/contribute/source/plugin/wasi_nn/#build-wasmedge-with-wasi-nn-llamacpp-backend) to build WasmEdge with WASI-NN llama.cpp backend.   
```bash
$ cmake -GNinja -Bbuild -DCMAKE_BUILD_TYPE=Release \  
  -DWASMEDGE_PLUGIN_WASI_NN_BACKEND="GGML" \  
  -DWASMEDGE_PLUGIN_WASI_NN_GGML_LLAMA_METAL=ON \  
  -DWASMEDGE_PLUGIN_WASI_NN_GGML_LLAMA_BLAS=OFF \  
  .
```
