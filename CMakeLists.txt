cmake_minimum_required(VERSION 3.24)

set(APP_NAME openGLHello)
project(${APP_NAME})

set(CUR_DIR .)

get_filename_component(TOP_WORK_DIR ${CUR_DIR} ABSOLUTE)

# 使用 C++ 11 标准
set(CMAKE_CXX_STANDARD 11)


# 设置编译源文件
file(GLOB_RECURSE SRC_FILES
    ${TOP_WORK_DIR}/source/*.c
    ${TOP_WORK_DIR}/source/*.cpp)

# 设置目标，为可执行文件
add_executable(${APP_NAME} ${SRC_FILES})

# 添加头文件
target_include_directories(${PROJECT_NAME}
    PRIVATE
    ${TOP_WORK_DIR}
    ${TOP_WORK_DIR}/glfw-3.3.2.bin.WIN32/include
    ${TOP_WORK_DIR}/include
)

# 添加目标链接
target_link_libraries(${PROJECT_NAME}
    PRIVATE
    ${TOP_WORK_DIR}/glfw-3.3.2.bin.WIN32/lib-mingw/libglfw3.a
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

# 链接必要的库
# target_link_libraries(${APP_NAME} PUBLIC -lX11 -lpthread -lXrandr -lXi)


###########################################################
# 如果是vulkan为api，则需要添加如下的命令并删除opengl相关的命令
## Vulkan
#find_package(Vulkan REQUIRED)
## 添加头文件
#target_include_directories(${PROJECT_NAME}
#    PRIVATE
#    Vulkan::Headers
#)
#
## 添加目标链接
#target_link_libraries(${PROJECT_NAME}
#    PRIVATE
#    Vulkan::Vulkan
#)