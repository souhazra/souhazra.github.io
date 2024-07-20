---
layout: post
title:  "Image Segmentation: Dividing and Conquering"
author: Souren
categories: [Image Processing]
image: assets/images/dive_into_image_processing/image-segmentation.png
tags: [image]
---

# Image segmentation is a crucial step in image processing
 and computer vision, aimed at dividing an image into meaningful regions or objects. This process helps in understanding and analyzing the contents of an image by isolating objects of interest. In this blog, we’ll explore three common segmentation techniques: Thresholding, Region Growing, and Clustering.

## Thresholding

### What is Thresholding?
Thresholding is the simplest and most intuitive segmentation technique. It separates pixels based on their intensity values. By choosing a specific threshold value, we can classify pixels into foreground and background.

### How it Works
Pixels with intensity values above the threshold are classified as foreground (usually white), while those below are classified as background (usually black). This technique is particularly effective for images with a distinct contrast between the object and the background.

### Example
```python
import cv2

# Load an image in grayscale
image = cv2.imread('image.jpg', cv2.IMREAD_GRAYSCALE)

# Apply global thresholding
_, thresholded_image = cv2.threshold(image, 127, 255, cv2.THRESH_BINARY)

# Display results
cv2.imshow('Original Image', image)
cv2.imshow('Thresholded Image', thresholded_image)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

In this example, we use a global threshold value of 127 to segment the image.

## Region Growing

### What is Region Growing?
Region Growing is a more sophisticated technique that starts with a seed pixel and merges neighboring pixels with similar properties (e.g., intensity, color).

### How it Works
1. **Select a Seed Pixel**: Choose an initial pixel, often manually or using a predefined criterion.
2. **Merge Neighboring Pixels**: Expand the region by adding neighboring pixels that have similar properties to the seed pixel.
3. **Iterate**: Continue the process until no more pixels can be added to the region.

### Example
```python
import numpy as np

def region_growing(img, seed, threshold=5):
    height, width = img.shape
    segmented = np.zeros((height, width), np.uint8)
    seed_value = img[seed]
    stack = [seed]

    while stack:
        x, y = stack.pop()
        if segmented[x, y] == 0:
            segmented[x, y] = 255
            for dx in [-1, 0, 1]:
                for dy in [-1, 0, 1]:
                    nx, ny = x + dx, y + dy
                    if 0 <= nx < height and 0 <= ny < width:
                        if segmented[nx, ny] == 0 and abs(int(img[nx, ny]) - int(seed_value)) < threshold:
                            stack.append((nx, ny))
    return segmented

# Load an image in grayscale
image = cv2.imread('image.jpg', cv2.IMREAD_GRAYSCALE)
seed_point = (100, 100)  # Example seed point
segmented_image = region_growing(image, seed_point)

# Display results
cv2.imshow('Original Image', image)
cv2.imshow('Segmented Image', segmented_image)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

In this example, we use a seed point and a threshold value to perform region growing segmentation.

## Clustering

### What is Clustering?
Clustering groups pixels into clusters based on some similarity measure, such as color or intensity. The most common clustering algorithm used for segmentation is K-means clustering.

### How it Works
1. **Initialize Centroids**: Randomly initialize K centroids.
2. **Assign Pixels to Clusters**: Assign each pixel to the nearest centroid based on a similarity measure.
3. **Update Centroids**: Recompute the centroids as the mean of all pixels assigned to each cluster.
4. **Iterate**: Repeat the assignment and update steps until convergence.

### Example
```python
import cv2
import numpy as np

# Load an image in color
image = cv2.imread('image.jpg')
Z = image.reshape((-1, 3))

# Convert to float32
Z = np.float32(Z)

# Define criteria and apply KMeans
criteria = (cv2.TERM_CRITERIA_EPS + cv2.TERM_CRITERIA_MAX_ITER, 10, 1.0)
K = 3
_, labels, centers = cv2.kmeans(Z, K, None, criteria, 10, cv2.KMEANS_RANDOM_CENTERS)

# Convert back to uint8 and reshape
centers = np.uint8(centers)
segmented_image = centers[labels.flatten()]
segmented_image = segmented_image.reshape((image.shape))

# Display results
cv2.imshow('Original Image', image)
cv2.imshow('Segmented Image', segmented_image)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

In this example, we use K-means clustering to segment an image into K clusters based on color similarity.

## Conclusion

Image segmentation is a powerful tool for dividing an image into meaningful regions or objects. Whether using simple thresholding, more advanced region growing, or clustering techniques, segmentation helps in understanding and analyzing visual data. By mastering these techniques, you can unlock new possibilities in image processing and computer vision.