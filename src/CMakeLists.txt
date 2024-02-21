IF (CMAKE_BUILD_TYPE MATCHES "Debug")
    MESSAGE("Debug -g -O0 -rdynamic")
    SET(CMAKE_CXX_FLAGS_DEBUG "-g -O0")# -g show more info for debug
ELSE ()
    MESSAGE("Release -O3 -s")
    SET(CMAKE_CXX_FLAGS_RELEASE "-O3 -s -rpath")#-Wall show all the warning
ENDIF ()

FILE(GLOB_RECURSE CLIENT_SRCs "*.c*" "*.h*")

SET(LIB_DIRECTORY ${PROJECT_SOURCE_DIR}/lib/${PLATFORM})
LINK_DIRECTORIES(
        ${LIB_DIRECTORY}
)

LINK_LIBRARIES(
        libffi.so
        libz.so
        libpcre.so
        libgmodule-2.0.so
        librt.so
        libbluetooth.so
        libglib-2.0.so
        libsbc.so
        libjson-c.so
        libgio-2.0.so
        libgobject-2.0.so
        libasound.so
        libbtmg.so
        libresolv.so
)

ADD_EXECUTABLE(${PROJECT_NAME} ${CLIENT_SRCs})
TARGET_LINK_LIBRARIES(${PROJECT_NAME} PUBLIC pthread dl m shared-mainloop bluetooth-internal)