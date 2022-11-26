---
title: "[ROS] PCL To/From ROS msg 변환"

sidebar:
    nav: "dev"
---

<br/>


ROS 토픽 메시지를 PCL 형태로 변환하기 위해 아래 함수를 사용한다.


# 1. PCL to ROS msg

```cpp
#include <pcl_ros/point_cloud.h>

pcl::PointCloud<pcl::PointXYZ>::Ptr input_lidar (new pcl::PointCloud<pcl::PointXYZ>);
sensor_msgs::PointCloud2 lidar_msg;

pcl::toROSMsg(*input_lidar, lidar_msg);
lidar_msg.header.frame_id = frame_id;
```
<br/>


# 2. PCL from ROS msg 

```cpp
#include <pcl_ros/point_cloud.h>

pcl::PointCloud<pcl::PointXYZ>::Ptr input_lidar (new pcl::PointCloud<pcl::PointXYZ>);
sensor_msgs::PointCloud2 lidar_msg;

pcl::fromROSMsg(lidar_msg, *input_lidar);
```


<br/>


