# Neural Codes for Image Retrieval

#### Part of Assignment of Deep Learning Course (2IMM10) at TU/e 


## Objective

### Data: Tiny Imagenet 

Use the training set of [Tiny Imagenet](https://tiny-imagenet.herokuapp.com/), consisting of 200 classes, with 500 images per class (total 100, 000 images), each image being of dimensions 64 × 64 RGB. The Jupyter notebook already gets the data for you, and also performs the following steps.

> Split the 200 classes into two sets, one containing 190 classes and the other containing the remaining 10 classes.
> Shuffle the set with 190 classes and divide it into training, validation, and test sets, according to the proportions 80/10/10. These will be used to train, validate and test the model.
> The set with the remaining 10 classes serves as out-of-domain (ood) data, used for image retrieval.
> Normalize pixel values to [0, 1].

### Task 1: Implement ConvNet
Implement a modified version of the ConvNet architecture from [Babenko et al.](/reading/neural_codes_for_image_retrieval.pdf):
* Layer 1, use kernel size 4 × 4 (instead of 11 × 11) and stride 1 (instead of 4).
* For the hidden fully connected layers, Layer 6 and Layer 7, use 2048 units (instead of 4096).
* Consult the paper for the rest of the architecture.
* For all pooling layers, use a window size of 3 × 3 and stride 2.
* Apply dropout with rate 0.5 before Layer 6 and Layer 7.

### Task 2: Train and Evaluate ConvNet

* Train the model by optimizing cross-entropy on the training set with the Adam optimizer, using a learning rate of 0.0001 and a batch size of 100. Set Adam’s flag amsgrad to True.
* Train for maximal 100 epochs and perform early stopping, by monitoring the loss on the validation set, and terminating training as soon as it starts to increase.
* Evaluate and report the train, validation and test performance, in terms of cross-entropy, classification accuracy and top-5 classification accuracy.
* Name two techniques which would likely improve the test accuracy.

### Task 3: Image Retrieval

Use the trained ConvNet to perform image retrieval on the ood data. When using a certain image as query image, the remaining 4, 999 images should serve as a retrieval date base. Perform image retrieval using neural codes from the same 3 layers which were also used in the paper by [Babenko et al.](/reading/neural_codes_for_image_retrieval.pdf) Compare the results.

* Obtain neural codes for each image in the ood data.
* Normalize the codes to have unit length.
* For the first 10 images in the ood set, find the respectively 5 closest3 images in the data base. Plot the query image next to the 5 retrieved images (sorted from most to least similar) and mark the images which have the same class as the query image (see Fig. 2 and 3 in the paper).
* What are the qualitative differences between the different layers for neural codes?
* Compute and report the mean average precision (mAP) over the whole ood set, for each of the 3 layers.
* Do the observed mAP values (roughly) confirm the observations by [Babenko et al.](/reading/neural_codes_for_image_retrieval.pdf)?