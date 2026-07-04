# Plant Disease Detection

A deep learning system that classifies plant leaf images into **four categories** — Healthy, Multiple Diseases, Rust, and Scab — using an ensemble of transfer-learning CNNs. Built on the [Plant Pathology 2020](https://www.kaggle.com/c/plant-pathology-2020-fgvc7) dataset.

## Overview

| | |
|---|---|
| **Task** | Multi-class image classification (4 classes) |
| **Dataset** | 1,822 labeled leaf images |
| **Approach** | Ensemble of Xception + DenseNet121 (transfer learning) |
| **Trainable Parameters** | 8,196 (Dense classification heads only) |
| **Validation Accuracy** | **98%** |
| **Framework** | TensorFlow / Keras |

## Model Architecture

The model combines two pretrained backbones via **prediction averaging**:

1. **Xception** (ImageNet weights, frozen) → GlobalAveragePooling2D → Dense(4, softmax)
2. **DenseNet121** (ImageNet weights, frozen) → GlobalAveragePooling2D → Dense(4, softmax)
3. Final output = **average of both branches' softmax predictions**

```
Input (512x512x3)
      │
   ┌──┴──┐
Xception  DenseNet121
   │         │
 GAP       GAP
   │         │
 Dense(4)  Dense(4)
   │         │
   └───┬─────┘
    Average
       │
   Output (4 classes)
```

Only the two Dense classification heads (8,196 parameters total) were trained — both backbones were used purely as frozen feature extractors, keeping training fast and reducing overfitting risk on a small dataset.

## Data Pipeline

- Images resized to `512x512`
- On-the-fly augmentation via `ImageDataGenerator`:
  - Rotation (±180°), zoom (15%), width/height shift (15%)
  - Horizontal & vertical flips
  - Pixel rescaling (1/255)
- 95/5 train-validation split

## Training Details

- **Optimizer:** Adam
- **Loss:** Categorical Crossentropy
- **Learning Rate Schedule:** Custom ramp-up → sustain → exponential decay scheduler
  - Start: `1e-5` → Max: `1e-4` → Min: `1e-5`
- **Epochs:** 10
- **Batch Size:** 8
- **Callback:** `ModelCheckpoint` saving the best model on `val_accuracy`

## Results

The ensemble achieved **98% validation accuracy**, with training/validation accuracy and loss curves tracked and plotted across epochs (see notebook for full plots).

## Repository Structure

```
plant-disease-detection/
├── model.ipynb          # Full training pipeline (EDA, model building, training, inference)
├── ModelHistory.csv      # Per-epoch training/validation metrics
├── submission.csv        # Sample inference output
└── README.md
```

## Pretrained Model

The trained model (`model.h5`) is available here (not included in the repo due to size):

**[Download model.h5 from Google Drive](# Plant Disease Detection

A deep learning system that classifies plant leaf images into **four categories** — Healthy, Multiple Diseases, Rust, and Scab — using an ensemble of transfer-learning CNNs. Built on the [Plant Pathology 2020](https://www.kaggle.com/c/plant-pathology-2020-fgvc7) dataset.

## Overview

| | |
|---|---|
| **Task** | Multi-class image classification (4 classes) |
| **Dataset** | 1,822 labeled leaf images |
| **Approach** | Ensemble of Xception + DenseNet121 (transfer learning) |
| **Trainable Parameters** | 8,196 (Dense classification heads only) |
| **Validation Accuracy** | **98%** |
| **Framework** | TensorFlow / Keras |

## Model Architecture

The model combines two pretrained backbones via **prediction averaging**:

1. **Xception** (ImageNet weights, frozen) → GlobalAveragePooling2D → Dense(4, softmax)
2. **DenseNet121** (ImageNet weights, frozen) → GlobalAveragePooling2D → Dense(4, softmax)
3. Final output = **average of both branches' softmax predictions**

```
Input (512x512x3)
      │
   ┌──┴──┐
Xception  DenseNet121
   │         │
 GAP       GAP
   │         │
 Dense(4)  Dense(4)
   │         │
   └───┬─────┘
    Average
       │
   Output (4 classes)
```

Only the two Dense classification heads (8,196 parameters total) were trained — both backbones were used purely as frozen feature extractors, keeping training fast and reducing overfitting risk on a small dataset.

## Data Pipeline

- Images resized to `512x512`
- On-the-fly augmentation via `ImageDataGenerator`:
  - Rotation (±180°), zoom (15%), width/height shift (15%)
  - Horizontal & vertical flips
  - Pixel rescaling (1/255)
- 95/5 train-validation split

## Training Details

- **Optimizer:** Adam
- **Loss:** Categorical Crossentropy
- **Learning Rate Schedule:** Custom ramp-up → sustain → exponential decay scheduler
  - Start: `1e-5` → Max: `1e-4` → Min: `1e-5`
- **Epochs:** 10
- **Batch Size:** 8
- **Callback:** `ModelCheckpoint` saving the best model on `val_accuracy`

## Results

The ensemble achieved **98% validation accuracy**, with training/validation accuracy and loss curves tracked and plotted across epochs (see notebook for full plots).

## Repository Structure

```
plant-disease-detection/
├── model.ipynb          # Full training pipeline (EDA, model building, training, inference)
├── ModelHistory.csv      # Per-epoch training/validation metrics
├── submission.csv        # Sample inference output
└── README.md
```

## Pretrained Model

The trained model (`model.h5`) is available here (not included in the repo due to size):

**[Download model.h5 from Google Drive](# Plant Disease Detection

A deep learning system that classifies plant leaf images into **four categories** — Healthy, Multiple Diseases, Rust, and Scab — using an ensemble of transfer-learning CNNs. Built on the [Plant Pathology 2020](https://www.kaggle.com/c/plant-pathology-2020-fgvc7) dataset.

## Overview

| | |
|---|---|
| **Task** | Multi-class image classification (4 classes) |
| **Dataset** | 1,822 labeled leaf images |
| **Approach** | Ensemble of Xception + DenseNet121 (transfer learning) |
| **Trainable Parameters** | 8,196 (Dense classification heads only) |
| **Validation Accuracy** | **98%** |
| **Framework** | TensorFlow / Keras |

## Model Architecture

The model combines two pretrained backbones via **prediction averaging**:

1. **Xception** (ImageNet weights, frozen) → GlobalAveragePooling2D → Dense(4, softmax)
2. **DenseNet121** (ImageNet weights, frozen) → GlobalAveragePooling2D → Dense(4, softmax)
3. Final output = **average of both branches' softmax predictions**

```
Input (512x512x3)
      │
   ┌──┴──┐
Xception  DenseNet121
   │         │
 GAP       GAP
   │         │
 Dense(4)  Dense(4)
   │         │
   └───┬─────┘
    Average
       │
   Output (4 classes)
```

Only the two Dense classification heads (8,196 parameters total) were trained — both backbones were used purely as frozen feature extractors, keeping training fast and reducing overfitting risk on a small dataset.

## Data Pipeline

- Images resized to `512x512`
- On-the-fly augmentation via `ImageDataGenerator`:
  - Rotation (±180°), zoom (15%), width/height shift (15%)
  - Horizontal & vertical flips
  - Pixel rescaling (1/255)
- 95/5 train-validation split

## Training Details

- **Optimizer:** Adam
- **Loss:** Categorical Crossentropy
- **Learning Rate Schedule:** Custom ramp-up → sustain → exponential decay scheduler
  - Start: `1e-5` → Max: `1e-4` → Min: `1e-5`
- **Epochs:** 10
- **Batch Size:** 8
- **Callback:** `ModelCheckpoint` saving the best model on `val_accuracy`

## Results

The ensemble achieved **98% validation accuracy**, with training/validation accuracy and loss curves tracked and plotted across epochs (see notebook for full plots).

## Repository Structure

```
plant-disease-detection/
├── model.ipynb          # Full training pipeline (EDA, model building, training, inference)
├── ModelHistory.csv      # Per-epoch training/validation metrics
├── submission.csv        # Sample inference output
└── README.md
```

## Pretrained Model

The trained model (`model.h5`) is available here (not included in the repo due to size):

**[Download model.h5 from Google Drive](https://drive.google.com/drive/folders/1_mq-aGpwK9i6btEwiNOtvsfPpSEoaXYI?usp=drive_link)**

### Usage

```python
import tensorflow as tf

model = tf.keras.models.load_model('model.h5')

# img: preprocessed image of shape (1, 512, 512, 3), rescaled to [0, 1]
predictions = model.predict(img)
# predictions -> [P(healthy), P(multiple_diseases), P(rust), P(scab)]
```

## Tech Stack

`TensorFlow` `Keras` `Python` `Pandas` `Matplotlib` `scikit-learn`

## Future Improvements

- Fine-tune backbone layers instead of using them as frozen feature extractors
- Add Grad-CAM visualizations for model interpretability
- Deploy as a lightweight web/mobile inference app
- Expand dataset size and class diversity

## License

This project is open source and available under the [MIT License](LICENSE).)**

### Usage

```python
import tensorflow as tf

model = tf.keras.models.load_model('model.h5')

# img: preprocessed image of shape (1, 512, 512, 3), rescaled to [0, 1]
predictions = model.predict(img)
# predictions -> [P(healthy), P(multiple_diseases), P(rust), P(scab)]
```

## Tech Stack

`TensorFlow` `Keras` `Python` `Pandas` `Matplotlib` `scikit-learn`

## Future Improvements

- Fine-tune backbone layers instead of using them as frozen feature extractors
- Add Grad-CAM visualizations for model interpretability
- Deploy as a lightweight web/mobile inference app
- Expand dataset size and class diversity

## License

This project is open source and available under the [MIT License](LICENSE).)**

### Usage

```python
import tensorflow as tf

model = tf.keras.models.load_model('model.h5')

# img: preprocessed image of shape (1, 512, 512, 3), rescaled to [0, 1]
predictions = model.predict(img)
# predictions -> [P(healthy), P(multiple_diseases), P(rust), P(scab)]
```

## Tech Stack

`TensorFlow` `Keras` `Python` `Pandas` `Matplotlib` `scikit-learn`

## Future Improvements

- Fine-tune backbone layers instead of using them as frozen feature extractors
- Add Grad-CAM visualizations for model interpretability
- Deploy as a lightweight web/mobile inference app
- Expand dataset size and class diversity

## License

This project is open source and available under the [MIT License](LICENSE).