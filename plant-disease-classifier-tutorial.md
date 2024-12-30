
###  Step I: create an Azure AI Services resource
From the Azure Portal, search the Azure AI multi-service account and create an account.


### Create a Custom Vision AI project

Navigate to the [custom vision portal](https://www.customvision.ai/projects) to create a custom vision project.

We created a project with:

* Name:  `paddy-disease-bejo`

* Project Type - Classification. Since we are classifying whether the image is having `bacterial_leaf_blight`, `bacterial_leaf_streak` , `bacterial_panicle_blight` , `blast` , `brown spot` , `dead heart` , `downy mildew` , `hispa` , `normal` and `tungro`

* Classification Type:  `Multiclass`. There are 2 choices here, Multiclass and Multilabel. We choose `Multiclass` since the image is associated with only one class ( `bacterial_leaf_blight`, `bacterial_leaf_streak` , `bacterial_panicle_blight` , `blast` , `brown spot` , `dead heart` , `downy mildew` , `hispa` , `normal` and `tungro`). A single image is not associated with multiple classes.

If a single image was associated with multiple classes, then we had to choose the Classification type as Multilabel.



### Add Images
We upload the `bacterial_leaf_blight` images and also tag them.

<image> 

We also add images of other classes: `bacterial_leaf_streak` , `bacterial_panicle_blight` , `blast` , `brown spot` , `dead heart` , `downy mildew` , `hispa` , `normal` and `tungro`

### Train the a model based on the training set 
In Azure Custom Vision, the Quick Training and Advanced Training options offer different levels of control and customization over the model training process. Here's a breakdown of their differences:

#### Quick Training
 
* Purpose: Quick Training is designed for ease of use and speed. It is suitable for rapid prototyping and getting results quickly without needing to configure many details.

* Configuration: Minimal configuration is required. The system automatically selects default training parameters that are generally effective for many tasks.

* Speed: As the name suggests, it aims to provide faster results. It's useful when you want to quickly iterate on model development or when you have a small dataset.

* Use Case: Best for initial experiments, smaller datasets, or when you need a quick evaluation of model performance without diving deep into customization.

#### Advanced Training
 

* Purpose: Advanced Training offers more control and customization over the training process, allowing you to tailor the model to potentially achieve better performance on specific tasks.

* Configuration: Provides options to adjust various training parameters, such as the number of iterations, learning rate, and more. This allows you to fine-tune the model based on your data and requirements.

* Flexibility: You can choose to use more computational resources and longer training times to potentially improve model accuracy.
Use Case: Best for refining models, larger datasets, or when specific training optimizations are needed to meet performance goals.

#### Choosing Between Them
Quick Training is ideal when you're starting out, experimenting with new ideas, or working with smaller datasets.
Advanced Training is more suitable when you need to optimize the model's performance for production use, have a larger and more complex dataset, or need specific configurations that the Quick Training option does not cover.

Ultimately, the choice between Quick and Advanced Training will depend on your project's specific needs, including the complexity of the data, the required performance, and how much time you are willing to invest in model development and optimization.

If you choose the `Quick training` you will see something like that 

<image>

If we choose Advanced Training to train the model, we will see the various iterations and the potential improvement after each iteration. 

For this demo we choose the quick training option. This is the output from the quick training option   

<image>

In the picture, you see three key metrics used to evaluate the performance of a machine learning model for image classification: Precision, Recall, and AP (Average Precision). Here's what each of these metrics means in simple terms:

#### Precision
* <strong>Definition</strong>.: Precision is the percentage of correctly predicted positive results out of all positive predictions made by the model.
<strong>Simple Explanation</strong>.: It tells you how often the model's predictions are correct when it says an image belongs to a certain class.
<strong>Example</strong>.: If the model predicts 100 images as a certain disease, and 95 of them are actually correct, the precision is 95%.

#### Recall

<strong>Definition</strong>: Recall is the percentage of actual positive cases that were correctly identified by the model.
<strong>Simple Explanation</strong>: It measures how well the model finds all the images that truly belong to a certain class.
<strong>Example</strong>: If there are 100 actual images of a disease, and the model correctly identifies 94 of them, the recall is 94%.

#### AP (Average Precision)

Definition: AP combines precision and recall into a single metric that summarizes the model's performance across different threshold levels.
Simple Explanation: It provides an overall measure of the model's ability to identify classes correctly, considering both precision and recall.
Example: A higher AP means the model is generally good at both identifying true positives and minimizing false positives across various thresholds.
Performance Per Tag
In the table, you see the performance metrics (Precision, Recall, AP) for each specific class or "tag" in your dataset, along with the image count for each class. This helps you understand how well the model performs for each specific category.

Precision, Recall, and AP per Tag: Indicates how accurately and completely the model identifies each specific type of image, like "bacterial leaf streak" or "blast."

Understanding these metrics helps you evaluate how well your model is performing and where it might need improvement. For instance, if a particular class has low recall, you might need more training data for that class or to adjust the model to better capture those cases.