cmake_minimum_required(VERSION 3.0.2)
project(bt_tutorials)

add_compile_options(-std=c++17 -funroll-loops -Wall -Ofast)
set(CMAKE_BUILD_TYPE Release)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  behaviortree_cpp
)

catkin_package(
  INCLUDE_DIRS include 
  LIBRARIES #${PROJECT_NAME}
  CATKIN_DEPENDS roscpp  rospy behaviortree_cpp
)
include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)


# make node executable 
add_executable(${PROJECT_NAME}_node src/node.cpp
  )
add_dependencies(${PROJECT_NAME}_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(${PROJECT_NAME}_node
  ${catkin_LIBRARIES}
)

FILE(GLOB_RECURSE YamlFiles "config/*.yaml")
add_custom_target(yaml SOURCES ${YamlFiles})

FILE(GLOB_RECURSE LaunchFiles "launch/*.launch")
add_custom_target(launch SOURCES ${LaunchFiles})


