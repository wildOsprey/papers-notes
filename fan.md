## How far are we from solving the 2D&3D Face Alignment problem? (and a dataset of 230,000 3D facial landmarks)
*Adrian Bulat, Georgios Tzimiropoulos*

[Link to the paper](https://arxiv.org/abs/1703.07332)


### Research Direction

2D&3D Facial Alignment


### Abstract / Brief Introduction

Authors made a research about state-of-art algorithms for landmarks localization and create a network based on two state-of-art components (HourGlass[4] or HG for short and the hierarchical, parallel and multi-scale block[3]) for 2D and 3D face alignment task. In addition, they created a dataset with 3D landmarks. 


### Research Focus

Authors examine the problem of large poses (from -90° to 90°). The accuracy of these poses is often bad because the amount of visible landmarks is too small. In the process of solving this problem, they also faced a problem of small available data with 3D landmarks. Most datasets provide only 2D annotations, among them, they found only one dataset with 2D and corresponding to it 3D annotations and one with just 3D annotations. Moreover, in the biggest and the most popular face alignment, dataset 300-VW pose variations is only from -45° to 45° so that the network trained on this data would have a bad performance on large poses (ex. from 60° to 90°). 


### Research Methodology

Authors used three neural networks: for 2D face alignment, 3D face alignment and for transformation 2D landmarks into 3D landmarks. They called it Face Alignment Network or FAN: 2D-FAN, 3D-FAN, and 2D-to-3D-FAN.

All of them is based on HourGlass[4,5] architecture, but instead of bottleneck[6] they used the hierarchical, parallel and multi-scale block[3]. In Figure 1 you can see the original architecture of the HG, Figure 2 shows the difference between the bottleneck and the block approach. The architecture, used in the paper, is shown in Figure 3.


![An original implementation of HourGlass](https://github.com/wildOsprey/papers_notes/blob/master/images/fan/hg.jpeg)
*Figure 1. An original implementation of HourGlass[5].*

![The first scheme shows the original bottleneck and the second one - the hierarchical, parallel and multi-scale block](https://github.com/wildOsprey/papers_notes/blob/master/images/fan/bottleneck_vs_block.JPG)
*Figure 2. The first scheme shows the original bottleneck and the second one - the hierarchical, parallel and multi-scale block[3].*


![FAN architecture](https://github.com/wildOsprey/papers_notes/blob/master/images/fan/fan_architecture.jpeg)
*Figure 3. FAN architecture.*

During the process of training, each heatpoint is been found separately from the others and transferred to its own layer. As a result of each hourglass block, we got a (64,64,68) tensor, where the first two digits are output size and the last one is the number of heatpoints. 

All networks use RMSprop.

All three networks have their specific details:

#### 2D & 3D face alignment

2D- and 3D-FAN network  uses the following parameters:

    initial learning rate is 10-4 for 
    number of epochs - 40
    learning rate schedule
    after 15 peaches - 10-5
    after another 15 - 10-6
    augmentation: flipping, rotation (from -50° to 50°), color jittering, scale noise (from 0.8 to 1.2) and random occlusion.

#### 2D-to-3D

2D-to-3D-FAN network  uses the following parameters:

    the initial learning rate is 10-3 for 
    number of epochs - 40
    learning rate schedule
    after 15 peaches - 10-5
    after another 15 - 10-6
    augmentation: flipping, rotation (from -70° to 70°), color jittering, scale noise (from 0.7 to 1.3) and random occlusion.

You can find the original implementation on PyTorch and Torch7 above the link[7]. 

### Data Collection / Data Analysis

Authors examined already existed datasets and selected the most popular among them. In Figure 4 you can see a little summary of their research.

![Popular datasets for face alignment](https://github.com/wildOsprey/papers_notes/blob/master/images/fan/popular_datasets.JPG)
*Figure 4. Popular datasets for face alignment.*

For training, they used 300-W-LP dataset, which provides both 2D and 3D landmarks. For some 2D experiments, they also used the original 300-W dataset. For 3D training, they created their own dataset named LS3D-W. For testing, they used 300-W test set, 300-VW, and Menpo - for 2D, AFLW2000-3D. 

Authors tried to decrease the number of parameters, the result is shown in Figure 5.

![Results depend on the number of params and pose](https://github.com/wildOsprey/papers_notes/blob/master/images/fan/result6.JPG)
*Figure 5. Results depend on the number of params and pose.*


### Results

As a result, the authors created the largest 3D landmarks dataset and gave a free access for everyone. 

![Predictions on AFLW000-3D. Red - ground truth, white - FAN prediction](https://github.com/wildOsprey/papers_notes/blob/master/images/fan/result4.JPG)
*Figure 6. Predictions on AFLW000-3D. Red - ground truth, white - FAN prediction.*

![Predictions on 300-VW. Red - ground truth, white - FAN prediction](https://github.com/wildOsprey/papers_notes/blob/master/images/fan/result1.JPG)
*Figure 7. Predictions on 300-VW. Red - ground truth, white - FAN prediction.*

![3D-FAN results with different noise and pose](https://github.com/wildOsprey/papers_notes/blob/master/images/fan/result5.JPG)
*Figure 8. 3D-FAN results with different noise and pose.*


### Advantages / Disadvantages

Pros:

	3D-FAN network shows good results regardless of resolution, weights initialization, and facial pose.
	The community got a large dataset and an opportunity to transfer landmarks from 2D to 3D.

Cons: 

	The model has a large number of params and has no option to decrease it (with decreasing of it sharply decreases accuracy).

### Useful Links

1. [HourGlass implementation in Keras](https://gist.github.com/SaifAlDilaimi/cdacc15129fb71f905990282c20b0b35)

2. [Original repo](https://github.com/1adrianb/2D-and-3D-face-alignment)

3. [Binarized Convolutional Landmark Localizers for Human Pose Estimation and Face Alignment with Limited Resources](https://arxiv.org/pdf/1703.00862.pdf)

4. [Stacked Hourglass Networks for Human Pose Estimation](https://arxiv.org/pdf/1603.06937.pdf)

5. https://github.com/aleju/papers/blob/master/neural-nets/Stacked_Hourglass_Networks_for_Human_Pose_Estimation.md

6. [Deep Learning and the Information Bottleneck Principle](https://arxiv.org/abs/1503.02406)

7. [Original publication](https://www.adrianbulat.com/face-alignment/)
