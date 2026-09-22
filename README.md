## Build

```
make           # CPU backend
make cuda      # CUDA backend
```

The default GPU architecture is `sm_89`. Override `CUDA_ARCH` to target a
different architecture.

## Download the model

```
hf download carmelosca/gpt2-fp32-gguf --local-dir models --include gpt2-small-fp32.gguf
```

## Run

```
./gpt2 --model <model.gguf> [options]
```

Options:

- `--model <file>`       model file (required)
- `--prompt-length <n>`  number of input tokens (default 10)
- `--max-tokens <n>`     maximum tokens to generate (default 100)
- `--show-gguf`          print GGUF metadata and exit
- `--show-stats`         print prefill/decode timings
- `--help`

Example:

```
./gpt2 --model models/gpt2-small-fp32.gguf --prompt-length 512 --max-tokens 128
```

## Project structure

```
src/
  gguf.c/.h                GGUF parsing
  model.c/.h               Model description and tensor loading
  transformer.c/.h         Forward pass and KV cache
  backend.h                Backend abstraction
  backend/backend_cpu.c    CPU backend
  backend/backend_cuda.cu  CUDA backend
  backend/kernels_cuda.cu  CUDA kernels
  main.c                   Command-line interface
```
