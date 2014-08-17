SET(OBJ runShowPic)

# set source files
SET(SRC_LIST runShowPic.cpp)

# set link libraries
IF(WIN32)
	IF(CMAKE_BUILD_TYPE MATCHES Debug)
		SET(LIBS opencv_highgui231d opencv_core231d)
	ELSE()
		SET(LIBS opencv_highgui231 opencv_core231)
	ENDIF()
ELSEIF(UNIX)
	IF(CMAKE_BUILD_TYPE MATCHES Debug)
		SET(LIBS opencv_highgui opencv_core)
	ELSE()
		SET(LIBS opencv_highgui opencv_core)
	ENDIF()
ENDIF()

ADD_EXECUTABLE(${OBJ} ${SRC_LIST})
TARGET_LINK_LIBRARIES(${OBJ} ${LIBS})
INSTALL(TARGETS ${OBJ} DESTINATION "bin") 

#test
ADD_TEST(NAME ShowPicRun COMMAND ${OBJ})
