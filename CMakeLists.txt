cmake_minimum_required(VERSION 2.8.3)
project(dualarm_mobile_bringup)

find_package(catkin REQUIRED COMPONENTS
  geometry_msgs
  nav_msgs
  roscpp
  std_msgs
  nodelet
  tf
  
)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES dualarm_mobile_bringup 
  CATKIN_DEPENDS 
    geometry_msgs 
    nav_msgs 
    roscpp 
    std_msgs
    vehicle_control
    
)


include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${CATKIN_DEVEL_PREFIX}/${CATKIN_GLOBAL_INCLUDE_DESTINATION}
)

add_executable(bringup_publisher src/bringup_publisher.cpp)
add_dependencies(bringup_publisher vehicle_control_generate_messages_cpp ${catkin_EXPORTED_TARGETS})
target_link_libraries(bringup_publisher ${catkin_LIBRARIES})

add_executable(odom_publisher src/odom_publisher.cpp)
target_link_libraries(odom_publisher ${catkin_LIBRARIES})
