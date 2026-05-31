# Runtimes & SDKs

"**Which runtime do I use?**" is the single most common edge-AI question — and the honest answer is that your **hardware mostly decides for you**. This section maps each runtime to where it shines, with deep-dive pages for the big ones.

## Selection matrix

| Your target hardware | Primary runtime | Video pipeline | Notes |
|---|---|---|---|
| NVIDIA GPU / Jetson | **TensorRT** | **DeepStream** | DeepStream is built on GStreamer |
| Intel CPU / iGPU / NPU / Arc | **OpenVINO** | Intel DL Streamer | + OpenVINO GenAI for LLMs |
| Qualcomm Snapdragon (Hexagon) | **Qualcomm AI Hub** → LiteRT/ONNX RT/QNN | — | 150+ pre-optimized models |
| Microcontroller (ESP32, Cortex-M) | **LiteRT for Microcontrollers** | — | kB–MB of RAM |
| Phone / generic on-device | **LiteRT** (was TF Lite) | — | `.tflite` format |
| "Run my ONNX anywhere" | **ONNX Runtime** (+EP) | via GStreamer/app | EP picks the backend |
| Rockchip RK3588 | **RKNN-Toolkit2 / rkllm** | GStreamer | convert from ONNX/PyTorch |
| AMD Ryzen AI | **Ryzen AI Software** (ONNX) | — | Vitis AI Quantizer (ONNX) |

## The two mental models

1. **Vendor runtime (max performance):** TensorRT (NVIDIA), OpenVINO (Intel), HailoRT (Hailo), RKNN (Rockchip). Best throughput on *that* silicon; least portable.
2. **Portable runtime (write once):** **ONNX Runtime** with an **Execution Provider** that delegates to the vendor backend (CUDA/TensorRT, OpenVINO, QNN, DirectML, CoreML…). Slightly less peak performance, far more portable.

A common production pattern: **prototype with ONNX Runtime**, then **switch the Execution Provider** (or drop to TensorRT/OpenVINO directly) once you've locked the target hardware.

## Deep-dive pages
- [**ONNX Runtime**](onnx-runtime.md) — the portable backbone; Execution Providers explained.
- [**LiteRT** (formerly TensorFlow Lite) & TFLite-Micro](litert.md) — phones, SBCs, microcontrollers.
- [**TensorRT & DeepStream**](tensorrt-and-deepstream.md) — NVIDIA's max-throughput inference + video analytics.
- [**OpenVINO**](openvino.md) — Intel CPU/iGPU/NPU/Arc + GenAI.

## Also relevant
- **Qualcomm AI Hub** ([aihub.qualcomm.com](https://aihub.qualcomm.com/)) — compile/benchmark/deploy **150+** models to Snapdragon; export to LiteRT, ONNX Runtime, or **QNN**. Repo: [qualcomm/ai-hub-models](https://github.com/quic/ai-hub-models).
- **Apache TVM** ([tvm.apache.org](https://tvm.apache.org/)) — a compiler stack (now a top-level Apache project, latest **v0.22.0**, **TVM Unity** = Relax + TensorIR). Underpins **MLC-LLM** and several vendor compilers (e.g., Axelera Voyager). Use it when you need to target hardware without a first-party runtime, or to squeeze a specific model.
- **Model optimization** (quantization/pruning) lives in [deployment-and-optimization](../deployment-and-optimization/): OpenVINO **NNCF**, **ONNX Runtime quantization**, **TensorRT Model Optimizer**.
