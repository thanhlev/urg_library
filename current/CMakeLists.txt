cmake_minimum_required(VERSION 3.20)
project(urg_cpp_lib VERSION 1.0)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

find_package(Threads REQUIRED)

add_library(urg_cpp SHARED
    src/ticks.cpp
    src/urg_connection.c
    src/urg_debug.c
    src/Urg_driver.cpp
    src/urg_ring_buffer.c
    src/urg_sensor.c
    src/urg_serial.c
    src/urg_serial_utils_linux.c
    src/urg_tcpclient.c
    src/urg_utils.c
)

target_include_directories(urg_cpp PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include/cpp>
    $<INSTALL_INTERFACE:include>
)
target_include_directories(urg_cpp PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include/c>
    $<INSTALL_INTERFACE:include>
)

install(TARGETS urg_cpp
    EXPORT urg_cpp_Targets
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
    INCLUDES DESTINATION include
)

install(DIRECTORY include/ DESTINATION include/urg_cpp)

install(EXPORT urg_cpp_Targets
    FILE urg_cpp_Targets.cmake
    NAMESPACE urg_cpp::
    DESTINATION lib/cmake/urg_cpp
)

include(CMakePackageConfigHelpers)
configure_package_config_file(${CMAKE_CURRENT_SOURCE_DIR}/Config.cmake.in
    "${CMAKE_CURRENT_BINARY_DIR}/urg_cppConfig.cmake"
    INSTALL_DESTINATION lib/cmake/urg_cpp
)

write_basic_package_version_file(
    "${CMAKE_CURRENT_BINARY_DIR}/urg_cppConfigVersion.cmake"
    VERSION ${PROJECT_VERSION}
    COMPATIBILITY SameMajorVersion
)

install(FILES
    "${CMAKE_CURRENT_BINARY_DIR}/urg_cppConfig.cmake"
    "${CMAKE_CURRENT_BINARY_DIR}/urg_cppConfigVersion.cmake"
    DESTINATION lib/cmake/urg_cpp
)
