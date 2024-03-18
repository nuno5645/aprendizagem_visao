# Deep Learning for Computer Vision Challenges

Welcome to the repository for the **Deep Learning for Computer Vision** course challenges. This space hosts the code and reports for a series of tasks that deal with advanced image processing and machine learning techniques to tackle complex computer vision problems.

## Challenge 1: Coin Detection

The first challenge involves creating an algorithm capable of detecting coins in images using morphological operations and computer vision techniques. The code for this challenge leverages the OpenCV library to process the images and identify the coins.

### Challenge 1 Contents

The Python script `find_coins.py` performs the following operations:

- Reading and converting images to grayscale.
- Smoothing images to reduce noise.
- Image binarization using Otsu's method.
- Applying morphological operations to highlight the coins.
- Detecting and counting coins using connected components.
- Calculating the relative error between the actual and detected number of coins.
- Testing different iteration values to refine detection.
- Saving detection results for further analysis.
