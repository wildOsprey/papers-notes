## Generalized Procrustes Analyses (GPA)

**Procrustes was a bandit who, in Greek mythology, had a rather esoteric modus operandi: he would male his victims fit inside his bed by either stretching them if they were too short or cutting off pieces of them if they were too long.**

![One day from the life of a data scientist]()
*Figure 0. One day from the life of a data scientist.*

### Generalized Procrustes Analysis

#### What does Procrustes Analysis do?

    Centers all shapes at the origin (0, 0, 0)
    Scales all shapes to the same size (unit size = 1)
    Rotates each shape around the origin until the sum of squared distances among them is minimized
    Ensures that the differences in shape are minimized.

#### What is the difference between Procrustes Analysis and Generalized Procrustes Analysis?

![The difference between PA and GPA]()
*Figure 1. The difference between PA and GPA.*

#### Why do we need it? 

It helps to normalize positions of all shapes in order to compensate for differences in scale, rotation, and bias. Within the task of facial alignment, we need to find the mean face shape. Then, with the help of algorithms such as PCA, we can encode any individual shape by its variation from the mean. 

![Training points before and after normalization]()
Figure 2. Training points before and after normalization. Red keypoints and shape are got after applying PCA. 

1. https://graphics.stanford.edu/courses/cs164-09-spring/Handouts/paper_shape_spaces_imm403.pdf
2. http://www.cse.psu.edu/~rtc12/CSE586/lectures/cse586ShapeAndPCA.pdf
3. https://pdfs.semanticscholar.org/25bc/f60a07ecac712fe886103a6702513e7f3430.pdf
