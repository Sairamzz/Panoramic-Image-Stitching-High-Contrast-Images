# Panorama Stitching – High Contrast Images

This project implements a feature-based image stitching pipeline to create panoramas from high contrast images. The approach combines Harris corner detection with SIFT descriptors for feature extraction, followed by feature matching, homography estimation, and image blending.

## Functions Overview:
1. ``` harris(I, N=100, **kwargs) ```

Implements the Harris corner detector to identify interest points in grayscale images. The function supports Gaussian smoothing, frequency-domain convolution, tiling-based keypoint selection, and visualization of detected corners.

2. ``` gaussian_kernel(size, sigma) ```

Generates a normalized 2D Gaussian kernel, used for smoothing image gradients in Harris detection.

3. ``` load_images(path) ```

Loads and converts images from a given folder into RGB format. Also provides a visualization of all input images in sequence.

4. ``` detect_and_compute_keypoints(img) ```

Combines Harris corners with SIFT descriptors. Harris points are first detected, then converted into OpenCV keypoints, and finally refined with SIFT descriptors for robust feature representation.

5. ``` match_features(des1, des2) ```

Uses a brute-force matcher (BFMatcher with L2 norm) to find correspondences between descriptors of two images. Applies Lowe’s ratio test to filter good matches.

6. ``` draw_matches(img1, img2, kp1, kp2, matches, num_matches=100) ```

Visualizes the top feature matches between two images, aiding debugging and inspection of alignment quality.

7. ``` warpPerspectivePadded(src, dst, H, ...) ```

Applies homography-based warping with padding to handle alignment and ensure stitched images fit within a single canvas.

8. ``` masking(bot, top, alpha) ```

Blends two images using alpha blending, ensuring smooth transitions while preserving non-overlapping regions.

9. ``` stitch_images(img1, img2, kp1, kp2, matches) ```

Computes homography between two images, warps them into alignment, and blends them to create a stitched output.

10. ``` create_panorama(images) ```

Main driver function: iteratively stitches a sequence of images into a panorama by detecting features, matching descriptors, computing homographies, and blending results.

## Results:

### 50% Overlap - Murals 1:

<img width="950" height="426" alt="image" src="https://github.com/user-attachments/assets/ed7c10a9-fbe3-441e-a718-abc31d443207" />

### 50% Overlap - Murals 2:

<img width="950" height="504" alt="image" src="https://github.com/user-attachments/assets/9275fe36-31c5-4c44-b316-72350af64878" />

### 50% Overlap - Brick wall:

<img width="950" height="416" alt="image" src="https://github.com/user-attachments/assets/0e5f34cd-da90-4785-9f04-1526fa48959a" />

### 50% Overlap - Cement wall:

<img width="950" height="425" alt="image" src="https://github.com/user-attachments/assets/f9ae8d5e-0b22-4b12-bf01-673938cc1064" />

### 15% Overlap:

<img width="950" height="428" alt="image" src="https://github.com/user-attachments/assets/c1edb800-6822-491a-b40c-36ed6b682e40" />

## Conclusion:

The panorama stitching algorithm successfully produced the desired panoramic images across different scenarios, demonstrating the robustness of the feature detection and matching techniques employed. The keypoints were detected using Harris corner detectors, and the feature descriptors were formulated from SIFT (Scale-Invariant Feature Transform). The Opencv provided us with all the requirements for this Lab assignment.

### >50% Overlapping Mural Images:
The high degree of overlap and distinct, well-defined features in the mural allowed for accurate feature detection and matching by the algorithm.

### >50% Overlapping Wall Images:
Despite the uniform texture and repetitive patterns in the wall images, the algorithm managed to align the images effectively because it was able to detect the less distinct features, like cracks and holes in the wall images and matched them to form the panorama.

### <15% Overlapping Mural Images:
This scenario had minimal overlap, making feature detection and matching significantly harder. Despite the limited overlapping region, the algorithm still produced a reasonable panorama.

## How to Run:

clone the repo into your local system and run the python notebook (Change the Image destinations in the data folder accordingly)
