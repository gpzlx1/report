# Preprocessing ------ midterm report

Deep convolutional neural networks have achieved great successes in the academy & industry domains. Current treads in the applications of deep CNN shows that its possibilities in the real-world are endless. Nowadays, deep CNN plays a significant and irreplaceable role in computer vision. It is well known that the preprocessing of raw images is very important which directly influences the accuracy and training speed of deep CNN. However, so many preprocessors is there. This article attempts to find the commonality of preprocessing in  main deep CNN model ( like `Inception`, `VGG`, `resnet`, `etc`. ) and tries to abstract the operations of image preprocessing in some open source machine learning library (`tensorflow`, `MXnet`, `pyTorch`, etc) 

##	The conventional & unconventional preprocessors

the preprocessors of image can be divided roughly into the conventional and the unconventional. They are all following.

###	Conventional preprocessors

####	data augmentation

> Recent advances in deep learning models have been largely attributed to the quantity and diversity of data gathered in recent years. Data augmentation is a strategy that enables practitioners to significantly increase the diversity of data available for training models, without actually collecting new data. Data augmentation techniques such as cropping, padding, and horizontal flipping are commonly used to train large neural networks.

####	data normalization （standardization)

> Broadly speaking, the reason we normalize the images is to make the model converge faster. When the data is not normalized, the shared weights of the network have different calibrations for different features, which can make the cost function to converge very slowly and ineffectively. Normalizing the data makes the cost function much easier to train.

###	Unconventional preprocessors

#### color space conversion

Many CNN models take the images as input in the form of RGB images and classify them without modifying them. There are some researches show the  great impact of the color space conversion on the accuracy of model. Therefore, it is necessary sometimes to convert the color space of images

#### image degradation

Image degradation is to reduce the bit depth of images to reduce calculation and speed up training and inference.

#### illumination normalization and insensitive feature preprocessing

These preprocessors are usually applied in face recognition.

> For  face  images  acquired  at  different  spectral  bands,  the effects of spatial variation in sensitivity of camera systems, is likely to occur.  To minimize the variability effect for the face images  of  the  same  class, rgbGELog and commonly used  illumination  normalization  techniques  are employed. Other  approaches, such  as LN and  CFSP, involve the extraction of illumination-insensitive features. These types of feature  preprocessors  mostly  enhance edges  as  opposed  to low-level features. To output a color image with HE, LN and CFSP,  a  color  image  version  of  the  preprocessors  is  used. Given  an  RGB  image,  each  channel  plane  is  processed   

## Commonality of preprocessing in main deep CNN model

Although the size and depth of several major CNN models differ greatly, there are commonality in the preprocessing of data. According to the summary of the `tf-slim` library, the main CNN models adopt four preprocessing methods:

* `vgg_preprocessing`
* `inception_preprocessing`
* `cifarnet_preprocessing`
* `lenet_preprocessin`

> ```
> preprocessing_fn_map = {
>       'cifarnet': cifarnet_preprocessing,
>       'inception': inception_preprocessing,
>       'inception_v1': inception_preprocessing,
>       'inception_v2': inception_preprocessing,
>       'inception_v3': inception_preprocessing,
>       'inception_v4': inception_preprocessing,
>       'inception_resnet_v2': inception_preprocessing,
>       'lenet': lenet_preprocessing,
>       'mobilenet_v1': inception_preprocessing,
>       'mobilenet_v2': inception_preprocessing,
>       'mobilenet_v2_035': inception_preprocessing,
>       'mobilenet_v2_140': inception_preprocessing,
>       'nasnet_mobile': inception_preprocessing,
>       'nasnet_large': inception_preprocessing,
>       'pnasnet_mobile': inception_preprocessing,
>       'pnasnet_large': inception_preprocessing,
>       'resnet_v1_50': vgg_preprocessing,
>       'resnet_v1_101': vgg_preprocessing,
>       'resnet_v1_152': vgg_preprocessing,
>       'resnet_v1_200': vgg_preprocessing,
>       'resnet_v2_50': vgg_preprocessing,
>       'resnet_v2_101': vgg_preprocessing,
>       'resnet_v2_152': vgg_preprocessing,
>       'resnet_v2_200': vgg_preprocessing,
>       'vgg': vgg_preprocessing,
>       'vgg_a': vgg_preprocessing,
>       'vgg_16': vgg_preprocessing,
>       'vgg_19': vgg_preprocessing,
>   }
> ```

### [cifarnet](https://github.com/tensorflow/models/blob/master/research/slim/preprocessing/cifarnet_preprocessing.py)

For training:

1. transform the image to floats
2. pad the image with zero from [ input_height, input_width, channel ] to [ 4 + input_height + 4, 4 + input_width + 4, channel ]
3. randomly crop a  [ out_height, out_width ]  section of the image
4. randomly flip the image horizontally
5. adjust the brightness of the image by a random factor.
6. adjust the contrast of the image by a random factor.
7. subtract off the mean and divide by the variance of the pixels ( standardization )

For evaluating:

1. transform the image to floats
2. resize the image centrally with crop or pad operation
3. subtract off the mean and divide by the variance of the pixels ( standardization )

Note:	

​	standardization uses `tf.image.per_image_standardization(image）`function which  computes `(x - mean) / adjusted_stddev`, where `x` is each pixel and `mean` is the average of all values in image, and `adjusted_stddev = max(stddev, 1.0/sqrt(iamge.NumElements))`.

### [inception](https://github.com/tensorflow/models/blob/master/research/slim/preprocessing/inception_preprocessing.py)

Notes:

- image: 3-D Tensor of image. If dtype is tf.float32 then the range should be [0, 1], otherwise it would converted to tf.float32 assuming that the range is [0, MAX], where MAX is largest positive representable number for int(8/16/32) data type (see `tf.image.convert_image_dtype` for details).

