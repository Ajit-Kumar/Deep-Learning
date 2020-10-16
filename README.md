# Deep-Learning
Semantic Segmentation Using Deep Learning

Pixel-wise image segmentation is a well-studied problem in medical domain. The task of semantic image segmentation is to classify each pixel in the image. 
❖ Input: Images
❖ Output: Recognizing, understanding what is in the image in pixel level. Assign a class
label to each pixel (Semantic Segmentation), but do not differentiate instances.

Data Understanding
Dataset details are mentioned below:
❖ total of 560 images of size 512x512 in png format.
❖ 280 images of normal tissue (colour mode ‘RGBA’)
❖ 280 images of annotation mask. (colour mode ‘P’)
❖ For each normal tissue there is annotation mask.
❖ Image annotation was done using semantic segmentation techniques.
❖ It has four classes 

Data Cleaning and preparation
Data cleaning and preparation is an important part, as it can improve the quality of the data
and in doing so, increases the overall productivity of the models.
The normal tissue and annotated mask image were separated and kept into two separate
folders and the file name of the input image and the corresponding segmentation image were
kept same.
Steps mentioned below were taken on raw images and annotated mask(labels)
❖ Annotated image is converted to RGBA format.
❖ NumPy array of the images and annotated mask is created for further processing.
❖ Normalization is applied on the generated NumPy arrays.
❖ The data is splitted into 80:20 ratio in training and testing set, respectively.
