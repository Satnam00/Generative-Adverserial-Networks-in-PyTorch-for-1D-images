# Generative-Adverserial-Networks-in-PyTorch
Deep neural networks are used mainly for supervised learning: classification or regression. Generative Adverserial Networks or GANs, however, use neural networks for a very different purpose: Generative modeling  Generative modeling is an unsupervised learning task in machine learning that involves automatically discovering and learning the regularities or patterns in input data in such a way that the model can be used to generate or output new examples that plausibly could have been drawn from the original dataset.

While there are many approaches used for generative modeling, a Generative Adverserial Network takes the following approach:
 
![6NMdO9u](https://user-images.githubusercontent.com/39052765/85935734-9692b100-b911-11ea-884e-805bc00d5aa7.png)

There are two neural networks: a Generator and a Discriminator. The generator generates a "fake" sample given a random vector/matrix, and the discriminator attempts to detect whether a given sample is "real" (picked from the training data) or "fake" (generated by the generator). Training happens in tandem: we train the discriminator for a few epochs, then train the generator for a few epochs, and repeat. This way both the generator and the discriminator get better at doing their jobs. This rather simple approach can lead to some astounding results. The following images for instances, were all generated using GANs:

<img width="555" alt="h" src="https://user-images.githubusercontent.com/39052765/85935861-bc6c8580-b912-11ea-8cf3-2d4a37733d15.png">

Most of the code for this tutorial has been borrowed for this excellent repository of PyTorch tutorials: github.com/yunjey/pytorch-tutorial.

## Dataset Used
MNIST Dataset
http://yann.lecun.com/exdb/mnist/

## Here's what we're going to do:
1. Define the problem statement
2. Load the data (with transforms and normalization)
3. Denormalize for visual inspection of samples
4. Define the Discriminator network
5. Study the activation function: Leaky ReLU
6. Define the Generator network
7. Explain the output activation function: TanH
8. Look at some sample outputs
9. Define losses, optimizers and helper functions for training
10. For discriminator
11. For generator
12. Train the model
13. Save intermediate generated images to file
14. Look at some outputs
15. Save the models
16. Commit to Jovian.ml

## Discriminator Network
The discriminator takes an image as input, and tries to classify it as "real" or "generated". In this sense, it's like any other neural network. While we can use a CNN for the discriminator, we'll use a simple feedforward network with 3 linear layers to keep things since. We'll treat each 28x28 image as a vector of size 784.

## Discriminator Training
Since the discriminator is a binary classification model, we can use the binary cross entropy loss function to quantify how well it is able to differentiate between real and generated images.

![d](https://user-images.githubusercontent.com/39052765/85935983-115ccb80-b914-11ea-8b6d-334ccae3141b.jpg)

## Leaky ReLu activation function
We use the Leaky ReLU activation for the discriminator.


![01](https://user-images.githubusercontent.com/39052765/85935947-ad3a0780-b913-11ea-906b-423632271a3d.png)

Different from the regular ReLU function, Leaky ReLU allows the pass of a small gradient signal for negative values. As a result, it makes the gradients from the discriminator flows stronger into the generator. Instead of passing a gradient (slope) of 0 in the back-prop pass, it passes a small negative gradient. - Source

Just like any other binary classification model, the output of the discriminator is a single number between 0 and 1, which can be interpreted as the probability of the input image being fake i.e. generated

## Here are the steps involved in training the discriminator.
1.We expect the discriminator to output 1 if the image was picked from the real MNIST dataset, and 0 if it was generated.
2.We first pass a batch of real images, and compute the loss, setting the target labels to 1.
3.Then, we generate a batch of fake images using the generator, pass them into the discriminator, and compute the loss, setting the target labels to 0.
4.Finally we add the two losses and use the overall loss to perform gradient descent to adjust the weights of the discriminator.
5. It's important to note that we don't change the weights of the generator model while training the discriminator (d_optimizer only affects the D.parameters())

## Generator Training
Since the outputs of the generator are images, it's not obvious how we can train the generator. This is where we employ a rather elegant trick, which is to use the discriminator as a part of the loss function. 

Here's how it works:
1. We generate a batch of images using the generator, pass the into the discriminator.
2. We calculate the loss by setting the target labels to 1 i.e. real. We do this because the generator's objective is to "fool" the discriminator.
3. We use the loss to perform gradient descent i.e. change the weights of the generator, so it gets better at generating real-like images.
