# ✨ Plant Disease Detection With Azure Custom Vision

Welcome to this enhanced tutorial on setting up a Custom Vision AI project using Azure AI Services. Let’s dive in and make it efficient and enjoyable! 🚀

This tutorial demonstrates how to use Azure Custom Vision’s multi-class classifier to develop an automated and preventive system for diagnosing plant diseases.

![Preventive Plant Disease Diagnosis System](/img/00-image.png)

Azure Custom Vision is a no-code interface for building, training, and deploying image classification or object detection models. Visit [Custom Vision](https://www.customvision.ai) to learn more.

For detailed documentation, see the [Azure Custom Vision documentation](https://docs.microsoft.com/en-us/azure/cognitive-services/custom-vision-service/).

## 🔧 Features of Azure Custom Vision
Azure Custom Vision uses deep learning models optimized for image classification tasks. Some of the commonly used architectures include:

- **ResNet (Residual Networks):** Effective for image classification tasks, with variants like ResNet-50 and ResNet-101.
- **EfficientNet:** Known for balancing accuracy and computational efficiency.
- **Vision Transformers (ViTs):** Suitable for advanced feature extraction and generalization.
- **MobileNet:** Lightweight models ideal for edge deployments.

Azure Custom Vision leverages transfer learning and automated model selection to adapt pre-trained models (e.g., on ImageNet) to your custom datasets.

---

## 🌱 Getting Started

### **Step 1: Create an Azure AI Services Resource**

Begin by accessing the **Azure Portal**. Search for "Azure AI Services" and create a new service resource.

### **Step 2: Create a Custom Vision Project**

Visit the [Custom Vision Portal](https://www.customvision.ai/projects) to start your project. Set up the following:

- **Project Name:** `paddy-disease-bejo`
- **Project Type:** *Classification*
- **Classification Type:** *Multiclass* (each image belongs to one category).
- **Tags:** Categories include `bacterial_leaf_blight`, `bacterial_leaf_streak`, `bacterial_panicle_blight`, `blast`, `brown spot`, `dead heart`, `downy mildew`, `hispa`, `normal`, and `tungro`.

![Create a Project](/img/01-image.png)

### **Step 3: Add Images**

Upload and tag images for each class. Start with `bacterial_leaf_blight` and repeat for all categories.

![Upload Images Through the Portal](/img/02-image1.jpg)
![Add Training Images](/img/02-image2.png)

### **Step 4: Train the Model**

Azure Custom Vision offers two training modes: **Quick Training** and **Advanced Training**.

![Train the Model](/img/03-image.png)
![Train the Model](/img/04-image.png)

#### **Quick Training**
- **Purpose:** Ideal for rapid prototyping.
- **Configuration:** Minimal setup with default parameters.
- **Speed:** Fast results for small datasets.
- **Use Case:** Quick evaluations.

#### **Advanced Training**
- **Purpose:** Provides more control over training parameters.
- **Configuration:** Customize iterations, learning rate, and resources.
- **Flexibility:** Suitable for larger datasets or refined models.
- **Use Case:** Production-level accuracy.

#### **Choosing Between Modes**
- **Quick Training:** Great for beginners or small datasets.
- **Advanced Training:** Best for complex datasets or high-accuracy needs.

For this tutorial, we’ll use **Quick Training**. Here are sample metrics after training:

![Training Results](/img/07-image.png)

### **Key Metrics**
- **Precision:** Proportion of correct positive predictions.
- **Recall:** Proportion of actual positives correctly identified.
- **AP (Average Precision):** Combines precision and recall.

### **Performance Per Tag**
Evaluate each class’s metrics to identify areas for improvement. Increase training data for low-recall categories.

---

## 🎮 Model Evaluation and Iteration

After training, evaluate the model using a separate test image set. Iterate to improve accuracy:
- **Quick Test:** Upload a plant image and check predictions.
- **View Predictions:** Adjust parameters or add data if needed.

![Test the API](/img/08-image.png)

---

## 📡 Deployment and Integration

### **Deployment**
Once satisfied with the model, deploy it for integration with applications:
- **Publish:** Specify the model name and prediction resource.
- **Access Prediction URL:** Use the Prediction Key for API access.

![Publish the Model for Use](/img/09-image.png)

### **Integration**
Use the Custom Vision service’s APIs to integrate the deployed model into client applications.

---

## 🔧 Automate Model Training with the Custom Vision API

To automate model training, use the Custom Vision Training API:

1. Install the Python SDK:
   ```bash
   pip install azure-cognitiveservices-vision-customvision==3.1.0
   ```

2. Update configuration settings (e.g., endpoint, key, project ID) in a `.env` file.

3. Use the SDK to:
   - Upload and tag images programmatically.
   - Create training iterations.
   
4. Train the model:
   ```python
   from azure.cognitiveservices.vision.customvision.training import CustomVisionTrainingClient
   
   trainer = CustomVisionTrainingClient(training_key, endpoint)
   trainer.create_images_from_files(project_id, images)
   trainer.train_project(project_id)
   ```

5. Verify training results in the Custom Vision portal.

---

## 🌐 Publish the Image Classification Model

### Steps to Publish:
1. In the Custom Vision portal, navigate to the **Performance** page.
2. Click **Publish** and specify the model name and prediction resource.
3. Use the published model’s endpoint and key to make predictions.

---

## 🔍 Testing the Image Classifier

### Test Predictions
Use the prediction API to test the model on new images. Retrieve predicted tags and their confidence scores to validate model performance.

