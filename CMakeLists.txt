cmake_minimum_required (VERSION 3.5)
set(CMAKE_C_COMPILER "/usr/bin/clang")
set(CMAKE_CXX_COMPILER "/usr/bin/clang++")
project(Cobble)
set(CMAKE_CXX_FLAGS_RELEASE "-O3")
set(CMAKE_CXX_FLAGS_DEBUG "-DDEBUG -g")
set(CMAKE_CXX_FLAGS "-Wno-deprecated")
set(CMAKE_CXX_FLAGS "-Wno-deprecated-declarations")
set(CMAKE_CXX_FLAGS "-pthread")
set(CMAKE_CXX_STANDARD 14)
set(CBBL_VERSION "0.0.1")

include_directories(include)
include_directories(vendor/cxxopts/include)
include_directories(vendor/asio/asio/include)
include_directories(vendor/Simple-Web-Server)
include_directories(vendor/variant/include)
include_directories(vendor/protozero/include)
include_directories(vendor/vtzero/include)
include_directories(vendor/mapnik-vector-tile/src)
include_directories(vendor/geometry.hpp/include)
include_directories(vendor/gzip-hpp/include)
include_directories(../mapnik/include)
link_directories(.)

set(CMAKE_BUILD_WITH_INSTALL_RPATH ON)
if(APPLE)
    # custom Boost goes before macports
    include_directories(../etc/mapnik-boost/build/include)
    include_directories(/opt/local/include)
    link_directories(../etc/mapnik-boost/build/lib)
    link_directories(/opt/local/lib)
else()
set(CMAKE_INSTALL_RPATH "$ORIGIN")
endif()

add_executable(cbbl src/cmd.cpp src/tile.cpp src/source.cpp src/sink.cpp src/serve.cpp src/batch.cpp)
target_link_libraries(cbbl mapnik icuuc sqlite3 z boost_filesystem)

add_custom_target(archive COMMAND dist/archive.sh ${CBBL_VERSION} ${CMAKE_SYSTEM_NAME})
