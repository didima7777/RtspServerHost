project (Tutorial)

 cmake_minimum_required(VERSION 2.8)
set(CMAKE_BUILD_TYPE Release)
set(CMAKE_CXX_FLAGS "-std=c++11")  ## standart
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3")        ## Optimize
set(CMAKE_EXE_LINKER_FLAGS "-s ")  ## Strip binary

#set(MYLIBS "-lgstapp-1.0 -lgstbase-1.0 -lgstreamer-1.0 -lgstsdp-1.0 -lgstrtsp-1.0 ")
#set(MYLIBS "-lgstreamer-0.10 -lgstapp-0.10 -lgstbase-0.10")  
set(MYLIBS "-lgstreamer-0.10 -lgstapp-0.10 -lgstbase-0.10 -lgstsdp-0.10 -lgstrtsp-0.10 ")  
set(MYLIBS "${MYLIBS} -lgobject-2.0 -lgmodule-2.0 -pthread -lgthread-2.0 -pthread -lglib-2.0 -lxml2")
set(MYLIBS "${MYLIBS} -pthread  -fpermissive")
#set(MYLIBS "${MYLIBS} -lopencv_core -lopencv_imgproc -lopencv_highgui -lopencv_flann -lopencv_features2d -lopencv_calib3d -lopencv_video")		


#include_directories(${SDKTARGETSYSROOT}/usr/include/gstreamer-1.0)
include_directories(/usr/include/gstreamer-0.10)
include_directories(/usr/include/glib-2.0)
include_directories(/usr/include/glib-2.0/glib)
include_directories(/usr/lib/glib-2.0/include)
include_directories(/usr/include/libxml2)
include_directories(/usr/include/gstreamer-1.0)
include_directories(/usr/lib/i386-linux-gnu/glib-2.0/include/)
include_directories(/usr/lib/glib-2.0/include)


include_directories(rtsp-server)

#set (APP_NAME  test_gst_tcp)
set (APP_NAME  test_gst_server)

file(GLOB_RECURSE GstSever_SOURCES "rtsp-server/*.c")
file(GLOB_RECURSE GstSever_HEADERS "rtsp-server/*.h")




set (HEADERS ${GstSever_SOURCES})

list(APPEND SRC  test-launch.c)
list(APPEND SRC  ${GstSever_SOURCES})
list(APPEND SRC  ${htpp_requast_SOURCES})
list(APPEND SRC  ${Counting_SOURCES})
list(APPEND SRC  ${CamConfig_SOURCES})
list(APPEND SRC  ${AutoExpo_SOURCES})
list(APPEND SRC  ${ReadConf_SOURCES})
list(APPEND SRC  ${GPIO_SOURCES})
list(APPEND SRC  ${GPRS_SOURCES})

MESSAGE( STATUS "CMAKE_BINARY_DIR:        " ${CMAKE_BINARY_DIR} )
MESSAGE( STATUS "CMAKE_INCLUDE_PATH: 	  " ${CMAKE_INCLUDE_PATH} )
MESSAGE( STATUS "CMAKE_LIBRARY_PATH: 	  " ${CMAKE_LIBRARY_PATH} )
MESSAGE( STATUS "LIBRARY_OUTPUT_PATH:     " ${LIBRARY_OUTPUT_PATH} )
MESSAGE( STATUS "LIBRARY_OUTPUT_PATH:     " ${MYLIBS} )
MESSAGE( STATUS "CMAKE_MODULE_PATH: " ${CMAKE_MODULE_PATH} )
MESSAGE( STATUS "CMAKE_C_COMPILER: " ${CMAKE_C_COMPILER} )
MESSAGE( STATUS "CMAKE_CXX_COMPILER: " ${CMAKE_CXX_COMPILER} )
MESSAGE( STATUS "CMAKE_CXX_FLAGS: " ${CMAKE_CXX_FLAGS} )
MESSAGE( STATUS "CMAKE_C_FLAGS: " ${CMAKE_C_FLAGS} )
MESSAGE( STATUS "BUILD_SHARED_LIBS: " ${BUILD_SHARED_LIBS} )
	
add_executable(${APP_NAME}  ${SRC} ${HEADERS})
target_link_libraries(${APP_NAME}  ${MYLIBS})

