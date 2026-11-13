# Zero-Error Perception

**Zero Perception Error Rate-Distortion for Semantic Communication**

This repository brings together the research overview, study materials, and a small numerical illustration associated with our work on zero perception error (ZEPE) in semantic communication.

The focus is on understanding how distribution-preserving reconstruction changes the rate-distortion tradeoff and how this perspective extends to semantic sources with latent variables.

---

## Publication

J. Choi, H. Nam, J. Park, S.-W. Ko, and S.-L. Kim, “Zero Perception Error Rate-Distortion for Semantic Communication,” to be presented at, and to appear in Proc. of the 61st Allerton Conference on Communication, Control, and Computing, 2025.

---

## Overview

### Distortion and Perception

Distortion measures the difference between an individual source sample and its reconstruction. Perception instead compares the distributions of the source and reconstructed signals.

A reconstruction can have small sample distortion while its distribution differs from the source. Conversely, matching the source distribution does not guarantee that each reconstructed sample matches its original input.

### Zero Perception Error

ZEPE requires the reconstructed distribution to equal the source distribution:

$$
Q_Y(y) = P_X(y).
$$

Under this constraint, the rate-distortion problem becomes

$$
R_{\mathrm{ZEPE}}(D)
=
\min_{Q(y\mid x)} I(X;Y)
\quad
\text{subject to }
\mathbb{E}[d(X,Y)]\leq D,
\quad Q_Y=P_X.
$$

Preserving the distribution can require a higher rate than conventional rate-distortion coding at the same distortion. If sufficient distortion is allowed, independent sampling from the source distribution achieves ZEPE at zero rate.

### Semantic Sources and Generative Reconstruction

The paper extends this perspective to an inferred latent variable that represents the source semantics. The reconstruction preserves the source distribution conditioned on that latent variable, while additional transmitted information can improve sample fidelity.

The paper also discusses generative reconstruction using variational autoencoders and its relationship to hybrid semantic-classical communication.

---

## Study Materials

The [slides folder](slides/) is reserved for presentations and reading notes developed while studying the theoretical background of this work.

Suggested topics include:

- Classical rate-distortion theory.
- The distinction between sample distortion and distribution-level perception.
- The ZEPE constraint and optimal reconstruction distributions.
- Semantic sources, latent variables, and generative reconstruction.

Presentation files will be added separately. The numerical example below is included in this repository package.

---

## Numerical Illustration: Fig. 1

The single-file example, [fig1.py](fig1.py), implements the six-symbol setting from Example 1:

$$
\mathcal{X}=\mathcal{Y}=\{1,2,3,4,5,6\},
\qquad P_X(x)=\frac{x}{21},
\qquad d(x,y)=\frac{2}{5}(x-y)^2.
$$

It compares conventional and ZEPE rate-distortion curves and computes the perception error as $D_{\mathrm{KL}}(P_X\Vert Q_Y)$.

![Conventional and ZEPE rate-distortion curves](figures/fig1.png)

The conventional solution uses Blahut-Arimoto iteration. The ZEPE solution scales a symmetric joint probability matrix so that both marginals equal the source distribution.

### Getting Started

Install the two dependencies:

```bash
pip install numpy matplotlib
```

Run the example:

```bash
python fig1.py
```

No training, dataset download, GPU, or configuration file is required. To explore other settings, edit the source values, source probabilities, distortion matrix, or multiplier range at the top of `fig1.py`. The ZEPE routine assumes a symmetric distortion matrix and identical input/output alphabets.

The script saves:

| File | Contents |
| :--- | :--- |
| `figures/fig1.png` | Rate-distortion and KL-divergence plots. |
| `figures/conventional.csv` | Conventional distortion, rate, and KL values. |
| `figures/zepe.csv` | ZEPE distortion, rate, and KL values. |

### Reading the Results

The ZEPE constraint increases the required rate at a fixed distortion, while maintaining a KL divergence numerically equal to zero.

For this example, the zero-rate distortion is approximately **0.9333** for conventional reconstruction and **1.7778** for ZEPE reconstruction. At zero distortion, both rates equal the source entropy, approximately **1.6624 nats per source symbol**.

### Numerical Scope

This script is an independent numerical illustration of the optimization problem and Example 1, rather than the original plotting code. All logarithms are natural; divide rates by `np.log(2)` to express them in bits.

Equations (8)-(9), read literally without an input-dependent normalization factor, do not generally yield a conditional probability whose rows sum to one. The implementation therefore enforces both probability normalization and the ZEPE marginal constraint through matrix scaling.

The conventional KL curve is sensitive to tiny output probabilities and iteration tolerance. If an output probability is exactly zero while the corresponding source probability is positive, the KL divergence is infinite. The code records this as `inf` and omits infinite values from the plotted line; it does not replace zero probabilities with an arbitrary floor. Large finite KL values from near-zero probabilities should not be interpreted as precise theoretical values.

The figure uses two panels, a symmetric-log KL axis, and the complete zero-rate endpoints for clarity. Its numerical KL values and layout are not intended to match the paper's Fig. 1 pixel for pixel.

---

## Repository Contents

| Path | Purpose |
| :--- | :--- |
| `README.md` | Research overview and experiment guide. |
| `slides/` | Presentation materials and reading notes, to be added. |
| `fig1.py` | Standalone numerical illustration. |
| `figures/` | Generated plot and numerical data. |

---

## Citation

```bibtex
@inproceedings{choi2025zero,
  title     = {Zero Perception Error Rate-Distortion for Semantic Communication},
  author    = {Choi, Jinho and Nam, Hyelin and Park, Jihong
               and Ko, Seung-Woo and Kim, Seong-Lyun},
  booktitle = {61st Allerton Conference on Communication, Control, and Computing},
  year      = {2025},
  note      = {To be presented and to appear in the proceedings}
}
```

