Guided Masked Autoencoder for Coronary Angiography
This repository presents the code and experimental results for the project "Advancing Coronary Angiography Vessel Image Analysis via Guided Self-Supervised Masking Pre-training Strategy", conducted as part of the ROBT310 course at Nazarbayev University.

Overview
Coronary angiography is an essential diagnostic tool for identifying coronary artery disease (CAD). However, the annotation of coronary vessels is time-consuming and requires expert-level precision. This project explores a self-supervised learning approach using Masked Autoencoders (MAE), enhanced with a guided masking strategy based on Frangi filtering, to learn vessel-specific features from unlabeled medical images.

Objectives
Implement classical and Swin MAE architectures for coronary vessel image reconstruction

Investigate the impact of masking ratios on medical image reconstruction

Propose and implement a novel guided masking method that selectively masks vessel-related image patches using Frangi filtering

Improve the model’s ability to reconstruct fine-grained vessel structures without labeled data

Methodology
Data
A total of 55,000 unlabeled coronary angiography images were used, derived from the following datasets:

CADICA

XCAD

LM-CAD

All images were preprocessed to uniform size (224x224), enhanced via contrast normalization and Gaussian smoothing, and normalized for consistency.

Architectures
Two self-supervised learning frameworks were implemented:

Classical MAE: Vision Transformer-based encoder-decoder with 16x16 patch division

Swin MAE: Swin Transformer-based encoder-decoder with 4x4 patch division

Both models used MSE loss computed only over masked patches. The decoder was used only during training; the encoder was retained for downstream tasks.

Masking Strategies
Random Masking: Implemented with ratios ranging from 25% to 75%

Guided Masking: Used Frangi filter to generate a vessel probability map. Patches were ranked by vessel intensity, and a combination of vessel-rich and background patches were masked selectively.

Training Setup
Batch size: 96

Optimizer: Adam

Epochs: 200

Learning Rate: 0.001 with decay

Hardware: NVIDIA RTX 6000 (24 GB VRAM)

Frameworks: PyTorch, NumPy, skimage, OpenCV

Frangi filtering was optimized for GPU-based batch processing using tensor operations, significantly accelerating computation time.

Results
Classical MAE showed stronger reconstruction performance than Swin MAE, particularly at lower masking ratios.

Lower masking ratios (25–35%) yielded significantly better results for vessel structure reconstruction than the commonly used 75%.

Guided masking demonstrated improved vessel patch focus and learning efficiency, especially when paired with optimized Frangi sigma ranges (4–10).
