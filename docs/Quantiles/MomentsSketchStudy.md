---
layout: doc_page
---

# Moments Sketch Study

The goal of this article is to compare the accuracy performance of the Moments Sketch to an exact, brute-force computation using actual data extracted from one of our back-end servers. 

Please get familiar with the [Definitions]({{site.docs_dir}}/Quantiles/Definitions.html) for quantiles.

## Versions

* Moments Sketch code as of <a href="https://github.com/apache/incubator-druid/pull/6581">apache/incubator-druid Pull Request 6851 Feb 4, 2019</a>


## The Paper

The implementation of this Moments Sketch was based on the July 13, 2018 
[paper](https://arxiv.org/abs/1803.01969) 
by Edward Gan, Jialin Ding, Kai Sheng Tai, Vatsal Sharan, Peter Bailis of Stanford InfoLab. However, it should be noted that the authors of the paper specifially mention the following caveats:

* "The moments sketch accuracy is dataset dependent" Page 9, section 6.2.3.
* "The moments sketch runs into numeric stability issues past <i>k</i> &ge; 15 on some datasets." Page 9, Section 6.2.2
* "The moments sketch ... is most useful in datasets without strong discretization ...  The maximum entropy principle is less accurate when there are clusters of discrete values in a dataset." Page 2, Section 1.

Unfortunately, real data can be quite ugly as it can be highly skewed and with lots of zeros, nulls, and sometimes negative values. 

## The Input Data
The data file used for this evaluation, *streamA.txt*, is real data extracted from one of our back-end servers.  It represents one hour of web-site time-spent data measured in milliseconds. The data in this file has a smooth and well-behaved value distribution with a wide dynamic range.  It is a text file and consists of consecutive strings of numeric values separated by a line-feeds. Its size is about 2GB.

## Creating the Exact CDF and Histograms For Comparison
In order to measure the accuracy of the Approximate Histogram, we need an exact, brute-force analysis of *streamA.txt*. 

The process for creating these comparison standards can be found [here]({{site.docs_dir}}/Quantiles/ExactQuantiles.html).

## The Results

### K = 15, Size = 141 bytes,  <i>a priori</i> Accuracy = Unknown

The CDF plot:

<img class="doc-img-full" src="{{site.docs_img_dir}}/quantiles/MSketch_StreamA_CDF.png" alt="MSketch CDF of ranks to quantiles" />  

The green dots in the above plot represents the Exact cumulative distribution (CDF) of ranks to quantile values. The black circles in the upper right corner of the plot represent the values returned from the Approximate Histogram *getQuantiles(float[])* function. 

The plot reveals that the MSketch has improperly shifted the entire distribution by about 12% to the left creating a fixed rank error of at about 12% over the entire range. This is likely due to the zeros that naturally occur in this data. This failure is silent as MSketch does not provide any warning that this kind of distortion might be occurring.  

The Msketch does not provide the inverse *getRank(v)* functionality.  This means creating a Histogram or PMF from the Msketch is not simple to do.

Users would be well-advised to not use this tool for serious analysis.

## The Evaluation Source
The following are used to create the plots above.

* [Moments Sketch profiler](https://github.com/DataSketches/characterization/blob/master/src/main/java/com/yahoo/sketches/characterization/quantiles/MSketchStreamAProfile.java)
* [MSketch profiler config](https://github.com/DataSketches/characterization/blob/master/src/main/resources/quantiles/MSketchStreamAJob.conf)
* [StreamA Data file](https://github.com/DataSketches/characterization/blob/master/streamA.txt.zip) This is stored using git-lfs.

Run the above profilers as a java application and supply the config file as the single argument. The program will check if the data file has been unzipped, and if not it will unzip it for you. 




 