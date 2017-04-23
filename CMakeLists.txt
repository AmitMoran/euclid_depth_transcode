cmake_minimum_required(VERSION 2.8.3)
project(euclid_depth_transcode)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  std_msgs 
  image_transport
  nodelet
  cv_bridge
)


catkin_package(
 CATKIN_DEPENDS
)

###########
## Build ##
###########

include_directories(
  ${catkin_INCLUDE_DIRS}
)
add_library(EuclidDepthTranscode src/euclid_depth_transcode.cpp)

target_link_libraries( EuclidDepthTranscode
						${catkin_LIBRARIES} 
						${roscpp_LIBRARIES} 

)

# Install nodelet library
install(TARGETS EuclidDepthTranscode
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

# Install header files
install(DIRECTORY src/
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)

# Install launch files
install(DIRECTORY launch/
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/launch
)

# Install xml files
install(FILES nodelet_plugins.xml
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}
)
