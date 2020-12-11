cmake_minimum_required(VERSION 3.17)

set(APP_NAME openGLHello)
project(${APP_NAME})

set(CUR_DIR .)

get_filename_component(TOP_WORK_DIR ${CUR_DIR} ABSOLUTE)

# 使用 C++ 11 标准
set(CMAKE_CXX_STANDARD 11)

# 添加头文件
include_directories(
    ${TOP_WORK_DIR}
    ${TOP_WORK_DIR}/glfw-3.3.2.bin.WIN32/include
    ${TOP_WORK_DIR}/include
)

# 添加目标链接
link_libraries(${TOP_WORK_DIR}/glfw-3.3.2.bin.WIN32/lib-mingw/libglfw3.a
    opengl32.lib
)

# set debug flags
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Debug)
    message(STATUS "set CMAKE_BUILD_TYPE=" ${CMAKE_BUILD_TYPE})
endif()
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    message(STATUS "set debug option")
    add_compile_options(-g)
    set(D d)
endif()

# 设置编译源文件，执行编译命令
file(GLOB_RECURSE SRC_FILES
    ${TOP_WORK_DIR}/source/*.c
    ${TOP_WORK_DIR}/source/*.cpp)

add_executable(${APP_NAME} ${SRC_FILES})

# 链接必要的库
# target_link_libraries(${APP_NAME} PUBLIC -lGLEW -lX11 -lpthread -lXrandr -lXi)
