cmake_minimum_required(VERSION 3.16)
project(custos_hardware_airframes)

find_package(ament_cmake REQUIRED)

install(DIRECTORY airframes params
  DESTINATION share/${PROJECT_NAME}
  OPTIONAL
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
