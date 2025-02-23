# VR_Assignment1_HymavathiJayaramappa_MT2024067

####
Part 1: Use computer vision techniques to Detect, segment, and count coins from an
image containing scattered Indian coins.
___________________________________________________________________________
#### a. Detect all coins in the image 
Use edge detection, to detect all coins in the image.
Visualize the detected coins by outlining them in the image.
#### b. Segmentation of Each Coin
Apply region-based segmentation techniques to isolate individual coins from the
image.
Provide segmented outputs for each detected coin.
#### c. Count the Total Number of Coins 
Write a function to count the total number of coins detected in the image.
Display the final count as an output.

### Introduction:
We need to take an indian coins image and have to applky edge detection techniqe to detetct the coins and counbt the number of coins and we heve to segment each coin by apppling region based detection.

Here is what followed:


Detect Coins Using Edge Detection:
Read the input image
Convert the image to grayscale.
Apply Gaussian blur to reduce noise.
Use Canny edge detection to identify edges.
Find contours from the edges to detect coins.
Draw the detected contours on the original image for visualization.

###### Part a is about detecting all coins using edge detection and outlining them. So,  edge detection techniques like Canny are commonly used. I used canny in my case, But before applying Canny, we probably have to convert the image to grayscale and  apply some blurring to reduce noise in the image because noise is quite common while capturing images . Then, using the edges,based on them we can draw the circle outline around them so we can  visualize the detection.
I have considered below input image


1. First converted this image into a grayscale image because Indian coins may have different colors and different uneven outlines.
 2. Applied Gaussian blur to reduce noise in the image even though the image i considered may not seem to have noise it is possible. I used 5*5 kernel size with 0 standard deviation since my image seems not having much noise and working fine with these values.
3. First used canny edge detection to detect the edges and separate the coins and detecting them and for region based separation used thresholding.
converting the image to grayscale, applying Otsu's thresholding to get a binary image.
4. Then, applied connected components to identify each coin. However, if coins are touching, connected components would consider them as one. So used morphological operations to separate them-Closing is a morphological operation that consists of dilation followed by erosion.It is used to fill small gaps or holes in objects, especially in binary images (like edge-detected images).This helps in connecting broken edges or removing small black regions inside white regions.
5. Used Hough Circle technique to extract the circular objects(coins) in the image,Extracted individual segmented by overlaying the blue contour around it and a green dot to highlight the center.
6. After performing region based segmentation counted the individual coins and displayed them.

### STEPS TO RUN
1. Ensure you have OpenCV installed:
  ```sh
  pip install opencv-python numpy matplotlib.pyplot
```
2. Make sure to update the input image path in the code as per its location.
3. Open the terminal, navigate to the script location, and run.
  ```sh
  python VR_Coin_Segmentation.py
```


##### Find the tested as well as input images in Image folder



--------------------------------------------------------------------------PART-2--------------------------------------------------------------------------------------


#### Part 2: Create a stitched panorama from multiple overlapping images.
___________________________________________________________________
a. Extract Key Points
Detect key points in overlapping images.
b. Image Stitching 
Use the extracted key points to align and stitch the images into a single panorama.
Provide the final panorama image as output.


## Image Stitching using SIFT, FLANN, and RANSAC

## Procedure and Techniques Followed  

To extract the key features of the image, I have used the **SIFT detector**.  

### **SIFT (Scale-Invariant Feature Transform)**
SIFT is an algorithm used to detect and describe local features in digital images. It locates key points and assigns them **descriptors** that are invariant to various transformations. These keypoints are extracted by the **SIFT detector**, and their descriptors are computed by the **SIFT descriptor**.  

It is also common to use the SIFT detector independently (computing only the keypoints) or the SIFT descriptor (computing only the descriptors).  

---

### **FLANN Matching**
To match the key points across the images, I have used **FLANN (Fast Library for Approximate Nearest Neighbors)**.  

FLANN is an image matching algorithm optimized for fast approximate nearest neighbor searches in high-dimensional spaces. It works faster than BFMatcher for large datasets but does not always find the absolute best match. FLANN utilizes:  
- **Tree-based approaches** for efficient search.  
- **Hierarchical clustering** for indexing feature descriptors.  
- **Various distance measures**, including Euclidean and cosine distances.  

FLANN is particularly beneficial for large datasets where exact nearest-neighbor searches are computationally expensive.  

---

### **RANSAC (Random Sample Consensus)**
RANSAC is used to estimate the transformation between images while **eliminating outliers**.  

#### **How RANSAC Works:**
1. **Randomly select** a small subset of data points and compute the model.  
2. **Determine inliers** by checking which points fit within an error threshold.  
3. **Repeat** the process until the best-fitting model is found.  

#### **Advantages of RANSAC:**
✅ Robust against outliers.  
✅ Can find accurate transformations even with noisy data.  

#### **Disadvantages of RANSAC:**
❌ No upper bound on computation time.  
❌ May not find an optimal solution if limited iterations are used.  
❌ Performs poorly if inliers are **less than 50%** of the dataset.  

---

### **Image Stitching Steps**
1. **Extract Key Features** using **SIFT detector**.  
2. **Match Key Points** using **FLANN Matching**.  
3. **Estimate Transformation** using **RANSAC** to find the **Homography Matrix**.  
4. **Warp Images** using the computed **Homography Matrix**.  
5. **Blend Images** to produce the final **stitched image**.  

---

## STEPS TO RUN
1. Ensure you have OpenCV installed:
  ```sh
  pip install opencv-python numpy matplotlib.pyplot
```
2. Make sure to update the input image path in the code as per its location.
3. Open the terminal, navigate to the script location, and run.
  ```sh
  python VR_ass1_part2.py

## INPUT AND OUTPUT FILES
* Input Images - left.jpg,right.jpg
* Keypoints - keypoints1.jpg,keypoints2.jpg
* Matches - matches.jpg
* Panoroma - panoroma.jpg







