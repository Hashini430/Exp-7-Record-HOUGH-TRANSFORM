# Exp-7-Record-HOUGH-TRANSFORM
#  Lane Detection

##  Aim

To implement a basic lane detection pipeline using OpenCV by completing missing code segments at specified locations.

---

## Learning Objective

* Understand each stage of image processing
* Learn how to build a complete computer vision pipeline
* Practice writing code in guided sections

**Important Instruction:**
👉 Write code **ONLY in places marked as `# Your Code Here`**
👉 Do NOT modify any other part of the code

---

##  Software Used

* Anaconda – Python 3.7
* Jupyter Notebook / VS Code
* OpenCV (cv2)
* NumPy
* Matplotlib


###  Step 1: Import Libraries

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

# Step 2: Read the Image
# Read the image using OpenCV

###
# Your Code Here
###
image = cv2.imread('lane.jpg')
image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

# Step 3: Convert to Grayscale
# Convert to grayscale.

###
# Your Code Here
###
gray_image = cv2.cvtColor(image, cv2.COLOR_RGB2GRAY)

# Step 4: Display Images
plt.figure(figsize=(10,5))

###
# Your Code Here
###
plt.subplot(1,2,1)
plt.imshow(image)
plt.title("Original Image")

plt.subplot(1,2,2)
plt.imshow(gray_image, cmap='gray')
plt.title("Grayscale Image")

plt.show()

# Step 5: Thresholding
# Apply thresholding

threshold = 
###
# Your Code Here
###
_, threshold = cv2.threshold(gray_image, 150, 255, cv2.THRESH_BINARY)

plt.imshow(threshold, cmap='gray')
plt.title("Threshold Image")
plt.show()

# Step 6: Region of Interest (ROI)
# ROI masking already provided
# (Do not modify)

height = threshold.shape[0]
polygons = np.array([
    [(200, height), (550, 250), (900, height)]
])

mask = np.zeros_like(threshold)
cv2.fillPoly(mask, polygons, 255)
roi_image = cv2.bitwise_and(threshold, mask)

plt.imshow(roi_image, cmap='gray')
plt.title("ROI Masked Image")
plt.show()

# Step 7: Edge Detection (Canny)
# Perform Edge Detection

###
# Your Code Here
###
edges = cv2.Canny(roi_image, 50, 150)

plt.imshow(edges, cmap='gray')
plt.title("Edge Detection")
plt.show()

# Step 8: Gaussian Blur
# Apply Gaussian Blur

###
# Your Code Here
###
blur = cv2.GaussianBlur(edges, (5,5), 0)

plt.imshow(blur, cmap='gray')
plt.title("Gaussian Blur")
plt.show()

# Step 9: Hough Transform
# Detect lines using Hough Transform

###
# Your Code Here
###
lines = cv2.HoughLinesP(
    blur,
    1,
    np.pi/180,
    threshold=50,
    minLineLength=50,
    maxLineGap=10
)

line_image = np.copy(image)

if lines is not None:
    for line in lines:
        x1, y1, x2, y2 = line.reshape(4)
        cv2.line(line_image, (x1,y1), (x2,y2), (255,0,0), 5)

plt.imshow(line_image)
plt.title("Detected Lines")
plt.show()

# Step 10: Lane Detection Logic
# Already implemented
# (Do not modify)

# Final Output
final_image = cv2.addWeighted(image, 0.8, line_image, 1, 1)

plt.figure(figsize=(10,5))
plt.imshow(final_image)
plt.title("Final Lane Detection Output")
plt.axis('off')
plt.show()

# Result
print("Thus, the lane detection pipeline is successfully implemented.")

# Developed By
# Name: Hashini R
# Register No: 212224240055
