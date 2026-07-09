# Awesome Physical AI & Edge AI Resources [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated, vendor-neutral list of high-quality resources for Physical AI, Edge AI, and Embedded AI — official docs, SDKs, learning material, example repos, and research.

Only currently-maintained, authoritative, or high-signal resources are listed. Stale links get pruned. See the [contribution guide](../CONTRIBUTING.md) for the quality bar.

## Contents
- [Official docs & SDKs](#official-docs--sdks)
- [Hardware vendors](#hardware-vendors)
- [Example repos & demos](#example-repos--demos)
- [Learning: video & courses](#learning-video--courses)
- [Research & landscape](#research--landscape)
- [Other awesome lists](#other-awesome-lists)
- [Suggested GitHub topics](#suggested-github-topics)

## Official docs & SDKs
- [ONNX Runtime](https://onnxruntime.ai) - Portable inference across CPU/GPU/NPU via Execution Providers.
- [LiteRT (Google AI Edge)](https://ai.google.dev/edge/litert) - On-device runtime; successor to TensorFlow Lite.
- [LiteRT for Microcontrollers (tflite-micro)](https://github.com/tensorflow/tflite-micro) - TinyML on MCUs/DSPs.
- [NVIDIA TensorRT](https://docs.nvidia.com/deeplearning/tensorrt) - Max-throughput inference on NVIDIA GPUs/Jetson.
- [NVIDIA DeepStream](https://developer.nvidia.com/deepstream-sdk) - GStreamer-based multi-stream video analytics.
- [NVIDIA Isaac ROS](https://developer.nvidia.com/isaac/ros) - GPU-accelerated ROS 2 perception GEMs.
- [NVIDIA Holoscan SDK](https://developer.nvidia.com/holoscan-sdk) - Low-latency real-time sensor AI.
- [Intel OpenVINO docs](https://docs.openvino.ai) - Inference on Intel CPU/iGPU/NPU/Arc, plus OpenVINO GenAI.
- [Qualcomm AI Hub](https://aihub.qualcomm.com) - Compile/benchmark/deploy 150+ models to Snapdragon.
- [AMD Ryzen AI Software](https://www.amd.com/en/developer/resources/ryzen-ai-software.html) - ONNX-based NPU flow for XDNA.
- [Apache TVM](https://tvm.apache.org) - ML compiler stack (TVM Unity: Relax + TensorIR).
- [ROS 2 documentation](https://docs.ros.org) - Robotics middleware; pick an LTS distro.
- [GStreamer](https://gstreamer.freedesktop.org) - The multimedia-pipeline framework behind most edge video AI.
- [OpenCV](https://opencv.org) - Classic computer-vision library with an actively reworked DNN module.

## Hardware vendors
- [NVIDIA Jetson modules](https://developer.nvidia.com/embedded/jetson-modules) - Orin Nano Super → AGX Orin → AGX Thor.
- [Raspberry Pi AI documentation](https://www.raspberrypi.com/documentation/computers/ai.html) - AI HAT+ / AI HAT+ 2 (Hailo).
- [Hailo](https://hailo.ai) - Hailo-8/8L/10H edge AI processors; HailoRT, TAPPAS, Model Zoo.
- [Rockchip RKNN-Toolkit2](https://github.com/airockchip/rknn-toolkit2) - Toolchain for the RK3588 NPU.
- [Axelera AI](https://axelera.ai) - Metis AIPU and the Voyager SDK.
- [SiMa.ai MLSoC](https://sima.ai/mlsoc) - Multimodal MLSoC/Modalix and the Palette SDK.
- [MemryX](https://memryx.com) - MX3 accelerator with an open-source SDK.
- [Kneron](https://www.kneron.com) - Ultra-low-power KL-series NPUs; Kneron PLUS SDK.

## Example repos & demos
- [hailo-ai/hailo-rpi5-examples](https://github.com/hailo-ai/hailo-rpi5-examples) - Raspberry Pi 5 + Hailo detection/pose/segmentation.
- [hailo-ai/hailo-apps-infra](https://github.com/hailo-ai/hailo-apps-infra) - Reusable Hailo GStreamer pipeline infrastructure.
- [microsoft/onnxruntime-inference-examples](https://github.com/microsoft/onnxruntime-inference-examples) - ONNX Runtime samples incl. IoT/edge.
- [openvinotoolkit/openvino_notebooks](https://github.com/openvinotoolkit/openvino_notebooks) - Runnable OpenVINO Jupyter tutorials.
- [NVIDIA-ISAAC-ROS/isaac_ros_dnn_inference](https://github.com/NVIDIA-ISAAC-ROS/isaac_ros_dnn_inference) - Accelerated DNN inference in ROS 2.
- [airockchip/rknn_model_zoo](https://github.com/airockchip/rknn_model_zoo) - RK3588 NPU model examples (YOLO, Whisper, CLIP).
- [airockchip/rknn-llm](https://github.com/airockchip/rknn-llm) - Run small LLMs on the RK3588 NPU.
- [nvidia-holoscan/holohub](https://github.com/nvidia-holoscan/holohub) - Holoscan reference applications.

## Learning: video & courses
- [JetsonHacks (YouTube)](https://www.youtube.com/@JetsonHacks) - Practical Jetson tutorials and JetPack walkthroughs.
- [NVIDIA Developer (YouTube)](https://www.youtube.com/@NVIDIADeveloper) - TensorRT, DeepStream, Isaac, Holoscan sessions.
- [Edge Impulse (YouTube)](https://www.youtube.com/@EdgeImpulse) - TinyML and embedded ML from data to deployment.
- [NVIDIA Jetson AI Lab](https://www.jetson-ai-lab.com) - Hands-on generative-AI-on-Jetson tutorials.

## Research & landscape
- [NVIDIA Cosmos](https://www.nvidia.com/en-us/ai/cosmos) - World foundation models for Physical AI (Predict/Transfer/Reason).
- [Cosmos World Foundation Model Platform (arXiv:2501.03575)](https://arxiv.org/abs/2501.03575) - The platform paper.
- [Hailo Model Zoo](https://github.com/hailo-ai/hailo_model_zoo) - Pre-compiled edge models and benchmarks.

## Other awesome lists
- [sindresorhus/awesome](https://github.com/sindresorhus/awesome) - The index of awesome lists and the quality manifesto.
- [choushunn/awesome-RK3588](https://github.com/choushunn/awesome-RK3588) - Actively maintained RK3588 resource list.
- [rcmalli/awesome-edge-ai](https://github.com/rcmalli/awesome-edge-ai) - Edge-AI tools (verify currency; some entries are dated).
- [tobymcclean/awesome-edge-ai](https://github.com/tobymcclean/awesome-edge-ai) - Edge-AI references (verify currency).

*Found a great resource — or a dead link? [Open a PR](../CONTRIBUTING.md). Curation only stays useful if it stays current.*
