# SAM3 Speedup Wheels

Pre-built CUDA extension wheels for [ComfyUI-SAM3](https://github.com/PozzettiAndrea/ComfyUI-SAM3) GPU acceleration.

These wheels provide **5-10x faster video tracking** without requiring users to compile CUDA extensions themselves.

## Packages

| Package | Description | Source |
|---------|-------------|--------|
| torch_generic_nms | GPU-accelerated Non-Maximum Suppression | [ronghanghu/torch_generic_nms](https://github.com/ronghanghu/torch_generic_nms) |
| cc_torch | GPU-accelerated Connected Components | [ronghanghu/cc_torch](https://github.com/ronghanghu/cc_torch) |

## Installation

### Automatic (Recommended)

The easiest way is through ComfyUI-SAM3's speedup script:

```bash
cd ComfyUI/custom_nodes/ComfyUI-SAM3
python speedup.py
```

### Manual Installation

Find your CUDA and PyTorch versions:
```bash
python -c "import torch; print(f'CUDA: {torch.version.cuda}'); print(f'PyTorch: {torch.__version__}')"
```

Then install with the matching wheels:

```bash
# CUDA 12.6 + PyTorch 2.8.x (recommended for most users)
pip install torch_generic_nms cc_torch --find-links https://pozzettiandrea.github.io/sam3-speedup-wheels/cu126/

# CUDA 12.8 + PyTorch 2.9.x (latest)
pip install torch_generic_nms cc_torch --find-links https://pozzettiandrea.github.io/sam3-speedup-wheels/cu128/

# CUDA 12.4 + PyTorch 2.5.x (stable fallback)
pip install torch_generic_nms cc_torch --find-links https://pozzettiandrea.github.io/sam3-speedup-wheels/cu124/
```

## Available Builds

| CUDA | PyTorch | Python | Linux | Windows |
|------|---------|--------|-------|---------|
| 12.4 | 2.5.1 | 3.10, 3.11, 3.12 | ✅ | ✅ |
| 12.6 | 2.6.0 | 3.10, 3.11, 3.12, 3.13 | ✅ | ✅ |
| 12.6 | 2.8.1 | 3.10, 3.11, 3.12, 3.13 | ✅ | ✅ |
| 12.8 | 2.8.1 | 3.10, 3.11, 3.12, 3.13 | ✅ | ✅ |
| 12.8 | 2.9.1 | 3.10, 3.11, 3.12, 3.13 | ✅ | ✅ |

## GPU Architecture Support

Wheels are compiled for the following CUDA architectures:

| Compute Capability | Architecture | GPUs |
|--------------------|--------------|------|
| SM 7.5 | Turing | RTX 20 series |
| SM 8.6 | Ampere | RTX 30 series |
| SM 8.9 | Ada Lovelace | RTX 40 series |
| SM 9.0 | Hopper | H100 |
| SM 10.0 | Blackwell | RTX 50 series |

## Why Pre-built Wheels?

Building CUDA extensions requires:
- CUDA Toolkit with nvcc compiler
- C++ compiler (Visual Studio on Windows)
- Matching versions of everything

Many users hit compilation errors. These pre-built wheels skip all that complexity.

## Building Locally

If you need a specific configuration not provided here:

```bash
# Clone the source repos
git clone https://github.com/ronghanghu/torch_generic_nms.git
git clone https://github.com/ronghanghu/cc_torch.git

# Set your GPU architecture (e.g., 8.6 for RTX 30 series)
export TORCH_CUDA_ARCH_LIST="8.6"

# Build
cd torch_generic_nms && pip install . && cd ..
cd cc_torch && pip install . && cd ..
```

## License

- torch_generic_nms: BSD-3-Clause (Meta)
- cc_torch: BSD-3-Clause (Meta)

## Related

- [ComfyUI-SAM3](https://github.com/PozzettiAndrea/ComfyUI-SAM3) - The main SAM3 custom node
- [SAM3 by Meta](https://github.com/facebookresearch/sam3) - Segment Anything Model 3
