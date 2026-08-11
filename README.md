# Plant Disease Detection with Transfer Learning

### Tomato Leaves

## The Case

Plant diseases can affect crop quality, reduce yields, and lead to economic losses for growers. Detecting signs of disease early can help farmers take action before the problem spreads.

However, identifying plant diseases often requires knowledge and manual inspection. Our case explores whether image classification could be used as a first step toward making this process faster and more accessible for tomato growers.

### The Idea

Imagine a tool where a tomato grower takes a photo of a leaf and receives an indication of whether the leaf appears:

- **Healthy**
- Affected by **Early Blight**
- Affected by **Late Blight**

Instead of developing an image recognition model completely from scratch, we explore **transfer learning** — using a model that has already learned to recognize visual patterns from a large image dataset and adapting that knowledge to tomato disease classification.

## Business Value

A system like this could potentially help agricultural businesses:

- Detect possible tomato diseases earlier
- Reduce time spent on manual inspection
- Support growers in identifying plants that may require further attention
- Reduce crop losses through earlier intervention
- Make basic plant health screening more accessible

The model should not be considered a replacement for expert assessment. Instead, it could act as an early screening and decision-support tool.

## Project Goal

The goal of this project is to investigate whether transfer learning can be used to distinguish between healthy tomato leaves and leaves affected by Early Blight or Late Blight.

We will:

- Explore and understand the PlantVillage dataset
- Investigate the distribution of image classes
- Select suitable classes for the classification task
- Apply transfer learning using a pre-trained image classification model
- Train and evaluate the model
- Analyze the results, limitations, and potential business value

## Dataset

We use the **PlantVillage** dataset from Kaggle, which contains images of healthy and diseased plant leaves across several plant species and disease categories.

After exploring the dataset, we selected three classes from the same plant species:

| Class | Training Images | Validation Images |
|---|---:|---:|
| Tomato - Healthy | 1,273 | 318 |
| Tomato - Early Blight | 800 | 200 |
| Tomato - Late Blight | 1,527 | 382 |

The classes are not perfectly balanced, but all contain enough images for a small transfer learning experiment.

Using classes from the same plant species also creates a more meaningful classification problem. The model must learn disease-related visual patterns rather than simply learning to distinguish between different types of plants.

### Initial Visual Observations

An initial exploration of the images showed visible differences between the three classes:

- **Healthy leaves** appear mostly green with a relatively even color.
- **Early Blight** examples show smaller brown or dark spots while much of the leaf remains green.
- **Late Blight** examples show larger damaged or brown areas, with some leaves appearing more severely affected.

These observations suggest that features such as **color, texture, and patterns of leaf damage** may be useful for classification.

All images in the selected classes have a resolution of **256 × 256 pixels**.

## Dataset Setup

Each team member downloads the PlantVillage dataset locally. The image data is not included in this repository.

After downloading and extracting the dataset, place it inside:

`data/raw/`

Expected structure:

    data/
    └── raw/
        └── plantvillage/
            └── PlantVillage/
                ├── train/
                └── val/

## From Image to Insight

**Tomato leaf image → Pre-trained model → Transfer learning → Disease classification → Decision support**

The technical goal is to understand how transfer learning can reuse knowledge from an existing image model for a new classification problem.

The broader goal is to explore how this approach could form the foundation of a practical tool that helps growers identify potential plant health problems earlier.

## Limitations

The PlantVillage images are captured under relatively controlled conditions with similar backgrounds and image quality.

Real-world images taken by growers could contain different lighting conditions, backgrounds, angles, and image quality. Therefore, good performance on this dataset would not necessarily mean that the model is ready for real-world agricultural use.

This project should be considered a **proof of concept** rather than a production-ready disease detection system.