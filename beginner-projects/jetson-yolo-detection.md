# Quick-Win: Jetson Camera Object Detection (YOLO + TensorRT/DeepStream)

**What you'll build:** real-time object detection from a USB/CSI camera on an NVIDIA Jetson, accelerated by **TensorRT**, with an optional **DeepStream** multi-stream version — your first step toward robotics and video analytics.

| | |
|---|---|
| **Difficulty** | 🟡 Medium |
| **Time** | 2–4 hours |
| **Setup complexity** | Medium (JetPack + SDK/cloning) |
| **Cost** | from $249 (Orin Nano Super dev kit) + camera |

## Required hardware
- **Jetson Orin Nano Super Developer Kit** ($249) — or any Orin-class Jetson
- **USB webcam** or a compatible **CSI camera**
- Quality power supply + active cooling + NVMe/microSD per the kit instructions

## Path A — fastest: Ultralytics YOLO + TensorRT
Good for learning. Ultralytics auto-exports to a TensorRT engine for the Jetson's GPU.
1. **Flash JetPack 6.2** with NVIDIA SDK Manager (this also unlocks the Orin Nano "Super" 67-TOPS profile). [Getting started](https://developer.nvidia.com/embedded/learn/get-started-jetson-orin-nano-devkit).
2. **Install Ultralytics** (use a venv):
   ```bash
   python3 -m venv yolo && source yolo/bin/activate
   pip install ultralytics
   ```
3. **Run detection on your camera** (downloads a pretrained model on first run):
   ```bash
   yolo detect predict model=yolo11n.pt source=0 show=True   # source=0 = first camera
   ```
4. **Export to TensorRT for speed**, then run the engine:
   ```bash
   yolo export model=yolo11n.pt format=engine        # builds a .engine for THIS Jetson
   yolo detect predict model=yolo11n.engine source=0 show=True
   ```
   - **Why faster:** TensorRT fuses layers and uses FP16/INT8 tuned for your exact GPU. See [TensorRT](../runtimes-and-sdks/tensorrt-and-deepstream.md).

## Path B — production-style: DeepStream
Better for multi-stream/RTSP and structured event output.
1. Install the **DeepStream SDK** for your JetPack ([DeepStream](https://developer.nvidia.com/deepstream-sdk)).
2. Run a reference app or sample config (single USB/CSI camera → `nvinfer` detector → `nvdsosd` → display).
3. Read detections from **`NvDsBatchMeta`** to turn boxes into events (counts, alerts). Pipeline concepts: [GStreamer & DeepStream](../edge-pipelines/gstreamer-and-deepstream.md).

## What you just learned
- The **export path**: PyTorch → ONNX/engine → optimized TensorRT inference.
- Why an "engine" is **device-specific** (built for your GPU).
- The difference between a quick script (Path A) and a **scalable pipeline** (Path B).

## Go further
- Build the [RTSP detection pipeline](README.md) (multi-camera).
- Move perception into a robot with **[Isaac ROS](../robotics-and-ros2/)**.
- Try **INT8 quantization** for more FPS ([optimization](../deployment-and-optimization/)).

## Troubleshooting
- **Engine build is slow / OOM** → it's normal the first time; close other apps; the Orin Nano shares CPU/GPU memory, so use a small model (`yolo11n`).
- **No camera** → `ls /dev/video*` and try `source=1`; for CSI cameras follow the kit's CSI instructions.
- **Old tutorial says 40 TOPS / JetPack 5** → use **JetPack 6.2** for the Super profile. ([why](../renames-and-deprecations.md))
- **Low FPS** → confirm you're running the `.engine` (not the `.pt`) and that cooling is active.
