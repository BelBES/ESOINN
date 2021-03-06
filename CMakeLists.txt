project(ESOINN)
cmake_minimum_required(VERSION 2.8)
aux_source_directory(. SRC_LIST)

#Boost
find_package(Boost COMPONENTS ${BOOST_COMPONENTS} system filesystem serialization program_options graph REQUIRED)
if(NOT Boost_FOUND)
    message(SEND_ERROR "Failed to find Boost")
    return()
else()
    include_directories(${Boost_INCLUDE_DIRS})
    link_directories(${Boost_LIBRARY_DIRS})
    add_definitions(-DBOOST_ALL_NO_LIB)
    add_definitions(-DBOOST_ALL_DYN_LINK)
endif()

#OpenCV
find_package(OpenCV REQUIRED)
if(NOT OpenCV_FOUND)
    message(SEND_ERROR "Faild to find Opencv")
    return()
else()
    include_directories(${Opencv_INCLUDE_DIR})
endif()

#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -O3 -fprofile-arcs -ftest-coverage")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
#add_definitions(-fprofile-arcs)
#add_definitions(-ftest-coverage)

add_executable(${PROJECT_NAME} ${SRC_LIST})
target_link_libraries(${PROJECT_NAME} ${OpenCV_LIBS} ${Boost_LIBRARIES})
