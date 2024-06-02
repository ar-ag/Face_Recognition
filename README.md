
### Introduction

Our project leverages deep learning to enhance criminal identification by training a model on images of criminals and non-criminals. Integrated with a criminal database, the system extracts and compares facial features from input images to identify matches and retrieve information. Continuous model refinement and rigorous validation ensure accuracy and reliability. A user-friendly interface allows seamless interaction for law enforcement personnel, while strict privacy and security measures protect sensitive data. This solution provides an efficient and accurate tool for aiding investigations and enhancing public safety.
### Approach Overview

- **One-Shot Image Classification Focus**: 
  - Specializing in character recognition.
  
- **Utilizing Siamese Convolutional Neural Networks**: 
  - **Generic Image Feature Learning**: Capable of predicting unseen image classes with minimal data.
  - **Ease of Training**: Standard optimization methods on image pairs from the source dataset.
  - **Competitive and General**: No domain-specific knowledge required, leveraging deep learning.

- **Training Strategy**:
  - **Verification Task**: Train a network to distinguish if image pairs belong to the same or different classes.
  - **Foundation for Classification**: A network proficient in verification will excel in classifying new images through comparison.

- **Classification Method**:
  - **Pairwise Comparison**: Compare any new image to a known image from each class.
  - **Highest Score Identification**: The pair with the highest verification score indicates the new image's class.

- **Generalization**:
  - **Broad Exposure**: Train on diverse alphabets to ensure generalization to novel alphabets.
  - **Enhanced Feature Learning**: Exposure to various features improves accurate classification with minimal examples.
### Model Training Overview

1. **Setup**:
   - Utilized TensorFlow decorators for efficient graph operations.

2. **Gradient Recording**:
   - Employed `tf.GradientTape()` to automatically monitor operations for differentiation.

3. **Data Handling**:
   - Split input images into `X` (anchor-positive or anchor-negative pairs) and `y` (binary labels: 1 for similar, 0 for different).

4. **Model Forward Pass**:
   - Passed data through the Siamese Model to generate predictions based on current parameters.

5. **Loss Calculation**:
   - Computed binary cross-entropy loss between predicted and true labels to distinguish between the two classes.

6. **Backpropagation**:
   - Calculated gradients of the loss with respect to model parameters to guide weight updates.

7. **Parameter Update**:
   - Applied calculated gradients using a pre-configured optimizer to update model weights, minimizing loss.
### Embedding
 Embeddings are the interconnections between the discrete-categorial-dynamic to a list of continuous numbers. In the context of our Siamese model, embeddings are the low-dimensional, trained continuous list representations of unique and discrete variables. They aid in reducing the dimensionality of the input data while maintaining meaningful representations of the categories in the transformed space.
### Siamese Model

| Layer (Type)      | Output Shape    | Param   | Connected To                                   |
|-------------------|-----------------|---------|-----------------------------------------------|
| Input_img (inp)   | (None, 100, 100, 3) | 0       | []                                            |
| validation_img    | (None, 100, 100, 3) | 0       | []                                            |
| embedding         | (None, 4096)    | 38,960,448 | ['input_img[0][0]', 'validation_img[0][0]']    |
| l1_dist_11 (L1Dist)| (None, 4096)   | 0       | ['embedding[0][0]', 'embedding[0][1]']        |
| dense_2 (Dense)   | (None, 1)       | 4,097   | ['l1_dist_1[0][0]']                           |

### Embedding Model

| Layer (Type)      | Output Shape    | Param    |
|-------------------|-----------------|----------|
| Input_img (inp)   | (None, 100, 100, 3) | 0        |
| Conv2d            | (None, 91, 91, 64)  | 19,264   |
| max_pooling2d     | (None, 46, 46, 64)  | 0        |
| conv2d_1          | (None, 40, 40, 128) | 401,536  |
| max_pooling2d_1   | (None, 20, 20, 128) | 0        |
| conv2d_2          | (None, 17, 17, 128) | 262,272  |
| max_pooling2d_2   | (None, 9, 9, 128)   | 0        |
| con2d_3           | (None, 6, 6, 256)   | 524,544  |
| flatten           | (None, 9216)        | 0        |
| dense             | (None, 4096)        | 37,752,832 |

### Results
<div align="center"><img src="https://github.com/IIITManjeet/Face_Recognition/assets/96388375/ec8d3a75-3266-4e07-b13c-5c59dacf353c"></div>
<div align="center"><img src="https://github.com/IIITManjeet/Face_Recognition/assets/96388375/bc7faf61-5ea3-4339-8193-23cf581f8c56"></div>
<div align="center"><img src="https://github.com/IIITManjeet/Face_Recognition/assets/96388375/86928bdb-ab6a-4b9e-90dc-58a5cf22d3cc"></div>

