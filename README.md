<!--
  BEFORE YOU PUBLISH:
  1. Badges and links are configured for `Premchand006`.
  2. Replace social-preview image in repo Settings → "Social preview" for nice link unfurls.
  3. Add the GitHub topics listed in awesome-resources/README.md (Settings → Topics).
-->

<div align="center">

# Physical AI & Edge AI Stack

### From sensor → inference → actuation — across Jetson, Raspberry Pi + Hailo, RK3588, OpenVINO, ONNX Runtime, LiteRT, ROS 2, and more.

A cross-vendor, opinionated knowledge hub for **Physical AI, Edge AI, and Embedded AI**: a learning roadmap, a hardware & runtime landscape, reproducible starter projects, and a curated awesome list — kept current, in one place.

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Content: CC BY 4.0](https://img.shields.io/badge/Content-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)
<br/>
[![Link Check](https://img.shields.io/github/actions/workflow/status/Premchand006/awesome-physical-ai/link-check.yml?label=links)](.github/workflows/link-check.yml)
[![Awesome Lint](https://img.shields.io/github/actions/workflow/status/Premchand006/awesome-physical-ai/awesome-lint.yml?label=awesome-lint)](.github/workflows/awesome-lint.yml)
[![Last Commit](https://img.shields.io/github/last-commit/Premchand006/awesome-physical-ai)](https://github.com/Premchand006/awesome-physical-ai/commits/main)
[![Stars](https://img.shields.io/github/stars/Premchand006/awesome-physical-ai?style=social)](https://github.com/Premchand006/awesome-physical-ai/stargazers)

</div>

---

> [!NOTE]
> **The edge-AI landscape moved a lot in 2024–2026.** This repo tracks the changes so you don't have to. TensorFlow Lite is now **LiteRT**; Google **Coral / Edge TPU is effectively discontinued**; the Raspberry Pi **AI Kit was replaced by the AI HAT+ / AI HAT+ 2**; **Jetson AGX Thor** shipped; and the current ROS 2 LTS is **Lyrical Luth**. See [**Renames & Deprecations →**](renames-and-deprecations.md) before you buy hardware or pick a runtime.

## Why this exists

Physical AI and Edge AI knowledge is scattered across vendor docs, blog posts, YouTube, and one-off sample repos — each assuming you've already picked *their* stack. This hub answers the questions that actually block newcomers:

- **Which board should I buy?** → [Hardware Landscape](hardware-landscape/)
- **Which runtime should I use?** → [Runtimes & SDKs](runtimes-and-sdks/)
- **How do I build a camera → inference pipeline?** → [Edge Pipelines](edge-pipelines/)
- **What do I learn, and in what order?** → [Knowledge Roadmap](knowledge-roadmap.md)
- **What can I build *this weekend*?** → [Beginner Quick-Wins](beginner-projects/)

Why care at all? **Edge AI is roughly a USD 25B market in 2025, projected to reach USD 57–165B by 2030–2035** depending on scope, with computer vision the dominant application and manufacturing the fastest-growing vertical ([sources](industry-landscape/)). You're learning an in-demand skill.

---

## 🚀 Start Here

| Step | Do this | Go to |
|------|---------|-------|
| **1. Understand the terms** | Cloud vs Edge vs Embedded vs Physical AI — 10-minute read | [concepts-and-definitions →](concepts-and-definitions/) |
| **2. Pick a path** | Use the decision tree to choose your first board | [getting-started →](getting-started/) |
| **3. Get a quick win** | Run a real camera-detection demo on hardware you can buy today | [beginner-projects →](beginner-projects/) |
| **4. Follow the roadmap** | Beginner → advanced, phase by phase | [knowledge-roadmap →](knowledge-roadmap.md) |
| **5. Go deep** | Explore runtimes, pipelines, robotics, and the market | sections below |

**Three recommended tracks** (full detail in [getting-started](getting-started/)):

- 🟢 **Maker / lowest cost** → Raspberry Pi 5 + AI HAT+ (Hailo). [Quick-win →](beginner-projects/pi5-hailo-live-detection.md)
- 🟡 **Prototyping / robotics** → NVIDIA Jetson Orin Nano Super. [Quick-win →](beginner-projects/jetson-yolo-detection.md)
- 🔴 **Advanced / humanoid & multi-sensor** → Jetson AGX Thor + Isaac ROS. [Robotics →](robotics-and-ros2/)

---

## 🗺️ Visual Roadmap: From Zero to Physical AI

```mermaid
flowchart LR
    A["Phase 0\nLinux + Python/C++\nfoundations"] --> B["Phase 1\nEmbedded basics\n& TinyML"]
    B --> C["Phase 2\nInference runtimes\nONNX RT · LiteRT · TensorRT · OpenVINO"]
    C --> D["Phase 3\nMedia pipelines\nGStreamer · DeepStream"]
    D --> E["Phase 4\nCUDA & HW\nacceleration"]
    E --> F["Phase 5\nROS 2 &\nrobotics inference"]
    F --> G["Phase 6\nEdge deployment\n& optimization"]
    G --> H["Phase 7\nReal-world\nPhysical AI pipelines"]
```

Detailed, link-by-link version: **[knowledge-roadmap.md →](knowledge-roadmap.md)**

---

## 🧭 Hardware at a glance

A starter comparison. Full per-vendor pages, caveats, and buying advice live in **[hardware-landscape/](hardware-landscape/)**. TOPS are vendor maxima at the stated precision — real throughput differs; always check independent FPS/token benchmarks.

| Platform | AI perf (vendor) | Power | On-board RAM | GenAI-capable? | Approx. price | Best for |
|---|---|---|---|---|---|---|
| **RPi 5 + AI HAT+ (Hailo-8L/8)** | 13 / 26 TOPS (INT8) | ~5 W (NPU) | — (uses Pi RAM) | ❌ | $70–110 + Pi | Lowest-cost CV, learning |
| **RPi 5 + AI HAT+ 2 (Hailo-10H)** | 40 TOPS (INT4) | ~2.5 W (NPU) | 8 GB on HAT | ✅ (small LLM/VLM) | ~$130 + Pi | GenAI-at-edge on a budget |
| **Jetson Orin Nano Super** | 67 TOPS (INT8) | 7–25 W | 8 GB shared | ✅ (small) | $249 | Prototyping, robotics entry |
| **Jetson AGX Orin** | up to 275 TOPS (INT8) | 15–60 W | 32/64 GB shared | ✅ | $$$ | Multi-camera, mobile robots |
| **Jetson AGX Thor (T5000)** | up to 2,070 FP4 TFLOPS | 40–130 W | 128 GB | ✅✅ (VLA / LLM) | $3,499 (dev kit) | Humanoids, multi-sensor fusion |
| **RK3588 boards** | 6 TOPS (INT8) NPU | ~5–10 W | board-dependent | ⚠️ (small via rkllm) | $80–200 | Cheap Linux SBC + NPU |
| **Intel Core Ultra + OpenVINO** | NPU + iGPU (varies) | laptop/edge | system RAM | ✅ | varies | x86 edge servers, GenAI + CV |
| **AMD Ryzen AI (XDNA 2)** | up to 50–60 TOPS (NPU) | laptop/embedded | system RAM | ✅ | varies | AI PCs, industrial/automotive |
| **Hailo-10H (discrete M.2)** | 40 TOPS INT4 / 20 INT8 | ~2.5 W | 4/8 GB on-module | ✅ | module | Add GenAI to an x86/ARM host |
| **Axelera Metis (M.2/PCIe)** | up to 214 / 856 TOPS | M.2/card | on-card | ⚠️ | card | High-FPS multi-stream CV |
| **Google Coral / Edge TPU** | 4 TOPS (INT8) | ~2 W | — | ❌ | ⚠️ EOL | *Legacy only — see deprecations* |

> ⚠️ **Coral / Edge TPU is effectively abandoned** (kernel driver removed from staging, no stock). Use Hailo as the practical successor. Details: [renames-and-deprecations.md](renames-and-deprecations.md).

---

## ⚙️ Which runtime should I use?

Full matrix and per-runtime pages in **[runtimes-and-sdks/](runtimes-and-sdks/)**.

| If your target is… | Reach for | Notes |
|---|---|---|
| NVIDIA GPU / Jetson | **TensorRT** + (video) **DeepStream** | DeepStream is built on GStreamer |
| Intel CPU / iGPU / NPU / Arc | **OpenVINO** (+ OpenVINO GenAI) | Model Optimizer & Open Model Zoo are deprecated → use OVC + optimum-intel |
| Qualcomm Snapdragon (Hexagon NPU) | **Qualcomm AI Hub** → LiteRT / ONNX RT / QNN | 150+ pre-optimized models |
| Microcontrollers (Arduino, ESP32, Cortex-M) | **LiteRT for Microcontrollers** (`tflite-micro`) | kilobytes–megabytes of RAM |
| Phones / mixed on-device | **LiteRT** (was *TensorFlow Lite*) | `.tflite` format unchanged |
| "Run my ONNX model anywhere" | **ONNX Runtime** (pick an Execution Provider) | CUDA, TensorRT, OpenVINO, QNN, DirectML, CoreML, WebGPU… |
| Rockchip RK3588 NPU | **RKNN-Toolkit2** / **rkllm** | convert from ONNX/PyTorch |

---

## 📚 Repository structure

```text
awesome-physical-ai/
├── getting-started/            # Day 0 → Day 7: choose a board, set it up
├── concepts-and-definitions/   # Cloud vs Edge vs Embedded; Physical AI; latency
├── hardware-landscape/         # Jetson, Pi+Hailo, RK3588, OpenVINO, AMD, discrete NPUs
├── runtimes-and-sdks/          # ONNX Runtime, LiteRT, TensorRT/DeepStream, OpenVINO, TVM
├── edge-pipelines/             # camera → preproc → inference → postproc patterns
├── robotics-and-ros2/          # ROS 2 (Lyrical/Jazzy), Isaac ROS, the "3-computer" story
├── beginner-projects/          # reproducible quick-wins with a buy-list per project
├── deployment-and-optimization/# export, quantization, profiling, cloud→edge
├── industry-landscape/         # market size, vendor map, applications by vertical
├── awesome-resources/          # the curated "awesome list" core (docs, repos, videos, papers)
├── diagrams/                   # architecture & roadmap diagrams
├── knowledge-roadmap.md        # beginner → advanced learning path
├── renames-and-deprecations.md # what changed in 2024–2026 (read this!)
└── CONTRIBUTING.md             # how to add resources / projects (with quality bar)
```

### Explore by section

- 🏁 **[Getting Started](getting-started/)** — pick your first board with a decision tree.
- 🧩 **[Concepts & Definitions](concepts-and-definitions/)** — the vocabulary, done right.
- 🔌 **[Hardware Landscape](hardware-landscape/)** — every major platform, with caveats.
- ⚙️ **[Runtimes & SDKs](runtimes-and-sdks/)** — ONNX Runtime, LiteRT, TensorRT, OpenVINO, TVM.
- 🎥 **[Edge Pipelines](edge-pipelines/)** — GStreamer, DeepStream, ROS 2 perception.
- 🤖 **[Robotics & ROS 2](robotics-and-ros2/)** — Isaac ROS, NITROS, Physical AI framing.
- 🛠️ **[Beginner Projects](beginner-projects/)** — weekend quick-wins on real hardware.
- 🚢 **[Deployment & Optimization](deployment-and-optimization/)** — quantize, profile, ship.
- 📈 **[Industry Landscape](industry-landscape/)** — market data and where it's heading.
- ⭐ **[Awesome Resources](awesome-resources/)** — the curated link collection.

---

## 🤝 Contributing

This hub is only as good as the community keeps it. **Good first contributions:** add a new quick-win project, fix a broken link, add a board page, or correct a stale spec. The quality bar and step-by-step process are in **[CONTRIBUTING.md](CONTRIBUTING.md)**, and CI will run `awesome-lint` + a link checker on your PR.

Look for [`good first issue`](https://github.com/Premchand006/awesome-physical-ai/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22) and [`help wanted`](https://github.com/Premchand006/awesome-physical-ai/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22).

## 📄 License

Code/snippets: **MIT**. Curated prose, tables, and learning materials: **CC BY 4.0**. See [LICENSE](LICENSE).

## 🙏 Acknowledgements

Structure inspired by the broader [Awesome](https://awesome.re) movement and community knowledge hubs across the Jetson, OpenVINO, Hailo, ROS, and RK3588 ecosystems. All product names and trademarks belong to their respective owners; this is an independent, vendor-neutral resource.
