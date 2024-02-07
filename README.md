# LFX-Mentorship-Proposal-3170

## About:
This repository includes the pre-test for the LFX Mentorship (Mar-May, 2024) Proposal #3170: Integrate whisper.cpp as a new WASI-NN backend. You can find more details here: https://github.com/WasmEdge/WasmEdge/issues/3170

## Build: 

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
<img src="https://github.com/MaryamTaj/LFX-Pre-test/blob/main/cmake" width="200" height="200">

```bash
$ cmake --build build
  cmake –install build
```
<img src="https://github.com/MaryamTaj/LFX-Pre-test/blob/main/cmake%20%E2%80%93install%20build" width="200" height="200">

## Model Selection:
I chose the larger llama-2-13b parameter model, because it can answer more complex questions. I was curious to see its capabilities!

1. I downloaded the pre-built WASM application llama/wasmedge-ggml-llama.wasm, provided by this [repository](https://github.com/second-state/WasmEdge-WASINN-examples/blob/master/wasmedge-ggml/README.md).
2. I downloaded the llama model:
   <br>
`$ curl -LO https://huggingface.co/TheBloke/Llama-2-7b-Chat-GGUF/resolve/main/llama-2-7b-chat.Q5_K_M.gguf`

## Execution:
1. I executed the WASM with the wasmedge using the named model feature to preload a large model:
```bash
wasmedge --dir .:. \
  --nn-preload default:GGML:AUTO:llama-2-7b-chat.Q5_K_M.gguf \
  wasmedge-ggml-llama.wasm default
```
