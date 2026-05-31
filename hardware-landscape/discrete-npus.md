# Discrete Edge NPUs

Add an AI accelerator to an existing x86/Arm host via **M.2 or PCIe**. This is the fastest-growing slice of edge hardware — and where the 2025–2026 shift to **generative AI at the edge** (on-module DRAM enabling LLMs/VLMs) is most visible.

## Hailo
- **Org:** [github.com/hailo-ai](https://github.com/hailo-ai)
- **Hailo-8** — up to **26 TOPS**, ~2.5 W, on-chip memory (no external DRAM).
- **Hailo-8L** — **13 TOPS**, entry-level.
- **Hailo-10H** — **40 TOPS INT4 / 20 TOPS INT8**, on-module **4/8 GB** DRAM, runs LLMs/VLMs/Stable Diffusion. **GA July 2025**; automotive-qualified (AEC-Q100 Grade 2). The first widely-orderable discrete AI processor with native generative-AI edge support.
- **Software:** HailoRT, TAPPAS, Hailo Dataflow Compiler, Hailo Model Zoo. Also powers the [Raspberry Pi AI HAT+/HAT+ 2](raspberry-pi-and-hailo.md).
- ✅ Excellent perf/Watt and tooling for CV. ⚠️ custom models need compilation; 8/8L can't do LLMs (use 10H).

## Axelera AI — Metis
- **Site/repo:** [axelera.ai](https://axelera.ai/) · [axelera-ai-hub/voyager-sdk](https://github.com/axelera-ai-hub/voyager-sdk)
- **Metis AIPU** — up to **214 TOPS (M.2 / PCIe x1)** and **856 TOPS (PCIe x4)** (vendor figures).
- **Voyager SDK** — YAML-declared pipelines built on **Apache TVM** (compiler) + **GStreamer** (media). The Metis Compute Board pairs the AIPU with an RK3588.
- ✅ Very high vendor TOPS for multi-stream CV. ⚠️ independent reviewers report custom-model export friction and a pipeline-centric (not model-centric) workflow; benchmark before committing.

## SiMa.ai — MLSoC
- **Site/org:** [sima.ai/mlsoc](https://sima.ai/mlsoc/) · [github.com/sima-ai](https://github.com/sima-ai)
- First-gen **MLSoC** plus the new **MLSoC Modalix** family (**50–200 TOPS**, multimodal: text/image/audio/video; CNN/Transformer/LLM/GenAI).
- **Palette SDK** accelerates the *whole* pipeline (8-core Arm A65 + ISP + CV + MLA on one chip).
- ✅ True system-on-chip with strong perf/Watt; multimodal/GenAI focus. ⚠️ more enterprise/embedded-design oriented than hobbyist.

## MemryX — MX3
- **Site:** [memryx.com](https://memryx.com/)
- M.2 accelerator with **open-source drivers + SDK**, strong docs, **INT8 + BF16**, hosts on Windows/Linux/ARM/RISC-V.
- ✅ The most developer-friendly to get running; open stack. ⚠️ not the fastest vs Hailo/Axelera; ~40 MB on-chip weight memory limits large transformers; smaller community.

## Kneron
- **Org/docs:** [github.com/kneron](https://github.com/kneron) · [doc.kneron.com](https://doc.kneron.com/)
- Line: **KL520** (gen-1), **KL530** (INT4 + ViT), **KL630** (gen-3 NPU), **KL720** (1.4 TOPS, 0.9 TOPS/W), **KL730** (up to **3.6 eTOPS@INT8 / 7.2 eTOPS@INT4**, lightweight LLM/GPT), **KL830** (AI-PC focus).
- **SDK:** Kneron PLUS (v3.0.0+). Frameworks: Caffe/TF/TFLite/PyTorch/Keras/ONNX.
- ✅ Ultra-low-power dongles/SoCs for embedded vision. ⚠️ niche; smaller ecosystem.

## Google Coral / Edge TPU — ⚠️ legacy only
- **4 TOPS Edge TPU**, ~2 W. **Effectively abandoned:** the kernel **GASKET driver was removed from staging**, upstream runtimes dropped support, and stock is gone. Google has pivoted to a separate, not-yet-shipping open-source **"Coral NPU"** RISC-V architecture.
- **Recommendation:** don't pick Coral for new work — use **Hailo**. Full context: [renames-and-deprecations.md](../renames-and-deprecations.md).

## How to choose a discrete NPU
| Priority | Pick |
|---|---|
| Easiest to get running, open stack | **MemryX MX3** |
| Best CV perf/Watt + Raspberry Pi path | **Hailo** |
| On-device LLM/VLM on a small board | **Hailo-10H** |
| Max multi-stream CV throughput | **Axelera Metis** (benchmark first) |
| Full multimodal SoC for a product | **SiMa.ai Modalix** |
| Milliwatt embedded vision | **Kneron** |
