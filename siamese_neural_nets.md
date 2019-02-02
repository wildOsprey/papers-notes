## Siamese Neural Networks for One-shot Image Recognition
*Gregory Koch, Richard Zemel, Ruslan Salakhutdinov*

[Link to the paper](http://www.cs.toronto.edu/~zemel/documents/oneshot1.pdf)


### Research Direction

Object Classification, Object Verification, Object Clusterization


### Abstract / Brief Introduction

The authors focus on a solution for the one-shot verification problem: identification new classes with the samples of these classes. For this task, they used siamese convolution neural network[1] with the modified distance layer.

 

### Research Focus

The one-shot learning problem appears when you have to correctly make predictions given only a single example of each new class. It can be solved by finding similarities between images, text or sound and used for clusterization, verification or classification tasks. 


### Research Methodology

A Siamese neural network consists of twin networks which accept distinct inputs but are joined by an energy function at the top. These twin networks also share the same weights. In Figure 1, the architecture of the neural network is represented. You can read about parameters details in the chapter 3.2 Learning.

![Conv architecture](https://github.com/wildOsprey/papers_notes/blob/master/images/siamese_nns/convolution_architecture.JPG)
*Figure 1. Convolution architecture selected for the verification task from the paper. Siamese twin is not shown but joins after the 4096 unit fully-connected layer where L1 distance is computed.*


Each input is processed to the feature vector with the shape (4096,). Then, they are joined with the L1 siamese distance layer, which calculates the weighted L1 distance between the vectors combined with a sigmoid activation, which maps onto the interval [0,1].
It is trained on pairs of images, each pair is labeled as same or different. As an output, the net gives a number that indicated how close the images are or in other words what is the probability that these two images belong to the same class.
There is a good and understandable example on Keras on github[2].



### Data Collection / Data Analysis


For training, the authors used the Omniglot dataset[3] (it has alphabet from Futurama!), which is consist of 30 alphabets for 20 pictures for each symbol of each alphabet. For testing, they used the Omniglot and MNIST dataset[4].

To create validation set, they created 10000 example pairs taken from 10 alphabets and 4 additional drawers. Also, they reserved the last 10 alphabets and 4 drawers for testing.

For the final one-shot verification test authors used a technique, developed by Lake[5]. It is a 20-way within-alphabet is first chosen from among those reserved for evaluation set, along with twenty characters taken uniformly at random. The authors repeated this twice so that they got 40 one-shot learning trials for each of the ten evaluation alphabets.



### Results

Figures 2 shows the one-shot results on MNIST dataset. As you can see, the accuracy of Convolutional Siamese Net is pretty good, so we can conclude that authors made a great job and got the results they expected.  

![best accuracy](https://github.com/wildOsprey/papers_notes/blob/master/images/siamese_nns/best_acc.jpeg)
*Figure 2. Best one-shot accuracy from different types of network*


### Advantages / Disadvantages

Pros:

	You don’t need to retrain your network to classify new class.

Cons:

	Time for calculations is bigger because you need to train network on pairs, so there are twice as many images. Also, for better results, you may form not random pairs, but with a more advanced algorithm.


### Useful Links

1. [What are Siamese neural networks, what applications are they good for, and why?](https://www.quora.com/What-are-Siamese-neural-networks-what-applications-are-they-good-for-and-why)
2. [implementation of Siamese Networks for One Shot Learning paper](https://github.com/Goldesel23/Siamese-Networks-for-One-Shot-Learning)
3. [Omniglot dataset](https://github.com/brendenlake/omniglot)
4. [MNIST dataset](http://yann.lecun.com/exdb/mnist/)
5. [One-shot learning by inverting a compositional causal process](https://cims.nyu.edu/~brenden/LakeEtAlNips2013.pdf)




