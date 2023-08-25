cmake_minimum_required(VERSION 3.9)
project(clipper)

find_package(ament_cmake REQUIRED)

include_directories(
  inc
)

add_library(${PROJECT_NAME}
  src/clipper.cpp
)
target_include_directories(${PROJECT_NAME}
  PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/inc>
    $<INSTALL_INTERFACE:include>)

ament_export_include_directories(include)
ament_export_libraries(${PROJECT_NAME})
ament_export_targets(
  export_${PROJECT_NAME}
)

install(DIRECTORY inc/${PROJECT_NAME}/
   DESTINATION include/${PROJECT_NAME}/
   FILES_MATCHING PATTERN "*.h*"
)

install(TARGETS ${PROJECT_NAME}
  EXPORT export_${PROJECT_NAME}
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
)

ament_package()
