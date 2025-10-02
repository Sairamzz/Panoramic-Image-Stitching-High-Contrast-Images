# Panorama Stitching – High Contrast Images

This project implements a feature-based image stitching pipeline to create panoramas from high contrast images. The approach combines Harris corner detection with SIFT descriptors for feature extraction, followed by feature matching, homography estimation, and image blending.

Functions Overview
1. ``` harris(I, N=100, **kwargs) ```

Implements the Harris corner detector to identify interest points in grayscale images. The function supports Gaussian smoothing, frequency-domain convolution, tiling-based keypoint selection, and visualization of detected corners.

2. gaussian_kernel(size, sigma)

Generates a normalized 2D Gaussian kernel, used for smoothing image gradients in Harris detection.

3. load_images(path)

Loads and converts images from a given folder into RGB format. Also provides a visualization of all input images in sequence.

4. detect_and_compute_keypoints(img)

Combines Harris corners with SIFT descriptors. Harris points are first detected, then converted into OpenCV keypoints, and finally refined with SIFT descriptors for robust feature representation.

5. match_features(des1, des2)

Uses a brute-force matcher (BFMatcher with L2 norm) to find correspondences between descriptors of two images. Applies Lowe’s ratio test to filter good matches.

6. draw_matches(img1, img2, kp1, kp2, matches, num_matches=100)

Visualizes the top feature matches between two images, aiding debugging and inspection of alignment quality.

7. warpPerspectivePadded(src, dst, H, ...)

Applies homography-based warping with padding to handle alignment and ensure stitched images fit within a single canvas.

8. masking(bot, top, alpha)

Blends two images using alpha blending, ensuring smooth transitions while preserving non-overlapping regions.

9. stitch_images(img1, img2, kp1, kp2, matches)

Computes homography between two images, warps them into alignment, and blends them to create a stitched output.

10. create_panorama(images)

Main driver function: iteratively stitches a sequence of images into a panorama by detecting features, matching descriptors, computing homographies, and blending results.
