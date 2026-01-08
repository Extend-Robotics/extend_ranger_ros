cmake_minimum_required(VERSION 2.8.3)

project(ranger_mini_v2)

find_package(catkin REQUIRED)

catkin_package()

find_package(roslaunch)


add_custom_target( unZip ALL)
add_custom_command(TARGET unZip PRE_BUILD
   COMMAND ${CMAKE_COMMAND} -E tar xzf ${CMAKE_CURRENT_SOURCE_DIR}/meshes/ranger_base.tar.gz
WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/meshes
DEPENDS ${CMAKE_CURRENT_SOURCE_DIR}/meshes/ranger_base.tar.gz
COMMENT "Unpacking ranger_base.tar.gz"
VERBATIM)

foreach(dir config launch meshes urdf)
	install(DIRECTORY ${dir}/
		DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/${dir})
endforeach(dir)
