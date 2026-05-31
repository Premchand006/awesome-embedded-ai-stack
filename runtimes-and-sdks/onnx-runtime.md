# ONNX Runtime

The portable backbone of edge inference. Export almost any model to the open **ONNX** format, then run it across CPUs, GPUs, and NPUs by selecting an **Execution Provider (EP)** — write once, deploy widely.

- **Site/docs:** [onnxruntime.ai](https://onnxruntime.ai/)
- **Repo:** [microsoft/onnxruntime](https://github.com/microsoft/onnxruntime) · **Samples:** [onnxruntime-inference-examples](https://github.com/microsoft/onnxruntime-inference-examples)
- **Latest:** **v1.26.0 (May 2026)**. ORT now ships on a **monthly** cadence.

## Execution Providers (the key concept)
An EP delegates execution to a hardware backend. You keep the same model + API and swap the EP per target:

| EP | Targets |
|---|---|
| **CPU** (MLAS / KleidiAI) | x86 + Arm (default, always available) |
| **CUDA** / **TensorRT** | NVIDIA GPUs / Jetson |
| **OpenVINO** | Intel CPU/iGPU/NPU/Arc |
| **QNN** | Qualcomm Hexagon NPU |
| **DirectML** | any DirectX 12 GPU on Windows |
| **CoreML** | Apple silicon |
| **WebGPU / WebNN** | browser / web |

> ⚠️ **Removed in 1.26.0:** the **ArmNN EP**. Drop `--use_armnn`; on Arm use the **CPU EP** (MLAS/KleidiAI) or **QNN** for Qualcomm. ([deprecations](../renames-and-deprecations.md))

The OpenVINO EP is distributed via Intel's fork ([intel/onnxruntime](https://github.com/intel/onnxruntime)); recent builds pair ORT with OpenVINO 2025.x.

## Minimal example
```python
import onnxruntime as ort
import numpy as np

# Choose providers in priority order; ORT falls back left-to-right.
providers = ["TensorrtExecutionProvider", "CUDAExecutionProvider", "CPUExecutionProvider"]
sess = ort.InferenceSession("model.onnx", providers=providers)

inputs = {sess.get_inputs()[0].name: np.random.rand(1, 3, 640, 640).astype(np.float32)}
outputs = sess.run(None, inputs)
print(outputs[0].shape)
```

## Where it fits in this repo
- **Portability-first projects** and the [ONNX → edge export path](../deployment-and-optimization/).
- IoT/edge fleet deployment patterns: see [edge-pipelines](../edge-pipelines/).
- Quantize ONNX models with ORT's quantization tools ([optimization](../deployment-and-optimization/)).

**Strengths:** broadest hardware reach, stable API, strong tooling. **Trade-off:** a dedicated vendor runtime (TensorRT/OpenVINO) can edge out ORT on peak throughput for a fixed target.
