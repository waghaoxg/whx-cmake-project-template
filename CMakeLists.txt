CMAKE_MINIMUM_REQUIRED(VERSION 2.6)

PROJECT(testCMake CXX)

# for testing
#ENABLE_TESTING()

# use a config.h for macros. Optinal 
CONFIGURE_FILE("${PROJECT_SOURCE_DIR}/config.h.in" "${PROJECT_BINARY_DIR}/config.h")

# set macros in config.h
OPTION(PRINT_INFO "print info" OFF)

# set build type
SET(CMAKE_BUILD_TYPE Debug CACHE STRING "build type")

# set binary output path
SET(EXECUTABLE_OUTPUT_PATH "${PROJECT_BINARY_DIR}/bin")
SET(LIBRARY_OUTPUT_PATH "${PROJECT_BINARY_DIR}/bin")

# set install path prefix
SET(CMAKE_INSTALL_PREFIX "${PROJECT_BINARY_DIR}/INSTALL" CACHE PATH "install prefix" FORCE)

# set include_directory  and link_directory
IF(WIN32)
	#custom compile flags
	#SET(CMAKE_CXX_FLAGS "")
	SET(INCLUDE_DIR_LIST "d:/Program Files/OpenCV2.3/build/include/opencv2/" "d:/Program Files/OpenCV2.3/build/include/opencv/" "d:/Program Files/OpenCV2.3/build/include/" ${PROJECT_BINARY_DIR})
	SET(LIB_DIR_LIST "d:/Program Files/OpenCV2.3/build/x86/vc10/lib/")
ELSEIF(UNIX)
	#custom compile flags
	#SET(CMAKE_CXX_FLAGS "")
	SET(INCLUDE_DIR_LIST  "/usr/local/include/opencv" "/usr/local/include/opencv2" ${PROJECT_BINARY_DIR})
	SET(LIB_DIR_LIST "/usr/local/lib/")
ENDIF()

INCLUDE_DIRECTORIES(${INCLUDE_DIR_LIST})
LINK_DIRECTORIES(${LIB_DIR_LIST})

ADD_SUBDIRECTORY(src)

INSTALL(FILES ${PROJECT_BINARY_DIR}/config.h DESTINATION "include")
