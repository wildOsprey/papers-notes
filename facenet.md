## FaceNet: A Unified Embedding for Face Recognition and Clustering
*Florian Schroff, Dmitry Kalenichenko, James Philbin*

[Link to the paper](https://arxiv.org/abs/1503.03832)

### Research Direction

Face Recognition, Face Verification


### Abstract / Brief Introduction

Authors presented a system, called AlexNet, for face recognition, face verification and clustering tasks using a deep convolutional network (convnet) trained with triplets of roughly aligned matching / non-matching face patches. They also introduced the concept of harmonic embeddings and a harmonic triplet loss.


### Research Focus

One of the main goals of face verification and face recognition problems is that you need to make your system flexible. Imagine that you have a team and a face recognition or verification system. You trained your convnet to know who is who and everything is all right. But when you have a new member, you will need to train your network again. This is not very efficient. Authors offer one of possible solutions of this problem, using some ideas from DeepFace[4].


### Research Methodology

The method is based on learning Euclidean embedding per image using a deep convolutional network.

It is also known as **Siamise Network**[2, 3]. A Siamese Network is a type of neural network architecture that learns how to differentiate between two inputs.

The network is trained in such a way that the squared L2 distances in the embedding space directly correspond to face similarity: faces of the same person have small distances and faces of distinct people have large distances.

![FaceNet Architecture](https://github.com/wildOsprey/papers_notes/blob/master/images/facenet/facenet_architecture.png)
*Figure 1. FaceNet Architecture*


To train, they used triplets of roughly aligned matching / non-matching face patches. A triplet is a collection of one anchor image, one matching image and one non-matching image to the anchor image. The goal is to *minimize* the distance between anchor image and matching image and maximize the distance between anchor image and non-matching image.

![The Triplet Loss in action](https://github.com/wildOsprey/papers_notes/blob/master/images/facenet/triplet_loss.png)
*Figure 2. The Triplet Loss in action*


To do this, they defined *a triplet loss*. The loss is being minimized, when ![formula](https://github.com/wildOsprey/papers_notes/blob/master/images/facenet/formula.png)

So, to train neural network means to find this function .

As a result, when the system gets an input image, it encodes it with the help of convnet, calculates the distance between an encoding and the photos from the database and finds the minimal distance from all of them. The photo used to calculate this distance is a photo of our person.



### Data Collection / Data Analysis

For testing authors used Labeled Faces in the Wild (LFW)[5] and YouTube Faces DB[6] datasets.

As an architecture for their convnet authors tried two options: The Zeiler&Fergus[7] and the Inception[8].

The network, based on the Inception architecture showed better results. To train the CNN authors used Stochastic Gradient Descent (SGD) with standard backprop and Adaptive Gradient (AdaGrad). The margin is set to 0.2. Authors used 128 embedding dimensionality, they also tried 64, 256 and 512, but got worse results.


### Results

As a result, authors got a system for face recognition and verification with high accuracy (from 80 % to 89% depending on the convnet architecture). Also, their approach can be used for a clustering problem. 


### Advantages / Disadvantages

Pros:

	You do not need to train your network each time you add a new person to a database.

Cons:

	To train your convnet you need specific datasets.


### Useful Links

1. [Convolutional neural nets](https://www.coursera.org/learn/convolutional-neural-networks)
2. [Learning a Similarity Metric Discriminatively, with Application to Face Verification](http://yann.lecun.com/exdb/publis/pdf/chopra-05.pdf)
3. [Neural Networks - Siamese Network coursera lecture](https://www.youtube.com/watch?v=AKyHGzCSEK4)
4. [DeepFace: Closing the Gap to Human-Level Performance in Face Verification](https://www.cs.toronto.edu/~ranzato/publications/taigman_cvpr14.pdf)
5. [Labeled Faces in the Wild Home](http://vis-www.cs.umass.edu/lfw/)
6. [YouTube Faces](https://www.cs.tau.ac.il/~wolf/ytfaces/)
7. [Visualizing and Understanding Convolutional Networks](https://arxiv.org/pdf/1311.2901v3.pdf)





