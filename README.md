# SFND 2D Feature Tracking
## Sensor Fusion Engineer Nanodegree

![visualization.png](images/keypoints.png)

The purpose of this project is to test, analyze, and determine the most effectove combination of available OpenCV key-point detectors, descriptors, and matching methods to estimate Time-to-Collision (TTC), a metric used by collision avoidance systems in self-driving vehicles. TTC is based on the sequence of images provided by a monoview camera mounted on top of a vehicle, forward-facing. TTC involves trade-offs between multiple factors: the number of keypoints detected, the number of matches between the consecutive images, required processing time. 

The default OpenCV implementation parameters were used for each entity (detectors, descriptors, matchers, selectors). The measurements were taken on an Ubuntu virtual box, Linux 16.04LTS.

### Results

#### Keypoint Statistics
![keypoints.png](images/keypoint_figures.png)
For a detailed view, click the image above.

#### Match Statistics
![matches.png](images/match_figures.png)
For a detailed view, click the image above.

#### Timing Statistics
![timings.png](images/timing_figures.png)  
To see all the details, open the image above in a new tab and zoom.
For a detailed view, click the image above.

### Trade-off Factor Analysis

#### Number of Keypoints
The table below shows the keypoint detectors sorted in descending order based on the mean number of keypoints identified among 10 images from the monocamera video sequence. BRISK detected a mean XYZ keypoints in the image set, while at the low end  the HARRIS method detected only a mean of XYZ keypoints.  


| BRISK | AKAZE | FAST | SIFT | SHITOMASI | ORB | HARRIS |
|-------|-------|------|------|-----------|-----|--------|
| XYZ   | XYZ   | XYZ  | XYZ  | XYZ       | XYZ | XYZ    |


#### Number of Matches
Below is a list of TOP-5 combinations of detector+descriptor sorted 
in descending order based on the mean number of identified matches 
among 9 pairs of 10 consecutive images. 
The analysis is based on the matches data presented in the section 
[Matches Statistics](#matches-statistics).   

| Place     | Combination(s)                                                            |  
|-----------|---------------------------------------------------------------------------|  
| 1st (278) | BRISK+SIFT, BRISK+BRIEF, BRISK+BRISK, BRISK+ORB                           |  
| 2nd (258) | BRISK+FREAK                                                               |  
| 3rd (165) | AKAZE+SIFT, AKAZE+FREAK, AKAZE+ORB, AKAZE+AKAZE, AKAZE+BRIEF, AKAZE+BRISK |  
| 4th (149) | FAST+BRIEF, FAST+SIFT, FAST+BRISK, FAST+ORB, FAST+FREAK                   |
| 5th (138) | SIFT+BRISK, SIFT+BRIEF, SIFT+SIFT                                         |

#### Timings
Below is a list of TOP-5 detectors sorted 
in descending order based on the mean time required to identify keypoints in one image. 
The analysis is based on the timings data presented in the section 
[Timings Statistics](#timings-statistics).   

| FAST    | ORB     | HARRIS  | SHITOMASI | BRISK    |  
|---------|---------|---------|-----------|----------| 
| 0.74 ms | 5.22 ms | 8.86 ms | 9.29 ms   | 27.07 ms | 

Below is a list of TOP-5 descriptors sorted 
in descending order based on the mean time required to compute a set of descriptors 
for all the keypoints in one image. 
The analysis is based on the timings data presented in the section 
[Timings Statistics](#timings-statistics).  

| BRIEF   | BRISK   | ORB     | SIFT     | AKAZE    |  
|---------|---------|---------|----------|----------|  
| 0.59 ms | 1.28 ms | 1.73 ms | 15.41 ms | 29.16 ms |  

##### TOP-3 Detector+Descriptor Combinations
Assuming that the number of keypoints, number of matches, and timings 
ratings contribute equally, the TOP-3 detector-descriptor combinations 
are chosen.  

| Place                            | Combination | Score              |
|----------------------------------|-------------|--------------------|  
| 1st place (if you value accuracy)| BRISK+BRIEF | 8 = 1 + 1 + 5 + 1  | 
| 2nd place (if you value speed)   | FAST+BRIEF  | 9 = 3 + 4 + 1 + 1  |   
| 2nd place (if you value accuracy)| BRISK+BRISK | 9 = 1 + 1 + 5 + 2  | 
| 3rd place (if you value speed)   | FAST+BRISK  | 10 = 3 + 4 + 1 + 2 | 

##### Summary
The choice between BRISK+BRIEF and FAST+BRIEF should be based 
on the hardware available and accuracy requirements. 
From visual observations it is clear that both combinations produce some 
false matches on each pair of images, that is why it is probably better 
to choose FAST+BRIEF combination for collision avoidance system, 
given the significant gap between the FAST and BRISK keypoint 
detection times.

The winner is **FAST detector + BRIEF descriptor** combination.

# Installation

## Dependencies for Running Locally
* cmake >= 2.8
  * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1 (Linux, Mac), 3.81 (Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* OpenCV >= 4.1
  * This must be compiled from source using the `-D OPENCV_ENABLE_NONFREE=ON` cmake flag for testing the SIFT and SURF detectors.
  * The OpenCV 4.1.0 source code can be found [here](https://github.com/opencv/opencv/tree/4.1.0)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory in the top level directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./2D_feature_tracking`.