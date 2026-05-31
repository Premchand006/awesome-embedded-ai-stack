# Quick-Win: Raspberry Pi 5 + Hailo Live Object Detection

**What you'll build:** a live camera window with real-time object-detection boxes, running on a Raspberry Pi 5 with a Hailo NPU — the cheapest credible "real edge AI" demo.

| | |
|---|---|
| **Difficulty** | 🟢 Easy |
| **Time** | 1–2 hours (most of it OS setup) |
| **Setup complexity** | Low–medium (mostly `apt` + a clone) |
| **Cost** | ~$140–200 total |

## Required hardware
- **Raspberry Pi 5** (8 GB recommended)
- **AI HAT+** (13/26 TOPS, Hailo-8L/8) **or AI HAT+ 2** (40 TOPS, Hailo-10H, +GenAI) — includes the M.2 HAT
- **Raspberry Pi Camera Module 3** (CSI) **or** a USB webcam
- Official **27 W USB-C** PSU, an **active cooler**, and a microSD card (32 GB+)

## Steps (follow the official guides; key commands below)
1. **Assemble:** mount the AI HAT+ on the Pi 5 via the M.2 connector (use the supplied standoffs/ribbon). Connect the camera to a CSI port.
2. **Flash Raspberry Pi OS (64-bit, Bookworm)** with Raspberry Pi Imager; boot and update:
   ```bash
   sudo apt update && sudo apt full-upgrade -y
   sudo reboot
   ```
3. **Install the Hailo stack** (turnkey on Pi OS):
   ```bash
   sudo apt install hailo-all -y
   sudo reboot
   ```
4. **Verify the NPU is detected:**
   ```bash
   hailortcli fw-control identify
   ```
   You should see your Hailo device and firmware version.
5. **Clone and run the examples:**
   ```bash
   git clone https://github.com/hailo-ai/hailo-rpi5-examples.git
   cd hailo-rpi5-examples
   ./install.sh
   source setup_env.sh
   python basic_pipelines/detection.py --input rpi   # or: --input /dev/video0 for USB
   ```
   A window opens with live detection boxes. 🎉

- **Official references:** [Raspberry Pi AI docs](https://www.raspberrypi.com/documentation/computers/ai.html) · [hailo-rpi5-examples](https://github.com/hailo-ai/hailo-rpi5-examples)

## What you just learned
- An NPU accelerates inference while the Pi's CPU handles the rest.
- The demo is a **GStreamer pipeline** (camera → preprocess → Hailo inference → draw → display) — exactly the [canonical edge pipeline](../edge-pipelines/).
- Models run as pre-compiled **`.hef`** files from the Hailo Model Zoo.

## Go further
- Swap models (pose, segmentation, depth) from the Hailo Model Zoo.
- On **AI HAT+ 2 (Hailo-10H)**, try a small **on-device LLM/VLM** — the 8 GB on-board RAM makes GenAI feasible. ([hardware](../hardware-landscape/raspberry-pi-and-hailo.md))
- Compile a **custom** model with the Hailo Dataflow Compiler.

## Troubleshooting
- **NPU not found** → ensure `hailo-all` installed and you rebooted; reseat the M.2/ribbon; check the HAT is enabled in `raspi-config`.
- **Camera not detected** → `libcamera-hello` / `rpicam-hello` to test the CSI camera; for USB use `--input /dev/video0`.
- **Low FPS** → confirm you're on the Hailo path (not CPU); use the active cooler (thermal throttling kills FPS).
