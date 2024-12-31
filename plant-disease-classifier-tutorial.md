# 🌟 Plant Disease Detection With Azure Custom Vision
  
Welcome to this enhanced tutorial on setting up a Custom Vision AI project using Azure AI Services. Let's dive in and make it efficient and enjoyable! 🚀  
This tutorial of the use of Azure Custom Vision multi-class classifier to develop a solution a disease diagnostic system to automatically Automated and Preventive Paddy Disease Diagnosis System

![ Preventive Plant Disease Diagnosis System](/img/00-image.png)

Azure Custom Vision is a no code interface for building, training and deploying Image Classification or Object Detection models. www.customvision.ai

[Documentation:](https://docs.microsoft.com/en-us/azure/cognitive-services/custom-vision-service/)

Azure Custom Vision API, uses a combination of deep learning models underneath. These models are optimized for different types of image classification tasks and leverage frameworks such as `PyTorch` or `TensorFlow` for backend processing. Microsoft doesn't publicly disclose the exact models used, as they often employ a mix of architectures, including:

- **ResNet (Residual Networks):** ResNet architectures are commonly used due to their strong performance on image classification tasks. Variants like ResNet-50 or ResNet-101 may be part of the implementation.

- **EfficientNet:** EfficientNet models are highly efficient in terms of accuracy vs. computation trade-off and are likely leveraged for better performance on custom datasets.

- **Vision Transformers (ViTs):** For newer capabilities, Vision Transformers may be integrated for more complex feature extraction and generalization.

- **MobileNet:** For scenarios where edge deployment is a priority, lightweight models like MobileNet may be employed.

Azure Custom Vision focuses on enabling quick training and evaluation, so the models are often pre-trained on large datasets like ImageNet and fine-tuned on custom data provided by users. The system applies techniques like transfer learning and automated model selection to tailor the training process to the specific dataset and task, such as object detection or multi-label classification.


# Let Get Started
    
## **Step 1: Create an Azure AI Services Resource**  
  
Begin by accessing the **Azure Portal**. Search for the *Azure AI services* and proceed to create a service.  
  
## **Create a Custom Vision AI Project**  
  
Head over to the [Custom Vision Portal](https://www.customvision.ai/projects) to initiate your custom vision project. Here's a setup guide for our sample project:  
  
- **Project Name:** `paddy-disease-bejo`  
- **Project Type:** *Classification* - This project aims to classify images into one of the following categories: `bacterial_leaf_blight`, `bacterial_leaf_streak`, `bacterial_panicle_blight`, `blast`, `brown spot`, `dead heart`, `downy mildew`, `hispa`, `normal`, and `tungro`.  
- **Classification Type:** *Multiclass* - Choose Multiclass since each image belongs to only one category. If an image could belong to multiple categories, you would select *Multilabel*.  

![Create a project](/img/01-image.png)

## **Add Images**  
  
Upload images for each class, starting with `bacterial_leaf_blight`, and tag them accordingly. Don't forget to include images for the other categories: `bacterial_leaf_streak`, `bacterial_panicle_blight`, `blast`, `brown spot`, `dead heart`, `downy mildew`, `hispa`, `normal`, and `tungro`. 📷  

![Upload the images through the portal](/img/02-image1.jpg)


![Add the training images](/img/02-image2.png)


## **Train the Model**  
  
Azure Custom Vision offers two training options: **Quick Training** and **Advanced Training**.  

  ![Train the model](/img/03-image.png)
  ![Train the model](/img/04-image.png)


### **Quick Training**  
  
- **Purpose:** Ideal for speed and ease, especially for rapid prototyping.  
- **Configuration:** Minimal setup with default parameters.  
- **Speed:** Fast results, perfect for small datasets and quick iterations.  
- **Use Case:** Best for initial experiments or quick evaluations.  

   ![Quick Training](/img/05-image.png)

### **Advanced Training**  
  
- **Purpose:** Offers detailed control for tailored model training.  
- **Configuration:** Fine-tune parameters like iterations and learning rate.  
- **Flexibility:** Adjust resources and training duration for better accuracy.  
- **Use Case:** Suitable for refining models and handling larger datasets.  
   
   ![Advanced Training](/img/06-image.png)

### **Choosing Between Them**  
  
- **Quick Training:** Perfect for beginners and small datasets.  
- **Advanced Training:** Optimal for production-level models and complex datasets.  

----------------------------------------------------------------------------------------------------------------------------------------------  
For this demo, we'll use **Quick Training**. Here's a glimpse of the metrics after training:  

 ![Training Results](/img/07-image.png)

### **Key Metrics:**  
- **Precision:** Correct positive predictions out of all positive predictions.  
- **Recall:** Correct identification of actual positive cases.  
- **AP (Average Precision):** Combines precision and recall for a holistic view.  
  
### **Performance Per Tag:**  
  
Evaluate metrics like Precision, Recall, and AP for each class. This helps identify areas needing improvement, such as increasing training data for classes with low recall.  
  
## **Model Evaluation and Iteration**  
  
Upon training completion, assess the model with a separate test image set. Iterate if needed to enhance accuracy, either by tweaking parameters or adding more data.  
  
- **Quick Test:** Upload a plant image and observe the predictions.  
- **View Predictions:** Check model performance and adjust as necessary.  

  ![Test the API](/img/08-image.png)

## **Deployment and Integration**  
  
Once satisfied, deploy the model to integrate with applications used by agricultural experts. Use the Custom Vision service's APIs for seamless integration.  
  
- **Publish:** Set the model name and prediction resource, then publish.  
- **Access Prediction URL:** Obtain the Prediction Key for API access.  
  
 ![Publish the model for use](/img/09-image.png)


## Use the training API in combination with  Custom Vision Training package
## Use the *training* API

The Custom Vision portal provides a convenient user interface that you can use to upload and tag images, and train models. However, in some scenarios you may want to automate model training by using the Custom Vision training API.

> **Note**: In this exercise, you can choose to use the API from either the **C#** or **Python** SDK. In the steps below, perform the actions appropriate for your preferred language.

1. In Visual Studio Code, in the **Explorer** pane, browse to the **07-custom-vision-image-classification** folder and expand the **C-Sharp** or **Python** folder depending on your language preference.
2. Right-click the **train-classifier** folder and open an integrated terminal. Then install the Custom Vision Training package by running the appropriate command for your language preference:

**C#**

```
dotnet add package Microsoft.Azure.CognitiveServices.Vision.CustomVision.Training --version 2.0.0
```

**Python**

```
pip install azure-cognitiveservices-vision-customvision==3.1.0
```

3. View the contents of the **train-classifier** folder, and note that it contains a file for configuration settings:
    - **C#**: appsettings.json
    - **Python**: .env

    Open the configuration file and update the configuration values it contains to reflect the endpoint and key for your Custom Vision *training* resource, and the project ID for the classification project you created previously. Save your changes.
4. Note that the **train-classifier** folder contains a code file for the client application:

    - **C#**: Program.cs
    - **Python**: train-classifier.py

    Open the code file and review the code it contains, noting the following details:
    - Namespaces from the package you installed are imported
    - The **Main** function retrieves the configuration settings, and uses the key and endpoint to create an authenticated **CustomVisionTrainingClient**, which is then used with the project ID to create a **Project** reference to your project.
    - The **Upload_Images** function retrieves the tags that are defined in the Custom Vision project and then uploads image files from correspondingly named folders to the project, assigning the appropriate tag ID.
    - The **Train_Model** function creates a new training iteration for the project and waits for training to complete.
5. Return the integrated terminal for the **train-classifier** folder, and enter the following command to run the program:

**C#**

```
dotnet run
```

**Python**

```
python train-classifier.py
```
    
6. Wait for the program to end. Then return to your browser and view the **Training Images** page for your project in the Custom Vision portal (refreshing the browser if necessary).
7. Verify that some new tagged images have been added to the project. Then view the **Performance** page and verify that a new iteration has been created.

## Publish the image classification model

Now you're ready to publish your trained model so that it can be used from a client application.

1. In the Custom Vision portal, on the **Performance** page,  click **&#128504; Publish** to publish the trained model with the following settings:
    - **Model name**: fruit-classifier
    - **Prediction Resource**: *The **prediction** resource you created previously which ends with "-Prediction" (<u>not</u> the training resource)*.
2. At the top left of the **Project Settings** page, click the *Projects Gallery* (&#128065;) icon to return to the Custom Vision portal home page, where your project is now listed.
3. On the Custom Vision portal home page, at the top right, click the *settings* (&#9881;) icon to view the settings for your Custom Vision service. Then, under **Resources**, find your *prediction* resource which ends with "-Prediction" (<u>not</u> the training resource) to determine its **Key** and **Endpoint** values (you can also obtain this information by viewing the resource in the Azure portal).

## Use the *training* API

The Custom Vision portal provides a convenient user interface that you can use to upload and tag images, and train models. However, in some scenarios you may want to automate model training by using the Custom Vision training API.

> **Note**: In this exercise, you can choose to use the API from either the **C#** or **Python** SDK. In the steps below, perform the actions appropriate for your preferred language.

1. In Visual Studio Code, in the **Explorer** pane, browse to the **07-custom-vision-image-classification** folder and expand the **C-Sharp** or **Python** folder depending on your language preference.
2. Right-click the **train-classifier** folder and open an integrated terminal. Then install the Custom Vision Training package by running the appropriate command for your language preference:

**C#**

```
dotnet add package Microsoft.Azure.CognitiveServices.Vision.CustomVision.Training --version 2.0.0
```

**Python**

```
pip install azure-cognitiveservices-vision-customvision==3.1.0
```

3. View the contents of the **train-classifier** folder, and note that it contains a file for configuration settings:
    - **C#**: appsettings.json
    - **Python**: .env

    Open the configuration file and update the configuration values it contains to reflect the endpoint and key for your Custom Vision *training* resource, and the project ID for the classification project you created previously. Save your changes.
4. Note that the **train-classifier** folder contains a code file for the client application:

    - **C#**: Program.cs
    - **Python**: train-classifier.py

    Open the code file and review the code it contains, noting the following details:
    - Namespaces from the package you installed are imported
    - The **Main** function retrieves the configuration settings, and uses the key and endpoint to create an authenticated **CustomVisionTrainingClient**, which is then used with the project ID to create a **Project** reference to your project.
    - The **Upload_Images** function retrieves the tags that are defined in the Custom Vision project and then uploads image files from correspondingly named folders to the project, assigning the appropriate tag ID.
    - The **Train_Model** function creates a new training iteration for the project and waits for training to complete.
5. Return the integrated terminal for the **train-classifier** folder, and enter the following command to run the program:

**C#**

```
dotnet run
```

**Python**

```
python train-classifier.py
```
    
6. Wait for the program to end. Then return to your browser and view the **Training Images** page for your project in the Custom Vision portal (refreshing the browser if necessary).
7. Verify that some new tagged images have been added to the project. Then view the **Performance** page and verify that a new iteration has been created.

## Publish the image classification model

Now you're ready to publish your trained model so that it can be used from a client application.

1. In the Custom Vision portal, on the **Performance** page,  click **&#128504; Publish** to publish the trained model with the following settings:
    - **Model name**: fruit-classifier
    - **Prediction Resource**: *The **prediction** resource you created previously which ends with "-Prediction" (<u>not</u> the training resource)*.
2. At the top left of the **Project Settings** page, click the *Projects Gallery* (&#128065;) icon to return to the Custom Vision portal home page, where your project is now listed.
3. On the Custom Vision portal home page, at the top right, click the *settings* (&#9881;) icon to view the settings for your Custom Vision service. Then, under **Resources**, find your *prediction* resource which ends with "-Prediction" (<u>not</u> the training resource) to determine its **Key** and **Endpoint** values (you can also obtain this information by viewing the resource in the Azure portal).

## Use the image classifier from a client application

Now that you've published the image classification model, you can use it from a client application. Once again, you can choose to use **C#** or **Python**.

1. In Visual Studio Code, in the **07-custom-vision-image-classification** folder, in the subfolder for your preferred language (**C-Sharp** or **Python**), right- the **test-classifier** folder and open an integrated terminal. Then enter the following SDK-specific command to install the Custom Vision Prediction package:

**C#**

```
dotnet add package Microsoft.Azure.CognitiveServices.Vision.CustomVision.Prediction --version 2.0.0
```

**Python**

```
pip install azure-cognitiveservices-vision-customvision==3.1.0
```

> **Note**: The Python SDK package includes both training and prediction packages, and may already be installed.

2. Expand the **test-classifier** folder to view the files it contains, which are used to implement a test client application for your image classification model.
3. Open the configuration file for your client application (*appsettings.json* for C# or *.env* for Python) and update the configuration values it contains to reflect the endpoint and key for your Custom Vision *prediction* resource, the project ID for the classification project, and the name of your published model (which should be *fruit-classifier*). Save your changes.
4. Open the code file for your client application (*Program.cs* for C#, *test-classification.py* for Python) and review the code it contains, noting the following details:
    - Namespaces from the package you installed are imported
    - The **Main** function retrieves the configuration settings, and uses the key and endpoint to create an authenticated **CustomVisionPredictionClient**.
    - The prediction client object is used to predict a class for each image in the **test-images** folder, specifying the project ID and model name for each request. Each prediction includes a probability for each possible class, and only predicted tags with a probability greater than 50% are displayed.
5. Return the integrated terminal for the **test-classifier** folder, and enter the following SDK-specific command to run the program:

**C#**

```
dotnet run
```

**Python**

```
python test-classifier.py
```

6. View the label (tag) and probability scores for each prediction. You can view the images in the **test-images** folder to verify that the model has classified them correctly.

## More information

For more information about image classification with the Custom Vision service, see the [Custom Vision documentation](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/).