The Project
---


Video-Link:  https://www.youtube.com/watch?v=vQktBCCi7SI&feature=youtu.be

The goals / steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.


##Camera Calibration
To plot the true image we have to calibrate our camera. We calibrate our camera by detecting corners on Chessboardimages. If we located the corners we store these points in vectors. After checking all Chessboardimages and storing those cornerpoints, we feed those vectors to the function `cv2.calbrateCamera()` to obtain the parameters `ret, mtx ,dist ,rvecs ,tvecs`  which we feed to the function`cv2.undistort(params)`  which returns an undistorted image.

![Undistorted images](text/Undist.png?raw=true)

![Undistorted images](text/dsttt.PNG?raw=true)
---

##Sobel Filter 
To compute the gradients of a gray image I applied all Sobelfiltertechniques in the following combination:
(DirectionSobel bitwise and XSobel) or (DirectionSobel bitwise and YSobel) or (DirectionSobel and MagnitudeSobel)
The output is in image 3:

![Sobel images](text/sobel.PNG?raw=true)

##Color Threshold
After several hours of trying I decided to implement the H,V and L values.
V_threshold=(218,255)
S_treshold=(90,255)
H_treshold=(190,235)

![Color images](text/colorthresh.PNG?raw=true)

And here's the final output:

![Color images](text/finalcolor.PNG?raw=true)

---
## 4. Birdseyeview
To obtain the Birdseyeview we draw / choose 4 points from the original image and feed their location to the function 
M = cv2.getPerspectiveTransform(pts1,pts2)
which output we feed to:
dst = cv2.warpPerspective(imagek,M,(image.shape[1],image.shape[0]))

The result is given in image 6:
![Color images](text/bird.PNG?raw=true)

---
## 5 Sliding Window

After we transformed the image to a birdseyeview we apply a histogram on the lower part of the image. After we detected the lanelinepeaks we start searching for good pixels. We divided the image in 11 levels where we're searching for good lane line pixels.
![Color images](text/slide.PNG?raw=true)
Afterwards we fit a spline through those good pixels, 
![Color images](text/fitt.PNG?raw=true)
fill the plane between both splines with color and rewarp / transform the lane line detection back to the original image. The final result is given in the following image:

![Color images](text/finnnn.PNG?raw=true)
## Conclusion

This pipeline works for the project video but fails on both challenge videos. 
To improve this pipeline I should apply adapting colortresholding. If my pipeline detects certain brightness or contrast it should switch between several options to detect lanelines based on an if else architecture. I could work with convolutions to reduce my computation time. 
