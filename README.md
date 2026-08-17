# 🌿 Plant Disease Detection with Transfer Learning

> Image classification of tomato leaf diseases using pretrained CNN models and Transfer Learning.

**Members:** Spirit · Emmy · Mahtab

---

## 📌 Project Overview

The goal of this project is to investigate how **Transfer Learning** can be used to classify diseases in tomato leaves.

Given an image of a tomato leaf, the model predicts one of three classes:

- 🍃 **Healthy**
- 🟤 **Early Blight**
- 🍂 **Late Blight**

Instead of training a deep neural network completely from scratch, we use models that have already learned general visual features from **ImageNet** and adapt them to our tomato leaf classification problem.

---

## 🎯 Problem

Plant diseases can affect crop quality and production.

The task in this project is a **multiclass image classification problem**:

> Can a pretrained CNN model distinguish between Healthy tomato leaves, Early Blight and Late Blight?

The project investigates several parts of a complete machine learning workflow:

- Data inspection
- Data cleaning
- Duplicate and leakage checks
- Train / validation / test splitting
- Data augmentation
- Frozen feature extraction
- Fine-tuning
- Model comparison
- Confusion matrices
- F1-score evaluation
- Confidence analysis
- Error analysis
- Generalization on unseen test data

---

## 📊 Dataset

We use the **PlantVillage** dataset from Kaggle.

The complete PlantVillage dataset contains approximately **54,000 images** from several plant species and plant diseases.

For this project, we selected only three tomato classes.

### Selected Classes

| Class | Description |
|---|---|
| Tomato Healthy | Healthy tomato leaves |
| Tomato Early Blight | Tomato leaves affected by Early Blight |
| Tomato Late Blight | Tomato leaves affected by Late Blight |

For our selected classes, we started with:

**4,500 tomato leaf images**

After data cleaning:

**4,486 images remained**

---

## 🖼️ Initial Data Exploration

Before training any models, the dataset was inspected to understand the problem and the visual differences between the classes.

Sample images showed that:

- Healthy leaves were often visually easier to distinguish
- Early Blight contained visible spots and damaged areas
- Late Blight also contained discoloration and damaged areas
- Early Blight and Late Blight sometimes had similar visual characteristics

This later became important during the error analysis, because most classification errors occurred between **Early Blight and Late Blight**.

---

## 🧹 Data Cleaning

Before model training, the image data was checked carefully.

The analysis included:

- Checking folder structure
- Inspecting image files
- Checking class distributions
- Checking duplicate images
- Checking possible data leakage
- Identifying problematic samples
- Removing problematic images

### Before and After Cleaning

**Before cleaning:** 4,500 images  
**After cleaning:** 4,486 images

Only a small number of images were removed.

The overall class distribution therefore remained almost unchanged after cleaning.

---

## ✂️ Train / Validation / Test Split

After cleaning, the remaining **4,486 images** were divided into three separate datasets.

| Dataset | Number of Images | Purpose |
|---|---:|---|
| Training | 2,872 | Used to train the models |
| Validation | 719 | Used to compare and tune models |
| Test | 895 | Used only for final evaluation |
| **Total** | **4,486** | |

The **test set was kept separate until the final model had been selected**.

This is important because the validation set can be used during model development, while the test set should provide a final evaluation on data that has not influenced model selection.

---

## 🔄 Data Augmentation

Data augmentation was applied only to the **training data**.

The augmentation pipeline introduced small random transformations such as:

- Rotation
- Zoom
- Position changes
- Orientation changes

The purpose was to create more variation during training.

Instead of memorizing exact training images, the model is encouraged to learn more general visual patterns related to the plant diseases.

Data augmentation can also help reduce the risk of **overfitting** and improve generalization.

---

## 🧠 Transfer Learning

Transfer Learning allows knowledge from an already trained model to be reused for a new problem.

Instead of training a large CNN completely from scratch, we used models that had already been pretrained on **ImageNet**.

These pretrained models have already learned useful visual features such as:

- Edges
- Shapes
- Colors
- Textures
- Visual patterns

We then adapted these pretrained representations to our specific tomato disease classification task.

---

## 🔗 Transfer Learning Workflow

Our general Transfer Learning strategy was:

```text
Pretrained ImageNet Model
          ↓
Frozen Feature Extraction
          ↓
New Classification Head
          ↓
Healthy / Early Blight / Late Blight
          ↓
Fine-Tuning
          ↓
Model Evaluation
```

The original ImageNet classifier was not used for our final predictions.

Instead, a new classification head was added for our **three tomato classes**.

---

## 🧊 Frozen Feature Extraction