For training:

1. if data type is integer, transform the image to floats between 0 and 1
2. randomly crop the image
3. resize the image to the specified height and width. There are 1 or 4 way s to do it.
   - 1 (fast model) : Bilinear interpolation
   - 4 : Bilinear interpolation+ Nearest neighbor interpolation + Bicubic interpolation + Area interpolation.
4. randomly flip the image horizontally
5. Randomly distort the colors. There are 4 ways to do it.
   - 1 (fast model) : random_brightness + random_saturation
   - 4 ：random_brightness + random_saturation + random_hue + random_contrast
6. convert the pixel value to [ -1, 1 ]

For evaluating:

1. if data type is integer, transform the image to floats between 0 and 1
2. centrally crop the image with an area containing 87.5% of the original image
3. resize the image to the specified height and width
4. convert the pixel value to [ -1, 1 ] 

### [lenet](https://github.com/tensorflow/models/blob/master/research/slim/preprocessing/lenet_preprocessing.py)

1. transform the image to floats
2. centrally resize  the image with crop or pad operation
3. each pixel is  subtracted by 128.0 and divided by 128.0

### [vgg](https://github.com/tensorflow/models/blob/master/research/slim/preprocessing/vgg_preprocessing.py)

Notes:

- the color space of image should be RGB

For training:

1. resize the image  preserving the original aspect ratio by scaling the smallest side to a random number in [ 256, 512 ] 
2. randomly crop a  [ out_height, out_width ]  section of the image
3. transform the new image to floats
4. randomly flip the new image horizontally
5. subtract the given means from each new image channel. The given means is [ R_MEAN, G_MEAN, B_MEAN] which value is [ 123.68, 116.78, 103.94 ]

For evaluating:

1. resize the image  preserving the original aspect ratio by scaling the smallest side to a random number in [ 256, 512 ] 
2. centrally crop a  [ out_height, out_width ]  section of the image
3. transform the new image to floats
4. subtract the given means from each new image channel. The given means is [ R_MEAN, G_MEAN, B_MEAN] which value is [ 123.68, 116.78, 103.94 ]

###	summary

Although there are differences in the methods of data preprocessing, they mainly use data augmentation and data alignment and normalization [ standardization ].

For training: 

|           | Tofloats       | resize the image with crop or pad or interpolation | data augmentation                                            | normalization   \| standardization                           |
| --------- | -------------- | -------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| cifarnet  | √              | √                                                  | random_flip_horizontally & random_brightness & random_contrast | standardization （ each image is standardized separately ）  |
| inception | √ ( to [0,1] ) | √                                                  | random_brightness & random_saturation [ & random_hue  & random_contrast ] | normalization（convert pixels value to [-1, 1] using y = 2.0 * (x - 0.5) ) |
| lenet     | √              | √                                                  | ×                                                            | normalization（convert pixels value to [-1, 1] using y = (x - 128.0) / 128.0  ) |
| vgg       | √              | √                                                  | random_flip_horizontally                                     | normalization ( subtract the means of ImageNet dataset in each channel ) |

The preprocessing for evaluating is similar but without data augmentation.

## Basic image operations API in open source machine learning library

We have calculated the API of basic operation of image preprocessing provided in `mxnet`, `tensorflow` and `pyTorch`, and formed the following table. These basic operations can be broadly divided into four categories :`data augmentation`, `data normalization` , `data resizing` and `color space conversion`.

With tables and statistics, an open source machine learning should provide at least the following functional interfaces:

* `data augmentation`: adjustment of  brightness & contrast & hue & saturation, rotation, horizontally flip
* `data resizing`: crop, pad, interpolation, resize
* `data normalization`: normalization

The open source machine learning library should also support image processing library like OpenCV2, in case the users want to using unconventional preprocessors.

| ops        | data augmentation |          |       |      |            |          |                   |                 |           |        |              | data resize |        |      |               |       | data  normalization (standardization) | color space conversion |                      |                  |                  |
| ---------- | ----------------- | -------- | ----- | ---- | ---------- | -------- | ----------------- | --------------- | --------- | ------ | ------------ | ----------- | ------ | ---- | ------------- | ----- | ------------------------------------- | ---------------------- | -------------------- | ---------------- | ---------------- |
| model      | brightness        | contrast | gamma | hue  | saturation | rotation | horizontally flip | vertically flip | pca_noise | affine | jpeg_quality | crop        | resize | pad  | interpolation | erase | normalization (standardization)       | hsv, yiq, yuv_to_rgb   | rgb_to_hsv, yiq, yuv | rgb_to_grayscale | grayscale_to_rgb |
| tensorflow | √                 | √        | √     | √    | √          | √        | √                 | √               |           |        | √            | √           | √      | √    | √             |       | √                                     | √                      | √                    | √                | √                |
| mxnet      | √                 | √        |       | √    | √          | √        | √                 |                 | √         |        |              | √           | √      | √    | √             |       | √                                     |                        |                      |                  |                  |
| pytorch    | √                 | √        | √     | √    | √          | √        | √                 | √               |           | √      |              | √           | √      | √    | √             | √     | √                                     |                        |                      | √                |                  |

[see basic api here](API.md)

[table_in_excel](basic_api.xlsx)

## Reference

[1.Understanding Unconventional Preprocessors in Deep Convolutional Neural Networksfor FaceIdentification](https://arxiv.org/abs/1904.00815)

[2.1000x Faster Data Augmentation](https://bair.berkeley.edu/blog/2019/06/07/data_aug/#targetText=Data)

[3.ColorNet: Investigating the importance of colorspaces for image classification⋆](https://arxiv.org/abs/1902.00267)
