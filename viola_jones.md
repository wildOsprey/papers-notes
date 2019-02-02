## Rapid Object Detection using a Boosted Cascade of Simple Features
*Paul Viola, Michael Jones*


[Link to the paper](https://www.cs.cmu.edu/~efros/courses/LBMV07/Papers/viola-cvpr-01.pdf)

### Research Direction

Face Detection


### Abstract / Brief Introduction

The paper describes one of a machine learning approaches for visual object detection. It answers a question “How can we inhance the process of image preprocessing and achieve high detection rates?”. For this purpose authors offer the modified version of AdaBoost[3] algorithm and introduce a term “cascade” method. In addition, they present a new way to represent an image – “Integral image”. Then, they show the results of their research.


### Research Focus

Despite the fact, that this algorithm can be applied to detect objects, mainly it was created for face detection. The goal was to develop an effective algorithm for face detection which can be used in real time.

One of the problems of object detection – expensive calculations, especially if we’re talking about real-time processing. For example, if you want to calculate Haar features[6], you need to find the sums of pixels, then to subtract them and it should be done for each feature in a set of features in each sub-window (a window which takes only some part of the image), which is not this effective.

Then, when you have found these features you also need to decide, which are the most important, because in average there are about 180000 features for a 25 by 25 pixels sub-window. The next step is to find the most suitable sub-windows from the all set. There are more than 75000000 sub-windows, so if you want to process each of them you should try to find the most optimized way to do it.


### Research Methodology

In the paper, authors use a few methods combining. Let us divide it in two parts: training and detection.

For detection they use window which passes through the whole image looking for features. The goal is to find all the features in the current window. This supposed to be an object we are looking for.

The simple features that have been used are reminiscent of **Haar** basis functions. Authors used three kinds of them: *two-rectangle feature, three-rectangle, four-rectangle features.*

![Two-rectangle (A, B), three-rectangle (C) and four-rectangle (D) features](https://github.com/wildOsprey/papers_notes/blob/master/images/viola-jones/haar_features.PNG)
*Figure 1. Two-rectangle (A, B), three-rectangle (C) and four-rectangle (D) features*

The value of these features is calculated by subtraction the sums of light parts of feature and the dark ones. 

To optimize calculation of these features authors introduce the concept of **“Internal image”**. This is a new representation of our image, which is created by following the rules: for each pixel, you need to find a sum of all pixels above and to left and add it to the corresponding cell of new array.

So, when you need to decide whether your feature fits, you don’t need to sum each pixel. It can be computed with four array references.

![Example of calculating an integral image and finding a value of some feature](https://github.com/wildOsprey/papers_notes/blob/master/images/viola-jones/integral_image.PNG)
*Figure 2. An example of calculating an integral image and finding a value of some feature*

To train the model they used the modification of AdaBoost algorithm and the cascade structure.

AdaBoost (adaptive boosting) is used both to select a small set of features and to train a classifier. The idea is that we use the first weak classifier and find negative-false and positive-false points. Then, we increase the weights of these points and apply the next weak classifier. This process is repeated until we get the required accuracy of the classifier. Final strong classifier is a linear combination of weak classifies.

The outcome of the detection process is a degenerate decision tree, what they call the “cascade”. When you are passing through image, you are trying to classify a feature. A positive result from the first classifier triggers the next, and then if second classifier also has positive result, we call the next and so on. If it is negative – we reject current sub-window.

![Cascade architecture](https://github.com/wildOsprey/papers_notes/blob/master/images/viola-jones/cascade_architecture.PNG)
*Figure 3. Cascade architecture*

Sub-window processing is called a stage of cascade. Each stage is trained by adding features until the target detection and false positives rates are met (these rates are determined by testing the detector on a validation set). Stages are added until the overall target for false positive and detection rate is met.

![A nice visualization of the algorithm](https://github.com/wildOsprey/papers_notes/blob/master/images/viola-jones/ex.png)
*Figure 4. A nice visualization of the algorithm[8].*


### Data Collection / Data Analysis

The photos of faces, used for training their models, were extracted from images, downloaded during a random crawl of the Internet. In total they’ve got 4916 faces (plus their vertical mirrors) and  9544 non-faces images. Then, for tests, they used MIT+CMU frontal face test set, which consists of 130 images with 507 labeled frontal faces.

Each image was resized to a size of 24 by 24 pixels. Then, they represented each image as “internal image”.



### Results

The results were great. Comparing with other detectors the result on the large sample was times faster. It is 15 times faster than the RowleyBaluja-Kanade detector and about 600 times faster than the Schneiderman-Kanade detector.

This was achieved through the three key methods described above. According to one of the studies, only the integrated representation of the image increased the speed of the algorithm by 60 times[7]. They also proved their hypothesis in practice, that a very small number of these features can be combined to form an effective classiﬁer.


### Advantages / Disadvantages

At the time of writing, it was the first algorithm of face detection, which could do its job rapidly, efficiency and accuracy. Moreover, because of quick calculations, it can be used in the real-time. This was a real breakthrough in face detection, so that it was implemented in different devices like cameras and included to libraries like OpenCV. Because of its wide distribution and low false positive probability, it is still the most commonly used algorithm.

Of course, it has some limitations and disadvantages. One of the main is that it can detect face only if it is situated in front to camera. However, it shows not bad result in detection faces, which are rotated up to 30 degrees.

Nowadays, there are algorithms, which are faster and more efficient (SSD, Yolo). But, on the over hand, they need much more resources. Also, part of these algorithms are based on Viola Jones algorithm or applies some techniques from it (LBP approach). There are also some Viola Jones algorithm’s been modified.


### Useful Links

[1]: [Face detection in computer vision](http://vinsol.com/blog/2016/06/28/computer-vision-face-detection/)
[2]: [An Analysis of the Viola-Jones Face Detection Algorithm](https://www.researchgate.net/publication/272643562_An_Analysis_of_the_Viola-Jones_Face_Detection_Algorithm)
[3]: [AdaBoost](http://datascientist.one/adaboost-algorithm/)
[4]: [Learning: Boosting - MIT lecture](https://www.youtube.com/watch?v=UHBmv7qCey4)
[5]: [AdaBoost implementation](https://gist.github.com/tristanwietsma/5486024)
[6]: [Viola-Jones algorithm (habr, ru)](https://habrahabr.ru/post/133826/)
[7]: [Viola-Jones algorithm (ru)](http://elib.spbstu.ru/dl/2/v17-6320.pdf/download/v17-6320.pdf)
[8]: [Viola-Jones visualization](https://vimeo.com/12774628)




