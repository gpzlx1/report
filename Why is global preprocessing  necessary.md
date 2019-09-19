# Why is global preprocessing  necessary?

## A brief introduction to training and preprocessing

###	Preprocessing

The preprocessing of images is mainly to achieve the following objectives:

* The image size needs to be adapted to the network input requirements. Several mainstream CNN models have fixed image input size requirements. Like the VGG model, the input images are all 224 * 224 resolution
* The picture format needs to be adapted to the network training requirements. Some neural network training frameworks may only support images in jpeg format. So in some cases, you must convert the format of the image. Some neural networks may be trained in RGB space, which requires that all images be in RGB format.
* Reasonably divide the training set and the verification set.
* Make the necessary corrections to the data set distribution. If the training data is extremely unbalanced, then operations such as undersampling or oversampling or replenishment need to be done in order to prevent the model results from being biased towards large data categories.
* Extract data features. Some deep learning precision relies heavily on certain operations on the image, such as face recognition, which must first perform a data alignment operation (to  find out the part of the face in the image)

additional:

* Data augmentation. Extend the data set and improve the generalization ability of the model by cutting data, flipping, adjusting image parameters, etc.
* data normalization
* Process the data into a specific storage format, such as record. The record format facilitates sequential reading, which is disk and memory friendly and can  accelerate neural network training greatly.



###	Training

This is mainly based on supervised learning (all pictures have a label).

* Training set: using for training CNN, updating parameters

* Evaluation set: using to verify the generalization ability of the model in the training process, update the hyperparameter

  > (hyperparameter, refers to the learning rate and other artificially set model training parameters)

* Loss function: used to measure the deviation of the data set real label and neural network prediction results.

The neural network uses the **(batch)** **gradient descent** to update the parameters. The main training processes are:

1. Train the model on the training set

2. Calculate the loss function of the training set

3. Use chain rules to derive results and adjust the parameters of each layers

4. if epoch > epoch_num || model is convergent

   ​	go to 9;

   if epoch % N == 0; 

   ​	go to 5;

   else 

   ​	go to 1;

   > Simply, one epoch is an iteration


5. Verify the model by using a evaluation set
6. Calculate the loss function of evaluation set
7. Adjust the hyperparameter according to the loss function (such as reducing the learning rate)
8. go to 1
9. stop

Unsupervised learning is similar, except that there may be  no validation set.

## Why is there a global preprocessing before training？

It is feasible to form part of the lightweight image preprocessing and training model into a pipeline, and has achieved considerable improvement. For example, an open source machine learning architecture **MXNet** merges some lightweight pre-processing operations into the data prefetch during the training, reducing the time for global pre-processing without reducing training speed.

**But global image preprocessing is inevitable and worthwhile.**

There are three reasons:

1. Some image pre-processing operations need only be done once, such as resize  and jpeg compression operations, which usually reduce the size of the image, making the disk bandwidth less stressful during training.

2. When it comes to massive training data, even if only resize and compressed pictures are read, the disk bandwidth may still be the bottleneck in training process, especially in HDD. At this point, it is necessary to convert the data set to record file format. It compactly packs the data for efficient read and writes from distributed file system like Hadoop HDFS and AWS S3. 

   > Turning the data to record format will take up a lot of time

3. Some CNN models may use more complicated preprocessing methods (relatively rare)

About image preprocessing, different machine learning architectures have different policies. For example, `tensorflow` tends to complete all image pre-processing operations before training, while `MXnet` puts preprocessing operations in the training process as much as possible, but even so, global preprocessing is inevitable, especially generating data records.

[More detail about MXnet record](https://mxnet.apache.org/versions/master/architecture/note_data_loading.html)



## A trend：Transfer learning

> Transfer learning is a popular method in computer vision because it allows us to **build accurate models in a timesaving way** (Rawat & Wang 2017). With transfer learning, instead of starting the learning process from scratch, you start from patterns that have been learned when solving a different problem. This way you leverage previous learnings and avoid starting from scratch. Take it as the deep learning version of [Chartres](https://en.wikipedia.org/wiki/Standing_on_the_shoulders_of_giants)’ expression ‘standing on the shoulder of giants’.

Transfer learning using the pre-train model can spend only several hours to converge even on a big data set. But preprocessing of big data set can also spend dozens of minutes and even several hours. It seems necessary to speed up the preprocessing.

**However, talk is cheap, we need more experiments.**

