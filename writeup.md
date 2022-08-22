# Writeup: Track 3D-Objects Over Time

Please use this starter template to answer the following questions:

#### 1. Write a short recap of the four tracking steps and what you implemented there (filter, track management, association, camera fusion). Which results did you achieve? Which part of the project was most difficult for you to complete, and why?
## STEP - 1 - Compute Lidar Point-Cloud from Range Image
Range and intensity channels are extrected from lidar data, which is stored as range image in the Waymo Open Dataset. After that, floating-point data converted to an 8-bit integer value range. Finally, range and intensity image visualized with OpenCV.

![range_image](./img/range_image_screenshot_22.08.2022.png)


In second part of step-1, Open3D library used to display lidar point-clodu data in a 3d viewer.

![f5](./img/f5.PNG)


## STEP - 2 - Create Birds-Eye View from Lidar PCL
Created a birds-eye view (BEV) perspective from a lidar point-cloud. While doing this, (x,y) coordinates which is in sensor space, converted to BEV coordinate space.

![bev](./img/bev.PNG)

Also, "intensity" channel of the BEV map filled with data from the point-cloud. In order to do so, all points with the same (x,y)-coordinates identified within the BEV map and then assigned the intensity value of the top-most lidar point to the respective BEV pixel. After that, intensity image normalized using percentiles in order to ake sure that the influence of outlier values (very bright and very dark regions) is sufficiently mitigated and objects of interest (e.g. vehicles) are clearly separated from the background.

![intensity](./img/img_intensity_screenshot_22.08.2022.png)

On final part of this step, "height" channel of the BEV map filled with data from the point-cloud. While doing this, point-cloud sorted and pruned, additionally, the height in each BEV map pixel is normalized by the difference between max. and min.

![height](./img/img_height.PNG)


## STEP - 3 - Model-based Object Detection in BEV Image
In this step, the repo [Super Fast and Accurate 3D Object Detection based on 3D LiDAR Point Clouds](https://github.com/maudzung/SFA3D) used to extract model config parameters. With this paramters, fpn_resnet model is instantiated. After that, decoded the model output and post-processing performed. Finally, bounding boxes of detections converted using the limits in the configs structure.

As the model input is a three-channel BEV map, the detected objects will be returned with coordinates and properties in the BEV coordinate space. Thus, before the detections can move along in the processing pipeline, they need to be converted into metric coordinates in vehicle space. This task is about performing this conversion.

![bounding-boxes](./img/3d-bounding-boxes.png)


## STEP - 4 - Performance Evaluation for Object Detection




#### 2. Do you see any benefits in camera-lidar fusion compared to lidar-only tracking (in theory and in your concrete results)? 


#### 3. Which challenges will a sensor fusion system face in real-life scenarios? Did you see any of these challenges in the project?


#### 4. Can you think of ways to improve your tracking results in the future?

