#specify the minimum version of cmake
CMAKE_MINIMUM_REQUIRED(VERSION 2.8.8 FATAL_ERROR)

#set PROJECT_NAME
PROJECT(bluetoothclient)

#set executable target output path to dist
#SET(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/dist)

#set library target output path to dist
#SET(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/dist)

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}  -std=c++0x")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}  -D__GXX_EXPERIMENTAL_CXX0X__ ")
 
#add include path
INCLUDE_DIRECTORIES(${CMAKE_SOURCE_DIR}/include)

INCLUDE_DIRECTORIES(${SYSROOT_DIR}/usr/include)
INCLUDE_DIRECTORIES(${SYSROOT_DIR}/usr/include/c++/4.9.2/backward)
INCLUDE_DIRECTORIES(${SYSROOT_DIR}/usr/include/dbus-1.0/)
INCLUDE_DIRECTORIES(${SYSROOT_DIR}/usr/lib/dbus-1.0/include)

#indicate the library path for the compiler
#uncomment & modify this line on the basis of your project.
LINK_DIRECTORIES("${SYSROOT_DIR}/usr/lib")

#enumrate the source file under src folder
AUX_SOURCE_DIRECTORY(${CMAKE_SOURCE_DIR}/src/ SRC_CLIENT_LIST)

#add share library target
ADD_LIBRARY(bluetoothclient SHARED ${SRC_CLIENT_LIST})

#add static library target
#ADD_LIBRARY(${PROJECT_NAME} STATIC ${SRC_LIST})

#link the libhello.so which is under "/usr/lib" against the
#target created by ADD_XXX function.
TARGET_LINK_LIBRARIES(bluetoothclient pthread dbus-1 asound)

INSTALL(TARGETS bluetoothclient LIBRARY DESTINATION "/usr/lib/bluetooth")
INSTALL(DIRECTORY ${CMAKE_SOURCE_DIR}/include/ DESTINATION "/usr/include/bluetooth/client")
#INSTALL(DIRECTORY ${CMAKE_SOURCE_DIR}/scripts DESTINATION "/usr/bin/app" FILE_PERMISSIONS WORLD_EXECUTE WORLD_READ OWNER_EXECUTE OWNER_READ GROUP_EXECUTE GROUP_READ)
#INSTALL(FILES ${CMAKE_SOURCE_DIR}/conf/autocore.conf DESTINATION "/etc/")
#INSTALL(FILES ${CMAKE_SOURCE_DIR}/systemd/autocoreserver.service DESTINATION "/etc/systemd/system/")
#INSTALL(FILES ${CMAKE_SOURCE_DIR}/systemd/multi-user.target.wants/autocoreserver.service DESTINATION "/etc/systemd/system/multi-user.target.wants")
