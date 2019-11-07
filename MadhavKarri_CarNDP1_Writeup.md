# **Self-Driving Car**
# **Project: Finding Lane Lines on the Road**

## MK

**Overview**

Detect highway lane lines in images using Python and OpenCV, a package that has many useful tools for analyzing images.

The goals/steps for this project: build a pipeline that finds lane lines on the road

**Finding Lane Lines on Static Images/Frames**

Steps/process when working on Static Images/Frames
* Load all neccessary python imports
* Implement Gaussian Blur and Canny Edge Detection. For a single static image/frame fine tune parameters such as kernel size, low threshold and high threshold
* Followed by Masking and P-Hough Transform to extract lines and line-coordinates
* Calculate slopes for all line-coordinates from the previous step. Use the change in sign of slope values to segregrate lines and line-coordinates for each of the left and right lanes.
* To draw lines 
  - Slope (parameter m) and intercept (parameter b) in "y=mx+b" for each of the left and right lane lines were determined
  - The maximum y-coordinate for all images (bottom) was determined to be 540 (from image size). Using this y-coordinate, x-cordiante for each of the left and right lanes were determined using "m" and "b" parameters
  - Determine minimum y coordinates at top edge of the masking region: minimum y-coordinate from all the detected line-cordinates from P-Hough Transform for each of the left and right lanes were extracted. Corresponding x-coordiantes were determined using "m" and "b" parameters

The above set of steps were repeated on the following set of images
* solidWhiteRight.jpg
* solidWhiteCurve.jpg
* solidYellowLeft.jpg
* solidYellowCurve.jpg
* solidYellowCurve2.jpg
* whiteCarLaneSwitch.jpg


Results for solid-white-curve:

Python Code/Implementation: [Link](./MadhavKarri-Project1-Files/solidWhiteCurve-Copy1.ipynb)

* Gaussian Blur and Canny Edge Detection
![WI_SolidWhiteCurve1](./Writeup_IV/WI_SolidWhiteCurve1.png)
* Masking and P-Hough Transform
![WI_SolidWhiteCurve2](./Writeup_IV/WI_SolidWhiteCurve2.png)
* Final Output
![WI_SolidWhiteCurve3](./Writeup_IV/WI_SolidWhiteCurve3.png)

**Finding Lane Lines in a Video**

- Following are the pipeline/steps implemented for finding lane lines in a video
  - Implemented a python code to extract raw fraemes/static images from a video file
![WI_SolidWhiteRightV1](./Writeup_IV/WI_SolidWhiteRightV1.png)

  - Implemented a pipeline consisting primarily of 1 main function and 3 call-back function definitions:
    - Function1: "my_ced" that implements Canny Edge Detection 
      - Input: ".jpg" image file
      - Output: edges from the Canny Edge Detection algorithm
    - Function2: "my_mpht" that implements Masking and P-Hough Transform to get line and line-coordinates.
      - Input: ".jpg" image file, masking coordiantes, and edges output from ("my_ced") Canny Edge Detection algorithm
      - Output: co-ordinates for all the lines detected by P-Hough Transform and consequently "m-slope" and "b-intercept" parameters
    - Function3: "my_fld" that implements drawing final lines and adding transperency
      - Input: ".jpg" image file and co-ordinates of all the lines detected by P-Hough Transform
      - Output: Original raw image/frame overlayed with detected/predicted lane lines
      - Extras: In addition this function also adds trasparency and saves the final output as a ".jpg file"
    - Main Function/Wrapper: A while loop that calls Functions 1, 2, 3 repeatedly on each of the image frames extracted from the original video.

  - Implemented a python code to stich final output frames from the preceeding steps and convert it into a video
![WI_SolidWhiteRightV2](./Writeup_IV/WI_SolidWhiteRightV2.png)

**Final Video Output**

 - Solid White Right
   - Python Code/Implementation: [Link](./MadhavKarri-Project1-Files/Porject1Video-SolidWhiteRight/solidWhiteRight-mp4.ipynb)
   - Video Output File: [Link](./Writeup_IV/solidWhiteRight_fo.mp4)

  - Solid Yellow Left
    - Python Code/Implementation: [Link](./MadhavKarri-Project1-Files/Porject1Video-SolidWhiteRight/solidYellowLeft-mp4.ipynb)
    - Video Output File: [Link](./Writeup_IV/solidYellowLeft_fo.mp4) 
      
---

### Reflection

### Potential shortcomings with the current pipeline
- A lot of manual processing is involved with the exisiting pipeline.
  - Manual picking of masking co-ordinates
  - Fine tuning parameters for each of the Gaussian Blur/Canny Edge Detection/Masking/P-Hough Transform steps, specifically on each individual frames
  - Spurious or unwanted slopes, when segregating slopes to detect line segments associated with each of the left and right lanes

### Possible improvements to pipeline
- Research/Implement detection of arc/curvature line segments available in opencv
- Automate the process either through Machine Learning/AI for the following set of tasks
  - To pick optimal co-ordinates for masking
  - To reject spurious or unwanted slopes during slope segregation to identiyf left and right lanes
- Using mapping and localization explore possibility to detect and utilize priori information on lane coordinates and curvature
- Currently in the videos the lane detection lines are bumpy. The bumpiness can be minimized by adding weights during averaging of slopes. 

### Optional Challange
- Code that produced SolidYellowLeft.mp4 was attempted to detect lane lines. Although, it performed well on a good number of frames, it had issues detecting lane lines over the bridge.
- Tried modifying different parameters and found out converting the original raw image/frame using color space conversion code to hsv within cv2.cvtcolor resulted in optimal detection of the yellow and white lanes through all the frames in the video
- Solid Yellow Left
  - Python Code/Implementation: [Link](./MadhavKarri-Project1-Files/Porject1Video-Challenge/Challenge-mp4.ipynb)
  - Video Output File: [Link](./Writeup_IV/Challenge_fo.mp4)
