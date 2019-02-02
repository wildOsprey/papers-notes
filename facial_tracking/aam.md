## Active Appearance Model (AAM)


**Active Appearance Model (AAM)** contains a statistical model of the shape and grey-level appearance of the object of interest which can generalize to almost any valid example.

The idea is that you have a base shape and you try to fit it into the image as shown in Figure 1. 

![Blue lines represent a base shape, and the red ones - a final results.]()
*Figure 1.  Blue lines represent a base shape, and the red ones - a final results[2].*

AAM consist of the following parts: 

*Shape Model

    We can generate any shape from the base shape with parameters by **Equation 1**, where: 

    **c** - represents the shape parameters

    **Bs** - a shape basis (eigenvectors computed from the normalized shapes with PCA)

    **s0** - mean shape, computed from the training shapes before applying PCA

    Changing shape parameters, we can get different face deformations and fit them to the real face.

![The shape and its deformations]()
*Figure 2. The shape and its deformations[2].* 

AAM can be with rigid or non-rigid transformations. By the definition from the linear algebra, a rigid transformation is that transformation, which does not change the shape or size of the preimage. Non-rigid transformation can change the size but not the shape. Rigid information includes scale, rotation, and translation.

*Motion Model

The motion model consists of a warp function **W(s, p)** which is is one-to-one correspondence between all pixel locations with the convex hull matrix defined by shape **s** and parameter **p** . Parameter p represents shape parameters with rigid and non-rigid information included. Typical warping functions are the Piecewise Affine and the Thin Plate Splines.


*Appearance Model

Training of AAM model consist of three parts:

	First one is extracting features from the image. AAM can use holistic and part-based approaches for this task. A holistic approach is that approach, which uses warping function. In part-based approach, firstly we need to remove all rigid transformations, then extract features one by one and form the whole feature vector.

![Top image depicts holistic approach, bottom - part-based.]()
Figure 3. Top image depicts holistic approach, bottom - part-based. **f** - feature extraction function of the image **I** given the shape **s**. I can be the warped image (holistic approach) or the registered images in part-based approach[2].

    Next step is to normalize the image in order to compensate for the different lighting conditions. 
    One the third step we generate matrix Ba, so that we can form the representation of the face as  **A = A0 + Ba*c**, where **x0** - is the mean shape vector,  **Ba** - is the appearance basis and **c** - is the vector of appearance parameters. 

![An appearance and its deformation]()
*Figure 4. An appearance and its deformation[2].*

![The final output]()
*Figure 5. The final output[2].*

You can find the implementation of AAM in menpo python frameworks. How to install and how to use you can find on their [website](https://www.menpo.org/).
Useful Links:

1. [Active Appearance Model](https://www.cs.cmu.edu/~efros/courses/AP06/Papers/cootes-eccv-98.pdf)
2. [Анализ существующих подходов к распознаванию лиц](https://sohabr.net/habr/post/238129/)
3. [Активные модели внешнего вида](https://habr.com/post/155759/&post=5385365_18497/)
4. [Menpo](http://www.menpo.org/menpofit/aam.html)
