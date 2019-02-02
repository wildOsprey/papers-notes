## Local Binary Patterns

For the task of face recognition, Local Binary Patterns (LBP) are used for feature extraction and face matching. 

You can find a more complex explanation in this [paper](https://globaljournals.org/GJCST_Volume13/1-Face-Recognition-using-Local.pdf). Also, there are some videos from youtube: [1](https://www.youtube.com/watch?v=wpAwdsubl1w), [2](https://www.youtube.com/watch?v=-Ja-vLbHWLc&list=PLlmRs9D3BDwsrXMj2OdK0ZVV1_DWq_5S0).


Firstly, as you can see in Figure 1, a face is detected and divided into regions. 

![The face divided into regions]()
*Figure 1. The face divided into regions.*

Then from each region features are extracted.

The original LBP operator works with the eight neighbors of a pixel, using the value of this center pixel as a threshold. If a neighbor pixel has a higher gray value than the center pixel (or the the same gray value
than a one is assigned to that pixel, else it gets a zero. The LBP code for the center pixel is then produced by concatenating the eight ones or zeros to a binary code (Figure 2). 

![The process of encoding]()
*Figure 2. The process of encoding.*


The extended operator takes neighbors with some radius R. P, in this case, is a number of points (Figure 3).

![The extended LBP neighb]()
*Figure 3. The extended LBP neighbors.*


The algorithm is similar, the center value is comparing with values of neighbors, but these values are needed to be normalized. It is achieved with the next formula: ![formula]() 



Once the Local Binary Pattern for every pixel is calculated, the feature vector of the image can be constructed. For an efficient representation of the face, first, the image is divided into K2 regions. In Figure 4 a face image is divided into 82 = 64 regions. For every region, a histogram with all possible labels is constructed.

![Face image divided into 64 regions with corresponding histograms]()
*Figure 4.  Face image divided into 64 regions with corresponding histograms.*


Then, they are concatenated and compared with database samples. 

In Figure 5 there is a flowchart of the LBP and in Figure 6 - a flowchart for the recognition process.

![Flowchart of the LBP Process]()
*Figure 5. Flowchart of the LBP Process.*

![Flowchart for face recognition system]()
*Figure 6. Flowchart for face recognition system.*



