# workshop-1
# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look
Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
Detects the face in an image.
Places a stylish sunglass overlay perfectly on the face.
Works seamlessly with individual passport-size photos.
Customizable for different sunglasses styles or photo types.

## Technologies Used:
1.Python
2.OpenCV for image processing
3.Numpy for array manipulations

## How to Use:
Clone this repository.
Add your passport-sized photo to the images folder.
Run the script to see your "cool" transformation

## program:

developed by LITYA M              REGNO:-212225230152

```
# Import libraries

import cv2
import numpy as np
import matplotlib.pyplot as plt
# Load the passport photo

img = cv2.imread("passport.jpg")

# Check if the image was loaded correctly
if img is None:
    print("Image not found. Check the file name and path.")
else:
    print("Passport photo loaded successfully!")

# Convert BGR to RGB for displaying with Matplotlib
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

# Display the original image
plt.figure(figsize=(5, 5))
plt.imshow(img_rgb)
plt.axis("off")
plt.title("Original Passport Photo")
plt.show()
# Load the sunglasses image

sunglasses = cv2.imread("sunglass.jpg")

# Check if the sunglasses image was loaded
if sunglasses is None:
    print("Sunglasses image not found. Check the file name and path.")
else:
    print("Sunglasses image loaded successfully!")

    # Convert BGR to RGB for Matplotlib
    sunglasses_rgb = cv2.cvtColor(sunglasses, cv2.COLOR_BGR2RGB)

    # Display the sunglasses
    plt.figure(figsize=(6, 3))
    plt.imshow(sunglasses_rgb)
    plt.axis("off")
    plt.title("Sunglasses")
    plt.show()
# Check the size of the passport photo

height, width = img.shape[:2]

print("Image width :", width)
print("Image height:", height)

# Display the image with a coordinate grid
plt.figure(figsize=(6, 6))
plt.imshow(img_rgb)

plt.xticks(range(0, width, max(1, width // 10)))
plt.yticks(range(0, height, max(1, height // 10)))
plt.grid()

plt.title("Find the Eye Region Coordinates")
plt.show()
# Eye region coordinates

x = 140
y = 480
w = 300
h = 130

# Crop the eye region
eye_region = img[y:y+h, x:x+w]

# Display the selected eye region
eye_region_rgb = cv2.cvtColor(eye_region, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(8, 3))
plt.imshow(eye_region_rgb)
plt.axis("off")
plt.title("Selected Eye Region")
plt.show()
# Resize sunglasses to fit the eye region

sunglasses_resized = cv2.resize(sunglasses, (w, h))

# Convert to RGB for displaying
sunglasses_resized_rgb = cv2.cvtColor(
    sunglasses_resized,
    cv2.COLOR_BGR2RGB
)

# Display resized sunglasses
plt.figure(figsize=(8, 3))
plt.imshow(sunglasses_resized_rgb)
plt.axis("off")
plt.title("Resized Sunglasses")
plt.show()
# Convert sunglasses to grayscale
gray_sunglasses = cv2.cvtColor(sunglasses_resized, cv2.COLOR_BGR2GRAY)

# Create a binary mask
# Dark sunglasses = white in the mask
_, mask = cv2.threshold(
    gray_sunglasses,
    240,
    255,
    cv2.THRESH_BINARY_INV
)
# Get the eye region from the passport photo
eye_region = img[y:y+h, x:x+w]

# Create the inverse mask
mask_inv = cv2.bitwise_not(mask)

# Remove the background from the eye region
background = cv2.bitwise_and(
    eye_region,
    eye_region,
    mask=mask_inv
)

# Keep only the sunglasses
foreground = cv2.bitwise_and(
    sunglasses_resized,
    sunglasses_resized,
    mask=mask
)

# Combine the background and sunglasses
combined = cv2.add(background, foreground)

# Copy the combined image back into the passport photo
result = img.copy()
result[y:y+h, x:x+w] = combined

# Convert result to RGB
result_rgb = cv2.cvtColor(result, cv2.COLOR_BGR2RGB)

# Display final image
plt.figure(figsize=(6, 8))
plt.imshow(result_rgb)
plt.axis("off")
plt.title("Passport Photo with Sunglasses")
plt.show()

# Display the mask
plt.figure(figsize=(8, 3))
plt.imshow(mask, cmap="gray")
plt.axis("off")
plt.title("Sunglasses Mask")
plt.show()
# Save the final image

output_path = "final_sunglasses.jpg"

cv2.imwrite(output_path, result)

print("Final image saved successfully!")
print("File name:", output_path)
```
## output
<img width="260" height="517" alt="image" src="https://github.com/user-attachments/assets/a9b25298-b6ba-4fdd-9c5e-b8b3bffbfdae" />

<img width="502" height="275" alt="image" src="https://github.com/user-attachments/assets/f34f5c11-e44a-49f4-9a9c-7822a3271690" />

<img width="462" height="657" alt="image" src="https://github.com/user-attachments/assets/049c4fe5-7aca-4973-993a-f2d8f8522824" />

<img width="877" height="337" alt="image" src="https://github.com/user-attachments/assets/71153776-e7a4-43ce-937b-400934615431" />

<img width="781" height="305" alt="image" src="https://github.com/user-attachments/assets/36c322c7-b305-4e43-a2d3-ea9d4706ac6b" />

<img width="787" height="335" alt="image" src="https://github.com/user-attachments/assets/70fadec7-b058-42f3-8007-c34a68983215" />

<img width="400" height="752" alt="image" src="https://github.com/user-attachments/assets/1a1a40d5-d141-44b9-b037-c64f4125362d" />

## Applications:
1.Learning basic image processing techniques.
2.Adding flair to your photos for fun.
3.Practicing computer vision workflows.

## Result
The passport-size image was successfully processed using OpenCV by overlaying a pair of sunglasses onto the eye region. Image masking and alpha blending techniques were used to ensure the sunglasses blended naturally with the original image. The final output demonstrates the successful implementation of image overlay and basic image manipulation using OpenCV.
