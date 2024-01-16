## Ablation study
***
* **Using pre-trained weights and larger models:** Leveraging pre-trained weights and larger models can improve benchmark results. Pre-trained weights simplify training, enhance performance, and reduce training time. We experimented with ImageNet pre-trained models and a larger model (small version of MaxVit with 68.9 million parameters) to potentially achieve better performance.
* **Dataset spliting and validation:** The dataset is divided into four classes based on embryo health and age (3 and 5 days), with an imbalanced distribution. To ensure accurate training evaluation, 20% of images from each class are used to create a representative validation set.

* **Splitting the images into two datasets:** To address dataset imbalance, we split the images into two separate datasets for class 0 and class 1 instead of using weighted loss functions. We applied stronger augmentations to class 1 images and ensured that during training, each batch contained an equal number of images from both datasets, effectively balancing the dataset.

* **Ensemble model:** We enhanced model performance by employing 5-fold cross-validation, each fold trained separately with the same hyperparameters. We combined results through majority voting, a resource-intensive but effective approach often used in competitions.

* **Changing the prediction threshold:** To mitigate class imbalance, we lowered the decision threshold for class 1 using the SoftMax function. In our experiments, we set the threshold to 0.58, allowing class 1 to be selected more frequently despite being the minority class.
* **Using the embryo's day:** The embryo's age was added as an extra feature to the model, alongside the image, to enhance diagnosis accuracy, acknowledging the distinct differences in embryos across different days.

* **Using 4 classes:** We expanded to 4 classes based on the image's day (D3 healthy, D3 infertile, D5 healthy, D5 infertile). We trained using 8 datasets, balancing batches, and also explored single-day models with two classes each.

* **Model soup:** "Model soup" in machine learning involves combining diverse models to improve performance, reducing overfitting and enhancing predictions. We experimented with this technique by combining our trained folds to reduce inference time and memory usage.
  
***
* **Comparison between methods:** The enhanced version reduces training time with a larger model due to increased memory allowing for bigger batch sizes, despite higher memory usage. It also achieves high scores more quickly by using pre-trained weights for faster complex pattern recognition. Inference times remain similar for both the enhanced and benchmark versions, with efficient CPU execution, except for the assembly variant which is slower.
***
* Link notebook: https://github.com/RazvanPanaite/Advanced-Methods-in-Embryo-Fertility-Classification/blob/main/Ablation_Notebook.ipynb

| Method | Public Score | Private Score | Public Place | Private Place |
|--------|--------------|---------------|--------------|---------------|
| SOTA public | **0.82758** | 0.54545 | **1** | 16 |
| SOTA private | 0.69565 | **0.61538** | 29 | **1** |
| MaxViT extended | 0.62857 | **0.61538** | 56 | **1** |
| Ensemble - best fold | 0.73333 | **0.60869** | 15 | **2** |
| Ensemble - threshold 0.58 | **0.75862** | 0.40000 | **7** | 77 |
| MaxViT 4 classes | 0.55555 | 0.42857 | 79 | 73 |
| ResNeSt 2 models | 0.62857 | 0.52173 | 56 | 28 |
| Model Soup | 0.70967 | **0.57142** | 25 | **10** |

