cmake_minimum_required(VERSION 2.8.3)
project(multi_map_server)

find_package(catkin REQUIRED
        COMPONENTS
            roscpp
            map_server
            nav_msgs
            std_msgs
            roslib
        )

find_package(PkgConfig)
pkg_check_modules(NEW_YAMLCPP yaml-cpp>=0.5)

if(NEW_YAMLCPP_FOUND)
add_definitions(-DHAVE_NEW_YAMLCPP)
endif(NEW_YAMLCPP_FOUND)


catkin_package(
    LIBRARIES ${PROJECT_NAME}
    CATKIN_DEPENDS
        roscpp
        map_server
        roslib
        std_msgs
        nav_msgs
)

include_directories(include ${catkin_INCLUDE_DIRS})

add_executable(multi_map_server src/main.cpp)
target_link_libraries(multi_map_server
    ${catkin_LIBRARIES}
    yaml-cpp
)


## Install executables and/or libraries
install(TARGETS multi_map_server
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION})
