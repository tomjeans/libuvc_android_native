cmake_minimum_required(VERSION 3.4.1)
project(libuvc_split)





# include folder
message("include folder")
include_directories(${CMAKE_SOURCE_DIR}/include)
include_directories(${CMAKE_SOURCE_DIR}/include/libjpeg)
include_directories(${CMAKE_SOURCE_DIR}/include/libusb)
include_directories(${CMAKE_SOURCE_DIR}/include/libuvc)

# so folder
message("so folder")
link_directories(
	${CMAKE_SOURCE_DIR}/libs
	
)



# if(CMAKE_SYSTEM_NAME STREQUAL "Android")
    # set(RGA_LIB ${RGA_PATH}/lib/Android/${CMAKE_ANDROID_ARCH_ABI}/librga.a)
# else()
    # set(RGA_LIB ${RGA_PATH}/lib/Linux//${LIB_ARCH}/librga.so)
# endif()

# include_directories(${RGA_PATH}/include)


set(share_lib ${CMAKE_SOURCE_DIR}/libs/libstdc++.so)

add_executable(libuvc_split ./example.cc
                             )



target_link_libraries(libuvc_split -pthread -ldl -llog -lz -static-libstdc++)

set(CMAKE_CXX_FLAGS
    "${CMAKE_CXX_FLAGS} -ffast-math -Ofast -Os -DNDEBUG -fno-exceptions -fomit-frame-pointer -fno-asynchronous-unwind-tables -fno-unwind-tables -Wl,-rpath,./"
)


target_link_libraries(libuvc_split  #${share_lib}
                                    jpeg-turbo212
                                    #unrooted_android
                                    usb1.0
                                    uvc
                                    #"${CMAKE_SOURCE_DIR}/libyuvlibs/libyuv_static.a"
                                    )

