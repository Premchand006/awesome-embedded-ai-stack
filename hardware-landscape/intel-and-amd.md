# Intel (OpenVINO) & AMD (Ryzen AI)

The "you already own the hardware" path. If you have a recent x86 laptop or edge server, you can run accelerated inference on its **CPU, integrated GPU, and NPU** without buying anything — and scale to discrete GPUs/cards later.

## Intel + OpenVINO
**OpenVINO** is Intel's inference toolkit spanning **CPU, iGPU, NPU (Core Ultra), and Arc** GPUs (including the **Arc Pro B-series**). It's especially strong for x86 edge servers and increasingly for on-device GenAI.

- **Docs/repo:** [docs.openvino.ai](https://docs.openvino.ai/) · [openvinotoolkit/openvino](https://github.com/openvinotoolkit/openvino) · [notebooks](https://github.com/openvinotoolkit/openvino_notebooks)
- **Releases:** quarterly — 2025.0 → 2025.4 (2025), **2026.0** (adds an NPU ahead-of-time/on-device compiler).
- **GenAI:** **OpenVINO GenAI** is the LLM/VLM path; **NNCF** handles INT8/INT4 compression.

> ⚠️ **Deprecations:** the legacy **Model Optimizer**, the **`openvino-dev`** package, and the **Open Model Zoo** are deprecated/removed. Convert with **OVC** and pull models from **Hugging Face via `optimum-intel`**. ([details](../renames-and-deprecations.md))

**Strengths/trade-offs:** ✅ no new hardware; mature tooling and notebooks; great CPU/iGPU/NPU coverage. ⚠️ raw throughput trails a dedicated GPU/NPU card for heavy workloads.

→ Runtime page: [OpenVINO](../runtimes-and-sdks/openvino.md).

## AMD Ryzen AI (XDNA / XDNA 2 NPU)
AMD brings NPUs to x86 laptops and, newly, to **embedded/industrial/automotive** parts.

- **Docs:** [AMD Ryzen AI Software](https://www.amd.com/en/developer/resources/ryzen-ai-software.html)
- **NPUs:** **XDNA 2** up to **50 TOPS** on **Ryzen AI 300 / Ryzen AI Max** (Jan 2025); new **Ryzen AI 400 / PRO 400** up to **60 TOPS** (CES 2026).
- **Embedded:** **Ryzen AI Embedded P100 / X100** (Jan 2026) bring XDNA 2 (up to 50 TOPS) to physical-AI/industrial designs with a Xen-hypervisor-based stack.
- **Software:** **Ryzen AI Software** (an ONNX-based flow with the **Vitis AI Quantizer for ONNX**), plus Turnkey/Lemonade tools; **ROCm** is expanding to Ryzen AI 400 on Windows/Linux.

**Strengths/trade-offs:** ✅ NPUs in mainstream and embedded x86; ONNX-centric workflow; growing ROCm story. ⚠️ ecosystem/tooling is younger than NVIDIA/Intel; verify model coverage for your use case.

## Which one?
- Already on an **Intel** machine → **OpenVINO** (most mature, best notebooks).
- Already on an **AMD Ryzen AI** machine → **Ryzen AI Software** (ONNX flow).
- Need **portability across both** → **[ONNX Runtime](../runtimes-and-sdks/onnx-runtime.md)** with the OpenVINO or appropriate Execution Provider.
