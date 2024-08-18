
# FlySocialer

**FlySocialer** is a program designed to analyze the social interactions of individual fruit flies. The program is executed using MATLAB R2022a.

## Getting Started

1. Unzip the `FlySocialer.zip` file.
2. Move the `Matlab analysis code` folder to the `C:\` drive on your computer. This folder contains the following scripts:
   - `autoMarked`
   - `circle plot`
   - `Fake`
   - `interaction matrix`
   - `noiseProcess`
   - `order calculation`
   - `sand`
   - `trajectory`
   - `backAlternate`
   - `head_orientation_find_body_beta2`
   - `onlyIntractBatchContent`
   - `onlyIntractMain`
   - `onlyIntractMainBatch`
   - `task8manager_1_1`
   - `tasmManager_Special`

## Prerequisites

To collect behavioral data, we recorded images at 20 FPS during experiments. This program only analyzes a series of images, not video files. If you have video files, please convert them into an image sequence first.

**Important Notes:**
- **Do not use spaces in the image file names.** For example, use `_0718_1_CantonS_CantonS` instead of `0718 1 CantonS CantonS`. We will use this file name for the demonstration.
- **Recommended file structure:** `C:\20230718\_0718_1_CantonS_0_CantonS\images.jpg`
- Recommended images used should be 1024x2048 pixels at 96 dpi.
- **Avoid shadows of the fruit flies during image recording.**

## Data Analysis Procedure

### 1. Create Background

- **Location of the script:** `Matlab analysis code\circle plot\backCreate.m`
- **Key script variables:**
  ```matlab
  imageFolder = 'location of the image folder';
  savePath = 'location where you want to save the background';
  ```
- After inputting the information above, run the script to create the clear background.

### 2. Define the Region of Interest (ROI)

#### 2.1. Mark the ROI

- **Location of the script:** `Matlab analysis code\circle plot\circleDemo.m`
- **Key script variables:**
  ```matlab
  a = imread('location of the image folder\Image.jpg'); 
  % Example: a = imread('C:\20230718\_0718_1_CantonS_0_CantonS\images0.jpg');

  circles(X, Y, r, 'edgecolor', [.5 .2 .9], 'edgecolor', 'y', 'facecolor', 'none');
  ```
- Run the script. It will display a yellow circle as a temporary ROI marker. Adjust the `X`, `Y`, and `r` values to fit your desired ROI.

#### 2.2. Save the ROI

- **Location of the script:** `Matlab analysis code\circle plot\create_interest_circle.m`
- **Key script variables:**
  ```matlab
  a = imread('location of the image folder\Image.jpg'); 
  % Example: a = imread('C:\20230718\_0718_1_CantonS_0_CantonS\images0.jpg');

  if norm([p q] - [Y X]) < r
  save('location where you want to save the ROI\back_0718_1_CantonS_0_CantonS_interest_circle_1.mat', 'interest_circle');
  % Example: save('C:\20230718\back_0718_1_CantonS_0_CantonS_interest_circle_1.mat', 'interest_circle');
  ```

### 3. Set the Start Point of Each Fruit Fly

- **Location of the script:** `Matlab analysis code\circle plot\getStartPoint_original.m`
- **Key script variables:**
  ```matlab
  save_dir = 'location of the experiment folder';
  % Example: save_dir = 'C:\20230718';

  back = imread('location of the image folder\Image0.jpg');
  % Example: back = imread('C:\20230718\_0718_1_CantonS_0_CantonS\Image0.jpg');

  save([save_dir '\point1_file_name.mat'], 'previous_centroid2');
  % Example: save([save_dir '\point1_0718_1_CantonS_0_CantonS.mat'], 'previous_centroid2');
  ```

### 4. Check for Damaged Images

- **Location of the script:** `Matlab analysis code\noiseProcess\VideoPlusBrokenCheckMainMulti.m`
- **Key script variables:**
  ```matlab
  FramesPath = 'location of the experiment folder';
  % Example: FramesPath = 'C:\20230718';

  videoName = 'location of the image folder';
  % Example: videoName = '_0718_1_CantonS_0_CantonS';

  flyNum = INPUT_NUMBER_OF_FLIES in the corresponding arena;
  % Example for 10 fruit fly in a ROI:
  flyNum = 10;

  fps = FPS value;
  recordingFrame = minute * 60 * fps;
  intervalFrame = minute * 60 * fps;
  recordingFrame = minute * 60 * fps;
  % Example for 20 fps, 10-minute experiment:
  fps = 20;
  recordingFrame = 10 * 60 * fps;
  intervalFrame = 10 * 60 * fps;
  ```
- Run the script to identify any damaged images that cannot be analyzed.

### 5. Analyze Data

- **Location of the script:** `Matlab analysis code\task8manager_1_1.m`
- **Key script variables:**
  ```matlab
  cd 'location of the sand file';
  % Example: cd 'C:\Matlab analysis code\sand';

  MainPathWay = 'location of the experiment folder';
  % Example: MainPathWay = 'C:\20230718';

  SubPathWay = 'name of the image folder';
  % Example: SubPathWay = '_0718_1_CantonS_0_CantonS';

  ResultNum = 'interest_circle_number';
  % Example: ResultNum = '1';

  recordDuration = recorded duration (in minutes);
  % Example: for a 10-minute recording:
  recordDuration = 10;
  ```

After running `task8manager_1_1.m`, the locomotion and social interaction data will be saved in the experiment folder, in a subfolder named: `_0718_1_CantonS_0_CantonS_result1`.
