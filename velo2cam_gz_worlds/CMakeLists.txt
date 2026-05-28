cmake_minimum_required(VERSION 3.8)
project(velo2cam_gz_worlds)

find_package(ament_cmake REQUIRED)

# Install models and worlds so they are accessible via GZ_SIM_RESOURCE_PATH
install(
  DIRECTORY models worlds
  DESTINATION share/${PROJECT_NAME}
)

ament_environment_hooks(
  "${CMAKE_CURRENT_SOURCE_DIR}/env-hooks/${PROJECT_NAME}.dsv.in"
)

ament_package()
