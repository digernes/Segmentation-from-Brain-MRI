# Segmentation-from-Brain-MRI
On splitting up by subjects:
================================

The data consists of brain MRI images of different patients. However some subjects in the data set have more than one image. These images should not be split between the training and validation sets. This would cause the model to be trained on data that is super similar to the data it will be validated on. The point of the validation set is to consist of unseen data for the model. Having the same subjects in both sets would be against this point. Therefore a solution is needed to split up the subjects to not overlap. 

The image data provided contains the subject ID at the beginning of the file name. 


The first part separated by a dash ('-') is used to separate between the different subjects.
Example file name:
|--------|
027_S_0307-I34159-brain-ax3.png


There are different ways to solve this. You could put all images with the same subject IDs in seperate folders. When adding images to the validation and training sets, you could add whole folders. 
Another solution is to pass a function to the DataBlock API that splits the images based on it's ID. In our case we found that around 27,5% of the images had an ID that started with 1, so these were used as the validation set. This is a quick fix to the problem, but it is not an optimal one. It can introduce unforseen biases since we don't know the full details on how the IDs are assigned. Furthermore it can become problematic if the dataset were to increase in number of elements and would cause an imbalance. 


Larger context: 
===================================
The task at hand is to detect  and partition the region of the ventricles in 2D mid-slice MRI images of the brain through image segmentation.. The data set is from ADNI (Alzheimer's Disease Neuroimaging Initiative). The goal is to achieve precise localization of this region. 

Image segmentation has an important role in computer-aided systems for medical diagnosis. Dividing an image into different areas based on a defined characteristic has a wide range of applications, which includes segmenting virtually all body organs as well as anomaly and border detection.


This repository:
===================================

This repository contains two notebooks. These two notebooks are nearly identical, with a few differences. The first notebook `1_segmentation_on_brain.ipynb` is trained on brain MRI images of the brain without any surrounding skull. The second notebook `2_segmentation_on_full_skull_orig.ipynb` is trained on the pictures of the whole skull. The second repository has some more things that the was not included in the first. These two models are trained in parallel so the results could be compared.

### Comparison of the results

Before training any of the models, the initial thought was that the model trained on the skull-stripped images would outperform the other. This is because the image has less irrelevant noise in the image that could distract while training. However after training both models for 16 epochs, there weren't huge differences in segmentation results. If the models would have been trained for even longer, a more conclusive answer could be gained. The differences weren't as large as expected.
