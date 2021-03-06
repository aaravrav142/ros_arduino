cmake_minimum_required(VERSION 2.8.3)
project(ros_arduino_imu)

find_package(catkin REQUIRED COMPONENTS roscpp sensor_msgs geometry_msgs ros_arduino_msgs)


find_package(Boost REQUIRED COMPONENTS system)


catkin_package(
   #INCLUDE_DIRS include
   #LIBRARIES
   CATKIN_DEPENDS roscpp sensor_msgs geometry_msgs ros_arduino_msgs
#  DEPENDS system_lib
)

###########
## Build ##
###########

include_directories(
  #include
  ${catkin_INCLUDE_DIRS}
  ${Boost_INCLUDE_DIRS}
)

link_directories(${catkin_LIBRARY_DIRS})

add_executable(arduino_magnometer_calibration src/arduino_magnometer_calibration.cpp)
add_dependencies(arduino_magnometer_calibration ros_arduino_msgs_generate_messages_cpp)
target_link_libraries(arduino_magnometer_calibration ${catkin_LIBRARIES})

add_executable(raw_imu_bridge src/raw_imu_bridge.cpp)
add_dependencies(raw_imu_bridge ros_arduino_msgs_generate_messages_cpp)
target_link_libraries(raw_imu_bridge ${catkin_LIBRARIES})

#############
## Install ##
#############
install(TARGETS raw_imu_bridge arduino_magnometer_calibration
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)


