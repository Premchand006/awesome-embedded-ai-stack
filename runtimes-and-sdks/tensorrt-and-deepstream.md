# TensorRT & DeepStream

NVIDIA's path to maximum on-device throughput. **TensorRT** optimizes and quantizes a model for a specific GPU; **DeepStream** wraps inference in a high-performance, multi-stream **video analytics** pipeline.

## TensorRT
- **Docs:** [docs.nvidia.com/deeplearning/tensorrt](https://docs.nvidia.com/deeplearning/tensorrt/) · [Developer page](https://developer.nvidia.com/tensorrt)
- **Version:** **TensorRT 10.x** is current; **TensorRT 11.0** is coming (strongly-typed networks by default, explicit quantization, IPluginV3, multi-device inference GA).

What it does: takes an ONNX (or framework) model and builds an optimized **engine** for your exact GPU — layer/tensor fusion, kernel auto-tuning, and **precision calibration** (FP16/INT8/FP8/FP4). The result is often several times faster than a generic runtime on the same card.

Typical flow:
```
PyTorch → ONNX → trtexec (or the TensorRT API) → optimized .engine → deploy
```
For quantization (PTQ/QAT), use the **TensorRT Model Optimizer** ([optimization](../deployment-and-optimization/)).

## DeepStream
- **Docs:** [NVIDIA DeepStream](https://developer.nvidia.com/deepstream-sdk)
- **Version:** **DeepStream 7.x** (runs on JetPack 7 for Thor; JetPack 6 for Orin).

DeepStream is **"an optimized graph architecture built using the open-source GStreamer framework."** It gives you batteries-included plugins for real-time video AI:

| Plugin | Role |
|---|---|
| `Gst-nvstreammux` | batch multiple camera/RTSP streams |
| `Gst-nvinfer` | run TensorRT inference (detector/classifier) |
| `Gst-nvtracker` | multi-object tracking across frames |
| `Gst-nvdsosd` | draw boxes/labels for display |

Results flow as structured metadata (`NvDsBatchMeta`) you can read in C/C++ or Python. Because it's GStreamer underneath, the [GStreamer concepts](../edge-pipelines/gstreamer-and-deepstream.md) transfer directly.

## When to use which
- **Just need a fast model on a Jetson/GPU?** TensorRT alone.
- **Need to ingest cameras/RTSP, detect + track + display, possibly many streams?** DeepStream (which uses TensorRT for the inference step).

➡️ Build it: [RTSP / DeepStream pipeline](../edge-pipelines/gstreamer-and-deepstream.md) and the [Jetson YOLO quick-win](../beginner-projects/jetson-yolo-detection.md).
