# Avocado Ripening Classification — Greenpod Labs Assignment 2

## Project Overview

This project compares two computer vision approaches for image classification as part of Greenpod Labs Data Science Assignment 2.

The supplied dataset contains four categories: `blackspot`, `canker`, `fresh`, and `grenning`. The models were trained to classify these dataset categories.

**Dataset limitation:** The supplied dataset labels do not match the four avocado ripening stages specified in the assignment. Some images labelled `fresh` appear to show oranges. Therefore, the results below apply to the supplied dataset categories and do not establish validated avocado ripening-stage classification.

## Technologies Used

- Python
- Google Colab
- OpenCV
- NumPy and Pandas
- Scikit-image
- Scikit-learn
- PyTorch and Torchvision
- Matplotlib and Seaborn

## Dataset Summary

| Dataset split | Images |
|---|---:|
| Training | 991 |
| Testing | 99 |
| Total | 1,090 |

Classes: `blackspot`, `canker`, `fresh`, `grenning`.

All 1,090 images were readable during inspection. No exact duplicate file contents were detected. Image resolutions varied.

## Approach 1: Classical Computer Vision + SVM

- Extracted CIELAB color histograms.
- Extracted Local Binary Pattern (LBP) texture features.
- Standardized the features.
- Trained an RBF-kernel Support Vector Machine (SVM).

Validation accuracy: **96.48%**

## Approach 2: MobileNetV2 Transfer Learning

- Loaded pretrained MobileNetV2 weights.
- Froze the pretrained feature extractor.
- Replaced and trained the final classification layer.
- Applied image resizing, normalization, and training augmentation.

Validation accuracy after three epochs: **97.99%**

## Test Set Results

Both models were evaluated on the same 99 held-out test images.

| Metric | Classical SVM | MobileNetV2 |
|---|---:|---:|
| Accuracy | 95.96% | 91.92% |
| Macro Precision | 96.15% | 91.88% |
| Macro Recall | 95.45% | 90.91% |
| Macro F1-score | 95.42% | 91.14% |

**Best model on this test set:** Classical SVM, based on accuracy and macro F1-score.

These results are based on a small test set and should not be interpreted as production performance.

## Evaluation Metrics

- **Accuracy:** Overall proportion of correct predictions.
- **Precision:** How often a predicted class is correct.
- **Recall:** How many actual examples of a class are identified.
- **Macro F1-score:** Balances precision and recall while giving equal weight to each class.
- **Confusion matrix:** Shows correct and incorrect predictions by class.

## Project Files

- `notebooks/` — notebooks for dataset analysis, model training, evaluation, and demonstration.
- `src/` — Python source files.
- `models/` — saved model files.
- `data/` — dataset and processed data.
- `report/` — assignment report and evaluation outputs.
- `main_demo.py` — example inference script.
- `requirements.txt` — Python dependencies.

## How to Run

1. Open the completed Google Colab notebook.
2. Download the dataset using the provided dataset link.
3. Extract the dataset into the expected training and testing folder structure.
4. Install the dependencies listed in `requirements.txt` if needed.
5. Run the EDA, classical model, MobileNetV2, and evaluation sections in order.
6. Run the example prediction cell to compare both models.

## Mandatory Assignment Questions

### 1. In production, how does your model perform?

On the held-out test set, the SVM achieved 95.96% accuracy and 95.42% macro F1-score. MobileNetV2 achieved 91.92% accuracy and 91.14% macro F1-score. Production latency and performance have not been measured and would require testing under real operating conditions.

### 2. What are the drawbacks of your model?

The supplied dataset does not correctly establish the intended avocado ripening-stage labels. Image appearance can vary with lighting, backgrounds, resolution, and surface conditions. The test set is small, and the SVM relies on manually engineered color and texture features.

### 3. If given more time, what would you improve?

I would obtain a correctly labelled avocado ripening dataset, inspect and balance the classes, collect more diverse images, tune both models, and evaluate on an independent dataset. I would also measure inference speed and test the selected model under production conditions.

### 4. Where did you spend the most time?

The main effort went into dataset inspection and preprocessing, implementing both classification approaches, training the models, resolving evaluation issues, and comparing their performance on the held-out test set.

## Conclusion

Both classical computer vision and deep learning approaches were implemented and compared. The SVM achieved better test performance on the supplied dataset. A correctly labelled avocado ripening dataset is required to validate the intended application.