The first Transfer Learning strategy was **Frozen Feature Extraction**.

The pretrained base model was kept frozen.

This means that the pretrained weights inside the base model were not updated during this stage.

Only the newly added classification layers were trained for the tomato dataset.

Conceptually:

```text
Pretrained CNN
      ↓
Frozen Base Model
      ↓
New Classification Layers
      ↓
3 Tomato Classes
```

This allows us to benefit from previously learned visual representations without retraining the whole network.

---

## 🔧 Fine-Tuning

After training the frozen models, we also performed **controlled fine-tuning**.

During fine-tuning:

- Parts of the pretrained model were unfrozen
- Later layers were allowed to adapt to tomato leaf images
- A lower learning rate was used
- Earlier general visual features were preserved

The idea is that earlier CNN layers often learn general features such as edges and shapes, while later layers can become more specialized for the new classification task.

---

## 🤖 Models Evaluated

Two pretrained CNN architectures were evaluated in the main analysis:

### ResNet50V2

Experiments:

- **ResNet50V2 Frozen**
- **ResNet50V2 Fine-Tuned**

### EfficientNetB0

Experiments:

- **EfficientNetB0 Frozen**
- **EfficientNetB0 Fine-Tuned**

This resulted in four main model experiments.

---

## 📈 ResNet50V2 – Frozen

The first main experiment used **ResNet50V2** as a frozen feature extractor.

The model was:

- Pretrained on ImageNet
- Used without the original ImageNet classifier
- Kept frozen during the first training stage
- Extended with new classification layers for our three classes

### Validation Result

**Validation Accuracy: 95.6%**

This already provided a strong baseline.

---

## 🔧 ResNet50V2 – Fine-Tuning

The next experiment used controlled fine-tuning.

Fine-tuning improved ResNet50V2 across all main evaluation metrics.

### Frozen vs Fine-Tuned

- **Validation Accuracy**
  - Frozen: 95.6%
  - Fine-Tuned: **96.8%**

- **Macro F1**
  - Frozen: 95.0%
  - Fine-Tuned: **96.4%**

- **Weighted F1**
  - Frozen: 95.5%
  - Fine-Tuned: **96.8%**

Fine-tuning therefore improved all three main metrics for ResNet50V2.

---

## ⚡ EfficientNetB0

We also evaluated **EfficientNetB0** as a second pretrained CNN architecture.

The same overall Transfer Learning strategy was used:

1. Frozen feature extraction
2. Controlled fine-tuning
3. Validation evaluation

### Results

**EfficientNetB0 Frozen**

Validation Accuracy: **96.1%**

**EfficientNetB0 Fine-Tuned**

Validation Accuracy: **97.5%**

Fine-tuning therefore also improved EfficientNetB0.

---

## 🏆 Model Comparison

The four main experiments were compared using:

- Validation Accuracy
- Macro F1-score
- Weighted F1-score

### Validation Results

| Model | Validation Accuracy | Macro F1 | Weighted F1 |
|---|---:|---:|---:|
| ResNet50V2 Frozen | 95.6% | 95.0% | 95.5% |
| EfficientNetB0 Frozen | 96.1% | 95.6% | 96.1% |
| ResNet50V2 Fine-Tuned | 96.8% | 96.4% | 96.8% |
| **EfficientNetB0 Fine-Tuned** | **97.5%** | **97.1%** | **97.5%** |

### Best Model

🏆 **EfficientNetB0 Fine-Tuned**

It achieved the strongest overall validation performance.

The model was selected based on validation results **before the final test set was evaluated**.

---

## 🧪 Final Test Evaluation

After selecting the best model, **EfficientNetB0 Fine-Tuned** was evaluated on the separate test dataset.

### Final Result

- Test images: **895**
- Correct predictions: **866**
- Incorrect predictions: **29**
- **Test Accuracy: 96.76%**

The test accuracy remained close to the validation accuracy.

This is a positive indication that the model generalizes well to unseen data.

---

## 🔍 Final Confusion Matrix

The final test confusion matrix showed the following results.

### Early Blight

- Correctly classified: **188**
- Predicted as Late Blight: **7**
- Predicted as Healthy: **5**

### Late Blight

- Correctly classified: **362**
- Predicted as Early Blight: **13**
- Predicted as Healthy: **4**

### Healthy

- Correctly classified: **316**
- Predicted as Early Blight: **0**
- Predicted as Late Blight: **0**

The Healthy class was therefore classified perfectly in the final test set:

**316 / 316 Healthy images correctly classified**

Most remaining errors occurred between:

**Early Blight ↔ Late Blight**

---

## ⚠️ Error Analysis

Accuracy alone does not explain how or why a model fails.

