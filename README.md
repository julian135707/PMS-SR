# PMS-SR: Progressive Multi-Scale Super-Resolution via Cascaded Bicubic Anchors and Inter-Scale Mutual Refinement

[Chun-An Lin](https://orcid.org/0009-0004-8874-6196), Yu-Chia Chang, Chi-Mao Fan, [Yen-Chieh Ouyang](https://orcid.org/0000-0002-4221-2787), [Tsung-Jung Liu](https://orcid.org/0000-0003-4296-0942)

National Chung Hsing University · Providence University · ASUSTeK Computer Inc., Taiwan

[![arXiv](https://img.shields.io/badge/arXiv-2611.03390-b31b1b.svg)](https://arxiv.org/abs/2611.03390)
[![Status](https://img.shields.io/badge/IEEE%20-under%20review-blue.svg)]()
[![Code](https://img.shields.io/badge/code-released%20upon%20acceptance-lightgrey.svg)]()

One 7.95M-parameter model produces the ×2, ×4, and ×8 results of an input in a single forward pass. Among multi-scale methods, it has the highest PSNR in every ×4 and ×8 entry on all five standard benchmarks. It also outperforms the ×8-specific DRN-L on all five benchmarks and gives the best ×8 Urban100 result among all compared methods.

![Graphical abstract](assets/graphical_abstract.png)

## At a glance

| | Result |
|---|---|
| **×4 vs. multi-scale methods** | Best PSNR and SSIM on all 5 benchmarks (+0.06 to +0.36 dB PSNR over the runner-up) |
| **×8 vs. multi-scale methods** | Best PSNR on all 5 benchmarks (+0.08 to +0.32 dB over the runner-up) and best SSIM on 4 of 5 |
| **vs. ProSR-L, the strongest multi-scale baseline** | About half the parameters (7.95M vs. 15.50M), with higher PSNR in every ×4 and ×8 entry |
| **vs. three SwinIR-M models** | 22% of the parameters and 2.9× faster (32.8 ms vs. 94.4 ms) |

## Comparison with multi-scale methods

Multi-scale methods address the same task as PMS-SR: one model serves several magnification factors. Values are Y-channel PSNR / SSIM, and bold marks the best value in each column.

### ×8

| Method | Params | Set5 | Set14 | BSD100 | Urban100 | Manga109 |
|---|---|---|---|---|---|---|
| LapSRN | 1.31M | 26.14 / 0.738 | 24.44 / 0.623 | 24.54 / 0.586 | 21.81 / 0.581 | 23.39 / 0.735 |
| MS-LapSRN | 0.22M | 26.34 / 0.753 | 24.57 / 0.629 | 24.65 / 0.592 | 22.06 / 0.598 | 23.90 / 0.759 |
| MSWSR | 1.23M | 26.76 / 0.7631&dagger; | 24.82 / 0.6338 | 24.74 / 0.5914 | 22.30 / 0.6045 | 24.21 / 0.7609 |
| MLWAN | 1.23M | 26.89 / 0.7732 | 24.97 / **0.6574** | 24.81 / 0.5969 | 22.95 / 0.6371 | 24.51 / 0.7833 |
| ProSR-L | 15.50M | 27.35 / 0.7885&dagger; | 25.29 / 0.652 | 24.99 / 0.606 | 23.04 / 0.645 | 25.29 / 0.8045&dagger; |
| **PMS-SR (ours)** | **7.95M** | **27.49** / **0.7922** | **25.37** / 0.6551 | **25.07** / **0.6094** | **23.36** / **0.6593** | **25.58** / **0.8129** |

### ×4

| Method | Params | Set5 | Set14 | BSD100 | Urban100 | Manga109 |
|---|---|---|---|---|---|---|
| LapSRN | 1.31M | 31.54 / 0.885 | 28.19 / 0.772 | 27.32 / 0.728 | 25.21 / 0.756 | 29.09 / 0.890 |
| MS-LapSRN | 0.22M | 31.74 / 0.889 | 28.26 / 0.774 | 27.43 / 0.731 | 25.51 / 0.768 | 29.54 / 0.897 |
| MSWSR | 1.23M | 32.00 / 0.8913&dagger; | 28.47 / 0.7776 | 27.48 / 0.7311 | 25.78 / 0.7744 | 30.01 / 0.8999 |
| MLWAN | 1.23M | 32.19 / 0.8957 | 28.55 / 0.7797 | 27.67 / 0.7429 | 25.89 / 0.7779 | 30.16 / 0.9110 |
| MDSR | 8.00M | 32.50 / 0.8973 | 28.72 / 0.7857 | 27.72 / 0.7418 | 26.67 / 0.8041 | 31.04 / 0.9145&dagger; |
| ProSR-L | 15.50M | 32.53 / 0.8991&dagger; | 28.94 / 0.790 | 27.79 / 0.743 | 26.89 / 0.809 | 31.39 / 0.9181&dagger; |
| **PMS-SR (ours)** | **7.95M** | **32.72** / **0.9012** | **29.00** / **0.7915** | **27.87** / **0.7464** | **27.25** / **0.8177** | **31.69** / **0.9222** |

### ×2

At ×2, PMS-SR gives the best Urban100 result and is within 0.05 dB of the 15.50M ProSR-L on Set5, Set14, and BSD100. On Manga109, ProSR-L and MDSR are 0.18 and 0.17 dB ahead.

<details>
<summary>Show the ×2 table</summary>

| Method | Params | Set5 | Set14 | BSD100 | Urban100 | Manga109 |
|---|---|---|---|---|---|---|
| LapSRN | 1.31M | 37.52 / 0.959 | 33.08 / 0.913 | 31.80 / 0.895 | 30.41 / 0.910 | 37.27 / 0.974 |
| MS-LapSRN | 0.22M | 37.78 / 0.960 | 33.28 / 0.915 | 32.05 / 0.898 | 31.15 / 0.919 | 37.78 / 0.976 |
| MSWSR | 1.23M | 37.49 / 0.9582&dagger; | 33.23 / 0.9123 | 31.88 / 0.8929 | 31.14 / 0.9169 | 37.32 / 0.9733 |
| MLWAN | 1.23M | 37.68 / 0.9589 | 33.47 / **0.9227** | 31.96 / 0.8974 | 31.34 / 0.9309 | 37.39 / 0.9733 |
| MDSR | 8.00M | 38.11 / 0.9602 | 33.85 / 0.9198 | 32.29 / 0.9007 | 32.84 / 0.9347 | 39.09 / **0.9779**&dagger; |
| ProSR-L | 15.50M | **38.17** / 0.9608&dagger; | **34.00** / 0.921 | **32.34** / **0.902** | 32.91 / 0.935 | **39.10** / 0.9777&dagger; |
| **PMS-SR (ours)** | **7.95M** | 38.16 / **0.9611** | 33.95 / 0.9200 | 32.31 / 0.9002 | **33.03** / **0.9366** | 38.92 / 0.9777 |

</details>

<sub>&dagger;Measured by us from the authors' released weights to fill an unpublished entry; other baseline values are published results. MDSR does not support ×8. PMS-SR is trained on DF2K, and a DIV2K-only control in the paper separates the effect of the training data from that of the architecture.</sub>

## One network instead of a three-model ladder

| | Three SwinIR-M models | PMS-SR |
|---|---|---|
| Models / forward passes | 3 / 3 | **1 / 1** |
| Parameters | 35.70M | **7.95M** |
| Runtime for all three outputs | 94.4 ms | **32.8 ms** |
| Agreement, ×8→×4 | 34.5–42.5 dB | **45.6–52.4 dB** |
| Agreement, ×4→×2 | 38.3–44.3 dB | **45.5–50.9 dB** |

<sub>Whole-image inference on an RTX 4090, averaged over the 100 BSD100 ×8 LR inputs (about 60×40). Agreement ranges cover the five benchmarks; the paper reports them together with degenerate controls.</sub>

![Mean x8 PSNR vs. parameters needed for x2/x4/x8](assets/ladder_scatter_x8_mean.png)

<sub>Single-scale methods count as three models; where only one size is reported, it is tripled (values from the paper's Tables I and III).</sub>

## Highlights

- **One pass, three outputs.** A single forward pass delivers ×2, ×4, and ×8.
- **Cascaded bicubic anchors.** Each scale is a residual over the detached bicubic upsampling of the previous scale's prediction. With Dirac and zero initialization, training starts exactly from the bicubic cascade. Replacing the cascade with a direct anchor costs 2.4 dB at ×8 on BSD100.
- **Inter-scale mutual refinement (IMR).** Space-to-depth feedback, deformable cross-scale alignment, and per-pixel fusion let the scales exchange information in both directions, so ×8 features also refine the ×2 output. The whole ×8 refinement runs on the ×4 grid.

## Visual results

Urban100 img_043, ×8 (+1.45 dB over the best baseline):

![Urban100 x8](assets/qual_urban100_x8.png)

Manga109 *YukiNoFuruMachi*, ×8:

![Manga109 x8](assets/qual_manga109_x8.png)

Urban100 img_052, ×4:

![Urban100 x4](assets/qual_urban100_x4.png)

## Reference comparison with single-scale models

Single-scale models are trained for one factor each, so a ladder of them needs at least 4.5× the parameters of PMS-SR. At ×8, PMS-SR outperforms DRN-L on all five benchmarks and leads all compared models on Urban100. Elsewhere, the strongest ×8-specific models are ahead by at most 0.13 dB. At ×2 and ×4, SwinIR-M remains ahead by up to 1.00 and 0.34 dB, respectively.

<details>
<summary>Show the ×8 table and the SwinIR-M gaps</summary>

| Method | Params | Set5 | Set14 | BSD100 | Urban100 | Manga109 |
|---|---|---|---|---|---|---|
| RCAN | 15.7M | 27.31 / 0.7878 | 25.23 / 0.6511 | 24.98 / 0.6058 | 23.00 / 0.6452 | 25.24 / 0.8029 |
| DRN-L&dagger; | 10.0M | 27.42 / 0.7920 | 25.28 / 0.6528 | 25.01 / 0.6059 | 22.98 / 0.6434 | 25.32 / 0.8060 |
| DBPN-RES-MR64-3 | 23.1M | 27.51 / 0.793 | 25.41 / **0.657** | 25.05 / 0.607 | 23.20 / 0.652 | **25.71** / 0.813 |
| SwinIR-M | 12.1M | **27.55** / 0.7941 | **25.46** / 0.6568 | 25.04 / 0.6092 | 23.17 / 0.6547 | 25.55 / **0.8132** |
| RDRN | ≈36.4M | 27.52 / **0.7953** | 25.40 / 0.6548 | **25.10** / 0.6084 | 23.20 / 0.6511 | 25.66 / 0.8114 |
| **PMS-SR (one pass)** | 7.95M* | 27.49 / 0.7922 | 25.37 / 0.6551 | 25.07 / **0.6094** | **23.36** / **0.6593** | 25.58 / 0.8129 |

PSNR gap to SwinIR-M (dB):

| Benchmark | ×2 | ×4 | ×8 |
|---|---|---|---|
| Set5 | −0.26 | −0.20 | −0.06 |
| Set14 | −0.51 | −0.09 | −0.09 |
| BSD100 | −0.22 | −0.05 | **+0.03** |
| Urban100 | −0.78 | −0.20 | **+0.19** |
| Manga109 | −1.00 | −0.34 | **+0.03** |
| Average | −0.55 | −0.18 | **+0.02** |

<sub>*One model covers all three factors. &dagger;Measured by us from the officially released weights under the same protocol; all other rows are published results (SwinIR-M ×8 from its supplementary material; RDRN size reported for its ×4 model). At ×8, only the Urban100 difference from SwinIR-M is statistically significant in our paired per-image test.</sub>

</details>

## Evaluation protocol

- MATLAB-bicubic degradation; Y-channel PSNR/SSIM with a border of *s* pixels removed at scale *s*.
- Baselines with released weights (SwinIR-M, RCAN, DRN-L, MDSR, MSWSR, ProSR-L) were re-evaluated under the same protocol.
- Paired per-image Wilcoxon signed-rank tests with Holm correction are reported where PMS-SR loses as well as where it wins.
- A DIV2K-only control with one third of the schedule separates the effect of the architecture from that of the training data.

## Code and models

The training and evaluation code and the pretrained weights will be released in this repository after the paper is accepted.

## Citation

```bibtex
@article{lin2026progressive,
  title={Progressive Multi-Scale Super-Resolution via Cascaded Bicubic Anchors and Inter-Scale Mutual Refinement},
  author={Lin, Chun-An and Chang, Yu-Chia and Fan, Chi-Mao and Ouyang, Yen-Chieh and Liu, Tsung-Jung},
  journal={arXiv preprint arXiv:2611.03390},
  year={2026}
}
```

## Acknowledgment

This work was supported in part by the National Science and Technology Council, Taiwan, under Grant NSTC 114-2221-E-005-040-MY2.
