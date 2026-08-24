# AI Image Captioning System

An end-to-end deep learning project for automatically generating natural-language captions for images. The project explores multiple neural network architectures for combining visual image features with sequential text representations and compares their performance using BLEU scores.

## Overview

Image captioning combines two major areas of deep learning:

- **Computer Vision** for understanding image content
- **Natural Language Processing** for generating descriptive text

The system extracts visual features from images using pretrained convolutional neural networks and passes those features to sequence-based neural networks that generate captions word by word.

Multiple architectures were explored, including:

- LSTM
- GRU
- Transformer
- Convolutional-Bidirectional LSTM

The final Convolutional-Bidirectional model achieved the strongest BLEU performance among the final recurrent-model experiments.

---

## Architecture

The image-captioning pipeline consists of:

1. Image preprocessing
2. CNN-based feature extraction
3. Caption cleaning and tokenization
4. Sequence generation
5. Image and text feature fusion
6. Neural network training
7. Caption generation
8. BLEU-based evaluation

### Visual Feature Extraction

Pretrained CNN architectures were used to transform images into compact feature vectors.

Experiments included:

- ResNet-50 with MS COCO
- InceptionV3 with Flickr30k

The final training pipeline uses pre-extracted image features for efficient model training.

### Caption Processing

Captions are cleaned by:

- converting text to lowercase
- removing digits and special characters
- removing unnecessary whitespace
- adding `startseq` and `endseq` tokens
- tokenizing captions into integer sequences
- padding sequences to a consistent length

---

## Models

### LSTM

The LSTM architecture combines CNN image features with embedded caption sequences and learns temporal relationships between words.

Training loss decreased from:

```text
4.9723 → 2.9810
```

BLEU scores:

```text
BLEU-1: 0.4428
BLEU-2: 0.2380
```

### GRU

A GRU-based sequence decoder was evaluated as a computationally lighter alternative to LSTM.

Training loss decreased from:

```text
4.7969 → 2.9385
```

BLEU scores:

```text
BLEU-1: 0.4282
BLEU-2: 0.2317
```

### Transformer

A Transformer-based captioning architecture was also evaluated during the Flickr30k experiments.

Best observed:

```text
BLEU-4: 0.323
```

### Convolutional-Bidirectional Model

The final architecture combines image features with a bidirectional recurrent text encoder.

The image branch processes visual features using dropout and dense layers, while the caption branch uses:

- word embeddings
- dropout
- bidirectional LSTM layers
- dense layers
- softmax prediction

Training loss decreased from:

```text
5.1389 → 3.4807
```

BLEU scores:

```text
BLEU-1: 0.4496
BLEU-2: 0.2438
```

---

## Model Comparison

| Model | BLEU-1 | BLEU-2 |
|---|---:|---:|
| LSTM | 0.4428 | 0.2380 |
| GRU | 0.4282 | 0.2317 |
| Convolutional-Bidirectional | **0.4496** | **0.2438** |

The Convolutional-Bidirectional architecture produced the strongest BLEU-1 and BLEU-2 results among the final model experiments.

---

## Example Caption

The trained model was also tested on an external image outside the Flickr30k test set.

Example generated caption:

```text
dog is running through the grass
```

---

## Repository Structure

```text
image-captioning-deep-learning/
│
├── notebooks/
│   ├── 01_data_preprocessing.ipynb
│   ├── 02_model_training_comparison.ipynb
│   └── 03_final_image_captioning.ipynb
│
├── models/
│   └── conv_bidirectional.h5
│
├── docs/
│   └── AI_Image_Captioning_System_Report.pdf
│
├── samples/
│
├── requirements.txt
├── .gitattributes
├── .gitignore
└── README.md
```

---

## Dataset

The project initially explored the **MS COCO** image-caption dataset.

Due to the large storage and memory requirements of the full MS COCO training data, later experiments were performed using **Flickr30k**.

Flickr30k provides multiple human-written captions for each image and is widely used for evaluating image-captioning systems.

Large pre-extracted image feature files are intentionally excluded from this repository because of their size. They can be regenerated through the preprocessing workflow in the notebooks.

---

## Technologies

- Python
- TensorFlow
- Keras
- NumPy
- Pandas
- NLTK
- Pillow
- Matplotlib
- Scikit-learn
- Jupyter Notebook
- CNN
- LSTM
- GRU
- Bidirectional LSTM
- Transformer
- InceptionV3
- ResNet-50

---

## Installation

Clone the repository:

```bash
git clone https://github.com/Rishika73/image-captioning-deep-learning.git
cd image-captioning-deep-learning
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

---

## Project Workflow

The notebooks document the model development process:

### 1. Data Preprocessing

```text
notebooks/01_data_preprocessing.ipynb
```

Covers dataset preparation, caption preprocessing, tokenization, and image feature preparation.

### 2. Model Training and Comparison

```text
notebooks/02_model_training_comparison.ipynb
```

Contains experiments with different neural-network architectures and model evaluation.

### 3. Final Image Captioning Model

```text
notebooks/03_final_image_captioning.ipynb
```

Contains the final model architecture, training process, BLEU evaluation, and caption-generation workflow.

---

## Trained Model

The trained Convolutional-Bidirectional model is stored using **Git LFS**:

```text
models/conv_bidirectional.h5
```

After cloning the repository, Git LFS can be initialized with:

```bash
git lfs install
git lfs pull
```

---

## Evaluation

Model performance is evaluated using BLEU scores through NLTK.

BLEU measures the overlap between generated captions and human-written reference captions.

- **BLEU-1** evaluates individual word overlap.
- **BLEU-2** evaluates two-word sequence overlap.
- **BLEU-4** was additionally used during Transformer experiments.

---

## Future Improvements

Potential extensions include:

- attention-based caption generation
- Vision Transformer image encoders
- Transformer-based caption decoders
- beam-search decoding
- larger captioning datasets
- pretrained vision-language models
- interactive image-upload inference application

---

## Project Report

A detailed explanation of the architecture, experiments, training process, model comparisons, and results is available in:

```text
docs/AI_Image_Captioning_System_Report.pdf
```