Therefore, we also performed **error analysis** on the misclassified test images.

The final model made:

**29 incorrect predictions out of 895 test images**

Most errors involved confusion between Early Blight and Late Blight.

This was consistent with our visual exploration of the dataset.

Both diseases can contain similar visual features such as:

- Brown lesions
- Damaged leaf areas
- Discoloration
- Similar texture patterns

---

## 🎯 Confidence Analysis

We also examined the model's **confidence** for incorrect predictions.

For a three-class classification problem, the model produces scores for:

- Healthy
- Early Blight
- Late Blight

The class with the highest output score becomes the final prediction.

For example:

```text
Early Blight: 50%
Late Blight: 48%
Healthy:      2%
```

The model predicts **Early Blight**, but the scores show that it is uncertain between Early Blight and Late Blight.

A high-confidence prediction could instead look like:

```text
Early Blight: 98%
Late Blight:   1%
Healthy:       1%
```

However, an important observation from our error analysis was that:

> **High confidence does not automatically mean that the prediction is correct.**

Some misclassified images had high confidence values.

Confidence therefore describes how strongly the model prefers one class compared with the alternatives, but it does not guarantee that the prediction is correct.

---

## 📐 Evaluation Metrics

Several evaluation metrics were used instead of relying only on accuracy.

### Accuracy

Accuracy measures the proportion of all predictions that were correct.

```text
Correct Predictions
-------------------
Total Predictions
```

---

### Precision

Precision answers:

> When the model predicts a specific class, how often is it correct?

High precision means that the model makes relatively few false positive predictions for that class.

---

### Recall

Recall answers:

> Of all real examples belonging to a class, how many did the model successfully identify?

High recall means that the model misses relatively few examples of that class.

---

### F1-Score

F1-score combines **precision and recall** into one metric.

This is useful when we want to evaluate both false positives and false negatives.

---

### Macro F1

Macro F1 calculates an F1-score for each class and then gives every class equal importance.

Conceptually:

```text
F1 Healthy
+
F1 Early Blight
+
F1 Late Blight
----------------
       3
```

This is useful when we want smaller and larger classes to contribute equally to the final metric.

---

### Weighted F1

Weighted F1 also calculates F1 separately for every class.

However, the final value is weighted according to how many samples each class contains.

A larger class therefore contributes more to the final Weighted F1-score than a smaller class.

This is useful because our classes are not perfectly balanced.

---

## ⚖️ Class Imbalance

The three tomato classes do not contain exactly the same number of images.

For example, after the final split, the training data contained:

- Healthy: **1,015 images**
- Early Blight: **640 images**
- Late Blight: **1,217 images**

Early Blight therefore had fewer training examples than the other two classes.

Class imbalance is important because models can otherwise become more influenced by larger classes.

---

## ⚖️ Class Weights vs Weighted F1

These two concepts are related to class imbalance but are used differently.

### Class Weights

Class weights can be used **during training**.

Smaller classes can receive a larger weight so that mistakes on those classes have more impact on the training loss.

### Weighted F1

Weighted F1 is used **during evaluation**.

It summarizes class-specific F1-scores while taking the number of examples in each class into account.

In short:

```text
Class Weights
→ Training

Weighted F1
→ Evaluation
```

---

## 🌱 Practical Value

A model like this could potentially be used as a support tool for agriculture.

Possible applications include:

- Fast screening of tomato leaves
- Supporting farmers and growers
- Earlier identification of possible plant diseases
- Supporting manual inspection
- Agricultural decision support

A future application could allow a user to take a photograph of a tomato leaf and receive an initial classification.

For example:

```text
User takes a photo
        ↓
Model analyzes the leaf
        ↓
Prediction
        ↓
Healthy
or
Early Blight
or
Late Blight
```

The model should be considered a **decision-support tool** rather than a replacement for agricultural experts.

---

## ⚠️ Limitations

Although the results are strong, the project has several important limitations.

### Controlled Dataset

PlantVillage contains relatively clean and controlled images.

Real-world agricultural images may contain:

- Complex backgrounds
- Different lighting conditions
- Shadows
- Different camera angles
- Multiple leaves
- Other plants
- Occlusion
- Different image quality

The strong performance on PlantVillage therefore does not automatically guarantee the same performance in real agricultural environments.

---

### Limited Number of Classes

The project only includes three tomato classes:

- Healthy
- Early Blight
- Late Blight

A complete plant disease detection system would need to support more diseases and potentially additional plant species.

---

### Real-World Testing

The model should be tested on images collected directly from real farms or growing environments before being considered for practical deployment.

---

## 🔮 Future Work

Possible future improvements include:

