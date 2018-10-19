cmake_minimum_required(VERSION 2.8.3)
project(image_proc_tegra)

find_package(catkin REQUIRED COMPONENTS
  cv_bridge
  image_transport
  image_geometry
  sensor_msgs
  std_msgs
  roscpp
  nodelet  
)

find_package(OpenCV 
PATHS /usr/local
NO_DEFAULT_PATH
)

catkin_package(
  CATKIN_DEPENDS image_geometry roscpp sensor_msgs
  DEPENDS OpenCV

  LIBRARIES ${PROJECT_NAME}
)

add_compile_options(-std=c++11)

include_directories(SYSTEM ${catkin_INCLUDE_DIRS} ${OpenCV_INCLUDE_DIRS})


add_library(${PROJECT_NAME}     src/nodelets/rectify.cpp )
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES} ${OpenCV_LIBRARIES})

add_executable(image_proc_tegra_exe src/image_proc_tegra.cpp)

target_link_libraries(image_proc_tegra_exe
   ${PROJECT_NAME}
   ${catkin_LIBRARIES}
)
