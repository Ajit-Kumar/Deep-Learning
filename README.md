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

Modelling

In this work I have used U-Net as based on my research, I found that it is the best model for
biomedical Image Segmentation. In this model is implemented using Keras functional API
as the model has layers that require multiple input/outputs.

Implementation of U-Net

Encoder

❖ Encoder has conv_block function which gets two inputs- input_tensor and
num_filters(feature channel). The blocks are linear stack of convolutional layers, a
batch normalisation layer, and then relu activation is applied to map the input and
output.
The conv_block function is called in the encoder_block and maxpooling and dropout
of 20% is applied on each layer.
❖ Max pooling in the encoder_block reduces spatial resolution of feature map by factor
of 2.
❖ Dropout of 20% is introduced at each convolutional layer being called in the encoder
block.
❖ To Keep the track of the output of each block as I feed these high-resolution feature
maps to the decoder.

Decoder

❖ The decoder function gets three inputs - input tensor, concatenated tensor and the
feature channel.
❖ Then a 2D convolution transpose layer in 1st block of decoder is applied with stride =
(2, 2) to perform up-sampling at the very first layer. Which means the input image gets
doubled after the very first block.
❖ The second block in the decoder concatenates the output of the encoder to decoder.
❖ Then 3rd and 4th block of decoder have a liner stack of convolution layer followed by
relu activation and dropout layer of 20%.


Final Convolutional layer

❖ Performs a 1x1 convolution along the channels for each individual pixel - outputs a
Final segmentation mask.

The above-mentioned U-Net was trained several numbers of times using different combination
likes:
❖ Dropout layer combination tried from (0.2-0.5)
❖ Epochs combination tried from (10-100)
❖ Different combination of learning rate
❖ Different sets of optimizers used like Adam

Blockers Faced

Few blockers faced during the implementation; I was fortunate enough to handle most of
them.
❖ Understanding the problem statement and dataset e.g. the 4th channel
❖ Figuring out the model to be used, as there are plenty of models and U-Net being
the obvious choice I wanted to explore more and get the best out to address the
given problem.
❖ Channel conversion of masked image (conversion of p mode image to four RGBA
channels for balanced overlaying/prediction).
❖ The biggest drawback of deep learning models is that they take a lot of memory
for processing. As expected even I faced the resource exhaust error and session
crashed in google Collaboratory due to a large batch size. To handle this, I reduced
the batch size from 32 to 8. 

Conclusion

The proposed approach uses U-Net which a popular model for semantic segmentation in
medical applications. The total images provided are 560 and I took the 20% as validation set.
This states the model is being trained on 448 images that is not enough for a model to be
robust and maintain the consistency. Though I have calculated dice coefficient to which is
used to validate the volumetric segmentation of the medical images, there is a high possibility
the output may vary as we run the model time and again.

Future Work and steps for improvement

For future and step for improvement we can do the below mentioned things.
❖ One possible approach is by using transfer learning, by using pretrained model only to
replace the encoder block of the U-Net architecture.
❖ The second possible approach is to get more data and use the same approach as
proposed above. Bringing in more data will increase the robustness of the model.
❖ Carefully augmenting the data as medical images need high precision and one wrong
parameter can affect the accuracy of the model drastically
