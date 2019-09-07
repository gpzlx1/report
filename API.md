# API

## data augmentation

### tensorflow

[`adjust_brightness(...)`](https://www.tensorflow.org/api_docs/python/tf/image/adjust_brightness): Adjust the brightness of RGB or Grayscale images.

[`adjust_contrast(...)`](https://www.tensorflow.org/api_docs/python/tf/image/adjust_contrast): Adjust contrast of RGB or grayscale images.

[`adjust_gamma(...)`](https://www.tensorflow.org/api_docs/python/tf/image/adjust_gamma): Performs Gamma Correction on the input image.

[`adjust_hue(...)`](https://www.tensorflow.org/api_docs/python/tf/image/adjust_hue): Adjust hue of RGB images.

[`flip_left_right(...)`](https://www.tensorflow.org/api_docs/python/tf/image/flip_left_right): Flip an image horizontally (left to right).

[`flip_up_down(...)`](https://www.tensorflow.org/api_docs/python/tf/image/flip_up_down): Flip an image vertically (upside down).

[`random_brightness(...)`](https://www.tensorflow.org/api_docs/python/tf/image/random_brightness): Adjust the brightness of images by a random factor.

[`random_contrast(...)`](https://www.tensorflow.org/api_docs/python/tf/image/random_contrast): Adjust the contrast of an image or images by a random factor.

[`random_crop(...)`](https://www.tensorflow.org/api_docs/python/tf/image/random_crop): Randomly crops a tensor to a given size.

[`random_flip_left_right(...)`](https://www.tensorflow.org/api_docs/python/tf/image/random_flip_left_right): Randomly flip an image horizontally (left to right).

[`random_flip_up_down(...)`](https://www.tensorflow.org/api_docs/python/tf/image/random_flip_up_down): Randomly flips an image vertically (upside down).

[`random_hue(...)`](https://www.tensorflow.org/api_docs/python/tf/image/random_hue): Adjust the hue of RGB images by a random factor.

[`random_jpeg_quality(...)`](https://www.tensorflow.org/api_docs/python/tf/image/random_jpeg_quality): Randomly changes jpeg encoding quality for inducing jpeg noise.

[`random_saturation(...)`](https://www.tensorflow.org/api_docs/python/tf/image/random_saturation): Adjust the saturation of RGB images by a random factor.

## data resize

### tensorflow

[`central_crop(...)`](https://www.tensorflow.org/api_docs/python/tf/image/central_crop): Crop the central region of the image(s).

[`crop_and_resize(...)`](https://www.tensorflow.org/api_docs/python/tf/image/crop_and_resize): Extracts crops from the input image tensor and resizes them.

[`draw_bounding_boxes(...)`](https://www.tensorflow.org/api_docs/python/tf/image/draw_bounding_boxes): Draw bounding boxes on a batch of images.

[`pad_to_bounding_box(...)`](https://www.tensorflow.org/api_docs/python/tf/image/pad_to_bounding_box): Pad `image` with zeros to the specified `height` and `width`.

[`resize(...)`](https://www.tensorflow.org/api_docs/python/tf/image/resize_images): Resize `images` to `size` using the specified `method`.

[`resize_area(...)`](https://www.tensorflow.org/api_docs/python/tf/image/resize_area): Resize `images` to `size` using area interpolation.

[`resize_bicubic(...)`](https://www.tensorflow.org/api_docs/python/tf/image/resize_bicubic)

[`resize_bilinear(...)`](https://www.tensorflow.org/api_docs/python/tf/image/resize_bilinear)

[`resize_image_with_crop_or_pad(...)`](https://www.tensorflow.org/api_docs/python/tf/image/resize_with_crop_or_pad): Crops and/or pads an image to a target width and height.

[`resize_image_with_pad(...)`](https://www.tensorflow.org/api_docs/python/tf/image/resize_image_with_pad): Resizes and pads an image to a target width and height.

[`resize_images(...)`](https://www.tensorflow.org/api_docs/python/tf/image/resize_images): Resize `images` to `size` using the specified `method`.

[`resize_nearest_neighbor(...)`](https://www.tensorflow.org/api_docs/python/tf/image/resize_nearest_neighbor)

[`resize_with_crop_or_pad(...)`](https://www.tensorflow.org/api_docs/python/tf/image/resize_with_crop_or_pad): Crops and/or pads an image to a target width and height.

[`rot90(...)`](https://www.tensorflow.org/api_docs/python/tf/image/rot90): Rotate image(s) counter-clockwise by 90 degrees.

## data alignment and normalization （standardization)

### tensorflow

[`per_image_standardization(...)`](https://www.tensorflow.org/api_docs/python/tf/image/per_image_standardization): Linearly scales `image` to have zero mean and unit variance.

## color space conversion

### tensorflow

[`hsv_to_rgb(...)`](https://www.tensorflow.org/api_docs/python/tf/image/hsv_to_rgb): Convert one or more images from HSV to RGB.

[`yiq_to_rgb(...)`](https://www.tensorflow.org/api_docs/python/tf/image/yiq_to_rgb): Converts one or more images from YIQ to RGB.

[`yuv_to_rgb(...)`](https://www.tensorflow.org/api_docs/python/tf/image/yuv_to_rgb): Converts one or more images from YUV to RGB.

[`rgb_to_grayscale(...)`](https://www.tensorflow.org/api_docs/python/tf/image/rgb_to_grayscale): Converts one or more images from RGB to Grayscale.

[`rgb_to_hsv(...)`](https://www.tensorflow.org/api_docs/python/tf/image/rgb_to_hsv): Converts one or more images from RGB to HSV.

[`rgb_to_yiq(...)`](https://www.tensorflow.org/api_docs/python/tf/image/rgb_to_yiq): Converts one or more images from RGB to YIQ.

[`rgb_to_yuv(...)`](https://www.tensorflow.org/api_docs/python/tf/image/rgb_to_yuv): Converts one or more images from RGB to YUV.

## image degradation

### tensorflow

[`grayscale_to_rgb(...)`](https://www.tensorflow.org/api_docs/python/tf/image/grayscale_to_rgb): Converts one or more images from Grayscale to RGB.

## illumination normalization and insensitive feature preprocessing