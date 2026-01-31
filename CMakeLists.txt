cmake_minimum_required(VERSION 3.30)

project(RPiTelemetry C)
set(CMAKE_C_STANDARD 99)

set(SRC_DIR "${CMAKE_SOURCE_DIR}/src")
set(INCLUDE_DIR "${CMAKE_SOURCE_DIR}/include")

set(SRC
        ${SRC_DIR}/DataParsing.c
        ${SRC_DIR}/Sending.c
)

set(INCLUDE
        ${INCLUDE_DIR}/DataParsing.h
        ${INCLUDE_DIR}/Sending.h
)

add_library(core STATIC
        ${SRC}
        ${INCLUDE}
)

add_executable(RPiTelemetry main.c)

target_link_libraries(RPiTelemetry PRIVATE core)

set_target_properties(RPiTelemetry PROPERTIES
        RUNTIME_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}"
)

target_include_directories(core PUBLIC ${INCLUDE_DIR})
target_include_directories(RPiTelemetry PRIVATE ${INCLUDE_DIR})
