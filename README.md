# Brain Tumor Segmentation using Advanced U-Net Architectures

## 📋 Project Overview

This project focuses on the semantic segmentation of brain tumors from 3-Channels (pre, FLAIR, post) MRI scans. The goal is to accurately classify tumor regions to assist in medical diagnosis and treatment planning.

I implemented and trained four distinct Deep Learning architectures from scratch to compare their performance. The project addresses common hardware constraints (like Google Colab's GPU memory) using advanced optimization techniques.

## 📂 Dataset
The dataset used for this project was sourced from Kaggle. It contains MRI scans with corresponding masks manually annotated by radiologists.

**Source**: [https://www.kaggle.com/datasets/mateuszbuda/lgg-mri-segmentation/data]

**Preprocessing**: Images were normalized (MinMax) and augmented (rotations, flips using Albumentation) to increase model robustness.

## 🧠 Architectures Implemented

The following models were developed from scratch to evaluate the impact of attention mechanisms and nested skip pathways:

**Standard U-Net**: The baseline encoder-decoder architecture.

**Attention U-Net**: Integrates Attention Gates to enhance naive skip connections, focusing on relevant features from the encoder, discarding the rest.

**U-Net++**: Utilizes nested and dense skip connections to reduce the semantic gap between encoder and decoder feature maps.

**Attention U-Net++**: A hybrid approach combining nested skip pathways with attention mechanisms.

## 🛠️ Key Techniques & Optimizations

To ensure robust training and handle hardware constraints (OOM on Google Colab), the following techniques were employed:

### Optimization & Memory Management

**Batch Normalization**: Increase network stability by reducing internal covariate shift.

**Gradient Accumulation**: Simulates larger batch sizes by accumulating gradients over multiple mini-batches before updating weights, effectively bypassing GPU memory limits.

**Group Normalization**: Used (Group=16) as an alternative to Batch Normalization, which is beneficial when batch sizes are small due to memory constraints.

### Regularization & Stability

**Learning Rate Scheduler**: Dynamic adjustment of the learning rate to converge faster and avoid local minima.

**Early Stopping**: Monitors validation loss to stop training when performance plateaus, preventing overfitting.

**Dropout and L2-reg**: Applied to prevent overfitting.

**Reproducibility**: A fixed random seed was set for all experiments to ensure consistent and comparable results.

## 📉 Loss Functions

To deal with class imbalance (tumor pixels are much fewer than background pixels), several loss functions were experimented with:

**Binary Cross Entropy (BCE)**: Standard pixel-wise classification loss.

**Dice Loss**: Directly optimizes the Dice coefficient (Intersection over Union).

**Tversky Loss**: A generalization of Dice loss that allows weighting false positives and false negatives differently.

**Combined Loss**: 0.5 * BCE + 0.5 * Tversky to leverage pixel-wise loss (BCE) and region-wise loss (Tversky).

## 📉 Training Evaluation

<img width="350" height="350" alt="Train vs Loss" src="https://github.com/user-attachments/assets/7534bc04-dec7-49e3-b696-542232541259" />
<img width="350" height="350" alt="Attention U-Net Train vs Val loss" src="https://github.com/user-attachments/assets/5123e57f-9b2b-4cd8-a9e0-b0a2e476b4b1" />
<img width="350" height="350" alt="UNet++ train vs val loss" src="https://github.com/user-attachments/assets/bb5f169e-6cb2-413d-a008-619df65d6dad" />
<img width="350" height="350" alt="AttentionUNet++_trainVSval" src="https://github.com/user-attachments/assets/08d6f5fd-6add-4379-96bd-326b0b5b0ce5" />

## 📊 Experimental Results

The models were evaluated based on the Dice Score. Below is the performance comparison of the best saved models.

**Architecture | Dice Score**

U-Net: **0.82**

Attention U-Net: **0.87**

U-Net++: **0.85**

Attention U-Net++:	**0.76**

## 📈 Visualizations

Below are samples of the segmentation results compared to the Ground Truth.

<img width="991" height="191" alt="666" src="https://github.com/user-attachments/assets/89ee8433-0f68-4f37-a237-7f65f6c8427b" />
<img width="991" height="191" alt="361" src="https://github.com/user-attachments/assets/959a0979-beb2-4712-aacb-cc176280eb1f" />
<img width="991" height="191" alt="241" src="https://github.com/user-attachments/assets/aad7aa26-1f3d-46ce-8712-4c2b6c3099f8" />
<img width="991" height="191" alt="157" src="https://github.com/user-attachments/assets/ad61d7f1-51b1-4dbe-a910-9d6cf0ce35c5" />
<img width="991" height="191" alt="129" src="https://github.com/user-attachments/assets/e46e3766-02de-4ee7-bb4d-2fc0dc40a2bb" />
<img width="991" height="191" alt="75" src="https://github.com/user-attachments/assets/e257753c-1b55-474a-bde9-1cf1d97f227e" />
<img width="991" height="191" alt="43" src="https://github.com/user-attachments/assets/e3466d56-1a48-4ebc-b9ff-a2ac6d85f1bb" />
<img width="991" height="191" alt="563" src="https://github.com/user-attachments/assets/c8b3b99d-8d0f-4d76-a848-8b73866ec7e3" />
<img width="991" height="191" alt="688" src="https://github.com/user-attachments/assets/e70d8a11-5fe6-4935-b7dd-5e29576cad50" />
<img width="991" height="191" alt="804" src="https://github.com/user-attachments/assets/10dbedfe-9644-4191-ac72-4abdffc25cb9" />

## 📝 Conclusions

This project explored several deep learning architectures of the U-Net family to address a very sensitive image segmentation task such as Brain Tumor Segmentation.

The Attention U-Net variant proved to be the most effective, achieving the highest Dice score of 86.7%.

Next steps might involve changing the setup of the attention gates in Attention U-Net++ and trying other techniques to mitigate the small batch size constrained by OOM issues in Google Colab. A further step might be exploring a different family of architectures to compare the results.

These findings demonstrate the value of attention mechanisms in enhancing segmentation performance for medical imaging tasks.

⭐️ If you found this project useful, please star the repo!

Download the weights from here: [https://huggingface.co/mattarellidenis/BrainTumorSegmentation]

LinkedIn: [https://www.linkedin.com/in/denis-mattarelli-46938b163]

Contact: [d.mattarelliwork@gmail.com]
