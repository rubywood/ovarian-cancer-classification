### UBC Ovarian Cancer Subtype Classification and Outlier Detection (UBC-OCEAN) - Kaggle competition entry
Navigating Ovarian Cancer: Unveiling Common Histotypes and Unearthing Rare Variants

This Kaggle competition was set up to classify ovarian cancer subtypes from histopathology images, with a focus on generalisability across medical centres. Hence, in training my deep learning model, I carefully chose data augmentations to mimic possible images from other centres, and upsampled minority classes to ensure they would not be forgotten about by the model.

The general approach used here is to mask and patch the images, extract patch features using a pretrained histology model, train a simple model to classify these features, using the mode to get a slide-level prediction, and finally train an outlier detection model for use at inference.

Due to the nature of the Kaggle challenge, I wrote Python code in self-contained Jupyter Notebooks.

The notebooks are ordered and described here:
- ```1 Explore Metadata``` looks at the labels and data provided, exploring distributions
- ```2 Review Images``` loads and considers the images, including whole slide images (WSIs) and tissue microarrays (TMAs)
- ```3 Save as tiff``` saves each png image as a tiff file to help load the large images during training
- ```4 Mask TMAs``` uses traditional imaging techniques to develop an algorithm to mask out background for the TMAs
- ```5 Patch Images``` saves the coordinates of the image patches to save time during training
- ```6 Augment Data``` visualises possible augmentations to use on the images
- ```7 Construct Feature Model``` sets up the pretrained feature encoder model
- ```8 Train Decoder Model``` trains an MLP with dropout to classify the patch features
- ```9 Train Outlier Detection Model``` tests decoder model using mode for slide-level prediction and trains a one class SVM to detect outliers

Learnings and future work:
- Used OpenSlide initially but pyvips worked better on Kaggle.
- For training, pre-saved tissue patch coordinates and masked images as tiff files, using OpenSlide to load. For inference, sampled and checked patches in real time, loading using pyvips.
- With more time I would implement a more sophisticated MIL method e.g. an attention model

This entry received a bronze-level score in the final competition grading.

Link to Kaggle competition:
https://www.kaggle.com/competitions/UBC-OCEAN/overview 