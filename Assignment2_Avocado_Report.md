# Greenpod Labs — Assignment 2
## Computer Vision Classification

### 1. Objective
Build and compare two computer vision approaches for image classification.

### 2. Dataset Understanding
The supplied dataset contains 1,090 images across four labels:
blackspot, canker, fresh, and grenning.

Training images: 991
Test images: 99

Training distribution:
- blackspot: 184 (18.57%)
- canker: 179 (18.06%)
- fresh: 281 (28.36%)
- grenning: 347 (35.02%)

All 1,090 images were readable. No exact duplicate image pairs
were found by the file-content check. Image dimensions varied,
with widths from 144 to 800 pixels and heights from 138 to 800 pixels.

Visual inspection found differences in lighting, orientation,
background, and image appearance. Some examples labelled fresh
appear to show oranges rather than avocados. Therefore, the supplied
dataset does not establish the four avocado ripening stages described
in the assignment. The models below classify the dataset's actual
labels, not verified avocado ripening stages.

### 3. Approach 1 — Classical Computer Vision
CIELAB color histograms and Local Binary Pattern (LBP) texture
features were extracted from resized images. A standardized
RBF-kernel Support Vector Machine (SVM) was trained on these features.

Validation accuracy: 96.48%

### 4. Approach 2 — MobileNetV2
A pretrained MobileNetV2 model was used for transfer learning.
The feature extractor was frozen, and the final classification
layer was trained for four dataset classes over three epochs.

Validation accuracy: 97.99%

### 5. Test Results

| Metric | Classical SVM | MobileNetV2 |
|---|---:|---:|
| Accuracy | 95.96% | 91.92% |
| Macro Precision | 96.15% | 91.88% |
| Macro Recall | 95.45% | 90.91% |
| Macro F1-score | 95.42% | 91.14% |

The classical SVM performed better on the held-out test set.
Its macro F1-score was 95.42%, compared with 91.14% for MobileNetV2.

The test set contains only 99 images, so these estimates may vary
on a larger, more diverse dataset.

### 6. Evaluation Metrics
Accuracy measures the proportion of correct predictions.
Precision measures how often predictions for a class are correct.
Recall measures how many actual examples of a class are identified.
Macro F1-score gives equal weight to each class and is useful when
class sizes differ. Confusion matrices show which classes are confused.

### 7. Example Demonstration
The accompanying notebook runs one held-out test image through
both models and prints the actual dataset label and each prediction.
The recorded output should be retained as demonstration evidence.

### 8. Mandatory Questions

#### 1. In production, how does your model perform?
On the supplied held-out test set, SVM achieved 95.96% accuracy
and 95.42% macro F1-score. MobileNetV2 achieved 91.92% accuracy
and 91.14% macro F1-score. Production performance and inference
latency have not been measured. Real-world performance would require
testing on representative images from the intended production setting.

#### 2. What are the drawbacks of your model?
The dataset labels and some sample images do not match the stated
avocado ripening task. The test set is small. Differences in lighting,
background, image resolution, and surface appearance may affect
predictions. The SVM depends on manually designed color and texture
features, while MobileNetV2 may require more training data and tuning.

#### 3. If given more time, what would you improve?
Obtain a verified avocado dataset labelled by ripening stage.
Inspect labels and image quality, collect more balanced samples,
test under different lighting conditions, tune both models, and
evaluate them on an independent real-world dataset. Measure inference
latency before selecting a production deployment model.

#### 4. Where did you spend the most time?
The main effort was spent on dataset inspection and preprocessing,
implementing two different approaches, training the models, resolving
label-format issues during evaluation, and comparing the test metrics.

### 9. Conclusion
Both approaches were implemented and evaluated. Classical SVM was
the stronger model on this dataset's held-out test set. However,
the dataset mismatch must be resolved before either model can be
claimed to solve avocado ripening-stage classification.