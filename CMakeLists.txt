if("$ENV{ROS_VERSION}" STREQUAL "2")
  cmake_minimum_required(VERSION 3.8)
	set(DETECTED_ROS2 TRUE)
else()
  cmake_minimum_required(VERSION 2.8.3)
	set(DETECTED_ROS1 TRUE)
  set(CMAKE_AUTOMOC ON)
  set(CMAKE_AUTOUIC ON)

  SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}  -std=c++11")

  add_definitions(-std=c++11)
endif()

project(gtec_msgs)

if(DETECTED_ROS1)
  ## Find catkin macros and libraries
  ## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
  ## is used, also find other catkin packages
  find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  geometry_msgs
  message_generation
  )

  ## Generate messages in the 'msg' folder
  add_message_files(
    DIRECTORY
    msg-ros1
    FILES
    GenericRanging.msg
    Ranging.msg
    UWBRanging.msg
    DWRanging.msg
    PozyxRanging.msg
    RangingDiff.msg
    PozyxRangingWithCir.msg
    ESP32S2FTMFrame.msg
    ESP32S2FTMRanging.msg
    ESP32S2FTMRangingExtra.msg
    RadarCube.msg
    RadarRangeAzimuth.msg
    RadarRangeDoppler.msg
    RadarFusedPointStamped.msg
    DoorCounterEvent.msg
    ZoneOccupancy.msg
  )

  ## Generate added messages and services with any dependencies listed here
  generate_messages(
  DEPENDENCIES
  std_msgs
  geometry_msgs
  )

  catkin_package(
  )
endif()

if(DETECTED_ROS2)
  if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
    add_compile_options(-Wall -Wextra -Wpedantic)
  endif()

  # find dependencies
  find_package(ament_cmake REQUIRED)
  find_package(geometry_msgs REQUIRED)
  find_package(rosidl_default_generators REQUIRED)
  find_package(geometry_msgs)
  find_package(std_msgs)
  # uncomment the following section in order to fill in
  # further dependencies manually.
  # find_package(<dependency> REQUIRED)

  rosidl_generate_interfaces(${PROJECT_NAME}
    "msg-ros2/GenericRanging.msg"
    "msg-ros2/Ranging.msg"
    "msg-ros2/UWBRanging.msg"
    "msg-ros2/DWRanging.msg"
    "msg-ros2/PozyxRanging.msg"
    "msg-ros2/RangingDiff.msg"
    "msg-ros2/PozyxRangingWithCir.msg"
    "msg-ros2/ESP32S2FTMFrame.msg"
    "msg-ros2/ESP32S2FTMRanging.msg"
    "msg-ros2/ESP32S2FTMRangingExtra.msg"
    "msg-ros2/RadarCube.msg"
    "msg-ros2/RadarRangeAzimuth.msg"
    "msg-ros2/RadarRangeDoppler.msg"
    "msg-ros2/RadarFusedPointStamped.msg"
    "msg-ros2/DoorCounterEvent.msg"
    "msg-ros2/ZoneOccupancy.msg"
    DEPENDENCIES geometry_msgs std_msgs # Add packages that above messages depend on, in this case geometry_msgs for Sphere.msg
  )

  if(BUILD_TESTING)
    find_package(ament_lint_auto REQUIRED)
    # the following line skips the linter which checks for copyrights
    # comment the line when a copyright and license is added to all source files
    set(ament_cmake_copyright_FOUND TRUE)
    # the following line skips cpplint (only works in a git repo)
    # comment the line when this package is in a git repo and when
    # a copyright and license is added to all source files
    set(ament_cmake_cpplint_FOUND TRUE)
    ament_lint_auto_find_test_dependencies()
  endif()

  ament_package()
endif()