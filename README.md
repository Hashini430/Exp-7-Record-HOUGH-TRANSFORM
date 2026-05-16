# Lane Detection

## Aim

To implement a basic lane detection pipeline using OpenCV by completing missing code segments at specified locations.

---

## Learning Objective

- Understand each stage of image processing
- Learn how to build a complete computer vision pipeline
- Practice writing code in guided sections

---

## Software Used

- Python 3.7
- Jupyter Notebook / VS Code
- OpenCV (cv2)
- NumPy
- Matplotlib

---

# Algorithm & Explanation

---

## Step 1: Import Libraries

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

---

## Step 2: Read the Image

```python
# Read the image using OpenCV

image = cv2.imread('lane.jpg')
image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
```

---

## Step 3: Convert to Grayscale

```python
# Convert to grayscale.

gray_image = cv2.cvtColor(image, cv2.COLOR_RGB2GRAY)
```

---

## Step 4: Display Images

```python
plt.figure(figsize=(10,5))

plt.subplot(1,2,1)
plt.imshow(image)
plt.title("Original Image")

plt.subplot(1,2,2)
plt.imshow(gray_image, cmap='gray')
plt.title("Grayscale Image")

plt.show()
```

---

## Step 5: Thresholding

```python
# Apply thresholding

_, threshold = cv2.threshold(gray_image, 150, 255, cv2.THRESH_BINARY)
```

---

## Step 6: Region of Interest (ROI)

```python
# ROI masking already provided
# (Do not modify)

height = threshold.shape[0]

polygons = np.array([
    [(200, height), (550, 250), (900, height)]
])

mask = np.zeros_like(threshold)

cv2.fillPoly(mask, polygons, 255)

roi_image = cv2.bitwise_and(threshold, mask)
```

---

## Step 7: Edge Detection (Canny)

```python
# Perform Edge Detection

edges = cv2.Canny(roi_image, 50, 150)
```

---

## Step 8: Gaussian Blur

```python
# Apply Gaussian Blur

blur = cv2.GaussianBlur(edges, (5,5), 0)
```

---

## Step 9: Hough Transform

```python
# Detect lines using Hough Transform

lines = cv2.HoughLinesP(
    blur,
    1,
    np.pi/180,
    threshold=50,
    minLineLength=50,
    maxLineGap=10
)
```

---

## Step 10: Lane Detection Logic

```python
# Already implemented
# (Do not modify)

line_image = np.copy(image)

if lines is not None:
    for line in lines:
        x1, y1, x2, y2 = line.reshape(4)
        cv2.line(line_image, (x1,y1), (x2,y2), (255,0,0), 5)

final_image = cv2.addWeighted(image, 0.8, line_image, 1, 1)

plt.figure(figsize=(10,5))
plt.imshow(final_image)
plt.title("Final Lane Detection Output")
plt.axis('off')
plt.show()
```

---

# Expected Output

- Original image
  <img width="693" height="460" alt="image" src="https://github.com/user-attachments/assets/77550067-7d60-4198-aa6e-9dc85fcd484a" />

- Grayscale image
  <img width="700" height="468" alt="image" src="https://github.com/user-attachments/assets/18b2d180-25ca-4497-8a3d-c8d92dd678c9" />
  
- Edge detected image
  <img width="712" height="473" alt="image" src="https://github.com/user-attachments/assets/9f419281-2416-43d5-9ad7-6317108084aa" />

- Final lane detection output
  <img width="692" height="472" alt="image" src="https://github.com/user-attachments/assets/fe2158f3-41eb-4da9-aa80-00d31c70408f" />


---

# Result

Thus, the lane detection pipeline is successfully implemented by completing the missing code sections. The system detects and highlights lane lines effectively.

---


