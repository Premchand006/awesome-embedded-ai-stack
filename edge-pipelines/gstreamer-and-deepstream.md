# GStreamer & DeepStream

GStreamer is the open-source multimedia framework that underpins most edge-AI **video** pipelines. DeepStream (NVIDIA), DL Streamer (Intel), and Hailo TAPPAS are all built on it — so the concepts here transfer everywhere.

- **GStreamer:** [gstreamer.freedesktop.org](https://gstreamer.freedesktop.org/)
- **DeepStream:** [developer.nvidia.com/deepstream-sdk](https://developer.nvidia.com/deepstream-sdk)
- **Example repo:** [alexander-pv/inference-gstreamer](https://github.com/alexander-pv/inference-gstreamer)

## GStreamer in five terms
- **Element** — a processing block (a source, a decoder, an inference plugin, a sink).
- **Pad** — an element's input/output connector.
- **Caps** — the data format negotiated on a pad (e.g., `video/x-raw, format=NV12, width=1920`).
- **Pipeline** — elements linked together; data ("buffers") flows source → sink.
- **Bin** — a container grouping elements.

A first pipeline you can run on almost any Linux box with a webcam:
```bash
gst-launch-1.0 v4l2src device=/dev/video0 ! videoconvert ! autovideosink
```
That's source → format-convert → display. Add elements between them to do real work (decode RTSP, run a model, draw results).

## DeepStream = GStreamer + NVIDIA AI plugins
DeepStream is **"an optimized graph architecture built using the open-source GStreamer framework"** with batteries-included AI elements:

| Plugin | Role |
|---|---|
| `Gst-nvstreammux` | batch multiple input streams into one |
| `Gst-nvinfer` | TensorRT inference (primary detector / secondary classifiers) |
| `Gst-nvtracker` | multi-object tracking across frames |
| `Gst-nvdsosd` | on-screen display (boxes, labels) |

Inference results travel as structured metadata (**`NvDsBatchMeta`**) you read in C/C++ or Python — that's how you turn "boxes on a screen" into "events your app acts on" (counts, alerts, MQTT messages).

### Conceptual RTSP detection pipeline (DeepStream)
```
rtspsrc → depay/parse → nvv4l2decoder → nvstreammux → nvinfer (TensorRT model)
       → nvtracker → nvdsosd → (display | encode | metadata out)
```
This single graph can scale from one camera to many by feeding more sources into `nvstreammux`. Build it in the [Jetson YOLO quick-win](../beginner-projects/jetson-yolo-detection.md).

## On non-NVIDIA hardware
- **Intel:** DL Streamer provides analogous GStreamer elements backed by OpenVINO.
- **Hailo:** TAPPAS / `hailo-apps-infra` provide GStreamer elements backed by HailoRT — the basis of the [Pi 5 + Hailo project](../beginner-projects/pi5-hailo-live-detection.md).

## Debugging tips that save hours
- `GST_DEBUG=3 gst-launch-1.0 ...` to see negotiation errors.
- Caps mismatches are the #1 problem — print pad caps and insert `videoconvert`/`nvvidconv` where formats differ.
- Test each stage incrementally (source → sink first, then add inference).
