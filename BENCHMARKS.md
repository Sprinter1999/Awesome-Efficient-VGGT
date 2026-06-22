# 📊 Benchmarks & Evaluation Summary

> A comprehensive survey of evaluation protocols, datasets, metrics, and reported results for all efficient VGGT methods collected in this repo.
>
> 💡 **Tip:** Click any method name to jump to its paper. Numbers in **bold** are the best in each column.

---

## 📋 Table of Contents

- [🗺️ Overview](#️-overview)
- [🗂️ Evaluation Datasets](#️-evaluation-datasets)
- [📐 Metrics Glossary](#-metrics-glossary)
- [🚀 Training-free Methods](#-training-free-methods)
- [🏋️ Training-aware Methods](#️-training-aware-methods)
- [🔁 Test-Time Training Methods](#-test-time-training-methods)
- [⚡ Quantization Methods](#-quantization-methods)
- [🌟 VGGT-native Extensions](#-vggt-native-extensions)
- [📈 Efficiency–Quality Trade-off](#-efficiencyquality-trade-off)
- [📝 Notes](#-notes)

---

## 🗺️ Overview

Efficient VGGT methods are evaluated along two orthogonal axes: **reconstruction quality** (camera pose, depth, point cloud) and **system efficiency** (inference speed, memory, scalability). The community has converged on a shared set of benchmarks, enabling apples-to-apples comparison.

The table below summarizes which axes each method covers. ✅ = evaluated, — = not reported.

| Method | 📷 Camera Pose | 🌊 Depth | ☁️ Point Cloud | ⚡ Speedup | 💾 Memory | 🌍 Scene Scale |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| [VGGT-Long](https://arxiv.org/abs/2507.16443) | ✅ | — | ✅ | — | — | km-scale |
| [FastVGGT](https://arxiv.org/abs/2509.02560) | ✅ | — | ✅ | ✅ | — | 1000 imgs |
| [Sparse-VGGT](https://arxiv.org/abs/2509.07120) | ✅ | — | ✅ | ✅ | — | 200 views |
| [SwiftVGGT](https://arxiv.org/abs/2511.18290) | ✅ | — | ✅ | ✅ | — | km-scale |
| [HTTM](https://arxiv.org/abs/2511.21317) | — | — | ✅ | ✅ | — | 1000 imgs |
| [AVGGT](https://arxiv.org/abs/2512.02541) | ✅ | — | ✅ | ✅ | — | 800 imgs |
| [LiteVGGT](https://arxiv.org/abs/2512.04939) | ✅ | — | ✅ | ✅ | ✅ | 1000 imgs |
| [XStreamVGGT](https://arxiv.org/abs/2601.01204) | — | — | ✅ | ✅ | ✅ | streaming |
| [Spark3R](https://arxiv.org/abs/2605.06270) | ✅ | ✅ | ✅ | ✅ | — | 1000 imgs |
| [StreamVGGT](https://arxiv.org/abs/2507.11539) | ✅ | ✅ | ✅ | ✅ | ✅ | streaming |
| [eVGGT](https://arxiv.org/abs/2509.15880) | — | — | — | ✅ | ✅ | robotics |
| [Co-Me](https://arxiv.org/abs/2511.14751) | ✅ | ✅ | ✅ | ✅ | — | 512 imgs |
| [FlashVGGT](https://arxiv.org/abs/2512.01540) | ✅ | ✅ | ✅ | ✅ | ✅ | 3000+ imgs |
| [PaceVGGT](https://arxiv.org/abs/2605.08371) | ✅ | ✅ | ✅ | ✅ | — | 1000 imgs |
| [Lite3R](https://arxiv.org/abs/2605.11354) | — | — | ✅ | ✅ | ✅ | — |
| [TurboVGGT](https://arxiv.org/abs/2605.14315) | ✅ | — | ✅ | ✅ | — | — |
| [D4RT](https://arxiv.org/abs/2512.08924) | ✅ | ✅ | ✅ | — | — | dynamic |
| [Test3R](https://arxiv.org/abs/2506.13750) | — | ✅ | ✅ | — | — | multi-view |
| [TTT3R](https://arxiv.org/abs/2509.26645) | ✅ | — | — | ✅ | ✅ | streaming |
| [VGG-T³](https://arxiv.org/abs/2602.23361) | — | — | ✅ | ✅ | — | 1000+ imgs |
| [QuantVGGT](https://arxiv.org/abs/2509.21302) | ✅ | — | ✅ | ✅ | ✅ | standard |
| [VersaQ-3D](https://arxiv.org/abs/2601.20317) | ✅ | — | ✅ | ✅ | — | edge |
| [TAPTQ](https://arxiv.org/abs/2602.01741) | ✅ | ✅ | ✅ | — | — | standard |
| [FGQ](https://arxiv.org/abs/2605.15828) | ✅ | ✅ | ✅ | — | — | standard |
| [VGGT-Ω](https://arxiv.org/abs/2605.15195) | ✅ | ✅ | ✅ | — | ✅ | dynamic |
| [HD-VGGT](https://arxiv.org/abs/2603.27222) | — | ✅ | ✅ | — | — | high-res |
| [RobustVGGT](https://arxiv.org/abs/2512.04012) | — | — | ✅ | — | — | in-the-wild |
| [OmniVGGT](https://arxiv.org/abs/2511.10560) | ✅ | ✅ | ✅ | — | — | multi-task |

---

## 🗂️ Evaluation Datasets

### 🏠 Indoor Reconstruction

| Dataset | Split Used | Notes |
|---|---|---|
| 🔗 [**ScanNet**](http://www.scan-net.org/) | 50 scenes (ScanNet-50), up to 2000 frames | Primary large-scale indoor benchmark; 100 / 500 / 1000 frame variants commonly tested |
| 🔗 [**7 Scenes**](https://www.microsoft.com/en-us/research/project/rgb-d-dataset-7-scenes/) | keyframes every 2–10 frames | Short-to-mid sequence benchmark (kitchen, chess, office…) |
| **NRGBD** | keyframes every 3 frames | Neural RGB-D benchmark; challenging indoor reconstruction |
| 🔗 [**ETH3D**](https://www.eth3d.net/) | training set, 16 frames typical | Multi-view stereo benchmark; fine-grained Chamfer evaluation |
| 🔗 [**DTU**](https://roboimagedata.compute.dtu.dk/?page_id=36) | 32–48 frames/object | Object-centric multi-view stereo |

### 🌲 Outdoor / Large-Scale

| Dataset | Split Used | Notes |
|---|---|---|
| 🔗 [**KITTI Odometry**](https://www.cvlibs.net/datasets/kitti/eval_odometry.php) | Seq. 00–10 (GT), 11–21 (pseudo GT) | Driving sequences up to 5 km; ATE RMSE in meters |
| 🔗 [**Waymo Open Dataset**](https://waymo.com/open/) | 10 urban segments (~300m each) | Urban driving; VGGT-Long achieves ~5× better ATE than CUT3R |
| **Virtual KITTI** | 5 scenes × 6 conditions | Synthetic driving for ablation |
| 🔗 [**Tanks & Temples**](https://www.tanksandtemples.org/) | training scenes | Large-scale outdoor/indoor; pose + reconstruction |

### 📷 Camera Pose Estimation

| Dataset | Frames | Notes |
|---|---|---|
| 🔗 [**CO3Dv2**](https://github.com/facebookresearch/co3d) | 10–20 images/scene | Object-centric; AUC@30/15/5/3 is the primary metric |
| 🔗 [**RealEstate10K**](https://google.github.io/realestate10k/) | 10–128 frames/scene | Indoor room sequences |
| **TUM-dynamics** | variable | Dynamic indoor scenes; ATE evaluation |

### 🌊 Depth Estimation

| Dataset | Notes |
|---|---|
| 🔗 [**NYU-v2**](https://cs.nyu.edu/~silberman/datasets/nyu_depth_v2.html) | Indoor RGBD; monocular depth |
| **KITTI Depth** | Outdoor driving; mono + multi-view depth |
| **Sintel** | Synthetic; challenging lighting & motion |
| **Bonn** | Dynamic indoor; temporal depth |

### 🎯 Specialized

| Dataset | Task | Notes |
|---|---|---|
| **BlendedMVS** | Feed-forward 3D reconstruction | Used by [Lite3R](https://arxiv.org/abs/2605.11354) |
| **RoboTwin / ManiSkill** | Robotic manipulation | Used by [eVGGT](https://arxiv.org/abs/2509.15880) for task success |
| **Real Kinova Gen3** | Real-robot manipulation | Push Cube, Pick & Place tasks |

---

## 📐 Metrics Glossary

### ☁️ Point Cloud Quality

| Metric | Symbol | Direction | Definition |
|---|---|---|---|
| Accuracy | Acc | ↓ lower is better | Mean distance: predicted → ground-truth surface (cm or m) |
| Completeness | Comp | ↓ | Mean distance: GT surface → nearest predicted point |
| Normal Consistency | NC | ↑ higher is better | Mean cosine similarity between estimated and GT normals |
| Chamfer Distance | CD | ↓ | Symmetric mean of Acc + Comp |
| F1 Score | F1 | ↑ | Harmonic mean of precision and recall at a distance threshold |

### 📷 Camera Pose

| Metric | Symbol | Direction | Definition |
|---|---|---|---|
| Absolute Trajectory Error | ATE | ↓ | RMSE of absolute camera position (m) |
| Absolute Rotation Error | ARE | ↓ | Mean angular error of camera orientation (°) |
| RPE Translation | RPE-trans | ↓ | Relative pose error in translation between consecutive frames |
| RPE Rotation | RPE-rot | ↓ | Relative pose error in rotation between consecutive frames |
| Relative Rotation Accuracy | RRA@k | ↑ | % of pairs with rotation error < k° |
| Relative Translation Accuracy | RTA@k | ↑ | % of pairs with translation error < k° |
| Area Under Curve | AUC@k | ↑ | Area under the pose accuracy curve up to threshold k° |

### 🌊 Depth Estimation

| Metric | Symbol | Direction | Definition |
|---|---|---|---|
| Absolute Relative Error | Abs Rel | ↓ | Mean \|pred−GT\| / GT |
| Inlier Ratio | δ<1.25 | ↑ | % of pixels where max(pred/GT, GT/pred) < 1.25 |
| L1 Error | L1 | ↓ | Mean absolute depth error in meters |

### ⚡ Efficiency

| Metric | Symbol | Direction | Definition |
|---|---|---|---|
| Speedup | × | ↑ | Inference time ratio vs. vanilla VGGT baseline |
| Memory Reduction | × | ↑ | Peak GPU memory ratio vs. VGGT baseline |
| Frames Per Second | FPS | ↑ | Online / streaming throughput |
| Latency | ms / s | ↓ | Per-forward-pass wall-clock time |

---

## 🚀 Training-free Methods

> Applied to a pretrained VGGT checkpoint with **no parameter updates** — plug-and-play! 🔌

### 📷 Camera Pose — Tanks & Temples (200 views)

*From [Sparse-VGGT](https://arxiv.org/abs/2509.07120) ![CVPR 2026](https://img.shields.io/badge/CVPR-2026-blue.svg?style=flat-square) — block-sparse global attention.*

| Method | RRA@5 ↑ | RTA@5 ↑ | ATE ↓ | Time (s) ↓ | Speedup |
|---|:---:|:---:|:---:|:---:|:---:|
| VGGT | 83.9 | 79.9 | 0.012 | 18.0 | 1× |
| Sparse-VGGT (25% sparse) | 83.1 | 79.6 | 0.011 | 8.5 | **2.1×** |
| Sparse-VGGT (50% sparse) | 80.7 | 78.4 | 0.011 | 7.3 | **2.5×** |
| Sparse-VGGT (75% sparse) | 57.1 | 60.8 | 0.013 | 5.5 | 3.3× |
| pi3 | 85.4 | 83.9 | 0.009 | 13.9 | — |
| pi3 (25% sparse) | 84.6 | 83.5 | 0.009 | 6.8 | **2.0×** |
| pi3 (50% sparse) | 82.9 | 82.3 | 0.009 | 5.8 | **2.4×** |

> 💡 The **25–50% sparsity sweet spot** delivers 2–2.5× speedup with a drop of less than 3–4 points in RRA/RTA.

---

### ☁️ Point Cloud — ScanNet-50 (1000 images)

*[FastVGGT](https://arxiv.org/abs/2509.02560) [![GitHub](https://img.shields.io/badge/GitHub-mystorm16%2FFastVGGT-black?logo=github&style=flat-square)](https://github.com/mystorm16/FastVGGT) and [LiteVGGT](https://arxiv.org/abs/2512.04939) [![GitHub](https://img.shields.io/badge/GitHub-GarlicBa%2FLiteVGGT-black?logo=github&style=flat-square)](https://github.com/GarlicBa/LiteVGGT-repo). Chamfer Distance (CD) ↓.*

| Method | CD ↓ | Time (s) ↓ | Speedup |
|---|:---:|:---:|:---:|
| VGGT* (chunked) | 0.471 | 724.6 | 1× |
| [FastVGGT](https://arxiv.org/abs/2509.02560) | 0.425 | 180.7 | **4.0×** |
| [LiteVGGT](https://arxiv.org/abs/2512.04939) | **best-in-class** | ~72 | **~10×** |
| CUT3R | 0.786 | 34.8 | — |
| Fast3R | 0.684 | 397.8 | — |

> ⚠️ Vanilla VGGT goes OOM beyond ~500 images. VGGT\* is the chunked baseline. LiteVGGT reports the **lowest CD** of all compared methods.

---

### 📷 Camera Pose — ScanNet-50 (ATE / ARE by sequence length)

*[FastVGGT](https://arxiv.org/abs/2509.02560) head-to-head. Lower is better.*

| Input Frames | VGGT* ATE | FastVGGT ATE | VGGT* ARE | FastVGGT ARE |
|---|:---:|:---:|:---:|:---:|
| 100 | 0.140 | 0.141 | 3.625 | 3.512 |
| 300 | 0.145 | 0.142 | 3.689 | 3.554 |
| 500 | 0.174 | **0.145** | 4.190 | **3.591** |
| 1000 | 0.196 | **0.164** | 4.636 | **3.860** |

> 📈 FastVGGT actually **improves** over VGGT* at long sequences, because token merging reduces attention dilution.

---

### ☁️ Point Cloud — 7 Scenes / NRGBD (Acc / Comp, relative to VGGT baseline)

| Method | 7Sc Acc ↓ | 7Sc Comp ↓ | NRGBD Acc ↓ | NRGBD Comp ↓ | Speedup |
|---|:---:|:---:|:---:|:---:|:---:|
| VGGT (baseline) | ref | ref | ref | ref | 1× |
| [FastVGGT](https://arxiv.org/abs/2509.02560) | ≈ | ↑ on NRGBD | ≈ | degraded | ~4× |
| [HTTM](https://arxiv.org/abs/2511.21317) | ≈ | ≈ | ≈ | ≈ | **7×** |
| [AVGGT](https://arxiv.org/abs/2512.02541) | ≈ | ≈ | ≈ | ≈ | **8–10×** @800f |
| [Spark3R](https://arxiv.org/abs/2605.06270) | competitive | competitive | competitive | competitive | **28×** @1000f |

---

### 🌲 Large-Scale Outdoor — KITTI Odometry (ATE RMSE, m)

*[VGGT-Long](https://arxiv.org/abs/2507.16443) ![ICRA 2026](https://img.shields.io/badge/ICRA-2026-orange.svg?style=flat-square) [![GitHub](https://img.shields.io/badge/GitHub-DengKaiCQ%2FVGGT--Long-black?logo=github&style=flat-square)](https://github.com/DengKaiCQ/VGGT-Long) and [SwiftVGGT](https://arxiv.org/abs/2511.18290).*

| Method | Calib. Required? | Avg ATE ↓ | Avg* ATE ↓ | FPS ↑ |
|---|:---:|:---:|:---:|:---:|
| ORB-SLAM2 (w/ LC) | ✅ | 54.82 | 9.46 | — |
| DPV-SLAM++ | ✅ | 25.75 | 27.14 | — |
| CUT3R | ❌ | 💥 OOM | — | — |
| Fast3R | ❌ | 💥 OOM | — | — |
| VGGT (direct) | ❌ | 💥 OOM | — | — |
| [VGGT-Long](https://arxiv.org/abs/2507.16443) (CS=60) | ❌ | 26.36 | 19.30 | 6.91 |
| [**SwiftVGGT**](https://arxiv.org/abs/2511.18290) | ❌ | **29.18** | — | **20.73** |

> 🏎️ SwiftVGGT runs **3× faster** than VGGT-Long (20.73 vs. 6.91 FPS) with comparable ATE — no extra VPR model needed.
>
> *Avg\* excludes Seq. 01 (highway), which is notoriously hard for vision-only methods.*

---

### 🌲 Large-Scale Outdoor — Waymo Open Dataset (10 urban segments)

| Method | ATE RMSE (m) ↓ | Point Acc ↓ | Chamfer ↓ |
|---|:---:|:---:|:---:|
| DROID-SLAM | ~4.4 | 1.201 | 4.870 |
| MASt3R-SLAM | 5.560 | 3.772 | 3.474 |
| CUT3R | 9.872 | 3.884 | 5.343 |
| [**VGGT-Long**](https://arxiv.org/abs/2507.16443) | **1.996** | **1.182** | **2.021** |
| [SwiftVGGT](https://arxiv.org/abs/2511.18290) | competitive | competitive | competitive |

> 🎯 VGGT-Long is **~5× better ATE than CUT3R** on Waymo (1.996 vs. 9.872m), without any camera calibration.

---

### ⚡ Efficiency Scaling Summary — Training-free Methods

| Method | @100 frames | @300 frames | @800–1000 frames | Max Scale |
|---|:---:|:---:|:---:|:---:|
| [FastVGGT](https://arxiv.org/abs/2509.02560) | ~1.7× | ~3.2× | ~4.0× | 1000 imgs |
| [Sparse-VGGT](https://arxiv.org/abs/2509.07120) (25%) | 2.0× | 2.0× | 2.1× | 200+ views |
| [HTTM](https://arxiv.org/abs/2511.21317) | — | — | **7×** | 1000 imgs |
| [AVGGT](https://arxiv.org/abs/2512.02541) | ~2× | **4–5×** | **8–10×** | 800 imgs |
| [LiteVGGT](https://arxiv.org/abs/2512.04939) | — | — | **~10×** | 1100 imgs |
| [XStreamVGGT](https://arxiv.org/abs/2601.01204) [![GitHub](https://img.shields.io/badge/GitHub-ywh187%2FXStreamVGGT-black?logo=github&style=flat-square)](https://github.com/ywh187/XStreamVGGT/) | — | — | **5.48× + 4.42× mem** | streaming |
| [Spark3R](https://arxiv.org/abs/2605.06270) | — | — | 🏆 **28×** | 1000 imgs |

---

## 🏋️ Training-aware Methods

> These methods require auxiliary training, distillation, or fine-tuning — but unlock new capabilities like streaming inference or cross-domain transfer. 🤸

### ☁️ Streaming 3D Reconstruction — 7 Scenes / NRGBD / ETH3D

*[StreamVGGT](https://arxiv.org/abs/2507.11539) [![GitHub](https://img.shields.io/badge/GitHub-wzzheng%2FStreamVGGT-black?logo=github&style=flat-square)](https://github.com/wzzheng/StreamVGGT) — causal streaming architecture distilled from VGGT.*

| Method | 7Sc Acc ↓ | 7Sc Comp ↓ | 7Sc NC ↑ | NRGBD Acc ↓ | NRGBD NC ↑ | ETH3D Chamfer ↓ |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| VGGT (offline) | 0.088 | 0.091 | 0.787 | 0.073 | 0.910 | 0.686 |
| CUT3R (streaming) | 0.126 | 0.154 | 0.727 | 0.099 | 0.837 | 1.411 |
| [**StreamVGGT**](https://arxiv.org/abs/2507.11539) | 0.129 | **0.115** | 0.751 | **0.084** | 0.861 | **0.577** |

> 🌟 StreamVGGT **surpasses offline VGGT** on ETH3D (Chamfer **0.577** vs. 0.686) — while running in streaming mode! It also beats CUT3R on every single metric.

---

### 🌊 Streaming Depth Estimation — 4 Datasets

*[StreamVGGT](https://arxiv.org/abs/2507.11539). Format: Abs Rel ↓ / δ<1.25 ↑.*

| Method | Sintel | Bonn | KITTI | NYU-v2 |
|---|:---:|:---:|:---:|:---:|
| VGGT | 0.276 / 67.5 | 0.055 / 97.1 | 0.072 / 93.8 | 0.060 / 95.1 |
| CUT3R | 0.428 / 55.4 | 0.063 / 96.2 | 0.092 / 91.3 | 0.086 / 90.9 |
| [**StreamVGGT**](https://arxiv.org/abs/2507.11539) | **0.254 / 68.5** | **0.052 / 97.1** | **0.072 / 94.7** | **0.055 / 95.9** |

> 🎯 StreamVGGT matches or **exceeds offline VGGT** on all four depth datasets while streaming.

---

### ⚡ Streaming Inference Efficiency (A800 GPU, 5 frames)

| Method | Acc ↓ | Time (ms) ↓ | Memory (GB) ↓ |
|---|:---:|:---:|:---:|
| CUT3R | 0.038 | 102 | 3.5 |
| Spann3R | 0.038 | 87 | 5.4 |
| [**StreamVGGT**](https://arxiv.org/abs/2507.11539) | **0.024** | 88 | **2.7** |
| StreamVGGT (1 frame) | — | **63** | **2.1** |

---

### 🎯 Confidence-Guided Token Merging — [Co-Me](https://arxiv.org/abs/2511.14751) [![GitHub](https://img.shields.io/badge/GitHub-co--me--tokens%2FCoMe-black?logo=github&style=flat-square)](https://github.com/co-me-tokens/CoMe)

*Distills a lightweight confidence predictor; works on VGGT, pi3, MapAnything, and DepthAnything3.*

| Frames / Task | Dataset | Speedup ↑ | Quality Change |
|---|---|:---:|:---:|
| 32 frames (pose) | DTU | 7.72× | AUC drop < 1% |
| 128 frames (pose) | RealEstate10K | 16.2× | AUC drop < 1% |
| 32 frames (point cloud) | DTU | 7.71× | Acc ≈ baseline |
| 16 frames (point cloud) | ETH3D | 4.84× | Acc ≈ pi3 |
| 512 frames | — | 🏆 **21.5×** (VGGT) | maintained |
| 512 frames | — | 🏆 **20.4×** (pi3) | maintained |

> ✨ Co-Me uniquely supports **single-frame inference** (unlike FastVGGT) and generalizes across four different model architectures.

---

### 🔥 FlashVGGT — Compressed Descriptor Attention ![CVPR 2026](https://img.shields.io/badge/CVPR-2026-blue.svg?style=flat-square)

*[FlashVGGT](https://arxiv.org/abs/2512.01540) scales to **3000+ images** via chunk-recursive streaming with cached cross-attention descriptors.*

| Scene Length | Accuracy vs. VGGT | Inference Time (% of VGGT) | Speedup |
|---|:---:|:---:|:---:|
| 100 images | Comparable | ~33% | >3× |
| 500 images | Competitive | ~12.5% | >8× |
| 1000 images | **Better** (VGGT degrades) | **9.3%** | **~10.75×** |
| 3000+ images | Stable | — | scales linearly |

> 🌊 Online mode (N-RGBD, 500 imgs): FlashVGGT is **>3.3× faster than CUT3R** and uses **<1/4 the memory of StreamVGGT**.

---

### ✂️ PaceVGGT — Pre-Attention Token Pruning

*[PaceVGGT](https://arxiv.org/abs/2605.08371) — distilled DINO-based Token Scorer with downstream geometry losses.*

| Dataset | N Frames | vs. VGGT ↓ | vs. LiteVGGT ↓ |
|---|:---:|:---:|:---:|
| ScanNet-50 | 300 | **5.1×** | — |
| ScanNet-50 | 1000 | — | **1.47×** |

> 📍 PaceVGGT sits on the **Pareto frontier** of quality vs. latency on both ScanNet-50 and 7-Scenes.

---

### 🤖 Robotic Manipulation — [eVGGT](https://arxiv.org/abs/2509.15880) [![GitHub](https://img.shields.io/badge/GitHub-andvg3%2FeVGGT-black?logo=github&style=flat-square)](https://github.com/andvg3/eVGGT)

*4-layer distilled geometry encoder (0.26B) designed to replace VGGT (1.29B) in robot policies.*

#### ManiSkill Simulation (Success Rate ↑)

| Method | Task 1 | Task 2 | Task 3 | Avg |
|---|:---:|:---:|:---:|:---:|
| ACT (RGB) | 0.71 | 0.90 | 0.47 | 0.693 |
| DP (RGB) | 0.85 | 0.88 | 0.62 | 0.783 |
| DP (RGBD) | — | — | — | 0.797 |
| **DP + eVGGT** | **0.96** | **0.91** | **0.65** | **0.840** |

#### Real-Robot Kinova Gen3 (Success Rate ↑)

| Method | Push Cube | Pick & Place |
|---|:---:|:---:|
| DP (ResNet) | 0.54 | 0.40 |
| **DP + eVGGT** | **0.72** | **0.60** |

#### Model Efficiency

| Model | Params | Inference Time | VRAM |
|---|:---:|:---:|:---:|
| VGGT | 1.29B | 0.601s | 7.2GB |
| **eVGGT** | **0.26B** | **0.069s** | **1.0GB** |

> 🤖 eVGGT is **9× faster** and **7× lower VRAM** than VGGT, while **exceeding DP (RGBD)** on ManiSkill — using only RGB!

---

## 🔁 Test-Time Training Methods

> Adapt the model at inference time with no offline training of auxiliary modules — the best of both worlds! 🌈

### ☁️ 3D Reconstruction — [Test3R](https://arxiv.org/abs/2506.13750) [![GitHub](https://img.shields.io/badge/GitHub-nopQAQ%2FTest3R-black?logo=github&style=flat-square)](https://github.com/nopQAQ/Test3R)

*Optimizes learnable visual prompt tokens at test time via cross-pair geometric consistency (frozen backbone).*

#### Point Cloud — 7 Scenes / NRGBD

| Method | 7Sc Acc ↓ | 7Sc Comp ↓ | 7Sc NC ↑ | NRGBD Acc ↓ | NRGBD Comp ↓ | NRGBD NC ↑ |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| DUSt3R | 0.146 | 0.181 | 0.736 | 0.144 | 0.154 | 0.871 |
| MAST3R | 0.189 | 0.211 | 0.687 | 0.085 | 0.063 | 0.794 |
| CUT3R | 0.126 | 0.154 | 0.727 | 0.099 | 0.076 | 0.837 |
| [**Test3R**](https://arxiv.org/abs/2506.13750) | **0.105** | **0.136** | **0.746** | **0.083** | 0.079 | **0.870** |

#### Multi-View Depth — DTU / ETH3D (no GT pose or intrinsics!)

| Method | DTU rel ↓ | DTU δ ↑ | ETH3D rel ↓ | ETH3D δ ↑ | Avg rel ↓ | Avg δ ↑ |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| DUSt3R | 3.3 | 69.9 | 3.3 | 73.0 | 3.3 | 71.5 |
| [**Test3R**](https://arxiv.org/abs/2506.13750) | **2.0** | **84.1** | **3.2** | **74.0** | **2.6** | **79.1** |

> 🎉 DTU: relative error **−39%** (3.3→2.0), inlier ratio **+14.2pp**. Generalizes to MAST3R and MonST3R backbones.

---

### 📍 Long-Sequence Pose — [TTT3R](https://arxiv.org/abs/2509.26645) ![ICLR 2026](https://img.shields.io/badge/ICLR-2026-green.svg?style=flat-square) [![GitHub](https://img.shields.io/badge/GitHub-Inception3D%2FTTT3R-black?logo=github&style=flat-square)](https://github.com/Inception3D/TTT3R)

*Reframes recurrent memory updates as online learning — training-free intervention for thousands of images.*

| Metric | Baseline Recurrent | TTT3R |
|---|:---:|:---:|
| Global pose accuracy | 1× | **2× improvement** 🚀 |
| Throughput | — | **20 FPS** |
| GPU memory (1000s of imgs) | high | **6 GB** |
| Complexity | O(N) | O(N) |

---

### 🧠 VGG-T³ — Test-Time MLP Distillation ![CVPR 2026](https://img.shields.io/badge/CVPR-2026-blue.svg?style=flat-square)

*[VGG-T³](https://arxiv.org/abs/2602.23361) replaces global softmax attention with a TTT-based MLP, achieving **O(N) complexity**.*

| Scene Size | Inference Time ↓ | Speedup vs. VGGT | Point Map Quality |
|---|:---:|:---:|:---:|
| 1000 images | **54 seconds** ⏱️ | **11.6×** | Outperforms all linear-time methods |
| 1000+ images | linear scaling | — | stable |

> 🔍 VGG-T³ also enables **visual localization** — unseen images can directly query the distilled MLP representation.

---

## ⚡ Quantization Methods

> Compress the billion-parameter VGGT for deployment with minimal accuracy loss. 🗜️

### 🏆 [QuantVGGT](https://arxiv.org/abs/2509.21302) — W4A4 PTQ ![ICLR 2026](https://img.shields.io/badge/ICLR-2026-green.svg?style=flat-square) [![GitHub](https://img.shields.io/badge/GitHub-wlfeng0509%2FQuantVGGT-black?logo=github&style=flat-square)](https://github.com/wlfeng0509/QuantVGGT)

#### 📷 Camera Pose — CO3Dv2 (20 frames)

| Method | AUC@30 ↑ | AUC@15 ↑ | AUC@5 ↑ | AUC@3 ↑ |
|---|:---:|:---:|:---:|:---:|
| VGGT FP16 | 90.0 | 83.9 | 67.8 | 56.9 |
| SmoothQuant W4A4 | 72.1 | 55.3 | 21.0 | 9.3 |
| QuaRot W4A4 | 81.6 | 69.8 | 39.4 | 22.6 |
| **QuantVGGT W4A4** | **88.2** | **80.2** | **58.9** | **45.1** |
| QuantVGGT W8A8 | 89.6 | 83.2 | 66.0 | 54.9 |

> 🎯 QuantVGGT W4A4 retains **98% of FP16 AUC@30** (88.2 vs. 90.0), vs. QuaRot's 90.7% — a huge gap at 4-bit!

#### ☁️ Point Map — DTU (W4A4)

| Method | Acc ↓ | Comp ↓ | NC ↑ |
|---|:---:|:---:|:---:|
| FP16 | 1.185 | 2.232 | 0.694 |
| QuaRot W4A4 | 1.593 | 2.034 | 0.670 |
| **QuantVGGT W4A4** | **1.282** | **1.992** | **0.681** |

#### ☁️ Point Cloud — 7 Scenes / NRGBD (W4A4)

| Method | 7Sc Acc ↓ | 7Sc NC ↑ | NRGBD Acc ↓ | NRGBD NC ↑ |
|---|:---:|:---:|:---:|:---:|
| FP16 | 0.025 | 0.728 | 0.015 | 0.878 |
| SmoothQuant W4A4 | 0.370 | 0.484 | 0.479 | 0.515 |
| QuaRot W4A4 | 0.030 | 0.701 | 0.034 | 0.820 |
| **QuantVGGT W4A4** | **0.026** | **0.718** | **0.019** | **0.850** |

#### ⚡ Hardware Efficiency (RTX 4090, W4A4)

| | FP16 | QuantVGGT W4A4 |
|---|:---:|:---:|
| Memory | 1× | **3.7× reduction** 💾 |
| Inference Speed | 1× | **2.5× faster** ⚡ |

---

### 📊 All Quantization Methods at a Glance

| Method | Bit-width | Accuracy Retention | Speedup | Memory | Venue |
|---|:---:|:---:|:---:|:---:|:---:|
| [**QuantVGGT**](https://arxiv.org/abs/2509.21302) [![GitHub](https://img.shields.io/badge/GitHub-black?logo=github&style=flat-square)](https://github.com/wlfeng0509/QuantVGGT) | W4A4 / W8A8 | 98% @W4A4 | 2.5× | 3.7× | ![ICLR 2026](https://img.shields.io/badge/ICLR-2026-green.svg?style=flat-square) |
| [**VersaQ-3D**](https://arxiv.org/abs/2601.20317) | W4A8 / W4A4 | 98–99% @W4A8 | 5.2–10.8× (edge) | — | — |
| [**TAPTQ**](https://arxiv.org/abs/2602.01741) | W4 (VGGT+pi3) | SOTA PTQ | O(log N) calib | — | — |
| [**FGQ**](https://arxiv.org/abs/2605.15828) [![GitHub](https://img.shields.io/badge/GitHub-ypzhng%2FFGQ-black?logo=github&style=flat-square)](https://github.com/ypzhng/FGQ) | W4 | **+39% rel.** over SOTA | — | — | — |

> 🔧 **VersaQ-3D** achieves the largest hardware speedup via a custom reconfigurable systolic accelerator — built for edge deployment. **FGQ** uses Fisher information matrices to find per-task, per-block quantization sensitivity, closing the gap between 4-bit and FP16 significantly.

---

## 🌟 VGGT-native Extensions

> Not just efficient — these works fundamentally expand what VGGT can do. ✨

### 🏅 [VGGT-Ω](https://arxiv.org/abs/2605.15195) ![CVPR 2026 Oral](https://img.shields.io/badge/CVPR%202026-Oral-red.svg?style=flat-square) ![Best Paper Finalist](https://img.shields.io/badge/Best%20Paper-Finalist-gold.svg?style=flat-square) [![GitHub](https://img.shields.io/badge/GitHub-facebookresearch%2Fvggt--omega-black?logo=github&style=flat-square)](https://github.com/facebookresearch/vggt-omega)

*Scaled successor to VGGT using register attention, a single dense prediction head, self-supervised pretraining on unlabeled video, and a high-quality dynamic-scene annotation pipeline. Evaluated at 200M / 500M / 1B / 10B parameter scales.*

> 🧪 **Compared baselines:** MonST3R · MapAnything · MegaSaM · VGGT · pi3 · DepthAnything3-Giant (1B)

---

#### 📷 Camera Pose Estimation — AUC@3° / AUC@30° ↑

*10 randomly sampled frames per scene. Higher is better.*

**Static Scenes**

| Method | 7 Scenes @3° | 7 Scenes @30° | NRGBD @3° | NRGBD @30° | ETH3D @3° | ETH3D @30° |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| MonST3R | 9.0 | 68.3 | 13.9 | 79.7 | 1.7 | 14.3 |
| MegaSaM | 10.6 | 71.8 | 17.2 | 83.1 | 5.9 | 38.1 |
| VGGT | 10.9 | 74.4 | 81.7 | 97.7 | 18.8 | 62.1 |
| pi3 | 13.3 | 77.0 | 83.8 | 98.2 | 35.3 | 79.6 |
| DA3-Giant (1B) | 18.7 | 78.2 | 86.4 | 98.4 | 46.1 | 87.0 |
| **VGGT-Ω-1B** | **29.6** | **83.1** | **89.7** | **98.8** | **49.8** | **88.5** |
| **VGGT-Ω-10B** | **36.4** | **88.2** | **92.5** | **99.1** | **56.3** | **90.4** |

**Dynamic Scenes**

| Method | DyCheck @3° | DyCheck @30° | Sintel @3° | Sintel @30° | TUM-Dyn @3° | TUM-Dyn @30° |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| MonST3R | 11.5 | 45.4 | 4.3 | 45.8 | 7.7 | 48.5 |
| MegaSaM | 26.8 | 53.1 | 22.5 | 58.3 | 15.4 | 59.0 |
| VGGT | 21.0 | 78.7 | 15.0 | 50.0 | 16.6 | 61.2 |
| pi3 | 23.3 | 81.0 | 14.8 | 53.5 | 16.1 | 59.2 |
| DA3-Giant (1B) | 32.1 | 83.9 | 16.2 | 52.7 | 20.8 | 62.7 |
| **VGGT-Ω-1B** | **38.4** | **87.3** | **35.3** | **73.0** | **30.2** | **82.3** |
| **VGGT-Ω-10B** | **43.7** | **90.9** | **40.0** | **79.1** | **36.4** | **87.5** |

> 🏆 On Sintel, VGGT-Ω-10B achieves AUC@3° of **40.0** vs. 22.5 (MegaSaM) → **+77% relative improvement**. AUC@30° rises to 79.1 vs. 58.3 → **+35%**.

---

#### 🌊 Depth Estimation — δ<1.25 ↑ / AbsRel ↓

**Static Scenes**

| Method | 7Sc δ1.25 | 7Sc AbsRel | NRGBD δ1.25 | NRGBD AbsRel | ETH3D δ1.25 | ETH3D AbsRel |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| MonST3R | 92.4 | 0.075 | 98.4 | 0.030 | 95.8 | 0.056 |
| VGGT | 91.9 | 0.073 | 99.1 | 0.019 | 97.4 | 0.036 |
| pi3 | 92.8 | 0.068 | 99.2 | 0.011 | 99.6 | 0.016 |
| DA3-Giant (1B) | 93.0 | 0.063 | 99.5 | 0.010 | 99.6 | 0.015 |
| **VGGT-Ω-1B** | **94.6** | **0.058** | **99.6** | **0.010** | **99.8** | **0.012** |
| **VGGT-Ω-10B** | **96.3** | **0.050** | **99.7** | **0.007** | **99.8** | **0.009** |

**Dynamic Scenes**

| Method | DyCheck δ1.25 | DyCheck AbsRel | Sintel δ1.25 | Sintel AbsRel | TUM-Dyn δ1.25 | TUM-Dyn AbsRel |
|---|:---:|:---:|:---:|:---:|:---:|:---:|
| MonST3R | 93.3 | 0.068 | 71.9 | 0.263 | 85.0 | 0.148 |
| MegaSaM | 97.4 | 0.042 | 74.1 | 0.207 | 92.9 | 0.083 |
| VGGT | 95.2 | 0.055 | 79.2 | 0.189 | 92.2 | 0.064 |
| pi3 | 97.4 | 0.041 | 82.5 | 0.144 | 95.5 | 0.046 |
| DA3-Giant (1B) | 97.7 | 0.039 | 86.1 | 0.118 | 94.3 | 0.049 |
| **VGGT-Ω-1B** | **98.4** | **0.038** | **89.5** | **0.097** | **97.4** | **0.041** |
| **VGGT-Ω-10B** | **98.7** | **0.030** | **93.5** | **0.081** | **98.3** | **0.035** |

> 🌊 On Sintel (depth), VGGT-Ω-10B δ1.25 = **93.5** vs. DA3's 86.1, AbsRel = **0.081** vs. 0.118 — also **~50× faster** inference than MegaSaM.

---

#### 🤖 VLA / Robotics — LIBERO Benchmark (Success Rate % ↑)

*OpenVLA-OFT policy augmented with frozen VGGT-Ω scene tokens. 4 task suites.*

| Method | Spatial | Object | Goal | Long | **Avg** |
|---|:---:|:---:|:---:|:---:|:---:|
| Diffusion Policy | 78.3 | 92.5 | 68.3 | 50.5 | 72.4 |
| Octo | 78.9 | 85.7 | 84.6 | 51.1 | 75.1 |
| OpenVLA | 84.7 | 88.4 | 79.2 | 53.7 | 76.5 |
| pi0-FAST | 96.4 | 96.8 | 88.6 | 60.2 | 85.5 |
| pi0 | 96.8 | 98.8 | 95.8 | 85.2 | 94.2 |
| UniVLA | 96.5 | 96.8 | 95.6 | 92.0 | 95.2 |
| OpenVLA-OFT | 97.6 | 98.4 | 97.9 | 94.5 | 97.1 |
| **OpenVLA-OFT + VGGT-Ω** | **99.3** | **99.2** | **99.0** | **96.7** | **98.5** |

> 🤖 Adding frozen VGGT-Ω scene tokens to OpenVLA-OFT pushes average success rate from 97.1% to **98.5%** — new SOTA on LIBERO.

---

#### 🧠 Language Alignment (100 in-the-wild videos)

*Retrieve correct language description from register-token embeddings.*

| Setting | Top-1 Acc | Top-3 Acc |
|---|:---:|:---:|
| VLM embedding (training target) | 76.8% | 97.0% |
| Zero-shot text LLM (Qwen3) | 47.5% | 77.8% |

> 💬 Register tokens learn semantically meaningful scene representations that align with language — without any explicit language supervision during 3D training.

---

#### 🔬 Ablation Studies

**Data Scaling** (1B model, point prediction error ↓)

| Training Sequences | Point Error ↓ |
|---|:---:|
| ~2K | 0.275 |
| ~20K | 0.210 |
| ~200K | 0.160 |
| ~2M | ~0.129 |
| Full pipeline (2M+) | **0.073** |

**Model Scaling** (point prediction error ↓)

| Model Size | Point Error ↓ |
|---|:---:|
| 0.2B | 0.107 |
| ~0.5B | 0.073 |
| ~1B | 0.057 |
| ~5–10B | **0.046** |

**Architectural Ablations**

| Variant | Point Error ↓ | Notes |
|---|:---:|---|
| Full model (25% register attention) | **0.073** | Baseline |
| Global attention only | 0.071 | Nearly identical quality |
| No point & matching losses | 0.078 | +6.8% degradation |
| Self-supervised (10% SSL steps) | 0.070 | Slight gain from diversity |
| Register attention only (100%) | ~VGGT level | 6% FLOPs, but large drop |

> 💡 Replacing just **25% of global attention** with register attention saves ~23% FLOPs and ~16% memory with **no measurable quality loss**.

---

#### ⚡ Memory & Speed (Single A100 80GB, flash attention v2)

| Method | Max Frames | 1000-frame Time | Notes |
|---|:---:|:---:|---|
| DA3-Giant | ~750 frames | OOM | runs out near 750 frames |
| VGGT | ~1250 frames | — | after removing unnecessary inference cache |
| VGGT-Ω (standard) | ~1250 frames | 240.2 s | 16-px patches → ~25% fewer tokens than VGGT |
| **VGGT-Ω (register-only)** | ~1250 frames | **11.7 s** | **20.5× faster** than standard |

> 💾 VGGT-Ω uses only **~30% of VGGT's training GPU memory** — thanks to register attention, single prediction head, and MLP+pixel-shuffle replacing DPT convolutional layers.

---

#### 🏭 Annotation Pipeline Quality vs. MegaSaM (Sintel)

| Method | Camera AUC@30° | Depth δ1.25 |
|---|:---:|:---:|
| MegaSaM pseudo-GT | 62.1% | 77.2% |
| **VGGT-Ω annotation pipeline** | **96.4%** | **99.3%** |

> 🎯 The annotation pipeline is not just a training tool — it's dramatically more accurate than MegaSaM's pseudo-GT, which explains the quality leap on dynamic benchmarks.

---

### 🌐 [OmniVGGT](https://arxiv.org/abs/2511.10560) [![GitHub](https://img.shields.io/badge/GitHub-Livioni%2FOmniVGGT--official-black?logo=github&style=flat-square)](https://github.com/Livioni/OmniVGGT-official)

*Adds optional depth / intrinsics / extrinsics inputs via a lightweight GeoAdapter — truly omni-modal.*

| Input Modality | Depth Acc | Camera Pose | MVS Quality | VLA Tasks |
|---|:---:|:---:|:---:|:---:|
| RGB only | SOTA | SOTA | SOTA | ✅ |
| RGB + Depth | ↑ better | ↑ better | ↑ better | ✅ |
| RGB + Camera | — | ↑ better | ↑ better | — |
| Full multi-modal | **best** | **best** | **best** | **best** |

> 💡 Inference speed is comparable to vanilla VGGT despite the extra modalities. Outperforms point-cloud VLA baselines on robotic benchmarks.

---

### 🛡️ [RobustVGGT](https://arxiv.org/abs/2512.04012) [![GitHub](https://img.shields.io/badge/GitHub-cvlab--kaist%2FRobustVGGT-black?logo=github&style=flat-square)](https://github.com/cvlab-kaist/RobustVGGT)

*Discovers and exploits VGGT's internal ability to distinguish distractor / irrelevant views — zero fine-tuning needed.*

| Setting | Reconstruction Quality |
|---|:---:|
| VGGT (no outlier handling) | degrades with distractors |
| **RobustVGGT** (no fine-tuning) | ✅ robust across all distractor proportions |

> 🔬 A specific internal layer implicitly encodes view quality — RobustVGGT surfaces this for zero-shot outlier rejection across in-the-wild scenarios.

---

### 🔭 [HD-VGGT](https://arxiv.org/abs/2603.27222) — High-Resolution Reconstruction

*Dual-branch architecture: coarse global geometry branch + high-resolution local branch with feature upsampling.*

| Setting | Quality | Memory Cost |
|---|:---:|:---:|
| Standard VGGT | good | quadratic in resolution |
| **HD-VGGT** | **state-of-the-art** | avoids full-resolution transformer cost |

---

## 📈 Efficiency–Quality Trade-off

The diagram below illustrates the speedup–quality trade-off at **N = 1000 frames** on indoor benchmarks (higher = better quality; righter = faster).

```
 Quality
   ▲
   │  ● FlashVGGT (10.75×)    ● LiteVGGT (10×)
   │
   │               ● Co-Me (21.5×)
   │
   │         ● HTTM (7×)
   │    ● AVGGT (8–10×)
   │  ● FastVGGT (4×)
   │ ● Sparse-VGGT (2–3×)
   │                                          ● Spark3R (28×)
   └──────────────────────────────────────────────────────────► Speedup
      2×      5×       10×       15×      20×        28×
```

| Method | Speedup | Quality Drop | 🎯 Best For |
|---|:---:|:---:|:---:|
| [Spark3R](https://arxiv.org/abs/2605.06270) | 🏆 28× | small | max throughput |
| [Co-Me](https://arxiv.org/abs/2511.14751) | 21.5× | <1% | general acceleration |
| [FlashVGGT](https://arxiv.org/abs/2512.01540) | 10.75× | minimal | streaming + long-seq |
| [LiteVGGT](https://arxiv.org/abs/2512.04939) | ~10× | ~1% | high quality + fast |
| [AVGGT](https://arxiv.org/abs/2512.02541) | 8–10× | <2% | large-scale scenes |
| [HTTM](https://arxiv.org/abs/2511.21317) | 7× | negligible | long indoor sequences |
| [FastVGGT](https://arxiv.org/abs/2509.02560) | ~4× | negligible | simplest drop-in |
| [Sparse-VGGT](https://arxiv.org/abs/2509.07120) | 2–3× | <3pts RRA/RTA | cross-model (VGGT+pi3) |

---

## 📝 Notes

**🖥️ Hardware environments** vary across papers — speedup numbers are not directly comparable:
- NVIDIA A100 / H100 / H20: FastVGGT, HTTM, Co-Me, LiteVGGT
- NVIDIA A800: StreamVGGT
- RTX 4090: QuantVGGT
- Edge GPU targets: VersaQ-3D

**🔖 VGGT\*** refers to the chunked VGGT baseline (frames processed in overlapping windows to avoid OOM), **not** vanilla VGGT.

**💥 OOM at 1000 frames:** vanilla VGGT, Fast3R, CUT3R. VGGT\* (chunked) survives but is very slow.

**📚 Common baseline stack** across papers: `VGGT → pi3 → DUSt3R → MAST3R → CUT3R → Fast3R → Spann3R`

**⚠️ Speedup figures are not directly comparable** across papers — different hardware, sequence lengths, batch sizes, and whether FlashAttention / BFloat16 is applied to the baseline all affect numbers. Always use per-paper tables for cross-method comparison.

**🏆 Accepted venues in this list:**
- ![CVPR 2026](https://img.shields.io/badge/CVPR-2026-blue.svg?style=flat-square) Sparse-VGGT, FlashVGGT, VGG-T³, VGGT-Ω (Oral)
- ![ICLR 2026](https://img.shields.io/badge/ICLR-2026-green.svg?style=flat-square) QuantVGGT, TTT3R
- ![ICRA 2026](https://img.shields.io/badge/ICRA-2026-orange.svg?style=flat-square) VGGT-Long

---

*📅 Last updated: 2026-06-22 · Pull requests adding new evaluation results are warmly welcome — please follow the existing table format and include a link to the source paper. 🙏*
