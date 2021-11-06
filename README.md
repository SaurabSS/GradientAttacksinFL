Assignment 4, Problem 4 <br />
CS 6220-A, Big Data Systems and Analytics, Fall 2021 <br />
Course Website [Link](https://www.cc.gatech.edu/~lingliu/courses/cs6220/index.html) <br />
Professor: [Ling Liu](https://www.cc.gatech.edu/~lingliu/) <br />
Georgia Institute of Technology<br />

## Table of Contents

- [Directories Explained](#directories-explained)
- [To Run](#to-run)
- [Report](#analysis)
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


## Analysis

<p align="center">
  <img src="ImagesMaster/MultipleDatasets/GrandDLGonCIFAR100.png" width="550" title="hover text">
  <!-- <img src="your_relative_path_here_number_2_large_name" width="350" alt="accessibility text"> -->
</p>

