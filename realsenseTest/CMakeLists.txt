cmake_minimum_required(VERSION 2.8)
project(realsenseTest)

#aux_source_directory(. SRC_LIST)
add_executable(${PROJECT_NAME} 
# main.cpp
# rs_color.cpp
# rs_cv.cpp
# rs_wd.cpp
# rs_orbslam3.cpp
rs_mono.cpp
)
 
set(CMAKE_CXX_FLAGS "-std=c++11")
#寻找opencv库
find_package(OpenCV REQUIRED)
find_package(Eigen3 REQUIRED)
find_package(Pangolin REQUIRED)
#message(STATUS ${OpenCV_INCLUDE_DIRS})
#添加头文件

set(ORB_SLAM3 /home/flj/ORB_SLAM3)
include_directories(
include    
${OpenCV_INCLUDE_DIRS}
${EIGEN3_INCLUDE_DIR}
${Pangolin_INCLUDE_DIRS}
${ORB_SLAM3}/include
${ORB_SLAM3}/include/CameraModels
${ORB_SLAM3}/Thirdparty/Sophus
${ORB_SLAM3}/Thirdparty/g2o
${ORB_SLAM3}
)


#链接Opencv库
target_link_libraries(realsenseTest 
${OpenCV_LIBS} 
${EIGEN3_LIBS}
${Pangolin_LIBRARIES}
${ORB_SLAM3}/Thirdparty/DBoW2/lib/libDBoW2.so
${ORB_SLAM3}/Thirdparty/g2o/lib/libg2o.so
${ORB_SLAM3}/lib/libORB_SLAM3.so
-lboost_serialization
-lcrypto
)
#添加后可进行调试
set( CMAKE_BUILD_TYPE Debug )
set(DEPENDENCIES realsense2 )
target_link_libraries(realsenseTest 
${DEPENDENCIES})