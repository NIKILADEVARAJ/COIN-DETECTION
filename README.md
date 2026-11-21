# WORKSHOP 4: COIN DETECTION USING OPENCV

## NAME: NIKILA D
## REG NO: 212224230187

## Aim
To detect and count coins in an image using OpenCV image processing techniques such as grayscale conversion, Gaussian Blur, Canny Edge Detection, and Contour Detection.

## Requirements
- Python
- OpenCV
- NumPy
- Matplotlib
- Jupyter Notebook

## Program 
```PYTHON
import cv2
import numpy as np
import matplotlib.pyplot as plt
import os

image_path = "coin.png"

# Load image
image = cv2.imread(image_path)

if image is None:
    raise FileNotFoundError(f"Image not found at {image_path}")

gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

blurred = cv2.GaussianBlur(gray, (11, 11), 0)

edges = cv2.Canny(blurred, 30, 150)

contours, _ = cv2.findContours(
    edges.copy(),
    cv2.RETR_EXTERNAL,
    cv2.CHAIN_APPROX_SIMPLE
)

output = image.copy()

coin_count = 0

for contour in contours:
    # Filter out small contours (noise)
    area = cv2.contourArea(contour)

    if area < 300:
        continue

    # Draw contour
    ((x, y), radius) = cv2.minEnclosingCircle(contour)

    if radius > 15:
        coin_count += 1

        cv2.circle(
            output,
            (int(x), int(y)),
            int(radius),
            (0, 255, 0),
            2
        )

        cv2.putText(
            output,
            f"{coin_count}",
            (int(x - 10), int(y + 10)),
            cv2.FONT_HERSHEY_SIMPLEX,
            0.6,
            (0, 0, 255),
            2
        )

print(f"Total coins detected: {coin_count}")

plt.figure(figsize=(12, 6))

plt.subplot(1, 2, 1)
plt.title("Original Image")
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.axis("off")

plt.subplot(1, 2, 2)
plt.title(f"Detected Coins: {coin_count}")
plt.imshow(cv2.cvtColor(output, cv2.COLOR_BGR2RGB))
plt.axis("off")

plt.show()

fig, axs = plt.subplots(1, 5, figsize=(20, 6))

axs[0].imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
axs[0].set_title("Original Image")
axs[0].axis("off")

axs[1].imshow(gray, cmap='gray')
axs[1].set_title("Grayscale Image")
axs[1].axis("off")

axs[2].imshow(blurred, cmap='gray')
axs[2].set_title("Blurred Image")
axs[2].axis("off")

axs[3].imshow(edges, cmap='gray')
axs[3].set_title("Edge Detection (Canny)")
axs[3].axis("off")

axs[4].imshow(cv2.cvtColor(output, cv2.COLOR_BGR2RGB))
axs[4].set_title(f"Detected Coins: {coin_count}")
axs[4].axis("off")

plt.tight_layout()
plt.show()
```
## Algorithm
1. Import the required libraries.
2. Load the coin image.
3. Convert the image into grayscale.
4. Apply Gaussian Blur.
5. Perform Canny Edge Detection.
6. Find contours in the edge image.
7. Filter small contours based on area.
8. Detect coin boundaries using minimum enclosing circles.
9. Count the detected coins.
10. Display the original image and detected coin image.

## Output


<img width="1203" height="402" alt="image" src="https://github.com/user-attachments/assets/b902c9b1-cc87-403f-afa9-75e7dbb5f00c" />
<img width="1462" height="243" alt="image" src="https://github.com/user-attachments/assets/44a8d7a9-dee8-403e-9c39-e895500e3b5d" />

## Result
Thus, coins in the given image were successfully detected and counted using OpenCV through image preprocessing, edge detection, and contour detection techniques.
