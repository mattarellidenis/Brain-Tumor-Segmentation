# Brain Tumor Segmentation using Advanced U-Net Architectures

📋 Project Overview
This project focuses on the semantic segmentation of brain tumors from 3-Channels (pre, FLAIR, post) MRI scans. The goal is to accurately classify tumor regions to assist in medical diagnosis and treatment planning.

I implemented and trained four distinct Deep Learning architectures from scratch to compare their performance. The project addresses common hardware constraints (like Google Colab's GPU memory) using advanced optimization techniques.

🧠 Architectures Implemented
The following models were developed from scratch to evaluate the impact of attention mechanisms and nested skip pathways:

Standard U-Net: The baseline encoder-decoder architecture.

Attention U-Net: Integrates Attention Gates to focus on target structures of varying shapes and sizes.

U-Net++: Utilizes nested and dense skip connections to reduce the semantic gap between encoder and decoder feature maps.

Attention U-Net++: A hybrid approach combining nested skip pathways with attention mechanisms.

🛠️ Key Techniques & Optimizations
To ensure robust training and handle hardware constraints (OOM on Google Colab), the following techniques were employed:

Optimization & Memory Management

Gradient Accumulation: Simulates larger batch sizes by accumulating gradients over multiple mini-batches before updating weights, effectively bypassing GPU memory limits.

Batch Normalization: Increase network stability by reducing internal covariate shift.

Group Normalization: Used (Group=16) as an alternative to Batch Normalization, which is beneficial when batch sizes are small due to memory constraints.

Regularization & Stability

Learning Rate Scheduler: Dynamic adjustment of the learning rate to converge faster and avoid local minima.

Early Stopping: Monitors validation loss to stop training when performance plateaus, preventing overfitting.

Dropout and L2-reg: Applied to prevent overfitting.

Reproducibility: A fixed random seed was set for all experiments to ensure consistent and comparable results.

📉 Loss Functions
To deal with class imbalance (tumor pixels are much fewer than background pixels), several loss functions were experimented with:

Binary Cross Entropy (BCE): Standard pixel-wise classification loss.

Dice Loss: Directly optimizes the Dice coefficient (Intersection over Union).

Tversky Loss: A generalization of Dice loss that allows weighting false positives and false negatives differently.

Combined Loss: 1/2 * BCE + 1/2 * Tversky to leverage pixel-wise loss (BCE) and region-wise loss (Tversky).

📊 Experimental Results
The models were evaluated based on the Dice Score. Below is the performance comparison of the best saved models.

Architecture  Dice Score
U-Net:	0.82
Attention U-Net: 0.87
U-Net++: 0.85
Attention U-Net++:	0.81

📂 Dataset
The dataset used for this project was sourced from Kaggle. It contains MRI scans with corresponding masks manually annotated by radiologists.

Source: [https://www.kaggle.com/datasets/mateuszbuda/lgg-mri-segmentation/data]

Preprocessing: Images were normalized (MinMax) and augmented (rotations, flips using Albumentation) to increase model robustness.

📈 Visualizations
Below are samples of the segmentation results compared to the Ground Truth.

Input MRI	Ground Truth	Predicted Mask
🔗 Connect

If you found this project useful, please star the repo!

[Your LinkedIn Profile]
