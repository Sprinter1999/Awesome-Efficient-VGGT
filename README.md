# Awesome-Efficient-VGGT

A curated list of efficient methods for **Visual Geometry Grounded Transformer (VGGT)**, covering token reduction, sparse attention, model compression, quantization, and test-time training.

## Introduction

**Feed-forward 3D reconstruction** predicts 3D geometry and camera information directly from input images through a neural network forward pass, reducing the reliance on costly per-scene optimization in traditional reconstruction pipelines. For a broader collection of works in this direction, please refer to [Awesome-Feed-Forward-3D](https://github.com/ziplab/Awesome-Feed-Forward-3D).

[**VGGT**](https://arxiv.org/abs/2503.11651) is a representative feed-forward 3D model that directly predicts camera parameters, depth maps, point maps, and 3D point tracks from one or multiple input views. Since its global attention becomes computationally expensive as the number of visual tokens grows, recent studies explore efficient VGGT inference through token reduction, sparse attention, compact architectures, quantization, and test-time training. We also recommend some classic related works which also focus on the efficient feed-forward 3D.

| Method | Paper | Paper Link | GitHub Repo |
|---|---|---|---|
| VGGT | VGGT: Visual Geometry Grounded Transformer | [Paper](https://arxiv.org/abs/2503.11651) | [Code](https://github.com/facebookresearch/vggt) |

## Taxonomy

- **Training-free Approach**: Methods applied to pretrained VGGT without training additional parameters.
- **Training-aware Approach**: Methods requiring auxiliary-module training, distillation, fine-tuning, or training a new efficient architecture.
- **Test-Time Training Approach**: Methods that adapt the model at inference time via lightweight self-supervised optimization, without offline training of additional modules.
- **Quantization Approach**: Methods reducing numerical precision for efficient VGGT deployment.
- **VGGT-native Extensions**: Related extensions to VGGT.
## Training-free Approach

| Method | Paper | Paper Link | GitHub Repo |
|---|---|---|---|
| VGGT-Long | VGGT-Long: Chunk it, Loop it, Align it — Pushing VGGT's Limits on Kilometer-scale Long RGB Sequences | [Paper](https://arxiv.org/abs/2507.16443) | [Code](https://github.com/DengKaiCQ/VGGT-Long) |
| FastVGGT | FastVGGT: Training-Free Acceleration of Visual Geometry Transformer | [Paper](https://arxiv.org/abs/2509.02560) | [Code](https://github.com/mystorm16/FastVGGT) |
| Sparse-VGGT | Block-Sparse Global Attention for Efficient Multi-View Geometry Transformers | [Paper](https://arxiv.org/abs/2509.07120) | [Code](https://github.com/brianwang00001/sparse-vggt) |
| SwiftVGGT | SwiftVGGT: A Scalable Visual Geometry Grounded Transformer for Large-Scale Scenes | [Paper](https://arxiv.org/abs/2511.18290) | - |
| HTTM | HTTM: Head-wise Temporal Token Merging for Faster VGGT | [Paper](https://arxiv.org/abs/2511.21317) | - |
| AVGGT | AVGGT: Rethinking Global Attention for Accelerating VGGT | [Paper](https://arxiv.org/abs/2512.02541) | - |
| LiteVGGT | LiteVGGT: Boosting Vanilla VGGT via Geometry-aware Cached Token Merging | [Paper](https://arxiv.org/abs/2512.04939) | [Code](https://github.com/GarlicBa/LiteVGGT-repo) |
| XStreamVGGT | XStreamVGGT: Extremely Memory-Efficient Streaming Vision Geometry Grounded Transformer with KV Cache Compression | [Paper](https://arxiv.org/abs/2601.01204) | [Code](https://github.com/ywh187/XStreamVGGT/) |
| Spark3R | Spark3R: Asymmetric Token Reduction Makes Fast Feed-Forward 3D Reconstruction | [Paper](https://arxiv.org/abs/2605.06270) | - |
| RetrieveVGGT | Attention Itself Could Retrieve: Training-Free Long Context Streaming 3D Reconstruction via Query-Key Similarity Retrieval | [Paper](https://arxiv.org/abs/2605.09644) | - |
| RegimeVGGT | RegimeVGGT: Layer-Wise Spatially Preserving Redundancy Removal for Visual Geometry Grounded Transformer | [Paper](https://arxiv.org/abs/2606.18439) | - |
| DiversityVP | Diversity-aware View Partitioning for Scalable VGGT | [Paper](https://arxiv.org/abs/2607.01885) | - |

## Training-aware Approach

| Method | Paper | Paper Link | GitHub Repo |
|--|---|---|---|
| StreamVGGT | Streaming 4D Visual Geometry Transformer | [Paper](https://arxiv.org/abs/2507.11539) | [Code](https://github.com/wzzheng/StreamVGGT) |
| eVGGT | Improving Robotic Manipulation with Efficient Geometry-Aware Vision Encoder | [Paper](https://arxiv.org/abs/2509.15880) | [Code](https://github.com/andvg3/eVGGT) |
| Co-Me | Co-Me: Confidence-Guided Token Merging for Visual Geometric Transformers | [Paper](https://arxiv.org/abs/2511.14751) | [Code](https://github.com/co-me-tokens/CoMe) |
| FlashVGGT | FlashVGGT: Efficient and Scalable Visual Geometry Transformers with Compressed Descriptor Attention | [Paper](https://arxiv.org/abs/2512.01540) | - |
| PaceVGGT | PaceVGGT: Pre-Alternating-Attention Token Pruning for Visual Geometry Transformers | [Paper](https://arxiv.org/abs/2605.08371) | - |
| Lite3R | Lite3R: A Model-Agnostic Framework for Efficient Feed-Forward 3D Reconstruction | [Paper](https://arxiv.org/abs/2605.11354) | [Code](https://github.com/AIGeeksGroup/Lite3R) |
| TurboVGGT | TurboVGGT: Fast Visual Geometry Reconstruction with Adaptive Alternating Attention | [Paper](https://arxiv.org/abs/2605.14315) | - |
| D4RT | Efficiently Reconstructing Dynamic Scenes One D4RT at a Time | [Paper](https://arxiv.org/pdf/2512.08924) | - |
| Mamba-VGGT | Mamba-VGGT: Persistent Long-Sequence Video Geometry Grounded Transformer via External Sliding Window Mamba Memory | [Paper](https://arxiv.org/abs/2605.17478) | - |

> **Note:** Co-Me keeps the base model frozen, but is categorized as training-aware because it distills a lightweight confidence predictor. StreamVGGT is categorized as training-aware because it distills a causal architecture from VGGT.

## Test-Time Training Approach

| Method | Paper | Paper Link | GitHub Repo |
|---|---|---|---|
| Test3R | Test3R: Learning to Reconstruct 3D at Test Time | [Paper](https://arxiv.org/abs/2506.13750) | [Code](https://github.com/nopQAQ/Test3R) |
| TTT3R | TTT3R: 3D Reconstruction as Test-Time Training | [Paper](https://arxiv.org/abs/2509.26645) | [Code](https://github.com/Inception3D/TTT3R) |
| VGG-T³ | VGG-T³: Offline Feed-Forward 3D Reconstruction at Scale | [Paper](https://arxiv.org/abs/2602.23361) | - |

> **Note:** Test3R optimizes visual prompt tokens at test time via cross-pair geometric consistency (backbone frozen). TTT3R is a training-free intervention that reframes recurrent state updates as online learning. VGG-T³ replaces global softmax attention with a TTT-based MLP that distills the KV space, achieving O(N) complexity and 11.6× speedup over standard VGGT (CVPR 2026).

> **TTT--Pruning Synergy (Hypothesis):** Test-time training methods offer a complementary direction to token pruning. Pruning reduces the token count spatially (e.g., FastVGGT, LiteVGGT, RegimeVGGT), while TTT methods optimize the remaining computation: VGG-T³ distills global attention KV space into a fixed-size MLP via test-time training, achieving O(N) complexity and 11.6× speedup (CVPR 2026). TTT3R provides a training-free intervention for recurrent 3D models via closed-form memory updates. We hypothesize that combining spatial pruning with TTT optimization (prune first, then apply TTT on the compact token set) could yield greater efficiency gains than either approach alone, and is a promising open direction for future work, particularly on VGGT-Ω where the register-compressed token bottleneck provides a natural target for TTT optimization.

## Quantization Approach

| Method | Paper | Paper Link | GitHub Repo |
|---|---|---|---|
| QuantVGGT | Quantized Visual Geometry Grounded Transformer | [Paper](https://arxiv.org/abs/2509.21302) | [Code](https://github.com/wlfeng0509/QuantVGGT) |
| VersaQ-3D | VersaQ-3D: A Reconfigurable Accelerator Enabling Feed-Forward and Generalizable 3D Reconstruction via Versatile Quantization | [Paper](https://arxiv.org/abs/2601.20317) | - |
| TAPTQ | Tail-Aware Post-Training Quantization for 3D Geometry Models | [Paper](https://arxiv.org/abs/2602.01741) | - |
| FGQ | Not All Tasks Quantize Equally: Fisher-Guided Quantization for Visual Geometry Transformer | [Paper](https://arxiv.org/abs/2605.15828) | [Code](https://github.com/ypzhng/FGQ) |
| QVGGT | QVGGT: Post-Training Quantized Visual Geometry Grounded Transformer | [Paper](https://arxiv.org/abs/2605.31124) | - |


## VGGT-native Extensions

| Method | Paper | Paper Link | GitHub Repo |
|---|---|---|---|
| VGGT-Ω | VGGT-Ω | [Paper](https://arxiv.org/abs/2605.15195) | [Code](https://github.com/facebookresearch/vggt-omega) |
| HD-VGGT | HD-VGGT: High-Resolution Visual Geometry Transformer | [Paper](https://arxiv.org/abs/2603.27222) | - |
| RobustVGGT | Emergent Outlier View Rejection in Visual Geometry Grounded Transformers | [Paper](https://arxiv.org/abs/2512.04012) | [Code](https://github.com/cvlab-kaist/RobustVGGT) |
| OmniVGGT | OmniVGGT: Omni-Modality Driven Visual Geometry Grounded | [Paper](https://arxiv.org/abs/2511.10560) | [Code](https://github.com/Livioni/OmniVGGT-official) |
| VGGT-Occ | VGGT-Occ: Geometry-Grounded and Density-Aware Gated Fusion for 3D Occupancy Prediction | [Paper](https://arxiv.org/abs/2605.16911) | - |
| VGGT-CD | VGGT-CD: Training-Free Robust Registration for 3D Change Detection | [Paper](https://arxiv.org/abs/2605.16859) | - |
| VGGT-Edit | VGGT-Edit: Feed-forward Native 3D Scene Editing with Residual Field Prediction | [Paper](https://arxiv.org/abs/2605.15186) | - |

## 

## Contributing

Pull requests are welcome. Please provide the method name, paper title, paper link, GitHub repository if available, and taxonomy category.
