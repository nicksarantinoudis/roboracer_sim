cmake_minimum_required(VERSION 3.5)

project(roboracer_bringup)

find_package(ament_cmake REQUIRED)
find_package(roboracer_description REQUIRED)
find_package(roboracer_gz REQUIRED)

# Install project launch files
install(
  DIRECTORY
    launch/
  DESTINATION share/${PROJECT_NAME}/launch
)

# Install project configuration files
install(
  DIRECTORY
    config/
  DESTINATION share/${PROJECT_NAME}/config
)

# Install project parameter files
install(
  DIRECTORY
    params/
  DESTINATION share/${PROJECT_NAME}/params
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
