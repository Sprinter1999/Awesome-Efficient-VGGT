# Awesome-Efficient-VGGT

A curated list of efficient methods for **Visual Geometry Grounded Transformer (VGGT)**, covering token reduction, sparse attention, model compression, and quantization.

## Introduction

**Feed-forward 3D reconstruction** predicts 3D geometry and camera information directly from input images through a neural network forward pass, reducing the reliance on costly per-scene optimization in traditional reconstruction pipelines. For a broader collection of works in this direction, please refer to [Awesome-Feed-Forward-3D](https://github.com/ziplab/Awesome-Feed-Forward-3D).

[**VGGT**](https://arxiv.org/abs/2503.11651) is a representative feed-forward 3D model that directly predicts camera parameters, depth maps, point maps, and 3D point tracks from one or multiple input views. Since its global attention becomes computationally expensive as the number of visual tokens grows, recent studies explore efficient VGGT inference through token reduction, sparse attention, compact architectures, and quantization. We also recommend some classic related works which also focus on the efficient feed-forward 3D.

| Method | Paper | Paper Link | GitHub Repo |
|---|---|---|---|
| VGGT | VGGT: Visual Geometry Grounded Transformer | [Paper](https://arxiv.org/abs/2503.11651) | [Code](https://github.com/facebookresearch/vggt) |

## Taxonomy

- **Training-free Approach**: Methods applied to pretrained VGGT without training additional parameters.
- **Training-aware Approach**: Methods requiring auxiliary-module training, distillation, fine-tuning, or training a new efficient architecture.
- **Quantization Approach**: Methods reducing numerical precision for efficient VGGT deployment.

## Training-free Approach

| Method | Paper | Paper Link | GitHub Repo |
|---|---|---|---|
| FastVGGT | FastVGGT: Training-Free Acceleration of Visual Geometry Transformer | [Paper](https://arxiv.org/abs/2509.02560) | [Code](https://github.com/mystorm16/FastVGGT) |
| Sparse-VGGT | Block-Sparse Global Attention for Efficient Multi-View Geometry Transformers | [Paper](https://arxiv.org/abs/2509.07120) | [Code](https://github.com/brianwang00001/sparse-vggt) |
| HTTM | HTTM: Head-wise Temporal Token Merging for Faster VGGT | [Paper](https://arxiv.org/abs/2511.21317) | - |
| AVGGT | AVGGT: Rethinking Global Attention for Accelerating VGGT | [Paper](https://arxiv.org/abs/2512.02541) | - |
| LiteVGGT | LiteVGGT: Boosting Vanilla VGGT via Geometry-aware Cached Token Merging | [Paper](https://arxiv.org/abs/2512.04939) | [Code](https://github.com/GarlicBa/LiteVGGT-repo) |
| Spark3R | Spark3R: Asymmetric Token Reduction Makes Fast Feed-Forward 3D Reconstruction | [Paper](https://arxiv.org/abs/2605.06270) | - |

## Training-aware Approach

| Method | Paper | Paper Link | GitHub Repo |
|---|---|---|---|
| eVGGT | Improving Robotic Manipulation with Efficient Geometry-Aware Vision Encoder | [Paper](https://arxiv.org/abs/2509.15880) | [Code](https://github.com/andvg3/eVGGT) |
| Co-Me | Co-Me: Confidence-Guided Token Merging for Visual Geometric Transformers | [Paper](https://arxiv.org/abs/2511.14751) | [Code](https://github.com/co-me-tokens/CoMe) |
| FlashVGGT | FlashVGGT: Efficient and Scalable Visual Geometry Transformers with Compressed Descriptor Attention | [Paper](https://arxiv.org/abs/2512.01540) | - |
| PaceVGGT | PaceVGGT: Pre-Alternating-Attention Token Pruning for Visual Geometry Transformers | [Paper](https://arxiv.org/abs/2605.08371) | - |
| Lite3R | Lite3R: A Model-Agnostic Framework for Efficient Feed-Forward 3D Reconstruction | [Paper](https://arxiv.org/abs/2605.11354) | [Code](https://github.com/AIGeeksGroup/Lite3R) |
| TurboVGGT | TurboVGGT: Fast Visual Geometry Reconstruction with Adaptive Alternating Attention | [Paper](https://arxiv.org/abs/2605.14315) | - |

> **Note:** Co-Me keeps the base model frozen, but is categorized as training-aware because it distills a lightweight confidence predictor.

## Quantization Approach

| Method | Paper | Paper Link | GitHub Repo |
|---|---|---|---|
| QuantVGGT | Quantized Visual Geometry Grounded Transformer | [Paper](https://arxiv.org/abs/2509.21302) | [Code](https://github.com/wlfeng0509/QuantVGGT) |
| VersaQ-3D | VersaQ-3D: A Reconfigurable Accelerator Enabling Feed-Forward and Generalizable 3D Reconstruction via Versatile Quantization | [Paper](https://arxiv.org/abs/2601.20317) | - |
| TAPTQ | Tail-Aware Post-Training Quantization for 3D Geometry Models | [Paper](https://arxiv.org/abs/2602.01741) | - |
| FGQ | Not All Tasks Quantize Equally: Fisher-Guided Quantization for Visual Geometry Transformer | [Paper](https://arxiv.org/abs/2605.15828) | [Code](https://github.com/ypzhng/FGQ) |

## Contributing

Pull requests are welcome. Please provide the method name, paper title, paper link, GitHub repository if available, and taxonomy category.
