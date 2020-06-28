# Generative-Adverserial-Networks-in-PyTorch
Deep neural networks are used mainly for supervised learning: classification or regression. Generative Adverserial Networks or GANs, however, use neural networks for a very different purpose: Generative modeling  Generative modeling is an unsupervised learning task in machine learning that involves automatically discovering and learning the regularities or patterns in input data in such a way that the model can be used to generate or output new examples that plausibly could have been drawn from the original dataset.

While there are many approaches used for generative modeling, a Generative Adverserial Network takes the following approach:
 
![6NMdO9u](https://user-images.githubusercontent.com/39052765/85935734-9692b100-b911-11ea-884e-805bc00d5aa7.png)

There are two neural networks: a Generator and a Discriminator. The generator generates a "fake" sample given a random vector/matrix, and the discriminator attempts to detect whether a given sample is "real" (picked from the training data) or "fake" (generated by the generator). Training happens in tandem: we train the discriminator for a few epochs, then train the generator for a few epochs, and repeat. This way both the generator and the discriminator get better at doing their jobs. This rather simple approach can lead to some astounding results. The following images for instances, were all generated using GANs:


                          


Most of the code for this tutorial has been borrowed for this excellent repository of PyTorch tutorials: github.com/yunjey/pytorch-tutorial. Here's what we're going to do:

Define the problem statement
Load the data (with transforms and normalization)
Denormalize for visual inspection of samples
Define the Discriminator network
Study the activation function: Leaky ReLU
Define the Generator network
Explain the output activation function: TanH
Look at some sample outputs
Define losses, optimizers and helper functions for training
For discriminator
For generator
Train the model
Save intermediate generated images to file
Look at some outputs
Save the models
Commit to Jovian.ml
