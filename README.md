# Ikuno-Dictus-Feet

Just a place to put my AI stuff as I learn.

Don't expect anything useful. 😄

Everything here is tested only on my personal setup. Results may vary depending on hardware, quantization, inference engine, prompt format, and model version.

The goal of this repository is learning, experimentation, and sharing.

## Workstation

- ASUS ROG Zephyrus G GU502DU
- Windows 11 + WSL
- 16 GB DDR4 RAM
- NVIDIA GPU (6 GB VRAM)
- 4 cores / 8 threads

## AI Stack

- Hermes
- llama.cpp
- llama.cpp-turboquant

## Current Local Models

### Qwen3.6-28B-REAP20-A3B (Q3_K_S)

Used for:
- Planning
- Research
- Coding assistance
- Skill testing

Configuration available in:
`configs/qwen36-28b-reap20-a3b.md`

### Qwen3.5-9B-NSC-ACE-SABER (Q4_K_M)

Status:
- Currently being optimized on llama.cpp
- Testing blocked by a llama.cpp-turboquant issue

## Cloud Models

Used primarily for planning, reviews, validation, and comparison:

- Claude (free tier)
- ChatGPT (free tier)
- Gemini (free tier)
- Grok (free tier)
- DeepSeek (free tier)

## License

MIT
