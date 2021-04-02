cmake_minimum_required(VERSION 3.10.2)
project(lidar_localization)

SET(CMAKE_BUILD_TYPE "Release")
SET(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")
add_compile_options(-std=c++14)
add_definitions(-std=c++14)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  geometry_msgs
  sensor_msgs
  nav_msgs
  pcl_ros
  tf
  eigen_conversions
  message_generation 
  std_srvs
)

## Generate messages in the 'msg' folder
add_message_files(
    FILES
    # IMU:
    IMUGNSSMeasurement.msg
    # lidar:
    LidarMeasurement.msg
    # ESKF covariance monitor:
    ESKFStd.msg
    # EKF covariance monitor:
    EKFStd.msg
    # synced GNSS-odo measurement:
    PosVel.msg
    # synced GNSS-odo-mag measurement:
    PosVelMag.msg
)

add_service_files(
   FILES
   saveScanContext.srv
   saveMap.srv
   optimizeMap.srv
   saveOdometry.srv
)

generate_messages(
   DEPENDENCIES
   std_msgs
   geometry_msgs
   sensor_msgs
   nav_msgs
)

