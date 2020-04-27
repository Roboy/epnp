cmake_minimum_required(VERSION 3.5)
project(epnp)

if(NOT CMAKE_CXX_STANDARD)
    set(CMAKE_CXX_STANDARD 14)
endif()

find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)

find_package(OpenCV REQUIRED)


###########
## Build ##
###########

include_directories(
  include

)

## Declare a cpp library
add_library(${PROJECT_NAME}
  src/epnp.cpp
)
target_link_libraries(${PROJECT_NAME} ${OpenCV_LIBRARIES})
ament_target_dependencies(${PROJECT_NAME} rclcpp)

        ## Declare a cpp executable
add_executable(epnp_example src/main.cpp)
target_link_libraries(epnp_example
  ${PROJECT_NAME}
  ${OpenCV_LIBRARIES}
)
ament_target_dependencies(epnp_example rclcpp)


#############
## Install ##
#############

## Mark cpp header files for installation
install(DIRECTORY include/${PROJECT_NAME}/
        DESTINATION include/${PROJECT_NAME}
        FILES_MATCHING PATTERN "*.h"
)

ament_export_include_directories(include)
ament_export_libraries( ${PROJECT_NAME})
ament_package(
#        DEPENDS opencv
)
