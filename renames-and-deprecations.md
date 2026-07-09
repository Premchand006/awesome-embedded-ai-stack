# Renames & Deprecations (2024–2026)

> [!IMPORTANT]
> **This is the canonical Renames & Deprecations page.** The companion repos
> [`awesome-edge-ai`](https://github.com/Premchand006/awesome-edge-ai) and
> [`awesome-physical-ai`](https://github.com/Premchand006/awesome-physical-ai) link here instead of
> keeping their own copies, so there is a single source of truth to maintain. Found something stale?
> Fix it here.

The edge-AI ecosystem renamed, deprecated, and discontinued a lot between 2024 and 2026. Following an old tutorial can send you down a dead end — buying an abandoned accelerator, or `pip install`-ing a package that no longer exists. This page is the cheat-sheet. **Verify against the linked official source before acting**; dates are when the change was announced/confirmed.

> **How to use this page:** before buying hardware or choosing a runtime, scan the relevant row. If a guide you're following predates the change, treat its product names and install commands with suspicion.

---

## 🔴 Discontinued / abandoned

### Google Coral / Edge TPU — *effectively discontinued*
- **What happened:** the original Coral product line is no longer practically usable for new projects. The out-of-tree **Apex/GASKET PCIe driver was removed from the Linux kernel staging tree**, upstream `tflite-runtime` hasn't carried Coral patches for years, and stock is essentially zero across distributors. Community DKMS rebuilds exist but are fragile.
- **What to do instead:** for low-cost CV at the edge, use **Hailo** (Raspberry Pi AI HAT+ / AI HAT+ 2, or a discrete Hailo-8/8L/10H). See [hardware-landscape/raspberry-pi-and-hailo.md](hardware-landscape/raspberry-pi-and-hailo.md).
- **Note:** Google announced a *new*, unrelated open-source **"Coral NPU"** — a **RISC-V-based architecture/IP for silicon partners**, not a drop-in replacement product. Don't treat it as a ready Edge-TPU successor.
- **Source:** `coral.ai`; community reports (e.g., Frigate's deprecation discussion, `google-coral/edgetpu` issues).

### Raspberry Pi AI Kit — *discontinued*
- **What happened:** the original **AI Kit (Hailo-8L, 13 TOPS)** is "no longer in production."
- **What to do instead:** buy the **AI HAT+** (13 or 26 TOPS) or the newer **AI HAT+ 2** (Hailo-10H, 40 TOPS INT4, 8 GB on-board RAM, adds local LLM/VLM/GenAI). Production of the HAT+ 2 is guaranteed into 2036.
- **Source:** [raspberrypi.com/documentation/computers/ai.html](https://www.raspberrypi.com/documentation/computers/ai.html).

---

## 🟠 Renamed

### TensorFlow Lite → **LiteRT**
- **What happened:** in **September 2024** Google rebranded *TensorFlow Lite* as **LiteRT** ("Lite Runtime"). In **TensorFlow 2.20 (Aug 2025), `tf.lite` was deprecated** and on-device development moved to the standalone LiteRT project.
- **What stays the same:** the **`.tflite` file format is unchanged**; existing models keep working.
- **What to change:**
  - Python: `pip install tflite-runtime` → **`pip install ai-edge-litert`**; `import tflite_runtime` → `from ai_edge_litert.interpreter import Interpreter`.
  - Android (Maven): `org.tensorflow:tensorflow-lite` → **`com.google.ai.edge.litert`**.
- **Microcontrollers:** the MCU path is **LiteRT for Microcontrollers**, still developed in the **`tensorflow/tflite-micro`** repo.
- **Source:** [ai.google.dev/edge/litert/migration](https://ai.google.dev/edge/litert/migration), [github.com/google-ai-edge/LiteRT](https://github.com/google-ai-edge/LiteRT).

---

## 🟡 Deprecated within a still-active product

### OpenVINO: Model Optimizer & Open Model Zoo → **OVC + Hugging Face/optimum-intel**
- **What happened:** the legacy **Model Optimizer (`mo`)**, the **`openvino-dev`** package, and the **Open Model Zoo** are deprecated/removed.
- **What to do instead:** convert models with **OVC** (OpenVINO Model Converter) or `openvino.convert_model()`; get models from **Hugging Face** via **`optimum-intel`**. Use **OpenVINO GenAI** for LLM/VLM workflows and **NNCF** for compression (note `create_compressed_model()` is deprecated → use `nncf.quantize()`).
- **Source:** [docs.openvino.ai](https://docs.openvino.ai/) release notes (2025.x / 2026.0).

### ONNX Runtime: ArmNN Execution Provider removed
- **What happened:** the **ArmNN EP was removed in ONNX Runtime 1.26.0 (May 2026)**. ORT also moved to a **monthly** release cadence.
- **What to do instead:** drop `--use_armnn`; use the MLAS/KleidiAI-accelerated **CPU EP** on Arm, or the **QNN EP** for Qualcomm hardware.
- **Source:** [github.com/microsoft/onnxruntime/releases](https://github.com/microsoft/onnxruntime/releases).

---

## 🟢 New & noteworthy (not a deprecation, but changes your defaults)

### Jetson AGX Thor shipped (Aug 2025)
- **Up to 2,070 FP4 TFLOPS, 128 GB, 40–130 W**, Blackwell GPU; Developer Kit **$3,499**; runs **JetPack 7** (Ubuntu 24.04). A lower-power **T4000** module (1,200 FP4 TFLOPS, 64 GB) followed at CES 2026; **JetPack 7.1** is current. This is NVIDIA's flagship "runtime computer" for Physical AI / humanoids.
- **Source:** [Jetson Thor product page](https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/jetson-thor/).

### Jetson Orin Nano "Super" (Dec 2024)
- A **software unlock** turned the 40-TOPS Orin Nano into **67 TOPS (INT8)** at **$249**, via **JetPack 6.2**. If a tutorial quotes 40 TOPS, it predates the Super profile.

### ROS 2 LTS is now **Lyrical Luth** (May 22, 2026)
- Latest **LTS**, supported to **May 2031** (Ubuntu 24.04). Prior LTS: **Jazzy Jalisco** (May 2024, EOL 2029). **Kilted Kaiju** (May 2025) is a non-LTS release. **Humble** (2022) is LTS until 2027. **Rolling Ridley** is the dev line. Pick an LTS for new robots.
- **Source:** [docs.ros.org](https://docs.ros.org/).

### Hailo-10H (GA Jul 2025)
- First widely-orderable discrete edge AI processor with **native generative-AI support** (**40 TOPS INT4 / 20 TOPS INT8**, on-module DRAM, runs small LLMs/VLMs/Stable Diffusion). Powers the Raspberry Pi AI HAT+ 2.

### Apache TVM graduated to a top-level Apache project
- TVM is now `tvm.apache.org` (latest tagged **v0.22.0**, Oct 2025), built around **TVM Unity** (Relax + TensorIR). It underpins **MLC-LLM** and several vendor compilers (e.g., Axelera Voyager).

---

## Quick "if you read X, know Y" table

| If a guide says… | Today it's… |
|---|---|
| "TensorFlow Lite" / `tflite-runtime` | **LiteRT** / `ai-edge-litert` (`.tflite` unchanged) |
| "buy a Coral USB Accelerator" | **abandoned** — use Hailo instead |
| "Raspberry Pi AI Kit" | **AI HAT+** or **AI HAT+ 2** |
| "Jetson Orin Nano = 40 TOPS" | **67 TOPS** ("Super", JetPack 6.2) |
| "OpenVINO Model Optimizer (`mo`)" | **OVC** / `optimum-intel` |
| "OpenVINO Open Model Zoo" | **Hugging Face + optimum-intel** |
| "ONNX Runtime ArmNN EP" | **removed** (1.26) — use CPU EP (KleidiAI) or QNN |
| "ROS 2 Foxy/Galactic" | EOL — use **Lyrical Luth** or **Jazzy** (LTS) |

*Spot something stale or out of date? Please [open a PR](CONTRIBUTING.md) — keeping this page current is one of the most valuable contributions you can make.*
