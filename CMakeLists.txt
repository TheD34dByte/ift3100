cmake_minimum_required(VERSION 3.31.6)
project(soup CXX)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY
    "${CMAKE_SOURCE_DIR}/bin"
)

file(MAKE_DIRECTORY "${CMAKE_RUNTIME_OUTPUT_DIRECTORY}")

find_package(OpenGL REQUIRED)
find_package(glfw3 REQUIRED)

add_executable(${PROJECT_NAME} 
    src/main.cpp
)

target_link_libraries(${PROJECT_NAME} PRIVATE
    OpenGL::GL
    glfw
)

if(MSVC)
    target_compile_options(${PROJECT_NAME} PRIVATE /W4 /WX)
else()
    target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wextra -Wpedantic -Werror)
endif()

file(GLOB_RECURSE CPP_SOURCES CONFIGURE_DEPENDS
    "${CMAKE_SOURCE_DIR}/*.cpp"
)

file(GLOB_RECURSE CPP_HEADERS CONFIGURE_DEPENDS
    "${CMAKE_SOURCE_DIR}/*.h"
)

list(FILTER CPP_SOURCES EXCLUDE REGEX "^${CMAKE_BINARY_DIR}/")
list(FILTER CPP_HEADERS EXCLUDE REGEX "^${CMAKE_BINARY_DIR}/")

add_custom_target(format
    COMMAND clang-format -i ${CPP_SOURCES} ${CPP_HEADERS}
    WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
    COMMENT "Formatting C++ sources"
)

add_custom_target(lint
    COMMAND clang-tidy -p "${CMAKE_BINARY_DIR}" ${CPP_SOURCES} --warnings-as-errors=*
    WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
    COMMENT "Running clang-tidy"
)
