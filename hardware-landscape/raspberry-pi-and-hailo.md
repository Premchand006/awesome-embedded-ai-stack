# Raspberry Pi + Hailo

The cheapest credible path into real edge AI. A **Raspberry Pi 5** plus a **Hailo** accelerator gives you hardware-accelerated computer vision (and, with the newest HAT, on-device generative AI) for a fraction of a Jetson's cost — with the biggest beginner community anywhere.

- **Docs:** [Raspberry Pi AI](https://www.raspberrypi.com/documentation/computers/ai.html)
- **Examples:** [hailo-ai/hailo-rpi5-examples](https://github.com/hailo-ai/hailo-rpi5-examples) · [hailo-ai/hailo-apps-infra](https://github.com/hailo-ai/hailo-apps-infra)

## The accelerator options (2026)

| Product | NPU | AI perf | On-board RAM | GenAI | Price | Status |
|---|---|---|---|---|---|---|
| ~~AI Kit~~ | Hailo-8L | 13 TOPS | — | ❌ | — | **Discontinued** |
| **AI HAT+ (13 TOPS)** | Hailo-8L | 13 TOPS (INT8) | — | ❌ | ~$70 | Current |
| **AI HAT+ (26 TOPS)** | Hailo-8 | 26 TOPS (INT8) | — | ❌ | ~$110 | Current |
| **AI HAT+ 2** | Hailo-10H | 40 TOPS (INT4) | **8 GB** | ✅ | ~$130 | Current, newest |

> ⚠️ The original **AI Kit is discontinued** — buy an **AI HAT+** (M.2 HAT form) or the new **AI HAT+ 2**. ([deprecations](../renames-and-deprecations.md))

### AI HAT+ 2 — GenAI on a Pi
The standout 2026 option: the **Hailo-10H** with **8 GB of on-board RAM** lets a Raspberry Pi 5 run small **LLMs, VLMs, and image-generation** models locally, in addition to fast detection/segmentation. Production is guaranteed into 2036. Integrated into `libcamera`/`rpicam-apps`/`Picamera2`.

## What you need to start
- **Raspberry Pi 5** (8 GB recommended) + official 27 W USB-C PSU + active cooler.
- **AI HAT+** or **AI HAT+ 2** (includes the M.2 HAT and standoffs).
- **Camera Module 3** (CSI) or a USB webcam.
- A microSD card (or NVMe via a separate HAT).

## Software stack
- **HailoRT** — runtime + drivers (`hailortcli` to probe the device).
- **Hailo Model Zoo** — pre-compiled models (`.hef`) for detection, pose, segmentation, depth.
- **TAPPAS / hailo-apps-infra** — GStreamer-based reference pipelines.
- **Hailo Dataflow Compiler** — compile your own models to `.hef` (for custom models).

On Raspberry Pi OS the integration is largely turnkey: `sudo apt install hailo-all`, reboot, and run the example pipelines.

## Strengths & trade-offs
- ✅ Lowest cost; massive community and documentation.
- ✅ Very low power (~2.5 W for the NPU).
- ✅ AI HAT+ 2 brings genuine on-device GenAI to a hobbyist budget.
- ⚠️ Hailo-8/8L have **no on-chip DRAM** (weights stream from host) — great for CV, not for LLMs (that's what the 10H/HAT+ 2 fixes).
- ⚠️ Custom (non-zoo) models require compiling with the Dataflow Compiler — a learning curve.

➡️ First project: [Pi 5 + Hailo live detection](../beginner-projects/pi5-hailo-live-detection.md).
