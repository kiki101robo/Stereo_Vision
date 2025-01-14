# Stereo Vision and Disparity Mapping Pipeline

## Overview
This README details the methodology for a stereo vision pipeline designed to compute disparity maps and depth maps from a pair of stereo images. This process is essential for understanding depth information from stereo camera setups.

## Pipeline Steps

### 1. Data Reading
- **Function:** `read_data`
- **Input:** Filename, path to data
- **Output:** Stereo images, calibration matrices (intrinsic), and other stereo parameters.
- **Description:** Loads the stereo images and extracts calibration data, including camera intrinsic matrices and baseline distances.

### 2. Feature Detection and Matching
- **Function:** `get_points`
- **Input:** Two images
- **Output:** Coordinates of matched feature points in both images
- **Description:** Applies SIFT to detect keypoints and compute descriptors in both images. Matches keypoints using BFMatcher, applying a Lowe's ratio test to filter out weak matches.

### 3. Stereo Calibration and Rectification
- **Function:** `stereoCalibrate` and `stereoRectify`
- **Input:** Matched feature points, intrinsic camera parameters
- **Output:** Rotation and translation between cameras, rectification transforms, and projection matrices.
- **Description:** Estimates the rotation and translation between the stereo cameras using matched points and calibrates the stereo setup for rectification.

### 4. Disparity Computation
- **Function:** `compute_and_save_disparity_images`
- **Input:** Rectified images, disparity settings (min disparity, number of disparities, block size)
- **Output:** Disparity map and depth map
- **Description:** Computes the disparity map using StereoSGBM, then calculates the depth map from the disparity using the formula involving focal length and baseline.

## Usage
To run the pipeline, execute the script with the required image data and calibration data properly set up in your project directory.

## Data Format
The data folder for each scene should include:
- Stereo images named appropriately (e.g., `im0.png` and `im1.png`).
- A `calib.txt` file containing stereo calibration parameters.

Adjust the paths in the script to match your directory structure.

## Output
The script generates and saves disparity maps and depth maps as visual outputs, providing both heat map and grayscale visualizations.

## Libraries Required
- OpenCV
- NumPy
- Matplotlib

Ensure these libraries are installed in your Python environment to execute the script without issues.

## Conclusion
This pipeline facilitates the practical application of stereo vision concepts to derive depth information from stereo image pairs. It can be adapted and expanded based on specific project requirements or used as a teaching tool for understanding stereo vision fundamentals.
