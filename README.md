# Smart Agriculture – Plant Disease Detection Using Leaf Image Processing

An image-processing and deep learning-based project for identifying plant leaf diseases using the PlantVillage dataset and an EfficientNetB0 classification model.

## Project Overview

Plant diseases can affect crop quality, agricultural productivity, and food security. Early identification of plant diseases can help farmers take appropriate action and reduce potential crop losses.

This project explores plant disease identification from leaf images using image processing techniques and deep learning. It includes HSV-based leaf segmentation, color and texture feature extraction, and an EfficientNetB0-based image classification model.

The project is implemented using Python and Google Colab.

## Objectives

- Explore and analyse a plant leaf image dataset.
- Perform image preprocessing and resizing.
- Apply HSV-based color segmentation to isolate green leaf regions.
- Extract color and texture features using HSV histograms and GLCM.
- Build a plant disease classification model using EfficientNetB0.
- Train and fine-tune the model using transfer learning.
- Evaluate model performance using standard classification metrics.
- Predict the class of a newly uploaded leaf image.

## Technologies and Libraries

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| Google Colab | Development and execution environment |
| TensorFlow / Keras | Deep learning and model training |
| EfficientNetB0 | Transfer learning-based image classification |
| OpenCV | Image processing and segmentation |
| NumPy | Numerical operations |
| Pandas | Dataset organisation |
| Matplotlib | Data visualisation |
| Seaborn | Confusion matrix visualisation |
| Scikit-learn | Dataset splitting and evaluation |
| Scikit-image | GLCM texture feature extraction |

## Dataset

**Dataset:** PlantVillage Dataset

**Source:** [PlantVillage Dataset on Kaggle](https://www.kaggle.com/datasets/arjuntejaswi/plant-village)

The project notebook uses the Kaggle dataset identifier:

`arjuntejaswi/plant-village`

Dataset details in the project run:

- Total images: 20,638
- Number of classes: 15
- Training images: 14,446
- Validation images: 3,096
- Testing images: 3,096

The dataset contains healthy and diseased leaf images from pepper, potato, and tomato plants.

**Note:** The dataset is not included in this repository. Users must obtain it from Kaggle and follow the dataset provider's terms and licensing conditions.

## Project Workflow

The project follows these major steps:

1. **Environment Setup:** Import the required libraries and configure the Google Colab environment.
2. **Dataset Collection:** Configure Kaggle API access and download the PlantVillage dataset.
3. **Dataset Exploration:** Inspect image folders, identify disease classes, count images, and visualise sample images.
4. **Dataset Splitting:** Divide the dataset into training (70%), validation (15%), and testing (15%) subsets using stratified splitting.
5. **Image Preprocessing:** Resize images to 224 × 224 pixels and prepare TensorFlow datasets.
6. **HSV-Based Segmentation:** Convert leaf images into HSV color space and create a green-region segmentation mask.
7. **Feature Extraction:** Extract color histogram features from HSV images and texture features using the Gray-Level Co-occurrence Matrix (GLCM).
8. **Model Building:** Build an EfficientNetB0-based classification model with data augmentation and a classification layer.
9. **Class Weight Calculation:** Calculate class weights to help address differences in class sample counts.
10. **Model Training:** Train the classification model using transfer learning.
11. **Fine-Tuning:** Unfreeze selected EfficientNetB0 layers and continue training with a lower learning rate.
12. **Model Evaluation:** Evaluate the selected model using accuracy, precision, recall, F1-score, and a confusion matrix.
13. **New Image Prediction:** Upload a leaf image and predict its class using the trained model.
14. **Model Saving:** Save the trained model and class-name mapping for later use.

**Methodology note:** HSV segmentation and HSV + GLCM feature extraction are included as separate image-processing demonstrations in the current notebook. The EfficientNetB0 classifier is trained directly on the preprocessed RGB images; the handcrafted feature vector is not concatenated with the EfficientNetB0 input.

## Model Architecture

The classification model uses **EfficientNetB0**, a convolutional neural network pre-trained on ImageNet.

The model includes:

- Pre-trained EfficientNetB0 feature extractor
- Data augmentation
- Global Average Pooling
- Batch Normalization
- Dropout
- Softmax classification layer

The training process is performed in two stages:

- **Stage 1 – Transfer Learning:** The pre-trained EfficientNetB0 base layers are frozen while the classification head is trained.
- **Stage 2 – Fine-Tuning:** The last 30 layers of the base model are made trainable, while Batch Normalization layers remain frozen.

Training callbacks include Early Stopping, ReduceLROnPlateau, and Model Checkpointing.

## Model Performance

The following results were recorded in the project notebook:

| Evaluation Metric | Result |
|---|---:|
| Test Accuracy | 96.74% |
| Macro Precision | 95.94% |
| Macro Recall | 96.67% |
| Macro F1-Score | 96.23% |

These are the results from the recorded experiment. Results may vary when the notebook is executed again because of differences in the runtime environment, training process, and model initialisation.

## How to Run the Project

### 1. Open the Notebook

Open `Plant_Disease_Detection.ipynb` using Google Colab.

### 2. Enable GPU

In Google Colab:

- Open **Runtime → Change runtime type**.
- Select **T4 GPU**, if available.
- Save the runtime settings.

### 3. Configure Kaggle API

Create or download your Kaggle API token from your Kaggle account settings.

Upload `kaggle.json` when the notebook asks for it.

**Security warning:** Never upload `kaggle.json` to GitHub or share it publicly.

### 4. Run the Notebook

Execute the notebook cells in order, starting from Environment Setup and continuing through Model Saving.

The notebook installs the required libraries, downloads the dataset, prepares the images, trains the model, evaluates its performance, and supports prediction on a new leaf image.

### 5. Test a New Image

At the prediction section, upload a leaf image when prompted. The model will display the predicted class and its confidence score.

## Repository Structure

```text
Plant-Disease-Detection/
│
├── README.md
├── Plant_Disease_Detection.ipynb
├── requirements.txt
├── .gitignore
│
├── results/
│   ├── class_distribution.png
│   ├── segmentation_result.png
│   ├── training_graph.png
│   └── confusion_matrix.png
│
└── docs/
    └── project_report.pdf
```

The `results/` and `docs/` folders are optional. Add them only when the corresponding files are available.

## Limitations

- The model recognises only the 15 classes included in the training dataset.
- It may not correctly identify diseases that are not represented in the dataset.
- PlantVillage images may differ from real-world field images in lighting, background, and image quality.
- The confidence score is a model output and should not be treated as a guarantee of diagnosis.
- The HSV segmentation method focuses on green regions and may exclude some yellow or brown disease-affected areas.
- The current handcrafted color and texture features are not integrated into the EfficientNetB0 classifier.

## Future Improvements

- Test the model on leaf images captured in real agricultural environments.
- Explore additional plant disease datasets.
- Improve segmentation to preserve disease-affected leaf regions.
- Experiment with other CNN architectures.
- Integrate handcrafted color and texture features into a hybrid classification pipeline.
- Develop a simple web application for uploading leaf images and viewing predictions.

## Applications

- Educational demonstration of digital image processing.
- Plant leaf image classification.
- Experimentation with transfer learning.
- Agricultural disease identification research.

## Author

**Riya Dey**

BCA Honours – Computational Sciences

## Acknowledgements

- PlantVillage dataset contributors.
- TensorFlow and Keras documentation.
- OpenCV and Scikit-image communities.
- Scikit-learn documentation.

## Disclaimer

This project is developed for educational and academic purposes. Its predictions should not replace professional agricultural inspection or expert plant disease diagnosis.
