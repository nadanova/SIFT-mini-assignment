# SIFT Object Detection Project

## Table of Contents
- [Overview](#overview)
- [Requirements](#requirements)
- [How the Code Works](#how-the-code-works)
  - [Image Object Detection](#image-object-detection)
  - [Video Object Detection (Bonus)](#video-object-detection-bonus)
- [Results](#results)
  - [Test Images](#test-images)
  - [Bonus: Video Detection](#bonus-video-detection)
- [Discussion](#discussion)
- [How to Run](#how-to-run)
- [References](#references)

---

## Overview

This project demonstrates **object detection using SIFT (Scale-Invariant Feature Transform)** in Python and OpenCV.  
Given a query image (the object you want to find) and a target image (or video), the code detects and highlights the location of the query object in the target using robust feature matching.

The project covers:
- SIFT-based matching between a query and a target image.
- Drawing detected object location in the target image.
- (Bonus) Detecting and marking the object in each frame of a video.

---

## Requirements

- Python 3.7+
- OpenCV (`opencv-python`)
- NumPy

For running in Google Colab, add:
- `from google.colab.patches import cv2_imshow` for image display

Install requirements with:
```bash
pip install opencv-python numpy
```

---

## How the Code Works

### Image Object Detection

1. **Feature Extraction:**  
   SIFT detects keypoints and computes descriptors in both the query and the target images.

2. **Feature Matching:**  
   Descriptors are matched using FLANN-based matcher. Lowe's ratio test is used to filter for good matches.

3. **Homography Estimation:**  
   If enough matches are found, a homography is computed using RANSAC to estimate the object's location and orientation in the target.

4. **Visualization:**  
   The detected object outline is drawn in the target image, along with green circles marking the inlier matched keypoints.

### Video Object Detection (Bonus)

- The SIFT detection pipeline is applied to every frame of a video.
- If the object is detected in a frame, its outline is drawn.
- The output is saved as a new video with detection visualizations.

---

## Results

### Test Images

Below are the results for three example target images using a single query object image.

#### 1. **Test Image 1**

*Query and Target:*
![Query Image 1](main/passport.jpg)
![Target Image 1](main/table.jpg)

*Detection Result:*
![Detection 1](main/tableR.jpg)

#### 2. **Test Image 2**

*Query and Target:*
![Query Image 2](main/tshirt.jpg)
![Target Image 2](main/everything.jpg)

*Detection Result:*
![Detection 2](main/everythingR.jpg)

#### 3. **Test Image 3**

*Query and Target:*
![Query Image 3](main/everthing.jpg)
![Target Image 3](main/tool_box.jpg)

*Detection Result:*
![Detection 3](main/tool_box_R.jpg)

#### 4. **Test Image 4**

*Query and Target:*
![Query Image 4](main/socks.jpg)
![Target Image 4](main/table_lighter.jpg)



*Detection Result:*
![Detection 3](results/targetR.jpg)
---

### Bonus: Video Detection

- **Input video:** A sample video containing the object moving or appearing in different frames.
- **Output:**  
  The result video highlights the detected object in green for each frame where it is found.

[![Demo Video](results/queryAA.jpg)](results/output_detected_(4).mp4)
*(Click to view the video)*

---

## Discussion

### Strengths
- SIFT is robust to scale, rotation, and moderate illumination change.
- Homography estimation filters out false matches and localizes the object accurately.

### Limitations
- SIFT may fail if the object has few distinctive features (e.g., smooth, textureless regions).
- Detection can be slow on large images or videos due to the computational cost of SIFT.
- Highly cluttered backgrounds or occlusions may reduce accuracy.

### Practical Notes
- For best results, the query image should be a clear, tightly-cropped view of the object.
- If SIFT struggles (few matches), consider using template matching or deep learning for more challenging cases.

---

## How to Run

### 1. Prepare your images and/or video
- Place your query images and target images/videos in the project directory.

### 2. Run the Python scripts

#### Image detection:
```python
# Replace with your image paths
query_image_path = "query1.jpg"
target_image_path = "target1.jpg"
# Run the function (see sift_image_detection.py for full code)
feature_matching(query_image_path, target_image_path, use_sift=True)
```

#### Video detection:
```python
query_image_path = "querya.jpg"
video_path = "test_video.mp4"
output_video_path = "output_detected.mp4"
video_object_detection(query_image_path, video_path, output_video_path)
```

- Output images and video will be saved in the results directory.

---

## References

- [OpenCV SIFT documentation](https://docs.opencv.org/4.x/da/df5/tutorial_py_sift_intro.html)
- [Feature Matching with FLANN](https://docs.opencv.org/4.x/dc/dc3/tutorial_py_matcher.html)
- [Lowe, D. G. (2004). "Distinctive Image Features from Scale-Invariant Keypoints"](https://www.cs.ubc.ca/~lowe/papers/ijcv04.pdf)

---
