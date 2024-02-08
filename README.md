# LFX-Mentorship-Proposal-3170

## About:
This repository includes the pre-test for the LFX Mentorship (Mar-May, 2024) Proposal #3170: Integrate whisper.cpp as a new WASI-NN backend. You can find more details here: https://github.com/WasmEdge/WasmEdge/issues/3170

## Build: 

### Local Version:
To create a local version of the remote repository, I cloned it using the terminal.
1. `$ git clone https://github.com/WasmEdge/WasmEdge.git`
2. `$ git checkout hydai/0.13.5_ggml_lts`

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
```bash
$ cmake --build build
  cmake –install build
```
![cmake_build](https://github.com/MaryamTaj/LFX-Pre-test/assets/109046900/19c04133-76e2-48c9-a6c3-5c5fc62ebc01)

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
![execution](https://github.com/MaryamTaj/LFX-Pre-test/assets/109046900/9b591ed2-eedb-411b-98da-2b1c0c4890fa)

## whisper.cpp

1. To create a local version of the remote repository, I cloned it using the terminal:
   <br>
` $ git clone https://github.com/ggerganov/whisper.cpp.git`
2. I downloaded a Whisper model converted in ggml format:
   <br>
` $ bash ./models/download-ggml-model.sh base.en`
3. I then built the main example:
   <br>
` $ make`
![make](https://github.com/MaryamTaj/LFX-Pre-test/assets/109046900/e9582cf7-eed3-42a4-a8d6-4f408dac99da)


5. I transcribed the audio file:
   <br>
`$ ./main -f samples/jfk.wav`
![transcribe](https://github.com/MaryamTaj/LFX-Pre-test/assets/109046900/c4563026-4221-4c3b-8111-dc065c08e063)

6. I created a real-time audio input example:
   <br>
   I first installed sdl2, a library designed to provide low level access to audio, keyboard, mouse, joystick, and graphics hardware:
   <br>
   `$ brew install sdl2`
  ```bash
  make stream
  ./stream -m ./models/ggml-base.en.bin -t 8 --step 500 --length 5000
  ```
https://github.com/MaryamTaj/LFX-Pre-test/assets/109046900/1d29087b-6b0d-4dd6-b0c1-5adb3f4ccd39



