cmake_minimum_required(VERSION 2.8.3)
project(driver_imu_fsm)

set(CMAKE_MODULE_PATH "${CMAKE_MODULE_PATH}" "${CMAKE_CURRENT_SOURCE_DIR}/CMake")

set(LIBUSB1_FIND_REQUIRED ON)
find_package(libusb-1.0)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  sensor_msgs
)

catkin_package()

###########
## Build ##
###########

include_directories(
  ${catkin_INCLUDE_DIRS}
  ${LIBUSB_1_INCLUDE_DIRS}
  ${CMAKE_CURRENT_SOURCE_DIR}/lib/include
  ${CMAKE_CURRENT_SOURCE_DIR}/lib/include/freespace
)

add_executable(${PROJECT_NAME}_node src/driver_imu_fsm.cpp)

target_link_libraries(${PROJECT_NAME}_node
  ${catkin_LIBRARIES}
  ${CMAKE_CURRENT_SOURCE_DIR}/lib/libfreespace.a
  ${LIBUSB_1_LIBRARIES}
)

#############
## Install ##
#############

## Mark executables and/or libraries for installation
install(TARGETS ${PROJECT_NAME}_node
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)
