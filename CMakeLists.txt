cmake_minimum_required(VERSION 2.8.3)
project(slam_karto)

find_package(catkin REQUIRED
  COMPONENTS
    cmake_modules
    message_filters
    nav_msgs
	std_srvs
    open_karto
    rosconsole
    roscpp
    sensor_msgs
    sparse_bundle_adjustment
    tf
    visualization_msgs
	dynamic_reconfigure
)
find_package(Eigen REQUIRED)
include_directories(${catkin_INCLUDE_DIRS} ${EIGEN_INCLUDE_DIRS})
add_definitions(${EIGEN_DEFINITIONS})

find_package(Boost REQUIRED COMPONENTS thread serialization)

#generate_dynamic_reconfigure_options(
#	cfg/SlamKartoReconfigure.cfg
#	)

catkin_package()

add_executable(slam_karto src/slam_karto.cpp src/spa_solver.cpp)
add_dependencies(slam_karto ${PROJECT_NAME}_gencfg)
target_link_libraries(slam_karto ${catkin_LIBRARIES})
target_link_libraries(slam_karto ${Boost_LIBRARIES})

install(TARGETS slam_karto
	RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
	)
