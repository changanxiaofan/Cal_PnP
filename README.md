# Cal_PnP

This repository contains our C++ implementation of semi-automatic camera calibration based on Perspective-n-Point (PnP). It can be used to compute the homography matrix and manually correct radial distortion. 

## Introduction

This package is designed for computing camera homography matrix. The input includes a set of 3D points on the 3D ground plane and the corresponding 2D pixel points. We adopt the Perspective-n-Point (PnP) for camera calibration. The user can choose from different approaches such as (1) a regular method using all the points, (2) RANSAC-based robust method or (3) Least-Median robust method. The package also includes tools for manual 2D points selection. 

## Coding Structure
1. `./obj/` folder: Libraries of .cpp files
2. `./src/` folder: Source code
3. `./data/` folder: Example input files
   1. `cfg.json`: Configuration parameters in JSON format
   2. `frm.jpg`: Input frame image

## How to Build
1. Download and make the OpenCV library.
2. Compile using g++ in Linux environment. If you are new to g++ compilation with OpenCV, please refer to this [link](http://answers.opencv.org/question/25642/how-to-compile-basic-opencv-program-in-c-in-ubuntu/). In the command window, you can `cd` to the directory of `./Cal_PnP-master/` and use the following command to compile our source code, where `bin` is the executable file generated.  
```g++ -I/usr/local/include/ -L/usr/local/lib/ -g -o bin ./src/main.cpp ./src/Cfg.cpp ./src/CamCal.cpp -lopencv_core -lopencv_imgproc -lopencv_highgui -lopencv_imgcodecs -lopencv_calib3d -lm```

## How to Use
1. Set the corresponding input/output paths in the configuration file if necessary. 
2. Provide the coordinates of a set of 3D points on the ground plane (or any plane of interest). One way to do so is to find the GPS coordinates using [Google Maps](https://www.google.com/maps). 

<div align="center">
    <img src="/pic/pic0.png", width="611">
</div>

3. If the user wants to select the corresponding 2D pixel points on the image, set `calSel2dPtFlg` to 1. A new window called `selector of 2D points` pops out. The user can click on the image to select each 2D point. A blue circle stands for each click. After the selection is done, click `o`. Please make sure the number of selected 2D points should be the same as the provided 3D points (in the same order). During the selection, if mis-clicking on wrong places, the user can press `r`. All the markers will be cleared, and s/he can start over.

<div align="center">
    <img src="/pic/pic1.jpg", width="640">
</div>

4. If there exists redial distortion, the frame image can be manually corrected by by setting `calDistFlg` to 1 and providing the distortion coefficients (`calDistCoeff`) and intrinsic camera parameters (`calFocLen` and `calPrinPt`). 

<div align="center">
    <img src="/pic/pic2.jpg", width="640">
</div>

5. The user can choose to output the display image (with a colorful grid on the 3D plane) by setting `outCalDispFlg` to 1. 

## Disclaimer
For any question you can contact [Zheng (Thomas) Tang](https://github.com/zhengthomastang).


