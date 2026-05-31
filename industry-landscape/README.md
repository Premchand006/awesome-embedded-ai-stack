# Industry Landscape

Why this skill set is worth learning, who the players are, and where the growth is. Figures are from public market research (2025–2026) — **scope and definitions vary widely**, so we cite the range rather than a single hero number.

## Market size & growth
"Edge AI" is defined differently by each analyst (whole market vs. hardware-only vs. accelerators vs. off-device infrastructure), which is why the numbers diverge. The throughline: **a ~USD 25B market in 2025 heading to USD 57–165B by 2030–2035**, growing double-digits.

| Source (date) | Scope | ~2025 | Out-year | CAGR |
|---|---|---|---|---|
| BCC Research (Oct 2025) | Edge AI market | $11.8B | $56.8B (2030) | 36.9% |
| MarketsandMarkets (Aug 2025) | Edge AI **hardware** | $26.14B | $58.90B (2030) | 17.6% |
| Grand View Research | Edge AI | $24.91B | $118.69B (2033) | 21.7% |
| Precedence Research (2026) | Edge AI | $25.65B | $165.05B (2035) | 20.46% |
| Mordor Intelligence | Edge AI **accelerators** | $7.45B (2024) | $35.75B (2030) | 31% |
| STL Partners (Jan 2025) | Edge AI (off-device infra) | $54B (2024) | $157B (2030) | 19% |

**Takeaways:** hardware is the largest revenue slice; **accelerators are the fastest-growing** sub-segment (~31% CAGR per Mordor); estimates differ mainly because of scope. Always state the source + scope + year when you quote a figure.

## Vendor landscape
Names that recur across these reports as Edge AI hardware leaders: **NVIDIA, Qualcomm, Intel, AMD, Google, Huawei, Samsung, Apple, MediaTek**, plus pure-play edge-NPU vendors like **Hailo** (and Axelera, SiMa.ai, MemryX, Kneron). Map them to platforms in the [hardware landscape](../hardware-landscape/):

| Tier | Players | This repo's pages |
|---|---|---|
| Full robotics/edge platform | NVIDIA (Jetson, Isaac, Holoscan) | [Jetson](../hardware-landscape/jetson.md) · [Robotics](../robotics-and-ros2/) |
| x86 NPUs / inference toolkits | Intel (OpenVINO), AMD (Ryzen AI) | [Intel & AMD](../hardware-landscape/intel-and-amd.md) |
| Mobile / Snapdragon | Qualcomm (AI Hub) | [Runtimes](../runtimes-and-sdks/) |
| Discrete edge NPUs | Hailo, Axelera, SiMa.ai, MemryX, Kneron | [Discrete NPUs](../hardware-landscape/discrete-npus.md) |
| Low-cost SBC NPUs | Rockchip (RK3588) | [RK3588](../hardware-landscape/rk3588.md) |

Regionally, **North America led** Edge AI revenue in 2024 (~37–40%), with **Asia-Pacific the fastest-growing**. By component, **hardware** leads (~half of revenue); by application, **computer vision** dominates (~49.5%).

## Applications by vertical (where it's growing)
| Vertical | What edge AI does | Momentum |
|---|---|---|
| **Manufacturing** | defect detection, predictive maintenance, robotics | Fastest-growing end-use (~23% CAGR, GVR) |
| **Automotive / autonomous** | perception, driver monitoring, ADAS | Large, sustained |
| **Healthcare** | on-device monitoring, imaging, surgical AI | ~28% CAGR; ~950 FDA AI/ML device clearances in 2024 |
| **Retail** | video analytics, checkout-free, footfall | Major CV adopter |
| **Drones / robotics** | navigation, inspection, delivery | Rising with Physical AI |
| **Smart cities / security** | traffic, safety, anomaly detection | Steady; privacy pushes inference on-device |

## Skills that are becoming valuable
Build these (the [roadmap](../knowledge-roadmap.md) is organized around them):
- **Model optimization** — quantization/compression (INT8/INT4), pruning.
- **Runtime/EP selection** — ONNX Runtime, TensorRT, OpenVINO, LiteRT, QNN.
- **Pipeline engineering** — GStreamer/DeepStream, ROS 2 perception.
- **Embedded + CUDA** — JetPack/embedded Linux, CUDA/TensorRT optimization.
- **Sensor fusion** and **sim/synthetic-data** workflows (Omniverse/Cosmos).

## Where developers get confused (content opportunities)
This hub exists to fix exactly these:
1. **Hardware selection** — TOPS marketing vs. real FPS; memory limits for LLMs. → [hardware](../hardware-landscape/)
2. **Runtime selection** — which runtime/EP per chip. → [runtimes](../runtimes-and-sdks/)
3. **Pipeline building** — GStreamer/DeepStream vs. ROS 2 graphs. → [pipelines](../edge-pipelines/)
4. **Tracking change** — renames/deprecations (TFLite→LiteRT, Coral, ROS LTS). → [deprecations](../renames-and-deprecations.md)

*Figures here are approximate and sourced from public summaries of paywalled reports; verify against the original before citing in formal work.*
