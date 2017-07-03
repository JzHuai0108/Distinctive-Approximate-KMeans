cmake_minimum_required (VERSION 2.6)

SET(PROJECT_NAME DistinctApproximateKMeans)
project (${PROJECT_NAME})

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

# add our macro directory to cmake search path
if (EXISTS "${CMAKE_SOURCE_DIR}/cmake")
  set (CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_SOURCE_DIR}/cmake)
endif ()


find_package(Flann REQUIRED)
message("FLANN include dir " ${FLANN_INCLUDE_DIR} "  and lib dir " ${FLANN_LIBRARY_DIR})
message("FLANN library at " ${FLANN_LIBRARY})

include_directories (
  ${CMAKE_SOURCE_DIR}
  ${FLANN_INCLUDE_DIR}/flann
)

link_directories (
  ${FLANN_LIBRARY_DIR}
)

add_executable(${PROJECT_NAME} src/DAKMeans.cpp src/util.h)

target_link_libraries(${PROJECT_NAME} ${FLANN_LIBRARY} pthread)
