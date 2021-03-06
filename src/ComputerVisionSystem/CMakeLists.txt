cmake_minimum_required(VERSION 3.10)
project(ComputerVisionSystem)

set(CMAKE_CXX_STANDARD 17)

if(WIN32)
	set(OpenCV_DIR "D:/Common Files/OpenCV/build/x64/vc14/lib")
endif()

find_package(OpenCV REQUIRED)

add_library(ArucoMarker STATIC ArucoMarker/ArucoMarker.cpp)
target_link_libraries(ArucoMarker ${OpenCV_LIBS} )
if(CMAKE_COMPILER_IS_GNUCXX)
	target_link_libraries(ArucoMarker stdc++fs)
endif()

add_library(CamCalibWI STATIC CamCalibWI/CamCalibWI.cpp CamCalibWI/CameraCalibration/CameraCalibration.cpp)
target_link_libraries(CamCalibWI ${OpenCV_LIBS})

add_library(ComputerVisionSystem STATIC CVS.cpp)
target_link_libraries(ComputerVisionSystem ${OpenCV_LIBS} CamCalibWI ArucoMarker)
