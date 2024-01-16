## Benchmark Performance
***
* Weighted loss function: A weighted loss function is used to address the imbalance in a dataset with 124 healthy (class 1) and 716 infertile embryos (class 0), giving higher weight to class 1 to reduce bias.

* Dataset spliting and validation: The dataset is divided into four classes based on embryo health and age (3 and 5 days), with an imbalanced distribution. To ensure accurate training evaluation, 20% of images from each class are used to create a representative validation set.

* Data augmentation: The dataset, containing only 840 images, was expanded using various augmentations, including a Random Augmentation function and a custom resize function to maintain aspect ratios. Normalization was adjusted based on the mean and standard deviation of the augmented images. Additionally, CutOut augmentation was used, as it proved effective for this dataset.

* Models used: ResNeSt-14 and MaxVit-Tiny

* Loss function and Optimizer: The experiments utilized a weighted CrossEntropy loss function for unbalanced data and soft labels for improved generalization. The Sharpness-Aware Minimization (SAM) optimizer was used for better generalization, though it increased training time due to its two-step update process.

* Using the embryo's day: The embryo's age was added as an extra feature to the model, alongside the image, to enhance diagnosis accuracy, acknowledging the distinct differences in embryos across different days.

* Test Time Augmentations: Test Time Augmentations were used to improve model performance by generating 20 augmented versions of each test image. The model then classified these images, and the most common class assigned was used as the final result, providing multiple perspectives of the same image.

* Hyperparameters: Hyperparameters included a batch size of 16, a learning rate of 0.0001, image size of 224x224 pixels, 2 augmentations from RandAugment, 1000 epochs of training with 4 dataloader workers, and a weight decay of 0.005.

***
* Kaggle notebook: https://www.kaggle.com/code/serbandoncean/notebookc3c3ecb67a?scriptVersionId=158972769
* Score:
    * Public test set: 0.58823 (68th place)
    * Private test set: 0.54545 (16th place)
