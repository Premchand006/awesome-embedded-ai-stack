# NVIDIA Jetson

The most complete edge-AI/robotics platform: a single software stack (**JetPack**) spanning CUDA, **TensorRT**, **DeepStream**, and **Isaac ROS**, from a $249 dev kit up to a humanoid-class supercomputer. If you want one ecosystem to learn deeply, this is it.

- **Docs:** [Jetson developer site](https://developer.nvidia.com/embedded/jetson-modules) · [Jetson AI Lab](https://www.jetson-ai-lab.com/)
- **Community projects:** [Jetson Projects gallery](https://developer.nvidia.com/embedded/community/jetson-projects)

## The current lineup

| Module / kit | AI perf | Memory | Power | JetPack | Notes |
|---|---|---|---|---|---|
| **Orin Nano Super (dev kit)** | 67 TOPS (INT8) | 8 GB | 7–25 W | 6.2 | $249; a *software* unlock of the old 40-TOPS Nano |
| **Orin NX** | 100 / 157 TOPS | 8 / 16 GB | 10–25 W | 6 | Great robotics workhorse |
| **AGX Orin** | up to 275 TOPS | 32 / 64 GB | 15–60 W | 6 | Multi-camera analytics, mobile robots |
| **AGX Thor (T5000)** | up to 2,070 FP4 TFLOPS | 128 GB | 40–130 W | 7 | Flagship Physical-AI "runtime computer" |
| **T4000 (module)** | ~1,200 FP4 TFLOPS | 64 GB | lower | 7 | Announced CES 2026 |

> **"Super" matters:** JetPack 6.2 unlocked the Orin Nano to **67 TOPS** at $249. Earlier JetPack runs it at 40 TOPS. If a tutorial says 40, it predates the Super profile.

## Jetson AGX Thor — the Physical AI flagship
- **Up to 2,070 FP4 TFLOPS**, **128 GB**, **40–130 W** configurable, Blackwell GPU, 14-core Arm Neoverse-V3AE, Multi-Instance GPU. NVIDIA cites **>7.5× the AI compute and ~3.5× the energy efficiency of AGX Orin**.
- **Developer Kit: $3,499.** Runs **JetPack 7** (Jetson Linux 38.x, Ubuntu 24.04, kernel 6.8). **JetPack 7.1** is the current production release.
- **For:** humanoids, autonomous mobile robots, and multi-sensor fusion that needs VLA/LLM-class compute on-device.
- [Product page](https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/jetson-thor/) · [Announcement blog](https://developer.nvidia.com/blog/introducing-nvidia-jetson-thor-the-ultimate-platform-for-physical-ai/)

## JetPack & software
**JetPack** bundles Jetson Linux (L4T), CUDA, cuDNN, TensorRT, and multimedia/DeepStream support.
- **JetPack 6.x** — for the **Orin** family (Ubuntu 22.04). JetPack 6.2 enables the Orin Nano "Super" profile.
- **JetPack 7.x** — for **Thor** (Ubuntu 24.04, kernel 6.8). Orin support on JetPack 7 is planned for 7.2.

What you'll actually use on a Jetson:
- **[TensorRT](../runtimes-and-sdks/tensorrt-and-deepstream.md)** — optimize/quantize models for max throughput.
- **[DeepStream](../edge-pipelines/gstreamer-and-deepstream.md)** — multi-stream video analytics (built on GStreamer).
- **[Isaac ROS](../robotics-and-ros2/)** — GPU-accelerated ROS 2 perception (Visual SLAM, NVBlox, DNN inference) via **NITROS**.
- **[Holoscan](../robotics-and-ros2/)** — low-latency multi-sensor real-time AI.

## Strengths & trade-offs
- ✅ Best-in-class software maturity; one stack from prototype to humanoid.
- ✅ Huge community, tutorials (JetsonHacks), and the Jetson AI Lab.
- ⚠️ Higher cost and power than NPU-only options (Pi+Hailo, RK3588).
- ⚠️ Memory is **shared** CPU/GPU — watch your budget on large models.

➡️ First project: [Jetson YOLO detection](../beginner-projects/jetson-yolo-detection.md).
