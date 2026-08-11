# Plant Disease Detection with Transfer Learning

## The Case

Plant diseases can affect crop quality, reduce yields, and lead to economic losses for growers. Detecting signs of disease early can help farmers take action before the problem spreads.

However, identifying plant diseases often requires knowledge and manual inspection. Our case explores whether image classification could be used as a first step toward making this process faster and more accessible.

### The Idea

Imagine a tool where a grower takes a photo of a plant leaf and receives an indication of whether the plant appears healthy or shows signs of a specific disease.

Instead of developing an image recognition model completely from scratch, we explore **transfer learning** — using a model that has already learned to recognize visual patterns from a large image dataset and adapting that knowledge to plant disease classification.

## Business Value

A system like this could potentially help agricultural businesses:

* Detect possible plant diseases earlier
* Reduce time spent on manual inspection
* Support growers in identifying plants that may require further attention
* Reduce crop losses through earlier intervention
* Make basic plant health screening more accessible

The model should not be considered a replacement for expert assessment. Instead, it could act as an early screening and decision-support tool.

## Project Goal

The goal of this project is to investigate whether transfer learning can be used to distinguish between healthy and diseased plant leaves.

We will:

* Explore the PlantVillage image dataset
* Select suitable plant disease classes
* Use a pre-trained image classification model as our base model
* Adapt the model to our classification problem
* Train and evaluate the resulting model
* Analyze its strengths, limitations, and potential business value

## Dataset

We use the **PlantVillage** dataset from Kaggle, which contains images of healthy and diseased plant leaves across several plant species and disease categories.

Each team member downloads the dataset locally. The image data is therefore not included in this repository.

Expected local structure:

```text
data/
└── raw/
    └── plantvillage/
        └── PlantVillage/
            ├── train/
            └── val/
```

## Project Structure

```text
plant-disease-transfer-learning/
├── data/
│   └── raw/
├── notebooks/
├── .gitignore
├── README.md
└── requirements.txt
```

## From Image to Insight

The project follows a simple idea:

**Leaf image → Pre-trained model → Transfer learning → Plant health classification → Decision support**

The technical goal is to understand transfer learning. The broader goal is to explore how existing AI knowledge can be reused to solve a practical agricultural problem without training a large image recognition model from scratch.