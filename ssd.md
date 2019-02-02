## SSD: Single Shot MultiBox Detector 

*Wei Liu, Dragomir Anguelov, Dumitru Erhan, Christian Szegedy, Scott Reed, Cheng-Yang Fu, Alexander C. Berg*

[Link to the paper](https://arxiv.org/abs/1512.02325)

### Research Direction

Computer Vision, Object Detection, Object Classification


### Abstract / Brief Introduction

Authors introduced a new algorithm for object detection and classification, which is faster and more accurate than the previous state-of-art for single shot detectors (YOLO[2,3], Faster R-CNN[4]). It is based on OverFeat[5, 6] and YOLO[2,3], but has some significant improvements and modification such as using multiple layers for prediction at different scales.


### Research Focus

Current state-of-art object detection systems are variants of the following approach: hypothesize bounding boxes, resample pixels or features for each box, and apply a high-quality classifier. But these approaches are too computationally expensive and too slow for real-time applications. There have been many attempts to build faster detectors by attacking each stage of the detection pipeline, but signiﬁcantly increased speed comes only at the cost of signiﬁcantly decreased detection accuracy so far. The goal is to overcome this barrier.


### Research Methodology

SSD architecture is based on VGG16[7].

![Figure 1. SSD Architecture](https://github.com/wildOsprey/papers_notes/blob/ssd/images/ssd/ssd_architecture.png)
*Figure 1. SSD Architecture*


As you can see on the Figure1, VGG is used up to conv4_3. For each of next feature maps we apply detector and classifier. That allows us to find objects with different sizes. As a result we get coordinates of detection boxes and classification labels. Then, using **Non-Maximum Suppression** (NMS) algorithm[8] we merge discovered boxes to get final detection.

Let’s have a look on how detector and classifier work. As input, we have our feature map. First, we need to generate default boxes. Each cell in the feature map corresponds to 4 default boxes. Each default box is characterized by 4 parameters: coordinates of its center, width and height. For each box we need to find ratio vector to fix the size and location and confidence for each of the classes. Then, for all of these boxes we apply filter by confidence and choose the best option. The key point is that box predictions and class score are obtained by convolution.

This is the main idea, you can find more details with great explanation and all formulas at the chapter 2 “The Single Shot Detection (SSD)”.

![Figure 2. Example of feature map with default boxes and corresponding localization and confidence](https://github.com/wildOsprey/papers_notes/blob/ssd/images/ssd/ssd_features_ex.png)
*Figure 2. Example of feature map with default boxes and corresponding localization and confidence*

### Data Collection / Data Analysis

All experiments are based on VGG16, which is pre-trained on the ILSVRC CLS-LOC dataset. They convert fc6  and fc7 to convolutional layers, subsample parameters from fc6 and fc7, change pool5  from 2 × 2 − s2 to 3 × 3 − s1, and use the a trous algorithm [9] to ﬁll the ”holes”. Also, they fine-tuned the resulting model using SGD with initial learning rate 10−3, 0.9 momentum, 0.0005 weight decay, and batch size 32.

Authors trained network on PASCAL VOC2007, PASCAL VOC2012, COCO and ILSVRC datasets, fine-tune hyperparameters for each one and then compare results.

Input size of image was 300x300 and 512x512 (SSD300 and SSD512 accordingly).



### Results

If Faster-R-CNN operates at 7 frames per second (FPS) with mean Average Precision (mAP) 73.2% or YOLO 45 FPS with mAP 63.4%, SSD reaches 59 FPS with mAP 74.3% (all measures for VOC2007 dataset). So, authors got good results and really increased speed and accuracy.


### Advantages / Disadvantages

The main pros of this algorithm is its speed and accuracy, but as a cons it is not good at detecting smaller objects.


### Useful Links

    [1]: [SSD: Single Shot MultiBox Detector (How it works) - deepsystems.io](https://www.youtube.com/watch?v=P8e-G-Mhx4k)
    [2]: [YOLO: You only look once (How it works) - deepsystems.io](https://www.youtube.com/watch?v=L0tzmv--CGY)
    [3]: [You Only Look Once: Unified, Real-Time Object Detection](https://arxiv.org/pdf/1506.02640.pdf)
    [4]: [Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks](https://arxiv.org/abs/1506.01497)
    [5]: [OverFeat: Integrated Recognition, Localization and Detection using Convolutional Networks](https://arxiv.org/abs/1312.6229)
    [6]: [OverFeat implementation](https://github.com/sermanet/OverFeat)
    [7]: [Keras | VGG16 Places365 - VGG16 CNN models pre-trained on Places365-Standard for scene classification](https://github.com/GKalliatakis/Keras-VGG16-places365)
    [8]: [Non-Max Suppression lesson from coursera](https://ru.coursera.org/learn/convolutional-neural-networks/lecture/dvrjH/non-max-suppression)
    [9]: [Stationary waveler transform](https://en.wikipedia.org/wiki/Stationary_wavelet_transform)



