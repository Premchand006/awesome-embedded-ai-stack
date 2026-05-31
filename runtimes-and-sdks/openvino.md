# OpenVINO

Intel's inference toolkit for **CPU, integrated GPU, NPU (Core Ultra), and Arc** GPUs — the best way to use x86 silicon you already own, and increasingly capable for on-device generative AI.

- **Docs:** [docs.openvino.ai](https://docs.openvino.ai/) · **Repo:** [openvinotoolkit/openvino](https://github.com/openvinotoolkit/openvino)
- **Notebooks (great for learning):** [openvino_notebooks](https://github.com/openvinotoolkit/openvino_notebooks)
- **Releases:** quarterly — 2025.0 → 2025.4 (2025); **2026.0** adds an NPU ahead-of-time/on-device compiler (no OEM driver dependency).

## How it works
1. **Get a model** — from **Hugging Face** via **`optimum-intel`**, or convert your own with **OVC** (OpenVINO Model Converter) / `openvino.convert_model()`.
2. **Compile for a device** — `CPU`, `GPU`, `NPU`, or `AUTO` (let OpenVINO choose/distribute).
3. **Infer** — synchronous or async; the same model runs across devices.

```python
import openvino as ov
core = ov.Core()
print(core.available_devices)           # e.g. ['CPU', 'GPU', 'NPU']
model = core.read_model("model.xml")    # or convert_model(...)
compiled = core.compile_model(model, "AUTO")
result = compiled([input_tensor])
```

## Generative AI & compression
- **OpenVINO GenAI** — the supported path for LLMs/VLMs on Intel hardware.
- **NNCF** — Neural Network Compression Framework for INT8 PTQ and INT4/INT8 weight compression (use **`nncf.quantize()`**; `create_compressed_model()` is deprecated). See [optimization](../deployment-and-optimization/).

## ⚠️ Deprecations to know
- The legacy **Model Optimizer (`mo`)**, the **`openvino-dev`** package, and the **Open Model Zoo** are deprecated/removed. Use **OVC** + **optimum-intel/Hugging Face** instead. ([details](../renames-and-deprecations.md))

## Where it fits
- The **[Intel & AMD hardware page](../hardware-landscape/intel-and-amd.md)** for device coverage.
- The **OpenVINO Execution Provider** in [ONNX Runtime](onnx-runtime.md) if you want portability.
- **Intel DL Streamer** (GStreamer-based) for video pipelines, mirroring DeepStream on the Intel side.

**Strengths:** no new hardware, mature, excellent learning notebooks, strong CPU/iGPU/NPU coverage. **Trade-off:** peak throughput trails a dedicated GPU/NPU card for the heaviest workloads.
