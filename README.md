Assignment 4, Problem 4 <br />
CS 6220-A, Big Data Systems and Analytics, Fall 2021 <br />
Course Website [Link](https://www.cc.gatech.edu/~lingliu/courses/cs6220/index.html) <br />
Professor: [Ling Liu](https://www.cc.gatech.edu/~lingliu/) <br />
Georgia Institute of Technology<br />

## Table of Contents

- [Directories Explained](#directories-explained)
- [To Run](#to-run)
- [Cross Dataset Analysis (!! Complements the Report Submission)](#cross-dataset-analysis)
- [Loss rates for Batch Size x Client Iterations variations](#loss-rates-for-batch-size-x-client-variations)
  <!-- * [Introductory Analysis](#introductory-analysis)
  * [Hardware Specifications](#hardware-specifications)
  * [Overview of the Tasks](#overview-of-the-tasks)
  * [WordCount using MapReduce](#wordcount-using-mapreduce)
    + [Dataset](#dataset)
    + [Dataset Sample](#dataset-sample)
    + [Output Analysis](#output-analysis)
    + [Runtime Analysis](#runtime-analysis)
  * [TopN using MapReduce](#topn-using-mapreduce)
    + [Dataset](#dataset-1)
    + [Data Sample](#data-sample)
    + [Output Analysis](#output-analysis-1)
    + [Runtime Analysis](#runtime-analysis-1) -->


## Directories Explained

The `CPL_attack-master` contains the source code of the DLG and CPL attacks, and is borrowed from this [link](https://github.com/git-disl/CPL_attack).

The `ImagesMaster` directory contains all the images that were used as a part of analysis. 

`Assign4.pdf` is the final report submitted on Canvas.

`lfw_batch.py` is the modified source code to capture batch and client iteration effects on reconstruction quality. 

`lfw_deep_leakage_from_gradient` is the code with corresponging changes made to compare CPL with DLG. 

## To Run

All the notebooks relevant to CPL and DLG inside the `CPL_attack-master` folder can be ran on Google Colab. They run just like any other jupyter notebook. For more information on what individual notebooks contain, visit the README page [at this link](https://github.com/git-disl/CPL_attack). 


**Note:** There might be few modules that could be missing during your first run. In such cases, run
```
pip install <module-name>
```
to fix that issue.


## Cross Dataset Analysis

For CPL vs DLG analysis, look into `Assign4.pdf`. This section only covers the left out analysis on cross-dataset variance of an attack (DLG).

<p align="center">
  <img src="ImagesMaster/MultipleDatasets/GrandDLGonCIFAR100.png" width="600" title="hover text">
  <!-- <img src="your_relative_path_here_number_2_large_name" width="350" alt="accessibility text"> -->
</p>

The image above shows the comparision of reconstruction convergence on a new dataset that is not studied in the paper `Assign4.pdf`, the CIFAR-100 dataset. In clockwise order, the plots indicate random initialization cost (iters or time) vs effect (MSE or SSIM) for class1, class2 with random initializations and class2,class1 with patterned initializations. Below each progress series of images in CIFAR-100 is a reference image from LFW dataset for comparision. 

### Analysis

1. The first striking observation from the image above is the fact that patterned initialization converges a lot quicker (look for the elbows in the graph) compared to random initialization. We confirmed the same observation for DLG as well as CPL in case of LFW dataset. This shows that the proposal for using a patterned initialization is universally applicable across datasets. 

2. The second observation from the above image is that across the two classes, the convergence graph is roughly same for random as well as patterned initialization. This could be due to the fact that the iterative (de)noise added to the image is proportional to the difference between the computed gradient and the stolen gradient. The chance that a random gradient in a hyperspace is close to the stolen gradient is extremely low. Moreover, the images start out completely random (even if they are patterned, sub patterns are random). Hence, most of the convergence takes place in the first 50 iterations therefore making all of the images look like they converge at roughly around the same time.

3. The third observation from the above image is that CIFAR-100 is taking longer than LFW to converge. There could be two reasons behind this. One, the label prediction following the argmin technique could be incorrect in this specific example. Two, and more probably, since a human skin tone is fairly homogeneous, when faces are considered, it helps in convergence in that area. For example, within CIFAR-100 dataset, the image backgrounds that are fairly homogeneous are reconstructed in earlier iterations compared to the central image that has more contrast-edges.


## Loss rates for Batch Size x Client Variations

|  SSIM    | C = 1  | C = 2  | C = 5  | C = 10 | C = 20 | C = 50 |
|--------|--------|--------|--------|--------|--------|--------|
| B = 1  | 0.5954 | 0.3150 | 0.1535 | 0.1227 | 0.1206 | 0.1039 |
| B = 5  | 0.1218 | 0.0547 | 0.0421 | 0.0411 | 0.0504 | 0.0226 |
| B = 10 | 0.0813 | 0.0401 | 0.0297 | 0.0233 | 0.0467 | 0.0135 |
| B = 20 | 0.0384 | 0.0264 | 0.0188 | 0.0192 | 0.0289 | 0.0084 |


| MSE    | C = 1  | C = 2  | C = 5  | C = 10 | C = 20 | C = 50 |
|--------|--------|--------|--------|--------|--------|--------|
| B = 1  | 0.005  | 0.0144 | 0.0357 | 0.0458 | 0.0452 | 0.0495 |
| B = 5  | 0.0486 | 0.0964 | 0.161  | 0.0897 | 0.0663 | 0.1288 |
| B = 10 | 0.0666 | 0.1178 | 0.2115 | 0.0886 | 0.0709 | 0.1724 |
| B = 20 | 0.0855 | 0.3639 | 0.3751 | 0.0973 | 0.1004 | 0.2812 |


### Batch Size x Client Iterations Analysis

1. The key observation from the table above is that we observe an increasing loss as the client iterations increase. However, this change is not significant as compared to batch size.

2. Singular batch size has a significantly high lead in reconstruction, even compared to B=5. This can be attributed to the fact that images of the same class could have different backgrounds, and therefore the background cannot be reconstrcuted identical to image against which the loss is computed. Therefore, this sudden drop is expected.

3. When we run the same computation on DLG, we see an extreme drop in reconstruction quality for BxL>10. Therefore, these values are not included in the table. (MSE goes beyond 70 for B>5 with L>2).  This run can be found in the python notebook in this github repo's DLG notebook run. 