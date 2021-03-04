cmake_minimum_required(VERSION 3.5)
project(humanoid_nav_msgs)

# Add flags to support compiling on windows, since ROS2 supports it
if(NOT WIN32)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -Wall -Wextra")
endif()

#Declare build dependencies
find_package(ament_cmake REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(actionlib_msgs REQUIRED)
find_package(rosidl_default_generators REQUIRED)

#Add message files
set(msg_files "msg/StepTarget.msg")

#Add service files
set(srv_files
    "srv/ClipFootstep.srv"
    "srv/PlanFootsteps.srv"
    "srv/PlanFootstepsBetweenFeet.srv"
    "srv/StepTargetService.srv")

#Add action files
set(action_files
    "action/ExecFootsteps.action")

#And now generate the messages
rosidl_generate_interfaces(${PROJECT_NAME}
    ${msg_files}
    ${srv_files}
    ${action_files}
    DEPENDENCIES geometry_msgs actionlib_msgs rosidl_default_generators)

# Generate catkin/pkg-config import information
ament_export_dependencies(rosidl_default_runtime)

ament_package()

