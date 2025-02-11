cmake_minimum_required(VERSION 3.20)
set(PROJECT_NAME get_distance)

project(${PROJECT_NAME} C CXX ASM)


add_executable(${PROJECT_NAME})
# FILE(GLOB Sources *.cpp)
# FILE(GLOB Heasers *.h *.hpp)

target_sources(${PROJECT_NAME}
    PUBLIC
    get_distance.cpp
    Connection_information.cpp
    Connection_information.h
    # PRIVATE
    # ${Heasers}
)

find_package(urg_cpp REQUIRED)
target_link_libraries(${PROJECT_NAME} PRIVATE urg_cpp::urg_cpp)

# target_link_libraries(${PROJECT_NAME} drv_accelerometer_sensor)
# target_link_libraries(${PROJECT_NAME} inf_i2c_manager)
