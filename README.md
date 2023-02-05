
# Camera LiDAR Fusion

This Repository would contain the code for Early Fusion with KITTI Dataset. 

One type of early fusion where the LiDAR point clouds are projected on the image.
 - KITTI Dataset comes with the Calibrated Matrix Transformations for the LiDAR and the stereo cameras used.
 - Development to use my custom docker container that I built here. 


### Repo's organization (Subject to change)

```
camera-lidar-fusion
|
|___data
|   |
|   |___lidar_data
|   |___images
|   |___calibration_file.txt 
|
|___object_detector
|   |___image_preprocessor
|   |___detector
|
|___project_pcd_image
|   |___point_cloud_preprocessor
|   |___project_pcd_on_image
|
|___src
|   |___fuse_pcd_detections
|
|___utils
    |___lidar_camera_transform
    |___convert_pcd_file_format

```

### Steps in Early Fusion of LiDAR PCD on Image

- Visualizing the point cloud
- Visualizing the Image
- Performing object detection on the image 
- Projecting LiDAR point cloud on the image (this is essentially performing transform from LiDAR to camera) in other words, visualizing a 3D-point of the LiDAR through the camera image frame.  
    - Ensuring that the point clouds of only certain depth ranges and that fall with-in the image coordinates are projected and drawn 
- Now, removing all the other point cloud points projected which are not part of the detected bounding boxes should be done.
- The indices of the original pcd points must be  stored for the depth/distance estimation at later stages after fusion. 
    - Shrinking - Virtually reduce the Detected bounding boxes to get the most accurate projected pcd points for object distance estimation
- Perform Depth(object distance) estimation of the projected point cloud points that are inside the shrinked bounding box dimensions 
    - Further outlier removal of the projected pcd points can be made using the mean and the three sigma bounds of the distances of the pcd points through the selected indices. 
- Draw the bounding box, the projected pcd points and the distance on the images. 


### Next Steps of work:
- Object Oriented Design of the above listed functionalities. 
- Implementation of the fusion.
