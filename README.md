<div align="center">

<img src="./figs/calmera_icon.png" alt="icon" style="width:110px; height:95px;" />

# [**CaLoRAify: *Ca*lorie Estimation with Visual-Text Pairing and *LoRA*-Driven Visual Language Models**](https://arxiv.org/abs/2412.09936)

</div>

---

<div align="center">
	
**Dongyu Yao<sup>&dagger;</sup> Keling Yao<sup>&dagger;</sup> Junhong Zhou<sup>&dagger;</sup> Yinghao Zhang<sup>&dagger;</sup>**

**<sup>&dagger;</sup>: Equal contribution**

**Carnegie Mellon University**

[![arXiv](https://img.shields.io/badge/arXiv-2412.09936-B31B1B.svg?logo=arxiv&logoColor=white)](https://arxiv.org/abs/2412.09936)
[![Hugging Face](https://img.shields.io/badge/%F0%9F%A4%97-Hugging%20Face-blue)](https://huggingface.co/datasets/Kennyy/Cal_Data/tree/main)

</div>

---

## Overview

**CaLoRAify** is a novel project aimed at addressing the obesity epidemic (the "heavy" issue) by leveraging **Vision-Language Models (VLMs)**, fine-tuning techniques, and **Retrieval-Augmented Generation (RAG)** methods to estimate meal calorie content. The system serves as a **virtual dietitian**, offering users calorie analyses and dietary recommendations based on meal photos.

<img src="./figs/pipeline.png" />

---

## Features

- **Ingredient Recognition**: Analyze meal images to identify individual ingredients.
- **Calorie Estimation**: Use advanced models like **MiniGPT-4** for accurate calorie computations.
- **Retrieval-Augmented Generation (RAG)**: Enhance estimates with scientific nutritional data.
- **Interactive Feedback**: Support multi-turn dialogues for recalculating results based on user feedback.
- **Real-World Adaptation**: Address challenges in food presentation variability and ingredient complexity.

---

## Methodology

### 1. Data Sources

- **Recipe1M+ Dataset**: Base dataset for ingredient recognition.
- **USDA Food Calorie Database**: Reference for granular nutritional data.

Our self-constructed dataset store [here](https://huggingface.co/datasets/Kennyy/Cal_Data/tree/main).

### 2. Model Selection

- Fine-tuning **MiniGPT-4**, using **LoRA** and **QLoRA** methods.

### 3. Loss Function

The loss function combines cross-entropy and mean squared error (MSE):

$L = \lambda_{CE}L_{CE} + \lambda_{MSE}L_{MSE}$

Adjust weights $\lambda_{CE}$ and $\lambda_{MSE}$ to balance tasks.

### 4. Training and Evaluation

- **Multi-task Learning**: Train for ingredient classification and calorie estimation simultaneously.
- **Evaluation Metrics**:
  - **Precision** and **Recall** for ingredient prediction.
  - **Mean Squared Error (MSE)** for calorie estimates.

### 5. Inference

- Apply prompt engineering to minimize ambiguity in meal identification.
- Implement interactive recalculations for dynamic user interactions.

---

## Installation

### Requirements

- NVIDIA GPU with at least 48 GB memory
- Python environment compatible with CUDA

### Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/KennyYao2001/16824-CaLORAify.git
   cd 16824-CaLORAify
   ```

2.	Create and activate the environment:

   ```bash
   conda env create -f environment.yml
   conda activate minigptv
   ```

3.	Download the pre-trained MiniGPT-4 weights:
	- [MiniGPT-4 Checkpoints](https://drive.google.com/file/d/1y01_Vcwzp1jGi9IVOkYkDpn11lXxNKrZ/view?usp=sharing)
4.	Configure model paths:
	-	Update the configuration file at eval_configs/minigptv2_eval.yaml  with the path to downloaded weights.

Running the Demo

Launch the calorie estimation demo locally:
```bash
python demo_v2.py --cfg-path eval_configs/minigptv2_eval.yaml  --gpu-id 0
```
