# 🌟 Azure AI Custom Vision Tutorial  
  
Welcome to this enhanced tutorial on setting up a Custom Vision AI project using Azure AI Services. Let's dive in and make it efficient and enjoyable! 🚀  
  
## **Step 1: Create an Azure AI Services Resource**  
  
Begin by accessing the **Azure Portal**. Search for the *Azure AI multi-service account* and proceed to create an account.  
  
## **Create a Custom Vision AI Project**  
  
Head over to the [Custom Vision Portal](https://www.customvision.ai/projects) to initiate your custom vision project. Here's a setup guide for our sample project:  
  
- **Project Name:** `paddy-disease-bejo`  
- **Project Type:** *Classification* - This project aims to classify images into one of the following categories: `bacterial_leaf_blight`, `bacterial_leaf_streak`, `bacterial_panicle_blight`, `blast`, `brown spot`, `dead heart`, `downy mildew`, `hispa`, `normal`, and `tungro`.  
- **Classification Type:** *Multiclass* - Choose Multiclass since each image belongs to only one category. If an image could belong to multiple categories, you would select *Multilabel*.  
  
## **Add Images**  
  
Upload images for each class, starting with `bacterial_leaf_blight`, and tag them accordingly. Don't forget to include images for the other categories: `bacterial_leaf_streak`, `bacterial_panicle_blight`, `blast`, `brown spot`, `dead heart`, `downy mildew`, `hispa`, `normal`, and `tungro`. 📷  
  
## **Train the Model**  
  
Azure Custom Vision offers two training options: **Quick Training** and **Advanced Training**.  
  
### **Quick Training**  
  
- **Purpose:** Ideal for speed and ease, especially for rapid prototyping.  
- **Configuration:** Minimal setup with default parameters.  
- **Speed:** Fast results, perfect for small datasets and quick iterations.  
- **Use Case:** Best for initial experiments or quick evaluations.  
  
### **Advanced Training**  
  
- **Purpose:** Offers detailed control for tailored model training.  
- **Configuration:** Fine-tune parameters like iterations and learning rate.  
- **Flexibility:** Adjust resources and training duration for better accuracy.  
- **Use Case:** Suitable for refining models and handling larger datasets.  
  
### **Choosing Between Them**  
  
- **Quick Training:** Perfect for beginners and small datasets.  
- **Advanced Training:** Optimal for production-level models and complex datasets.  
  
For this demo, we'll use **Quick Training**. Here's a glimpse of the metrics after training:  
  
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
  
## **Deployment and Integration**  
  
Once satisfied, deploy the model to integrate with applications used by agricultural experts. Use the Custom Vision service's APIs for seamless integration.  
  
- **Publish:** Set the model name and prediction resource, then publish.  
- **Access Prediction URL:** Obtain the Prediction Key for API access.  
  
Developers can leverage the model through the `azure-cognitiveservices-vision-customvision` SDK. For an example, refer to the provided Notebook.  
  
### **Integration Example:**  
  
Integrate the model into a Blazor web app:  
  
1. Clone the repository.  
2. Update `appsettings