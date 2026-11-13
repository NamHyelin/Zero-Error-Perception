# Zero-Error Perception

**Zero Perception Error Rate-Distortion for Semantic Communication**

This repository brings together the research overview, study materials, and a small numerical illustration associated with our work on zero perception error (ZEPE) in semantic communication.

The focus is on formulating rate-perception-distortion tradeoff with given semantic latent variables.

[![Python](https://img.shields.io/badge/Python-262139?style=for-the-badge&logo=python&logoColor=F472B6)](#)
[![Information Theory](https://img.shields.io/badge/Information_Theory-202C49?style=for-the-badge&logoColor=79B8FF)](#)

---

## Publication

**Zero Perception Error Rate-Distortion for Semantic Communication**

J. Choi, **H. Nam**, J. Park, S.-W. Ko, and S.-L. Kim

*Proc. of the 61st Allerton Conference on Communication, Control, and Computing, 2025.*


[![IEEE Paper](https://img.shields.io/badge/IEEE-Paper-252341?style=for-the-badge&logo=ieee&logoColor=A78BFA)](https://www.ideals.illinois.edu/items/137322)
[![Google Scholar](https://img.shields.io/badge/Google_Scholar-202C49?style=for-the-badge&logo=googlescholar&logoColor=79B8FF)](https://scholar.google.com/citations?view_op=view_citation&hl=ko&user=KTjNYtAAAAAJ&sortby=pubdate&citation_for_view=KTjNYtAAAAAJ:WF5omc3nYNoC)


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

The [ZEPE.pdf](ZEPE.pdf) is reserved for presentations and reading notes developed while studying the theoretical background of this work.

---

## Experiment implementation

The python code [ZEPE.ipynb](ZEPE.ipynb), implements the six-symbol setting from example:

$$
\mathcal{X}=\mathcal{Y}=\{1,2,3,4,5,6\},
\qquad P_X(x)=\frac{x}{21},
\qquad d(x,y)=\frac{2}{5}(x-y)^2.
$$



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

