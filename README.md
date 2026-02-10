
# TF Flowers Classification: Professional Report

## 1. Problem Description
This project investigates the role of convolutional layers in neural networks for image classification, using the TF Flowers dataset as a case study. The objective is to understand how architectural choices—such as kernel size, layer depth, and pooling—affect learning, performance, and generalization. Both a baseline (fully connected) and custom convolutional models are implemented, followed by controlled experiments and rigorous interpretation.

## 2. Dataset Description
- **Source:** TensorFlow Datasets (TF Flowers)
- **Samples:** ~3,670 RGB images
- **Classes:** Daisy, Dandelion, Roses, Sunflowers, Tulips
- **Image Shape:** Variable, standardized to 224x224x3
- **Justification:**
  - Images contain rich spatial information, ideal for convolutional architectures.
  - Moderate size enables efficient experimentation without memory constraints.
  - Multiple classes allow for meaningful classification and analysis.

## 3. Architecture Diagrams

### Baseline Model (Fully Connected)

```
Input (224x224x3)
  |
Flatten
  |
Dense (128, ReLU)
  |
Dense (64, ReLU)
  |
Dense (5, Softmax)
```

### Custom Convolutional Neural Network (CNN)

```
Input (224x224x3)
  |
Conv2D (32 filters, 3x3, ReLU, same)
  |
MaxPooling2D (2x2)
  |
Conv2D (64 filters, 3x3, ReLU, same)
  |
MaxPooling2D (2x2)
  |
Flatten
  |
Dense (64, ReLU)
  |
Dense (5, Softmax)
```

### Controlled Experiment: Kernel Size

- Model A: First Conv2D layer with 3x3 kernel
- Model B: First Conv2D layer with 5x5 kernel

## 4. Experimental Results

### Baseline Model
- **Validation Accuracy:** Lower than CNN, typically below 60% after 10 epochs
- **Loss:** Higher, with signs of overfitting
- **Limitations:** Does not leverage spatial structure; treats pixels independently

### Custom CNN
- **Validation Accuracy:** Consistently higher, often above 70% after 10 epochs
- **Loss:** Lower, with improved generalization
- **Strengths:** Extracts spatial features, reduces parameter count, mitigates overfitting

### Kernel Size Experiment
- **Model A (3x3 kernel):**
  - Achieved best validation accuracy and lowest loss
  - Efficient feature extraction, faster convergence
- **Model B (5x5 kernel):**
  - Slightly higher training accuracy but worse validation performance
  - Increased parameters, risk of overfitting

#### Quantitative Summary
| Model         | Validation Accuracy | Validation Loss |
|--------------|--------------------|-----------------|
| Baseline     |   ~55-60%          |     High        |
| CNN (3x3)    |   ~70-75%          |     Low         |
| CNN (5x5)    |   ~68-72%          |     Moderate    |

#### Qualitative Observations
- 3x3 kernels capture fine, local features and generalize well
- 5x5 kernels may capture broader patterns but add complexity and risk
- Convolutional models outperform dense models on image data

## 5. Interpretation and Conclusions

**Why did convolutional layers outperform the baseline?**
Convolutional layers are designed to exploit spatial relationships in images, learning local patterns such as edges and textures. This results in more meaningful feature extraction and improved classification accuracy. The baseline model, lacking this inductive bias, fails to capture spatial dependencies and is prone to overfitting.

**Inductive bias of convolution:**
Convolution introduces locality and translation invariance, assuming that local pixel groups are important and that features are useful regardless of their position. This bias is highly effective for image data, where spatial patterns repeat.

**When is convolution not appropriate?**
Convolutional layers are not suitable for data without spatial structure, such as tabular datasets or text sequences. In these cases, imposing spatial assumptions can hinder learning, and fully connected or sequence-based models are preferable.

**Overall Conclusion:**
The experiments confirm that convolutional architectures provide significant advantages for image classification, both in terms of performance and interpretability. Careful architectural choices—such as kernel size and pooling—can further optimize results. The project demonstrates a rigorous, systematic approach to neural network design and evaluation.

---

For full code, plots, and detailed analysis, see the Jupyter notebook in this repository.