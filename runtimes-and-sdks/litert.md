# LiteRT (formerly TensorFlow Lite) & LiteRT for Microcontrollers

Google's on-device runtime for phones, SBCs, and microcontrollers. **Renamed from "TensorFlow Lite" to "LiteRT" in Sept 2024** — the `.tflite` model format is unchanged, but the packages and imports moved.

- **Docs:** [ai.google.dev/edge/litert](https://ai.google.dev/edge/litert) · **Repo:** [google-ai-edge/LiteRT](https://github.com/google-ai-edge/LiteRT)
- **Microcontrollers:** [tensorflow/tflite-micro](https://github.com/tensorflow/tflite-micro)

## What changed (read before following old tutorials)
- **TensorFlow 2.20 (Aug 2025) deprecated `tf.lite`**; on-device dev moved to the standalone LiteRT repo.
- **Python:** `pip install tflite-runtime` → **`pip install ai-edge-litert`**; `from ai_edge_litert.interpreter import Interpreter`.
- **Android (Maven):** `org.tensorflow:tensorflow-lite` → **`com.google.ai.edge.litert`**.
- New capabilities: a **Compiled Model API**, unified NPU acceleration, and **LiteRT-LM** for on-device LLMs.

Full migration notes: [renames-and-deprecations.md](../renames-and-deprecations.md).

## LiteRT (mobile / SBC)
Use it on phones and Linux SBCs (including Raspberry Pi) when you want a small, fast runtime and have `.tflite` models. Delegates accelerate execution (GPU, NNAPI/NPU, etc.).

```python
from ai_edge_litert.interpreter import Interpreter
import numpy as np

interp = Interpreter(model_path="model.tflite")
interp.allocate_tensors()
inp = interp.get_input_details()[0]
out = interp.get_output_details()[0]
interp.set_tensor(inp["index"], np.zeros(inp["shape"], dtype=inp["dtype"]))
interp.invoke()
print(interp.get_tensor(out["index"]).shape)
```

## LiteRT for Microcontrollers (TinyML)
The MCU path (Arduino, ESP32, Arm Cortex-M, DSPs) — kilobytes to a few megabytes of memory, often battery-powered and always-on. Still developed in the **`tflite-micro`** repo. Typical tasks: keyword spotting, gesture recognition, anomaly detection, simple vision.

This is the **Embedded AI** tier from [concepts](../concepts-and-definitions/). For a hands-on intro, see the [TinyML starter ideas](../beginner-projects/) and pair with platforms like Edge Impulse for data collection and deployment.

**Strengths:** tiny footprint, huge device support, mature. **Trade-off:** smaller op coverage than full runtimes; quantization (INT8) is usually required for MCUs.
