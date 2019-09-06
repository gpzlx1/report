#	preprocess of TF-slim

##	[cifarnet](https://github.com/tensorflow/models/blob/master/research/slim/preprocessing/cifarnet_preprocessing.py)

For training:

1. transform the image to floats
2. pad the image with zero from [ input_height, input_width, channel ] to [ 4 + input_height + 4, 4 + input_width + 4, channel ]
3. randomly crop a  [ height, width ]  section of the image
4. randomly flip the image horizontally
5. adjust the brightness of the image by a random factor.
6. adjust the contrast of the image by a random factor.
7. subtract off the mean and divide by the variance of the pixels ( standardization )

For evaluating:

1. transform the image to floats
2. resize the image with crop or pad operation
3. subtract off the mean and divide by the variance of the pixels ( standardization )

Note:	

​	standardization uses `tf.image.per_image_standardization(image）`function which  computes `(x - mean) / adjusted_stddev`, where `x` is each pixel and `mean` is the average of all values in image, and `adjusted_stddev = max(stddev, 1.0/sqrt(iamge.NumElements))`.

##	inception

## [lenet](https://github.com/tensorflow/models/blob/master/research/slim/preprocessing/lenet_preprocessing.py)

1. transform the image to floats

2. resize the image with crop or pad operation

3. each pixel is  subtracted by 128.0 and divided by 128.0 ( standardization )

##	[vgg](https://github.com/tensorflow/models/blob/master/research/slim/preprocessing/vgg_preprocessing.py)


