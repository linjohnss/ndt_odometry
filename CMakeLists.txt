cmake_minimum_required(VERSION 3.0.2)
project(ndt_odometry)

## Compile as C++11, supported in ROS Kinetic and newer
# add_compile_options(-std=c++11)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  ndt_omp
  roscpp
  rospy
  std_msgs
  sensor_msgs
  pcl_ros
  pcl_conversions
)

# add_compile_options(-std=c++11)
find_package(PCL 1.7 REQUIRED)
include_directories(${PCL_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})

message(STATUS "PCL_INCLUDE_DIRS:" ${PCL_INCLUDE_DIRS})
message(STATUS "PCL_LIBRARY_DIRS:" ${PCL_LIBRARY_DIRS})
message(STATUS "PCL_DEFINITIONS:" ${PCL_DEFINITIONS})

find_package(OpenMP)
if (OPENMP_FOUND)
    set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
endif()

###################################
## catkin specific configuration ##
###################################
catkin_package(
  CATKIN_DEPENDS ndt_omp
)

###########
## Build ##
###########
include_directories(
  ${catkin_INCLUDE_DIRS}
)

# add_executable(omp_visualize
#   src/omp_visualize.cpp
# )
# add_dependencies(omp_visualize
#   ndt_omp
# )
# target_link_libraries(omp_visualize
#   ${catkin_LIBRARIES}
#   ${PCL_LIBRARIES}
#   ndt_omp
# )

# add_executable(omp_optimizer
#   src/omp_optimizer.cpp
# )
# add_dependencies(omp_optimizer
#   ndt_omp
# )
# target_link_libraries(omp_optimizer
#   ${catkin_LIBRARIES}
#   ${PCL_LIBRARIES}
#   ndt_omp
# )

add_executable(ndt_odometry
  src/ndt_odometry.cpp
)
add_dependencies(ndt_odometry
  ndt_omp
)
target_link_libraries(ndt_odometry
  ${catkin_LIBRARIES}
  ${PCL_LIBRARIES}
  ndt_omp
)

add_executable(ndt_slam
  src/ndt_slam.cpp
)
add_dependencies(ndt_slam
  ndt_omp
)
target_link_libraries(ndt_slam
  ${catkin_LIBRARIES}
  ${PCL_LIBRARIES}
  ndt_omp
)



