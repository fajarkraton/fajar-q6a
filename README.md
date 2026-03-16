# fajar-q6a

> Fajar Lang hardware runtime for **Radxa Dragon Q6A** (Qualcomm QCS6490) — BSP, GPU, NPU, GPIO, examples, and deployment tools.

## Hardware

| Component | Detail |
|-----------|--------|
| **SoC** | Qualcomm QCS6490, TSMC 6nm |
| **CPU** | Kryo 670: 1xA78@2.71GHz + 3xA78@2.4GHz + 4xA55@1.96GHz |
| **GPU** | Adreno 643 @ 812MHz — Vulkan 1.3 (Mesa Turnip), OpenCL 3.0 |
| **NPU** | Hexagon 770 V68 — 12 TOPS INT8, QNN SDK v2.40 |
| **RAM** | 8GB LPDDR5 @ 3200MHz |
| **Storage** | 238GB Samsung NVMe PM9C1a (536 MB/s read) |
| **GPIO** | 40-pin header, 27 usable pins |

## Structure

```
fajar-q6a/
├── bsp/          ← Board Support Package (dragon_q6a module + Vulkan compute)
├── examples/     ← 55+ Q6A-specific .fj programs
├── models/       ← ONNX + QNN DLC models for NPU inference
├── docs/         ← Hardware guides, QNN setup, GPU compute, quickstart
└── scripts/      ← ONNX → QNN export pipeline
```

## Quick Start

```bash
# Install Fajar Lang compiler
git clone https://github.com/fajarkraton/fajar-lang
cd fajar-lang && cargo build --release
export PATH="$PWD/target/release:$PATH"

# Run on Q6A
scp target/aarch64-unknown-linux-gnu/release/fj radxa@192.168.50.94:~/
scp examples/q6a_blinky.fj radxa@192.168.50.94:~/
ssh radxa@192.168.50.94 "./fj run q6a_blinky.fj"
```

## Status

**v2.0 "Dawn"** — 222/240 tasks complete (93%)

- Vulkan compute: 6 SPIR-V kernels on Adreno 643
- QNN NPU pipeline: ONNX → DLC INT8 → inference on Q6A
- Cranelift AOT: native ARM64 ELF binaries
- 5,888 tests pass on Q6A hardware

## Related Repos

- [fajar-lang](https://github.com/fajarkraton/fajar-lang) — Compiler & runtime
- [fajar-os](https://github.com/fajarkraton/fajar-os) — FajarOS "Surya" (OS written in Fajar Lang)

## License

MIT
