# Qwen3.6-28B-REAP20-A3B (Q3_K_S)

## Hardware

- ASUS ROG Zephyrus G GU502DU
- 16 GB DDR4 RAM
- NVIDIA GPU (6 GB VRAM)
- Windows 11 + WSL

## Software

- llama.cpp-turboquant
- Hermes

## Notes

Current configuration used for testing and experimentation.

Results may vary depending on:
- llama.cpp version
- turboquant version
- GPU
- available RAM
- prompt format

## Launch Command

```bash
#!/bin/bash

./build/bin/llama-server \
  --jinja \
  -m ~/models/qwen28-reap/Qwen3.6-28B-REAP20-A3B-Q3_K_S.gguf \
  -c 65536 \
  -ngl 24 \
  -t 7 \
  -np 1 \
  --batch-size 1024 \
  --ubatch-size 1024 \
  --cache-type-k q8_0 \
  --cache-type-v turbo4 \
  --host 0.0.0.0 \
  --port 8081
```

## Performance Notes

### Strengths

- Planning
- Research
- Code review
- Architecture discussions

### Limitations

- Still being evaluated

## Last Updated

2026-06-04
