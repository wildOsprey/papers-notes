## Learning Video Object Segmentation from Static Images
*Anna Khoreva, Federico Perazzi, Rodrigo Benenson, Bernt Schiele, Alexander Sorkine-Hornung*

[Link to the paper](https://arxiv.org/abs/1612.02646)

### Research Direction

Computer Vision, Object Detection


### Abstract / Brief Introduction

Authors worked on one of the problems of computer vision: video object segmentation. The goal was to create an algorithm for object segmentation using state-of-art convolutional neural networks (convnets) and to find a way to apply training not on video sequences but on static images. For this purpose they revealed a new approach called **MaskTrack**.


### Research Focus

One of the problems of video object segmentation is that we need a sufficiently large body of densely, pixel-wise annotated video data for training. So the goal is to get rid of video data and try to use static images for training.

Another problem pops up when we are talking about implementation of such algorithms: to achieve coherent result we need to use too many global connections over multiple frames or even the whole video sequence. The way to fix this is to find a way to decrease a number of connections.


### Research Methodology

The main idea is that for each frame we use a mask from the previous frame to specify the object of interest so that the net is guided towards that object of interest. Authors called this approach the *guided instance segmentation*.

The algorithm is a combination of offline and online strategies. To create one, authors were inspired by GOTURN[3] and  MDNet[4].

Offline part consist of two stages. First one is to pre-train a convnet on ImageNet dataset for image labeling tasks. It is based on a VGG16 network. Second one is to train the network on MSRA10K dataset using deformation and coarsening on the image masks to produce accurate output masks from their rough estimates. As input the convnet receive an image expanded from RGB to RGB + mask channel, where RGB relates to current image and mask channel represents a rough estimate of the object mask. And as output we get an accurate segmentation of the object.

In online mode we fine-tune convnet for each frame to get an object segmentation using a current frame and a mask from the previous frame. For the first frame we generate previous mask by using deformations on ground truth of this image.

Authors called this full approach “MaskTrack”.

For training they use SGD with minibatches of 10 images and a polynomial learning policy with initial learning rate of 0.001. The momentum and weight decay are set to 0.9 and 0.0005, respectively. The network is trained for 20k iterations.

For the extra mask channel of ﬁlters in the ﬁrst convolutional layer they use gaussian initialization. We also tried zero initialization, but observed no difference.

![An example of the results on YoutubeObjects]()
*Figure 1. An example of the results on YoutubeObjects.*

Because of this flexibility, which is expressed in the fact that the algorithm can handle different types of input annotations, there are additional variations of this algorithm.

One of them is called MaskTrackBox. It takes a bounding box annotation in the first frame instead of a segmentation mask. To handle this variant they use a convnet model trained with a bounding box rectangles as input masks.

Another one is MaskTrack+Flow. It is based on the optical flow[7]. Given a video sequence, they compute the optical flow using EpicFlow with Flow Fields[8] matches and convolutional boundaries and in parallel to the MaskTrack they can compute a second output mask using the magnitude of the optical flow field as an input image (replicated into a three-channel image).

![An example of the results using different input annotations]()
*Figure 2. An example of the results using different input annotations.*


### Data Collection / Data Analysis

Authors fed convnet with ImageNet and MSRA10K datasets, but they also consider ECSSD, SOD and PASCAL-S datasets.

They evaluated their approach on three different video object segmentation datasets: DAVIS, YoutubeObjects and SegTrack-v2. Then, they compared results for each dataset with respect to other methods, sequences and attributes.


### Results

As a result, authors got a method, which can handle different types of input annotations and is competitive. They showed how convnets can be efficiently applied for video object segmentation and introduced the new approach - MaskTrack, which can be used as a base for other algorithms.


### Advantages / Disadvantages

I can highlight the next pros:

	To process the object segmentation we need a single pass over the video without considering more than one frame at a time
	Rough input masks are enough for our trained network to provide sensible output segment. Even a large bounding box as input will result in a reasonable output.
	Because we only use a mask instead of an image crop as an additional input we can easily synthesize training samples from single frame instance segmentation annotations.

And cons:

	We need ground truth for the first frame.
	We can detect the movements only of the object detected on the first frame.

To summarize, in 2017 in the DAVIS-2017 challenge [6] (a year after the work was published) all of the leading works was based on either MaskTrack or OSVOS[5].

![Top scores from DAVIS-2017 challenge]()
*Figure 3. Top scores from DAVIS-2017 challenge.*


### Useful Links

[1]: [Learning Video Object Segmentation From Static Images | Spotlight 2-2C](https://www.youtube.com/watch?v=aPSqUby99Wc&t=5s)
[2]: [Learning Video Object Segmentation from Static Images (results on YoutubeObjects)](https://www.youtube.com/watch?v=Ze7dKwwAw8o&t=11s)
[3]: [GOTURN: Generic Object Tracking Using Regression Networks](https://github.com/davheld/GOTURN)
[4]: [MDNet: Multi-Domain Convolutional Neural Network Tracker](https://github.com/HyeonseobNam/MDNet)
[5]: [The Basics of Video Object Segmentation](https://techburst.io/video-object-segmentation-the-basics-758e77321914?gi=7ebd410f75de)
[6]: [A Meta-analysis of DAVIS-2017 Video Object Segmentation Challenge](https://medium.com/@eddiesmo/a-meta-analysis-of-davis-2017-video-object-segmentation-challenge-c438790b3b56)




