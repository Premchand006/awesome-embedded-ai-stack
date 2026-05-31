# Beginner Quick-Wins

Run something real on real hardware **before** going deep on theory. Each project lists exact hardware, difficulty, time, and the learning outcome. We link to **official** tutorials for the steps (so they don't go stale) and add the gotchas that actually trip people up.

## Project table

| Project | Required hardware | Difficulty | Time | Learning outcome | Status |
|---|---|---|---|---|---|
| [**Pi 5 + Hailo live detection**](pi5-hailo-live-detection.md) | RPi 5 + AI HAT+ / HAT+ 2 + camera | 🟢 Easy | 1–2 h | Run an NPU CV pipeline end-to-end | ✅ Detailed |
| [**Jetson YOLO detection**](jetson-yolo-detection.md) | Jetson Orin Nano Super + USB/CSI cam | 🟡 Medium | 2–4 h | TensorRT + DeepStream single-cam detection | ✅ Detailed |
| **RTSP detection pipeline** | Jetson + DeepStream + RTSP source | 🟡 Medium | 3–5 h | Build a GStreamer RTSP→detect→display graph | 🔜 Planned |
| **ONNX Runtime edge YOLO** | Jetson or x86 edge device | 🟡 Medium | 2–3 h | Portable ONNX inference + EP selection | 🔜 Planned |
| **Coral USB classification** ⚠️ | Linux host + Coral USB (legacy) | 🟢 Easy | 1–2 h | TFLite/Edge-TPU basics — *with EOL caveat* | 🔜 Planned |
| **TFLite-Micro keyword spotting** | Arduino Nano 33 BLE / ESP32 | 🟡 Medium | 2–4 h | TinyML on a microcontroller | 🔜 Planned |
| **ROS 2 robot perception** | Jetson or x86+GPU + camera | 🔴 Hard | 4–8 h | Isaac ROS perception in a ROS 2 graph | 🔜 Planned |

> ⚠️ The **Coral** project is included for completeness, but Coral/Edge TPU is **effectively discontinued** — prefer the Pi + Hailo project for new work. ([why](../renames-and-deprecations.md))

## Which one should I do first?
- **On the cheapest budget / total beginner** → [Pi 5 + Hailo live detection](pi5-hailo-live-detection.md).
- **Building toward robotics** → [Jetson YOLO detection](jetson-yolo-detection.md).
- **No accelerator yet, just a laptop** → start with [OpenVINO notebooks](../runtimes-and-sdks/openvino.md) and an ONNX Runtime CPU demo.

## Want to add a project?
Use the template in [CONTRIBUTING.md](../CONTRIBUTING.md#quick-win-template), add a file here, and add a row to the table above. Quick-wins are the **highest-value contributions** to this hub — they prove it's practical, not just a link collection.
