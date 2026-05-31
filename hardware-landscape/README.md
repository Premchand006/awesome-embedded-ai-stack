# Hardware Landscape

Every major Physical/Edge AI platform, with the specs that matter and the trade-offs vendors don't put on the box. **All figures verified around May 2026** — TOPS, prices, and SDK versions change, so check the linked official page before buying.

> **Reading TOPS honestly:** a "TOPS" number is a theoretical peak at a specific precision (often INT8, sometimes INT4/FP4). Two chips with the same TOPS can deliver very different real-world FPS depending on memory bandwidth, on-chip SRAM, the model, and the toolchain. Treat TOPS as a rough class indicator, not a benchmark. Where independent FPS/token numbers exist, we cite them on the per-vendor page.

## Master comparison

| Platform | AI perf (vendor) | Precision | Power | On-board RAM | GenAI? | Price (approx.) | Software |
|---|---|---|---|---|---|---|---|
| **RPi 5 + AI HAT+ (Hailo-8L)** | 13 TOPS | INT8 | ~5 W | uses Pi RAM | ❌ | ~$70 + Pi | HailoRT, rpicam |
| **RPi 5 + AI HAT+ (Hailo-8)** | 26 TOPS | INT8 | ~5 W | uses Pi RAM | ❌ | ~$110 + Pi | HailoRT, rpicam |
| **RPi 5 + AI HAT+ 2 (Hailo-10H)** | 40 TOPS | INT4 | ~2.5 W | 8 GB on HAT | ✅ | ~$130 + Pi | HailoRT, rpicam |
| **Jetson Orin Nano Super** | 67 TOPS | INT8 | 7–25 W | 8 GB shared | ✅ small | $249 | JetPack 6.2 |
| **Jetson Orin NX** | 100 / 157 TOPS | INT8 | 10–25 W | 8 / 16 GB | ✅ | $$ | JetPack 6 |
| **Jetson AGX Orin** | up to 275 TOPS | INT8 | 15–60 W | 32 / 64 GB | ✅ | $$$ | JetPack 6 |
| **Jetson AGX Thor (T5000)** | up to 2,070 TFLOPS | FP4 | 40–130 W | 128 GB | ✅✅ | $3,499 devkit | JetPack 7 |
| **Jetson T4000 (module)** | ~1,200 TFLOPS | FP4 | lower | 64 GB | ✅✅ | module | JetPack 7 |
| **RK3588 SBC** | 6 TOPS | INT8 | ~5–10 W | board-dependent | ⚠️ via rkllm | $80–200 | RKNN-Toolkit2, rkllm |
| **Intel Core Ultra (+OpenVINO)** | NPU + iGPU (varies) | INT8/FP16 | laptop/edge | system | ✅ | varies | OpenVINO |
| **AMD Ryzen AI 300/400 (XDNA 2)** | 50–60 TOPS (NPU) | INT8 | laptop/embedded | system | ✅ | varies | Ryzen AI SW, ROCm |
| **Hailo-8 / 8L (discrete M.2)** | 26 / 13 TOPS | INT8 | ~2.5 W | none | ❌ | module | HailoRT, TAPPAS |
| **Hailo-10H (discrete M.2)** | 40 / 20 TOPS | INT4 / INT8 | ~2.5 W | 4/8 GB on-module | ✅ | module | HailoRT |
| **Axelera Metis (M.2 / PCIe)** | 214 / 856 TOPS | INT8 | card | on-card | ⚠️ | card | Voyager SDK (TVM+GStreamer) |
| **SiMa.ai MLSoC / Modalix** | 50–200 TOPS | mixed | low | on-chip | ✅ | module | Palette SDK |
| **MemryX MX3 (M.2)** | — (dataflow) | INT8/BF16 | low | ~40 MB on-chip | ⚠️ | module | open-source SDK |
| **Kneron KL730** | 3.6 / 7.2 eTOPS | INT8 / INT4 | low | — | ⚠️ small | SoC/dongle | Kneron PLUS |
| **Google Coral / Edge TPU** | 4 TOPS | INT8 | ~2 W | — | ❌ | ⚠️ **EOL** | *legacy* |

## Per-platform deep dives

- [**Jetson family**](jetson.md) — Orin Nano Super → AGX Orin → AGX Thor; JetPack; the reference robotics stack.
- [**Raspberry Pi + Hailo**](raspberry-pi-and-hailo.md) — the cheapest credible NPU path (AI HAT+ / AI HAT+ 2).
- [**Rockchip RK3588**](rk3588.md) — low-cost Linux SBC with a 6-TOPS NPU; RKNN + rkllm.
- [**Intel OpenVINO & AMD Ryzen AI**](intel-and-amd.md) — use the x86 silicon you already own.
- [**Discrete NPUs**](discrete-npus.md) — Hailo, Axelera, SiMa.ai, MemryX, Kneron, and the Coral status.

## How to choose (quick heuristics)

- **Cheapest way to learn CV:** Raspberry Pi 5 + AI HAT+.
- **Want on-device LLM/VLM on a budget:** Pi 5 + AI HAT+ 2 (Hailo-10H) or RK3588 + rkllm.
- **Robotics / ROS 2 / multi-camera:** Jetson (Orin Nano Super to start; AGX Orin/Thor to scale).
- **You have an x86 laptop/server:** start free with OpenVINO (Intel) or Ryzen AI (AMD) — no new hardware.
- **Battery sensor, always-on:** MCU + LiteRT for Microcontrollers.

Then pick a runtime in [runtimes-and-sdks](../runtimes-and-sdks/).
