# MNIST CNN & Grad-CAM++ (Google Colab)

[日本語版](README_ja.md)

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/TakaNori999/cnn_grad-cam_mnist/blob/main/MNIST_CNN_GradCAMpp_Colab.ipynb)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23992469.svg)](https://doi.org/10.5281/zenodo.23992469)

A **student-friendly Google Colab notebook** for training a small convolutional neural network on MNIST and visualizing class-related regions using Grad-CAM++ with mathematically exact second- and third-order derivatives for this ReLU-based classifier.

## What you can change

- The filter counts in 1–4 convolutional layers (optional layers can be disabled with 0)
- The number of training epochs (1–20)
- The external image index (one or several images)

## Run in Colab

1. Click **Open in Colab** and select a Python runtime (GPU recommended for faster training).
2. Run sections 1–6 in order; no Drive mounting or dataset upload is required.
3. Change the number of convolutional filters and epochs, then retrain before viewing updated explanations.
4. Section 4 downloads a fixed revision of [Num_sorce_mnist](https://github.com/TakaNori999/Num_sorce_mnist) (`num_src`, 30 handwritten-digit PNGs). Section 6 visualizes the selected image(s).

## Method and evaluation

| Setting | Default |
| --- | --- |
| Dataset for training | Keras MNIST (60,000 training + 10,000 test images) |
| Validation | Last 10% of MNIST training images (`validation_split=0.1`) |
| Network | Conv2D(32, 3×3, ReLU), optional further Conv2Ds, Flatten → Dense(64, ReLU) → Dense(10) → Softmax |
| Optimizer/loss | SGD / categorical crossentropy |
| Batch size / epochs | 32 / 1 (modifiable) |
| External images | [Num_sorce_mnist, `num_src`](https://github.com/TakaNori999/Num_sorce_mnist/tree/c41ab788a669ad03b58b1e387b69647faa699eaf/num_src), 30 images; pinned commit `c41ab788a669ad03b58b1e387b69647faa699eaf` |
| Attribution target | Predicted class logit, last enabled convolutional layer |
| Grad-CAM++ | **Exact analytic second-/third-order derivatives** of the exponential class score, using the piecewise-linear downstream classifier |

For the displayed feature maps, the network head contains only linear layers and ReLU, so the exponential-score derivative identities hold except at ReLU kinks. Full higher-order autodiff across every pixel is unnecessary. The code prints both held-out MNIST test accuracy and external-image accuracy. External images are converted from white-background/black-digit display format to the MNIST-like black-background/white-digit input format.

**Important limitations:** These visualizations do not establish faithful causal explanations. The network has no pooling; with large filter counts, the Flatten/Dense part can become computationally demanding. Training and results vary by runtime and library version.

## Data and licenses

This repository distributes **code only**. The 30 external test images are fetched at runtime from a separate repository; they are not included in this software's GitHub Release or Zenodo archive. **The 30 test images were originally created by the author of this educational code (Norihiro Takahashi).** The external image repository currently has no explicit reuse license; authorship alone does not grant reuse or redistribution rights to third parties. Specify a separate image license there if broad image reuse is intended.

MNIST is obtained through Keras and retains its own terms; the dataset is made available under CC BY-SA 3.0 according to the [Keras documentation](https://keras.io/api/datasets/mnist/). <https://keras.io/api/datasets/mnist/>

The code is MIT-licensed; third-party packages and data are not covered by this license.

## Grad-CAM++ reference

Chattopadhyay, A., Sarkar, A., Howlader, P., & Balasubramanian, V. N. (2018). *Grad-CAM++: Generalized Gradient-Based Visual Explanations for Deep Convolutional Networks.* WACV. https://doi.org/10.1109/WACV.2018.00097

## Citation and archival

Version **v1.0.0** has been published and archived on Zenodo. The assigned DOI is [10.5281/zenodo.23992469](https://doi.org/10.5281/zenodo.23992469). To cite this software, refer to [CITATION.cff](CITATION.cff), the DOI, or the GitHub **Cite this repository** feature. The Zenodo archive is a snapshot of the released version; subsequent changes to this README on GitHub do not modify the existing archive.

[Japanese GitHub + Zenodo release guide](ZENODO_RELEASE_GUIDE_ja.md)
