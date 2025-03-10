# Glioma-MDC-2025-ISBI
This repository refers to my attempt in a recently finished competition in Kaggle - Glioma-MDC 2025 (ISBI). Check my README and the link to the competition:
https://www.kaggle.com/competitions/glioma-mcd-2025/overview

![example_image.jpeg](https://github.com/sumone-compbio/Glioma-MDC-2025-ISBI-/blob/main/example_image.jpeg)

My method for this research problem:

(1) Since each image can have multiple regions of interest (ROIs) i.e. labelled mitosis or non-mitosis, I extracted the ROIs from the images using the coordinates of ROIs given in each image's corresponding JSON file.

(2) I tried several pre-trained CNN architectures, including ResNet50, ResNeXt50, InceptionNet, EfficientNet-B, DenseNet121, VGG16, VGG19, and even the Vision Transformer (ViT). Among them, VGG19 stood out with an impressive F1-score of 0.944 on the held-out test set, ranking me 12th in the competition.

(3) Beyond using VGG19, my methodology includes common practices:

    (a) Stratified sampling to maintain the balance of labels in both the train and the validation set.
    (b) Transforming train set (resize, flips, rotation, and normalisation only).
    (c) Since each image in the dataset can have a variable number of ROIs, a custom collate function is created which flattens all ROIs and labels into uniform standard tensors.
    (d) I tried freezing and training several layers in the VGG19 architecture but the best results were obtained by training the classifier layer only by gradually reducing the linear layer by batch-normalisation, dropout, and
        and GELU as an activation function. 
    (e) I used BCEWithLogitsLoss as the loss function and Adam optimizer, with ReduceLROnPlateau as the scheduler to adjust the learning rate when the validation loss starts flattening.
    (f) Beyond accuracy, and F1 score, I checked on other evaluation parameters including, balanced accuracy, MCC, roc-auc, sensitivity, specificity, etc. to ensure my model is learning both the classes well.
    (g) Saved the model from the epoch where the maximum F1-Score is achieved.
    (h) Got the predictions on the test set and submitted the results.

    
