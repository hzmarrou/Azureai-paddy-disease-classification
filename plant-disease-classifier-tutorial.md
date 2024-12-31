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

### Gather the project settings

The project you have created has been assigned a unique identifier, which you will need to specify in any code that interacts with it.

1. Click the settings (⚙) icon at the top right of the **Performance** page to view the project settings.

2. Under **General** (on the left), note the **Project Id** that uniquely identifies this project.

3. On the right, under **Resources** note that the key and endpoint are shown. These are the details for the training resource (you can also obtain this information by viewing the resource in the Azure portal).
Use the training API

### Use the Training API 

To automate model training, use the Custom Vision Training API.

* In Visual Studio Code, in the Explorer pane, browse to the `azure-custom-vision-python-sdk` folder and expand the `code` folder.

* Right-click the train-classifier folder and open an integrated terminal. Then install the Custom Vision Training package by running the appropriate command for your language preference:

1. Install the Python SDK:
   ```bash
   pip install azure-cognitiveservices-vision-customvision==3.1.0
   ```

2. Update configuration settings (e.g., endpoint, key, project ID) in a `.env` file.

3. Open the code file `train-classifier.py` in the **train-classifier** folder and review the code it contains, noting the following details:

   - Namespaces from the package you installed are imported.
   - The `main` function retrieves the configuration settings, and uses the key and endpoint to create an authenticated **CustomVisionTrainingClient**, which is then used with the project ID to create a Project reference to your project.
   - The `Upload_Images` function retrieves the tags that are defined in the Custom Vision project and then uploads image files from correspondingly named folders to the project, assigning the appropriate tag ID.
   - The `The Train_Model` function creates a new training iteration for the project and waits for training to complete.
   
4. Return the integrated terminal for the train-classifier folder, and enter the following command to run the program:

   ```python
   python train-classifier.py
   ```

5. Wait for the program to end. Then return to your browser and view the Training Images page for your project in the Custom Vision portal (refreshing the browser if necessary).

6. Verify that some new tagged images have been added to the project. Then view the Performance page and verify that a new iteration has been created.

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

1. Expand the test-classifier folder to view the files it contains, which are used to implement a test client application for your image classification model.

2. Open the configuration file for your client application ().env for Python) and update the configuration values it contains to reflect the endpoint and key for your Custom Vision prediction resource, the project ID for the classification project, and the name of your published model (which should be fruit-classifier). Save your changes.

3. Open the code file for your client application (`test-classification.py`) and review the code it contains, noting the following details:

* Namespaces from the package you installed are imported

* The `main` function retrieves the configuration settings, and uses the key and endpoint to create an authenticated CustomVisionPredictionClient.

* The prediction client object is used to predict a class for each image in the test-images folder, specifying the project ID and model name for each request. Each prediction includes a probability for each possible class, and only predicted tags with a probability greater than 50% are displayed.

4. Return the integrated terminal for the test-classifier folder, and enter the following SDK-specific command to run the program:
 ```python
   python test-classifier.py
   ```

5. View the label (tag) and probability scores for each prediction. You can view the images in the test-images folder to verify that the model has classified them correctly.   