- Testing the model on real-world field images
- Adding more tomato disease classes
- Adding other plant species
- Further hyperparameter tuning
- Confidence calibration
- Explainability methods such as Grad-CAM
- Comparing additional pretrained CNN architectures
- Building a web application
- Building a mobile application
- Testing the model in real agricultural environments

---

## 📁 Project Structure

```text
plant-disease-detection/
│
├── data/
│   └── raw/
│       └── plantvillage/
│           └── PlantVillage/
│
├── notebooks/
│   ├── emmy_analysis.ipynb
│   ├── spirit_analysis.ipynb
│   └── mahtab_analysis.ipynb
│
├── reports/
│   └── figures/
│       ├── emmy/
│       ├── spirit/
│       └── mahtab/
│
├── .gitignore
├── README.md
└── requirements.txt
```

---

## 📦 Dataset Setup

The PlantVillage dataset is **not stored in the GitHub repository**.

The `data/raw/` directory is gitignored because the dataset contains many image files and is too large to include directly in the repository.

Download the PlantVillage dataset from Kaggle and extract it so that the final local path becomes:

```text
data/raw/plantvillage/PlantVillage/
```

The `.gitkeep` file inside `data/raw/` is only used so that Git keeps the empty directory structure.

---

## ⚙️ Local Setup

Clone the repository:

```bash
git clone https://github.com/emmykristina/plant-disease-detection.git
cd plant-disease-detection
```

The shared development branch is:

```bash
git checkout dev
git pull origin dev
```

Create your own feature branch before starting new work:

```bash
git checkout -b feat/name-analysis
```

---

## 🐍 Virtual Environment

Create a local virtual environment:

```bash
python3 -m venv .venv
```

### Activate on Windows Git Bash

```bash
source .venv/Scripts/activate
```

Install project dependencies:

```bash
python3 -m pip install -r requirements.txt
```

The `.venv` directory should remain local and should not be pushed to GitHub.

---

## 📓 Notebooks

Each team member works in a separate notebook:

```text
notebooks/
├── emmy_analysis.ipynb
├── spirit_analysis.ipynb
└── mahtab_analysis.ipynb
```

This allows each analysis to be developed independently before the final results are compared.

---

## 📊 Figures

Generated figures are organized by team member:

```text
reports/
└── figures/
    ├── emmy/
    ├── spirit/
    └── mahtab/
```

Examples of generated analyses include:

- Sample class images
- Class distributions
- Cleaning comparisons
- Train / validation / test distributions
- Data augmentation examples
- Training history
- Validation metrics
- Model comparisons
- Confusion matrices
- Final test results
- Misclassified image analysis

---

## 🌿 Final Conclusion

This project demonstrates how **Transfer Learning can be used effectively for tomato leaf disease classification**.

We started with a subset of **4,500 PlantVillage images** from three tomato classes.

After data cleaning, **4,486 images** remained.

The dataset was then divided into:

- **2,872 training images**
- **719 validation images**
- **895 test images**

We evaluated two pretrained CNN architectures:

- ResNet50V2
- EfficientNetB0

Both architectures were tested using:

- Frozen feature extraction
- Controlled fine-tuning

Fine-tuning improved the performance of both models.

The strongest validation result was achieved by:

## 🏆 EfficientNetB0 Fine-Tuned

**Validation Accuracy: 97.5%**

The selected model was then evaluated on the completely separate test set.

### Final Test Performance

**Test Accuracy: 96.76%**

**866 of 895 test images were classified correctly.**

The model performed especially well on Healthy leaves, with:

**316 / 316 Healthy test images classified correctly.**

The main remaining challenge was distinguishing between:

**Early Blight ↔ Late Blight**

The error analysis also demonstrated that a model can sometimes make incorrect predictions with high confidence.

Therefore, the project shows the importance of evaluating machine learning models using more than one metric and performing detailed error analysis.

---

## 🔄 Complete ML Workflow

```text
PlantVillage Dataset
        ↓
Select 3 Tomato Classes
        ↓
Data Inspection
        ↓
Duplicate & Leakage Checks
        ↓
Data Cleaning
        ↓
Train / Validation / Test Split
        ↓
Data Augmentation
        ↓
Transfer Learning
        ↓
Frozen Feature Extraction
        ↓
Fine-Tuning
        ↓
Model Comparison
        ↓
Best Model Selection
        ↓
Final Test Evaluation
        ↓
Confusion Matrix
        ↓
Confidence & Error Analysis
        ↓
Practical Evaluation
```

---

## 👥 Team

- **Spirit**
- **Emmy**
- **Mahtab**

---

**Healthy plants, better future. 🌿**