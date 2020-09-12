## Research papers Challenge from thinkautonomous ai

A collection of research papers shared by Jeremy Cohen as part of his Weekly Research paper challenge.
A great newsletter to subscribe to, if you're interested in Self-driving vehicles, Perception, AI etc

https://www.thinkautonomous.ai/

## Paper 1
## 1. Real-Time Hybrid Multi-Sensor Fusion Framework for Perception in Autonomous Vehicles

### Link to paper
https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6833089/pdf/sensors-19-04357.pdf?__s=t7tzc5quajh4nil2qyo0

`Objective of Papers` 
  - Perceive the environment (Perception) - drivable space estimation and estimate
  states of objects by fusing data from Lidar, Camera and RADAR sensors. 

  - The presented algorithm is aimed at real time implementation on an embedded device while achieving 
  accuracies similar to benchmark models. Hybrid comes from the part that two parallel algorithms 

  a. Camera + Lidar for road segmentation, object detection
  b. Lidar + Radar for obstacle detection and state tracking

  are run and results are overlaid to get a better sense of environment.

`Obstacle detection using Lidar data`

  - Lidar gives Point cloud data (PCD) which is very accurate, dense information of the environment 
    (order of million points / sec). 

  a. Downsample - using Voxel grid
  b. Filter points outside ROI (Region of interest) - buildings etc
  c. Segmentation into road and obstacle points - using RANSAC, treating road points as inliers, 
     obstacle points as outliers. 
  d. Clustering - Obstacle points can be grouped based on heuristics such as euclidean distance into 
     groups, each point is assigned to a cluster, and cluster coordinate is the mean of points assigned to it.

`Role of Non linear Kalman filters`

  - KF is a state estimation algorithm
  - It can fuse data from different sensors (in this case Lidar and Radar) to get better estimates 
    of our state (2d position and velocities). 
  - KF is based on linear prediction and measurement models and Gaussian distributions. But real world 
    systems are non linear. 
  - In our case, Radar measurements are in polar coordinates while our state variables are in cartesian 
    space. 
  - So, we use linear approximation (jacobian of the measurement model, at our recent state estimates) 
    to update our state variables with corresponding measurements. 
  - There's also Unscented Kalman filter (UKF) and CKF which use sigma point methods (approximate the 
    distribution rather than the model itself) to generally give better results for highly non linear 
    cases but are relatively more expensive to compute.



## Paper 2
## 2. PointNet: Deep Learning on Point Sets for 3D Classification and Segmentation

- Proposes a new Deep Learning architecture that can directly work on Point cloud data and perform 
  Object classification and semantic segmentation tasks. 

- `Core idea` A symmetric function (max pooling layer) along with input and feature transformation
  techniques help classify and segment unordered point cloud data. 

- Performance compared againts benchmarks (MV-CNN, 3D CNN) etc, gives similar / better performance with 
  improvements in inference time, memory consumption. Has O(N) Linear space and time complexity. 

- Theoretical and empirical analysis of the proposed solution explained with intuition of the network 
  learnings via various visualisations - tSNE, Depth maps etc
