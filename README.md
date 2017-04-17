The Project
---

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
## Sliding Window


The images for camera calibration are stored in the folder called `camera_cal`.  The images in `test_images` are for testing your pipeline on single frames.  If you want to extract more test images from the videos, you can simply use an image writing method like `cv2.imwrite()`, i.e., you can read the video in frame by frame as usual, and for frames you want to save for later you can write to an image file.  

To help the reviewer examine your work, please save examples of the output from each stage of your pipeline in the folder called `ouput_images`, and include a description in your writeup for the project of what each image shows.    The video called `project_video.mp4` is the video your pipeline should work well on.  

The `challenge_video.mp4` video is an extra (and optional) challenge for you if you want to test your pipeline under somewhat trickier conditions.  The `harder_challenge.mp4` video is another optional challenge and is brutal!

If you're feeling ambitious (again, totally optional though), don't stop there!  We encourage you to go out and take video of your own, calibrate your camera and show us how you would implement this project from scratch!
