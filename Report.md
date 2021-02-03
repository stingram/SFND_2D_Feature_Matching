# SFND 2D Feature Tracking Report

## MP.1

To implement the ring buffer I remove the first element of the databuffer if it already has a length of 10 and more data needs to be added to it. In this way, the oldest elements from the databuffer are removed when new data is collected.

## MP.2

The detectors have been implemented and selectable via a string as required. See code for implementation.

## MP.3

Any keypoints not inside bounding rectangle provided are removed. See code for implementation.

## MP.4

Keypoint descriptors have been implemented and selectabled via a string as required. See code for implementation.

## MP.5

FLANN matching and k-nearest neighbor selection are implemented. Both methods are selectable via a string in the main function. See code for implementation. 

## MP.6

K-Nearest-Neighbor matching is implemented for the descriptor distance ratio test with a ratio set to 0.8.

## MP.7

Keypoint counts and a note on the distribution of the size is given in results.csv under section MP.7 for all keypoint detectors.


## MP.8

The number of matched keypoints for all ten images is recorded in spreadsheet under section MP.8 in results.csv. In the matching step with the descriptor distance ratio set to 0.8

## MP.9

The average time taken across all images for keypoint detection and descriptor extraction can be found under section MP.9 in the spreadsheet in results.csv. Based on the average time taken across all images, the three detector/descriptor combinations with the lowest computation time are: FAST/ORB at about 6ms, FAST/BRIEF at about 7ms, and FAST/BRISK at about 8ms. If only speed is to be considered, these three detector/descriptor combinations would be the best for detecting keypoints on vehicles.